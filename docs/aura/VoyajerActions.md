---
layout: default
title: VoyajerActions
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerActions
## Fields
### VoyajerActionsController

```
({
  doInit: function (component, event, helper) {
    var callToParent = component.getEvent("callToParent");
    callToParent.setParam("action", "loadItineraries");
    callToParent.fire();
  },

  loadTable: function (component, event, helper) {
    var service = component.find("selectService").set("v.value", "all");
    var action = component.find("selectAction").set("v.value", "all");
    var itineraries = component.get("v.itineraries");
    component.set("v.itinerariesFiltered", itineraries);
  },
  doSaveTrace: function (cmp, event, helper) {
        // cb : add in call to parent for spinner
    var recordId = event.getSource().get("v.value");
    var itineraries = cmp.get("v.itineraries");
    var serviceId = "";
    if (!!recordId) {
      itineraries.forEach((itinerary) => {
        if (itinerary.serviceId == recordId) serviceId = itinerary.serviceId;
      });
    }

    if (!!serviceId && !!recordId) {
      cmp.set("v.optionRecordId", recordId); 
    }
    let productionId = "";
 
    var callToParent = cmp.getEvent("callToParent");
    callToParent.setParam("action", "updatingUser");
    callToParent.fire();
    console.log("saving");
    var action = cmp.get("c.submitTraceResendContract");
    productionId = cmp.get("v.productionSelected");
    console.log("service id : " + serviceId);
    console.log("production id : " + productionId);
    action.setParams({
      theProductionId: productionId,
      theServiceId: serviceId
    });
    action.setCallback(
      this,
      $A.getCallback(function (response) {
        var state = response.getState();
        var response = response.getReturnValue();
        if (state === "SUCCESS") {
          if (response){
            var callToParent = cmp.getEvent("callToParent");
            callToParent.setParam("action", "showDashboard");
            callToParent.fire();
            var callToParent2 = cmp.getEvent("callToParent");
            callToParent2.setParam("action", "contentLoaded");
            callToParent2.fire();
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "success",
              message: "Request has been sent."
            });
            toastEvent.fire();
          } else {
            var callToParent2 = cmp.getEvent("callToParent");
            callToParent2.setParam("action", "contentLoaded");
            callToParent2.fire();
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "error",
              message:
                "Something went wrong. Please refresh the page and try again."
            });
  
            toastEvent.fire();
          }

        } else {
          // Display the message
          var callToParent2 = cmp.getEvent("callToParent");
          callToParent2.setParam("action", "contentLoaded");
          callToParent2.fire();
          console.error('FATAL error...missing Contract Coordinator to assign task to');
          var toastEvent = $A.get("e.force:showToast");
          toastEvent.setParams({
            type: "error",
            message:
              "Something went wrong. Please refresh the page and try again."
          });

          toastEvent.fire();
        }

      })
    );
    $A.enqueueAction(action);
  },
  openOptions: function (component, event, helper) {
    var recordId = event.getSource().get("v.value");
    var itineraries = component.get("v.itineraries");
    var service = "";
    if (!!recordId)
      itineraries.forEach((itinerary) => {
        if (itinerary.serviceId == recordId) service = itinerary.service;
      });
    if (!!service && !!recordId) {
      component.set("v.optionRecordId", recordId);
      if (service == "lodging")
        component.set("v.mainContent", "optionsHousing");
      if (service == "ground") component.set("v.mainContent", "optionsGT");
      if (service == "air") component.set("v.mainContent", "optionsAir");
      if (service == "freight")
        component.set("v.mainContent", "optionsFreight");
    }
  },

  openCongaSign: function (component, event, helper) {
    var recordId = event.getSource().get("v.value");
    var congaSignMap = {};
    component.get("v.itineraries").forEach((itinerary) => {
      if (itinerary.serviceId == recordId)
        congaSignMap = itinerary.congaSignMap;
    });
    if (!$A.util.isEmpty(congaSignMap.bidId)) {
      window.open(
        "/apex/APXT_CongaSign__apxt_sendForSignature?id=" +
          congaSignMap.bidId +
          "&recipient1=" +
          congaSignMap.recipient1Id +
          "&recipient1role=in_person_signer" +
          (!$A.util.isEmpty(congaSignMap.recipient2Id)
            ? "&recipient2=" +
              congaSignMap.recipient2Id +
              "&recipient2role=signer"
            : "") +
          "&routingType=SERIAL&documentId=" +
          congaSignMap.documentId,
        "scrollbars=yes"
      );
    }
  },

  backToDashboard: function (component, event, helper) {
    component.set("v.productionSelected", "");
    component.set("v.mainContent", "dashboard");
  },

  handleFilter: function (component, event, helper) {
    var service = component.find("selectService").get("v.value");
    var action = component.find("selectAction").get("v.value");
    var itineraries = component.get("v.itineraries");
    var itinerariesFiltered = [];
    var addItem = false;
    itineraries.forEach((itinerary) => {
      addItem = false;
      if (service == "all") addItem = true;
      else
        addItem =
          itinerary.service.toLowerCase() == service.toLowerCase()
            ? true
            : false;
      if (addItem && action != "all")
        addItem =
          itinerary.action.toLowerCase() == action.toLowerCase() ? true : false;
      if (addItem) itinerariesFiltered.push(itinerary);
    });
    component.set("v.itinerariesFiltered", itinerariesFiltered);
  }
});
```
### VoyajerActions

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerActions

```
.THIS .page-header {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1em;
    align-items: flex-end;
}

.THIS .page-section-filters {
    align-items: center;
    display: flex;
    justify-content: flex-end;
}

.THIS .productionTitle {
    flex: 1;
    overflow: hidden;
}

.THIS .productionTitle > div,
.THIS .productionTitle h3 {
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .productionTitle h3 {
    font-size: 1.45rem;
    font-weight: 600;
}

.THIS .filterSelector {
    padding: 0 0.5em;
}

.THIS .filterSelector label {
    display: none;
}

.THIS .itineraryTable {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-width: 600px;
}

.THIS .itineraryTableHeader {
    display: flex;
    flex-direction: row;
    font-weight: 500;
    border-bottom: 1px solid #606060;
}

.THIS .itineraryTableHeader > div {
    padding: 0 0.8em 0.6em;
    width: 7em;
    text-align: center;
}

.THIS .itineraryTableHeader > div:last-child,
.THIS .itineraryTableRow > div:last-child {
    width: auto;
}

.THIS .itineraryTableBody {
    display: flex;
    flex-direction: column;
}

.THIS .itineraryTableRow {
    display: flex;
    flex-direction: row;
    width: 100%;
    align-items: center;
}

.THIS .itineraryTableRow > div {
    padding: 0.6em 0.8em;
    width: 7em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .itineraryTableRow:nth-child(odd) {
    background-color: #f7f9fe;
}

.THIS .itineraryTableHeader .itineraryLocationColumn,
.THIS .itineraryTableRow .itineraryLocationColumn {
    flex: 1;
    text-align: left;
}

.THIS .itineraryService {
    padding: 0 0.25em;
    width: 100%;
    text-align: center;
    color: #00b4ff;
}
```
### VoyajerActionsHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerActions

```
<aura:component controller="VoyajerController">
    <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
    <aura:attribute type="List" name="itineraries" />
    <aura:attribute type="List" name="itinerariesFiltered" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="productionCompany" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.itineraries}" action="{!c.loadTable}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <div class="productionTitle">
                            <div><h3>{!v.productionName}</h3></div>
                            <div>{!v.productionCompany}</div>
                        </div>
                        <div class="productionBackButton">
                            <lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.backToDashboard}" />
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <h3><i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em;"></i>Actions Needed</h3>
                    </div>
                    <div class="page-section-filters">
                        <p class="hideOnMobile" style="padding-right: 0.5em;">Filter by</p>
                        <lightning:select aura:id="selectService" name="selectService" label="" variant="label-hidden" class="filterSelector" onchange="{!c.handleFilter}">
                            <option value="all" selected="true">Select Service</option>
                            <option value="lodging">Lodging</option>
                            <option value="ground">Ground</option>
                            <option value="air">Air</option>
                            <option value="freight">Freight</option>
                        </lightning:select>
                        <lightning:select aura:id="selectAction" name="selectAction" label="" variant="label-hidden" class="filterSelector" onchange="{!c.handleFilter}">
                            <option value="all" selected="true">Select Action</option>
                            <option value="resendContract">Resend Contract</option>
                            <option value="selectOption">View Options</option>
                        </lightning:select>
                        <lightning:button label="Update" variant="brand" class="formButtonBrandLight hideOnMobile" onclick="{!c.doInit}" />
                        <lightning:buttonIcon iconName="utility:sync" variant="brand" class="formButtonBrandLight showOnMobile" onclick="{!c.doInit}" />
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section" style="overflow-x: auto;">
                        <div class="itineraryTable">
                            <div class="itineraryTableHeader">
                                <div>Service</div>
                                <div>Start Date</div>
                                <div>End Date</div>
                                <div class="itineraryLocationColumn">Location</div>
                                <div></div>
                            </div>
                            <div class="itineraryTableBody">
                                <aura:iteration items="{!v.itinerariesFiltered}" var="itinerary">
                                    <div class="itineraryTableRow">
                                        <div>
                                            <aura:if isTrue="{!itinerary.service=='lodging'}"><div class="itineraryService"><i class="fas fa-home"></i></div></aura:if>
                                            <aura:if isTrue="{!itinerary.service=='ground'}"><div class="itineraryService"><i class="fas fa-car"></i></div></aura:if>
                                            <aura:if isTrue="{!itinerary.service=='air'}"><div class="itineraryService"><i class="fas fa-plane"></i></div></aura:if>
                                            <aura:if isTrue="{!itinerary.service=='freight'}"><div class="itineraryService"><i class="fas fa-truck"></i></div></aura:if>
                                        </div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!itinerary.startDate}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!itinerary.endDate}</div>
                                        <div class="itineraryLocationColumn">{!itinerary.location}</div>
                                        <div style="text-align: center; letter-spacing: .5px;">
                                            <aura:if isTrue="{!itinerary.action=='resendContract'}">
                                                Contract sent to email, ready for signature&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                                            </aura:if>
                                            
                                            <!-- CB: Adding in resend contract logic specific to the Pending Client Signature status-->
                                            <aura:if isTrue="{!itinerary.action=='resendContract'}">
                                                <lightning:button label="Request to Resend Contract" variant="success" class="formButtonSuccess hideOnTablet" value="{!itinerary.serviceId}" onclick="{!c.doSaveTrace}" />
                                                <lightning:buttonIcon iconName="utility:advertising" variant="success" class="formButtonSuccess showOnTablet" value="{!itinerary.serviceId}" onclick="{!c.doSaveTrace}" />
                                            </aura:if>
                                            <aura:if isTrue="{!itinerary.action=='selectOption'}">
                                                <lightning:button label="View Options" variant="success" class="formButtonSuccess hideOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openOptions}" />
                                                <lightning:buttonIcon iconName="utility:trail" variant="success" class="formButtonSuccess showOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openOptions}" />
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:iteration>
                                <aura:if isTrue="{!empty(v.itinerariesFiltered)}">
                                    <div class="itineraryTableRow"><div></div><div style="text-align: left; font-style: italic; flex: 1;">No productions found.</div></div>
                                </aura:if>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerActionsController

```
({
  doInit: function (component, event, helper) {
    var callToParent = component.getEvent("callToParent");
    callToParent.setParam("action", "loadItineraries");
    callToParent.fire();
  },

  loadTable: function (component, event, helper) {
    var service = component.find("selectService").set("v.value", "all");
    var action = component.find("selectAction").set("v.value", "all");
    var itineraries = component.get("v.itineraries");
    component.set("v.itinerariesFiltered", itineraries);
  },
  doSaveTrace: function (cmp, event, helper) {
        // cb : add in call to parent for spinner
    var recordId = event.getSource().get("v.value");
    var itineraries = cmp.get("v.itineraries");
    var serviceId = "";
    if (!!recordId) {
      itineraries.forEach((itinerary) => {
        if (itinerary.serviceId == recordId) serviceId = itinerary.serviceId;
      });
    }

    if (!!serviceId && !!recordId) {
      cmp.set("v.optionRecordId", recordId); 
    }
    let productionId = "";
 
    var callToParent = cmp.getEvent("callToParent");
    callToParent.setParam("action", "updatingUser");
    callToParent.fire();
    console.log("saving");
    var action = cmp.get("c.submitTraceResendContract");
    productionId = cmp.get("v.productionSelected");
    console.log("service id : " + serviceId);
    console.log("production id : " + productionId);
    action.setParams({
      theProductionId: productionId,
      theServiceId: serviceId
    });
    action.setCallback(
      this,
      $A.getCallback(function (response) {
        var state = response.getState();
        var response = response.getReturnValue();
        if (state === "SUCCESS") {
          if (response){
            var callToParent = cmp.getEvent("callToParent");
            callToParent.setParam("action", "showDashboard");
            callToParent.fire();
            var callToParent2 = cmp.getEvent("callToParent");
            callToParent2.setParam("action", "contentLoaded");
            callToParent2.fire();
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "success",
              message: "Request has been sent."
            });
            toastEvent.fire();
          } else {
            var callToParent2 = cmp.getEvent("callToParent");
            callToParent2.setParam("action", "contentLoaded");
            callToParent2.fire();
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
              type: "error",
              message:
                "Something went wrong. Please refresh the page and try again."
            });
  
            toastEvent.fire();
          }

        } else {
          // Display the message
          var callToParent2 = cmp.getEvent("callToParent");
          callToParent2.setParam("action", "contentLoaded");
          callToParent2.fire();
          console.error('FATAL error...missing Contract Coordinator to assign task to');
          var toastEvent = $A.get("e.force:showToast");
          toastEvent.setParams({
            type: "error",
            message:
              "Something went wrong. Please refresh the page and try again."
          });

          toastEvent.fire();
        }

      })
    );
    $A.enqueueAction(action);
  },
  openOptions: function (component, event, helper) {
    var recordId = event.getSource().get("v.value");
    var itineraries = component.get("v.itineraries");
    var service = "";
    if (!!recordId)
      itineraries.forEach((itinerary) => {
        if (itinerary.serviceId == recordId) service = itinerary.service;
      });
    if (!!service && !!recordId) {
      component.set("v.optionRecordId", recordId);
      if (service == "lodging")
        component.set("v.mainContent", "optionsHousing");
      if (service == "ground") component.set("v.mainContent", "optionsGT");
      if (service == "air") component.set("v.mainContent", "optionsAir");
      if (service == "freight")
        component.set("v.mainContent", "optionsFreight");
    }
  },

  openCongaSign: function (component, event, helper) {
    var recordId = event.getSource().get("v.value");
    var congaSignMap = {};
    component.get("v.itineraries").forEach((itinerary) => {
      if (itinerary.serviceId == recordId)
        congaSignMap = itinerary.congaSignMap;
    });
    if (!$A.util.isEmpty(congaSignMap.bidId)) {
      window.open(
        "/apex/APXT_CongaSign__apxt_sendForSignature?id=" +
          congaSignMap.bidId +
          "&recipient1=" +
          congaSignMap.recipient1Id +
          "&recipient1role=in_person_signer" +
          (!$A.util.isEmpty(congaSignMap.recipient2Id)
            ? "&recipient2=" +
              congaSignMap.recipient2Id +
              "&recipient2role=signer"
            : "") +
          "&routingType=SERIAL&documentId=" +
          congaSignMap.documentId,
        "scrollbars=yes"
      );
    }
  },

  backToDashboard: function (component, event, helper) {
    component.set("v.productionSelected", "");
    component.set("v.mainContent", "dashboard");
  },

  handleFilter: function (component, event, helper) {
    var service = component.find("selectService").get("v.value");
    var action = component.find("selectAction").get("v.value");
    var itineraries = component.get("v.itineraries");
    var itinerariesFiltered = [];
    var addItem = false;
    itineraries.forEach((itinerary) => {
      addItem = false;
      if (service == "all") addItem = true;
      else
        addItem =
          itinerary.service.toLowerCase() == service.toLowerCase()
            ? true
            : false;
      if (addItem && action != "all")
        addItem =
          itinerary.action.toLowerCase() == action.toLowerCase() ? true : false;
      if (addItem) itinerariesFiltered.push(itinerary);
    });
    component.set("v.itinerariesFiltered", itinerariesFiltered);
  }
});
```
### VoyajerActions

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerActions

```
.THIS .page-header {
    display: flex;
    justify-content: flex-end;
    margin-bottom: 1em;
    align-items: flex-end;
}

.THIS .page-section-filters {
    align-items: center;
    display: flex;
    justify-content: flex-end;
}

.THIS .productionTitle {
    flex: 1;
    overflow: hidden;
}

.THIS .productionTitle > div,
.THIS .productionTitle h3 {
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .productionTitle h3 {
    font-size: 1.45rem;
    font-weight: 600;
}

.THIS .filterSelector {
    padding: 0 0.5em;
}

.THIS .filterSelector label {
    display: none;
}

.THIS .itineraryTable {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-width: 600px;
}

.THIS .itineraryTableHeader {
    display: flex;
    flex-direction: row;
    font-weight: 500;
    border-bottom: 1px solid #606060;
}

.THIS .itineraryTableHeader > div {
    padding: 0 0.8em 0.6em;
    width: 7em;
    text-align: center;
}

.THIS .itineraryTableHeader > div:last-child,
.THIS .itineraryTableRow > div:last-child {
    width: auto;
}

.THIS .itineraryTableBody {
    display: flex;
    flex-direction: column;
}

.THIS .itineraryTableRow {
    display: flex;
    flex-direction: row;
    width: 100%;
    align-items: center;
}

.THIS .itineraryTableRow > div {
    padding: 0.6em 0.8em;
    width: 7em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .itineraryTableRow:nth-child(odd) {
    background-color: #f7f9fe;
}

.THIS .itineraryTableHeader .itineraryLocationColumn,
.THIS .itineraryTableRow .itineraryLocationColumn {
    flex: 1;
    text-align: left;
}

.THIS .itineraryService {
    padding: 0 0.25em;
    width: 100%;
    text-align: center;
    color: #00b4ff;
}
```
### VoyajerActionsHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerActions

```
<aura:component controller="VoyajerController">
    <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
    <aura:attribute type="List" name="itineraries" />
    <aura:attribute type="List" name="itinerariesFiltered" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="productionCompany" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.itineraries}" action="{!c.loadTable}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <div class="productionTitle">
                            <div><h3>{!v.productionName}</h3></div>
                            <div>{!v.productionCompany}</div>
                        </div>
                        <div class="productionBackButton">
                            <lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.backToDashboard}" />
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <h3><i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em;"></i>Actions Needed</h3>
                    </div>
                    <div class="page-section-filters">
                        <p class="hideOnMobile" style="padding-right: 0.5em;">Filter by</p>
                        <lightning:select aura:id="selectService" name="selectService" label="" variant="label-hidden" class="filterSelector" onchange="{!c.handleFilter}">
                            <option value="all" selected="true">Select Service</option>
                            <option value="lodging">Lodging</option>
                            <option value="ground">Ground</option>
                            <option value="air">Air</option>
                            <option value="freight">Freight</option>
                        </lightning:select>
                        <lightning:select aura:id="selectAction" name="selectAction" label="" variant="label-hidden" class="filterSelector" onchange="{!c.handleFilter}">
                            <option value="all" selected="true">Select Action</option>
                            <option value="resendContract">Resend Contract</option>
                            <option value="selectOption">View Options</option>
                        </lightning:select>
                        <lightning:button label="Update" variant="brand" class="formButtonBrandLight hideOnMobile" onclick="{!c.doInit}" />
                        <lightning:buttonIcon iconName="utility:sync" variant="brand" class="formButtonBrandLight showOnMobile" onclick="{!c.doInit}" />
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section" style="overflow-x: auto;">
                        <div class="itineraryTable">
                            <div class="itineraryTableHeader">
                                <div>Service</div>
                                <div>Start Date</div>
                                <div>End Date</div>
                                <div class="itineraryLocationColumn">Location</div>
                                <div></div>
                            </div>
                            <div class="itineraryTableBody">
                                <aura:iteration items="{!v.itinerariesFiltered}" var="itinerary">
                                    <div class="itineraryTableRow">
                                        <div>
                                            <aura:if isTrue="{!itinerary.service=='lodging'}"><div class="itineraryService"><i class="fas fa-home"></i></div></aura:if>
                                            <aura:if isTrue="{!itinerary.service=='ground'}"><div class="itineraryService"><i class="fas fa-car"></i></div></aura:if>
                                            <aura:if isTrue="{!itinerary.service=='air'}"><div class="itineraryService"><i class="fas fa-plane"></i></div></aura:if>
                                            <aura:if isTrue="{!itinerary.service=='freight'}"><div class="itineraryService"><i class="fas fa-truck"></i></div></aura:if>
                                        </div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!itinerary.startDate}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!itinerary.endDate}</div>
                                        <div class="itineraryLocationColumn">{!itinerary.location}</div>
                                        <div style="text-align: center; letter-spacing: .5px;">
                                            <aura:if isTrue="{!itinerary.action=='resendContract'}">
                                                Contract sent to email, ready for signature&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
                                            </aura:if>
                                            
                                            <!-- CB: Adding in resend contract logic specific to the Pending Client Signature status-->
                                            <aura:if isTrue="{!itinerary.action=='resendContract'}">
                                                <lightning:button label="Request to Resend Contract" variant="success" class="formButtonSuccess hideOnTablet" value="{!itinerary.serviceId}" onclick="{!c.doSaveTrace}" />
                                                <lightning:buttonIcon iconName="utility:advertising" variant="success" class="formButtonSuccess showOnTablet" value="{!itinerary.serviceId}" onclick="{!c.doSaveTrace}" />
                                            </aura:if>
                                            <aura:if isTrue="{!itinerary.action=='selectOption'}">
                                                <lightning:button label="View Options" variant="success" class="formButtonSuccess hideOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openOptions}" />
                                                <lightning:buttonIcon iconName="utility:trail" variant="success" class="formButtonSuccess showOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openOptions}" />
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:iteration>
                                <aura:if isTrue="{!empty(v.itinerariesFiltered)}">
                                    <div class="itineraryTableRow"><div></div><div style="text-align: left; font-style: italic; flex: 1;">No productions found.</div></div>
                                </aura:if>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```

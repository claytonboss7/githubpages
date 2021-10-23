---
layout: default
title: VoyajerVendorActions
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerVendorActions
## Fields
### VoyajerVendorActions

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorActions

```
<aura:component >
    <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
    <aura:attribute type="List" name="itineraries" />
    <aura:attribute type="List" name="itinerariesFiltered" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="serviceId" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="productionCompany" />
    <aura:attribute type="String" name="productionAssocUserName" />
    <aura:attribute type="String" name="productionAssocUserPhone" />
    <aura:attribute type="String" name="productionAssocUserEmail" />
    <aura:attribute type="String" name="productionAssocRole" />
    
    <!--component -->
    <aura:attribute type="String" name="bidRecordId" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.itineraries}" action="{!c.loadTable}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <aura:iteration items="{!v.itinerariesFiltered}" var="itinerary" end="1">
                    <div class="page-section">
                        <div class="page-header">
                            <div class="productionTitle">
                                <div><h3>{!v.productionName}</h3></div>
                                <div>{!v.productionCompany}</div>
                                <div style="font-weight:bold;color:#00b4ff;">{!itinerary.location}</div>
                                <div style="font-weight:bold;color:#00b4ff;">{!itinerary.startDate} - {!itinerary.endDate}</div>
                            </div>
                            <div>
                        		<div class="slds-text-align_right slds-m-bottom_x-small">
                                    <lightning:button label="Back" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backToDashboard}"/>
                                </div>
                                <div class="productionCoordinatorInfo" style="color: #fff;background-color: #0065ff;font-weight: 700;">
                                    <i class="fas fa-comments" style="margin-right: 0.5em;"></i>Need assistance?
                                </div>
                                <div class="productionCoordinatorInfo" style="font-weight: 700;">
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocUserName != null}">
                                        	{!v.productionAssocUserName}
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocRole != null}">
                                            {!v.productionAssocRole}
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocUserPhone != null}">
                                        	<i class="fas fa-phone-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserPhone}
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocUserEmail != null}">
                                            <i class="far fa-envelope" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserEmail}
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                        <div class="page-section">
                            <h3><i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em;"></i>Actions Needed</h3>
                        </div>
                    </div>
                    <div class="pageContentDashboard">
                        <div class="page-section" style="overflow-x: auto;">
                            <div class="itineraryTable">
                                <div class="itineraryTableHeader">
                                    <!--<div>Start Date</div>
                                    <div>End Date</div>
                                    <div class="itineraryLocationColumn">Location</div>-->
                                    <div class="itineraryLocationColumn">Please complete the following actions</div>
                                    <div></div>
                                </div>
                                <div class="itineraryTableBody">
                                    <aura:iteration items="{!v.itinerariesFiltered}" var="itinerary">
                                        <div class="itineraryTableRow">
                                            <!--<div style="text-align: center; letter-spacing: 1px;">{!itinerary.startDate}</div>
                                            <div style="text-align: center; letter-spacing: 1px;">{!itinerary.endDate}</div>
                                            <div class="itineraryLocationColumn">{!itinerary.location}</div>-->
                                            <div class="itineraryLocationColumn">
                                                <aura:if isTrue="{!itinerary.action=='enterOption'}">
                                                    Submit your best bid for this stay.
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='housingCloseOut'}">
                                                    Please submit your close out report.
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='signOption'}">
                                                    Your contract is ready for you to sign.
                                                </aura:if>
                                            </div>
                                            <div>
                                                <aura:if isTrue="{!itinerary.action=='enterOption'}">
                                                    <lightning:button label="Enter Bid" variant="success" class="formButtonSuccess hideOnTablet csBtnWidth1" value="{!itinerary.serviceId}" onclick="{!c.openEnterBid}" />
                                                    <lightning:buttonIcon iconName="utility:trail" variant="success" class="formButtonSuccess showOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openEnterBid}" />
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='housingCloseOut'}">
                                                    <lightning:button label="Close Out" variant="success" class="formButtonSuccess hideOnTablet csBtnWidth1" value="{!itinerary.serviceId}" onclick="{!c.openHousingCloseOut}" />
                                                    <lightning:buttonIcon iconName="utility:trail" variant="success" class="formButtonSuccess showOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openHousingCloseOut}" />
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='signOption'}">
                                                    <lightning:button label="Sign Contract" variant="success" class="formButtonSuccess hideOnTablet csBtnWidth1" value="{!itinerary.serviceId}" onclick="{!c.openCongaSign}" />
                                                    <lightning:buttonIcon iconName="utility:advertising" variant="destructive" class="formButtonSuccess showOnTablet" value="{!itinerary.serviceId}" onclick="{!c.openCongaSign}" />
                                                </aura:if>
                                            </div>
                                        </div>
                                    </aura:iteration>
                                    <!--<aura:if isTrue="{!empty(v.itinerariesFiltered)}">
                                        <div class="itineraryTableRow"><div></div><div style="text-align: left; font-style: italic; flex: 1;">No bids found.</div></div>
                                    </aura:if>-->
                                </div>
                            </div>
                        </div>
                    </div>
                </aura:iteration>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerVendorActions

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

.THIS .csBtnWidth1 {
    width: 150px;
}

.THIS .productionCoordinatorInfo {
    padding: 10px 20px;
    background-color: #fff;
}
```
### VoyajerVendorActionsController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorProductionBids");
        callToParent.fire();
	},
    
    loadTable : function(component, event, helper) {
        var itineraries = component.get("v.itineraries");
        component.set("v.itinerariesFiltered",itineraries);
    },
    
    openEnterBid : function(component, event, helper) {
        console.log("openEnterBid()");
        var recordId = event.getSource().get("v.value");
        var itineraries = component.get("v.itineraries");
        var service = '';
        if(!!recordId) itineraries.forEach(itinerary => { if(itinerary.serviceId == recordId) service = itinerary.service; });
        console.log("# service = " + service);
        console.log("# recordId = " + recordId);
        if(!!service && !!recordId) {
            component.set("v.optionRecordId",recordId);
            if(service == 'Housing Bid') component.set("v.mainContent","bidVendorHousing");
            if(service == 'GT Bid') component.set("v.mainContent","bidVendorGround");
            //if(service == 'air') component.set("v.mainContent","bidVendorAir");
            //if(service == 'Freight Bid') component.set("v.mainContent","bidVendorFreight");
        }
    },
    
    openHousingCloseOut : function(component, event, helper) {
        console.log("openHousingCloseOut");
        var serviceId = event.getSource().get("v.value");
        var itineraries = component.get("v.itineraries");
        var service = '';
        if(!!serviceId) itineraries.forEach(itinerary => { if(itinerary.serviceId == serviceId) service = itinerary.service; });
        if(!!service && !!serviceId) {
            component.set("v.serviceId",serviceId);
            if(service == 'Housing Bid') component.set("v.mainContent","closeOutHousing");
            //if(service == 'GT Bid') component.set("v.mainContent","bidVendorGround");
            //if(service == 'air') component.set("v.mainContent","optionsAir");
            //if(service == 'Freight Bid') component.set("v.mainContent","optionsFreight");
        }
    },

    openCongaSign : function(component, event, helper) {
        var congaSignMap = {};
        component.get("v.itineraries").forEach(itinerary => { if(itinerary.action == "signOption") congaSignMap = itinerary.congaSignMap; });
        if(!$A.util.isEmpty(congaSignMap.bidId)){
            window.open('/apex/APXT_CongaSign__apxt_sendForSignature?id=' + congaSignMap.bidId + '&recipient1=' + congaSignMap.recipient1Id + '&recipient1role=in_person_signer' + (!$A.util.isEmpty(congaSignMap.recipient2Id) ? '&recipient2=' + congaSignMap.recipient2Id + '&recipient2role=signer' : '') + '&routingType=SERIAL&documentId=' + congaSignMap.documentId, 'scrollbars=yes');
        }
    },
    
    backToDashboard : function(component, event, helper) {
        component.set("v.mainContent","dashboardBids");
    }
})
```
### VoyajerVendorActions

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorActions

```
<aura:component >
    <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
    <aura:attribute type="List" name="itineraries" />
    <aura:attribute type="List" name="itinerariesFiltered" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="serviceId" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="productionCompany" />
    <aura:attribute type="String" name="productionAssocUserName" />
    <aura:attribute type="String" name="productionAssocUserPhone" />
    <aura:attribute type="String" name="productionAssocUserEmail" />
    <aura:attribute type="String" name="productionAssocRole" />
    
    <!--component -->
    <aura:attribute type="String" name="bidRecordId" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.itineraries}" action="{!c.loadTable}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <aura:iteration items="{!v.itinerariesFiltered}" var="itinerary" end="1">
                    <div class="page-section">
                        <div class="page-header">
                            <div class="productionTitle">
                                <div><h3>{!v.productionName}</h3></div>
                                <div>{!v.productionCompany}</div>
                                <div style="font-weight:bold;color:#00b4ff;">{!itinerary.location}</div>
                                <div style="font-weight:bold;color:#00b4ff;">{!itinerary.startDate} - {!itinerary.endDate}</div>
                            </div>
                            <div>
                        		<div class="slds-text-align_right slds-m-bottom_x-small">
                                    <lightning:button label="Back" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backToDashboard}"/>
                                </div>
                                <div class="productionCoordinatorInfo" style="color: #fff;background-color: #0065ff;font-weight: 700;">
                                    <i class="fas fa-comments" style="margin-right: 0.5em;"></i>Need assistance?
                                </div>
                                <div class="productionCoordinatorInfo" style="font-weight: 700;">
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocUserName != null}">
                                        	{!v.productionAssocUserName}
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocRole != null}">
                                            {!v.productionAssocRole}
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocUserPhone != null}">
                                        	<i class="fas fa-phone-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserPhone}
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.productionAssocUserEmail != null}">
                                            <i class="far fa-envelope" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserEmail}
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                        <div class="page-section">
                            <h3><i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em;"></i>Actions Needed</h3>
                        </div>
                    </div>
                    <div class="pageContentDashboard">
                        <div class="page-section" style="overflow-x: auto;">
                            <div class="itineraryTable">
                                <div class="itineraryTableHeader">
                                    <!--<div>Start Date</div>
                                    <div>End Date</div>
                                    <div class="itineraryLocationColumn">Location</div>-->
                                    <div class="itineraryLocationColumn">Please complete the following actions</div>
                                    <div></div>
                                </div>
                                <div class="itineraryTableBody">
                                    <aura:iteration items="{!v.itinerariesFiltered}" var="itinerary">
                                        <div class="itineraryTableRow">
                                            <!--<div style="text-align: center; letter-spacing: 1px;">{!itinerary.startDate}</div>
                                            <div style="text-align: center; letter-spacing: 1px;">{!itinerary.endDate}</div>
                                            <div class="itineraryLocationColumn">{!itinerary.location}</div>-->
                                            <div class="itineraryLocationColumn">
                                                <aura:if isTrue="{!itinerary.action=='enterOption'}">
                                                    Submit your best bid for this stay.
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='housingCloseOut'}">
                                                    Please submit your close out report.
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='signOption'}">
                                                    Your contract is ready for you to sign.
                                                </aura:if>
                                            </div>
                                            <div>
                                                <aura:if isTrue="{!itinerary.action=='enterOption'}">
                                                    <lightning:button label="Enter Bid" variant="success" class="formButtonSuccess hideOnTablet csBtnWidth1" value="{!itinerary.serviceId}" onclick="{!c.openEnterBid}" />
                                                    <lightning:buttonIcon iconName="utility:trail" variant="success" class="formButtonSuccess showOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openEnterBid}" />
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='housingCloseOut'}">
                                                    <lightning:button label="Close Out" variant="success" class="formButtonSuccess hideOnTablet csBtnWidth1" value="{!itinerary.serviceId}" onclick="{!c.openHousingCloseOut}" />
                                                    <lightning:buttonIcon iconName="utility:trail" variant="success" class="formButtonSuccess showOnMobile" value="{!itinerary.serviceId}" onclick="{!c.openHousingCloseOut}" />
                                                </aura:if>
                                                <aura:if isTrue="{!itinerary.action=='signOption'}">
                                                    <lightning:button label="Sign Contract" variant="success" class="formButtonSuccess hideOnTablet csBtnWidth1" value="{!itinerary.serviceId}" onclick="{!c.openCongaSign}" />
                                                    <lightning:buttonIcon iconName="utility:advertising" variant="destructive" class="formButtonSuccess showOnTablet" value="{!itinerary.serviceId}" onclick="{!c.openCongaSign}" />
                                                </aura:if>
                                            </div>
                                        </div>
                                    </aura:iteration>
                                    <!--<aura:if isTrue="{!empty(v.itinerariesFiltered)}">
                                        <div class="itineraryTableRow"><div></div><div style="text-align: left; font-style: italic; flex: 1;">No bids found.</div></div>
                                    </aura:if>-->
                                </div>
                            </div>
                        </div>
                    </div>
                </aura:iteration>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerVendorActions

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

.THIS .csBtnWidth1 {
    width: 150px;
}

.THIS .productionCoordinatorInfo {
    padding: 10px 20px;
    background-color: #fff;
}
```
### VoyajerVendorActionsController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorProductionBids");
        callToParent.fire();
	},
    
    loadTable : function(component, event, helper) {
        var itineraries = component.get("v.itineraries");
        component.set("v.itinerariesFiltered",itineraries);
    },
    
    openEnterBid : function(component, event, helper) {
        console.log("openEnterBid()");
        var recordId = event.getSource().get("v.value");
        var itineraries = component.get("v.itineraries");
        var service = '';
        if(!!recordId) itineraries.forEach(itinerary => { if(itinerary.serviceId == recordId) service = itinerary.service; });
        console.log("# service = " + service);
        console.log("# recordId = " + recordId);
        if(!!service && !!recordId) {
            component.set("v.optionRecordId",recordId);
            if(service == 'Housing Bid') component.set("v.mainContent","bidVendorHousing");
            if(service == 'GT Bid') component.set("v.mainContent","bidVendorGround");
            //if(service == 'air') component.set("v.mainContent","bidVendorAir");
            //if(service == 'Freight Bid') component.set("v.mainContent","bidVendorFreight");
        }
    },
    
    openHousingCloseOut : function(component, event, helper) {
        console.log("openHousingCloseOut");
        var serviceId = event.getSource().get("v.value");
        var itineraries = component.get("v.itineraries");
        var service = '';
        if(!!serviceId) itineraries.forEach(itinerary => { if(itinerary.serviceId == serviceId) service = itinerary.service; });
        if(!!service && !!serviceId) {
            component.set("v.serviceId",serviceId);
            if(service == 'Housing Bid') component.set("v.mainContent","closeOutHousing");
            //if(service == 'GT Bid') component.set("v.mainContent","bidVendorGround");
            //if(service == 'air') component.set("v.mainContent","optionsAir");
            //if(service == 'Freight Bid') component.set("v.mainContent","optionsFreight");
        }
    },

    openCongaSign : function(component, event, helper) {
        var congaSignMap = {};
        component.get("v.itineraries").forEach(itinerary => { if(itinerary.action == "signOption") congaSignMap = itinerary.congaSignMap; });
        if(!$A.util.isEmpty(congaSignMap.bidId)){
            window.open('/apex/APXT_CongaSign__apxt_sendForSignature?id=' + congaSignMap.bidId + '&recipient1=' + congaSignMap.recipient1Id + '&recipient1role=in_person_signer' + (!$A.util.isEmpty(congaSignMap.recipient2Id) ? '&recipient2=' + congaSignMap.recipient2Id + '&recipient2role=signer' : '') + '&routingType=SERIAL&documentId=' + congaSignMap.documentId, 'scrollbars=yes');
        }
    },
    
    backToDashboard : function(component, event, helper) {
        component.set("v.mainContent","dashboardBids");
    }
})
```

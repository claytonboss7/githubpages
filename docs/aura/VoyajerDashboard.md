---
layout: default
title: VoyajerDashboard
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerDashboard
## Fields
### VoyajerDashboard

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerDashboardController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadProductions");
        callToParent.fire();
	},
    
    loadTable : function(component, event, helper) {
        /**Fix By Clay Dev 2 April, 2021 #177403104
        component.set("v.filterStatus","View all");**/
        var filterStatus = "Active";
        component.set("v.filterStatus",filterStatus);
        component.set("v.startDateBegin","");
        component.set("v.startDateEnd","");
        var productions = component.get("v.productions");
        var productionsOnAlert = 0;
        productions.forEach(production => { if(production.isMissingAction) productionsOnAlert++ });
        if(productionsOnAlert > 1) component.set("v.dashboardPillMessage","You have "+productionsOnAlert+" productions with an action needed.");
        else if(productionsOnAlert == 1) component.set("v.dashboardPillMessage","You have 1 production with an action needed.");
        else component.set("v.isDashboardPillRead",true);
        component.set("v.productionsFiltered",productions);
        
        //sort..
        /**Fix By Clay Dev 2 April, 2021 #177403104
        var productionsSorted = helper.sortMethod(component);
        component.set("v.productionsFiltered", productionsSorted);**/
        
        productions = helper.sortMethod(component);
        var productionsFiltered = [];
        productions.forEach(production => { 
            if(production.status.toLowerCase() == filterStatus.toLowerCase()) 
            productionsFiltered.push(production) 
        });
        component.set("v.productionsFiltered", productionsFiltered);
    },
    
    handleRemoveDashboardPill : function(component, event, helper) {
        component.set("v.isDashboardPillRead",true);
    },    
    handleShowMessages : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","showMessages");
        callToParent.fire();    
    },
    handleNewProduction : function(component, event, helper) {
        component.set("v.mainContent","newProduction");
    },
    
    handleFilter : function(component, event, helper) {
        var filterStatus = "";
        var sourceName = event.getSource().get("v.name");
        if(sourceName.localeCompare("startDateBegin") !== 0 && sourceName.localeCompare("startDateEnd") !== 0) filterStatus = event.getSource().get("v.value");
        else filterStatus = component.get("v.filterStatus");
        var productions = component.get("v.productions");
        var productionsFiltered = [];
        if(filterStatus != "View all") productions.forEach(production => { if(production.status.toLowerCase() == filterStatus.toLowerCase()) productionsFiltered.push(production) });
        else productionsFiltered = productions.slice(0);
        component.set("v.filterStatus",filterStatus);
        var validExpense = component.find('startDateRange').reduce(function (validSoFar, inputComponent) {
            // Displays error messages for invalid fields
            inputComponent.showHelpMessageIfInvalid();
            return validSoFar && inputComponent.get('v.validity').valid;
        }, true);
        // If we pass error checking, do some real work
        if(validExpense) {
            var productionsFilteredByDate = [];
            var startDateBegin = component.get("v.startDateBegin");
            var startDateEnd = component.get("v.startDateEnd");
            if(startDateBegin && startDateEnd) {
                productionsFiltered.forEach(production => { if(production.hasOwnProperty("comparisonDate") && new Date(production.comparisonDate) >= new Date(startDateBegin)  && new Date(production.comparisonDate) <= new Date(startDateEnd)) productionsFilteredByDate.push(production) });
            } else if(startDateBegin) {
                productionsFiltered.forEach(production => { if(production.hasOwnProperty("comparisonDate") && new Date(production.comparisonDate) >= new Date(startDateBegin)) productionsFilteredByDate.push(production) });
            } else if(startDateEnd) {
                productionsFiltered.forEach(production => { if(production.hasOwnProperty("comparisonDate") && new Date(production.comparisonDate) <= new Date(startDateEnd)) productionsFilteredByDate.push(production) });
            } else {
                productionsFilteredByDate = productionsFiltered.slice(0);
            }
            productionsFiltered = productionsFilteredByDate.slice(0);
        }
        component.set("v.productionsFiltered",productionsFiltered);
        
        //sort..
        var productionsSorted = helper.sortMethod(component);
        component.set("v.productionsFiltered", productionsSorted);
    },
    
    handleSort : function(component, event, helper) {
        var productionsSorted = helper.sortMethod(component);
        component.set("v.productionsFiltered", productionsSorted);
        //console.log('#productionsSorted = ' + JSON.stringify(productionsSorted));
    },
    
    openViewActions : function(component, event, helper) {
        component.set("v.productionSelected",event.getSource().get("v.value"));
        
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadContactUsData");
        callToParent.fire();
        component.set("v.mainContent","actions");
    },
    
    openEnterItinerary : function(component, event, helper) {
        component.set("v.productionSelected",event.getSource().get("v.value"));
        
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadContactUsData");
        callToParent.fire();
        component.set("v.mainContent","itinerary");
    },
    
    openItineraryOverview : function(component, event, helper) {
        var productionSelected = event.getSource().get("v.value");
        var productionName = "";
        var productionsFiltered = component.get("v.productionsFiltered");
        productionsFiltered.forEach(production => { if(production.recordId == productionSelected) productionName = production.name });
        component.set("v.productionName",productionName);
        component.set("v.productionSelected",productionSelected);
        
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadContactUsData");
        callToParent.fire();
        component.set("v.mainContent","overview");
    }
})
```
### VoyajerDashboardHelper

```
({
	sortMethod : function(component) {
        //console.log('# sortMethod');
        var productions = component.get("v.productionsFiltered");
        var sortValue = component.find("sortBy").get("v.value");
        
		if(sortValue == 'productionNameAsc'){
            //console.log('# productionNameAsc');
        	productions.sort((a, b) => a.name.localeCompare(b.name));
        }else if(sortValue == 'startDateAsc'){
            //console.log('# startDateAsc');
            productions.sort((a, b) => new Date(a.startDate) - new Date(b.startDate));
        }else if(sortValue == 'startDateDesc'){
            //console.log('# startDateDesc');
            productions.sort((a, b) => new Date(b.startDate) - new Date(a.startDate));
        }else if(sortValue == 'endDateAsc'){
            //console.log('# endDateAsc');
            productions.sort((a, b) => new Date(a.endDate) - new Date(b.endDate));
        }else if(sortValue == 'endDateDesc'){
            //console.log('# endDateDesc');
            productions.sort((a, b) => new Date(b.endDate) - new Date(a.endDate));
        }else if(sortValue == 'statusAsc'){
            //console.log('# statusAsc');
            productions.sort((a, b) => a.status.localeCompare(b.status));
        }
        
        //result
        return productions;
	}
})
```
### VoyajerDashboard

```
.THIS .startDateContainer {
    align-items: center;
    display: flex;
    border: 1px solid #dbdbdb;
    border-radius: 2em;
    padding: 0 0.75em;
    margin-right: 0.25em;
    max-width: 17rem;
}

.THIS .filterButtons {
    display: flex;
    width: 100%;
    justify-content: flex-start;
}

.THIS .formField {
    width: auto;
    margin-bottom: 0;
}

.THIS .startDateContainer .slds-input__icon {
    display: none;
}

.THIS .startDateInput .slds-input {
    padding: 0 0.25em;
    max-width: calc(8rem + 2px);
    text-align: center;
    border-width: 0;
}

.THIS .productionTable {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-width: 900px;
}

.THIS .productionTableHeader {
    display: flex;
    flex-direction: row;
    font-weight: 500;
    border-bottom: 1px solid #606060;
}

.THIS .productionTableHeader > div {
    padding: 0 0.8em 0.6em;
    width: 7em;
}

.THIS .productionTableHeader > div:nth-child(2) {
    /*flex: 1;*/
    flex: 2;
    width: auto;
}

.THIS .productionTableHeader > div:last-child {
    flex: 3;
    width: auto;
}

.THIS .productionTableBody {
    display: flex;
    flex-direction: column;
}

.THIS .productionTableRow {
    display: flex;
    flex-direction: row;
    width: 100%;
    align-items: center;
}

.THIS .productionTableRow > div {
    padding: 0.6em 0.8em;
    width: 7em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .productionTableRow:nth-child(odd) {
    background-color: #f7f9fe;
}

.THIS .productionTableRow:not(:first-child) {
    border-top: 1px solid #dbdbdb;
}

.THIS .productionTableHeader > div:first-child,
.THIS .productionTableRow > div:first-child {
    text-align: center;
    width: 2.75em;
}

.THIS .productionTableRow > div:first-child svg {
    fill: #e00000
}

.THIS .productionTableRow > div:nth-child(2) {
    /*flex: 1;*/
    flex: 2;
    width: auto;
}

.THIS .productionTableRow > div:last-child {
    flex: 3;
    text-align: right;
    width: auto;
}

.THIS .productionTableHeader .productionServicesColumn,
.THIS .productionTableRow .productionServicesColumn {
    display: flex;
    width: 8em;
}

.THIS .productionTableHeader .productionCompanyColumn,
.THIS .productionTableRow .productionCompanyColumn {
    width: 12em;
}

.THIS .productionService {
    padding: 0 0.25em;
}

.THIS .formField {
    margin-bottom: 0;
}

.THIS .updateColumn {
    align-items: center;
    justify-content: flex-end;
    align-items: flex-start;
    justify-content: flex-start;
}

@media (max-width: 1200px) {
    .THIS .productionTableHeader > div:last-child,
    .THIS .productionTableRow > div:last-child {
        flex: none;
        width: 11em;
    }
}

@media (max-width: 1024px) {
    .THIS .startDateInput {
        /*max-width: 11em;*/
    }
}

@media (max-width: 550px) {
    .THIS .startDateContainer {
        flex-wrap: wrap;
        width: 100%;
        margin: 0;
    }
    
    .THIS .filterButtons {
        justify-content: space-between;
    }
    
    .THIS .startDateInput {
        /*max-width: 9em;*/
    }
}

/*util*/
.THIS .label-hidden > label {
    display: none;
}
```
### VoyajerDashboard

```
<aura:component>
  <aura:attribute
    type="User"
    name="userLogged"
    default="{'sobjectType' : 'User'}"
  />
  <aura:attribute type="String" name="communityNote" default="" />
  <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
  <aura:attribute type="List" name="productions" />
  <aura:attribute type="List" name="productionsFiltered" />
  <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
  <aura:attribute type="String" name="mainContent" />
  <!--Fix By Clay Dev 2 April, 2021 #177403104
  <aura:attribute type="String" name="filterStatus" default="View all" />-->
  <aura:attribute type="String" name="filterStatus" default="Active" />
  <aura:attribute
    type="String"
    name="dashboardPillMessage"
    default="You have 1 production with an action needed."
  />
  <aura:attribute type="String" name="startDateBegin" default="" />
  <aura:attribute type="String" name="startDateEnd" default="" />
  <aura:attribute type="String" name="officePreference" />
  <aura:attribute type="String" name="productionSelected" />
  <aura:attribute type="String" name="productionName" />

  <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
  <aura:handler
    name="change"
    value="{!v.productions}"
    action="{!c.loadTable}"
  />
  <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

  <div>
    <div class="pageContent">
      <div class="pageContentSpaces">
        <div class="page-section">
          <div class="page-header">
            <h1><span>{!v.userLogged.Contact.Account.Name}</span></h1>
          </div>
        </div>
        <aura:if isTrue="{!not(v.isDashboardPillRead)}">
          <div class="pageContentDashboard" style="margin-bottom: 2em">
            <lightning:pill
              label="{!v.dashboardPillMessage}"
              onremove="{!c.handleRemoveDashboardPill}"
              class="dashboardPill"
            >
              <aura:set attribute="media"
                ><i class="fas fa-bell" style="margin-right: 0.5em"></i
              ></aura:set>
            </lightning:pill>
          </div>
        </aura:if>
        <div style="margin-bottom: 1em; text-align: right">
          <lightning:button
            label="Create new production"
            variant="brand"
            iconName="utility:add"
            iconPosition="left"
            class="formButtonBrandLight"
            onclick="{!c.handleNewProduction}"
          />
        </div>
        <div
          class="pageContentDashboard"
          style="border-bottom: 1px solid #dbdbdb"
        >
          <div class="page-section">
            <h3>
              <i
                class="far fa-star"
                style="color: #9f9f9f; margin-right: 0.5em"
              ></i
              >Productions
            </h3>
          </div>
          <div class="page-section-buttons">
            <div style="flex: 1">
              <div
                class="formColumnThreeChilds"
                style="justify-content: space-between"
              >
                <div
                  class="formField"
                  style="display: flex; align-items: flex-end"
                >
                  <div class="formField filterButtons">
                    <lightning:button
                      label="Active"
                      name="Active"
                      variant="{!if(v.filterStatus=='Active','brand','neutral')}"
                      class="{!if(v.filterStatus=='Active','formButtonBrand','')}"
                      value="Active"
                      onclick="{!c.handleFilter}"
                    />
                    <lightning:button
                      label="Historic"
                      name="Historic"
                      variant="{!if(v.filterStatus=='Historic','brand','neutral')}"
                      class="{!if(v.filterStatus=='Historic','formButtonBrand','')}"
                      value="Historic"
                      onclick="{!c.handleFilter}"
                    />
                    <lightning:button
                      label="View all"
                      name="View all"
                      variant="{!if(v.filterStatus=='View all','brand','neutral')}"
                      class="{!if(v.filterStatus=='View all','formButtonBrand','')}"
                      value="View all"
                      onclick="{!c.handleFilter}"
                    />
                    <lightning:buttonIcon
                      iconName="utility:sync"
                      variant="brand"
                      class="formButtonBrandLight showOnMobile"
                      onclick="{!c.doInit}"
                    />
                  </div>
                </div>
                <div class="formField">
                  <label class="hideOnMobile">Sort by</label>
                  <lightning:select
                    label="Sort"
                    aura:id="sortBy"
                    variant="label-hidden"
                    class="slds-form-element-filter label-hidden"
                    onchange="{!c.handleSort}"
                  >
                    <option value="productionNameAsc" selected="true">
                      Production Name (A-Z)
                    </option>
                    <option value="startDateAsc">Start Date (Asc)</option>
                    <option value="startDateDesc">Start Date (Desc)</option>
                    <option value="endDateAsc">End Date (Asc)</option>
                    <option value="endDateDesc">End Date (Desc)</option>
                    <option value="statusAsc">Status (A-Z)</option>
                  </lightning:select>
                </div>
                <div
                  class="formField"
                  style="margin-bottom: 0; flex-direction: column"
                >
                  <label class="hideOnMobile">Filter by Start Date</label>
                  <div class="startDateContainer">
                    <div style="padding-right: 0.5em">
                      <lightning:icon
                        iconName="utility:date_input"
                        alternativeText="Connected"
                        size="x-small"
                      />
                    </div>
                    <div class="formField" style="margin-bottom: 0">
                      <lightning:input
                        aura:id="startDateRange"
                        class="startDateInput"
                        name="startDateBegin"
                        type="date"
                        label=""
                        variant="label-hidden"
                        dateStyle="short"
                        placeholder="{!if(v.officePreference=='RRE','dd-mm-yyyy','mm/dd/yyyy')}"
                        max="{!v.startDateEnd}"
                        value="{!v.startDateBegin}"
                        onchange="{!c.handleFilter}"
                        autocomplete="off"
                      />
                    </div>
                    <div style="padding: 0 0.5em">
                      {!if(v.officePreference=='RRE',' / ',' - ')}
                    </div>
                    <div class="formField" style="margin-bottom: 0">
                      <lightning:input
                        aura:id="startDateRange"
                        class="startDateInput"
                        name="startDateEnd"
                        type="date"
                        label=""
                        variant="label-hidden"
                        dateStyle="short"
                        placeholder="{!if(v.officePreference=='RRE','dd-mm-yyyy','mm/dd/yyyy')}"
                        min="{!v.startDateBegin}"
                        value="{!v.startDateEnd}"
                        onchange="{!c.handleFilter}"
                        autocomplete="off"
                      />
                    </div>
                  </div>
                </div>
                <div
                  class="formField hideOnMobile"
                  style="display: flex; align-items: flex-end"
                >
                  <div class="formField">
                    <lightning:button
                      label="Update"
                      variant="brand"
                      class="formButtonBrandLight hideOnMobile"
                      onclick="{!c.doInit}"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="pageContentDashboard">
          <div class="page-section" style="overflow-x: auto">
            <div class="productionTable">
              <div class="productionTableHeader">
                <div></div>
                <div>Production Name</div>
                <div>Start Date</div>
                <div>End Date</div>
                <!--<div class="productionCompanyColumn">Company</div>-->
                <div class="productionServicesColumn">Services</div>
                <div>Status</div>
                <div></div>
              </div>
              <div class="productionTableBody">
                <aura:iteration
                  items="{!v.productionsFiltered}"
                  var="production"
                >
                  <div class="productionTableRow">
                    <div style="color: #e00000">
                      <aura:if isTrue="{!production.isMissingAction}"
                        ><lightning:icon
                          iconName="utility:notification"
                          variant="error"
                          size="xx-small"
                      /></aura:if>
                    </div>
                    <div>{!production.name}</div>
                    <div style="text-align: center; letter-spacing: 1px">
                      {!production.startDate}
                    </div>
                    <div style="text-align: center; letter-spacing: 1px">
                      {!production.endDate}
                    </div>
                    <!--<div class="productionCompanyColumn">{!production.company}</div>-->
                    <div
                      class="productionServicesColumn"
                      style="color: #00b4ff"
                    >
                      <aura:if isTrue="{!production.haveServiceHousing}"
                        ><div class="productionService">
                          <i class="fas fa-home"></i></div
                      ></aura:if>
                      <aura:if isTrue="{!production.haveServiceGround}"
                        ><div class="productionService">
                          <i class="fas fa-car"></i></div
                      ></aura:if>
                      <aura:if isTrue="{!production.haveServiceAir}"
                        ><div class="productionService">
                          <i class="fas fa-plane"></i></div
                      ></aura:if>
                      <aura:if isTrue="{!production.haveServiceFreight}"
                        ><div class="productionService">
                          <i class="fas fa-truck"></i></div
                      ></aura:if>
                    </div>
                    <div>{!production.status}</div>
                    <div>
                        <aura:if isTrue="{!production.isMissingAction}">
                        <lightning:button
                          label="Action Needed"
                          variant="destructive"
                          class="formButtonDestructive hideOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openViewActions}"
                        />
                        <lightning:buttonIcon
                          iconName="utility:advertising"
                          variant="destructive"
                          class="formButtonDestructive showOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openViewActions}"
                        />
                      </aura:if>
                      <aura:if
                        isTrue="{!production.status=='Active'? true : false}"
                      >
                        <lightning:button
                          label="Enter Itinerary"
                          class="formButtonBrandInverse hideOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openEnterItinerary}"
                        />
                        <lightning:buttonIcon
                          iconName="utility:trail"
                          class="formButtonBrandInverse showOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openEnterItinerary}"
                        />
                      </aura:if>
                      <lightning:button
                        label="View"
                        class="formButtonDestructiveInverse hideOnTablet"
                        value="{!production.recordId}"
                        onclick="{!c.openItineraryOverview}"
                      />
                      <lightning:buttonIcon
                        iconName="utility:description"
                        class="formButtonDestructiveInverse showOnTablet"
                        value="{!production.recordId}"
                        onclick="{!c.openItineraryOverview}"
                      />
                    </div>
                  </div>
                </aura:iteration>
                <aura:if isTrue="{!empty(v.productionsFiltered)}">
                  <div class="productionTableRow">
                    <div></div>
                    <div style="text-align: left; font-style: italic">
                      No productions found.
                    </div>
                  </div>
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
### VoyajerDashboard

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerDashboardController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadProductions");
        callToParent.fire();
	},
    
    loadTable : function(component, event, helper) {
        /**Fix By Clay Dev 2 April, 2021 #177403104
        component.set("v.filterStatus","View all");**/
        var filterStatus = "Active";
        component.set("v.filterStatus",filterStatus);
        component.set("v.startDateBegin","");
        component.set("v.startDateEnd","");
        var productions = component.get("v.productions");
        var productionsOnAlert = 0;
        productions.forEach(production => { if(production.isMissingAction) productionsOnAlert++ });
        if(productionsOnAlert > 1) component.set("v.dashboardPillMessage","You have "+productionsOnAlert+" productions with an action needed.");
        else if(productionsOnAlert == 1) component.set("v.dashboardPillMessage","You have 1 production with an action needed.");
        else component.set("v.isDashboardPillRead",true);
        component.set("v.productionsFiltered",productions);
        
        //sort..
        /**Fix By Clay Dev 2 April, 2021 #177403104
        var productionsSorted = helper.sortMethod(component);
        component.set("v.productionsFiltered", productionsSorted);**/
        
        productions = helper.sortMethod(component);
        var productionsFiltered = [];
        productions.forEach(production => { 
            if(production.status.toLowerCase() == filterStatus.toLowerCase()) 
            productionsFiltered.push(production) 
        });
        component.set("v.productionsFiltered", productionsFiltered);
    },
    
    handleRemoveDashboardPill : function(component, event, helper) {
        component.set("v.isDashboardPillRead",true);
    },    
    handleShowMessages : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","showMessages");
        callToParent.fire();    
    },
    handleNewProduction : function(component, event, helper) {
        component.set("v.mainContent","newProduction");
    },
    
    handleFilter : function(component, event, helper) {
        var filterStatus = "";
        var sourceName = event.getSource().get("v.name");
        if(sourceName.localeCompare("startDateBegin") !== 0 && sourceName.localeCompare("startDateEnd") !== 0) filterStatus = event.getSource().get("v.value");
        else filterStatus = component.get("v.filterStatus");
        var productions = component.get("v.productions");
        var productionsFiltered = [];
        if(filterStatus != "View all") productions.forEach(production => { if(production.status.toLowerCase() == filterStatus.toLowerCase()) productionsFiltered.push(production) });
        else productionsFiltered = productions.slice(0);
        component.set("v.filterStatus",filterStatus);
        var validExpense = component.find('startDateRange').reduce(function (validSoFar, inputComponent) {
            // Displays error messages for invalid fields
            inputComponent.showHelpMessageIfInvalid();
            return validSoFar && inputComponent.get('v.validity').valid;
        }, true);
        // If we pass error checking, do some real work
        if(validExpense) {
            var productionsFilteredByDate = [];
            var startDateBegin = component.get("v.startDateBegin");
            var startDateEnd = component.get("v.startDateEnd");
            if(startDateBegin && startDateEnd) {
                productionsFiltered.forEach(production => { if(production.hasOwnProperty("comparisonDate") && new Date(production.comparisonDate) >= new Date(startDateBegin)  && new Date(production.comparisonDate) <= new Date(startDateEnd)) productionsFilteredByDate.push(production) });
            } else if(startDateBegin) {
                productionsFiltered.forEach(production => { if(production.hasOwnProperty("comparisonDate") && new Date(production.comparisonDate) >= new Date(startDateBegin)) productionsFilteredByDate.push(production) });
            } else if(startDateEnd) {
                productionsFiltered.forEach(production => { if(production.hasOwnProperty("comparisonDate") && new Date(production.comparisonDate) <= new Date(startDateEnd)) productionsFilteredByDate.push(production) });
            } else {
                productionsFilteredByDate = productionsFiltered.slice(0);
            }
            productionsFiltered = productionsFilteredByDate.slice(0);
        }
        component.set("v.productionsFiltered",productionsFiltered);
        
        //sort..
        var productionsSorted = helper.sortMethod(component);
        component.set("v.productionsFiltered", productionsSorted);
    },
    
    handleSort : function(component, event, helper) {
        var productionsSorted = helper.sortMethod(component);
        component.set("v.productionsFiltered", productionsSorted);
        //console.log('#productionsSorted = ' + JSON.stringify(productionsSorted));
    },
    
    openViewActions : function(component, event, helper) {
        component.set("v.productionSelected",event.getSource().get("v.value"));
        
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadContactUsData");
        callToParent.fire();
        component.set("v.mainContent","actions");
    },
    
    openEnterItinerary : function(component, event, helper) {
        component.set("v.productionSelected",event.getSource().get("v.value"));
        
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadContactUsData");
        callToParent.fire();
        component.set("v.mainContent","itinerary");
    },
    
    openItineraryOverview : function(component, event, helper) {
        var productionSelected = event.getSource().get("v.value");
        var productionName = "";
        var productionsFiltered = component.get("v.productionsFiltered");
        productionsFiltered.forEach(production => { if(production.recordId == productionSelected) productionName = production.name });
        component.set("v.productionName",productionName);
        component.set("v.productionSelected",productionSelected);
        
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadContactUsData");
        callToParent.fire();
        component.set("v.mainContent","overview");
    }
})
```
### VoyajerDashboardHelper

```
({
	sortMethod : function(component) {
        //console.log('# sortMethod');
        var productions = component.get("v.productionsFiltered");
        var sortValue = component.find("sortBy").get("v.value");
        
		if(sortValue == 'productionNameAsc'){
            //console.log('# productionNameAsc');
        	productions.sort((a, b) => a.name.localeCompare(b.name));
        }else if(sortValue == 'startDateAsc'){
            //console.log('# startDateAsc');
            productions.sort((a, b) => new Date(a.startDate) - new Date(b.startDate));
        }else if(sortValue == 'startDateDesc'){
            //console.log('# startDateDesc');
            productions.sort((a, b) => new Date(b.startDate) - new Date(a.startDate));
        }else if(sortValue == 'endDateAsc'){
            //console.log('# endDateAsc');
            productions.sort((a, b) => new Date(a.endDate) - new Date(b.endDate));
        }else if(sortValue == 'endDateDesc'){
            //console.log('# endDateDesc');
            productions.sort((a, b) => new Date(b.endDate) - new Date(a.endDate));
        }else if(sortValue == 'statusAsc'){
            //console.log('# statusAsc');
            productions.sort((a, b) => a.status.localeCompare(b.status));
        }
        
        //result
        return productions;
	}
})
```
### VoyajerDashboard

```
.THIS .startDateContainer {
    align-items: center;
    display: flex;
    border: 1px solid #dbdbdb;
    border-radius: 2em;
    padding: 0 0.75em;
    margin-right: 0.25em;
    max-width: 17rem;
}

.THIS .filterButtons {
    display: flex;
    width: 100%;
    justify-content: flex-start;
}

.THIS .formField {
    width: auto;
    margin-bottom: 0;
}

.THIS .startDateContainer .slds-input__icon {
    display: none;
}

.THIS .startDateInput .slds-input {
    padding: 0 0.25em;
    max-width: calc(8rem + 2px);
    text-align: center;
    border-width: 0;
}

.THIS .productionTable {
    display: flex;
    flex-direction: column;
    width: 100%;
    min-width: 900px;
}

.THIS .productionTableHeader {
    display: flex;
    flex-direction: row;
    font-weight: 500;
    border-bottom: 1px solid #606060;
}

.THIS .productionTableHeader > div {
    padding: 0 0.8em 0.6em;
    width: 7em;
}

.THIS .productionTableHeader > div:nth-child(2) {
    /*flex: 1;*/
    flex: 2;
    width: auto;
}

.THIS .productionTableHeader > div:last-child {
    flex: 3;
    width: auto;
}

.THIS .productionTableBody {
    display: flex;
    flex-direction: column;
}

.THIS .productionTableRow {
    display: flex;
    flex-direction: row;
    width: 100%;
    align-items: center;
}

.THIS .productionTableRow > div {
    padding: 0.6em 0.8em;
    width: 7em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .productionTableRow:nth-child(odd) {
    background-color: #f7f9fe;
}

.THIS .productionTableRow:not(:first-child) {
    border-top: 1px solid #dbdbdb;
}

.THIS .productionTableHeader > div:first-child,
.THIS .productionTableRow > div:first-child {
    text-align: center;
    width: 2.75em;
}

.THIS .productionTableRow > div:first-child svg {
    fill: #e00000
}

.THIS .productionTableRow > div:nth-child(2) {
    /*flex: 1;*/
    flex: 2;
    width: auto;
}

.THIS .productionTableRow > div:last-child {
    flex: 3;
    text-align: right;
    width: auto;
}

.THIS .productionTableHeader .productionServicesColumn,
.THIS .productionTableRow .productionServicesColumn {
    display: flex;
    width: 8em;
}

.THIS .productionTableHeader .productionCompanyColumn,
.THIS .productionTableRow .productionCompanyColumn {
    width: 12em;
}

.THIS .productionService {
    padding: 0 0.25em;
}

.THIS .formField {
    margin-bottom: 0;
}

.THIS .updateColumn {
    align-items: center;
    justify-content: flex-end;
    align-items: flex-start;
    justify-content: flex-start;
}

@media (max-width: 1200px) {
    .THIS .productionTableHeader > div:last-child,
    .THIS .productionTableRow > div:last-child {
        flex: none;
        width: 11em;
    }
}

@media (max-width: 1024px) {
    .THIS .startDateInput {
        /*max-width: 11em;*/
    }
}

@media (max-width: 550px) {
    .THIS .startDateContainer {
        flex-wrap: wrap;
        width: 100%;
        margin: 0;
    }
    
    .THIS .filterButtons {
        justify-content: space-between;
    }
    
    .THIS .startDateInput {
        /*max-width: 9em;*/
    }
}

/*util*/
.THIS .label-hidden > label {
    display: none;
}
```
### VoyajerDashboard

```
<aura:component>
  <aura:attribute
    type="User"
    name="userLogged"
    default="{'sobjectType' : 'User'}"
  />
  <aura:attribute type="String" name="communityNote" default="" />
  <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
  <aura:attribute type="List" name="productions" />
  <aura:attribute type="List" name="productionsFiltered" />
  <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
  <aura:attribute type="String" name="mainContent" />
  <!--Fix By Clay Dev 2 April, 2021 #177403104
  <aura:attribute type="String" name="filterStatus" default="View all" />-->
  <aura:attribute type="String" name="filterStatus" default="Active" />
  <aura:attribute
    type="String"
    name="dashboardPillMessage"
    default="You have 1 production with an action needed."
  />
  <aura:attribute type="String" name="startDateBegin" default="" />
  <aura:attribute type="String" name="startDateEnd" default="" />
  <aura:attribute type="String" name="officePreference" />
  <aura:attribute type="String" name="productionSelected" />
  <aura:attribute type="String" name="productionName" />

  <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
  <aura:handler
    name="change"
    value="{!v.productions}"
    action="{!c.loadTable}"
  />
  <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

  <div>
    <div class="pageContent">
      <div class="pageContentSpaces">
        <div class="page-section">
          <div class="page-header">
            <h1><span>{!v.userLogged.Contact.Account.Name}</span></h1>
          </div>
        </div>
        <aura:if isTrue="{!not(v.isDashboardPillRead)}">
          <div class="pageContentDashboard" style="margin-bottom: 2em">
            <lightning:pill
              label="{!v.dashboardPillMessage}"
              onremove="{!c.handleRemoveDashboardPill}"
              class="dashboardPill"
            >
              <aura:set attribute="media"
                ><i class="fas fa-bell" style="margin-right: 0.5em"></i
              ></aura:set>
            </lightning:pill>
          </div>
        </aura:if>
        <div style="margin-bottom: 1em; text-align: right">
          <lightning:button
            label="Create new production"
            variant="brand"
            iconName="utility:add"
            iconPosition="left"
            class="formButtonBrandLight"
            onclick="{!c.handleNewProduction}"
          />
        </div>
        <div
          class="pageContentDashboard"
          style="border-bottom: 1px solid #dbdbdb"
        >
          <div class="page-section">
            <h3>
              <i
                class="far fa-star"
                style="color: #9f9f9f; margin-right: 0.5em"
              ></i
              >Productions
            </h3>
          </div>
          <div class="page-section-buttons">
            <div style="flex: 1">
              <div
                class="formColumnThreeChilds"
                style="justify-content: space-between"
              >
                <div
                  class="formField"
                  style="display: flex; align-items: flex-end"
                >
                  <div class="formField filterButtons">
                    <lightning:button
                      label="Active"
                      name="Active"
                      variant="{!if(v.filterStatus=='Active','brand','neutral')}"
                      class="{!if(v.filterStatus=='Active','formButtonBrand','')}"
                      value="Active"
                      onclick="{!c.handleFilter}"
                    />
                    <lightning:button
                      label="Historic"
                      name="Historic"
                      variant="{!if(v.filterStatus=='Historic','brand','neutral')}"
                      class="{!if(v.filterStatus=='Historic','formButtonBrand','')}"
                      value="Historic"
                      onclick="{!c.handleFilter}"
                    />
                    <lightning:button
                      label="View all"
                      name="View all"
                      variant="{!if(v.filterStatus=='View all','brand','neutral')}"
                      class="{!if(v.filterStatus=='View all','formButtonBrand','')}"
                      value="View all"
                      onclick="{!c.handleFilter}"
                    />
                    <lightning:buttonIcon
                      iconName="utility:sync"
                      variant="brand"
                      class="formButtonBrandLight showOnMobile"
                      onclick="{!c.doInit}"
                    />
                  </div>
                </div>
                <div class="formField">
                  <label class="hideOnMobile">Sort by</label>
                  <lightning:select
                    label="Sort"
                    aura:id="sortBy"
                    variant="label-hidden"
                    class="slds-form-element-filter label-hidden"
                    onchange="{!c.handleSort}"
                  >
                    <option value="productionNameAsc" selected="true">
                      Production Name (A-Z)
                    </option>
                    <option value="startDateAsc">Start Date (Asc)</option>
                    <option value="startDateDesc">Start Date (Desc)</option>
                    <option value="endDateAsc">End Date (Asc)</option>
                    <option value="endDateDesc">End Date (Desc)</option>
                    <option value="statusAsc">Status (A-Z)</option>
                  </lightning:select>
                </div>
                <div
                  class="formField"
                  style="margin-bottom: 0; flex-direction: column"
                >
                  <label class="hideOnMobile">Filter by Start Date</label>
                  <div class="startDateContainer">
                    <div style="padding-right: 0.5em">
                      <lightning:icon
                        iconName="utility:date_input"
                        alternativeText="Connected"
                        size="x-small"
                      />
                    </div>
                    <div class="formField" style="margin-bottom: 0">
                      <lightning:input
                        aura:id="startDateRange"
                        class="startDateInput"
                        name="startDateBegin"
                        type="date"
                        label=""
                        variant="label-hidden"
                        dateStyle="short"
                        placeholder="{!if(v.officePreference=='RRE','dd-mm-yyyy','mm/dd/yyyy')}"
                        max="{!v.startDateEnd}"
                        value="{!v.startDateBegin}"
                        onchange="{!c.handleFilter}"
                        autocomplete="off"
                      />
                    </div>
                    <div style="padding: 0 0.5em">
                      {!if(v.officePreference=='RRE',' / ',' - ')}
                    </div>
                    <div class="formField" style="margin-bottom: 0">
                      <lightning:input
                        aura:id="startDateRange"
                        class="startDateInput"
                        name="startDateEnd"
                        type="date"
                        label=""
                        variant="label-hidden"
                        dateStyle="short"
                        placeholder="{!if(v.officePreference=='RRE','dd-mm-yyyy','mm/dd/yyyy')}"
                        min="{!v.startDateBegin}"
                        value="{!v.startDateEnd}"
                        onchange="{!c.handleFilter}"
                        autocomplete="off"
                      />
                    </div>
                  </div>
                </div>
                <div
                  class="formField hideOnMobile"
                  style="display: flex; align-items: flex-end"
                >
                  <div class="formField">
                    <lightning:button
                      label="Update"
                      variant="brand"
                      class="formButtonBrandLight hideOnMobile"
                      onclick="{!c.doInit}"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="pageContentDashboard">
          <div class="page-section" style="overflow-x: auto">
            <div class="productionTable">
              <div class="productionTableHeader">
                <div></div>
                <div>Production Name</div>
                <div>Start Date</div>
                <div>End Date</div>
                <!--<div class="productionCompanyColumn">Company</div>-->
                <div class="productionServicesColumn">Services</div>
                <div>Status</div>
                <div></div>
              </div>
              <div class="productionTableBody">
                <aura:iteration
                  items="{!v.productionsFiltered}"
                  var="production"
                >
                  <div class="productionTableRow">
                    <div style="color: #e00000">
                      <aura:if isTrue="{!production.isMissingAction}"
                        ><lightning:icon
                          iconName="utility:notification"
                          variant="error"
                          size="xx-small"
                      /></aura:if>
                    </div>
                    <div>{!production.name}</div>
                    <div style="text-align: center; letter-spacing: 1px">
                      {!production.startDate}
                    </div>
                    <div style="text-align: center; letter-spacing: 1px">
                      {!production.endDate}
                    </div>
                    <!--<div class="productionCompanyColumn">{!production.company}</div>-->
                    <div
                      class="productionServicesColumn"
                      style="color: #00b4ff"
                    >
                      <aura:if isTrue="{!production.haveServiceHousing}"
                        ><div class="productionService">
                          <i class="fas fa-home"></i></div
                      ></aura:if>
                      <aura:if isTrue="{!production.haveServiceGround}"
                        ><div class="productionService">
                          <i class="fas fa-car"></i></div
                      ></aura:if>
                      <aura:if isTrue="{!production.haveServiceAir}"
                        ><div class="productionService">
                          <i class="fas fa-plane"></i></div
                      ></aura:if>
                      <aura:if isTrue="{!production.haveServiceFreight}"
                        ><div class="productionService">
                          <i class="fas fa-truck"></i></div
                      ></aura:if>
                    </div>
                    <div>{!production.status}</div>
                    <div>
                        <aura:if isTrue="{!production.isMissingAction}">
                        <lightning:button
                          label="Action Needed"
                          variant="destructive"
                          class="formButtonDestructive hideOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openViewActions}"
                        />
                        <lightning:buttonIcon
                          iconName="utility:advertising"
                          variant="destructive"
                          class="formButtonDestructive showOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openViewActions}"
                        />
                      </aura:if>
                      <aura:if
                        isTrue="{!production.status=='Active'? true : false}"
                      >
                        <lightning:button
                          label="Enter Itinerary"
                          class="formButtonBrandInverse hideOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openEnterItinerary}"
                        />
                        <lightning:buttonIcon
                          iconName="utility:trail"
                          class="formButtonBrandInverse showOnTablet"
                          value="{!production.recordId}"
                          onclick="{!c.openEnterItinerary}"
                        />
                      </aura:if>
                      <lightning:button
                        label="View"
                        class="formButtonDestructiveInverse hideOnTablet"
                        value="{!production.recordId}"
                        onclick="{!c.openItineraryOverview}"
                      />
                      <lightning:buttonIcon
                        iconName="utility:description"
                        class="formButtonDestructiveInverse showOnTablet"
                        value="{!production.recordId}"
                        onclick="{!c.openItineraryOverview}"
                      />
                    </div>
                  </div>
                </aura:iteration>
                <aura:if isTrue="{!empty(v.productionsFiltered)}">
                  <div class="productionTableRow">
                    <div></div>
                    <div style="text-align: left; font-style: italic">
                      No productions found.
                    </div>
                  </div>
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

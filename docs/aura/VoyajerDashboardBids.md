---
layout: default
title: VoyajerDashboardBids
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerDashboardBids
## Fields
### VoyajerDashboardBidsController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        //callToParent.setParam("action","loadVendorProductions");
        callToParent.setParam("action","loadVendorBids");
        callToParent.fire();
	},
    
    loadTable : function(component, event, helper) {
        component.set("v.filterStatus","View all");
        component.set("v.startDateBegin","");
        component.set("v.startDateEnd","");
        var bids = component.get("v.bids");
        var bidsOnAlert = 0;
        console.log("# bids.length = " + bids.length);
        bids.forEach(bid => { if(bid.isMissingAction) bidsOnAlert++ });
        if(bidsOnAlert > 1) component.set("v.dashboardPillMessage","You have "+bidsOnAlert+" bids with an action needed.");
        else if(bidsOnAlert == 1) component.set("v.dashboardPillMessage","You have 1 bid with an action needed.");
        else component.set("v.isDashboardPillRead",true);
        component.set("v.bidsFiltered",bids);
        
        /**Fix by Clay Dev 29 Jan, 2021 #176564085
        var bidsFiltered = component.get("v.bidsFiltered");
        console.log("# bidsFiltered.length = " + bidsFiltered.length);
        
        //sort...
        var bidsSorted = helper.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);**/
        helper.filterMethod(component, "View all");
    },
    
    
    /*handleRemoveDashboardPill : function(component, event, helper) {
        component.set("v.isDashboardPillRead",true);
    },
    
    handleNewProduction : function(component, event, helper) {
        component.set("v.mainContent","newProduction");
    },
    
    openEnterItinerary : function(component, event, helper) {
        component.set("v.productionSelected",event.getSource().get("v.value"));
        component.set("v.mainContent","itinerary");
    },*/
    
    handleFilter : function(component, event, helper) {
        var filterStatus = filterStatus = event.getSource().get("v.value");
        /**Fix By Clay Dev 30 Jan 2021 #176564085
        var bids = component.get("v.bids");
        var bidsFiltered = [];
        
        if(filterStatus != "View all") 
            bids.forEach(bid => {
                if(filterStatus == "Won" && bid.bidStatus.toLowerCase() == "contracted")
                	bidsFiltered.push(bid)
                else if (filterStatus == "Lost" && bid.bidStatus.toLowerCase() == "cancelled")
                	bidsFiltered.push(bid)
            });
        else bidsFiltered = bids.slice(0);
        component.set("v.filterStatus",filterStatus);
        component.set("v.bidsFiltered",bidsFiltered);
        
        //sort...
        var bidsSorted = helper.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);**/
        helper.filterMethod(component, filterStatus);
        component.set("v.filterStatus",filterStatus);
    },
    
    handleSort : function(component, event, helper) {
        var bidsSorted = helper.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);
        //console.log('#bidsSorted = ' + JSON.stringify(bidsSorted));
    },
    
    openViewActions : function(component, event, helper) {
        var bidSelected = $(event.currentTarget).parents('.bid_buttons').data('serviceid');
        component.set("v.bidRecordId", bidSelected);
        /*component.set("v.bidSelected", bidSelected);
component.set("v.productionSelected", bidSelected);*/
        component.set("v.mainContent","vendorActions");
    },
    
    handleDocuments : function(component, event, helper){
        console.log('# handleDocuments()');
        var bidSelected = $(event.currentTarget).parents('.bid_buttons').data('serviceid');
        var productionName = "";
        var bidName = "";
        var bidsFiltered = component.get("v.bidsFiltered");
        bidsFiltered.forEach(bid => { if(bid.bidId == bidSelected){
                                     	productionName = bid.productionName;
                                     	bidName = bid.bidName;
                                     	//console.log('bid = ' + JSON.stringify(bid));
                                    }});
        
        component.set("v.productionName",productionName);
        component.set("v.bidName",bidName);
        
		component.set("v.serviceId", bidSelected);
		component.set("v.serviceType", $(event.currentTarget).parents('.bid_buttons').data('servicetype'));
        //component.set("v.serviceDateInAndOut", $(event.currentTarget).parents('.bid_buttons').data('servicedateinandout'));
        component.set("v.serviceDateInAndOut", $(event.currentTarget).parents('.bid_buttons').data('servicedatein').replace(/-/g, "/") + " - " + $(event.currentTarget).parents('.bid_buttons').data('servicedateout').replace(/-/g, "/"));
        component.set("v.serviceCityName", $(event.currentTarget).parents('.bid_buttons').data('servicecityname'));
		component.set("v.mainContent", "documents");
        
        console.log('# seviceId = ' + $(event.currentTarget).parents('.bid_buttons').data('serviceid'));
        console.log('# seviceId = ' + bidSelected);
    },
    
    openReservationDetail : function(component, event, helper) {
        var bidSelected = $(event.currentTarget).parents('.bid_buttons').data('serviceid');
        var productionName = "";
        var bidName = "";
        var bidsFiltered = component.get("v.bidsFiltered");
        bidsFiltered.forEach(bid => { if(bid.bidId == bidSelected) {
                                         productionName = bid.productionName;
                                         bidName = bid.bidName;
                                    }});
        component.set("v.productionName",productionName);
        component.set("v.bidName",bidName);
        component.set("v.bidRecordId",bidSelected);
        
        var userProfile = component.get("v.userProfile");
        console.log('# userProfile = ' + userProfile);
        if(userProfile == "GroundVendor") component.set("v.mainContent", "vendorReservationGTDetails");
        else if(userProfile == "HousingVendor" || userProfile == "CorporateVendor") component.set("v.mainContent", "vendorReservationHousingDetails");
        
        //component.set("v.mainContent","vendorReservationGTDetails");
    }
})
```
### VoyajerDashboardBids

```
<aura:component >
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="List" name="bids" />
    <aura:attribute type="List" name="bidsFiltered" />
    <aura:attribute type="String" name="bidRecordId" />
    <aura:attribute type="String" name="userProfile" />
    
    <aura:attribute type="List" name="productions" />
    <aura:attribute type="List" name="productionsFiltered" />
    <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="filterStatus" default="View all" />
    <aura:attribute type="String" name="dashboardPillMessage" default="You have 1 bid with an action needed." />
    <aura:attribute type="String" name="startDateBegin" default="" />
    <aura:attribute type="String" name="startDateEnd" default="" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    
    <!--docs-->
    <aura:attribute name="serviceId" type="String"/>
    <aura:attribute name="serviceType" type="String"/>
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <!--end docs-->
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bids}" action="{!c.loadTable}" />
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
                    <div class="pageContentDashboard" style="margin-bottom: 2em;">
                        <lightning:pill label="{!v.dashboardPillMessage}" onremove="{!c.handleRemoveDashboardPill}" class="dashboardPill">
                            <aura:set attribute="media"><i class="fas fa-bell" style="margin-right: 0.5em;"></i></aura:set>
                        </lightning:pill>
                    </div>
                </aura:if>
                <!--<div style="margin-bottom: 1em; text-align: right;">
                    <lightning:button label="Create new production" variant="brand" iconName="utility:add" iconPosition="left" class="formButtonBrandLight" onclick="{!c.handleNewProduction}" />
                </div>-->
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <h3><i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em;"></i>Bids</h3>
                    </div>
                    <div class="page-section-buttons">
                        <div style="height: 2.5em;">
                            <lightning:button label="Won" 
                                              name="Won" 
                                              variant="{!if(v.filterStatus=='Won','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='Won','formButtonBrand','')}"
                                              value="Won"
                                              onclick="{!c.handleFilter}" />
                            <lightning:button label="Lost" 
                                              name="Lost" 
                                              variant="{!if(v.filterStatus=='Lost','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='Lost','formButtonBrand','')}" 
                                              value="Lost"
                                              onclick="{!c.handleFilter}" />
                            <lightning:button label="View all" 
                                              name="View all" 
                                              variant="{!if(v.filterStatus=='View all','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='View all','formButtonBrand','')}" 
                                              value="View all"
                                              onclick="{!c.handleFilter}" />
                            <!--Fix By Clay Dev 30 Jan 2021 #176564085-->
                            <lightning:button label="Cancelled" 
                                              name="Cancelled" 
                                              variant="{!if(v.filterStatus=='Cancelled','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='Cancelled','formButtonBrand','')}" 
                                              value="Cancelled"
                                              onclick="{!c.handleFilter}" />
                            <lightning:buttonIcon iconName="utility:sync" variant="brand" class="formButtonBrandLight showOnMobile" onclick="{!c.doInit}" />
                        </div>
                        <div style="align-items: center; justify-content: flex-end; flex: 1;">
                            <p class="hideOnMobile" style="margin-right: 0.5em;">Sort by</p>
                            <lightning:select label="Sort" aura:id="sortBy" variant="label-hidden" class="slds-form-element-filter label-hidden" onchange="{!c.handleSort}">
                                <option value="productionNameAsc" selected="true">Production Name (A-Z)</option>
                                <option value="startDateAsc">Start Date (Asc)</option>
                                <option value="startDateDesc">Start Date (Desc)</option>
                                <option value="endDateAsc">End Date (Asc)</option>
                                <option value="endDateDesc">End Date (Desc)</option>
                            </lightning:select>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section" style="overflow-x: auto;">
                        <div class="productionTable">
                            <div class="productionTableHeader">
                                <div></div>
                                <div>Production Name</div>
                                <div>Start Date</div>
                                <div>End Date</div>
                                <div class="productionCompanyColumn">Company</div>
                                <div class="productionCompanyColumn">Location</div>
                                <!--<div>Bids Won</div>
                                <div>Bids Lost</div>-->
                                <div></div>
                            </div>
                            <div class="productionTableBody">
                                <aura:iteration items="{!v.bidsFiltered}" var="bid">
                                    <div class="productionTableRow">
                                        <div style="color: #e00000;">
                                            <aura:if isTrue="{!bid.isMissingAction}"><lightning:icon iconName="utility:notification" variant="error" size="xx-small"/></aura:if>
                                        </div>
                                        <div>{!bid.productionName}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!bid.startDate}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!bid.endDate}</div>
                                        <div class="productionCompanyColumn">{!bid.company}</div>
                                        <div class="productionCompanyColumn">{!bid.location}</div>
                                        <!--<div style="text-align: center; letter-spacing: 1px;">{!production.numBidsContracted}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!production.numBidsCancelled}</div>-->
                                        
                                        <div class="bid_buttons" data-servicetype="{!bid.bidType}" data-serviceid="{!bid.bidId}" data-servicedateinandout="{!bid.startDate + ' - ' + bid.endDate}" data-servicecityname="{!bid.location}" data-servicedatein="{!bid.startDate}"  data-servicedateout="{!bid.endDate}">
                                            <!--Fix By Clay Dev 4 Feb, 2021 #176564085 -->
                                            <aura:if isTrue="{!v.filterStatus != 'Cancelled'}">
                                            <aura:if isTrue="{!bid.isMissingAction}">
                                                <!--<lightning:button label="Action Needed" variant="destructive" class="formButtonDestructive hideOnTablet" value="{!production.recordId}" onclick="{!c.openViewActions}" />-->
                                               	<button class="slds-button slds-button_neutral formButtonDestructive hideOnTablet" onclick="{!c.openViewActions}">Action Needed</button>
                                                <!--<lightning:buttonIcon iconName="utility:advertising" variant="destructive" class="formButtonDestructive showOnTablet" value="{!production.recordId}" onclick="{!c.openViewActions}" />-->
                                            </aura:if>
                                            <!--Fix By Clay Dev 4 Feb, 2021 #176564085 -->
                                            </aura:if>
                                            <!--<aura:if isTrue="{!production.status=='Active'? true : false}">
                                                <lightning:button label="Enter Itinerary" class="formButtonBrandInverse hideOnTablet" value="{!production.recordId}" onclick="{!c.openEnterItinerary}" />
                                                <lightning:buttonIcon iconName="utility:trail" class="formButtonBrandInverse showOnTablet" value="{!production.recordId}" onclick="{!c.openEnterItinerary}" />
                                            </aura:if>-->
                                            
                                            <button class="slds-button slds-button_brand formButtonBrandLight hideOnTablet" onclick="{!c.handleDocuments}">Documents</button>
                                            <!--<span class="showOnTablet" onclick="{!c.handleDocuments}"><lightning:icon iconName="action:add_file" alternativeText="Documents" title="Documents" /></span>
                                            <lightning:button label="Documents" variant="brand" class="formButtonBrandLight hideOnTablet" value="{!production.recordId}" onclick="{!c.handleDocuments}" />
                                            <lightning:buttonIcon iconName="utility:description" class="formButtonBrandLight showOnTablet" value="{!production.recordId}" onclick="{!c.handleDocuments}" />-->
                                            
                                            <button class="slds-button slds-button_neutral formButtonDestructiveInverse hideOnTablet" onclick="{!c.openReservationDetail}">View</button>
                                            <!-- <lightning:buttonIcon iconName="utility:description" class="formButtonDestructiveInverse showOnTablet" value="{!bid.productionId}" onclick="{!c.openReservationDetail}" /> -->
                                        </div>
                                    </div>
                                </aura:iteration>
                                <aura:if isTrue="{!empty(v.bidsFiltered)}">
                                    <div class="productionTableRow"><div></div><div style="text-align: left; font-style: italic;">No bids found.</div></div>
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
### VoyajerDashboardBids

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerDashboardBidsHelper

```
({
	sortMethod : function(component) {
        //console.log('# sortMethod');
        var bids = component.get("v.bidsFiltered");
        var sortValue = component.find("sortBy").get("v.value");
        
		if(sortValue == 'productionNameAsc'){
            //console.log('# productionNameAsc');
        	bids.sort((a, b) => a.productionName.localeCompare(b.productionName));
        }else if(sortValue == 'startDateAsc'){
            //console.log('# startDateAsc');
            bids.sort((a, b) => new Date(a.startDate) - new Date(b.startDate));
        }else if(sortValue == 'startDateDesc'){
            //console.log('# startDateDesc');
            bids.sort((a, b) => new Date(b.startDate) - new Date(a.startDate));
        }else if(sortValue == 'endDateAsc'){
            //console.log('# endDateAsc');
            bids.sort((a, b) => new Date(a.endDate) - new Date(b.endDate));
        }else if(sortValue == 'endDateDesc'){
            //console.log('# endDateDesc');
            bids.sort((a, b) => new Date(b.endDate) - new Date(a.endDate));
        }else if(sortValue == 'statusAsc'){
            //console.log('# statusAsc');
            bids.sort((a, b) => a.status.localeCompare(b.status));
        }
        
        //result
        return bids;
	},
    //Fix by Clay Dev 29 Jan, 2021 #176564085
    filterMethod : function(component, filterStatus) {
        var bids = component.get("v.bids");
        var bidsFiltered = [];
        
        bids.forEach(bid => {
            //Fix by Clay Dev 1 Feb, 2021 #176564085
            if(bid.bidStatus != undefined && bid.bidStatus != null) {
                if(filterStatus == "View all" && bid.bidStatus.toLowerCase() != "cancelled")
                    bidsFiltered.push(bid);
                else if(filterStatus == "Won" && bid.bidStatus.toLowerCase() == "contracted")
                    bidsFiltered.push(bid);
                else if (filterStatus == "Lost" && bid.bidStatus.toLowerCase() == "cancelled")
                    bidsFiltered.push(bid);
                else if (filterStatus == "Cancelled" && bid.bidStatus.toLowerCase() == "cancelled")
                    bidsFiltered.push(bid);
        	}
        });
       
        component.set("v.bidsFiltered", bidsFiltered);
        var bidsSorted = this.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);
        
    }
})
```
### VoyajerDashboardBids

```
.THIS .startDateContainer {
    align-items: center;
    display: flex;
    border: 1px solid #dbdbdb;
    border-radius: 2em;
    padding: 0 0.75em;
    margin-right: 0.25em;
}

.THIS .startDateContainer .slds-input__icon {
    display: none;
}


.THIS .startDateInput {
    padding: 0 0.25em;
    text-align: center;
    border: none;
    max-width: 8em;
}

.THIS .startDateInput input {
    padding: 0 0.25em;
    text-align: center;
    border: none;
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
    flex: 1;
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
    flex: 1;
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

@media (max-width: 1200px) {
    .THIS .productionTableHeader > div:last-child,
    .THIS .productionTableRow > div:last-child {
        flex: none;
        width: 11em;
    }
}

@media (max-width: 1024px) {
    .THIS .startDateInput {
        max-width: 11em;
    }
}

@media (max-width: 550px) {
    .THIS .startDateContainer {
        flex-wrap: wrap;
        width: 100%;
        margin: 0;
    }
    
    .THIS .startDateInput {
        max-width: 9em;
    }
}

/*util*/
.THIS .label-hidden > label {
    display: none;
}
```
### VoyajerDashboardBidsController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        //callToParent.setParam("action","loadVendorProductions");
        callToParent.setParam("action","loadVendorBids");
        callToParent.fire();
	},
    
    loadTable : function(component, event, helper) {
        component.set("v.filterStatus","View all");
        component.set("v.startDateBegin","");
        component.set("v.startDateEnd","");
        var bids = component.get("v.bids");
        var bidsOnAlert = 0;
        console.log("# bids.length = " + bids.length);
        bids.forEach(bid => { if(bid.isMissingAction) bidsOnAlert++ });
        if(bidsOnAlert > 1) component.set("v.dashboardPillMessage","You have "+bidsOnAlert+" bids with an action needed.");
        else if(bidsOnAlert == 1) component.set("v.dashboardPillMessage","You have 1 bid with an action needed.");
        else component.set("v.isDashboardPillRead",true);
        component.set("v.bidsFiltered",bids);
        
        /**Fix by Clay Dev 29 Jan, 2021 #176564085
        var bidsFiltered = component.get("v.bidsFiltered");
        console.log("# bidsFiltered.length = " + bidsFiltered.length);
        
        //sort...
        var bidsSorted = helper.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);**/
        helper.filterMethod(component, "View all");
    },
    
    
    /*handleRemoveDashboardPill : function(component, event, helper) {
        component.set("v.isDashboardPillRead",true);
    },
    
    handleNewProduction : function(component, event, helper) {
        component.set("v.mainContent","newProduction");
    },
    
    openEnterItinerary : function(component, event, helper) {
        component.set("v.productionSelected",event.getSource().get("v.value"));
        component.set("v.mainContent","itinerary");
    },*/
    
    handleFilter : function(component, event, helper) {
        var filterStatus = filterStatus = event.getSource().get("v.value");
        /**Fix By Clay Dev 30 Jan 2021 #176564085
        var bids = component.get("v.bids");
        var bidsFiltered = [];
        
        if(filterStatus != "View all") 
            bids.forEach(bid => {
                if(filterStatus == "Won" && bid.bidStatus.toLowerCase() == "contracted")
                	bidsFiltered.push(bid)
                else if (filterStatus == "Lost" && bid.bidStatus.toLowerCase() == "cancelled")
                	bidsFiltered.push(bid)
            });
        else bidsFiltered = bids.slice(0);
        component.set("v.filterStatus",filterStatus);
        component.set("v.bidsFiltered",bidsFiltered);
        
        //sort...
        var bidsSorted = helper.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);**/
        helper.filterMethod(component, filterStatus);
        component.set("v.filterStatus",filterStatus);
    },
    
    handleSort : function(component, event, helper) {
        var bidsSorted = helper.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);
        //console.log('#bidsSorted = ' + JSON.stringify(bidsSorted));
    },
    
    openViewActions : function(component, event, helper) {
        var bidSelected = $(event.currentTarget).parents('.bid_buttons').data('serviceid');
        component.set("v.bidRecordId", bidSelected);
        /*component.set("v.bidSelected", bidSelected);
component.set("v.productionSelected", bidSelected);*/
        component.set("v.mainContent","vendorActions");
    },
    
    handleDocuments : function(component, event, helper){
        console.log('# handleDocuments()');
        var bidSelected = $(event.currentTarget).parents('.bid_buttons').data('serviceid');
        var productionName = "";
        var bidName = "";
        var bidsFiltered = component.get("v.bidsFiltered");
        bidsFiltered.forEach(bid => { if(bid.bidId == bidSelected){
                                     	productionName = bid.productionName;
                                     	bidName = bid.bidName;
                                     	//console.log('bid = ' + JSON.stringify(bid));
                                    }});
        
        component.set("v.productionName",productionName);
        component.set("v.bidName",bidName);
        
		component.set("v.serviceId", bidSelected);
		component.set("v.serviceType", $(event.currentTarget).parents('.bid_buttons').data('servicetype'));
        //component.set("v.serviceDateInAndOut", $(event.currentTarget).parents('.bid_buttons').data('servicedateinandout'));
        component.set("v.serviceDateInAndOut", $(event.currentTarget).parents('.bid_buttons').data('servicedatein').replace(/-/g, "/") + " - " + $(event.currentTarget).parents('.bid_buttons').data('servicedateout').replace(/-/g, "/"));
        component.set("v.serviceCityName", $(event.currentTarget).parents('.bid_buttons').data('servicecityname'));
		component.set("v.mainContent", "documents");
        
        console.log('# seviceId = ' + $(event.currentTarget).parents('.bid_buttons').data('serviceid'));
        console.log('# seviceId = ' + bidSelected);
    },
    
    openReservationDetail : function(component, event, helper) {
        var bidSelected = $(event.currentTarget).parents('.bid_buttons').data('serviceid');
        var productionName = "";
        var bidName = "";
        var bidsFiltered = component.get("v.bidsFiltered");
        bidsFiltered.forEach(bid => { if(bid.bidId == bidSelected) {
                                         productionName = bid.productionName;
                                         bidName = bid.bidName;
                                    }});
        component.set("v.productionName",productionName);
        component.set("v.bidName",bidName);
        component.set("v.bidRecordId",bidSelected);
        
        var userProfile = component.get("v.userProfile");
        console.log('# userProfile = ' + userProfile);
        if(userProfile == "GroundVendor") component.set("v.mainContent", "vendorReservationGTDetails");
        else if(userProfile == "HousingVendor" || userProfile == "CorporateVendor") component.set("v.mainContent", "vendorReservationHousingDetails");
        
        //component.set("v.mainContent","vendorReservationGTDetails");
    }
})
```
### VoyajerDashboardBids

```
<aura:component >
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="List" name="bids" />
    <aura:attribute type="List" name="bidsFiltered" />
    <aura:attribute type="String" name="bidRecordId" />
    <aura:attribute type="String" name="userProfile" />
    
    <aura:attribute type="List" name="productions" />
    <aura:attribute type="List" name="productionsFiltered" />
    <aura:attribute type="Boolean" name="isDashboardPillRead" default="false" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="filterStatus" default="View all" />
    <aura:attribute type="String" name="dashboardPillMessage" default="You have 1 bid with an action needed." />
    <aura:attribute type="String" name="startDateBegin" default="" />
    <aura:attribute type="String" name="startDateEnd" default="" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    
    <!--docs-->
    <aura:attribute name="serviceId" type="String"/>
    <aura:attribute name="serviceType" type="String"/>
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <!--end docs-->
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bids}" action="{!c.loadTable}" />
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
                    <div class="pageContentDashboard" style="margin-bottom: 2em;">
                        <lightning:pill label="{!v.dashboardPillMessage}" onremove="{!c.handleRemoveDashboardPill}" class="dashboardPill">
                            <aura:set attribute="media"><i class="fas fa-bell" style="margin-right: 0.5em;"></i></aura:set>
                        </lightning:pill>
                    </div>
                </aura:if>
                <!--<div style="margin-bottom: 1em; text-align: right;">
                    <lightning:button label="Create new production" variant="brand" iconName="utility:add" iconPosition="left" class="formButtonBrandLight" onclick="{!c.handleNewProduction}" />
                </div>-->
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <h3><i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em;"></i>Bids</h3>
                    </div>
                    <div class="page-section-buttons">
                        <div style="height: 2.5em;">
                            <lightning:button label="Won" 
                                              name="Won" 
                                              variant="{!if(v.filterStatus=='Won','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='Won','formButtonBrand','')}"
                                              value="Won"
                                              onclick="{!c.handleFilter}" />
                            <lightning:button label="Lost" 
                                              name="Lost" 
                                              variant="{!if(v.filterStatus=='Lost','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='Lost','formButtonBrand','')}" 
                                              value="Lost"
                                              onclick="{!c.handleFilter}" />
                            <lightning:button label="View all" 
                                              name="View all" 
                                              variant="{!if(v.filterStatus=='View all','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='View all','formButtonBrand','')}" 
                                              value="View all"
                                              onclick="{!c.handleFilter}" />
                            <!--Fix By Clay Dev 30 Jan 2021 #176564085-->
                            <lightning:button label="Cancelled" 
                                              name="Cancelled" 
                                              variant="{!if(v.filterStatus=='Cancelled','brand','neutral')}" 
                                              class="{!if(v.filterStatus=='Cancelled','formButtonBrand','')}" 
                                              value="Cancelled"
                                              onclick="{!c.handleFilter}" />
                            <lightning:buttonIcon iconName="utility:sync" variant="brand" class="formButtonBrandLight showOnMobile" onclick="{!c.doInit}" />
                        </div>
                        <div style="align-items: center; justify-content: flex-end; flex: 1;">
                            <p class="hideOnMobile" style="margin-right: 0.5em;">Sort by</p>
                            <lightning:select label="Sort" aura:id="sortBy" variant="label-hidden" class="slds-form-element-filter label-hidden" onchange="{!c.handleSort}">
                                <option value="productionNameAsc" selected="true">Production Name (A-Z)</option>
                                <option value="startDateAsc">Start Date (Asc)</option>
                                <option value="startDateDesc">Start Date (Desc)</option>
                                <option value="endDateAsc">End Date (Asc)</option>
                                <option value="endDateDesc">End Date (Desc)</option>
                            </lightning:select>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section" style="overflow-x: auto;">
                        <div class="productionTable">
                            <div class="productionTableHeader">
                                <div></div>
                                <div>Production Name</div>
                                <div>Start Date</div>
                                <div>End Date</div>
                                <div class="productionCompanyColumn">Company</div>
                                <div class="productionCompanyColumn">Location</div>
                                <!--<div>Bids Won</div>
                                <div>Bids Lost</div>-->
                                <div></div>
                            </div>
                            <div class="productionTableBody">
                                <aura:iteration items="{!v.bidsFiltered}" var="bid">
                                    <div class="productionTableRow">
                                        <div style="color: #e00000;">
                                            <aura:if isTrue="{!bid.isMissingAction}"><lightning:icon iconName="utility:notification" variant="error" size="xx-small"/></aura:if>
                                        </div>
                                        <div>{!bid.productionName}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!bid.startDate}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!bid.endDate}</div>
                                        <div class="productionCompanyColumn">{!bid.company}</div>
                                        <div class="productionCompanyColumn">{!bid.location}</div>
                                        <!--<div style="text-align: center; letter-spacing: 1px;">{!production.numBidsContracted}</div>
                                        <div style="text-align: center; letter-spacing: 1px;">{!production.numBidsCancelled}</div>-->
                                        
                                        <div class="bid_buttons" data-servicetype="{!bid.bidType}" data-serviceid="{!bid.bidId}" data-servicedateinandout="{!bid.startDate + ' - ' + bid.endDate}" data-servicecityname="{!bid.location}" data-servicedatein="{!bid.startDate}"  data-servicedateout="{!bid.endDate}">
                                            <!--Fix By Clay Dev 4 Feb, 2021 #176564085 -->
                                            <aura:if isTrue="{!v.filterStatus != 'Cancelled'}">
                                            <aura:if isTrue="{!bid.isMissingAction}">
                                                <!--<lightning:button label="Action Needed" variant="destructive" class="formButtonDestructive hideOnTablet" value="{!production.recordId}" onclick="{!c.openViewActions}" />-->
                                               	<button class="slds-button slds-button_neutral formButtonDestructive hideOnTablet" onclick="{!c.openViewActions}">Action Needed</button>
                                                <!--<lightning:buttonIcon iconName="utility:advertising" variant="destructive" class="formButtonDestructive showOnTablet" value="{!production.recordId}" onclick="{!c.openViewActions}" />-->
                                            </aura:if>
                                            <!--Fix By Clay Dev 4 Feb, 2021 #176564085 -->
                                            </aura:if>
                                            <!--<aura:if isTrue="{!production.status=='Active'? true : false}">
                                                <lightning:button label="Enter Itinerary" class="formButtonBrandInverse hideOnTablet" value="{!production.recordId}" onclick="{!c.openEnterItinerary}" />
                                                <lightning:buttonIcon iconName="utility:trail" class="formButtonBrandInverse showOnTablet" value="{!production.recordId}" onclick="{!c.openEnterItinerary}" />
                                            </aura:if>-->
                                            
                                            <button class="slds-button slds-button_brand formButtonBrandLight hideOnTablet" onclick="{!c.handleDocuments}">Documents</button>
                                            <!--<span class="showOnTablet" onclick="{!c.handleDocuments}"><lightning:icon iconName="action:add_file" alternativeText="Documents" title="Documents" /></span>
                                            <lightning:button label="Documents" variant="brand" class="formButtonBrandLight hideOnTablet" value="{!production.recordId}" onclick="{!c.handleDocuments}" />
                                            <lightning:buttonIcon iconName="utility:description" class="formButtonBrandLight showOnTablet" value="{!production.recordId}" onclick="{!c.handleDocuments}" />-->
                                            
                                            <button class="slds-button slds-button_neutral formButtonDestructiveInverse hideOnTablet" onclick="{!c.openReservationDetail}">View</button>
                                            <!-- <lightning:buttonIcon iconName="utility:description" class="formButtonDestructiveInverse showOnTablet" value="{!bid.productionId}" onclick="{!c.openReservationDetail}" /> -->
                                        </div>
                                    </div>
                                </aura:iteration>
                                <aura:if isTrue="{!empty(v.bidsFiltered)}">
                                    <div class="productionTableRow"><div></div><div style="text-align: left; font-style: italic;">No bids found.</div></div>
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
### VoyajerDashboardBids

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerDashboardBidsHelper

```
({
	sortMethod : function(component) {
        //console.log('# sortMethod');
        var bids = component.get("v.bidsFiltered");
        var sortValue = component.find("sortBy").get("v.value");
        
		if(sortValue == 'productionNameAsc'){
            //console.log('# productionNameAsc');
        	bids.sort((a, b) => a.productionName.localeCompare(b.productionName));
        }else if(sortValue == 'startDateAsc'){
            //console.log('# startDateAsc');
            bids.sort((a, b) => new Date(a.startDate) - new Date(b.startDate));
        }else if(sortValue == 'startDateDesc'){
            //console.log('# startDateDesc');
            bids.sort((a, b) => new Date(b.startDate) - new Date(a.startDate));
        }else if(sortValue == 'endDateAsc'){
            //console.log('# endDateAsc');
            bids.sort((a, b) => new Date(a.endDate) - new Date(b.endDate));
        }else if(sortValue == 'endDateDesc'){
            //console.log('# endDateDesc');
            bids.sort((a, b) => new Date(b.endDate) - new Date(a.endDate));
        }else if(sortValue == 'statusAsc'){
            //console.log('# statusAsc');
            bids.sort((a, b) => a.status.localeCompare(b.status));
        }
        
        //result
        return bids;
	},
    //Fix by Clay Dev 29 Jan, 2021 #176564085
    filterMethod : function(component, filterStatus) {
        var bids = component.get("v.bids");
        var bidsFiltered = [];
        
        bids.forEach(bid => {
            //Fix by Clay Dev 1 Feb, 2021 #176564085
            if(bid.bidStatus != undefined && bid.bidStatus != null) {
                if(filterStatus == "View all" && bid.bidStatus.toLowerCase() != "cancelled")
                    bidsFiltered.push(bid);
                else if(filterStatus == "Won" && bid.bidStatus.toLowerCase() == "contracted")
                    bidsFiltered.push(bid);
                else if (filterStatus == "Lost" && bid.bidStatus.toLowerCase() == "cancelled")
                    bidsFiltered.push(bid);
                else if (filterStatus == "Cancelled" && bid.bidStatus.toLowerCase() == "cancelled")
                    bidsFiltered.push(bid);
        	}
        });
       
        component.set("v.bidsFiltered", bidsFiltered);
        var bidsSorted = this.sortMethod(component);
        component.set("v.bidsFiltered", bidsSorted);
        
    }
})
```
### VoyajerDashboardBids

```
.THIS .startDateContainer {
    align-items: center;
    display: flex;
    border: 1px solid #dbdbdb;
    border-radius: 2em;
    padding: 0 0.75em;
    margin-right: 0.25em;
}

.THIS .startDateContainer .slds-input__icon {
    display: none;
}


.THIS .startDateInput {
    padding: 0 0.25em;
    text-align: center;
    border: none;
    max-width: 8em;
}

.THIS .startDateInput input {
    padding: 0 0.25em;
    text-align: center;
    border: none;
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
    flex: 1;
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
    flex: 1;
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

@media (max-width: 1200px) {
    .THIS .productionTableHeader > div:last-child,
    .THIS .productionTableRow > div:last-child {
        flex: none;
        width: 11em;
    }
}

@media (max-width: 1024px) {
    .THIS .startDateInput {
        max-width: 11em;
    }
}

@media (max-width: 550px) {
    .THIS .startDateContainer {
        flex-wrap: wrap;
        width: 100%;
        margin: 0;
    }
    
    .THIS .startDateInput {
        max-width: 9em;
    }
}

/*util*/
.THIS .label-hidden > label {
    display: none;
}
```

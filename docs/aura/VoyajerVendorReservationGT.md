---
layout: default
title: VoyajerVendorReservationGT
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerVendorReservationGT
## Fields
### VoyajerVendorReservationGTController

```
({
	doInit : function(component, event, helper) {
		var id = component.get("v.bidRecordId");
        console.log('# bidRecordId = ' + id);

        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadReservationGTDetail");
        callToParent.setParam("data",{
            detailRecordId: id
        });
        callToParent.fire();
	},
	handleBack : function(component, event, helper){
        component.set("v.mainContent", "dashboardBids");
	},
    handleDocuments : function(component, event, helper){
        var bidSelected = $(event.currentTarget).parents('.reservation_buttons').data('serviceid');
        var productionName = component.get("v.productionName");
        
        component.set("v.productionName",productionName);
		component.set("v.serviceId", bidSelected);
		component.set("v.serviceType", $(event.currentTarget).parents('.reservation_buttons').data('servicetype'));
        component.set("v.serviceDateInAndOut", $(event.currentTarget).parents('.reservation_buttons').data('servicedateinandout'));
        component.set("v.serviceCityName", $(event.currentTarget).parents('.reservation_buttons').data('servicecityname'));
		component.set("v.mainContent", "documents");
        
        console.log('# seviceId = ' + $(event.currentTarget).parents('.reservation_buttons').data('serviceid'));
        console.log('# seviceId = ' + bidSelected);
    }
})
```
### VoyajerVendorReservationGT

```
<aura:component >
    <!--HERE add mainContent to cmp param-->
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    
    <!-- reservation component -->
    <aura:attribute type="String" name="bidRecordId" />
    <aura:attribute type="Object" name="reservationDetail" />
    <aura:attribute type="List" name="lsReservationDetails" default="[]" />
    <aura:attribute type="String" name="officePreference" />
    <!--docs-->
    <aura:attribute name="serviceId" type="String"/>
    <aura:attribute name="serviceType" type="String"/>
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <aura:attribute type="String" name="agreementText" default="Company agrees to negotaite with Road Rebel ONLY moving forward and not offer lower rates directly. If either is breached, you
                                                                agree to pay Road Rebel commission on any trip booked with your company. This also serves as the commission agreement in 
                                                                the event we go to contract. By selecting Submit, you are signing this agreement electronically.*" />
    <!--end docs-->
    
	<aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            Reservation Details
                        </h1>
                        <lightning:button label="Back" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/><!--reservationDetail.length-->
                    </div>
                </div>
                <!-- content -->
                <div class="pageContentDashboard pageContentDashboardVendor">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters">
                            <div class="slds-col slds-size_1-of-2">
                                <h3><strong>{!v.productionName}</strong></h3>
                                <strong>{!v.reservationDetail.vendor}</strong>
                            </div>
                            <div class="slds-col slds-size_1-of-2" style="text-align:right;">
                                <div style="font-weight:bold;">Status: <span style="color:green;">{!v.reservationDetail.status}</span></div>
                                <div style="font-weight:bold;">{!v.reservationDetail.bidName}</div>
                                <div style="font-weight:bold;color:#00b4ff;text-transform:uppercase;">
                                    {!v.reservationDetail.startCity} {!if(v.reservationDetail.endCity != '',' to ' + v.reservationDetail.endCity,'')} | {!v.reservationDetail.startDate} - {!v.reservationDetail.endDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="pageContentDashboard pageContentDashboardVendor slds-m-bottom_large" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-border_top slds-border_bottom slds-border_left slds-border_right slds-p-horizontal_medium">
                        <div class="slds-grid slds-wrap slds-p-around_small">
                            <div class="slds-col slds-size_1-of-1">
                                <header class="slds-text-title_bold" style="color:#00b4ff;">TRIP DETAILS</header>
                            </div>
                        </div>
                        <aura:iteration items="{!v.reservationDetail.travels}" var="travel">
                            <div class="slds-p-vertical_small slds-border_top">
                                <header class="slds-grid slds-wrap">
                                    <div class="slds-col slds-size_4-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-bottom_xxx-small slds-text-title_bold">PICK UP</div>
                                        <div class="slds-p-vertical_xxx-small">
                                            <!--{!travel.startCity}<br/>-->
                                            {!travel.locationPickup}<br/>
                                            <span style="text-transform:uppercase;">{!travel.dayStart + ', ' + travel.dayNumberStart + ' ' + travel.monthStart + ' ' + travel.yearStart} | {!travel.startDateTime}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_4-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-bottom_xxx-small slds-text-title_bold">DROP OFF</div>
                                        <div class="slds-p-vertical_xxx-small">
                                            {!travel.startCity}<br/>
                                            <!--{!travel.endCity}<br/>-->
                                            {!travel.locationDropOff}<br/>
                                            <span style="text-transform:uppercase;">{!travel.dayEnd + ', ' + travel.dayNumberEnd + ' ' + travel.monthEnd + ' ' + travel.yearEnd} | {!travel.endDateTime}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_4-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-bottom_xxx-small slds-text-title_bold">TRIP DESCRIPTION</div>
                                        <div class="slds-p-vertical_xxx-small">
                                            <span>{!travel.description}</span>
                                        </div>
                                    </div>
                                </header>
                                <div class="slds-grid slds-wrap slds-p-top_small">
                                    <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small">
                                        <aura:iteration items="{!v.reservationDetail.vehicles}" var="vehicle">
                                            <div class="slds-p-top_xxx-small"><strong>{!vehicle.vehicleName}</strong></div>
                                        </aura:iteration>
                                    </div>
                                    <div class="slds-col slds-size_11-of-12 slds-p-horizontal_small">
                                        <aura:iteration items="{!v.reservationDetail.vehicles}" var="vehicle">
                                            <div class="slds-p-top_xxx-small">
                                                {!if(vehicle.vehicleType != null, vehicle.vehicleType + ' | ','')}
                                                {!if(and(vehicle.make != null,vehicle.model != null),vehicle.make + '/',vehicle.make)}{!vehicle.model} 
                                                {!if(vehicle.year != null,' ' + vehicle.year,'')} | {!if(and(vehicle.capacity != null,vehicle.capacity != ''),vehicle.capacity + ' PAX - ','')}
                                                {!if(vehicle.amenities != null, vehicle.amenities,'')}
                                            </div>
                                        </aura:iteration>
                                    </div>
                                </div>
                            </div>
                        </aura:iteration>
                        <div class="slds-p-vertical_small slds-border_top">
                            <div class="slds-grid slds-p-bottom_small">
                                <div class="slds-col slds-size_10-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong>GRATUITY</strong>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <lightning:formattedNumber value="{!if(v.reservationDetail.gratuity > 0, v.reservationDetail.gratuity, '0')}" style="currency" currencyCode="{!v.reservationDetail.currencyIsoCode}"/>
                                </div>
                            </div>
                            <div class="slds-grid slds-p-bottom_small">
                                <div class="slds-col slds-size_10-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong>BASE COST</strong>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <lightning:formattedNumber value="{!if(v.reservationDetail.baseCost > 0, v.reservationDetail.baseCost, '0')}" style="currency" currencyCode="{!v.reservationDetail.currencyIsoCode}"/>
                                </div>
                            </div>
                            <div class="slds-grid">
                                <div class="slds-col slds-size_10-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong style="color:green;">TOTAL PRICE</strong>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong>
                                        <lightning:formattedNumber value="{!if(v.reservationDetail.totalPrice > 0, v.reservationDetail.totalPrice, '0')}" style="currency" currencyCode="{!v.reservationDetail.currencyIsoCode}"/>
                                    </strong>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="slds-p-vertical_medium slds-p-horizontal_medium">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Additional Fees &amp; Details</strong>
                                <aura:iteration items="{!v.reservationDetail.concessions}" var="concession">
                                    <div class="slds-p-top_xxx-small">
                                        &bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c+': ','')}&nbsp;{!concession.Rate__c}
                                        , {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' in rate','')}
                                    </div>
                                </aura:iteration>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Additional Notes</strong>
                                <p>
                                    {!v.reservationDetail.additionalInformation}
                                </p>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Road Rebel Commission</strong>
                                <div>
                                    Standard {!if(v.reservationDetail.rate > 0, v.reservationDetail.rate, '0')}%
                                    <!-- {!v.reservationDetail.rate}% -->
                                </div>
                            </div>
                        </div>
                        <aura:if isTrue="{!v.reservationDetail.record.Property_Agrees__c}">
                            <div class="slds-grid slds-p-top_medium">
                                <div class="slds-col slds-size_1-of-1">
                                    <br/>
                                    <p>{!v.agreementText}</p>
                                </div>
                            </div>
                            <div class="slds-grid slds-p-top_medium">
                                <div class="slds-col slds-size_1-of-1">
                                    <strong>Signed by</strong>
                                    <p>{!v.reservationDetail.record.responseVendorName__c}</p>
                                    <p>{!v.reservationDetail.record.responseVendorTitle__c}</p>
                                    <p>{!v.reservationDetail.record.responseVendorEmail__c}</p>
                                    <p>{!v.reservationDetail.record.responseVendorPhone__c}</p>
                                </div>
                            </div>
                        </aura:if>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1 slds-text-align_right reservation_buttons" data-servicetype="GT Bid" data-serviceid="{!v.reservationDetail.recordId}" data-servicedateinandout="{!v.reservationDetail.startDate + ' - ' + v.reservationDetail.endDate}" data-servicecityname="{!v.reservationDetail.startCity}">
                                <button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleDocuments}">DOCUMENTS</button>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- end content -->
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerVendorReservationGT

```
.THIS {}
```
### VoyajerVendorReservationGT

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorReservationGTController

```
({
	doInit : function(component, event, helper) {
		var id = component.get("v.bidRecordId");
        console.log('# bidRecordId = ' + id);

        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadReservationGTDetail");
        callToParent.setParam("data",{
            detailRecordId: id
        });
        callToParent.fire();
	},
	handleBack : function(component, event, helper){
        component.set("v.mainContent", "dashboardBids");
	},
    handleDocuments : function(component, event, helper){
        var bidSelected = $(event.currentTarget).parents('.reservation_buttons').data('serviceid');
        var productionName = component.get("v.productionName");
        
        component.set("v.productionName",productionName);
		component.set("v.serviceId", bidSelected);
		component.set("v.serviceType", $(event.currentTarget).parents('.reservation_buttons').data('servicetype'));
        component.set("v.serviceDateInAndOut", $(event.currentTarget).parents('.reservation_buttons').data('servicedateinandout'));
        component.set("v.serviceCityName", $(event.currentTarget).parents('.reservation_buttons').data('servicecityname'));
		component.set("v.mainContent", "documents");
        
        console.log('# seviceId = ' + $(event.currentTarget).parents('.reservation_buttons').data('serviceid'));
        console.log('# seviceId = ' + bidSelected);
    }
})
```
### VoyajerVendorReservationGT

```
<aura:component >
    <!--HERE add mainContent to cmp param-->
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    
    <!-- reservation component -->
    <aura:attribute type="String" name="bidRecordId" />
    <aura:attribute type="Object" name="reservationDetail" />
    <aura:attribute type="List" name="lsReservationDetails" default="[]" />
    <aura:attribute type="String" name="officePreference" />
    <!--docs-->
    <aura:attribute name="serviceId" type="String"/>
    <aura:attribute name="serviceType" type="String"/>
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <aura:attribute type="String" name="agreementText" default="Company agrees to negotaite with Road Rebel ONLY moving forward and not offer lower rates directly. If either is breached, you
                                                                agree to pay Road Rebel commission on any trip booked with your company. This also serves as the commission agreement in 
                                                                the event we go to contract. By selecting Submit, you are signing this agreement electronically.*" />
    <!--end docs-->
    
	<aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            Reservation Details
                        </h1>
                        <lightning:button label="Back" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/><!--reservationDetail.length-->
                    </div>
                </div>
                <!-- content -->
                <div class="pageContentDashboard pageContentDashboardVendor">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters">
                            <div class="slds-col slds-size_1-of-2">
                                <h3><strong>{!v.productionName}</strong></h3>
                                <strong>{!v.reservationDetail.vendor}</strong>
                            </div>
                            <div class="slds-col slds-size_1-of-2" style="text-align:right;">
                                <div style="font-weight:bold;">Status: <span style="color:green;">{!v.reservationDetail.status}</span></div>
                                <div style="font-weight:bold;">{!v.reservationDetail.bidName}</div>
                                <div style="font-weight:bold;color:#00b4ff;text-transform:uppercase;">
                                    {!v.reservationDetail.startCity} {!if(v.reservationDetail.endCity != '',' to ' + v.reservationDetail.endCity,'')} | {!v.reservationDetail.startDate} - {!v.reservationDetail.endDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="pageContentDashboard pageContentDashboardVendor slds-m-bottom_large" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-border_top slds-border_bottom slds-border_left slds-border_right slds-p-horizontal_medium">
                        <div class="slds-grid slds-wrap slds-p-around_small">
                            <div class="slds-col slds-size_1-of-1">
                                <header class="slds-text-title_bold" style="color:#00b4ff;">TRIP DETAILS</header>
                            </div>
                        </div>
                        <aura:iteration items="{!v.reservationDetail.travels}" var="travel">
                            <div class="slds-p-vertical_small slds-border_top">
                                <header class="slds-grid slds-wrap">
                                    <div class="slds-col slds-size_4-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-bottom_xxx-small slds-text-title_bold">PICK UP</div>
                                        <div class="slds-p-vertical_xxx-small">
                                            <!--{!travel.startCity}<br/>-->
                                            {!travel.locationPickup}<br/>
                                            <span style="text-transform:uppercase;">{!travel.dayStart + ', ' + travel.dayNumberStart + ' ' + travel.monthStart + ' ' + travel.yearStart} | {!travel.startDateTime}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_4-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-bottom_xxx-small slds-text-title_bold">DROP OFF</div>
                                        <div class="slds-p-vertical_xxx-small">
                                            {!travel.startCity}<br/>
                                            <!--{!travel.endCity}<br/>-->
                                            {!travel.locationDropOff}<br/>
                                            <span style="text-transform:uppercase;">{!travel.dayEnd + ', ' + travel.dayNumberEnd + ' ' + travel.monthEnd + ' ' + travel.yearEnd} | {!travel.endDateTime}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_4-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-bottom_xxx-small slds-text-title_bold">TRIP DESCRIPTION</div>
                                        <div class="slds-p-vertical_xxx-small">
                                            <span>{!travel.description}</span>
                                        </div>
                                    </div>
                                </header>
                                <div class="slds-grid slds-wrap slds-p-top_small">
                                    <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small">
                                        <aura:iteration items="{!v.reservationDetail.vehicles}" var="vehicle">
                                            <div class="slds-p-top_xxx-small"><strong>{!vehicle.vehicleName}</strong></div>
                                        </aura:iteration>
                                    </div>
                                    <div class="slds-col slds-size_11-of-12 slds-p-horizontal_small">
                                        <aura:iteration items="{!v.reservationDetail.vehicles}" var="vehicle">
                                            <div class="slds-p-top_xxx-small">
                                                {!if(vehicle.vehicleType != null, vehicle.vehicleType + ' | ','')}
                                                {!if(and(vehicle.make != null,vehicle.model != null),vehicle.make + '/',vehicle.make)}{!vehicle.model} 
                                                {!if(vehicle.year != null,' ' + vehicle.year,'')} | {!if(and(vehicle.capacity != null,vehicle.capacity != ''),vehicle.capacity + ' PAX - ','')}
                                                {!if(vehicle.amenities != null, vehicle.amenities,'')}
                                            </div>
                                        </aura:iteration>
                                    </div>
                                </div>
                            </div>
                        </aura:iteration>
                        <div class="slds-p-vertical_small slds-border_top">
                            <div class="slds-grid slds-p-bottom_small">
                                <div class="slds-col slds-size_10-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong>GRATUITY</strong>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <lightning:formattedNumber value="{!if(v.reservationDetail.gratuity > 0, v.reservationDetail.gratuity, '0')}" style="currency" currencyCode="{!v.reservationDetail.currencyIsoCode}"/>
                                </div>
                            </div>
                            <div class="slds-grid slds-p-bottom_small">
                                <div class="slds-col slds-size_10-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong>BASE COST</strong>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <lightning:formattedNumber value="{!if(v.reservationDetail.baseCost > 0, v.reservationDetail.baseCost, '0')}" style="currency" currencyCode="{!v.reservationDetail.currencyIsoCode}"/>
                                </div>
                            </div>
                            <div class="slds-grid">
                                <div class="slds-col slds-size_10-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong style="color:green;">TOTAL PRICE</strong>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small slds-text-align_right">
                                    <strong>
                                        <lightning:formattedNumber value="{!if(v.reservationDetail.totalPrice > 0, v.reservationDetail.totalPrice, '0')}" style="currency" currencyCode="{!v.reservationDetail.currencyIsoCode}"/>
                                    </strong>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="slds-p-vertical_medium slds-p-horizontal_medium">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Additional Fees &amp; Details</strong>
                                <aura:iteration items="{!v.reservationDetail.concessions}" var="concession">
                                    <div class="slds-p-top_xxx-small">
                                        &bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c+': ','')}&nbsp;{!concession.Rate__c}
                                        , {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' in rate','')}
                                    </div>
                                </aura:iteration>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Additional Notes</strong>
                                <p>
                                    {!v.reservationDetail.additionalInformation}
                                </p>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Road Rebel Commission</strong>
                                <div>
                                    Standard {!if(v.reservationDetail.rate > 0, v.reservationDetail.rate, '0')}%
                                    <!-- {!v.reservationDetail.rate}% -->
                                </div>
                            </div>
                        </div>
                        <aura:if isTrue="{!v.reservationDetail.record.Property_Agrees__c}">
                            <div class="slds-grid slds-p-top_medium">
                                <div class="slds-col slds-size_1-of-1">
                                    <br/>
                                    <p>{!v.agreementText}</p>
                                </div>
                            </div>
                            <div class="slds-grid slds-p-top_medium">
                                <div class="slds-col slds-size_1-of-1">
                                    <strong>Signed by</strong>
                                    <p>{!v.reservationDetail.record.responseVendorName__c}</p>
                                    <p>{!v.reservationDetail.record.responseVendorTitle__c}</p>
                                    <p>{!v.reservationDetail.record.responseVendorEmail__c}</p>
                                    <p>{!v.reservationDetail.record.responseVendorPhone__c}</p>
                                </div>
                            </div>
                        </aura:if>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1 slds-text-align_right reservation_buttons" data-servicetype="GT Bid" data-serviceid="{!v.reservationDetail.recordId}" data-servicedateinandout="{!v.reservationDetail.startDate + ' - ' + v.reservationDetail.endDate}" data-servicecityname="{!v.reservationDetail.startCity}">
                                <button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleDocuments}">DOCUMENTS</button>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- end content -->
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerVendorReservationGT

```
.THIS {}
```
### VoyajerVendorReservationGT

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

---
layout: default
title: VoyajerVendorReservationHousing
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerVendorReservationHousing
## Fields
### VoyajerVendorReservationHousing

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorReservationHousing

```
<aura:component >
    <!--HERE add mainContent to cmp param-->
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    
    <!-- reservation component -->
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="bidRecordId" />
    <aura:attribute type="Object" name="reservationDetail" />
    <aura:attribute type="String" name="officePreference" />
    <!--docs-->
    <aura:attribute name="serviceId" type="String"/>
    <aura:attribute name="serviceType" type="String"/>
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <aura:attribute type="String" name="agreementText" default="Property agrees to negotiate with Road Rebel ONLY moving forward and not offer client lower rates directly. If either is breached, 
                                                                you agree to pay Road Rebel commission on any room pick-up at your property(s). This also serves as the commission agreement in the event we go to contract.
                                                                By selecting Submit, you are signing this agreement electronically.*" />
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
                        <lightning:button label="Back" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/>
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
                                    {!v.reservationDetail.city} | {!v.reservationDetail.startDate} - {!v.reservationDetail.endDate}
                                </div>
                                <div style="font-weight:bold;">Room Release Date: <span style="text-transform:uppercase;">{!v.reservationDetail.roomReleaseDate}</span></div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="pageContentDashboard pageContentDashboardVendor slds-m-bottom_large" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-border_top slds-border_bottom slds-border_left slds-border_right slds-p-horizontal_small" style="text-align:left;">
                        <div class="slds-grid slds-wrap slds-p-around_small">
                            <div class="slds-col slds-size_1-of-1">
                                <header class="slds-text-title_bold" style="color:#00b4ff;">STAY DETAILS</header>
                            </div>
                        </div>
                        
                        <div class="slds-p-vertical_small slds-border_top">
                            <header class="slds-grid slds-wrap">
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">CHECK-IN</div>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_xxx-small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">CHECK-OUT</div>
                                </div>
                                <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">ROOMS</div>
                                </div>
                                <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">ROOM DESCRIPTION</div>
                                </div>
                                <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">SPECIAL CONSIDERATIONS</div>
                                </div>
                                <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">RATE</div>
                                </div>
                            </header>
                            <aura:iteration items="{!v.reservationDetail.roomTypes}" var="roomType">
                                <div class="slds-grid slds-wrap slds-p-top_small">
                                    <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-vertical_xxx-small">
                                            <span style="text-transform:uppercase;">{!roomType.Date_In_Text__c}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_2-of-12 slds-p-horizontal_xxx-small">
                                        <div class="slds-p-vertical_xxx-small">
                                            <span style="text-transform:uppercase;">{!roomType.Date_Out_Text__c}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small slds-text-align_center">
                                        <div class="slds-p-vertical_xxx-small">
                                            {!roomType.Units__c}
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-vertical_xxx-small">
                                            {!roomType.Unit_Type__c}
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-vertical_xxx-small">
                                            {!roomType.Special_Notes__c}
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small slds-text-align_right">
                                        <div class="slds-p-vertical_xxx-small">
                                            <!--$<span>{!roomType.Rate__c}</span>-->
                                            <lightning:formattedNumber value="{!if(roomType.Rate__c > 0, roomType.Rate__c, '0')}" style="currency" currencyCode="{!v.reservationDetail.rateDetails.CurrencyIsoCode}"/>
                                            <!--{!if(roomType.Rate__c > 0, roomType.Rate__c, '0')}-->
                                        </div>
                                    </div>
                                </div>
                            </aura:iteration>
                        </div>
                    </div>
                    
                    <div class="slds-p-vertical_medium slds-p-horizontal_medium">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Currency</strong>
                                <p>
                                    {!v.reservationDetail.rateDetails.CurrencyIsoCode}
                                </p>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Tax / Surcharge</strong>
                                <p>
                                    {!v.reservationDetail.rateDetails.Tax__c}%&nbsp;{!if(v.reservationDetail.rateDetails.Tax_Included__c == true,'Included','Not Included')}&nbsp;/&nbsp;
                                    <span>
                                        <aura:if isTrue="{!v.reservationDetail.rateDetails.Surcharge__c != null}">
                                            <lightning:formattedNumber value="{!v.reservationDetail.rateDetails.Surcharge__c}" 
                                                                       style="currency" 
                                                                       minimumFractionDigits="2" 
                                                                       maximumFractionDigits="2" 
                                                                       currencyCode="{!if(v.reservationDetail.rateDetails.CurrencyIsoCode != null,v.reservationDetail.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            &nbsp;{!if(v.reservationDetail.rateDetails.Surcharge_included__c == true,'Included','Not Included')}
                                            <aura:set attribute="else">No Surcharge</aura:set>
                                        </aura:if>
                                    </span>
                                </p>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Concessions</strong>
                                <aura:iteration items="{!v.reservationDetail.concessions}" var="concession">
                                    <div class="slds-p-top_xxx-small">
                                        &bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c,'')} {!if(concession.Concession_Provided__c != null, ' - ' + concession.Concession_Provided__c,'')}
                                    </div>
                                </aura:iteration>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Road Rebel Commission</strong>
                                <aura:if isTrue="{!empty(v.reservationDetail.rateDetails.Id)}">
                                    <div>-</div>
                                     <aura:set attribute="else">
                                         <aura:if isTrue="{!v.reservationDetail.rateDetails.Commission_Type__c == 'Percentage'}">
                                             <div>{!v.reservationDetail.rateDetails.Commission_Percent__c}% commission on a total rate</div>
                                         </aura:if>
                                         <aura:if isTrue="{!v.reservationDetail.rateDetails.Commission_Type__c == 'Amount'}">
                                             <div><lightning:formattedNumber value="{!if(v.reservationDetail.rateDetails.Commission__c > 0, v.reservationDetail.rateDetails.Commission__c, '0')}" style="currency" currencyCode="{!v.reservationDetail.rateDetails.CurrencyIsoCode}"/> commission on a total rate</div>
                                         </aura:if>
                                    </aura:set>
                                </aura:if>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Additional Notes</strong>
                                <p>
                                    {!if(empty(v.reservationDetail.additionalInformation),'-',v.reservationDetail.additionalInformation)}
                                </p>
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
                            <div class="slds-col slds-size_1-of-1 slds-text-align_right reservation_buttons" data-servicetype="Housing Bid" data-serviceid="{!v.reservationDetail.recordId}" data-servicedateinandout="{!v.reservationDetail.startDate + ' - ' + v.reservationDetail.endDate}" data-servicecityname="{!v.reservationDetail.city}">
                                <aura:if isTrue="{!v.reservationDetail.isClouseOutAvailable}">
                                    <button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.openHousingCloseOut}">PICK UP</button>
                                </aura:if>
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
### VoyajerVendorReservationHousingController

```
({
	doInit : function(component, event, helper) {
		var id = component.get("v.bidRecordId");
        console.log('# bidRecordId = ' + id);

        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadReservationHousingDetail");
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
    },
    openHousingCloseOut : function(component, event, helper) {
        console.log("openHousingCloseOut");
        var record = component.get("v.reservationDetail").record;
        component.set("v.serviceId",record.Housing__c);
        component.set("v.mainContent","closeOutHousing");
        /*
        var itineraries = component.get("v.itineraries");
        var service = '';
        console.log(itineraries);
        if(!!recordId) itineraries.forEach(itinerary => { if(itinerary.serviceId == recordId) service = itinerary.service; });
        console.log("# service = " + service);
        console.log("# recordId = " + recordId);
        if(!!service && !!recordId) {
            component.set("v.optionRecordId",recordId);
            if(service == 'Housing Bid') component.set("v.mainContent","closeOutHousing");
            //if(service == 'GT Bid') component.set("v.mainContent","bidVendorGround");
            //if(service == 'air') component.set("v.mainContent","optionsAir");
            //if(service == 'Freight Bid') component.set("v.mainContent","optionsFreight");
        }
        */
    }
})
```
### VoyajerVendorReservationHousing

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorReservationHousing

```
<aura:component >
    <!--HERE add mainContent to cmp param-->
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    
    <!-- reservation component -->
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="bidRecordId" />
    <aura:attribute type="Object" name="reservationDetail" />
    <aura:attribute type="String" name="officePreference" />
    <!--docs-->
    <aura:attribute name="serviceId" type="String"/>
    <aura:attribute name="serviceType" type="String"/>
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <aura:attribute type="String" name="agreementText" default="Property agrees to negotiate with Road Rebel ONLY moving forward and not offer client lower rates directly. If either is breached, 
                                                                you agree to pay Road Rebel commission on any room pick-up at your property(s). This also serves as the commission agreement in the event we go to contract.
                                                                By selecting Submit, you are signing this agreement electronically.*" />
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
                        <lightning:button label="Back" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/>
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
                                    {!v.reservationDetail.city} | {!v.reservationDetail.startDate} - {!v.reservationDetail.endDate}
                                </div>
                                <div style="font-weight:bold;">Room Release Date: <span style="text-transform:uppercase;">{!v.reservationDetail.roomReleaseDate}</span></div>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="pageContentDashboard pageContentDashboardVendor slds-m-bottom_large" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-border_top slds-border_bottom slds-border_left slds-border_right slds-p-horizontal_small" style="text-align:left;">
                        <div class="slds-grid slds-wrap slds-p-around_small">
                            <div class="slds-col slds-size_1-of-1">
                                <header class="slds-text-title_bold" style="color:#00b4ff;">STAY DETAILS</header>
                            </div>
                        </div>
                        
                        <div class="slds-p-vertical_small slds-border_top">
                            <header class="slds-grid slds-wrap">
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">CHECK-IN</div>
                                </div>
                                <div class="slds-col slds-size_2-of-12 slds-p-horizontal_xxx-small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">CHECK-OUT</div>
                                </div>
                                <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">ROOMS</div>
                                </div>
                                <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">ROOM DESCRIPTION</div>
                                </div>
                                <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">SPECIAL CONSIDERATIONS</div>
                                </div>
                                <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small">
                                    <div class="slds-p-bottom_xxx-small slds-text-title_bold">RATE</div>
                                </div>
                            </header>
                            <aura:iteration items="{!v.reservationDetail.roomTypes}" var="roomType">
                                <div class="slds-grid slds-wrap slds-p-top_small">
                                    <div class="slds-col slds-size_2-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-vertical_xxx-small">
                                            <span style="text-transform:uppercase;">{!roomType.Date_In_Text__c}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_2-of-12 slds-p-horizontal_xxx-small">
                                        <div class="slds-p-vertical_xxx-small">
                                            <span style="text-transform:uppercase;">{!roomType.Date_Out_Text__c}</span>
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small slds-text-align_center">
                                        <div class="slds-p-vertical_xxx-small">
                                            {!roomType.Units__c}
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-vertical_xxx-small">
                                            {!roomType.Unit_Type__c}
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_3-of-12 slds-p-horizontal_small">
                                        <div class="slds-p-vertical_xxx-small">
                                            {!roomType.Special_Notes__c}
                                        </div>
                                    </div>
                                    <div class="slds-col slds-size_1-of-12 slds-p-horizontal_small slds-text-align_right">
                                        <div class="slds-p-vertical_xxx-small">
                                            <!--$<span>{!roomType.Rate__c}</span>-->
                                            <lightning:formattedNumber value="{!if(roomType.Rate__c > 0, roomType.Rate__c, '0')}" style="currency" currencyCode="{!v.reservationDetail.rateDetails.CurrencyIsoCode}"/>
                                            <!--{!if(roomType.Rate__c > 0, roomType.Rate__c, '0')}-->
                                        </div>
                                    </div>
                                </div>
                            </aura:iteration>
                        </div>
                    </div>
                    
                    <div class="slds-p-vertical_medium slds-p-horizontal_medium">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Currency</strong>
                                <p>
                                    {!v.reservationDetail.rateDetails.CurrencyIsoCode}
                                </p>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Tax / Surcharge</strong>
                                <p>
                                    {!v.reservationDetail.rateDetails.Tax__c}%&nbsp;{!if(v.reservationDetail.rateDetails.Tax_Included__c == true,'Included','Not Included')}&nbsp;/&nbsp;
                                    <span>
                                        <aura:if isTrue="{!v.reservationDetail.rateDetails.Surcharge__c != null}">
                                            <lightning:formattedNumber value="{!v.reservationDetail.rateDetails.Surcharge__c}" 
                                                                       style="currency" 
                                                                       minimumFractionDigits="2" 
                                                                       maximumFractionDigits="2" 
                                                                       currencyCode="{!if(v.reservationDetail.rateDetails.CurrencyIsoCode != null,v.reservationDetail.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            &nbsp;{!if(v.reservationDetail.rateDetails.Surcharge_included__c == true,'Included','Not Included')}
                                            <aura:set attribute="else">No Surcharge</aura:set>
                                        </aura:if>
                                    </span>
                                </p>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Concessions</strong>
                                <aura:iteration items="{!v.reservationDetail.concessions}" var="concession">
                                    <div class="slds-p-top_xxx-small">
                                        &bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c,'')} {!if(concession.Concession_Provided__c != null, ' - ' + concession.Concession_Provided__c,'')}
                                    </div>
                                </aura:iteration>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Road Rebel Commission</strong>
                                <aura:if isTrue="{!empty(v.reservationDetail.rateDetails.Id)}">
                                    <div>-</div>
                                     <aura:set attribute="else">
                                         <aura:if isTrue="{!v.reservationDetail.rateDetails.Commission_Type__c == 'Percentage'}">
                                             <div>{!v.reservationDetail.rateDetails.Commission_Percent__c}% commission on a total rate</div>
                                         </aura:if>
                                         <aura:if isTrue="{!v.reservationDetail.rateDetails.Commission_Type__c == 'Amount'}">
                                             <div><lightning:formattedNumber value="{!if(v.reservationDetail.rateDetails.Commission__c > 0, v.reservationDetail.rateDetails.Commission__c, '0')}" style="currency" currencyCode="{!v.reservationDetail.rateDetails.CurrencyIsoCode}"/> commission on a total rate</div>
                                         </aura:if>
                                    </aura:set>
                                </aura:if>
                            </div>
                        </div>
                        <div class="slds-grid slds-p-top_medium">
                            <div class="slds-col slds-size_1-of-1">
                                <strong>Additional Notes</strong>
                                <p>
                                    {!if(empty(v.reservationDetail.additionalInformation),'-',v.reservationDetail.additionalInformation)}
                                </p>
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
                            <div class="slds-col slds-size_1-of-1 slds-text-align_right reservation_buttons" data-servicetype="Housing Bid" data-serviceid="{!v.reservationDetail.recordId}" data-servicedateinandout="{!v.reservationDetail.startDate + ' - ' + v.reservationDetail.endDate}" data-servicecityname="{!v.reservationDetail.city}">
                                <aura:if isTrue="{!v.reservationDetail.isClouseOutAvailable}">
                                    <button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.openHousingCloseOut}">PICK UP</button>
                                </aura:if>
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
### VoyajerVendorReservationHousingController

```
({
	doInit : function(component, event, helper) {
		var id = component.get("v.bidRecordId");
        console.log('# bidRecordId = ' + id);

        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadReservationHousingDetail");
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
    },
    openHousingCloseOut : function(component, event, helper) {
        console.log("openHousingCloseOut");
        var record = component.get("v.reservationDetail").record;
        component.set("v.serviceId",record.Housing__c);
        component.set("v.mainContent","closeOutHousing");
        /*
        var itineraries = component.get("v.itineraries");
        var service = '';
        console.log(itineraries);
        if(!!recordId) itineraries.forEach(itinerary => { if(itinerary.serviceId == recordId) service = itinerary.service; });
        console.log("# service = " + service);
        console.log("# recordId = " + recordId);
        if(!!service && !!recordId) {
            component.set("v.optionRecordId",recordId);
            if(service == 'Housing Bid') component.set("v.mainContent","closeOutHousing");
            //if(service == 'GT Bid') component.set("v.mainContent","bidVendorGround");
            //if(service == 'air') component.set("v.mainContent","optionsAir");
            //if(service == 'Freight Bid') component.set("v.mainContent","optionsFreight");
        }
        */
    }
})
```

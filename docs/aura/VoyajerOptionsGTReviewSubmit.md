---
layout: default
title: VoyajerOptionsGTReviewSubmit
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsGTReviewSubmit
## Fields
### VoyajerOptionsGTReviewSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsGTReviewSubmitController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadOptionsGTDetail");
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    backOptionsGT: function(component,event,helper){
        component.set("v.mainContent","optionsGT");
    },
    submitSelection: function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","submitOptionSelected");
        callToParent.setParam("data",{
            serviceType: "ground",
            serviceId: component.get("v.groundId"),
            serviceName: component.get("v.serviceData").recordName,
            bidVendorName: component.get("v.optionDetailRecord").vendor,
            bidVendorId: component.get("v.optionDetailRecord").vendorId,
            bidId: component.get("v.optionDetailRecord").recordId,
            comments: component.get("v.comments")
        });
        callToParent.fire();
    }
})
```
### VoyajerOptionsGTReviewSubmit

```
<aura:component>
    <aura:attribute type="String" name="groundId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="comments" default="" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fab fa-telegram-plane" style="color: #9f9f9f; margin-right: 0.5em;"></i>Review &amp; Submit
                        </h1>
                        <lightning:button label="BACK TO THE OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsGT}" />
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(v.serviceData.endCityName != null,' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                            	<p>Group Type: {!v.serviceData.groupType}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <section class="page-section slds-card-overview">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside slds-card-overview_icon">
                                <i class="fas fa-bus icon"></i>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-overview_item-content slds-card-overview_header">
                                <header class="slds-grid">
                                    <h3>
                                        {!v.optionDetailRecord.vendor}
                                    </h3>
                                </header>
                            </div>
                        </div>
                        <aura:iteration items="{!v.optionDetailRecord.travels}" var="travel">
                            <article class="slds-grid slds-wrap slds-card-overview_item">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside">
                                    <div class="slds-media slds-media_responsive">
                                        <div class="slds-media__figure" style="margin-top:10px;margin-right:0;">
                                            <span class="slds-left_day">
                                                <span class="small">{!travel.dayStart}</span> <br/>
                                                <span class="big">{!travel.dayNumberStart}</span> <br/>
                                                <span class="small">{!travel.monthStart}</span> <br/>
                                            </span>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-overview_item-content-item">
                                    <header class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12 slds-box-item slds-p-horizontal_small">
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 title">
                                                    <!--{!travel.startCity}-->
                                                    {!travel.startCityShortName}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-7 arrow">
                                                    <i class="fas fa-arrow-right"></i>
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 title">
                                                    <!--{!travel.endCity}-->
                                                    {!travel.endCityShortName}
                                                </div>                                            
                                            </div>
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    {!travel.locationType}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-7 arrow"></div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    <!--{!travel.locationDropOff}-->
                                                    {!travel.locationDropOffType}
                                                </div>
                                            </div>
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    {!travel.startDateTime}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-7 arrow"></div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    {!travel.endDateTime}
                                                </div>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12 slds-text-align_right slds-p-horizontal_small">
                                            <div>
                                            	<span style="font-weight:bold;">Trip Type: </span><span>{!travel.tripType}</span> | <span>{!travel.capacity}</span> Passengers
                                            </div>
                                            <div>
                                                <span style="font-weight:bold;">Gear/Luggage Space Needed: </span><span>{!travel.gearLuggage}</span>
                                            </div>
                                        </div>
                                    </header>
                                    <div class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-box-item-detail">
                                            <div>PICK UP</div>
                                            <div>DROP OFF</div>
                                            <div>BUS TYPE</div>
                                            <aura:iteration items="{!v.optionDetailRecord.vehicles}" var="vehicle">
                                                <aura:if isTrue="{!if(travel.vehicleId == vehicle.vehicleId,true,false)}"><!--filter for only show vehicles related to this travel -->
                                                	<div>{!vehicle.vehicleName}</div>
                                                </aura:if>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-box-item-detail-info">
                                            <div>
                                                <span style="text-transform:uppercase;">{!travel.dayStart + ', ' + travel.dayNumberStart + ' ' + travel.monthStart + ' ' + travel.yearStart}</span> | {!travel.startDateTime} from {!travel.startCity} ({!travel.locationType})
                                            </div>
                                            <div>
                                                <span style="text-transform:uppercase;">{!travel.dayEnd + ', ' + travel.dayNumberEnd + ' ' + travel.monthEnd + ' ' + travel.yearEnd}</span> | {!travel.endDateTime} {!travel.endCity} <!--({!travel.locationDropOff})--> ({!travel.locationDropOffType})
                                            </div>
                                            <div>{!if(and(travel.vehicleType != null,travel.vehicleType != ''),travel.vehicleType,'&nbsp;')}</div>
                                            <aura:iteration items="{!v.optionDetailRecord.vehicles}" var="vehicle">
                                                <aura:if isTrue="{!if(travel.vehicleId == vehicle.vehicleId,true,false)}">
                                                    <div>
                                                        {!if(and(vehicle.make != null,vehicle.model != null),vehicle.make + '/',vehicle.make)}{!vehicle.model} 
                                                        {!if(vehicle.year != null,' ' + vehicle.year,'')} | {!if(and(vehicle.capacity != null,vehicle.capacity != ''),vehicle.capacity + ' PAX','')}
                                                        <span style="{!if(vehicle.wifi_option == true,'','display:none;')}">
                                                            <i class="fas fa-wifi icon"></i> Wi-Fi
                                                        </span>
                                                        <span style="{!if(vehicle.outlets_option == true,'','display:none;')}">
                                                            <i class="fas fa-shopping-basket icon"></i> Outlets
                                                        </span>
                                                        <span style="{!if(vehicle.restroom_option == true,'','display:none;')}">
                                                            <i class="fas fa-restroom icon"></i> Restroom
                                                        </span>
                                                        <span style="{!if(vehicle.dvd_option == true,'','display:none;')}">
                                                            <i class="fas fa-compact-disc icon"></i> DVD
                                                        </span>
                                                        <span style="{!if(vehicle.satellitetv_option == true,'','display:none;')}">
                                                            <i class="fas fa-tv icon"></i> Satellite TV
                                                        </span>
                                                        <span style="{!if(vehicle.table_option == true,'','display:none;')}">
                                                            <i class="fas fa-table icon"></i> Table
                                                        </span>
                                                        <span style="{!if(vehicle.trailerhitch_option == true,'','display:none;')}">
                                                            <i class="fas fa-caravan icon"></i> Trailer Hitch
                                                        </span>
                                                        <span style="{!if(vehicle.trailer_option == true,'','display:none;')}">
                                                            <i class="fas fa-trailer icon"></i> Trailer
                                                        </span>
                                                        <span style="{!if(vehicle.coach_option == true,'','display:none;')}">
                                                            <i class="fas fa-user-friends icon"></i> Executive Coach
                                                        </span>
                                                        <span style="{!if(vehicle.sleepers_option == true,'','display:none;')}">
                                                            <i class="fas fa-restroom icon"></i> Sleepers
                                                        </span>
                                                        {!if(vehicle.otherAmenities != null,' - ' + vehicle.otherAmenities,'')}
                                                    </div>
                                                </aura:if>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                    <div class="slds-grid slds-wrap" style="{!if(travel.lastDetail == true,'','display:none;')}">
                                    	<div class="slds-col slds-size_1-of-1 slds-medium-size_9-of-12 total-price-description">
                                            Total Price
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_3-of-12 total-price-info">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.totalPrice}" style="currency" currencyCode="{!v.optionDetailRecord.currencyIsoCode}"/>
                                            <!--${!v.optionDetailRecord.totalPrice}-->
                                        </div>
                                    </div>
                                </div>
                            </article>
                        </aura:iteration>
                    </section>
                    <section class="page-section slds-other-info" style="padding: 0em 1em 2em 1em;">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>Trip Notes</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.tripNotes}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>ADDITIONAL FEES</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                <aura:iteration items="{!v.optionDetailRecord.concessions}" var="concession">
                                    <div class="slds-p-top_xxx-small">
                                        <!--&bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c,'')} - {!if(and(concession.Rate__c != null, concession.Rate__c > 0), '$','')} {!if(concession.Rate__c != null, concession.Rate__c,'')}, {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' in rate','')}-->
                                        &bull; {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' - ','')} {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c + ' - ','')}
                                        <aura:if isTrue="{!if(and(concession.Rate__c != null, concession.Rate__c > 0), true, false)}">
                                            <lightning:formattedNumber value="{!concession.Rate__c}" style="currency" currencyCode="{!v.optionDetailRecord.currencyIsoCode}"/>
                                            <aura:set attribute="else">
                                                {!if(concession.Rate__c != null, concession.Rate__c,'')}
                                            </aura:set>
                                        </aura:if>
                                        <aura:if isTrue="{!if(concession.Notes__c != null, true, false)}">
                                            <br/>Notes: {!concession.Notes__c}
                                        </aura:if>
                                    </div>
                                </aura:iteration>
                            </div>
                            <!--<div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.gratuity}
                            </div>-->
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>PAYMENTS ACCEPTED</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.paymentsAccepted}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>PAYMENT POLICY</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.paymentPolicy}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>CANCELLATION POLICY</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.cancellationPolicy}
                            </div>
                        </div>
                        <div class="slds-grid" style="margin-top: 1.5em;">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>ADDITIONAL INFORMATION</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description"></div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                            	<span style="margin-left: 0.5em;">{!v.optionDetailRecord.additionalInformation}</span>
                            </div>
                        </div>
                        <div class="slds-grid slds-wrap" style="margin-top: 1em;padding-bottom: 2em;border-bottom: 1px solid #dbdbdb;">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                <span style="font-size: 12px;font-weight: bold;">ADD COMMENTS</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                <div class="formField">
                                    <lightning:textarea aura:id="recordField" name="" label="" value="{!v.comments}" variant="label-hidden" />
                                </div>
                            </div>
                        </div>
                        <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                            <div class="slds-col slds-size_1-of-1" style="text-align: right;">
                                <lightning:button label="CANCEL" variant="neutral" onclick="{!c.backOptionsGT}" />
                                <lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
                            </div>
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </div>
	
</aura:component>
```
### VoyajerOptionsGTReviewSubmit

```
.THIS .slds-card-overview_icon{
    background-color: #f6f7fc;
    color: #022066;
    font-weight: bold;
    padding: .5em 1.5em 0.7em;
    font-size: 22px;
}

.THIS .slds-card-overview_header{
    color: #022066;
    font-weight: bold;
    padding: 0.5em 1.5em;
}

.THIS .slds-card-overview_header>h3{
    padding: 1rem;
}

.THIS .slds-card-overview_item{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    background-color: #022066;
    transition: transform 0.1s ease;
}

.THIS .slds-card-overview_item-leftside{
    display:flex;
    height: 100%;
    justify-content: center;
}

.THIS .slds-card-overview_item-content{
    background-color: white;
    padding-bottom: 10px;
    border: 1px solid #eaeaea;
}

.THIS .slds-card-overview_item-content-item{
    background-color: white;
    border: 1px solid #eaeaea;
    margin-top: -1px;
}

.THIS .slds-card-overview_item header{
    margin-top: .5rem;
}

.THIS .slds-card-overview_item header h3{
    font-weight: bold;
    color: #022066;
}

.THIS .slds-left_day{
    text-transform: uppercase;
    color: white;
    width: 3rem;
    text-align: center;
    font-size: 1.125rem;
    font-weight: 300;
    line-height: 1.1;
    overflow: hidden;
    display: inline-block;
    vertical-align: middle;
    margin: 0.5em 0;
}

.THIS .slds-left_day .small{
    font-size: 0.7em;
    font-weight: bold;
}

.THIS .slds-left_day .big{
    font-size: 1.5em;
    font-weight: bold;
}

.THIS .slds-box-item .title{
    text-align: center;
    font-weight: bold;
    font-size: 1.5em;
}

.THIS .slds-box-item .sub{
    text-align: center;
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .slds-box-item .arrow{
    text-align: center;
    font-size: 1.3em;
    color: grey;
}

.THIS .slds-box-item-detail{
    text-transform: uppercase;
    text-align: right;
    padding-right: 4em;
    margin-top: 1em;
    line-height: 1.6em;
    font-weight: bold;
    color: gray;
    padding-bottom: 20px;
}

.THIS .slds-box-item-detail-info{
    text-align: left;
    margin-top: 1em;
    line-height: 1.6em;
    color: gray;
    padding-bottom: 20px;
}

.THIS .slds-box-item-detail-info .icon{
    color: #007bff;
    margin-left: 1em;
}

.THIS .total-price-description{
    background-color: #f6f7fc;
    text-align: right;
    font-size: 1em;
    padding: 1.9em;
}

.THIS .total-price-info{
    background-color: #f6f7fc;
    text-align: center;
    font-size: 2.5em;
    font-weight: bold;
    padding: 0.3em;
}

.THIS .slds-other-info{
    margin-top: 1em;
    line-height: 1.8em;
}

.THIS .slds-other-info-title{
    text-align: right;
    text-transform: uppercase;
    font-weight: bold;
}

.THIS .slds-other-info-description{
    margin-left: 2em;
}

.THIS .box-decisionBy{
    display: inline-block;
    padding: 1rem 1.5rem;
    background-color: #ec4518;
    border: none;
    text-align: center;
    color: white;
    font-weight: bold;
}

.THIS .pageContentDashboard-grey{
    background-color: #f0f0f0 !important;
    box-shadow: none !important;
}

.THIS .option_pagination{
    margin-left: 1em;
    border: 1px solid #09b7ff;
    border-radius: 3em;
    background-color: white;
}

.THIS .option_pagination .option_pagination_button-left{
    padding: .6em .5em;
    border-top-left-radius: 3em;
    border-bottom-left-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_button-right{
    padding: .6em .5em;
    border-top-right-radius: 3em;
    border-bottom-right-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_counter{
    padding: .4em 1em;
}

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}
```
### VoyajerOptionsGTReviewSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsGTReviewSubmitController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadOptionsGTDetail");
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    backOptionsGT: function(component,event,helper){
        component.set("v.mainContent","optionsGT");
    },
    submitSelection: function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","submitOptionSelected");
        callToParent.setParam("data",{
            serviceType: "ground",
            serviceId: component.get("v.groundId"),
            serviceName: component.get("v.serviceData").recordName,
            bidVendorName: component.get("v.optionDetailRecord").vendor,
            bidVendorId: component.get("v.optionDetailRecord").vendorId,
            bidId: component.get("v.optionDetailRecord").recordId,
            comments: component.get("v.comments")
        });
        callToParent.fire();
    }
})
```
### VoyajerOptionsGTReviewSubmit

```
<aura:component>
    <aura:attribute type="String" name="groundId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="comments" default="" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fab fa-telegram-plane" style="color: #9f9f9f; margin-right: 0.5em;"></i>Review &amp; Submit
                        </h1>
                        <lightning:button label="BACK TO THE OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsGT}" />
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(v.serviceData.endCityName != null,' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                            	<p>Group Type: {!v.serviceData.groupType}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <section class="page-section slds-card-overview">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside slds-card-overview_icon">
                                <i class="fas fa-bus icon"></i>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-overview_item-content slds-card-overview_header">
                                <header class="slds-grid">
                                    <h3>
                                        {!v.optionDetailRecord.vendor}
                                    </h3>
                                </header>
                            </div>
                        </div>
                        <aura:iteration items="{!v.optionDetailRecord.travels}" var="travel">
                            <article class="slds-grid slds-wrap slds-card-overview_item">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside">
                                    <div class="slds-media slds-media_responsive">
                                        <div class="slds-media__figure" style="margin-top:10px;margin-right:0;">
                                            <span class="slds-left_day">
                                                <span class="small">{!travel.dayStart}</span> <br/>
                                                <span class="big">{!travel.dayNumberStart}</span> <br/>
                                                <span class="small">{!travel.monthStart}</span> <br/>
                                            </span>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-overview_item-content-item">
                                    <header class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12 slds-box-item slds-p-horizontal_small">
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 title">
                                                    <!--{!travel.startCity}-->
                                                    {!travel.startCityShortName}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-7 arrow">
                                                    <i class="fas fa-arrow-right"></i>
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 title">
                                                    <!--{!travel.endCity}-->
                                                    {!travel.endCityShortName}
                                                </div>                                            
                                            </div>
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    {!travel.locationType}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-7 arrow"></div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    <!--{!travel.locationDropOff}-->
                                                    {!travel.locationDropOffType}
                                                </div>
                                            </div>
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    {!travel.startDateTime}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-7 arrow"></div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-7 sub">
                                                    {!travel.endDateTime}
                                                </div>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12 slds-text-align_right slds-p-horizontal_small">
                                            <div>
                                            	<span style="font-weight:bold;">Trip Type: </span><span>{!travel.tripType}</span> | <span>{!travel.capacity}</span> Passengers
                                            </div>
                                            <div>
                                                <span style="font-weight:bold;">Gear/Luggage Space Needed: </span><span>{!travel.gearLuggage}</span>
                                            </div>
                                        </div>
                                    </header>
                                    <div class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-box-item-detail">
                                            <div>PICK UP</div>
                                            <div>DROP OFF</div>
                                            <div>BUS TYPE</div>
                                            <aura:iteration items="{!v.optionDetailRecord.vehicles}" var="vehicle">
                                                <aura:if isTrue="{!if(travel.vehicleId == vehicle.vehicleId,true,false)}"><!--filter for only show vehicles related to this travel -->
                                                	<div>{!vehicle.vehicleName}</div>
                                                </aura:if>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-box-item-detail-info">
                                            <div>
                                                <span style="text-transform:uppercase;">{!travel.dayStart + ', ' + travel.dayNumberStart + ' ' + travel.monthStart + ' ' + travel.yearStart}</span> | {!travel.startDateTime} from {!travel.startCity} ({!travel.locationType})
                                            </div>
                                            <div>
                                                <span style="text-transform:uppercase;">{!travel.dayEnd + ', ' + travel.dayNumberEnd + ' ' + travel.monthEnd + ' ' + travel.yearEnd}</span> | {!travel.endDateTime} {!travel.endCity} <!--({!travel.locationDropOff})--> ({!travel.locationDropOffType})
                                            </div>
                                            <div>{!if(and(travel.vehicleType != null,travel.vehicleType != ''),travel.vehicleType,'&nbsp;')}</div>
                                            <aura:iteration items="{!v.optionDetailRecord.vehicles}" var="vehicle">
                                                <aura:if isTrue="{!if(travel.vehicleId == vehicle.vehicleId,true,false)}">
                                                    <div>
                                                        {!if(and(vehicle.make != null,vehicle.model != null),vehicle.make + '/',vehicle.make)}{!vehicle.model} 
                                                        {!if(vehicle.year != null,' ' + vehicle.year,'')} | {!if(and(vehicle.capacity != null,vehicle.capacity != ''),vehicle.capacity + ' PAX','')}
                                                        <span style="{!if(vehicle.wifi_option == true,'','display:none;')}">
                                                            <i class="fas fa-wifi icon"></i> Wi-Fi
                                                        </span>
                                                        <span style="{!if(vehicle.outlets_option == true,'','display:none;')}">
                                                            <i class="fas fa-shopping-basket icon"></i> Outlets
                                                        </span>
                                                        <span style="{!if(vehicle.restroom_option == true,'','display:none;')}">
                                                            <i class="fas fa-restroom icon"></i> Restroom
                                                        </span>
                                                        <span style="{!if(vehicle.dvd_option == true,'','display:none;')}">
                                                            <i class="fas fa-compact-disc icon"></i> DVD
                                                        </span>
                                                        <span style="{!if(vehicle.satellitetv_option == true,'','display:none;')}">
                                                            <i class="fas fa-tv icon"></i> Satellite TV
                                                        </span>
                                                        <span style="{!if(vehicle.table_option == true,'','display:none;')}">
                                                            <i class="fas fa-table icon"></i> Table
                                                        </span>
                                                        <span style="{!if(vehicle.trailerhitch_option == true,'','display:none;')}">
                                                            <i class="fas fa-caravan icon"></i> Trailer Hitch
                                                        </span>
                                                        <span style="{!if(vehicle.trailer_option == true,'','display:none;')}">
                                                            <i class="fas fa-trailer icon"></i> Trailer
                                                        </span>
                                                        <span style="{!if(vehicle.coach_option == true,'','display:none;')}">
                                                            <i class="fas fa-user-friends icon"></i> Executive Coach
                                                        </span>
                                                        <span style="{!if(vehicle.sleepers_option == true,'','display:none;')}">
                                                            <i class="fas fa-restroom icon"></i> Sleepers
                                                        </span>
                                                        {!if(vehicle.otherAmenities != null,' - ' + vehicle.otherAmenities,'')}
                                                    </div>
                                                </aura:if>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                    <div class="slds-grid slds-wrap" style="{!if(travel.lastDetail == true,'','display:none;')}">
                                    	<div class="slds-col slds-size_1-of-1 slds-medium-size_9-of-12 total-price-description">
                                            Total Price
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_3-of-12 total-price-info">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.totalPrice}" style="currency" currencyCode="{!v.optionDetailRecord.currencyIsoCode}"/>
                                            <!--${!v.optionDetailRecord.totalPrice}-->
                                        </div>
                                    </div>
                                </div>
                            </article>
                        </aura:iteration>
                    </section>
                    <section class="page-section slds-other-info" style="padding: 0em 1em 2em 1em;">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>Trip Notes</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.tripNotes}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>ADDITIONAL FEES</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                <aura:iteration items="{!v.optionDetailRecord.concessions}" var="concession">
                                    <div class="slds-p-top_xxx-small">
                                        <!--&bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c,'')} - {!if(and(concession.Rate__c != null, concession.Rate__c > 0), '$','')} {!if(concession.Rate__c != null, concession.Rate__c,'')}, {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' in rate','')}-->
                                        &bull; {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' - ','')} {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c + ' - ','')}
                                        <aura:if isTrue="{!if(and(concession.Rate__c != null, concession.Rate__c > 0), true, false)}">
                                            <lightning:formattedNumber value="{!concession.Rate__c}" style="currency" currencyCode="{!v.optionDetailRecord.currencyIsoCode}"/>
                                            <aura:set attribute="else">
                                                {!if(concession.Rate__c != null, concession.Rate__c,'')}
                                            </aura:set>
                                        </aura:if>
                                        <aura:if isTrue="{!if(concession.Notes__c != null, true, false)}">
                                            <br/>Notes: {!concession.Notes__c}
                                        </aura:if>
                                    </div>
                                </aura:iteration>
                            </div>
                            <!--<div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.gratuity}
                            </div>-->
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>PAYMENTS ACCEPTED</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.paymentsAccepted}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>PAYMENT POLICY</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.paymentPolicy}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>CANCELLATION POLICY</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.cancellationPolicy}
                            </div>
                        </div>
                        <div class="slds-grid" style="margin-top: 1.5em;">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>ADDITIONAL INFORMATION</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description"></div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                            	<span style="margin-left: 0.5em;">{!v.optionDetailRecord.additionalInformation}</span>
                            </div>
                        </div>
                        <div class="slds-grid slds-wrap" style="margin-top: 1em;padding-bottom: 2em;border-bottom: 1px solid #dbdbdb;">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                <span style="font-size: 12px;font-weight: bold;">ADD COMMENTS</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                <div class="formField">
                                    <lightning:textarea aura:id="recordField" name="" label="" value="{!v.comments}" variant="label-hidden" />
                                </div>
                            </div>
                        </div>
                        <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                            <div class="slds-col slds-size_1-of-1" style="text-align: right;">
                                <lightning:button label="CANCEL" variant="neutral" onclick="{!c.backOptionsGT}" />
                                <lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
                            </div>
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </div>
	
</aura:component>
```
### VoyajerOptionsGTReviewSubmit

```
.THIS .slds-card-overview_icon{
    background-color: #f6f7fc;
    color: #022066;
    font-weight: bold;
    padding: .5em 1.5em 0.7em;
    font-size: 22px;
}

.THIS .slds-card-overview_header{
    color: #022066;
    font-weight: bold;
    padding: 0.5em 1.5em;
}

.THIS .slds-card-overview_header>h3{
    padding: 1rem;
}

.THIS .slds-card-overview_item{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    background-color: #022066;
    transition: transform 0.1s ease;
}

.THIS .slds-card-overview_item-leftside{
    display:flex;
    height: 100%;
    justify-content: center;
}

.THIS .slds-card-overview_item-content{
    background-color: white;
    padding-bottom: 10px;
    border: 1px solid #eaeaea;
}

.THIS .slds-card-overview_item-content-item{
    background-color: white;
    border: 1px solid #eaeaea;
    margin-top: -1px;
}

.THIS .slds-card-overview_item header{
    margin-top: .5rem;
}

.THIS .slds-card-overview_item header h3{
    font-weight: bold;
    color: #022066;
}

.THIS .slds-left_day{
    text-transform: uppercase;
    color: white;
    width: 3rem;
    text-align: center;
    font-size: 1.125rem;
    font-weight: 300;
    line-height: 1.1;
    overflow: hidden;
    display: inline-block;
    vertical-align: middle;
    margin: 0.5em 0;
}

.THIS .slds-left_day .small{
    font-size: 0.7em;
    font-weight: bold;
}

.THIS .slds-left_day .big{
    font-size: 1.5em;
    font-weight: bold;
}

.THIS .slds-box-item .title{
    text-align: center;
    font-weight: bold;
    font-size: 1.5em;
}

.THIS .slds-box-item .sub{
    text-align: center;
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .slds-box-item .arrow{
    text-align: center;
    font-size: 1.3em;
    color: grey;
}

.THIS .slds-box-item-detail{
    text-transform: uppercase;
    text-align: right;
    padding-right: 4em;
    margin-top: 1em;
    line-height: 1.6em;
    font-weight: bold;
    color: gray;
    padding-bottom: 20px;
}

.THIS .slds-box-item-detail-info{
    text-align: left;
    margin-top: 1em;
    line-height: 1.6em;
    color: gray;
    padding-bottom: 20px;
}

.THIS .slds-box-item-detail-info .icon{
    color: #007bff;
    margin-left: 1em;
}

.THIS .total-price-description{
    background-color: #f6f7fc;
    text-align: right;
    font-size: 1em;
    padding: 1.9em;
}

.THIS .total-price-info{
    background-color: #f6f7fc;
    text-align: center;
    font-size: 2.5em;
    font-weight: bold;
    padding: 0.3em;
}

.THIS .slds-other-info{
    margin-top: 1em;
    line-height: 1.8em;
}

.THIS .slds-other-info-title{
    text-align: right;
    text-transform: uppercase;
    font-weight: bold;
}

.THIS .slds-other-info-description{
    margin-left: 2em;
}

.THIS .box-decisionBy{
    display: inline-block;
    padding: 1rem 1.5rem;
    background-color: #ec4518;
    border: none;
    text-align: center;
    color: white;
    font-weight: bold;
}

.THIS .pageContentDashboard-grey{
    background-color: #f0f0f0 !important;
    box-shadow: none !important;
}

.THIS .option_pagination{
    margin-left: 1em;
    border: 1px solid #09b7ff;
    border-radius: 3em;
    background-color: white;
}

.THIS .option_pagination .option_pagination_button-left{
    padding: .6em .5em;
    border-top-left-radius: 3em;
    border-bottom-left-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_button-right{
    padding: .6em .5em;
    border-top-right-radius: 3em;
    border-bottom-right-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_counter{
    padding: .4em 1em;
}

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}
```

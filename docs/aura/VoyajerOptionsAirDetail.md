---
layout: default
title: VoyajerOptionsAirDetail
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsAirDetail
## Fields
### VoyajerOptionsAirDetailController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadOptionsAirDetail");
        console.log(list);
        console.log(index);
        console.log(list[index]);
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    backOptionsAir: function(component,event,helper){
        component.set("v.mainContent","optionsAir");
    },
    changeOptionsAirDetail: function(component,event,helper){
        var index = parseInt(event.currentTarget.dataset.bidindex);
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        console.log(list.length);
        
        if(event.currentTarget.dataset.actionto == 'next')
            index = index + 1;
        else
            index = index - 1;

        console.log(index);
        if((event.currentTarget.dataset.actionto == 'next' && index < list.length) || (event.currentTarget.dataset.actionto == 'last' && index >= 0)){
            component.set("v.optionDetailRecordId",index);
            component.set("v.optionDetailRecordIdReal",index + 1);
            component.set("v.bidOptionsSize",list.length);
            callToParent.setParam("action","loadOptionsAirDetail");
            callToParent.setParam("data",{
                detailRecordId: list[index].recordId
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerOptionsAirDetail

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsAirDetail

```
<aura:component>
    <aura:attribute type="String" name="airId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
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
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i> Option {!v.optionDetailRecordIdReal}
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsAir}"/>
                        <div class="option_pagination">
                            <button class="option_pagination_button-left" data-bidindex="{!v.optionDetailRecordId}" data-actionto="last" title="{!v.index}" onclick="{!c.changeOptionsAirDetail}">
                                <i class="fas fa-angle-left"></i>
                            </button>
                            <span class="option_pagination_counter">{!v.optionDetailRecordIdReal} of {!v.bidOptionsSize}</span>
                            <button class="option_pagination_button-right" data-bidindex="{!v.optionDetailRecordId}" data-actionto="next"  onclick="{!c.changeOptionsAirDetail}">
                                <i class="fas fa-angle-right"></i>
                            </button>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-3">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(and(v.serviceData.endCityName != null, v.serviceData.tripType != 'Round Trip'),' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.serviceData.releaseDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:2em;border-bottom: 1px solid #dbdbdb;">
                    <section class="page-section slds-card-overview">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside slds-card-overview_icon">
                                <i class="fas fa-plane icon"></i>
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
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12 slds-box-item">
                                            <div style="padding: 0 3em 0 3em;">
                                                <div class="slds-grid slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                        {!travel.startCity}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow">
                                                        <i class="fas fa-arrow-right"></i>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                        {!travel.endCity}
                                                    </div>                                            
                                                </div>
                                                <div class="slds-grid slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                        {!travel.startAirport}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                        {!travel.endAirport}
                                                    </div>
                                                </div>
                                                <div class="slds-grid slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                        {!travel.startDateTime}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                        {!travel.endDateTime} <span style="{!if(travel.arrivesNextDay == true,'font-size: 11px;color:red;margin-left: 1.5em;','display:none;')}">ARRIVES NEXT DAY</span>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12">
                                            <div class="slds-grid slds-wrap item" style="font-weight:bold;margin-top: 2em;">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;">
                                                    {!travel.flightDuration}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                    {!if(travel.stops > 0, travel.stops + ' Stop','Nonstop')}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                    {!v.optionDetailRecord.seats} Seats
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                    {!travel.classAir}
                                                </div>
                                            </div>
                                        </div>
                                    </header>
                                    <div class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1 slds-box-item-detail">
                                            <aura:iteration items="{!travel.layovers}" var="layover">
                                                <div class="slds-grid slds-wrap item">
                                                    <aura:if isTrue="{!if(layover.layoverName == '',false,true)}">
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                                                            <div style="font-weight:bold;text-align:left;padding: 2em 0 0.5em 2em;">{!layover.layoverName} | {!layover.layoverDifference}</div>
                                                        </div>
                                                    </aura:if>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                        DEPARTS
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                        <span style="margin-right: 0.5em;">{!layover.departDate}</span> | <span style="margin-left: 0.5em;">{!layover.departTime} FROM {!layover.departCity}</span>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">
                                                        ARRIVES
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">
                                                        <span style="{!if(layover.arrivesOtherDay == true,'color:red;','')}">
                                                            <span style="margin-right: 0.5em;">{!layover.arriveDate}</span> | <span style="margin-left: 0.5em;">{!layover.arriveTime}</span>
                                                        </span> TO {!layover.arriveCity}
                                                        <!--<span style="margin-right: 0.5em;">{!layover.arriveDate}</span> | <span style="margin-left: 0.5em;">{!layover.arriveTime}</span>&nbsp;{!layover.arriveCity}-->
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">FLIGHT</div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.flight}</div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">AIRCRAFT</div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.aircraft}</div>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                    <div class="slds-grid slds-wrap" style="{!if(travel.lastDetail == true,'','display:none;')}">
                                    	<div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 total-price-description">
                                            Price Per ticket
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 total-price-info">
                                            ${!v.optionDetailRecord.totalPrice}
                                        </div>
                                    </div>
                                </div>
                            </article>
                        </aura:iteration>
                        <aura:if isTrue="{!!empty(v.optionDetailRecord.deviations)}">
                            <div style="margin-top: 2em;">
                                <aura:iteration items="{!v.optionDetailRecord.deviations}" var="travel">
                                    <article class="slds-grid slds-wrap slds-card-overview_item">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside" style="{!if(travel.firstDetail == true,'margin-top: 2.7em;','')}">
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
                                                <aura:if isTrue="{!if(travel.firstDetail == true,true,false)}">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                                        <div class="box-deviation">Deviation Flight</div>
                                                    </div>
                                                </aura:if>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12 slds-box-item">
                                                    <div style="padding: 0 3em 0 3em;">
                                                        <div class="slds-grid slds-wrap">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                                {!travel.startCity}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow">
                                                                <i class="fas fa-arrow-right"></i>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                                {!travel.endCity}
                                                            </div>                                            
                                                        </div>
                                                        <div class="slds-grid slds-wrap">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                                {!travel.startAirport}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                                {!travel.endAirport}
                                                            </div>
                                                        </div>
                                                        <div class="slds-grid slds-wrap">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                                {!travel.startDateTime}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                                {!travel.endDateTime} <span style="{!if(travel.arrivesNextDay == true,'font-size: 11px;color:red;margin-left: 1.5em;','display:none;')}">ARRIVES NEXT DAY</span>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12">
                                                    <div class="slds-grid slds-wrap item" style="font-weight:bold;margin-top: 2em;">
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;">
                                                            {!travel.flightDuration}
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                            {!if(travel.stops > 0, travel.stops + ' Stop','Nonstop')}
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                            {!v.optionDetailRecord.seatsDeviation} Seats
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                            {!travel.classAir}
                                                        </div>
                                                    </div>
                                                </div>
                                            </header>
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1 slds-box-item-detail">
                                                    <aura:iteration items="{!travel.layovers}" var="layover">
                                                        <div class="slds-grid slds-wrap item">
                                                            <aura:if isTrue="{!if(layover.layoverName == '',false,true)}">
                                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                                                                    <div style="font-weight:bold;text-align:left;padding: 2em 0 0.5em 2em;">{!layover.layoverName} | {!layover.layoverDifference}</div>
                                                                </div>
                                                            </aura:if>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                                DEPARTS
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                                <span style="margin-right: 0.5em;">{!layover.departDate}</span> | <span style="margin-left: 0.5em;">{!layover.departTime} FROM {!layover.departCity}</span>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">
                                                                ARRIVES
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">
                                                                <span style="margin-right: 0.5em;">{!layover.arriveDate}</span> | <span style="margin-left: 0.5em;">{!layover.arriveTime}&nbsp;{!layover.arriveCity}</span> <span style="{!if(layover.arrivesNextDay == true,'font-size: 11px;color:red;margin-left: 1.5em;','display:none;')}">ARRIVES NEXT DAY</span>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">FLIGHT</div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.flight}</div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">AIRCRAFT</div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.aircraft}</div>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                            </div>
                                            <div class="slds-grid slds-wrap" style="{!if(travel.lastDetail == true,'','display:none;')}">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 total-price-description">
                                                    Price Per ticket
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 total-price-info">
                                                    ${!v.optionDetailRecord.totalPriceDeviation}
                                                </div>
                                            </div>
                                        </div>
                                    </article>
                                </aura:iteration>
                            </div>
                        </aura:if>
                    </section>
                    <section class="page-section slds-other-info">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>CONTRACT DUE</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.contractDue}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>DEPOSIT DUE</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.depositDue}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>UTILIZATION DUE</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.utilizationDue}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>NAMES &amp; FINAL PAYMENT</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.namesFinalPayment}
                            </div>
                        </div>
                        <div class="slds-grid" style="margin-top: 1.5em;">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>GROUP BOOKING POLICY</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description"></div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                            	<span style="margin-left: 0.5em;">{!v.optionDetailRecord.additionalInformation}</span>
                            </div>
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </div>
	
</aura:component>
```
### VoyajerOptionsAirDetail

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
    margin-bottom: -1px;
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

.THIS .slds-box-item {
	margin-top: 1em;    
}

.THIS .slds-box-item .title{
    text-align: left;
    font-weight: bold;
    font-size: 1.5em;
}

.THIS .slds-box-item .sub{
    text-align: left;
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .slds-box-item .arrow{
    text-align: left;
    font-size: 1.3em;
    color: grey;
}

.THIS .slds-box-item-detail{
    text-align: right;
    margin-top: 1em;
    line-height: 1.6em;
    color: gray;
    padding-bottom: 20px;
    padding-left: 2em;
    padding-right: 2em;
}

.THIS .slds-box-item-detail .item{
    text-transform:uppercase;
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
    padding: 1.89em;
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
    text-transform:uppercase;
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

.THIS .box-deviation{
    padding: 0.8em 2em 0.8em 2em;
    background-color: orange;
    color: white;
    font-weight: bold;
    width: 155px;
    margin-left: -1px;
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
### VoyajerOptionsAirDetailController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadOptionsAirDetail");
        console.log(list);
        console.log(index);
        console.log(list[index]);
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    backOptionsAir: function(component,event,helper){
        component.set("v.mainContent","optionsAir");
    },
    changeOptionsAirDetail: function(component,event,helper){
        var index = parseInt(event.currentTarget.dataset.bidindex);
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        console.log(list.length);
        
        if(event.currentTarget.dataset.actionto == 'next')
            index = index + 1;
        else
            index = index - 1;

        console.log(index);
        if((event.currentTarget.dataset.actionto == 'next' && index < list.length) || (event.currentTarget.dataset.actionto == 'last' && index >= 0)){
            component.set("v.optionDetailRecordId",index);
            component.set("v.optionDetailRecordIdReal",index + 1);
            component.set("v.bidOptionsSize",list.length);
            callToParent.setParam("action","loadOptionsAirDetail");
            callToParent.setParam("data",{
                detailRecordId: list[index].recordId
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerOptionsAirDetail

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsAirDetail

```
<aura:component>
    <aura:attribute type="String" name="airId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
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
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i> Option {!v.optionDetailRecordIdReal}
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsAir}"/>
                        <div class="option_pagination">
                            <button class="option_pagination_button-left" data-bidindex="{!v.optionDetailRecordId}" data-actionto="last" title="{!v.index}" onclick="{!c.changeOptionsAirDetail}">
                                <i class="fas fa-angle-left"></i>
                            </button>
                            <span class="option_pagination_counter">{!v.optionDetailRecordIdReal} of {!v.bidOptionsSize}</span>
                            <button class="option_pagination_button-right" data-bidindex="{!v.optionDetailRecordId}" data-actionto="next"  onclick="{!c.changeOptionsAirDetail}">
                                <i class="fas fa-angle-right"></i>
                            </button>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-3">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(and(v.serviceData.endCityName != null, v.serviceData.tripType != 'Round Trip'),' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.serviceData.releaseDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:2em;border-bottom: 1px solid #dbdbdb;">
                    <section class="page-section slds-card-overview">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside slds-card-overview_icon">
                                <i class="fas fa-plane icon"></i>
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
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12 slds-box-item">
                                            <div style="padding: 0 3em 0 3em;">
                                                <div class="slds-grid slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                        {!travel.startCity}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow">
                                                        <i class="fas fa-arrow-right"></i>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                        {!travel.endCity}
                                                    </div>                                            
                                                </div>
                                                <div class="slds-grid slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                        {!travel.startAirport}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                        {!travel.endAirport}
                                                    </div>
                                                </div>
                                                <div class="slds-grid slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                        {!travel.startDateTime}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                        {!travel.endDateTime} <span style="{!if(travel.arrivesNextDay == true,'font-size: 11px;color:red;margin-left: 1.5em;','display:none;')}">ARRIVES NEXT DAY</span>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12">
                                            <div class="slds-grid slds-wrap item" style="font-weight:bold;margin-top: 2em;">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;">
                                                    {!travel.flightDuration}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                    {!if(travel.stops > 0, travel.stops + ' Stop','Nonstop')}
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                    {!v.optionDetailRecord.seats} Seats
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                    {!travel.classAir}
                                                </div>
                                            </div>
                                        </div>
                                    </header>
                                    <div class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1 slds-box-item-detail">
                                            <aura:iteration items="{!travel.layovers}" var="layover">
                                                <div class="slds-grid slds-wrap item">
                                                    <aura:if isTrue="{!if(layover.layoverName == '',false,true)}">
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                                                            <div style="font-weight:bold;text-align:left;padding: 2em 0 0.5em 2em;">{!layover.layoverName} | {!layover.layoverDifference}</div>
                                                        </div>
                                                    </aura:if>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                        DEPARTS
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                        <span style="margin-right: 0.5em;">{!layover.departDate}</span> | <span style="margin-left: 0.5em;">{!layover.departTime} FROM {!layover.departCity}</span>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">
                                                        ARRIVES
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">
                                                        <span style="{!if(layover.arrivesOtherDay == true,'color:red;','')}">
                                                            <span style="margin-right: 0.5em;">{!layover.arriveDate}</span> | <span style="margin-left: 0.5em;">{!layover.arriveTime}</span>
                                                        </span> TO {!layover.arriveCity}
                                                        <!--<span style="margin-right: 0.5em;">{!layover.arriveDate}</span> | <span style="margin-left: 0.5em;">{!layover.arriveTime}</span>&nbsp;{!layover.arriveCity}-->
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">FLIGHT</div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.flight}</div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">AIRCRAFT</div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.aircraft}</div>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                    <div class="slds-grid slds-wrap" style="{!if(travel.lastDetail == true,'','display:none;')}">
                                    	<div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 total-price-description">
                                            Price Per ticket
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 total-price-info">
                                            ${!v.optionDetailRecord.totalPrice}
                                        </div>
                                    </div>
                                </div>
                            </article>
                        </aura:iteration>
                        <aura:if isTrue="{!!empty(v.optionDetailRecord.deviations)}">
                            <div style="margin-top: 2em;">
                                <aura:iteration items="{!v.optionDetailRecord.deviations}" var="travel">
                                    <article class="slds-grid slds-wrap slds-card-overview_item">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside" style="{!if(travel.firstDetail == true,'margin-top: 2.7em;','')}">
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
                                                <aura:if isTrue="{!if(travel.firstDetail == true,true,false)}">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                                        <div class="box-deviation">Deviation Flight</div>
                                                    </div>
                                                </aura:if>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12 slds-box-item">
                                                    <div style="padding: 0 3em 0 3em;">
                                                        <div class="slds-grid slds-wrap">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                                {!travel.startCity}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow">
                                                                <i class="fas fa-arrow-right"></i>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 title">
                                                                {!travel.endCity}
                                                            </div>                                            
                                                        </div>
                                                        <div class="slds-grid slds-wrap">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                                {!travel.startAirport}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5" style="font-weight: bold;text-align:left;">
                                                                {!travel.endAirport}
                                                            </div>
                                                        </div>
                                                        <div class="slds-grid slds-wrap">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                                {!travel.startDateTime}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5 arrow"></div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-5 sub" style="font-weight: bold;">
                                                                {!travel.endDateTime} <span style="{!if(travel.arrivesNextDay == true,'font-size: 11px;color:red;margin-left: 1.5em;','display:none;')}">ARRIVES NEXT DAY</span>
                                                            </div>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12">
                                                    <div class="slds-grid slds-wrap item" style="font-weight:bold;margin-top: 2em;">
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;">
                                                            {!travel.flightDuration}
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                            {!if(travel.stops > 0, travel.stops + ' Stop','Nonstop')}
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                            {!v.optionDetailRecord.seatsDeviation} Seats
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align:center;border-left: 1px solid #eaeaea">
                                                            {!travel.classAir}
                                                        </div>
                                                    </div>
                                                </div>
                                            </header>
                                            <div class="slds-grid slds-wrap">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1 slds-box-item-detail">
                                                    <aura:iteration items="{!travel.layovers}" var="layover">
                                                        <div class="slds-grid slds-wrap item">
                                                            <aura:if isTrue="{!if(layover.layoverName == '',false,true)}">
                                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                                                                    <div style="font-weight:bold;text-align:left;padding: 2em 0 0.5em 2em;">{!layover.layoverName} | {!layover.layoverDifference}</div>
                                                                </div>
                                                            </aura:if>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                                DEPARTS
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;margin-top: 0.5em;border-top: 1px solid #eaeaea;padding-top: 1em;">
                                                                <span style="margin-right: 0.5em;">{!layover.departDate}</span> | <span style="margin-left: 0.5em;">{!layover.departTime} FROM {!layover.departCity}</span>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">
                                                                ARRIVES
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">
                                                                <span style="margin-right: 0.5em;">{!layover.arriveDate}</span> | <span style="margin-left: 0.5em;">{!layover.arriveTime}&nbsp;{!layover.arriveCity}</span> <span style="{!if(layover.arrivesNextDay == true,'font-size: 11px;color:red;margin-left: 1.5em;','display:none;')}">ARRIVES NEXT DAY</span>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">FLIGHT</div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.flight}</div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12" style="font-weight:bold;">AIRCRAFT</div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12" style="text-align:left;padding-left:2em;">{!layover.aircraft}</div>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                            </div>
                                            <div class="slds-grid slds-wrap" style="{!if(travel.lastDetail == true,'','display:none;')}">
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 total-price-description">
                                                    Price Per ticket
                                                </div>
                                                <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 total-price-info">
                                                    ${!v.optionDetailRecord.totalPriceDeviation}
                                                </div>
                                            </div>
                                        </div>
                                    </article>
                                </aura:iteration>
                            </div>
                        </aura:if>
                    </section>
                    <section class="page-section slds-other-info">
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>CONTRACT DUE</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.contractDue}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>DEPOSIT DUE</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.depositDue}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>UTILIZATION DUE</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.utilizationDue}
                            </div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>NAMES &amp; FINAL PAYMENT</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description">
                                {!v.optionDetailRecord.namesFinalPayment}
                            </div>
                        </div>
                        <div class="slds-grid" style="margin-top: 1.5em;">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-12 slds-other-info-title">
                                <span>GROUP BOOKING POLICY</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_10-of-12 slds-other-info-description"></div>
                        </div>
                        <div class="slds-grid">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_12-of-12">
                            	<span style="margin-left: 0.5em;">{!v.optionDetailRecord.additionalInformation}</span>
                            </div>
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </div>
	
</aura:component>
```
### VoyajerOptionsAirDetail

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
    margin-bottom: -1px;
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

.THIS .slds-box-item {
	margin-top: 1em;    
}

.THIS .slds-box-item .title{
    text-align: left;
    font-weight: bold;
    font-size: 1.5em;
}

.THIS .slds-box-item .sub{
    text-align: left;
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .slds-box-item .arrow{
    text-align: left;
    font-size: 1.3em;
    color: grey;
}

.THIS .slds-box-item-detail{
    text-align: right;
    margin-top: 1em;
    line-height: 1.6em;
    color: gray;
    padding-bottom: 20px;
    padding-left: 2em;
    padding-right: 2em;
}

.THIS .slds-box-item-detail .item{
    text-transform:uppercase;
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
    padding: 1.89em;
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
    text-transform:uppercase;
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

.THIS .box-deviation{
    padding: 0.8em 2em 0.8em 2em;
    background-color: orange;
    color: white;
    font-weight: bold;
    width: 155px;
    margin-left: -1px;
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

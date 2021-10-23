---
layout: default
title: VoyajerOptionsGTCompare
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsGTCompare
## Fields
### VoyajerOptionsGTCompare

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsGTCompareHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsGTCompare

```
<aura:component>
    <aura:attribute type="String" name="groundId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="compareList" />
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>Compare Options
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(v.serviceData.endCityName != null,' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                                <p>Group Type: {!v.serviceData.groupType}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.serviceData.releaseDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:2em;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-carousel__stage section-compare">
                        <div class="slds-grid slds-wrap">
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-grid slds-gutters_x-small slds-wrap section-compare_header">
                                    <div class="slds-col slds-size_1-of-4">
                                    </div>
                                    <aura:iteration items="{!v.compareList}" var="bid">
                                        <div class="slds-col slds-size_1-of-4 section-compare_header_item">
                                            <div class="header">{!bid.vendor}</div>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Information Details">Information Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Website</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="color: #00b4ff;">
                                                    {!bid.record.Vendor__r.Website}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Address</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingStreet}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>City, State / Postal Code</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingCity + ', ' + bid.record.Vendor__r.ShippingState + ' ' + bid.record.Vendor__r.ShippingPostalCode}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Phone</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.Phone}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Rate Details">Rate Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Pick Up - Drop Off Details</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.travels}" var="travel">
                                                        <div style="margin-bottom: 1em;">
                                                            <span style="text-transform:uppercase;font-weight:bold;">{!travel.dayStart}, {!travel.dayNumberStart + ' ' + travel.monthStart + ' ' + travel.yearStart} | {!travel.startDateTime}</span><br/>
                                                            <span>from {!travel.startCity}</span><br/>
                                                            <span>{!if(and(travel.locationType != null,travel.locationType != ''), '(' + travel.locationType + ')','')}</span><br/>
                                                            <!--<span>({!travel.locationPickup})</span><br/>-->
                                                            <span style="text-transform:uppercase;font-weight:bold;">{!travel.dayEnd}, {!travel.dayNumberEnd + ' ' + travel.monthEnd + ' ' + travel.yearEnd} | {!travel.endDateTime}</span><br/>
                                                        	<span>to {!travel.endCity}</span><br/>
                                                            <span>{!if(and(travel.locationDropOffType != null,travel.locationDropOffType != ''), '(' + travel.locationDropOffType + ')','')}</span><br/>
                                                            <!--<span>({!travel.locationDropOff})</span><br/>-->
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Bus Details</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.vehicles}" var="vehicle">
                                                        <div style="margin-bottom: 1em;">
                                                            <span style="font-weight:bold;">{!vehicle.vehicleName}</span> <br/>
                                                            <!--<span>{!if(vehicle.record.Qty_of_Buses__c != null,'QTY ' + vehicle.record.Qty_of_Buses__c,'QTY 0')}</span> <br/>-->
                                                            <span>QTY 1</span> <br/>
                                                            <span>{!if(and(vehicle.make != null,vehicle.model != null),vehicle.make + '/',vehicle.make)}{!vehicle.model} {!if(vehicle.year != null,' ' + vehicle.year,'')}</span> <br/>
                                                            <span>{!if(and(vehicle.capacity != null,vehicle.capacity != ''),vehicle.capacity + ' PAX','')}</span>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Gear / Luggage Space</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.vehicles}" var="vehicle">
                                                        <aura:if isTrue="{!if(vehicle.record.Gear_Luggage_Space__c != null,true,false)}">
                                                            {!vehicle.record.Gear_Luggage_Space__c} <br/>
                                                        </aura:if>
                                                    </aura:iteration>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Amenities</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.amenities}
                                                </div>
                                            </aura:iteration>
                                        </div>                                        
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Additional Fees &amp; Details</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.concessions}" var="concession">
                                                        <div class="slds-p-top_xxx-small slds-text-align_left">
                                                            <!--&bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c,'')} - {!if(and(concession.Rate__c != null, concession.Rate__c > 0), '$','')} {!if(concession.Rate__c != null, concession.Rate__c,'')}, {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' in rate','')}-->
                                                            &bull; {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' - ','')} {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c + ' - ','')}
                                                            <aura:if isTrue="{!if(and(concession.Rate__c != null, concession.Rate__c > 0), true, false)}">
                                                                <lightning:formattedNumber value="{!concession.Rate__c}" style="currency" currencyCode="{!bid.currencyIsoCode}"/>
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
                                            </aura:iteration>
                                        </div>
                                        <!--<div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Gratuity</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!if(and(bid.gratuity != null,bid.gratuity != ''),'$' + bid.gratuity,'')} <br/>
                                                    {!if(and(bid.gratuity != null,bid.gratuity != ''),'included in rate','')}
                                                </div>
                                            </aura:iteration>
                                        </div>-->
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Payments accepted</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.paymentsAccepted}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Payment Policy</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.paymentPolicy}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Cancellation Policy</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.cancellationPolicy}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Total Price</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="font-weight: bold;font-size:16px;">
                                                    <lightning:formattedNumber value="{!bid.totalPrice}" style="currency" currencyCode="{!bid.currencyIsoCode}"/>
                                                    <!--{!if(and(bid.totalPrice != null,bid.totalPrice != ''),'$' + bid.totalPrice,'$0.00')}-->
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header"></div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="text-align: center;">
                                                    <lightning:button label="SELECT" variant="brand" class="formButtonBrand btn-custom" iconName="utility:check" iconPosition="right" value="{!bid.recordId}" onclick="{!c.openReviewSubmit}"/>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="page-section">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1" style="margin-top: 2em;text-align: right;">
                            <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <aura:if isTrue="{!v.openSelectOptionsAlert}">
        <c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}"/>
      </aura:if>	
</aura:component>
```
### VoyajerOptionsGTCompareController

```
({
	doInit : function(component, event, helper) {
        
	},
    openReviewSubmit: function(component,event,helper){
        var bidindex = event.currentTarget.dataset.bidindex;
        var list = component.get("v.bidOptions");
        component.set("v.optionDetailRecordId",bidindex);
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.bidOptionsSize",list.length);
        component.set("v.mainContent","optionsGTReviewSubmit");
    },
    openReviewSubmit : function(component, event, helper) {
      var theURL = window.location.href;
      var isPreview = theURL.includes('VoyajerPreviewApp');
      var okToAdvance = true;
  
      if (isPreview){
        okToAdvance = false;
      } else {
        var list = component.get("v.bidOptions");
        var recordId = event.getSource().get("v.value");
        var index = 0;
        var indexActual;
        okToAdvance = true;
    
        list.forEach(function (bid) {
          if (bid.recordId == recordId) {
            indexActual = index;
          }
          index++;
        });
    
        if ((list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
          okToAdvance = false;
        }
      }
  
      if (okToAdvance) {
        component.set("v.optionDetailRecordId", indexActual);
        component.set("v.bidOptionsSize", list.length);
        component.set("v.mainContent", "optionsGTReviewSubmit");
      } else {
        component.set("v.openSelectOptionsAlert", true);
      }
      
    },
    handleBack : function(component, event, helper){
		component.set("v.mainContent", "optionsGT");
	}
})
```
### VoyajerOptionsGTCompare

```
.THIS .optionBox {
    padding: 1.5em 2em 1.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: white;
    margin: 1.5em 1em 1.5em 0;
    box-shadow: 4px 4px 4px 0 #dbdbdb;
    border-left: 1px solid #dbdbdb;
    border-top: 1px solid #dbdbdb;
}

.THIS .optionBox.left{
    width: 60%;
}

.THIS .optionBox.right{
    width: 38%;
}

.THIS .optionBoxIcon {
    padding-bottom: 1em;
}

.THIS .optionBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .optionBoxName {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 1.25em;
    display: flex;
    align-items: center;
    justify-content: left;
}

.THIS .optionBoxName p {
    line-height: 1.5;
    margin-bottom: 0.2em !important;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    max-height: 3em;
}

.THIS .optionBoxDescription p {
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    min-height: 1.5em;
}

.THIS .optionBoxDescription .room-type {
    min-width: 1.5em;
}

.THIS .pageContentOptions{
    display: flex;
    flex-flow: wrap;
}

.THIS .pageContentForm p {
    margin-bottom: 0 !important;
}

.THIS .recordTable,
.THIS .tableHeader,
.THIS .tableRow {
    display: flex;
    width: 100%;
}

.THIS .recordTable {
    flex-direction: column;
    border: 1px solid #dbdbdb;
    margin: .5em 0 1em;
}

.THIS .tableHeader {
    flex: 1;
    background-color: #f7f9fe;
    font-weight: 500;
}

.THIS .tableRow {
    flex: 1;
    min-width: 0;
}

.THIS .tableList > .tableRow ~ .tableRow {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em 1em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
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

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .slds-card-overview .information-label{
    background-color: #f0f0f0;
    padding: 1.1em;
    color: #00b4ff;
    font-weight:bold;
}

.THIS .slds-card-overview .information-label-other{
    padding: 1.1em;
    font-weight:bold;
    font-size: 12px;
    border-left: 1px solid #f0f0f0;
    border-bottom: 1px solid #f0f0f0
}

.THIS .slds-card-overview .information-label.first{
    margin-top: 4.9em;
}

.THIS .slds-card-overview .information-label-value{
    padding: 1.1em;
    font-size: 12px;
    border-bottom: 1px solid #f0f0f0;
    text-align: center;
}

/*--------------------
-----Compare------
----------------------*/

.THIS .section-compare{
}

.THIS .section-compare .section-compare_header{
}

.THIS .section-compare .section-compare_header > .section-compare_header_space{
    
}

.THIS .section-compare .section-compare_header > .section-compare_header_item .header{
    background-color: #085ee2;
    color: white;
    text-align: center;
    padding: 1.5em;
    font-weight: bold;
    font-size: 1.1em;
}

.THIS .section-compare .section-compare_header > .section-compare_header_item > h3{
    min-height: 5em;
    padding: 1em 2.2em;
    background-color: #0670c8;
    text-align: center;
    font-size: 1.1rem;
    color: white;
}

.THIS .section-compare .section-compare_content{
    margin-top: 0;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header{
    background-color: #eff2f7;
    border-radius: 0;
    font-size:.875rem;
    font-weight: 600;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header > .slds-button-expandable{
    padding: .8em 1.5em;
    text-transform: none;
}

.THIS .section-compare .section-compare_content .section-compare_content_row{
    border: 1px solid #eff2f7;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_header{
    padding: .8em 1.5em;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_content{
    padding: .8em 1.5em;
    text-align: center;
}

/*--------------------
-----Button------
----------------------*/

.THIS .slds-button-expandable{
    background:none;
    justify-content:space-between;
    color:#00b4ff;
}

.THIS .slds-button-expandable:hover,
.THIS .slds-button-expandable:focus,
.THIS .slds-button-expandable:active{
    background: none;
    box-shadow: none;
    color:#00b4ff;
}

.THIS .buttonIcon-bluelight{
    color:#00b4ff;
}

.THIS button.btn-blue{
    padding-left: 3rem;
    padding-right: 3rem;
    background-color: #0065ff;
}

.THIS button.btn-blue:active,
.THIS button.btn-blue:visited,
.THIS button.btn-blue:focus {
    background-color: #0453cc;
}


/*--------------------
-----Medias queries------
----------------------*/

@media (min-width: 768px){
    .THIS .section-compare .section-compare_header > .section-compare_header_space{
        width: 22%;
    }
}
```
### VoyajerOptionsGTCompare

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsGTCompareHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsGTCompare

```
<aura:component>
    <aura:attribute type="String" name="groundId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="compareList" />
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>Compare Options
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(v.serviceData.endCityName != null,' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                                <p>Group Type: {!v.serviceData.groupType}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.serviceData.releaseDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:2em;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-carousel__stage section-compare">
                        <div class="slds-grid slds-wrap">
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-grid slds-gutters_x-small slds-wrap section-compare_header">
                                    <div class="slds-col slds-size_1-of-4">
                                    </div>
                                    <aura:iteration items="{!v.compareList}" var="bid">
                                        <div class="slds-col slds-size_1-of-4 section-compare_header_item">
                                            <div class="header">{!bid.vendor}</div>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Information Details">Information Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Website</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="color: #00b4ff;">
                                                    {!bid.record.Vendor__r.Website}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Address</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingStreet}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>City, State / Postal Code</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingCity + ', ' + bid.record.Vendor__r.ShippingState + ' ' + bid.record.Vendor__r.ShippingPostalCode}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Phone</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.Phone}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Rate Details">Rate Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Pick Up - Drop Off Details</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.travels}" var="travel">
                                                        <div style="margin-bottom: 1em;">
                                                            <span style="text-transform:uppercase;font-weight:bold;">{!travel.dayStart}, {!travel.dayNumberStart + ' ' + travel.monthStart + ' ' + travel.yearStart} | {!travel.startDateTime}</span><br/>
                                                            <span>from {!travel.startCity}</span><br/>
                                                            <span>{!if(and(travel.locationType != null,travel.locationType != ''), '(' + travel.locationType + ')','')}</span><br/>
                                                            <!--<span>({!travel.locationPickup})</span><br/>-->
                                                            <span style="text-transform:uppercase;font-weight:bold;">{!travel.dayEnd}, {!travel.dayNumberEnd + ' ' + travel.monthEnd + ' ' + travel.yearEnd} | {!travel.endDateTime}</span><br/>
                                                        	<span>to {!travel.endCity}</span><br/>
                                                            <span>{!if(and(travel.locationDropOffType != null,travel.locationDropOffType != ''), '(' + travel.locationDropOffType + ')','')}</span><br/>
                                                            <!--<span>({!travel.locationDropOff})</span><br/>-->
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Bus Details</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.vehicles}" var="vehicle">
                                                        <div style="margin-bottom: 1em;">
                                                            <span style="font-weight:bold;">{!vehicle.vehicleName}</span> <br/>
                                                            <!--<span>{!if(vehicle.record.Qty_of_Buses__c != null,'QTY ' + vehicle.record.Qty_of_Buses__c,'QTY 0')}</span> <br/>-->
                                                            <span>QTY 1</span> <br/>
                                                            <span>{!if(and(vehicle.make != null,vehicle.model != null),vehicle.make + '/',vehicle.make)}{!vehicle.model} {!if(vehicle.year != null,' ' + vehicle.year,'')}</span> <br/>
                                                            <span>{!if(and(vehicle.capacity != null,vehicle.capacity != ''),vehicle.capacity + ' PAX','')}</span>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Gear / Luggage Space</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.vehicles}" var="vehicle">
                                                        <aura:if isTrue="{!if(vehicle.record.Gear_Luggage_Space__c != null,true,false)}">
                                                            {!vehicle.record.Gear_Luggage_Space__c} <br/>
                                                        </aura:if>
                                                    </aura:iteration>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Amenities</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.amenities}
                                                </div>
                                            </aura:iteration>
                                        </div>                                        
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Additional Fees &amp; Details</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:iteration items="{!bid.concessions}" var="concession">
                                                        <div class="slds-p-top_xxx-small slds-text-align_left">
                                                            <!--&bull; {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c,'')} - {!if(and(concession.Rate__c != null, concession.Rate__c > 0), '$','')} {!if(concession.Rate__c != null, concession.Rate__c,'')}, {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' in rate','')}-->
                                                            &bull; {!if(concession.Included_Excluded__c != null, concession.Included_Excluded__c + ' - ','')} {!if(concession.Concessions_Requested__c != null, concession.Concessions_Requested__c + ' - ','')}
                                                            <aura:if isTrue="{!if(and(concession.Rate__c != null, concession.Rate__c > 0), true, false)}">
                                                                <lightning:formattedNumber value="{!concession.Rate__c}" style="currency" currencyCode="{!bid.currencyIsoCode}"/>
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
                                            </aura:iteration>
                                        </div>
                                        <!--<div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Gratuity</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!if(and(bid.gratuity != null,bid.gratuity != ''),'$' + bid.gratuity,'')} <br/>
                                                    {!if(and(bid.gratuity != null,bid.gratuity != ''),'included in rate','')}
                                                </div>
                                            </aura:iteration>
                                        </div>-->
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Payments accepted</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.paymentsAccepted}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Payment Policy</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.paymentPolicy}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Cancellation Policy</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.cancellationPolicy}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Total Price</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="font-weight: bold;font-size:16px;">
                                                    <lightning:formattedNumber value="{!bid.totalPrice}" style="currency" currencyCode="{!bid.currencyIsoCode}"/>
                                                    <!--{!if(and(bid.totalPrice != null,bid.totalPrice != ''),'$' + bid.totalPrice,'$0.00')}-->
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header"></div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="text-align: center;">
                                                    <lightning:button label="SELECT" variant="brand" class="formButtonBrand btn-custom" iconName="utility:check" iconPosition="right" value="{!bid.recordId}" onclick="{!c.openReviewSubmit}"/>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="page-section">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1" style="margin-top: 2em;text-align: right;">
                            <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.handleBack}"/>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <aura:if isTrue="{!v.openSelectOptionsAlert}">
        <c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}"/>
      </aura:if>	
</aura:component>
```
### VoyajerOptionsGTCompareController

```
({
	doInit : function(component, event, helper) {
        
	},
    openReviewSubmit: function(component,event,helper){
        var bidindex = event.currentTarget.dataset.bidindex;
        var list = component.get("v.bidOptions");
        component.set("v.optionDetailRecordId",bidindex);
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.bidOptionsSize",list.length);
        component.set("v.mainContent","optionsGTReviewSubmit");
    },
    openReviewSubmit : function(component, event, helper) {
      var theURL = window.location.href;
      var isPreview = theURL.includes('VoyajerPreviewApp');
      var okToAdvance = true;
  
      if (isPreview){
        okToAdvance = false;
      } else {
        var list = component.get("v.bidOptions");
        var recordId = event.getSource().get("v.value");
        var index = 0;
        var indexActual;
        okToAdvance = true;
    
        list.forEach(function (bid) {
          if (bid.recordId == recordId) {
            indexActual = index;
          }
          index++;
        });
    
        if ((list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
          okToAdvance = false;
        }
      }
  
      if (okToAdvance) {
        component.set("v.optionDetailRecordId", indexActual);
        component.set("v.bidOptionsSize", list.length);
        component.set("v.mainContent", "optionsGTReviewSubmit");
      } else {
        component.set("v.openSelectOptionsAlert", true);
      }
      
    },
    handleBack : function(component, event, helper){
		component.set("v.mainContent", "optionsGT");
	}
})
```
### VoyajerOptionsGTCompare

```
.THIS .optionBox {
    padding: 1.5em 2em 1.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: white;
    margin: 1.5em 1em 1.5em 0;
    box-shadow: 4px 4px 4px 0 #dbdbdb;
    border-left: 1px solid #dbdbdb;
    border-top: 1px solid #dbdbdb;
}

.THIS .optionBox.left{
    width: 60%;
}

.THIS .optionBox.right{
    width: 38%;
}

.THIS .optionBoxIcon {
    padding-bottom: 1em;
}

.THIS .optionBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .optionBoxName {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 1.25em;
    display: flex;
    align-items: center;
    justify-content: left;
}

.THIS .optionBoxName p {
    line-height: 1.5;
    margin-bottom: 0.2em !important;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    max-height: 3em;
}

.THIS .optionBoxDescription p {
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    min-height: 1.5em;
}

.THIS .optionBoxDescription .room-type {
    min-width: 1.5em;
}

.THIS .pageContentOptions{
    display: flex;
    flex-flow: wrap;
}

.THIS .pageContentForm p {
    margin-bottom: 0 !important;
}

.THIS .recordTable,
.THIS .tableHeader,
.THIS .tableRow {
    display: flex;
    width: 100%;
}

.THIS .recordTable {
    flex-direction: column;
    border: 1px solid #dbdbdb;
    margin: .5em 0 1em;
}

.THIS .tableHeader {
    flex: 1;
    background-color: #f7f9fe;
    font-weight: 500;
}

.THIS .tableRow {
    flex: 1;
    min-width: 0;
}

.THIS .tableList > .tableRow ~ .tableRow {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em 1em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
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

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .slds-card-overview .information-label{
    background-color: #f0f0f0;
    padding: 1.1em;
    color: #00b4ff;
    font-weight:bold;
}

.THIS .slds-card-overview .information-label-other{
    padding: 1.1em;
    font-weight:bold;
    font-size: 12px;
    border-left: 1px solid #f0f0f0;
    border-bottom: 1px solid #f0f0f0
}

.THIS .slds-card-overview .information-label.first{
    margin-top: 4.9em;
}

.THIS .slds-card-overview .information-label-value{
    padding: 1.1em;
    font-size: 12px;
    border-bottom: 1px solid #f0f0f0;
    text-align: center;
}

/*--------------------
-----Compare------
----------------------*/

.THIS .section-compare{
}

.THIS .section-compare .section-compare_header{
}

.THIS .section-compare .section-compare_header > .section-compare_header_space{
    
}

.THIS .section-compare .section-compare_header > .section-compare_header_item .header{
    background-color: #085ee2;
    color: white;
    text-align: center;
    padding: 1.5em;
    font-weight: bold;
    font-size: 1.1em;
}

.THIS .section-compare .section-compare_header > .section-compare_header_item > h3{
    min-height: 5em;
    padding: 1em 2.2em;
    background-color: #0670c8;
    text-align: center;
    font-size: 1.1rem;
    color: white;
}

.THIS .section-compare .section-compare_content{
    margin-top: 0;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header{
    background-color: #eff2f7;
    border-radius: 0;
    font-size:.875rem;
    font-weight: 600;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header > .slds-button-expandable{
    padding: .8em 1.5em;
    text-transform: none;
}

.THIS .section-compare .section-compare_content .section-compare_content_row{
    border: 1px solid #eff2f7;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_header{
    padding: .8em 1.5em;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_content{
    padding: .8em 1.5em;
    text-align: center;
}

/*--------------------
-----Button------
----------------------*/

.THIS .slds-button-expandable{
    background:none;
    justify-content:space-between;
    color:#00b4ff;
}

.THIS .slds-button-expandable:hover,
.THIS .slds-button-expandable:focus,
.THIS .slds-button-expandable:active{
    background: none;
    box-shadow: none;
    color:#00b4ff;
}

.THIS .buttonIcon-bluelight{
    color:#00b4ff;
}

.THIS button.btn-blue{
    padding-left: 3rem;
    padding-right: 3rem;
    background-color: #0065ff;
}

.THIS button.btn-blue:active,
.THIS button.btn-blue:visited,
.THIS button.btn-blue:focus {
    background-color: #0453cc;
}


/*--------------------
-----Medias queries------
----------------------*/

@media (min-width: 768px){
    .THIS .section-compare .section-compare_header > .section-compare_header_space{
        width: 22%;
    }
}
```

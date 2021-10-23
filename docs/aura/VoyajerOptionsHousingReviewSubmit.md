---
layout: default
title: VoyajerOptionsHousingReviewSubmit
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsHousingReviewSubmit
## Fields
### VoyajerOptionsHousingReviewSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingReviewSubmit

```
<aura:component>
    <aura:attribute type="String" name="housingId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="String" name="comments" default="" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />
    <!-- Changes as per 176793176 -->
    <aura:attribute type="String" name="lengthDiv" default="0 of 255" />
    <aura:attribute type="List" name="preferencesSelected" default="['Bus Parking','Valet parking','Self-Parking','Room Service','Comp Breakfast','Hotel Restaurant(s)','Hotel Bar(s)','Airport Shuttle','Hotel Shuttle','Fitness Room','Pool/Hot tub','Safe','Bathtub','Hairdryer','Coffee maker','Refrigerator','Microwave','Rooms / Suites #','Star Rating','Year Built / Renovated','100% Non-Smoking','Lift / Elevator','Property Entry','Porterage','Windows that open','Air conditioning','High Speed Internet','Pets Allowed']" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fab fa-telegram-plane" style="font-size: 0.7em;"></i> Review &amp; Submit
                        </h1>
                        <lightning:button label="BACK TO THE OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}" />
                    </div>
                </div>
                <div class="pageContentForm header">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1 optionBox">
                            <div class="slds-grid slds-wrap" style="padding-bottom: 1em;border-bottom: 1px solid #dbdbdb;">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                    <div class="optionBoxName">
                                        <p title="Report Name">{!v.optionDetailRecord.vendor}</p>
                                    </div>
                                    <div class="optionBoxDescription">
                                        <p>
                                            <aura:iteration items="{!v.optionDetailRecord.stars}" var="star">
                                                <i class="fas fa-star" style="color: #ffa000"></i>
                                            </aura:iteration>
                                        </p>
                                        <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_venue}</p>
                                        <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.optionDetailRecord.physical}</p>
                                        <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">
                                            <aura:if isTrue="{!and(v.optionDetailRecord.website != null, v.optionDetailRecord.website != '')}">
                                                <lightning:formattedText linkify="true" value="{!v.optionDetailRecord.website}" />
                                            </aura:if>
                                        </p>
                                        <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_onevenue}</p>
                                        <!-- Fix By Clay Dev 31 Jan, 2021 #176367796-->
                                        <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                                        <!--<p>
                                        <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                                        <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                        <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                        <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                    </p>-->
                                        <p>
                                            <a href="javascript:void(0)" data-bidindex="{!v.optionDetailRecordId}" onclick="{!c.openOptionDetail}" style="font-size: 12px;font-weight: bold;">
                                                VIEW DETAILS
                                            </a>
                                        </p>
                                    </div>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right;">
                                    <div class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;">
                                            <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName}</span> | <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.dateIn} - {!v.serviceData.dateOut}</span>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;margin-bottom: 1em;">
                                            <div class="slds-grid slds-wrap">
                                                <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_4-of-5">
                                                        <span class="room-type" style="padding-right: 0.5em;">{!roomtype.Units__c}</span> - 
                                                        <span class="room-type" style="padding-left: 0.5em;">{!roomtype.Unit_Type__c}</span>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5" style="text-align: right;">
                                                        <span class="room-type" style="font-weight:bold;">
                                                            <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                            <!--${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}-->
                                                        </span>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div style="margin-top: 1em;">
                                                <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                                    Total Rate
                                                    <span style="margin-left: 1em;">
                                                        <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                                   style="currency" 
                                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                   currencyDisplayAs="symbol" />
                                                        <!--${!v.optionDetailRecord.avgrate}-->
                                                    </span>
                                                </span>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div style="margin-top: 1em;">
                                                <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                                    Weighted Avg Rate
                                                    <span style="margin-left: 1em;">
                                                        <lightning:formattedNumber value="{!v.optionDetailRecord.avgrate}" 
                                                                                   style="currency" 
                                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                   currencyDisplayAs="symbol" />
                                                        <!--${!v.optionDetailRecord.avgrate}-->
                                                    </span>
                                                </span>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                            	<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                    <span style="font-size: 12px;font-weight: bold;">Add Comments</span>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                    <div class="formField">
                                        <!-- Changes as per 176793176 -->
                                        <lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" aura:id="recordField" name="" label="" value="{!v.comments}" variant="label-hidden" />
                                        <!--lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" value="{!v.info.notes}" aura:id="notesTxtBox" class="formTextarea" variant="label-hidden" /-->
                        	            <div style="float:right;">{!v.lengthDiv}</div>
                                    </div>
                                </div>
                            </div>
                        </div>  
                        <div class="slds-col slds-size_1-of-1" style="text-align: right;">
                        	<lightning:button label="CANCEL" variant="neutral" onclick="{!c.backOptionsHousing}" />
                            <lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
	
</aura:component>
```
### VoyajerOptionsHousingReviewSubmit

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

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}
```
### VoyajerOptionsHousingReviewSubmitHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsHousingReviewSubmitController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadOptionsHousingDetail");
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    
    backOptionsHousing: function(component,event,helper){
        component.set("v.mainContent","optionsHousing");
    },

    //Changes as per 176793176
    checkLength : function(component, event, helper) {
        component.set('v.lengthDiv', '');
        var notesTxtBoxVal = component.find("recordField").get("v.value");
        component.set('v.lengthDiv', notesTxtBoxVal.length  + ' of 255');
    },
    
    openOptionDetail: function(component,event,helper){
        var bidindex = event.currentTarget.dataset.bidindex;
        var list = component.get("v.bidOptions");
        component.set("v.optionDetailRecordId",bidindex);
        component.set("v.mainContent","optionsHousingDetail");
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.bidOptionsSize",list.length);
    },
    
    submitSelection: function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","submitOptionSelected");
        callToParent.setParam("data",{
            serviceType: "housing",
            serviceId: component.get("v.housingId"),
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
### VoyajerOptionsHousingReviewSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingReviewSubmit

```
<aura:component>
    <aura:attribute type="String" name="housingId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="String" name="comments" default="" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />
    <!-- Changes as per 176793176 -->
    <aura:attribute type="String" name="lengthDiv" default="0 of 255" />
    <aura:attribute type="List" name="preferencesSelected" default="['Bus Parking','Valet parking','Self-Parking','Room Service','Comp Breakfast','Hotel Restaurant(s)','Hotel Bar(s)','Airport Shuttle','Hotel Shuttle','Fitness Room','Pool/Hot tub','Safe','Bathtub','Hairdryer','Coffee maker','Refrigerator','Microwave','Rooms / Suites #','Star Rating','Year Built / Renovated','100% Non-Smoking','Lift / Elevator','Property Entry','Porterage','Windows that open','Air conditioning','High Speed Internet','Pets Allowed']" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fab fa-telegram-plane" style="font-size: 0.7em;"></i> Review &amp; Submit
                        </h1>
                        <lightning:button label="BACK TO THE OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}" />
                    </div>
                </div>
                <div class="pageContentForm header">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1 optionBox">
                            <div class="slds-grid slds-wrap" style="padding-bottom: 1em;border-bottom: 1px solid #dbdbdb;">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                    <div class="optionBoxName">
                                        <p title="Report Name">{!v.optionDetailRecord.vendor}</p>
                                    </div>
                                    <div class="optionBoxDescription">
                                        <p>
                                            <aura:iteration items="{!v.optionDetailRecord.stars}" var="star">
                                                <i class="fas fa-star" style="color: #ffa000"></i>
                                            </aura:iteration>
                                        </p>
                                        <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_venue}</p>
                                        <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.optionDetailRecord.physical}</p>
                                        <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">
                                            <aura:if isTrue="{!and(v.optionDetailRecord.website != null, v.optionDetailRecord.website != '')}">
                                                <lightning:formattedText linkify="true" value="{!v.optionDetailRecord.website}" />
                                            </aura:if>
                                        </p>
                                        <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_onevenue}</p>
                                        <!-- Fix By Clay Dev 31 Jan, 2021 #176367796-->
                                        <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                                        <!--<p>
                                        <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                                        <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                        <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                        <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                    </p>-->
                                        <p>
                                            <a href="javascript:void(0)" data-bidindex="{!v.optionDetailRecordId}" onclick="{!c.openOptionDetail}" style="font-size: 12px;font-weight: bold;">
                                                VIEW DETAILS
                                            </a>
                                        </p>
                                    </div>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right;">
                                    <div class="slds-grid slds-wrap">
                                        <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;">
                                            <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName}</span> | <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.dateIn} - {!v.serviceData.dateOut}</span>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;margin-bottom: 1em;">
                                            <div class="slds-grid slds-wrap">
                                                <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_4-of-5">
                                                        <span class="room-type" style="padding-right: 0.5em;">{!roomtype.Units__c}</span> - 
                                                        <span class="room-type" style="padding-left: 0.5em;">{!roomtype.Unit_Type__c}</span>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5" style="text-align: right;">
                                                        <span class="room-type" style="font-weight:bold;">
                                                            <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                            <!--${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}-->
                                                        </span>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div style="margin-top: 1em;">
                                                <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                                    Total Rate
                                                    <span style="margin-left: 1em;">
                                                        <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                                   style="currency" 
                                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                   currencyDisplayAs="symbol" />
                                                        <!--${!v.optionDetailRecord.avgrate}-->
                                                    </span>
                                                </span>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div style="margin-top: 1em;">
                                                <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                                    Weighted Avg Rate
                                                    <span style="margin-left: 1em;">
                                                        <lightning:formattedNumber value="{!v.optionDetailRecord.avgrate}" 
                                                                                   style="currency" 
                                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                   currencyDisplayAs="symbol" />
                                                        <!--${!v.optionDetailRecord.avgrate}-->
                                                    </span>
                                                </span>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                            	<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                    <span style="font-size: 12px;font-weight: bold;">Add Comments</span>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                                    <div class="formField">
                                        <!-- Changes as per 176793176 -->
                                        <lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" aura:id="recordField" name="" label="" value="{!v.comments}" variant="label-hidden" />
                                        <!--lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" value="{!v.info.notes}" aura:id="notesTxtBox" class="formTextarea" variant="label-hidden" /-->
                        	            <div style="float:right;">{!v.lengthDiv}</div>
                                    </div>
                                </div>
                            </div>
                        </div>  
                        <div class="slds-col slds-size_1-of-1" style="text-align: right;">
                        	<lightning:button label="CANCEL" variant="neutral" onclick="{!c.backOptionsHousing}" />
                            <lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
	
</aura:component>
```
### VoyajerOptionsHousingReviewSubmit

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

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}
```
### VoyajerOptionsHousingReviewSubmitHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsHousingReviewSubmitController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadOptionsHousingDetail");
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    
    backOptionsHousing: function(component,event,helper){
        component.set("v.mainContent","optionsHousing");
    },

    //Changes as per 176793176
    checkLength : function(component, event, helper) {
        component.set('v.lengthDiv', '');
        var notesTxtBoxVal = component.find("recordField").get("v.value");
        component.set('v.lengthDiv', notesTxtBoxVal.length  + ' of 255');
    },
    
    openOptionDetail: function(component,event,helper){
        var bidindex = event.currentTarget.dataset.bidindex;
        var list = component.get("v.bidOptions");
        component.set("v.optionDetailRecordId",bidindex);
        component.set("v.mainContent","optionsHousingDetail");
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.bidOptionsSize",list.length);
    },
    
    submitSelection: function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","submitOptionSelected");
        callToParent.setParam("data",{
            serviceType: "housing",
            serviceId: component.get("v.housingId"),
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

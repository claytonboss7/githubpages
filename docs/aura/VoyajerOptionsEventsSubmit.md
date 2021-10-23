---
layout: default
title: VoyajerOptionsEventsSubmit
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsEventsSubmit
## Fields
### VoyajerOptionsEventsSubmit

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerOptionsEventsSubmit

```
<aura:component>
	<aura:attribute type="String" name="housingId" />
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="officePreference" />
	<aura:attribute type="String" name="comments" default="" />
	<aura:attribute type="Object" name="serviceData" />
	<aura:attribute type="Integer" name="optionDetailRecordId" />
	<aura:attribute type="List" name="bidOptions" />
	<aura:attribute type="List" name="bidsSelected" />
	<aura:attribute type="List" name="lodgingRecords" default="['cityTitle','Test']" />
	<aura:attribute type="Object" name="optionDetailRecord" />
	<aura:attribute type="Integer" name="optionDetailRecordIdReal" />
	<aura:attribute type="Integer" name="bidOptionsSize" />
	<aura:attribute type="Integer" name="firstTime" default="1"/>
	<aura:attribute
		type="List"
		name="preferencesSelected"
		default="['Bus Parking','Valet parking','Self-Parking','Room Service','Comp Breakfast','Hotel Restaurant(s)','Hotel Bar(s)','Airport Shuttle','Hotel Shuttle','Fitness Room','Pool/Hot tub','Safe','Bathtub','Hairdryer','Coffee maker','Refrigerator','Microwave','Rooms / Suites #','Star Rating','Year Built / Renovated','100% Non-Smoking','Lift / Elevator','Property Entry','Porterage','Windows that open','Air conditioning','High Speed Internet','Pets Allowed']"
	/>
	<aura:attribute type="Integer" name="recordOpened" default="-1"/>
	<aura:attribute type="Boolean" name="showRecordDetails" default="true" />
	<aura:attribute type="Boolean" name="showOtherDetails" default="true" />
	<aura:attribute type="Object" name="itineraryData" />

	<aura:handler name="init" value="{!this}" action="{!c.doInit}" />
	<aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

	<div class="pageContent">
		<div class="pageContentSpaces">
			<div class="page-header">
				<h1 class="page-header-title"><i class="fab fa-telegram-plane" style="font-size: 0.7em"></i> Review &amp; Submit</h1>
				<lightning:button
					label="BACK TO THE OPTIONS"
					variant="brand"
					class="formButtonBrandLight btn-custom"
					onclick="{!c.backOptionsHousing}"
				/>
			</div>
			<!---->
			<aura:iteration items="{!v.bidsSelected}" var="option" indexVar="lodgingIndex">
				<div class="page-section" style="align-items: center; width: 100%">
					<div class="page-section_record">
						<!--<c:VoyajerOptionsHousingReviewItem optionDetailRecord="{!option}" />-->
						<div class="recordHeader">
							<div
								class="recordBodySideColumn"
								style="{!if(true==true,'background-color: #0065ff; color: white;',if(true==true,'background-color: #ff0000; color: white;',''))}"
							>
								<span>{!lodgingIndex+1}</span>
							</div>
							<div class="recordTitle">
								<div class="recordTitleText">
									<aura:if isTrue="true">
										<div class="location" title="{!'Stay '+(lodgingIndex+1)}">{!option.record.Vendor__r.Name}</div>
										<aura:set attribute="else">
											<div class="location" title="asdf">asdf</div>
											<div class="dates">date 1 - date 2</div>
										</aura:set>
									</aura:if>
								</div>
								<div class="recordTitleButton">
									<lightning:buttonIcon
										iconName="{!v.recordOpened==lodgingIndex?'utility:up':'utility:down'}"
										value="{!lodgingIndex}"
										variant="bare"
										alternativeText="Open"
										onclick="{!c.handleShowRecord}"
									/>
								</div>
							</div>
						</div>
						<aura:if isTrue="{!v.recordOpened==lodgingIndex||and(v.firstTime==1,lodgingIndex==0)?true:false}">
							<div class="recordBody">
								<div
									class="recordBodySideColumn hideOnMobile"
									style="{!if(true==true,'background-color: #c5dcff;',if(true==true,'background-color: #ffe9e9;',''))}"
								></div>
								<aura:if isTrue="{!v.showRecordDetails==true}">
									<c:VoyajerOptionsHousingReviewItem optionDetailRecord="{!option}" serviceData="{!v.serviceData}" optionIndex="{!lodgingIndex}" />
								</aura:if>
							</div>
						</aura:if>
					</div>

					<!--
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
                                                                    <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                                                                    <p>
                                                                    <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                                                                    <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                                                    <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                                                    <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                                                </p>-
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
                                                                                        ${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}
                                                                                    </span>
                                                                                </div>
                                                                            </aura:iteration>
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
                                                                                    ${!v.optionDetailRecord.avgrate}
                                                                                </span>
                                                                            </span>
                                                                        </div>
                                                                    </div>
                                                                    <div class="slds-col slds-size_1-of-1">
                                                                        <div style="margin-top: 1em;">
                                                                            <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                                                                Total Cost
                                                                                <span style="margin-left: 1em;">
                                                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                                                            style="currency" 
                                                                                                            currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                                            currencyDisplayAs="symbol" />
                                                                                    ${!v.optionDetailRecord.avgrate}
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
                                                                    <lightning:textarea aura:id="recordField" name="" label="" value="{!v.comments}" variant="label-hidden" />
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>  
                                                    </div>
                                            </div>
                                        
                                        </div>
                                    </aura:if>
                                </div>-->
				</div>
				<br />
			</aura:iteration>

			<div class="slds-grid slds-wrap" style="margin-top: 1em">
				<div class="slds-col slds-size_1-of-1" style="text-align: right">
					<lightning:button label="CANCEL" variant="neutral" onclick="{!c.backOptionsAir}" />
					<lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
				</div>
			</div>
		</div>
	</div>
</aura:component>
```
### VoyajerOptionsEventsSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>50.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsEventsSubmit

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
### VoyajerOptionsEventsSubmit

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerOptionsEventsSubmitRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerOptionsEventsSubmitHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerOptionsEventsSubmit

```
<design:component >

</design:component>
```
### VoyajerOptionsEventsSubmitController

```
({
	backOptionsHousing: function (component, event, helper) {
		component.set("v.mainContent", "optionsHousing");
	},

	openOptionDetail: function (component, event, helper) {
		var bidindex = event.currentTarget.dataset.bidindex;
		var list = component.get("v.bidOptions");
		component.set("v.optionDetailRecordId", bidindex);
		component.set("v.mainContent", "optionsHousingDetail");
		component.set("v.optionDetailRecordIdReal", parseInt(bidindex) + 1);
		component.set("v.bidOptionsSize", list.length);
	},

	submitSelection: function (component, event, helper) {
		var callToParent = component.getEvent("callToParent");
		callToParent.setParam("action", "submitMultipleOptionsSelected");
		callToParent.setParam("data", {
			serviceType: "housing",
			//Fix By Clay Dev 30 March, 2021, #177544779
			submittedBids: component.get("v.bidsSelected"),
			comments: component.get("v.comments"),
		});
		callToParent.fire();
		console.log("fired event with submitMultipleOptionsSelected");
	},

	doInit: function (component, event, helper) {
		component.set("v.recordOpened", "-1");
		var callToParent = component.getEvent("callToParent");
		callToParent.setParam("action", "loadOptionsHousing");
		callToParent.fire();
		console.log("after event for loadmultipleoptions");
	},
	handleShowRecord: function (cmp, event, helper) {
		var index = parseInt(event.getSource().get("v.value"));
		console.log("value :: " + index);
		var recordOpened = cmp.get("v.recordOpened");
		console.log("recordOpened :: " + recordOpened);
		cmp.set("v.showRecordDetails", true);
		cmp.set("v.showOtherDetails", true);
		if (recordOpened !== index && cmp.get("v.firstTime") === 0) cmp.set("v.recordOpened", index);
		else cmp.set("v.recordOpened", "-1");
		cmp.set("v.firstTime", 0);
	},
});
```
### VoyajerOptionsEventsSubmit

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerOptionsEventsSubmit

```
<aura:component>
	<aura:attribute type="String" name="housingId" />
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="officePreference" />
	<aura:attribute type="String" name="comments" default="" />
	<aura:attribute type="Object" name="serviceData" />
	<aura:attribute type="Integer" name="optionDetailRecordId" />
	<aura:attribute type="List" name="bidOptions" />
	<aura:attribute type="List" name="bidsSelected" />
	<aura:attribute type="List" name="lodgingRecords" default="['cityTitle','Test']" />
	<aura:attribute type="Object" name="optionDetailRecord" />
	<aura:attribute type="Integer" name="optionDetailRecordIdReal" />
	<aura:attribute type="Integer" name="bidOptionsSize" />
	<aura:attribute type="Integer" name="firstTime" default="1"/>
	<aura:attribute
		type="List"
		name="preferencesSelected"
		default="['Bus Parking','Valet parking','Self-Parking','Room Service','Comp Breakfast','Hotel Restaurant(s)','Hotel Bar(s)','Airport Shuttle','Hotel Shuttle','Fitness Room','Pool/Hot tub','Safe','Bathtub','Hairdryer','Coffee maker','Refrigerator','Microwave','Rooms / Suites #','Star Rating','Year Built / Renovated','100% Non-Smoking','Lift / Elevator','Property Entry','Porterage','Windows that open','Air conditioning','High Speed Internet','Pets Allowed']"
	/>
	<aura:attribute type="Integer" name="recordOpened" default="-1"/>
	<aura:attribute type="Boolean" name="showRecordDetails" default="true" />
	<aura:attribute type="Boolean" name="showOtherDetails" default="true" />
	<aura:attribute type="Object" name="itineraryData" />

	<aura:handler name="init" value="{!this}" action="{!c.doInit}" />
	<aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

	<div class="pageContent">
		<div class="pageContentSpaces">
			<div class="page-header">
				<h1 class="page-header-title"><i class="fab fa-telegram-plane" style="font-size: 0.7em"></i> Review &amp; Submit</h1>
				<lightning:button
					label="BACK TO THE OPTIONS"
					variant="brand"
					class="formButtonBrandLight btn-custom"
					onclick="{!c.backOptionsHousing}"
				/>
			</div>
			<!---->
			<aura:iteration items="{!v.bidsSelected}" var="option" indexVar="lodgingIndex">
				<div class="page-section" style="align-items: center; width: 100%">
					<div class="page-section_record">
						<!--<c:VoyajerOptionsHousingReviewItem optionDetailRecord="{!option}" />-->
						<div class="recordHeader">
							<div
								class="recordBodySideColumn"
								style="{!if(true==true,'background-color: #0065ff; color: white;',if(true==true,'background-color: #ff0000; color: white;',''))}"
							>
								<span>{!lodgingIndex+1}</span>
							</div>
							<div class="recordTitle">
								<div class="recordTitleText">
									<aura:if isTrue="true">
										<div class="location" title="{!'Stay '+(lodgingIndex+1)}">{!option.record.Vendor__r.Name}</div>
										<aura:set attribute="else">
											<div class="location" title="asdf">asdf</div>
											<div class="dates">date 1 - date 2</div>
										</aura:set>
									</aura:if>
								</div>
								<div class="recordTitleButton">
									<lightning:buttonIcon
										iconName="{!v.recordOpened==lodgingIndex?'utility:up':'utility:down'}"
										value="{!lodgingIndex}"
										variant="bare"
										alternativeText="Open"
										onclick="{!c.handleShowRecord}"
									/>
								</div>
							</div>
						</div>
						<aura:if isTrue="{!v.recordOpened==lodgingIndex||and(v.firstTime==1,lodgingIndex==0)?true:false}">
							<div class="recordBody">
								<div
									class="recordBodySideColumn hideOnMobile"
									style="{!if(true==true,'background-color: #c5dcff;',if(true==true,'background-color: #ffe9e9;',''))}"
								></div>
								<aura:if isTrue="{!v.showRecordDetails==true}">
									<c:VoyajerOptionsHousingReviewItem optionDetailRecord="{!option}" serviceData="{!v.serviceData}" optionIndex="{!lodgingIndex}" />
								</aura:if>
							</div>
						</aura:if>
					</div>

					<!--
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
                                                                    <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                                                                    <p>
                                                                    <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                                                                    <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                                                    <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                                                    <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                                                </p>-
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
                                                                                        ${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}
                                                                                    </span>
                                                                                </div>
                                                                            </aura:iteration>
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
                                                                                    ${!v.optionDetailRecord.avgrate}
                                                                                </span>
                                                                            </span>
                                                                        </div>
                                                                    </div>
                                                                    <div class="slds-col slds-size_1-of-1">
                                                                        <div style="margin-top: 1em;">
                                                                            <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                                                                Total Cost
                                                                                <span style="margin-left: 1em;">
                                                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                                                            style="currency" 
                                                                                                            currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                                            currencyDisplayAs="symbol" />
                                                                                    ${!v.optionDetailRecord.avgrate}
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
                                                                    <lightning:textarea aura:id="recordField" name="" label="" value="{!v.comments}" variant="label-hidden" />
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </div>  
                                                    </div>
                                            </div>
                                        
                                        </div>
                                    </aura:if>
                                </div>-->
				</div>
				<br />
			</aura:iteration>

			<div class="slds-grid slds-wrap" style="margin-top: 1em">
				<div class="slds-col slds-size_1-of-1" style="text-align: right">
					<lightning:button label="CANCEL" variant="neutral" onclick="{!c.backOptionsAir}" />
					<lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
				</div>
			</div>
		</div>
	</div>
</aura:component>
```
### VoyajerOptionsEventsSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>50.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsEventsSubmit

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
### VoyajerOptionsEventsSubmit

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerOptionsEventsSubmitRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerOptionsEventsSubmitHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerOptionsEventsSubmit

```
<design:component >

</design:component>
```
### VoyajerOptionsEventsSubmitController

```
({
	backOptionsHousing: function (component, event, helper) {
		component.set("v.mainContent", "optionsHousing");
	},

	openOptionDetail: function (component, event, helper) {
		var bidindex = event.currentTarget.dataset.bidindex;
		var list = component.get("v.bidOptions");
		component.set("v.optionDetailRecordId", bidindex);
		component.set("v.mainContent", "optionsHousingDetail");
		component.set("v.optionDetailRecordIdReal", parseInt(bidindex) + 1);
		component.set("v.bidOptionsSize", list.length);
	},

	submitSelection: function (component, event, helper) {
		var callToParent = component.getEvent("callToParent");
		callToParent.setParam("action", "submitMultipleOptionsSelected");
		callToParent.setParam("data", {
			serviceType: "housing",
			//Fix By Clay Dev 30 March, 2021, #177544779
			submittedBids: component.get("v.bidsSelected"),
			comments: component.get("v.comments"),
		});
		callToParent.fire();
		console.log("fired event with submitMultipleOptionsSelected");
	},

	doInit: function (component, event, helper) {
		component.set("v.recordOpened", "-1");
		var callToParent = component.getEvent("callToParent");
		callToParent.setParam("action", "loadOptionsHousing");
		callToParent.fire();
		console.log("after event for loadmultipleoptions");
	},
	handleShowRecord: function (cmp, event, helper) {
		var index = parseInt(event.getSource().get("v.value"));
		console.log("value :: " + index);
		var recordOpened = cmp.get("v.recordOpened");
		console.log("recordOpened :: " + recordOpened);
		cmp.set("v.showRecordDetails", true);
		cmp.set("v.showOtherDetails", true);
		if (recordOpened !== index && cmp.get("v.firstTime") === 0) cmp.set("v.recordOpened", index);
		else cmp.set("v.recordOpened", "-1");
		cmp.set("v.firstTime", 0);
	},
});
```

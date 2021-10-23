---
layout: default
title: VoyajerOptionsFreightCompare
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsFreightCompare
## Fields
### VoyajerOptionsFreightCompareController

```
({
	onInit : function(component, event, helper){
		//helper.getData(component, "searchBidOptions");
	},
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	},
	handleViewAllOptions : function(component, event, helper){
		component.set("v.content", "all");
	},
	handlePrevBids : function(component, event, helper){
		helper.setControls(component, "prevBids");
	},
	handleNextBids : function(component, event, helper){
		helper.setControls(component, "nextBids");
	},
	handleNavigation : function(component, event, helper){
		event.preventDefault();
		console.log("$(event.currentTarget).text(): " + $(event.currentTarget).text());
		component.find("navigationService").navigate({
			type: "standard__webPage",
			attributes: {
				url: $(event.currentTarget).text()
			}
		});		
	},
	handleExpand : function(component, event, helper){
		$(event.currentTarget).parents('.slds-section').toggleClass("slds-is-open");
	}
})
```
### VoyajerOptionsFreightCompare

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsFreightCompare

```
<aura:component controller="VoyajerOptionsFreightController" implements="force:appHostable,flexipage:availableForAllPageTypes">
    <aura:attribute name="content" type="String"/>
    <aura:attribute name="itinerary" type="Object"/>
    <aura:attribute name="bidsSelected" type="List"/>
    <ltng:require scripts="{!$Resource.UltimateUtils + '/js/jquery-3.3.1.min.js'}"/>
    
    <aura:handler name="init" value="{!this}" action="{!c.onInit}" />
    <aura:handler name="render" value="{!this}" action="{!c.onRender}" />
    <div>
        <lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
        <div class="pageContent" style="min-height:680px;">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">Options</h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="btn btn-bluelight" onclick="{!c.handleViewAllOptions}"/>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><i class="fas fa-shield-alt" style="color: #9f9f9f; margin-left: 0.5em;"></i><strong style="color:black;">{!!empty(v.itinerary.Production__r) ? v.itinerary.Production__r.Name : ''}</strong></h3>
                                <p style="margin-left: 0.5em;font-weight:bold;color:#00b4ff;">{!(!empty(v.itinerary.Start_city__r) ? ((!empty(v.itinerary.Start_city__r.City__c) ? v.itinerary.Start_city__r.City__c : '') + (!empty(v.itinerary.Start_city__r.State__c) ? ', ' + v.itinerary.Start_city__r.State__c : '')) : '') + ' to ' + (!empty(v.itinerary.End_city__r) ? ((!empty(v.itinerary.End_city__r.City__c) ? v.itinerary.End_city__r.City__c : '') + (!empty(v.itinerary.End_city__r.State__c) ? ', ' + v.itinerary.End_city__r.State__c : '')) : '') + ' | ' + (!empty(v.itinerary.Start_Date__c) ? v.itinerary.Start_Date__c : '') + (!empty(v.itinerary.End_Date__c) ? ' - ' + v.itinerary.End_Date__c : '')}</p>
                                <p style="margin-left: 0.5em;">Freight Type: {!!empty(v.itinerary.Service_Type__c) ? ' - ' + v.itinerary.Service_Type__c : ''}</p>
                                <p style="margin-left: 0.5em;">Contents: {!!empty(v.itinerary.Freight_Trip_Contents__c) ? ' - ' + v.itinerary.Freight_Trip_Contents__c : ''}</p>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    12/17/18
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <section class="slds-grid slds-gutters slds-wrap">
                        <div class="slds-col slds-size_1-of-1">
                            <div class="slds-carousel carousel">
                                <div class="slds-carousel__col-center slds-is-absolute slds-hide_large carousel-control_left" style="{!v.bidsSelected.length > 1 ? '' : 'display:none;'}">
                                    <button type="button" class="slds-button slds-button_icon-border-filled slds-button_icon-small slds-button_icon slds-carousel__button" onclick="{!c.handlePrevBids}">
                                        <lightning:icon iconName="utility:chevronleft" size="x-small"/>
                                        <span class="slds-assistive-text">Previous</span>
                                    </button>
                                </div>                          
                                <div class="slds-carousel__stage section-compare">
                                    <div class="slds-carousel__panels slds-is-relative slds-grid slds-wrap" aura:id="bids">
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-grid slds-gutters_x-small section-compare_header">
                                                <div class="slds-col slds-size_1-of-1 slds-show_large section-compare_header_space">
                                                    <lightning:navigation aura:id="navigationService"/> 
                                                </div>
                                                <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                    <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_2-of-4' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-4 section-compare_header_item' + (i > 0 ? ' header_margin-left' : '')}">
                                                        <h3 class="slds-align_absolute-center"><strong>{!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Name : ''}</strong></h3>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-section slds-is-open section-compare_content">
                                                <h4 class="slds-section__title section-compare_content_header">
                                                    <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-show_large slds-button-expandable" onclick="{!c.handleExpand}">
                                                        <span class="slds-truncate" title="Information Details">Information Details</span>
                                                        <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                                    </button>
                                                </h4>
                                                <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-1 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-hide_large section-compare_content_row_header' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <strong style="color:#00b4ff;">Information Details</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Website</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <a onclick="{!c.handleNavigation}" class="website">{!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Website : ''}</a>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Address</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    {!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.ShippingStreet : ''}
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>City. State / Postal Code</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    {!(!empty(bid.record.Vendor__r) ? (!empty(bid.record.Vendor__r.ShippingCity) ? bid.record.Vendor__r.ShippingCity + ', ' : '') + (!empty(bid.record.Vendor__r.ShippingState) ? bid.record.Vendor__r.ShippingState + ' ' : '') + (!empty(bid.record.Vendor__r.ShippingPostalCode) ? bid.record.Vendor__r.ShippingPostalCode : '') : '')}
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Phone</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    {!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Phone : ''}
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-section slds-is-open section-compare_content">
                                                <h4 class="slds-section__title section-compare_content_header">
                                                    <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-show_large slds-button-expandable" onclick="{!c.handleExpand}">
                                                        <span class="slds-truncate" title="Rate Details">Rate Details</span>
                                                        <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                                    </button>
                                                </h4>
                                                <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-1 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-hide_large section-compare_content_row_header' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <strong style="color:#00b4ff;">Rate Details</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Pick Up - Drop Off Details</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <aura:iteration items="{!bid.relatedRecords}" var="subtrip">
                                                                        <aura:if isTrue="{!!empty(subtrip.FreightEquipments__r)}">
                                                                            <aura:iteration items="{!subtrip.FreightEquipments__r.records}" var="travel" indexVar="i">
                                                                                <p style="{!subtrip.FreightEquipments__r.totalSize - 1 != i ? 'margin-bottom:1.8em;' : ''}">
                                                                                    <strong style="text-transform:uppercase;">
                                                                                        <c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="EEE, dd MMM yyyy"/> | {!!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : ''}<br/>
                                                                                    </strong>
                                                                                    from {!!empty(travel.Location_Details__c) ? travel.Location_Details__c : ''} <br/>
                                                                                    {!!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c : ''} <br/>
                                                                                    <strong style="text-transform:uppercase;">
                                                                                        <c:auraFormattedDate date="{!travel.End_Date__c}" dateFormat="EEE, dd MMM yyyy"/> | {!!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : ''}<br/>
                                                                                    </strong>
                                                                                    from {!!empty(travel.Location_Details_Drop_Off__c) ? travel.Location_Details_Drop_Off__c : ''} <br/>
                                                                                    {!!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c : ''}
                                                                                </p>
                                                                            </aura:iteration>
                                                                        </aura:if>
                                                                    </aura:iteration>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Freight Truck sq ft</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>fuel</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>loading / unloading</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Cargo List</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Cargo List</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Payment Terms</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Total Price</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_header' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <lightning:button label="SELECT" variant="brand" iconName="utility:check" iconPosition="right" class="btn btn-blue" onclick="{!c.handleViewAllOptions}"/>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-carousel__col-center slds-is-absolute slds-hide_large carousel-control_right" style="{!v.bidsSelected.length > 1 ? '' : 'display:none;'}">
                                    <button type="button" class="slds-button slds-button_icon-border-filled slds-button_icon-small slds-button_icon slds-carousel__button" onclick="{!c.handleNextBids}">
                                        <lightning:icon iconName="utility:chevronright" size="x-small"/>
                                        <span class="slds-assistive-text">Next</span>
                                    </button>
                                </div>                        
                            </div>                         
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerOptionsFreightCompare

```
/*
	Version:	    V1.0
	Create Date:	2/17/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}

/*--------------------
-----Carousel------
----------------------*/

.THIS .carousel{
}

.THIS .carousel .carousel-control_left{
    top: 2em;
    left: 2%;
    z-index: 1;
}

.THIS .carousel .carousel-control_right{
    top: 2em;
    right: 2%;
    z-index: 1;
}

.THIS .prev_bid{
    transform: translateX(0%);
}

.THIS .prev_bid2{
    transform: translateX(-100%);
}

.THIS .next_bid{
    transform: translateX(-100%);
}

.THIS .next_bid2{
    transform: translateX(-200%);
}

/*--------------------
-----Compare------
----------------------*/

.THIS .section-compare{
}

.THIS .section-compare .section-compare_header{
}

.THIS .section-compare .section-compare_header .section-compare_header_space{
    
}

.THIS .section-compare .section-compare_header .section-compare_header_item > h3{
    min-height: 5em;
    padding: 0 .5em;
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
    border: none;
}

.THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    padding: .8em;
    border-bottom: 1px solid #eff2f7;
    text-align: center;
}

.THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_content{
    padding: .8em;
    border-bottom: 1px solid #eff2f7;
    text-align: center;
}

.THIS .section-compare .section-compare_content .section-compare_content_row .website{
    text-decoration: none;
    font-weight: bold;
    color: #00b4ff;
}

.THIS .header_margin-left{
    margin-left: .7em;
}

.THIS .content_margin-left{
    margin-left: 3.5em;
}

/*--------------------
-----Button------
----------------------*/

.THIS .slds-button-expandable{
    background:none;
    justify-content:center;
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

@media (max-width: 480px){

    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    }
}

@media (min-width: 480px){

    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    }

    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn-blue{
        margin: 0 1.5em;
    }
}

@media (min-width: 768px){

    /*--------------------
    -----Carousel------
    ----------------------*/

    .THIS .next_bid{
        transform: translateX(-50%);
    }

    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_header .section-compare_header_space{
        width: 22%;
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    }

    .THIS .header_margin-left{
        margin-left: 0;
    }

    .THIS .content_margin-left{
        margin-left: 0;
    }
}

@media (min-width: 1024px){
    
    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_header > .section-compare_header_space{
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row{
        border: 1px solid #eff2f7;
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
        border-bottom: none;
        text-align: left;
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_content{
        padding: .8em;
        border-bottom: none;
        text-align: center;
    }

    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS .slds-button-expandable{
        justify-content:space-between;
    }
    
}
```
### VoyajerOptionsFreightCompareHelper

```
({
	setControls : function(component, goTo){
		var mobileScreen = window.matchMedia('screen and (max-width:768px)'); 
		var tabletScreen = window.matchMedia('screen and (min-width:768px)'); 
		console.log("mobileScreen.matches: " + mobileScreen.matches);
		console.log("tabletScreen.matches: " + tabletScreen.matches);
		if(goTo == "prevBids"){
			if(mobileScreen.matches){
				if(component.get("v.bidsSelected").length == 2){
					if($A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.addClass(component.find("bids"), "prev_bid");
					}
				}
				else if(component.get("v.bidsSelected").length > 2){
					if($A.util.hasClass(component.find("bids"), "next_bid2")){
						$A.util.removeClass(component.find("bids"), "next_bid2");
						$A.util.addClass(component.find("bids"), "prev_bid2");
					}
					else if($A.util.hasClass(component.find("bids"), "next_bid") || $A.util.hasClass(component.find("bids"), "prev_bid2")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.removeClass(component.find("bids"), "prev_bid2");
						$A.util.addClass(component.find("bids"), "prev_bid");
					}
				}
			}
			else if(tabletScreen.matches){
				if(component.get("v.bidsSelected").length > 2){
					if($A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.addClass(component.find("bids"), "prev_bid");
					}
				}
			}
		}
		else if(goTo == "nextBids"){
			if(mobileScreen.matches){
				if(component.get("v.bidsSelected").length == 2){
					if(!$A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "prev_bid");
						$A.util.addClass(component.find("bids"), "next_bid");
					}
				}
				if(component.get("v.bidsSelected").length > 2){
					if(!$A.util.hasClass(component.find("bids"), "next_bid") && !$A.util.hasClass(component.find("bids"), "next_bid2")){
						$A.util.removeClass(component.find("bids"), "prev_bid");
						$A.util.addClass(component.find("bids"), "next_bid");
					}
					else if($A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.addClass(component.find("bids"), "next_bid2");
					}
				}
			}
			else if(tabletScreen.matches){
				if(component.get("v.bidsSelected").length > 2){
					if(!$A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "prev_bid");
						$A.util.addClass(component.find("bids"), "next_bid");
					}
				}
			}
		}
	},
})
```
### VoyajerOptionsFreightCompareController

```
({
	onInit : function(component, event, helper){
		//helper.getData(component, "searchBidOptions");
	},
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	},
	handleViewAllOptions : function(component, event, helper){
		component.set("v.content", "all");
	},
	handlePrevBids : function(component, event, helper){
		helper.setControls(component, "prevBids");
	},
	handleNextBids : function(component, event, helper){
		helper.setControls(component, "nextBids");
	},
	handleNavigation : function(component, event, helper){
		event.preventDefault();
		console.log("$(event.currentTarget).text(): " + $(event.currentTarget).text());
		component.find("navigationService").navigate({
			type: "standard__webPage",
			attributes: {
				url: $(event.currentTarget).text()
			}
		});		
	},
	handleExpand : function(component, event, helper){
		$(event.currentTarget).parents('.slds-section').toggleClass("slds-is-open");
	}
})
```
### VoyajerOptionsFreightCompare

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsFreightCompare

```
<aura:component controller="VoyajerOptionsFreightController" implements="force:appHostable,flexipage:availableForAllPageTypes">
    <aura:attribute name="content" type="String"/>
    <aura:attribute name="itinerary" type="Object"/>
    <aura:attribute name="bidsSelected" type="List"/>
    <ltng:require scripts="{!$Resource.UltimateUtils + '/js/jquery-3.3.1.min.js'}"/>
    
    <aura:handler name="init" value="{!this}" action="{!c.onInit}" />
    <aura:handler name="render" value="{!this}" action="{!c.onRender}" />
    <div>
        <lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
        <div class="pageContent" style="min-height:680px;">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">Options</h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="btn btn-bluelight" onclick="{!c.handleViewAllOptions}"/>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><i class="fas fa-shield-alt" style="color: #9f9f9f; margin-left: 0.5em;"></i><strong style="color:black;">{!!empty(v.itinerary.Production__r) ? v.itinerary.Production__r.Name : ''}</strong></h3>
                                <p style="margin-left: 0.5em;font-weight:bold;color:#00b4ff;">{!(!empty(v.itinerary.Start_city__r) ? ((!empty(v.itinerary.Start_city__r.City__c) ? v.itinerary.Start_city__r.City__c : '') + (!empty(v.itinerary.Start_city__r.State__c) ? ', ' + v.itinerary.Start_city__r.State__c : '')) : '') + ' to ' + (!empty(v.itinerary.End_city__r) ? ((!empty(v.itinerary.End_city__r.City__c) ? v.itinerary.End_city__r.City__c : '') + (!empty(v.itinerary.End_city__r.State__c) ? ', ' + v.itinerary.End_city__r.State__c : '')) : '') + ' | ' + (!empty(v.itinerary.Start_Date__c) ? v.itinerary.Start_Date__c : '') + (!empty(v.itinerary.End_Date__c) ? ' - ' + v.itinerary.End_Date__c : '')}</p>
                                <p style="margin-left: 0.5em;">Freight Type: {!!empty(v.itinerary.Service_Type__c) ? ' - ' + v.itinerary.Service_Type__c : ''}</p>
                                <p style="margin-left: 0.5em;">Contents: {!!empty(v.itinerary.Freight_Trip_Contents__c) ? ' - ' + v.itinerary.Freight_Trip_Contents__c : ''}</p>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    12/17/18
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <section class="slds-grid slds-gutters slds-wrap">
                        <div class="slds-col slds-size_1-of-1">
                            <div class="slds-carousel carousel">
                                <div class="slds-carousel__col-center slds-is-absolute slds-hide_large carousel-control_left" style="{!v.bidsSelected.length > 1 ? '' : 'display:none;'}">
                                    <button type="button" class="slds-button slds-button_icon-border-filled slds-button_icon-small slds-button_icon slds-carousel__button" onclick="{!c.handlePrevBids}">
                                        <lightning:icon iconName="utility:chevronleft" size="x-small"/>
                                        <span class="slds-assistive-text">Previous</span>
                                    </button>
                                </div>                          
                                <div class="slds-carousel__stage section-compare">
                                    <div class="slds-carousel__panels slds-is-relative slds-grid slds-wrap" aura:id="bids">
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-grid slds-gutters_x-small section-compare_header">
                                                <div class="slds-col slds-size_1-of-1 slds-show_large section-compare_header_space">
                                                    <lightning:navigation aura:id="navigationService"/> 
                                                </div>
                                                <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                    <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_2-of-4' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-4 section-compare_header_item' + (i > 0 ? ' header_margin-left' : '')}">
                                                        <h3 class="slds-align_absolute-center"><strong>{!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Name : ''}</strong></h3>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-section slds-is-open section-compare_content">
                                                <h4 class="slds-section__title section-compare_content_header">
                                                    <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-show_large slds-button-expandable" onclick="{!c.handleExpand}">
                                                        <span class="slds-truncate" title="Information Details">Information Details</span>
                                                        <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                                    </button>
                                                </h4>
                                                <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-1 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-hide_large section-compare_content_row_header' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <strong style="color:#00b4ff;">Information Details</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Website</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <a onclick="{!c.handleNavigation}" class="website">{!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Website : ''}</a>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Address</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    {!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.ShippingStreet : ''}
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>City. State / Postal Code</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    {!(!empty(bid.record.Vendor__r) ? (!empty(bid.record.Vendor__r.ShippingCity) ? bid.record.Vendor__r.ShippingCity + ', ' : '') + (!empty(bid.record.Vendor__r.ShippingState) ? bid.record.Vendor__r.ShippingState + ' ' : '') + (!empty(bid.record.Vendor__r.ShippingPostalCode) ? bid.record.Vendor__r.ShippingPostalCode : '') : '')}
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Phone</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    {!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Phone : ''}
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-section slds-is-open section-compare_content">
                                                <h4 class="slds-section__title section-compare_content_header">
                                                    <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-show_large slds-button-expandable" onclick="{!c.handleExpand}">
                                                        <span class="slds-truncate" title="Rate Details">Rate Details</span>
                                                        <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                                    </button>
                                                </h4>
                                                <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-1 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-hide_large section-compare_content_row_header' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <strong style="color:#00b4ff;">Rate Details</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Pick Up - Drop Off Details</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <aura:iteration items="{!bid.relatedRecords}" var="subtrip">
                                                                        <aura:if isTrue="{!!empty(subtrip.FreightEquipments__r)}">
                                                                            <aura:iteration items="{!subtrip.FreightEquipments__r.records}" var="travel" indexVar="i">
                                                                                <p style="{!subtrip.FreightEquipments__r.totalSize - 1 != i ? 'margin-bottom:1.8em;' : ''}">
                                                                                    <strong style="text-transform:uppercase;">
                                                                                        <c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="EEE, dd MMM yyyy"/> | {!!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : ''}<br/>
                                                                                    </strong>
                                                                                    from {!!empty(travel.Location_Details__c) ? travel.Location_Details__c : ''} <br/>
                                                                                    {!!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c : ''} <br/>
                                                                                    <strong style="text-transform:uppercase;">
                                                                                        <c:auraFormattedDate date="{!travel.End_Date__c}" dateFormat="EEE, dd MMM yyyy"/> | {!!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : ''}<br/>
                                                                                    </strong>
                                                                                    from {!!empty(travel.Location_Details_Drop_Off__c) ? travel.Location_Details_Drop_Off__c : ''} <br/>
                                                                                    {!!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c : ''}
                                                                                </p>
                                                                            </aura:iteration>
                                                                        </aura:if>
                                                                    </aura:iteration>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Freight Truck sq ft</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>fuel</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>loading / unloading</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Cargo List</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Cargo List</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Payment Terms</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i">
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-1 section-compare_content_row_header' + (i > 0 ? ' slds-hide_large content_margin-left' : '')}">
                                                                    <strong>Total Price</strong>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_1-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_header' + (i > 0 ? ' content_margin-left' : '')}">
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                        <div class="slds-col slds-size_1-of-1 slds-large-size_4-of-5 slds-grid">
                                                            <aura:iteration items="{!v.bidsSelected}" var="bid" indexVar="i"> 
                                                                <div class="{!'slds-col slds-size_1-of-1 slds-small-size_1-of-1' + (v.bidsSelected.length > 1 ? ' slds-medium-size_1-of-2' : ' slds-medium-size_1-of-1') + ' slds-large-size_1-of-3 section-compare_content_row_content' + (i > 0 ? ' content_margin-left' : '')}">
                                                                    <lightning:button label="SELECT" variant="brand" iconName="utility:check" iconPosition="right" class="btn btn-blue" onclick="{!c.handleViewAllOptions}"/>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-carousel__col-center slds-is-absolute slds-hide_large carousel-control_right" style="{!v.bidsSelected.length > 1 ? '' : 'display:none;'}">
                                    <button type="button" class="slds-button slds-button_icon-border-filled slds-button_icon-small slds-button_icon slds-carousel__button" onclick="{!c.handleNextBids}">
                                        <lightning:icon iconName="utility:chevronright" size="x-small"/>
                                        <span class="slds-assistive-text">Next</span>
                                    </button>
                                </div>                        
                            </div>                         
                        </div>
                    </section>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerOptionsFreightCompare

```
/*
	Version:	    V1.0
	Create Date:	2/17/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}

/*--------------------
-----Carousel------
----------------------*/

.THIS .carousel{
}

.THIS .carousel .carousel-control_left{
    top: 2em;
    left: 2%;
    z-index: 1;
}

.THIS .carousel .carousel-control_right{
    top: 2em;
    right: 2%;
    z-index: 1;
}

.THIS .prev_bid{
    transform: translateX(0%);
}

.THIS .prev_bid2{
    transform: translateX(-100%);
}

.THIS .next_bid{
    transform: translateX(-100%);
}

.THIS .next_bid2{
    transform: translateX(-200%);
}

/*--------------------
-----Compare------
----------------------*/

.THIS .section-compare{
}

.THIS .section-compare .section-compare_header{
}

.THIS .section-compare .section-compare_header .section-compare_header_space{
    
}

.THIS .section-compare .section-compare_header .section-compare_header_item > h3{
    min-height: 5em;
    padding: 0 .5em;
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
    border: none;
}

.THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    padding: .8em;
    border-bottom: 1px solid #eff2f7;
    text-align: center;
}

.THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_content{
    padding: .8em;
    border-bottom: 1px solid #eff2f7;
    text-align: center;
}

.THIS .section-compare .section-compare_content .section-compare_content_row .website{
    text-decoration: none;
    font-weight: bold;
    color: #00b4ff;
}

.THIS .header_margin-left{
    margin-left: .7em;
}

.THIS .content_margin-left{
    margin-left: 3.5em;
}

/*--------------------
-----Button------
----------------------*/

.THIS .slds-button-expandable{
    background:none;
    justify-content:center;
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

@media (max-width: 480px){

    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    }
}

@media (min-width: 480px){

    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    }

    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn-blue{
        margin: 0 1.5em;
    }
}

@media (min-width: 768px){

    /*--------------------
    -----Carousel------
    ----------------------*/

    .THIS .next_bid{
        transform: translateX(-50%);
    }

    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_header .section-compare_header_space{
        width: 22%;
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
    }

    .THIS .header_margin-left{
        margin-left: 0;
    }

    .THIS .content_margin-left{
        margin-left: 0;
    }
}

@media (min-width: 1024px){
    
    /*--------------------
    -----Compare------
    ----------------------*/
    
    .THIS .section-compare .section-compare_header > .section-compare_header_space{
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row{
        border: 1px solid #eff2f7;
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_header{
        border-bottom: none;
        text-align: left;
    }
    
    .THIS .section-compare .section-compare_content .section-compare_content_row .section-compare_content_row_content{
        padding: .8em;
        border-bottom: none;
        text-align: center;
    }

    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS .slds-button-expandable{
        justify-content:space-between;
    }
    
}
```
### VoyajerOptionsFreightCompareHelper

```
({
	setControls : function(component, goTo){
		var mobileScreen = window.matchMedia('screen and (max-width:768px)'); 
		var tabletScreen = window.matchMedia('screen and (min-width:768px)'); 
		console.log("mobileScreen.matches: " + mobileScreen.matches);
		console.log("tabletScreen.matches: " + tabletScreen.matches);
		if(goTo == "prevBids"){
			if(mobileScreen.matches){
				if(component.get("v.bidsSelected").length == 2){
					if($A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.addClass(component.find("bids"), "prev_bid");
					}
				}
				else if(component.get("v.bidsSelected").length > 2){
					if($A.util.hasClass(component.find("bids"), "next_bid2")){
						$A.util.removeClass(component.find("bids"), "next_bid2");
						$A.util.addClass(component.find("bids"), "prev_bid2");
					}
					else if($A.util.hasClass(component.find("bids"), "next_bid") || $A.util.hasClass(component.find("bids"), "prev_bid2")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.removeClass(component.find("bids"), "prev_bid2");
						$A.util.addClass(component.find("bids"), "prev_bid");
					}
				}
			}
			else if(tabletScreen.matches){
				if(component.get("v.bidsSelected").length > 2){
					if($A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.addClass(component.find("bids"), "prev_bid");
					}
				}
			}
		}
		else if(goTo == "nextBids"){
			if(mobileScreen.matches){
				if(component.get("v.bidsSelected").length == 2){
					if(!$A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "prev_bid");
						$A.util.addClass(component.find("bids"), "next_bid");
					}
				}
				if(component.get("v.bidsSelected").length > 2){
					if(!$A.util.hasClass(component.find("bids"), "next_bid") && !$A.util.hasClass(component.find("bids"), "next_bid2")){
						$A.util.removeClass(component.find("bids"), "prev_bid");
						$A.util.addClass(component.find("bids"), "next_bid");
					}
					else if($A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "next_bid");
						$A.util.addClass(component.find("bids"), "next_bid2");
					}
				}
			}
			else if(tabletScreen.matches){
				if(component.get("v.bidsSelected").length > 2){
					if(!$A.util.hasClass(component.find("bids"), "next_bid")){
						$A.util.removeClass(component.find("bids"), "prev_bid");
						$A.util.addClass(component.find("bids"), "next_bid");
					}
				}
			}
		}
	},
})
```

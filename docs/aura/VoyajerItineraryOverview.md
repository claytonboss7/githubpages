---
layout: default
title: VoyajerItineraryOverview
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerItineraryOverview
## Fields
### VoyajerItineraryOverviewController

```
({
  onRender: function (component, event, helper) {
    //Fix By Clay Dev 27 Feb, 2021 #177024410
    //helper.getData(component, "searchItineraries", null);
    
      if(component.get('v.startDate') != undefined || component.get('v.endDate') != undefined || 
        (component.get('v.selectedLookupId') != undefined && component.get('v.selectedPillText') != undefined)) {
    	component.find('startDateInput').set("v.value", component.get('v.startDate'));
    	component.find('endDateInput').set("v.value", component.get('v.endDate'));
          if(component.get('v.selectedLookupId') != undefined && component.get('v.selectedPillText') != undefined) {
            component.find('lookupCity').set('v.lookupId', component.get('v.selectedLookupId'));
            component.find('lookupCity').set('v.pillText', component.get('v.selectedPillText'));
            component.find('lookupCity').set("v.isEdited",true);
          
            var forclose = component.find('lookupCity').find("lookup-pill");
            $A.util.addClass(forclose, 'slds-show');
            $A.util.removeClass(forclose, 'slds-hide');
          
            var forclose = component.find('lookupCity').find("searchRes");
            $A.util.addClass(forclose, 'slds-is-close');
            $A.util.removeClass(forclose, 'slds-is-open');
            $A.util.removeClass(forclose, 'slds-has-error');
            
            var message = component.find('lookupCity').find("requiredMessage");
            $A.util.addClass(message, 'slds-hide');
            $A.util.removeClass(message, 'slds-show');
          
            var lookUpTarget = component.find('lookupCity').find("lookupField");
            $A.util.addClass(lookUpTarget, 'slds-hide');
            $A.util.removeClass(lookUpTarget, 'slds-show'); 
        }
      
    	component.set('v.startDate', null);
        component.set('v.endDate', null);
        component.set('v.selectedLookupId', null);
        component.set('v.selectedPillText', null);
        helper.getData(component, "searchItineraries", null);
      } else {
          $A.util.addClass(component.find("loading"), "slds-hide");
      }
  },

  handleBack: function (component, event, helper) {
    component.set("v.productionSelected", "");
    component.set("v.mainContent", "dashboard");
  },

  handleUpdate: function (component, event, helper) {
    var thelookup = component.find('lookupCity').get('v.lookupId');
    helper.getData(component, "searchItineraries",thelookup);
    console.log ('theLookup :: ' + thelookup);
  },

  handleClear: function (component, event, helper) {
    helper.clearData(component, event);
  },

  handleExpand: function (component, event, helper) {
    $(event.currentTarget).parents(".slds-section").toggleClass("slds-is-open");
  },

  handleDocuments: function (component, event, helper) {
    console.log("handleDocuments");
    var serviceId = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("serviceid");
    var serviceType = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("servicetype");
    component.set("v.serviceId", serviceId);
    component.set("v.serviceType", serviceType);
    component.set(
      "v.serviceDateInAndOut",
      $(event.currentTarget)
        .parents(".itinerary_buttons")
        .data("servicedateinandout")
    );
    component.set(
      "v.serviceCityName",
      $(event.currentTarget)
        .parents(".itinerary_buttons")
        .data("servicecityname")
    );
    helper.setSearchParameters(component, event);
    component.set("v.mainContent", "documents");
  },

  handleOptions: function (component, event, helper) {
    console.log("handleOptions");
    component.set("v.displaySelect", false);
    
    var serviceId = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("serviceid");
    var serviceType = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("servicetype");
    if (!!serviceId && !!serviceType) {
      component.set("v.optionRecordId", serviceId);
      helper.setSearchParameters(component, event);
      if (serviceType == "Housing__c")
        component.set("v.mainContent", "optionsHousing");
      if (serviceType == "Ground__c")
        component.set("v.mainContent", "optionsGT");
      if (serviceType == "Freight__c")
        component.set("v.mainContent", "optionsFreight");
      if (serviceType == "Air__c") component.set("v.mainContent", "optionsAir");
    }
  },

  openReviewSubmit: function (component, event, helper) {
    /*//HERE 080520 - enviar bidId, cambiar en review component de cada servicio, para que use el bidId, y no el index (victor)
        var serviceType = $(event.currentTarget).parents('.itinerary_buttons').data('servicetype');
        var bidId = $(event.currentTarget).parents('.itinerary_buttons').data('serviceid');
        
        if(!!bidId && !!serviceType) {
            console.log('# serviceId = ' + serviceId);
            console.log('# serviceType = ' + serviceType);
            component.set("v.bidRecordId", bidId);
            
            if(serviceType == 'Housing__c') component.set("v.mainContent","optionsHousingReviewSubmit");
            //if(serviceType == 'Ground__c') component.set("v.mainContent","optionsGT");
            //if(serviceType == 'Freight__c') component.set("v.mainContent","optionsFreight");
            //if(serviceType == 'Air__c') component.set("v.mainContent","optionsAir");
        }*/
  },
    handleCommunicationEventGetCity : function(component, event, helper) {
        console.log("Inside parent");
		var obj = event.getParam("data");
		console.log(JSON.stringify(obj));
        component.set("v.serviceCity", obj);
    }
});
```
### VoyajerItineraryOverviewHelper

```
({
	getData : function(component, method,city){
		var action = component.get("c." + method);
        var lookupValue = component.find('lookupCity').get('v.lookupId');
		if(method == "searchItineraries") action.setParams({opportunityId: component.get("v.productionSelected"), startDate: component.find('startDateInput').get("v.value"), endDate: component.find('endDateInput').get("v.value"), cityId: lookupValue});
		action.setCallback(this, function(response){
			var state = response.getState();
			if(state === "SUCCESS"){
				var result = JSON.parse(response.getReturnValue());
                var resultMap = [];
                for(var key in result) resultMap.unshift({key: $A.localizationService.formatDate(key, "EEE, dd MMM yyyy"), value: result[key]});
				console.log(resultMap);
				if(method == "searchItineraries") component.set("v.data", resultMap);
                $A.util.addClass(component.find("loading"), "slds-hide");
			}
			else if(state === "INCOMPLETE"){
			}
			else if(state === "ERROR"){
				var errors = response.getError();
				if(errors){
					if(errors[0] && errors[0].message) console.log("Error message: " + errors[0].message);
				}
				else{
					console.log("Unknown error");
				}
			}
		});
		//$A.util.removeClass(component.find("loading"), "slds-hide");
		$A.enqueueAction(action);
	},
    
	clearData : function(component, event){
		component.find('startDateInput').set("v.value", null);
		component.find('endDateInput').set("v.value", null);
		component.set("v.data", null);
        
        var pillTarget = component.find('lookupCity').find("lookup-pill");
        var lookUpTarget = component.find('lookupCity').find("lookupField"); 
        
        $A.util.addClass(pillTarget, 'slds-hide');
        $A.util.removeClass(pillTarget, 'slds-show');
        
        $A.util.addClass(lookUpTarget, 'slds-show');
        $A.util.removeClass(lookUpTarget, 'slds-hide');
        
        component.find('lookupCity').set("v.searchKeyWord","");
        component.find('lookupCity').set("v.listOfSearchRecords", null);
        component.find('lookupCity').set("v.selectedRecord",{});
        if(!!component.find('lookupCity').get("v.lookupId")) component.find('lookupCity').set("v.isEdited",true);
        component.find('lookupCity').set("v.lookupId","");
        
	},
    
    setSearchParameters : function(component, event){
		component.set("v.startDate", component.find('startDateInput').get("v.value"));
      	component.set("v.endDate", component.find('endDateInput').get("v.value"));
      	component.set("v.selectedLookupId", component.find('lookupCity').get('v.lookupId'));
      	component.set("v.selectedPillText", component.find('lookupCity').get('v.pillText'));
	}
})
```
### VoyajerItineraryOverview

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerItineraryOverview

```
/*
	Version:	    V1.0
	Create Date:	2/09/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}

/*--------------------
-----Overview------
----------------------*/

.THIS .slds-card-overview_header{
    background-color: #f6f7fc;
    color: #022066;
    font-weight: bold;
}

.THIS .slds-card-overview_header>h3{
    padding: 1rem;
}

.THIS .slds-card-overview_item{
    margin-top: .8rem;
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    background-color: #022066;
    transition: transform 0.1s ease;
}

.THIS .slds-card-overview_item:hover{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    -webkit-transform: scale(1.01);
    -moz-transform: scale(1.01);
    -o-transform: scale(1.01);
    transform: scale(1.01);
}

.THIS .slds-card-overview_item-leftside{
    display:flex;
    height: 100%;
    justify-content: center;
}

.THIS .slds-card-overview_item-content{
    background-color: white;
    padding-bottom: 10px;
    border-bottom: 1px solid #eaeaea;
}

.THIS .slds-card-overview_item header{
    margin-top: .5rem;
}

.THIS .slds-card-overview_item header h3{
    font-weight: bold;
    color: #022066;
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

/*--------------------
-----Input Dates------
----------------------*/

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

/*--------------------
-----Medias queries------
----------------------*/

@media (max-width: 768px){
    .THIS .slds-section__content{
        overflow-x: auto !important;
    }
}
```
### VoyajerItineraryOverview

```
<aura:component controller="VoyajerItineraryOverviewController">
	<aura:attribute name="mainContent" type="String" />
	<aura:attribute type="String" name="optionRecordId" />
	<aura:attribute name="productionSelected" type="String" default="0065600000765ufAAA" />
	<aura:attribute name="productionName" type="String" />
	<aura:attribute name="displaySelect" type="Boolean" default="true" />
	<aura:attribute name="productionCompany" type="String" />
	<aura:attribute name="serviceId" type="String" />
	<aura:attribute name="serviceType" type="String" />
	<aura:attribute name="serviceDateInAndOut" type="String" />
	<aura:attribute name="serviceCityName" type="String" />
	<aura:attribute name="serviceCity" type="Object" default="{}" />

	<aura:attribute name="startDate" type="String" />
	<aura:attribute name="endDate" type="String" />
	<aura:attribute name="selectedLookupId" type="String" />
	<aura:attribute name="selectedPillText" type="String" />
	<aura:attribute name="data" type="List" access="private" />
	<ltng:require scripts="{!$Resource.RoadRebelUtils + '/js/jquery-3.3.1.min.js'}" />

	<aura:handler name="callToParentGetCity" action="{!c.handleCommunicationEventGetCity}" event="c:VoyajerCustomLookupGetSelectedCity" />

	<aura:handler name="render" value="{!this}" action="{!c.onRender}" />
	<div>
		<lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
		<div class="pageContent" style="min-height: 680px">
			<div class="pageContentSpaces">
				<div class="page-section">
					<div class="page-header">
						<h1 class="page-header-title">Itinerary Overview</h1>
						<lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
					</div>
				</div>
				<div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb">
					<div class="page-section">
						<h3>
							<i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em"></i
							><strong style="color: black">{!v.productionName}</strong>
						</h3>
						<h4 style="color: black">{!v.productionCompany}</h4>
					</div>
					<div class="page-section-buttons">
						<div style="align-items: center; justify-content: flex-start; flex: 1">
							<p style="margin-right: 0.5em">Filter by</p>
							<lightning:layout horizontalAlign="center" verticalAlign="center">
								<lightning:layoutItem padding="around-medium">
									<br/>
									<div class="startDateContainer">
										<lightning:input
											aura:id="startDateInput"
											type="date"
											label=""
											variant="label-hidden"
											dateStyle="short"
											placeholder="mm/dd/yyyy"
											class="startDateInput"
											onchange=""
											autocomplete="off"
										/>
										<div style="padding: 0 0.5em">-</div>
										<lightning:input
											aura:id="endDateInput"
											type="date"
											label=""
											variant="label-hidden"
											dateStyle="short"
											placeholder="mm/dd/yyyy"
											class="startDateInput"
											onchange=""
											autocomplete="off"
										/>
										<div style="padding-right: 0.5em">
											<lightning:icon iconName="utility:date_input" size="x-small" />
										</div>
									</div>
								</lightning:layoutItem>
								<lightning:layoutItem>
									<div class="formField" style="width: 300px">
										<c:VoyajerCustomLookup
											aura:id="lookupCity"
											objectAPIName="City__c"
											fieldName="City__c"
											iconName="custom:custom24"
											lookupId=""
											label=""
											inputPlaceholder="Enter Location"
											isRequired="false"
											isEdited="false"
											loadCityLookup="{!v.loadCityLookup}"
											triggerLookupValidation="{!v.triggerLookupValidation}"
										/>
									</div>
								</lightning:layoutItem>
								<lightning:layoutItem padding="around-large">
									<br/>
									<lightning:button label="Update" variant="brand" class="formButtonBrandLight" onclick="{!c.handleUpdate}" />
									<lightning:button label="Clear" variant="neutral" onclick="{!c.handleClear}" />
								</lightning:layoutItem>
							</lightning:layout>
						</div>
					</div>
				</div>
				<div class="pageContentDashboard" style="padding-top: 0; border-bottom: 1px solid #dbdbdb">
					<section class="page-section slds-card-overview">
						<aura:iteration items="{!v.data}" var="dataMap" indexVar="key">
							<header class="slds-grid slds-gutters slds-wrap slds-card-overview_header">
								<h3>{!dataMap.key}<br /></h3>
							</header>
							<aura:iteration items="{!dataMap.value}" var="itinerary">
								<article class="slds-grid slds-gutters slds-wrap slds-card-overview_item">
									<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside">
										<div class="slds-media slds-media_responsive">
											<div class="slds-media__figure" style="margin-top: 10px; margin-right: 0">
												<span class="slds-avatar slds-avatar_large">
													<img
														src="{!$Resource.CommunityImages + (itinerary.record.attributes.type == 'Housing__c' ? '/SelectServiceIcons/service_housing_icons.png' : itinerary.record.attributes.type == 'Ground__c' ? '/SelectServiceIcons/service_busing_icons.png' : itinerary.record.attributes.type == 'Freight__c' ? '/SelectServiceIcons/service_freight_icons.png' : itinerary.record.attributes.type == 'Air__c' ? '/SelectServiceIcons/service_plane_icons.png' : '')}"
														title="housing"
													/>
												</span>
											</div>
										</div>
									</div>
									<div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-overview_item-content">
										<header class="slds-grid slds-gutters slds-wrap">
											<div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12">
												<h3>
													{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Name : (itinerary.record.Status_CC__c == 'Layoff' ? itinerary.record.Status_CC__c : 'Vendor TBD')) : itinerary.record.attributes.type == 'Ground__c' ?
													(!empty(itinerary.record.Vendor_lookup__r) ? itinerary.record.Vendor_lookup__r.Name : 'Vendor TBD') :
													itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Name : 'Vendor TBD') : itinerary.record.attributes.type == 'Air__c' ?
													(!empty(itinerary.record.Vendor__r) ? itinerary.record.Vendor__r.Name : 'Vendor TBD') : ''}
												</h3>
												<p style="color: #333; font-weight: bold">
													{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													(!empty(itinerary.record.Vendor_lookup__r.ShippingStreet) ? itinerary.record.Vendor_lookup__r.ShippingStreet + ' '
													: '') + (!empty(itinerary.record.Vendor_lookup__r.ShippingCity) ? itinerary.record.Vendor_lookup__r.ShippingCity +
													', ' : '') + (!empty(itinerary.record.Vendor_lookup__r.ShippingState) ?
													itinerary.record.Vendor_lookup__r.ShippingState + ', ' : '') +
													(!empty(itinerary.record.Vendor_lookup__r.ShippingCountryCode) ?
													itinerary.record.Vendor_lookup__r.ShippingCountryCode : '') : '') : itinerary.record.attributes.type ==
													'Ground__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													(!empty(itinerary.record.Vendor_lookup__r.BillingStreet) ? itinerary.record.Vendor_lookup__r.BillingStreet + ' ' :
													'') + (!empty(itinerary.record.Vendor_lookup__r.BillingCity) ? itinerary.record.Vendor_lookup__r.BillingCity + ',
													' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingState) ? itinerary.record.Vendor_lookup__r.BillingState
													+ ', ' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingCountryCode) ?
													itinerary.record.Vendor_lookup__r.BillingCountryCode : '') : '') : itinerary.record.attributes.type ==
													'Freight__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													(!empty(itinerary.record.Vendor_lookup__r.BillingStreet) ? itinerary.record.Vendor_lookup__r.BillingStreet + ' ' :
													'') + (!empty(itinerary.record.Vendor_lookup__r.BillingCity) ? itinerary.record.Vendor_lookup__r.BillingCity + ',
													' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingState) ? itinerary.record.Vendor_lookup__r.BillingState
													+ ', ' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingCountryCode) ?
													itinerary.record.Vendor_lookup__r.BillingCountryCode : '') : '') : itinerary.record.attributes.type == 'Air__c' ?
													(!empty(itinerary.record.Vendor__r) ? (!empty(itinerary.record.Vendor__r.BillingStreet) ?
													itinerary.record.Vendor__r.BillingStreet + ' ' : '') + (!empty(itinerary.record.Vendor__r.BillingCity) ?
													itinerary.record.Vendor__r.BillingCity + ', ' : '') + (!empty(itinerary.record.Vendor__r.BillingState) ?
													itinerary.record.Vendor__r.BillingState + ', ' : '') + (!empty(itinerary.record.Vendor__r.BillingCountryCode) ?
													itinerary.record.Vendor__r.BillingCountryCode : '') : '') : ''} <br />
													{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Phone : '') : itinerary.record.attributes.type == 'Ground__c' ?
													(!empty(itinerary.record.Vendor_lookup__r) ? itinerary.record.Vendor_lookup__r.Phone : '') :
													itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Phone : '') : itinerary.record.attributes.type == 'Air__c' ?
													(!empty(itinerary.record.Vendor__r) ? itinerary.record.Vendor__r.Phone : '') : ''}
												</p>
											</div>
											<div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12" style="font-weight: bold; color: #00b4ff">
												<span
													>{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.City__r) ?
													((!empty(itinerary.record.City__r.City__c) ? itinerary.record.City__r.City__c : '') +
													(!empty(itinerary.record.City__r.State__c) ? ', ' + itinerary.record.City__r.State__c : '')) : '') :
													itinerary.record.attributes.type == 'Ground__c' ? (!empty(itinerary.record.Start_city__r) ?
													((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') +
													(!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') :
													itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Start_city__r) ?
													((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') +
													(!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') :
													itinerary.record.attributes.type == 'Air__c' ? (!empty(itinerary.record.Departure_City__r) &amp;&amp;
													!empty(itinerary.record.Departure_City__r.City__r) ? ((!empty(itinerary.record.Departure_City__r.City__r.City__c)
													? itinerary.record.Departure_City__r.City__r.City__c : '') +
													(!empty(itinerary.record.Departure_City__r.City__r.State__c) ? ', ' +
													itinerary.record.Departure_City__r.City__r.State__c : '')) : '') : ''}</span
												>
												|
												<span
													>{!itinerary.record.attributes.type == 'Housing__c' ? itinerary.record.Date_In_Text__c +
													(!empty(itinerary.record.Date_Out_Text__c) ? ' - ' + itinerary.record.Date_Out_Text__c : '') :
													itinerary.record.attributes.type == 'Ground__c' ? itinerary.record.Start_Date_Text__c +
													(!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') :
													itinerary.record.attributes.type == 'Freight__c' ? itinerary.record.Start_Date_Text__c +
													(!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') :
													itinerary.record.attributes.type == 'Air__c' ? itinerary.record.Departure_Date_Text__c +
													(!empty(itinerary.record.Return_Date_Text__c) ? ' - ' + itinerary.record.Return_Date_Text__c : '') : ''}</span
												>
												<p>
													{!itinerary.record.attributes.type == 'Housing__c' ? (not(empty(itinerary.record.Venue__c))?
													itinerary.record.Venue__r.Name : '') : ''}
												</p>
											</div>
										</header>
										<div class="slds-grid slds-gutters slds-wrap">
											<div class="slds-col slds-size_1-of-1">
												<div class="slds-section slds-is-open">
													<h4 class="slds-section__title" style="border-top: 1px solid #eaeaea">
														<button
															aria-controls="expando-unique-id"
															aria-expanded="true"
															class="slds-button slds-section__title-action slds-button-expandable"
															onclick="{!c.handleExpand}"
														>
															<span
																class="slds-truncate"
																style="font-size: 0.875rem; font-weight: 600"
																title="{!itinerary.record.attributes.type == 'Housing__c' ? 'STAY DETAILS' : itinerary.record.attributes.type == 'Ground__c' ? 'TRIP DETAILS' : itinerary.record.attributes.type == 'Freight__c' ? 'TRIP DETAILS' : itinerary.record.attributes.type == 'Air__c' ? 'FLIGHT DETAILS' : ''}"
																>{!itinerary.record.attributes.type == 'Housing__c' ? 'STAY' : itinerary.record.attributes.type ==
																'Ground__c' ? 'TRIP' : itinerary.record.attributes.type == 'Freight__c' ? 'TRIP' :
																itinerary.record.attributes.type == 'Air__c' ? 'FLIGHT' : ''} DETAILS</span
															>
															<lightning:buttonIcon
																iconName="utility:down"
																variant="bare"
																alternativeText="Open"
																iconClass="buttonIcon-bluelight"
															/>
														</button>
													</h4>
													<div aria-hidden="false" class="slds-section__content" id="expando-unique-id" style="padding-top: 0; color: #333">
														<table
															class="{!itinerary.record.attributes.type == 'Housing__c' ? 'slds-table slds-table_cell-buffer' : itinerary.record.attributes.type == 'Ground__c' ? '' : itinerary.record.attributes.type == 'Freight__c' ? '' : itinerary.record.attributes.type == 'Air__c' ? '' : ''}"
														>
															<aura:if isTrue="{!itinerary.record.attributes.type == 'Housing__c'}">
																<thead>
																	<tr class="slds-line-height_reset">
																		<th class="" scope="col">
																			<div class="slds-truncate" title="CHECK-IN">CHECK-IN</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="CHECK-OUT">CHECK-OUT</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="ROOMS">ROOMS</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="ROOM DESCRIPTION">ROOM DESCRIPTION</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="RATE">RATE</div>
																		</th>
																	</tr>
																</thead>
																<aura:set attribute="else">
																	<aura:if isTrue="{!itinerary.record.attributes.type == 'Ground__c'}">
																		<aura:set attribute="else">
																			<aura:if isTrue="{!itinerary.record.attributes.type == 'Freight__c'}">
																				<aura:set attribute="else">
																					<aura:if isTrue="{!itinerary.record.attributes.type == 'Air__c'}"> </aura:if>
																				</aura:set>
																			</aura:if>
																		</aura:set>
																	</aura:if>
																</aura:set>
															</aura:if>
															<tbody>
																<aura:if isTrue="{!itinerary.record.attributes.type == 'Housing__c'}">
																	<!-- Fix By Clay Dev 14 may, 2021 #178008238
																	<aura:if isTrue="{!!empty(itinerary.record.Housing__r)}">
																		<aura:iteration items="{!itinerary.record.Housing__r.records}" var="roomType">-->
																		<aura:if isTrue="{!!empty(itinerary.relatedRecords)}">
																		<aura:iteration items="{!itinerary.relatedRecords}" var="roomType">
																			<tr class="slds-hint-parent">
																				<td data-label="CHECK-IN">
																					<div
																						class="slds-truncate"
																						title="{!!empty(roomType.Date_In_Text__c) ? roomType.Date_In_Text__c : ''}"
																					>
																						{!!empty(roomType.Date_In_Text__c) ? roomType.Date_In_Text__c : ''}
																					</div>
																				</td>
																				<td data-label="CHECK-OUT">
																					<div
																						class="slds-truncate"
																						title="{!!empty(roomType.Date_Out_Text__c) ? roomType.Date_Out_Text__c : ''}"
																					>
																						{!!empty(roomType.Date_Out_Text__c) ? roomType.Date_Out_Text__c : ''}
																					</div>
																				</td>
																				<td data-label="ROOMS">
																					<div class="slds-truncate" title="{!!empty(roomType.Units__c) ? roomType.Units__c : ''}">
																						{!!empty(roomType.Units__c) ? roomType.Units__c : ''}
																					</div>
																				</td>
																				<td data-label="ROOM DESCRIPTION">
																					<div class="slds-truncate" title="{!!empty(roomType.Unit_Type__c) ? roomType.Unit_Type__c : ''}">
																						{!!empty(roomType.Unit_Type__c) ? roomType.Unit_Type__c : ''}
																					</div>
																				</td>
																				<td data-label="RATE">
																					<div class="slds-truncate" title="{!!empty(roomType.Rate__c) ? roomType.Rate__c : ''}">
																						{!!empty(roomType.Rate__c) ? '' + roomType.CurrencyIsoCode +  roomType.Rate__c + ' ' +roomType.Rate_Period__c : ''}
																					</div>
																				</td>
																			</tr>
																		</aura:iteration>
																	</aura:if>
																	<aura:set attribute="else">
																		<aura:if isTrue="{!itinerary.record.attributes.type == 'Ground__c'}">
																			<aura:iteration items="{!itinerary.relatedRecords}" var="subTrip">
																				<aura:if isTrue="{!!empty(subTrip.GTTravels__r)}">
																					<tr>
																						<td>
																							<table class="slds-table slds-table_cell-buffer" style="border-top: 1px solid #eaeaea">
																								<thead>
																									<tr class="slds-line-height_reset">
																										<th width="33.3%" scope="col">
																											<div class="slds-truncate" title="PICK-UP">PICK-UP</div>
																										</th>
																										<th width="33.3%" scope="col">
																											<div class="slds-truncate" title="DROP-OFF">DROP-OFF</div>
																										</th>
																										<th width="33.3%" scope="col">
																											<div class="slds-truncate" title="TRIP DESCRIPTION">TRIP DESCRIPTION</div>
																										</th>
																									</tr>
																								</thead>
																								<tbody>
																									<aura:iteration items="{!subTrip.GTTravels__r.records}" var="travel">
																										<tr class="slds-hint-parent">
																											<td data-label="PICK-UP">
																												<div
																													class="slds-truncate"
																													title="{!(!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c + ' - ' : '') + (!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c + ' | ' : '') + (!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : '')}"
																												>
																													<aura:if isTrue="{!!empty(travel.Location_Details__c)}"
																														>{!travel.Location_Details__c}<br /></aura:if
																													>{!(!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c : '') }<br />{!(!empty(travel.Start_Date_Text__c)
																													? travel.Start_Date_Text__c + ' | ' : '') +
																													(!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : '')}
																												</div>
																											</td>
																											<td data-label="DROP-OFF">
																												<div
																													class="slds-truncate"
																													title="{!(!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c + ' - ' : '') + (!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c + ' | ' : '') + (!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : '')}"
																												>
																													<aura:if isTrue="{!!empty(travel.Location_Drop_off__c)}"
																														>{!travel.Location_Drop_off__c}<br /></aura:if
																													>{!(!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c : '')}<br />{!(!empty(travel.End_Date_Text__c)
																													? travel.End_Date_Text__c + ' | ' : '') + (!empty(travel.End_Date_Time_Text__c) ?
																													travel.End_Date_Time_Text__c : '')}
																												</div>
																											</td>
																											<td data-label="TRIP DESCRIPTION">
																												<div
																													class="slds-truncate"
																													title="{!!empty(travel.Airline_Info_Special_Notes__c) ? travel.Airline_Info_Special_Notes__c : ''}"
																												>
																													{!!empty(travel.Airline_Info_Special_Notes__c) ?
																													travel.Airline_Info_Special_Notes__c : ''}
																												</div>
																											</td>
																										</tr>
																									</aura:iteration>
																								</tbody>
																							</table>
																						</td>
																					</tr>
																				</aura:if>
																				<aura:if isTrue="{!!empty(itinerary.record.Ground__r)}">
																					<tr>
																						<td>
																							<table class="slds-table slds-table_cell-buffer">
																								<tbody>
																									<aura:iteration items="{!itinerary.record.Ground__r.records}" var="vehicle">
																										<tr class="slds-hint-parent">
																											<td width="10%">
																												<div
																													class="slds-truncate"
																													title="{!!empty(vehicle.Vehicle_Ref__c) ? vehicle.Vehicle_Ref__c : ''}"
																												>
																													<strong>{!!empty(vehicle.Vehicle_Ref__c) ? vehicle.Vehicle_Ref__c : ''}</strong>
																												</div>
																											</td>
																											<td width="60%">
																												<div
																													class="slds-truncate"
																													title="{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') + (!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') + (!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '')}"
																												>
																													{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') +
																													(!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') +
																													(!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '')}
																												</div>
																											</td>
																											<td width="30%"></td>
																										</tr>
																									</aura:iteration>
																								</tbody>
																							</table>
																						</td>
																					</tr>
																				</aura:if>
																			</aura:iteration>
																			<tr>
																				<td>
																					<table
																						class="slds-table slds-table_cell-buffer"
																						style="border-top: 1px solid #eaeaea; border-bottom: 1px solid #eaeaea"
																					>
																						<tbody>
																							<tr class="slds-hint-parent">
																								<td width="40%"></td>
																								<td width="40%"></td>
																								<td width="20%">
																									<div class="slds-truncate">
																										<strong style="margin-right: 20px">TOTAL PRICE</strong
																										>{!!empty(itinerary.record.Total_Price__c) ? '$' + itinerary.record.Total_Price__c : ''}
																									</div>
																								</td>
																							</tr>
																						</tbody>
																					</table>
																				</td>
																			</tr>
																			<aura:set attribute="else">
																				<aura:if isTrue="{!itinerary.record.attributes.type == 'Freight__c'}">
																					<aura:iteration items="{!itinerary.relatedRecords}" var="subTrip">
																						<aura:if isTrue="{!!empty(subTrip.FreightEquipments__r)}">
																							<tr>
																								<td>
																									<table class="slds-table slds-table_cell-buffer" style="border-top: 1px solid #eaeaea">
																										<thead>
																											<tr class="slds-line-height_reset">
																												<th width="33.3%" scope="col">
																													<div class="slds-truncate" title="PICK-UP">PICK-UP</div>
																												</th>
																												<th width="33.3%" scope="col">
																													<div class="slds-truncate" title="DROP-OFF">DROP-OFF</div>
																												</th>
																												<th width="33.3%" scope="col">
																													<div class="slds-truncate" title="FREIGHT TRUCK SQ FT">FREIGHT TRUCK SQ FT</div>
																												</th>
																											</tr>
																										</thead>
																										<tbody>
																											<aura:iteration items="{!subTrip.FreightEquipments__r.records}" var="travel">
																												<tr class="slds-hint-parent">
																													<td data-label="PICK-UP">
																														<div
																															class="slds-truncate"
																															title="{!(!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c + ' - ' : '') + (!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c + ' | ' : '') + (!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : '')}"
																														>
																															<aura:if isTrue="{!!empty(travel.Location_Pick_up__c)}"
																																>{!travel.Location_Pick_up__c}<br /></aura:if
																															>{!(!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c + ' | ' :
																															'') + (!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c
																															: '')}
																														</div>
																													</td>
																													<td data-label="DROP-OFF">
																														<div
																															class="slds-truncate"
																															title="{!(!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c + ' - ' : '') + (!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c + ' | ' : '') + (!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : '')}"
																														>
																															<aura:if isTrue="{!!empty(travel.Location_Drop_off__c)}"
																																>{!travel.Location_Drop_off__c}<br /></aura:if
																															>{!(!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c + ' | ' : '') +
																															(!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : '')}
																														</div>
																													</td>
																													<td data-label="FREIGHT TRUCK SQ FT">
																														<div
																															class="slds-truncate"
																															title="{!!empty(travel.Freight_Truck_Sq_Ft__c) ? travel.Freight_Truck_Sq_Ft__c : ''}"
																														>
																															{!!empty(travel.Freight_Truck_Sq_Ft__c) ? travel.Freight_Truck_Sq_Ft__c : ''}
																														</div>
																													</td>
																												</tr>
																											</aura:iteration>
																										</tbody>
																									</table>
																								</td>
																							</tr>
																						</aura:if>
																						<aura:if isTrue="{!!empty(itinerary.record.FreightSubTrips__r)}">
																							<tr>
																								<td>
																									<table class="slds-table slds-table_cell-buffer">
																										<tbody>
																											<aura:iteration items="{!itinerary.record.FreightSubTrips__r.records}" var="vehicle">
																												<tr class="slds-hint-parent">
																													<td width="10%">
																														<div
																															class="slds-truncate"
																															title="{!!empty(vehicle.Equipment__c) ? vehicle.Equipment__c : ''}"
																														>
																															<strong>{!!empty(vehicle.Equipment__c) ? vehicle.Equipment__c : ''}</strong>
																														</div>
																													</td>
																													<td width="60%">
																														<div
																															class="slds-truncate"
																															title="{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') + (!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') + (!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '') + (!empty(vehicle.Freight_Truck_Sq_Ft__c) ? ' | ' + vehicle.Freight_Truck_Sq_Ft__c : '')}"
																														>
																															{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') +
																															(!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') +
																															(!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '') +
																															(!empty(vehicle.Freight_Truck_Sq_Ft__c) ? ' | ' +
																															vehicle.Freight_Truck_Sq_Ft__c : '')}
																														</div>
																													</td>
																													<td width="30%"></td>
																												</tr>
																											</aura:iteration>
																										</tbody>
																									</table>
																								</td>
																							</tr>
																						</aura:if>
																					</aura:iteration>
																					<tr>
																						<td>
																							<table
																								class="slds-table slds-table_cell-buffer"
																								style="border-top: 1px solid #eaeaea; border-bottom: 1px solid #eaeaea"
																							>
																								<tbody>
																									<tr class="slds-hint-parent">
																										<td width="40%"></td>
																										<td width="40%"></td>
																										<td width="20%">
																											<div class="slds-truncate">
																												<strong style="margin-right: 20px">TOTAL PRICE</strong
																												>{!!empty(itinerary.record.Total_Price__c) ? '$' + itinerary.record.Total_Price__c :
																												''}
																											</div>
																										</td>
																									</tr>
																								</tbody>
																							</table>
																						</td>
																					</tr>
																					<aura:set attribute="else">
																						<aura:if isTrue="{!itinerary.record.attributes.type == 'Air__c'}">
																							<aura:if isTrue="{!!empty(itinerary.record.Air_Segments__r)}">
																								<tr>
																									<td>
																										<table class="slds-table slds-table_cell-buffer" style="border-top: 1px solid #eaeaea">
																											<thead>
																												<tr class="slds-line-height_reset">
																													<th width="33.3%" scope="col">
																														<div class="slds-truncate" title="DEPART">DEPART</div>
																													</th>
																													<th width="33.3%" scope="col">
																														<div class="slds-truncate" title="DROP-OFF">DROP-OFF</div>
																													</th>
																													<th width="33.3%" scope="col">
																														<div class="slds-truncate" title="FLIGHT DESCRIPTION">FLIGHT DESCRIPTION</div>
																													</th>
																												</tr>
																											</thead>
																											<tbody>
																												<aura:iteration items="{!itinerary.record.Air_Segments__r.records}" var="segment">
																													<tr class="slds-hint-parent">
																														<td data-label="DEPART">
																															<div
																																class="slds-truncate"
																																title="{!(!empty(segment.Departure_City__r) &amp;&amp; !empty(segment.Departure_City__r.City__r) ? ((!empty(segment.Departure_City__r.City__r.City__c) ? segment.Departure_City__r.City__r.City__c : '') + (!empty(segment.Departure_City__r.City__r.State__c) ? ', ' + segment.Departure_City__r.City__r.State__c : '')) : '') + (!empty(segment.Departure_City__r) ?  ' - ' + segment.Departure_City__r.Name : '') + (!empty(segment.Departure_Date_Text__c) ? ' - ' + segment.Departure_Date_Text__c : '')}"
																															>
																																{!(!empty(segment.Departure_City__r) &amp;&amp;
																																!empty(segment.Departure_City__r.City__r) ?
																																((!empty(segment.Departure_City__r.City__r.City__c) ?
																																segment.Departure_City__r.City__r.City__c : '') +
																																(!empty(segment.Departure_City__r.City__r.State__c) ? ', ' +
																																segment.Departure_City__r.City__r.State__c : '')) : '')}<br />{!(!empty(segment.Departure_City__r)
																																? segment.Departure_City__r.Name : '')}<br />{!(!empty(segment.Departure_Date_Text__c)
																																? segment.Departure_Date_Text__c + ' | ' : '') +
																																(!empty(segment.Dep_Time_Text__c) ? segment.Dep_Time_Text__c : '')}
																															</div>
																														</td>
																														<td data-label="DROP-OFF">
																															<div
																																class="slds-truncate"
																																title="{!(!empty(segment.Arrival_City__r) &amp;&amp; !empty(segment.Arrival_City__r.City__r) ? ((!empty(segment.Arrival_City__r.City__r.City__c) ? segment.Arrival_City__r.City__r.City__c : '') + (!empty(segment.Arrival_City__r.City__r.State__c) ? ', ' + segment.Arrival_City__r.City__r.State__c : '')) : '') + (!empty(segment.Arrival_City__r) ?  ' - ' + segment.Arrival_City__r.Name : '') + (!empty(segment.Arrival_Date_Text__c) ? ' - ' + segment.Arrival_Date_Text__c : '')}"
																															>
																																{!(!empty(segment.Arrival_City__r) &amp;&amp;
																																!empty(segment.Arrival_City__r.City__r) ?
																																((!empty(segment.Arrival_City__r.City__r.City__c) ?
																																segment.Arrival_City__r.City__r.City__c : '') +
																																(!empty(segment.Arrival_City__r.City__r.State__c) ? ', ' +
																																segment.Arrival_City__r.City__r.State__c : '')) : '')}<br />{!(!empty(segment.Arrival_City__r)
																																? segment.Arrival_City__r.Name : '')}<br />{!(!empty(segment.Arrival_Date_Text__c)
																																? segment.Arrival_Date_Text__c + ' | ' : '') +
																																(!empty(segment.Arr_Time_Text__c) ? segment.Arr_Time_Text__c : '')}
																															</div>
																														</td>
																														<td data-label="FLIGHT DESCRIPTION">
																															{!(!empty(segment.Flight_Duration_hrs__c) ? segment.Flight_Duration_hrs__c +
																															'hr ' : '') + (!empty(segment.Flight_Duration_Mins__c) ?
																															segment.Flight_Duration_Mins__c + 'min ' : '') +
																															(!empty(segment.Number_of_Seats__c) ? ' | ' + segment.Number_of_Seats__c + '
																															seats ' : '') + (!empty(segment.Equip_Type__c) ? ' | ' + segment.Equip_Type__c
																															: '')}
																														</td>
																													</tr>
																												</aura:iteration>
																											</tbody>
																										</table>
																									</td>
																								</tr>
																							</aura:if>
																							<tr>
																								<td>
																									<table
																										class="slds-table slds-table_cell-buffer"
																										style="border-top: 1px solid #eaeaea; border-bottom: 1px solid #eaeaea"
																									>
																										<tbody>
																											<tr class="slds-hint-parent">
																												<td width="40%"></td>
																												<td width="40%"></td>
																												<td width="20%">
																													<div class="slds-truncate">
																														<strong style="margin-right: 20px">PRICE PER TICKET</strong
																														>{!!empty(itinerary.record.Total_Price__c) ? '$' +
																														itinerary.record.Total_Price__c : ''}
																													</div>
																												</td>
																											</tr>
																										</tbody>
																									</table>
																								</td>
																							</tr>
																						</aura:if>
																					</aura:set>
																				</aura:if>
																			</aura:set>
																		</aura:if>
																	</aura:set>
																</aura:if>
															</tbody>
														</table>
													</div>
												</div>
											</div>
										</div>
										<footer class="slds-grid slds-gutters slds-wrap">
											<div class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12"></div>
											<div
												class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12 itinerary_buttons"
												data-servicetype="{!itinerary.record.attributes.type}"
												data-serviceid="{!itinerary.record.Id}"
												data-servicedateinandout="{!itinerary.record.attributes.type == 'Housing__c' ? itinerary.record.Date_In_Text__c + (!empty(itinerary.record.Date_Out_Text__c) ? ' - ' + itinerary.record.Date_Out_Text__c : '') : itinerary.record.attributes.type == 'Ground__c' ? itinerary.record.Start_Date_Text__c + (!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') : itinerary.record.attributes.type == 'Freight__c' ? itinerary.record.Start_Date_Text__c + (!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') : itinerary.record.attributes.type == 'Air__c' ? itinerary.record.Departure_Date_Text__c + (!empty(itinerary.record.Return_Date_Text__c) ? ' - ' + itinerary.record.Return_Date_Text__c : '') : ''}"
												data-servicecityname="{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.City__r) ? ((!empty(itinerary.record.City__r.City__c) ? itinerary.record.City__r.City__c : '') + (!empty(itinerary.record.City__r.State__c) ? ', ' + itinerary.record.City__r.State__c : '')) : '') : itinerary.record.attributes.type == 'Ground__c' ? (!empty(itinerary.record.Start_city__r) ? ((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') + (!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') : itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Start_city__r) ? ((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') + (!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') : itinerary.record.attributes.type == 'Air__c' ? (!empty(itinerary.record.Departure_City__r) &amp;&amp; !empty(itinerary.record.Departure_City__r.City__r) ? ((!empty(itinerary.record.Departure_City__r.City__r.City__c) ? itinerary.record.Departure_City__r.City__r.City__c : '') + (!empty(itinerary.record.Departure_City__r.City__r.State__c) ? ', ' + itinerary.record.Departure_City__r.City__r.State__c : '')) : '') : ''}"
											>
                                                <!-- Fix By Clay Dev #178056511-->
												<aura:if
													isTrue="{!or(and(itinerary.record.attributes.type == 'Housing__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Decision' || itinerary.record.Status_CC__c == 'Pending Client Signature'), and(itinerary.record.attributes.type == 'Freight__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature'), and(itinerary.record.attributes.type == 'Air__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature'), and(itinerary.record.attributes.type == 'Ground__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature') )}"
												>
													<button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleOptions}">
														VIEW OPTIONS
													</button>
													<!--<button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleOptions}">REVIEW CONTRACT</button>-->
												</aura:if>
												<aura:if
													isTrue="{!or(and(itinerary.record.attributes.type == 'Housing__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature'),and(itinerary.record.attributes.type == 'Ground__c', itinerary.record.Status_Ground__c == 'Contracted'), and(itinerary.record.attributes.type == 'Freight__c', itinerary.record.Status__c == 'Contracted'), and(itinerary.record.attributes.type == 'Air__c', itinerary.record.Status__c == 'Contracted'))}"
												>
													<!-- remove documents button <button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleDocuments}">
														DOCUMENTS
													</button>-->
												</aura:if>
											</div>
										</footer>
									</div>
								</article>
							</aura:iteration>
						</aura:iteration>
					</section>
				</div>
			</div>
		</div>
	</div>
</aura:component>
```
### VoyajerItineraryOverviewController

```
({
  onRender: function (component, event, helper) {
    //Fix By Clay Dev 27 Feb, 2021 #177024410
    //helper.getData(component, "searchItineraries", null);
    
      if(component.get('v.startDate') != undefined || component.get('v.endDate') != undefined || 
        (component.get('v.selectedLookupId') != undefined && component.get('v.selectedPillText') != undefined)) {
    	component.find('startDateInput').set("v.value", component.get('v.startDate'));
    	component.find('endDateInput').set("v.value", component.get('v.endDate'));
          if(component.get('v.selectedLookupId') != undefined && component.get('v.selectedPillText') != undefined) {
            component.find('lookupCity').set('v.lookupId', component.get('v.selectedLookupId'));
            component.find('lookupCity').set('v.pillText', component.get('v.selectedPillText'));
            component.find('lookupCity').set("v.isEdited",true);
          
            var forclose = component.find('lookupCity').find("lookup-pill");
            $A.util.addClass(forclose, 'slds-show');
            $A.util.removeClass(forclose, 'slds-hide');
          
            var forclose = component.find('lookupCity').find("searchRes");
            $A.util.addClass(forclose, 'slds-is-close');
            $A.util.removeClass(forclose, 'slds-is-open');
            $A.util.removeClass(forclose, 'slds-has-error');
            
            var message = component.find('lookupCity').find("requiredMessage");
            $A.util.addClass(message, 'slds-hide');
            $A.util.removeClass(message, 'slds-show');
          
            var lookUpTarget = component.find('lookupCity').find("lookupField");
            $A.util.addClass(lookUpTarget, 'slds-hide');
            $A.util.removeClass(lookUpTarget, 'slds-show'); 
        }
      
    	component.set('v.startDate', null);
        component.set('v.endDate', null);
        component.set('v.selectedLookupId', null);
        component.set('v.selectedPillText', null);
        helper.getData(component, "searchItineraries", null);
      } else {
          $A.util.addClass(component.find("loading"), "slds-hide");
      }
  },

  handleBack: function (component, event, helper) {
    component.set("v.productionSelected", "");
    component.set("v.mainContent", "dashboard");
  },

  handleUpdate: function (component, event, helper) {
    var thelookup = component.find('lookupCity').get('v.lookupId');
    helper.getData(component, "searchItineraries",thelookup);
    console.log ('theLookup :: ' + thelookup);
  },

  handleClear: function (component, event, helper) {
    helper.clearData(component, event);
  },

  handleExpand: function (component, event, helper) {
    $(event.currentTarget).parents(".slds-section").toggleClass("slds-is-open");
  },

  handleDocuments: function (component, event, helper) {
    console.log("handleDocuments");
    var serviceId = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("serviceid");
    var serviceType = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("servicetype");
    component.set("v.serviceId", serviceId);
    component.set("v.serviceType", serviceType);
    component.set(
      "v.serviceDateInAndOut",
      $(event.currentTarget)
        .parents(".itinerary_buttons")
        .data("servicedateinandout")
    );
    component.set(
      "v.serviceCityName",
      $(event.currentTarget)
        .parents(".itinerary_buttons")
        .data("servicecityname")
    );
    helper.setSearchParameters(component, event);
    component.set("v.mainContent", "documents");
  },

  handleOptions: function (component, event, helper) {
    console.log("handleOptions");
    component.set("v.displaySelect", false);
    
    var serviceId = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("serviceid");
    var serviceType = $(event.currentTarget)
      .parents(".itinerary_buttons")
      .data("servicetype");
    if (!!serviceId && !!serviceType) {
      component.set("v.optionRecordId", serviceId);
      helper.setSearchParameters(component, event);
      if (serviceType == "Housing__c")
        component.set("v.mainContent", "optionsHousing");
      if (serviceType == "Ground__c")
        component.set("v.mainContent", "optionsGT");
      if (serviceType == "Freight__c")
        component.set("v.mainContent", "optionsFreight");
      if (serviceType == "Air__c") component.set("v.mainContent", "optionsAir");
    }
  },

  openReviewSubmit: function (component, event, helper) {
    /*//HERE 080520 - enviar bidId, cambiar en review component de cada servicio, para que use el bidId, y no el index (victor)
        var serviceType = $(event.currentTarget).parents('.itinerary_buttons').data('servicetype');
        var bidId = $(event.currentTarget).parents('.itinerary_buttons').data('serviceid');
        
        if(!!bidId && !!serviceType) {
            console.log('# serviceId = ' + serviceId);
            console.log('# serviceType = ' + serviceType);
            component.set("v.bidRecordId", bidId);
            
            if(serviceType == 'Housing__c') component.set("v.mainContent","optionsHousingReviewSubmit");
            //if(serviceType == 'Ground__c') component.set("v.mainContent","optionsGT");
            //if(serviceType == 'Freight__c') component.set("v.mainContent","optionsFreight");
            //if(serviceType == 'Air__c') component.set("v.mainContent","optionsAir");
        }*/
  },
    handleCommunicationEventGetCity : function(component, event, helper) {
        console.log("Inside parent");
		var obj = event.getParam("data");
		console.log(JSON.stringify(obj));
        component.set("v.serviceCity", obj);
    }
});
```
### VoyajerItineraryOverviewHelper

```
({
	getData : function(component, method,city){
		var action = component.get("c." + method);
        var lookupValue = component.find('lookupCity').get('v.lookupId');
		if(method == "searchItineraries") action.setParams({opportunityId: component.get("v.productionSelected"), startDate: component.find('startDateInput').get("v.value"), endDate: component.find('endDateInput').get("v.value"), cityId: lookupValue});
		action.setCallback(this, function(response){
			var state = response.getState();
			if(state === "SUCCESS"){
				var result = JSON.parse(response.getReturnValue());
                var resultMap = [];
                for(var key in result) resultMap.unshift({key: $A.localizationService.formatDate(key, "EEE, dd MMM yyyy"), value: result[key]});
				console.log(resultMap);
				if(method == "searchItineraries") component.set("v.data", resultMap);
                $A.util.addClass(component.find("loading"), "slds-hide");
			}
			else if(state === "INCOMPLETE"){
			}
			else if(state === "ERROR"){
				var errors = response.getError();
				if(errors){
					if(errors[0] && errors[0].message) console.log("Error message: " + errors[0].message);
				}
				else{
					console.log("Unknown error");
				}
			}
		});
		//$A.util.removeClass(component.find("loading"), "slds-hide");
		$A.enqueueAction(action);
	},
    
	clearData : function(component, event){
		component.find('startDateInput').set("v.value", null);
		component.find('endDateInput').set("v.value", null);
		component.set("v.data", null);
        
        var pillTarget = component.find('lookupCity').find("lookup-pill");
        var lookUpTarget = component.find('lookupCity').find("lookupField"); 
        
        $A.util.addClass(pillTarget, 'slds-hide');
        $A.util.removeClass(pillTarget, 'slds-show');
        
        $A.util.addClass(lookUpTarget, 'slds-show');
        $A.util.removeClass(lookUpTarget, 'slds-hide');
        
        component.find('lookupCity').set("v.searchKeyWord","");
        component.find('lookupCity').set("v.listOfSearchRecords", null);
        component.find('lookupCity').set("v.selectedRecord",{});
        if(!!component.find('lookupCity').get("v.lookupId")) component.find('lookupCity').set("v.isEdited",true);
        component.find('lookupCity').set("v.lookupId","");
        
	},
    
    setSearchParameters : function(component, event){
		component.set("v.startDate", component.find('startDateInput').get("v.value"));
      	component.set("v.endDate", component.find('endDateInput').get("v.value"));
      	component.set("v.selectedLookupId", component.find('lookupCity').get('v.lookupId'));
      	component.set("v.selectedPillText", component.find('lookupCity').get('v.pillText'));
	}
})
```
### VoyajerItineraryOverview

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerItineraryOverview

```
/*
	Version:	    V1.0
	Create Date:	2/09/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}

/*--------------------
-----Overview------
----------------------*/

.THIS .slds-card-overview_header{
    background-color: #f6f7fc;
    color: #022066;
    font-weight: bold;
}

.THIS .slds-card-overview_header>h3{
    padding: 1rem;
}

.THIS .slds-card-overview_item{
    margin-top: .8rem;
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    background-color: #022066;
    transition: transform 0.1s ease;
}

.THIS .slds-card-overview_item:hover{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    -webkit-transform: scale(1.01);
    -moz-transform: scale(1.01);
    -o-transform: scale(1.01);
    transform: scale(1.01);
}

.THIS .slds-card-overview_item-leftside{
    display:flex;
    height: 100%;
    justify-content: center;
}

.THIS .slds-card-overview_item-content{
    background-color: white;
    padding-bottom: 10px;
    border-bottom: 1px solid #eaeaea;
}

.THIS .slds-card-overview_item header{
    margin-top: .5rem;
}

.THIS .slds-card-overview_item header h3{
    font-weight: bold;
    color: #022066;
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

/*--------------------
-----Input Dates------
----------------------*/

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

/*--------------------
-----Medias queries------
----------------------*/

@media (max-width: 768px){
    .THIS .slds-section__content{
        overflow-x: auto !important;
    }
}
```
### VoyajerItineraryOverview

```
<aura:component controller="VoyajerItineraryOverviewController">
	<aura:attribute name="mainContent" type="String" />
	<aura:attribute type="String" name="optionRecordId" />
	<aura:attribute name="productionSelected" type="String" default="0065600000765ufAAA" />
	<aura:attribute name="productionName" type="String" />
	<aura:attribute name="displaySelect" type="Boolean" default="true" />
	<aura:attribute name="productionCompany" type="String" />
	<aura:attribute name="serviceId" type="String" />
	<aura:attribute name="serviceType" type="String" />
	<aura:attribute name="serviceDateInAndOut" type="String" />
	<aura:attribute name="serviceCityName" type="String" />
	<aura:attribute name="serviceCity" type="Object" default="{}" />

	<aura:attribute name="startDate" type="String" />
	<aura:attribute name="endDate" type="String" />
	<aura:attribute name="selectedLookupId" type="String" />
	<aura:attribute name="selectedPillText" type="String" />
	<aura:attribute name="data" type="List" access="private" />
	<ltng:require scripts="{!$Resource.RoadRebelUtils + '/js/jquery-3.3.1.min.js'}" />

	<aura:handler name="callToParentGetCity" action="{!c.handleCommunicationEventGetCity}" event="c:VoyajerCustomLookupGetSelectedCity" />

	<aura:handler name="render" value="{!this}" action="{!c.onRender}" />
	<div>
		<lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
		<div class="pageContent" style="min-height: 680px">
			<div class="pageContentSpaces">
				<div class="page-section">
					<div class="page-header">
						<h1 class="page-header-title">Itinerary Overview</h1>
						<lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
					</div>
				</div>
				<div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb">
					<div class="page-section">
						<h3>
							<i class="far fa-star" style="color: #9f9f9f; margin-right: 0.5em"></i
							><strong style="color: black">{!v.productionName}</strong>
						</h3>
						<h4 style="color: black">{!v.productionCompany}</h4>
					</div>
					<div class="page-section-buttons">
						<div style="align-items: center; justify-content: flex-start; flex: 1">
							<p style="margin-right: 0.5em">Filter by</p>
							<lightning:layout horizontalAlign="center" verticalAlign="center">
								<lightning:layoutItem padding="around-medium">
									<br/>
									<div class="startDateContainer">
										<lightning:input
											aura:id="startDateInput"
											type="date"
											label=""
											variant="label-hidden"
											dateStyle="short"
											placeholder="mm/dd/yyyy"
											class="startDateInput"
											onchange=""
											autocomplete="off"
										/>
										<div style="padding: 0 0.5em">-</div>
										<lightning:input
											aura:id="endDateInput"
											type="date"
											label=""
											variant="label-hidden"
											dateStyle="short"
											placeholder="mm/dd/yyyy"
											class="startDateInput"
											onchange=""
											autocomplete="off"
										/>
										<div style="padding-right: 0.5em">
											<lightning:icon iconName="utility:date_input" size="x-small" />
										</div>
									</div>
								</lightning:layoutItem>
								<lightning:layoutItem>
									<div class="formField" style="width: 300px">
										<c:VoyajerCustomLookup
											aura:id="lookupCity"
											objectAPIName="City__c"
											fieldName="City__c"
											iconName="custom:custom24"
											lookupId=""
											label=""
											inputPlaceholder="Enter Location"
											isRequired="false"
											isEdited="false"
											loadCityLookup="{!v.loadCityLookup}"
											triggerLookupValidation="{!v.triggerLookupValidation}"
										/>
									</div>
								</lightning:layoutItem>
								<lightning:layoutItem padding="around-large">
									<br/>
									<lightning:button label="Update" variant="brand" class="formButtonBrandLight" onclick="{!c.handleUpdate}" />
									<lightning:button label="Clear" variant="neutral" onclick="{!c.handleClear}" />
								</lightning:layoutItem>
							</lightning:layout>
						</div>
					</div>
				</div>
				<div class="pageContentDashboard" style="padding-top: 0; border-bottom: 1px solid #dbdbdb">
					<section class="page-section slds-card-overview">
						<aura:iteration items="{!v.data}" var="dataMap" indexVar="key">
							<header class="slds-grid slds-gutters slds-wrap slds-card-overview_header">
								<h3>{!dataMap.key}<br /></h3>
							</header>
							<aura:iteration items="{!dataMap.value}" var="itinerary">
								<article class="slds-grid slds-gutters slds-wrap slds-card-overview_item">
									<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-overview_item-leftside">
										<div class="slds-media slds-media_responsive">
											<div class="slds-media__figure" style="margin-top: 10px; margin-right: 0">
												<span class="slds-avatar slds-avatar_large">
													<img
														src="{!$Resource.CommunityImages + (itinerary.record.attributes.type == 'Housing__c' ? '/SelectServiceIcons/service_housing_icons.png' : itinerary.record.attributes.type == 'Ground__c' ? '/SelectServiceIcons/service_busing_icons.png' : itinerary.record.attributes.type == 'Freight__c' ? '/SelectServiceIcons/service_freight_icons.png' : itinerary.record.attributes.type == 'Air__c' ? '/SelectServiceIcons/service_plane_icons.png' : '')}"
														title="housing"
													/>
												</span>
											</div>
										</div>
									</div>
									<div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-overview_item-content">
										<header class="slds-grid slds-gutters slds-wrap">
											<div class="slds-col slds-size_1-of-1 slds-medium-size_7-of-12">
												<h3>
													{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Name : (itinerary.record.Status_CC__c == 'Layoff' ? itinerary.record.Status_CC__c : 'Vendor TBD')) : itinerary.record.attributes.type == 'Ground__c' ?
													(!empty(itinerary.record.Vendor_lookup__r) ? itinerary.record.Vendor_lookup__r.Name : 'Vendor TBD') :
													itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Name : 'Vendor TBD') : itinerary.record.attributes.type == 'Air__c' ?
													(!empty(itinerary.record.Vendor__r) ? itinerary.record.Vendor__r.Name : 'Vendor TBD') : ''}
												</h3>
												<p style="color: #333; font-weight: bold">
													{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													(!empty(itinerary.record.Vendor_lookup__r.ShippingStreet) ? itinerary.record.Vendor_lookup__r.ShippingStreet + ' '
													: '') + (!empty(itinerary.record.Vendor_lookup__r.ShippingCity) ? itinerary.record.Vendor_lookup__r.ShippingCity +
													', ' : '') + (!empty(itinerary.record.Vendor_lookup__r.ShippingState) ?
													itinerary.record.Vendor_lookup__r.ShippingState + ', ' : '') +
													(!empty(itinerary.record.Vendor_lookup__r.ShippingCountryCode) ?
													itinerary.record.Vendor_lookup__r.ShippingCountryCode : '') : '') : itinerary.record.attributes.type ==
													'Ground__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													(!empty(itinerary.record.Vendor_lookup__r.BillingStreet) ? itinerary.record.Vendor_lookup__r.BillingStreet + ' ' :
													'') + (!empty(itinerary.record.Vendor_lookup__r.BillingCity) ? itinerary.record.Vendor_lookup__r.BillingCity + ',
													' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingState) ? itinerary.record.Vendor_lookup__r.BillingState
													+ ', ' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingCountryCode) ?
													itinerary.record.Vendor_lookup__r.BillingCountryCode : '') : '') : itinerary.record.attributes.type ==
													'Freight__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													(!empty(itinerary.record.Vendor_lookup__r.BillingStreet) ? itinerary.record.Vendor_lookup__r.BillingStreet + ' ' :
													'') + (!empty(itinerary.record.Vendor_lookup__r.BillingCity) ? itinerary.record.Vendor_lookup__r.BillingCity + ',
													' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingState) ? itinerary.record.Vendor_lookup__r.BillingState
													+ ', ' : '') + (!empty(itinerary.record.Vendor_lookup__r.BillingCountryCode) ?
													itinerary.record.Vendor_lookup__r.BillingCountryCode : '') : '') : itinerary.record.attributes.type == 'Air__c' ?
													(!empty(itinerary.record.Vendor__r) ? (!empty(itinerary.record.Vendor__r.BillingStreet) ?
													itinerary.record.Vendor__r.BillingStreet + ' ' : '') + (!empty(itinerary.record.Vendor__r.BillingCity) ?
													itinerary.record.Vendor__r.BillingCity + ', ' : '') + (!empty(itinerary.record.Vendor__r.BillingState) ?
													itinerary.record.Vendor__r.BillingState + ', ' : '') + (!empty(itinerary.record.Vendor__r.BillingCountryCode) ?
													itinerary.record.Vendor__r.BillingCountryCode : '') : '') : ''} <br />
													{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Phone : '') : itinerary.record.attributes.type == 'Ground__c' ?
													(!empty(itinerary.record.Vendor_lookup__r) ? itinerary.record.Vendor_lookup__r.Phone : '') :
													itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Vendor_lookup__r) ?
													itinerary.record.Vendor_lookup__r.Phone : '') : itinerary.record.attributes.type == 'Air__c' ?
													(!empty(itinerary.record.Vendor__r) ? itinerary.record.Vendor__r.Phone : '') : ''}
												</p>
											</div>
											<div class="slds-col slds-size_1-of-1 slds-medium-size_5-of-12" style="font-weight: bold; color: #00b4ff">
												<span
													>{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.City__r) ?
													((!empty(itinerary.record.City__r.City__c) ? itinerary.record.City__r.City__c : '') +
													(!empty(itinerary.record.City__r.State__c) ? ', ' + itinerary.record.City__r.State__c : '')) : '') :
													itinerary.record.attributes.type == 'Ground__c' ? (!empty(itinerary.record.Start_city__r) ?
													((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') +
													(!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') :
													itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Start_city__r) ?
													((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') +
													(!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') :
													itinerary.record.attributes.type == 'Air__c' ? (!empty(itinerary.record.Departure_City__r) &amp;&amp;
													!empty(itinerary.record.Departure_City__r.City__r) ? ((!empty(itinerary.record.Departure_City__r.City__r.City__c)
													? itinerary.record.Departure_City__r.City__r.City__c : '') +
													(!empty(itinerary.record.Departure_City__r.City__r.State__c) ? ', ' +
													itinerary.record.Departure_City__r.City__r.State__c : '')) : '') : ''}</span
												>
												|
												<span
													>{!itinerary.record.attributes.type == 'Housing__c' ? itinerary.record.Date_In_Text__c +
													(!empty(itinerary.record.Date_Out_Text__c) ? ' - ' + itinerary.record.Date_Out_Text__c : '') :
													itinerary.record.attributes.type == 'Ground__c' ? itinerary.record.Start_Date_Text__c +
													(!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') :
													itinerary.record.attributes.type == 'Freight__c' ? itinerary.record.Start_Date_Text__c +
													(!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') :
													itinerary.record.attributes.type == 'Air__c' ? itinerary.record.Departure_Date_Text__c +
													(!empty(itinerary.record.Return_Date_Text__c) ? ' - ' + itinerary.record.Return_Date_Text__c : '') : ''}</span
												>
												<p>
													{!itinerary.record.attributes.type == 'Housing__c' ? (not(empty(itinerary.record.Venue__c))?
													itinerary.record.Venue__r.Name : '') : ''}
												</p>
											</div>
										</header>
										<div class="slds-grid slds-gutters slds-wrap">
											<div class="slds-col slds-size_1-of-1">
												<div class="slds-section slds-is-open">
													<h4 class="slds-section__title" style="border-top: 1px solid #eaeaea">
														<button
															aria-controls="expando-unique-id"
															aria-expanded="true"
															class="slds-button slds-section__title-action slds-button-expandable"
															onclick="{!c.handleExpand}"
														>
															<span
																class="slds-truncate"
																style="font-size: 0.875rem; font-weight: 600"
																title="{!itinerary.record.attributes.type == 'Housing__c' ? 'STAY DETAILS' : itinerary.record.attributes.type == 'Ground__c' ? 'TRIP DETAILS' : itinerary.record.attributes.type == 'Freight__c' ? 'TRIP DETAILS' : itinerary.record.attributes.type == 'Air__c' ? 'FLIGHT DETAILS' : ''}"
																>{!itinerary.record.attributes.type == 'Housing__c' ? 'STAY' : itinerary.record.attributes.type ==
																'Ground__c' ? 'TRIP' : itinerary.record.attributes.type == 'Freight__c' ? 'TRIP' :
																itinerary.record.attributes.type == 'Air__c' ? 'FLIGHT' : ''} DETAILS</span
															>
															<lightning:buttonIcon
																iconName="utility:down"
																variant="bare"
																alternativeText="Open"
																iconClass="buttonIcon-bluelight"
															/>
														</button>
													</h4>
													<div aria-hidden="false" class="slds-section__content" id="expando-unique-id" style="padding-top: 0; color: #333">
														<table
															class="{!itinerary.record.attributes.type == 'Housing__c' ? 'slds-table slds-table_cell-buffer' : itinerary.record.attributes.type == 'Ground__c' ? '' : itinerary.record.attributes.type == 'Freight__c' ? '' : itinerary.record.attributes.type == 'Air__c' ? '' : ''}"
														>
															<aura:if isTrue="{!itinerary.record.attributes.type == 'Housing__c'}">
																<thead>
																	<tr class="slds-line-height_reset">
																		<th class="" scope="col">
																			<div class="slds-truncate" title="CHECK-IN">CHECK-IN</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="CHECK-OUT">CHECK-OUT</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="ROOMS">ROOMS</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="ROOM DESCRIPTION">ROOM DESCRIPTION</div>
																		</th>
																		<th class="" scope="col">
																			<div class="slds-truncate" title="RATE">RATE</div>
																		</th>
																	</tr>
																</thead>
																<aura:set attribute="else">
																	<aura:if isTrue="{!itinerary.record.attributes.type == 'Ground__c'}">
																		<aura:set attribute="else">
																			<aura:if isTrue="{!itinerary.record.attributes.type == 'Freight__c'}">
																				<aura:set attribute="else">
																					<aura:if isTrue="{!itinerary.record.attributes.type == 'Air__c'}"> </aura:if>
																				</aura:set>
																			</aura:if>
																		</aura:set>
																	</aura:if>
																</aura:set>
															</aura:if>
															<tbody>
																<aura:if isTrue="{!itinerary.record.attributes.type == 'Housing__c'}">
																	<!-- Fix By Clay Dev 14 may, 2021 #178008238
																	<aura:if isTrue="{!!empty(itinerary.record.Housing__r)}">
																		<aura:iteration items="{!itinerary.record.Housing__r.records}" var="roomType">-->
																		<aura:if isTrue="{!!empty(itinerary.relatedRecords)}">
																		<aura:iteration items="{!itinerary.relatedRecords}" var="roomType">
																			<tr class="slds-hint-parent">
																				<td data-label="CHECK-IN">
																					<div
																						class="slds-truncate"
																						title="{!!empty(roomType.Date_In_Text__c) ? roomType.Date_In_Text__c : ''}"
																					>
																						{!!empty(roomType.Date_In_Text__c) ? roomType.Date_In_Text__c : ''}
																					</div>
																				</td>
																				<td data-label="CHECK-OUT">
																					<div
																						class="slds-truncate"
																						title="{!!empty(roomType.Date_Out_Text__c) ? roomType.Date_Out_Text__c : ''}"
																					>
																						{!!empty(roomType.Date_Out_Text__c) ? roomType.Date_Out_Text__c : ''}
																					</div>
																				</td>
																				<td data-label="ROOMS">
																					<div class="slds-truncate" title="{!!empty(roomType.Units__c) ? roomType.Units__c : ''}">
																						{!!empty(roomType.Units__c) ? roomType.Units__c : ''}
																					</div>
																				</td>
																				<td data-label="ROOM DESCRIPTION">
																					<div class="slds-truncate" title="{!!empty(roomType.Unit_Type__c) ? roomType.Unit_Type__c : ''}">
																						{!!empty(roomType.Unit_Type__c) ? roomType.Unit_Type__c : ''}
																					</div>
																				</td>
																				<td data-label="RATE">
																					<div class="slds-truncate" title="{!!empty(roomType.Rate__c) ? roomType.Rate__c : ''}">
																						{!!empty(roomType.Rate__c) ? '' + roomType.CurrencyIsoCode +  roomType.Rate__c + ' ' +roomType.Rate_Period__c : ''}
																					</div>
																				</td>
																			</tr>
																		</aura:iteration>
																	</aura:if>
																	<aura:set attribute="else">
																		<aura:if isTrue="{!itinerary.record.attributes.type == 'Ground__c'}">
																			<aura:iteration items="{!itinerary.relatedRecords}" var="subTrip">
																				<aura:if isTrue="{!!empty(subTrip.GTTravels__r)}">
																					<tr>
																						<td>
																							<table class="slds-table slds-table_cell-buffer" style="border-top: 1px solid #eaeaea">
																								<thead>
																									<tr class="slds-line-height_reset">
																										<th width="33.3%" scope="col">
																											<div class="slds-truncate" title="PICK-UP">PICK-UP</div>
																										</th>
																										<th width="33.3%" scope="col">
																											<div class="slds-truncate" title="DROP-OFF">DROP-OFF</div>
																										</th>
																										<th width="33.3%" scope="col">
																											<div class="slds-truncate" title="TRIP DESCRIPTION">TRIP DESCRIPTION</div>
																										</th>
																									</tr>
																								</thead>
																								<tbody>
																									<aura:iteration items="{!subTrip.GTTravels__r.records}" var="travel">
																										<tr class="slds-hint-parent">
																											<td data-label="PICK-UP">
																												<div
																													class="slds-truncate"
																													title="{!(!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c + ' - ' : '') + (!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c + ' | ' : '') + (!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : '')}"
																												>
																													<aura:if isTrue="{!!empty(travel.Location_Details__c)}"
																														>{!travel.Location_Details__c}<br /></aura:if
																													>{!(!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c : '') }<br />{!(!empty(travel.Start_Date_Text__c)
																													? travel.Start_Date_Text__c + ' | ' : '') +
																													(!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : '')}
																												</div>
																											</td>
																											<td data-label="DROP-OFF">
																												<div
																													class="slds-truncate"
																													title="{!(!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c + ' - ' : '') + (!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c + ' | ' : '') + (!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : '')}"
																												>
																													<aura:if isTrue="{!!empty(travel.Location_Drop_off__c)}"
																														>{!travel.Location_Drop_off__c}<br /></aura:if
																													>{!(!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c : '')}<br />{!(!empty(travel.End_Date_Text__c)
																													? travel.End_Date_Text__c + ' | ' : '') + (!empty(travel.End_Date_Time_Text__c) ?
																													travel.End_Date_Time_Text__c : '')}
																												</div>
																											</td>
																											<td data-label="TRIP DESCRIPTION">
																												<div
																													class="slds-truncate"
																													title="{!!empty(travel.Airline_Info_Special_Notes__c) ? travel.Airline_Info_Special_Notes__c : ''}"
																												>
																													{!!empty(travel.Airline_Info_Special_Notes__c) ?
																													travel.Airline_Info_Special_Notes__c : ''}
																												</div>
																											</td>
																										</tr>
																									</aura:iteration>
																								</tbody>
																							</table>
																						</td>
																					</tr>
																				</aura:if>
																				<aura:if isTrue="{!!empty(itinerary.record.Ground__r)}">
																					<tr>
																						<td>
																							<table class="slds-table slds-table_cell-buffer">
																								<tbody>
																									<aura:iteration items="{!itinerary.record.Ground__r.records}" var="vehicle">
																										<tr class="slds-hint-parent">
																											<td width="10%">
																												<div
																													class="slds-truncate"
																													title="{!!empty(vehicle.Vehicle_Ref__c) ? vehicle.Vehicle_Ref__c : ''}"
																												>
																													<strong>{!!empty(vehicle.Vehicle_Ref__c) ? vehicle.Vehicle_Ref__c : ''}</strong>
																												</div>
																											</td>
																											<td width="60%">
																												<div
																													class="slds-truncate"
																													title="{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') + (!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') + (!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '')}"
																												>
																													{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') +
																													(!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') +
																													(!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '')}
																												</div>
																											</td>
																											<td width="30%"></td>
																										</tr>
																									</aura:iteration>
																								</tbody>
																							</table>
																						</td>
																					</tr>
																				</aura:if>
																			</aura:iteration>
																			<tr>
																				<td>
																					<table
																						class="slds-table slds-table_cell-buffer"
																						style="border-top: 1px solid #eaeaea; border-bottom: 1px solid #eaeaea"
																					>
																						<tbody>
																							<tr class="slds-hint-parent">
																								<td width="40%"></td>
																								<td width="40%"></td>
																								<td width="20%">
																									<div class="slds-truncate">
																										<strong style="margin-right: 20px">TOTAL PRICE</strong
																										>{!!empty(itinerary.record.Total_Price__c) ? '$' + itinerary.record.Total_Price__c : ''}
																									</div>
																								</td>
																							</tr>
																						</tbody>
																					</table>
																				</td>
																			</tr>
																			<aura:set attribute="else">
																				<aura:if isTrue="{!itinerary.record.attributes.type == 'Freight__c'}">
																					<aura:iteration items="{!itinerary.relatedRecords}" var="subTrip">
																						<aura:if isTrue="{!!empty(subTrip.FreightEquipments__r)}">
																							<tr>
																								<td>
																									<table class="slds-table slds-table_cell-buffer" style="border-top: 1px solid #eaeaea">
																										<thead>
																											<tr class="slds-line-height_reset">
																												<th width="33.3%" scope="col">
																													<div class="slds-truncate" title="PICK-UP">PICK-UP</div>
																												</th>
																												<th width="33.3%" scope="col">
																													<div class="slds-truncate" title="DROP-OFF">DROP-OFF</div>
																												</th>
																												<th width="33.3%" scope="col">
																													<div class="slds-truncate" title="FREIGHT TRUCK SQ FT">FREIGHT TRUCK SQ FT</div>
																												</th>
																											</tr>
																										</thead>
																										<tbody>
																											<aura:iteration items="{!subTrip.FreightEquipments__r.records}" var="travel">
																												<tr class="slds-hint-parent">
																													<td data-label="PICK-UP">
																														<div
																															class="slds-truncate"
																															title="{!(!empty(travel.Location_Pick_up__c) ? travel.Location_Pick_up__c + ' - ' : '') + (!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c + ' | ' : '') + (!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : '')}"
																														>
																															<aura:if isTrue="{!!empty(travel.Location_Pick_up__c)}"
																																>{!travel.Location_Pick_up__c}<br /></aura:if
																															>{!(!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c + ' | ' :
																															'') + (!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c
																															: '')}
																														</div>
																													</td>
																													<td data-label="DROP-OFF">
																														<div
																															class="slds-truncate"
																															title="{!(!empty(travel.Location_Drop_off__c) ? travel.Location_Drop_off__c + ' - ' : '') + (!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c + ' | ' : '') + (!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : '')}"
																														>
																															<aura:if isTrue="{!!empty(travel.Location_Drop_off__c)}"
																																>{!travel.Location_Drop_off__c}<br /></aura:if
																															>{!(!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c + ' | ' : '') +
																															(!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : '')}
																														</div>
																													</td>
																													<td data-label="FREIGHT TRUCK SQ FT">
																														<div
																															class="slds-truncate"
																															title="{!!empty(travel.Freight_Truck_Sq_Ft__c) ? travel.Freight_Truck_Sq_Ft__c : ''}"
																														>
																															{!!empty(travel.Freight_Truck_Sq_Ft__c) ? travel.Freight_Truck_Sq_Ft__c : ''}
																														</div>
																													</td>
																												</tr>
																											</aura:iteration>
																										</tbody>
																									</table>
																								</td>
																							</tr>
																						</aura:if>
																						<aura:if isTrue="{!!empty(itinerary.record.FreightSubTrips__r)}">
																							<tr>
																								<td>
																									<table class="slds-table slds-table_cell-buffer">
																										<tbody>
																											<aura:iteration items="{!itinerary.record.FreightSubTrips__r.records}" var="vehicle">
																												<tr class="slds-hint-parent">
																													<td width="10%">
																														<div
																															class="slds-truncate"
																															title="{!!empty(vehicle.Equipment__c) ? vehicle.Equipment__c : ''}"
																														>
																															<strong>{!!empty(vehicle.Equipment__c) ? vehicle.Equipment__c : ''}</strong>
																														</div>
																													</td>
																													<td width="60%">
																														<div
																															class="slds-truncate"
																															title="{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') + (!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') + (!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '') + (!empty(vehicle.Freight_Truck_Sq_Ft__c) ? ' | ' + vehicle.Freight_Truck_Sq_Ft__c : '')}"
																														>
																															{!(!empty(vehicle.Vehicle_Type__c) ? vehicle.Vehicle_Type__c : '') +
																															(!empty(vehicle.Make_Model__c) ? ' | ' + vehicle.Make_Model__c : '') +
																															(!empty(vehicle.Year__c) ? ' ' + vehicle.Year__c : '') +
																															(!empty(vehicle.Freight_Truck_Sq_Ft__c) ? ' | ' +
																															vehicle.Freight_Truck_Sq_Ft__c : '')}
																														</div>
																													</td>
																													<td width="30%"></td>
																												</tr>
																											</aura:iteration>
																										</tbody>
																									</table>
																								</td>
																							</tr>
																						</aura:if>
																					</aura:iteration>
																					<tr>
																						<td>
																							<table
																								class="slds-table slds-table_cell-buffer"
																								style="border-top: 1px solid #eaeaea; border-bottom: 1px solid #eaeaea"
																							>
																								<tbody>
																									<tr class="slds-hint-parent">
																										<td width="40%"></td>
																										<td width="40%"></td>
																										<td width="20%">
																											<div class="slds-truncate">
																												<strong style="margin-right: 20px">TOTAL PRICE</strong
																												>{!!empty(itinerary.record.Total_Price__c) ? '$' + itinerary.record.Total_Price__c :
																												''}
																											</div>
																										</td>
																									</tr>
																								</tbody>
																							</table>
																						</td>
																					</tr>
																					<aura:set attribute="else">
																						<aura:if isTrue="{!itinerary.record.attributes.type == 'Air__c'}">
																							<aura:if isTrue="{!!empty(itinerary.record.Air_Segments__r)}">
																								<tr>
																									<td>
																										<table class="slds-table slds-table_cell-buffer" style="border-top: 1px solid #eaeaea">
																											<thead>
																												<tr class="slds-line-height_reset">
																													<th width="33.3%" scope="col">
																														<div class="slds-truncate" title="DEPART">DEPART</div>
																													</th>
																													<th width="33.3%" scope="col">
																														<div class="slds-truncate" title="DROP-OFF">DROP-OFF</div>
																													</th>
																													<th width="33.3%" scope="col">
																														<div class="slds-truncate" title="FLIGHT DESCRIPTION">FLIGHT DESCRIPTION</div>
																													</th>
																												</tr>
																											</thead>
																											<tbody>
																												<aura:iteration items="{!itinerary.record.Air_Segments__r.records}" var="segment">
																													<tr class="slds-hint-parent">
																														<td data-label="DEPART">
																															<div
																																class="slds-truncate"
																																title="{!(!empty(segment.Departure_City__r) &amp;&amp; !empty(segment.Departure_City__r.City__r) ? ((!empty(segment.Departure_City__r.City__r.City__c) ? segment.Departure_City__r.City__r.City__c : '') + (!empty(segment.Departure_City__r.City__r.State__c) ? ', ' + segment.Departure_City__r.City__r.State__c : '')) : '') + (!empty(segment.Departure_City__r) ?  ' - ' + segment.Departure_City__r.Name : '') + (!empty(segment.Departure_Date_Text__c) ? ' - ' + segment.Departure_Date_Text__c : '')}"
																															>
																																{!(!empty(segment.Departure_City__r) &amp;&amp;
																																!empty(segment.Departure_City__r.City__r) ?
																																((!empty(segment.Departure_City__r.City__r.City__c) ?
																																segment.Departure_City__r.City__r.City__c : '') +
																																(!empty(segment.Departure_City__r.City__r.State__c) ? ', ' +
																																segment.Departure_City__r.City__r.State__c : '')) : '')}<br />{!(!empty(segment.Departure_City__r)
																																? segment.Departure_City__r.Name : '')}<br />{!(!empty(segment.Departure_Date_Text__c)
																																? segment.Departure_Date_Text__c + ' | ' : '') +
																																(!empty(segment.Dep_Time_Text__c) ? segment.Dep_Time_Text__c : '')}
																															</div>
																														</td>
																														<td data-label="DROP-OFF">
																															<div
																																class="slds-truncate"
																																title="{!(!empty(segment.Arrival_City__r) &amp;&amp; !empty(segment.Arrival_City__r.City__r) ? ((!empty(segment.Arrival_City__r.City__r.City__c) ? segment.Arrival_City__r.City__r.City__c : '') + (!empty(segment.Arrival_City__r.City__r.State__c) ? ', ' + segment.Arrival_City__r.City__r.State__c : '')) : '') + (!empty(segment.Arrival_City__r) ?  ' - ' + segment.Arrival_City__r.Name : '') + (!empty(segment.Arrival_Date_Text__c) ? ' - ' + segment.Arrival_Date_Text__c : '')}"
																															>
																																{!(!empty(segment.Arrival_City__r) &amp;&amp;
																																!empty(segment.Arrival_City__r.City__r) ?
																																((!empty(segment.Arrival_City__r.City__r.City__c) ?
																																segment.Arrival_City__r.City__r.City__c : '') +
																																(!empty(segment.Arrival_City__r.City__r.State__c) ? ', ' +
																																segment.Arrival_City__r.City__r.State__c : '')) : '')}<br />{!(!empty(segment.Arrival_City__r)
																																? segment.Arrival_City__r.Name : '')}<br />{!(!empty(segment.Arrival_Date_Text__c)
																																? segment.Arrival_Date_Text__c + ' | ' : '') +
																																(!empty(segment.Arr_Time_Text__c) ? segment.Arr_Time_Text__c : '')}
																															</div>
																														</td>
																														<td data-label="FLIGHT DESCRIPTION">
																															{!(!empty(segment.Flight_Duration_hrs__c) ? segment.Flight_Duration_hrs__c +
																															'hr ' : '') + (!empty(segment.Flight_Duration_Mins__c) ?
																															segment.Flight_Duration_Mins__c + 'min ' : '') +
																															(!empty(segment.Number_of_Seats__c) ? ' | ' + segment.Number_of_Seats__c + '
																															seats ' : '') + (!empty(segment.Equip_Type__c) ? ' | ' + segment.Equip_Type__c
																															: '')}
																														</td>
																													</tr>
																												</aura:iteration>
																											</tbody>
																										</table>
																									</td>
																								</tr>
																							</aura:if>
																							<tr>
																								<td>
																									<table
																										class="slds-table slds-table_cell-buffer"
																										style="border-top: 1px solid #eaeaea; border-bottom: 1px solid #eaeaea"
																									>
																										<tbody>
																											<tr class="slds-hint-parent">
																												<td width="40%"></td>
																												<td width="40%"></td>
																												<td width="20%">
																													<div class="slds-truncate">
																														<strong style="margin-right: 20px">PRICE PER TICKET</strong
																														>{!!empty(itinerary.record.Total_Price__c) ? '$' +
																														itinerary.record.Total_Price__c : ''}
																													</div>
																												</td>
																											</tr>
																										</tbody>
																									</table>
																								</td>
																							</tr>
																						</aura:if>
																					</aura:set>
																				</aura:if>
																			</aura:set>
																		</aura:if>
																	</aura:set>
																</aura:if>
															</tbody>
														</table>
													</div>
												</div>
											</div>
										</div>
										<footer class="slds-grid slds-gutters slds-wrap">
											<div class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12"></div>
											<div
												class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12 itinerary_buttons"
												data-servicetype="{!itinerary.record.attributes.type}"
												data-serviceid="{!itinerary.record.Id}"
												data-servicedateinandout="{!itinerary.record.attributes.type == 'Housing__c' ? itinerary.record.Date_In_Text__c + (!empty(itinerary.record.Date_Out_Text__c) ? ' - ' + itinerary.record.Date_Out_Text__c : '') : itinerary.record.attributes.type == 'Ground__c' ? itinerary.record.Start_Date_Text__c + (!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') : itinerary.record.attributes.type == 'Freight__c' ? itinerary.record.Start_Date_Text__c + (!empty(itinerary.record.End_Date_Text__c) ? ' - ' + itinerary.record.End_Date_Text__c : '') : itinerary.record.attributes.type == 'Air__c' ? itinerary.record.Departure_Date_Text__c + (!empty(itinerary.record.Return_Date_Text__c) ? ' - ' + itinerary.record.Return_Date_Text__c : '') : ''}"
												data-servicecityname="{!itinerary.record.attributes.type == 'Housing__c' ? (!empty(itinerary.record.City__r) ? ((!empty(itinerary.record.City__r.City__c) ? itinerary.record.City__r.City__c : '') + (!empty(itinerary.record.City__r.State__c) ? ', ' + itinerary.record.City__r.State__c : '')) : '') : itinerary.record.attributes.type == 'Ground__c' ? (!empty(itinerary.record.Start_city__r) ? ((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') + (!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') : itinerary.record.attributes.type == 'Freight__c' ? (!empty(itinerary.record.Start_city__r) ? ((!empty(itinerary.record.Start_city__r.City__c) ? itinerary.record.Start_city__r.City__c : '') + (!empty(itinerary.record.Start_city__r.State__c) ? ', ' + itinerary.record.Start_city__r.State__c : '')) : '') : itinerary.record.attributes.type == 'Air__c' ? (!empty(itinerary.record.Departure_City__r) &amp;&amp; !empty(itinerary.record.Departure_City__r.City__r) ? ((!empty(itinerary.record.Departure_City__r.City__r.City__c) ? itinerary.record.Departure_City__r.City__r.City__c : '') + (!empty(itinerary.record.Departure_City__r.City__r.State__c) ? ', ' + itinerary.record.Departure_City__r.City__r.State__c : '')) : '') : ''}"
											>
                                                <!-- Fix By Clay Dev #178056511-->
												<aura:if
													isTrue="{!or(and(itinerary.record.attributes.type == 'Housing__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Decision' || itinerary.record.Status_CC__c == 'Pending Client Signature'), and(itinerary.record.attributes.type == 'Freight__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature'), and(itinerary.record.attributes.type == 'Air__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature'), and(itinerary.record.attributes.type == 'Ground__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature') )}"
												>
													<button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleOptions}">
														VIEW OPTIONS
													</button>
													<!--<button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleOptions}">REVIEW CONTRACT</button>-->
												</aura:if>
												<aura:if
													isTrue="{!or(and(itinerary.record.attributes.type == 'Housing__c',itinerary.record.Status_CC__c == 'Contracted' || itinerary.record.Status_CC__c == 'In Contracting' || itinerary.record.Status_CC__c == 'Pending Client Signature'),and(itinerary.record.attributes.type == 'Ground__c', itinerary.record.Status_Ground__c == 'Contracted'), and(itinerary.record.attributes.type == 'Freight__c', itinerary.record.Status__c == 'Contracted'), and(itinerary.record.attributes.type == 'Air__c', itinerary.record.Status__c == 'Contracted'))}"
												>
													<!-- remove documents button <button class="slds-button slds-button_brand formButtonBrandLight" onclick="{!c.handleDocuments}">
														DOCUMENTS
													</button>-->
												</aura:if>
											</div>
										</footer>
									</div>
								</article>
							</aura:iteration>
						</aura:iteration>
					</section>
				</div>
			</div>
		</div>
	</div>
</aura:component>
```

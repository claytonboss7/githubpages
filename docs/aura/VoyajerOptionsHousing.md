---
layout: default
title: VoyajerOptionsHousing
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsHousing
## Fields
### VoyajerOptionsHousingController

```
({
  doInit: function (component, event, helper) {
    var callToParent = component.getEvent("callToParent");
    console.log('source:: ' + component.get('v.source'));
    if (component.get('v.source') === 'preview') {
      callToParent.setParam("action", "loadOptionsHousingPreview");
    } else {
      callToParent.setParam("action", "loadOptionsHousing");
    }
    callToParent.fire();
  },
  submitSelectedOptions: function (cmp, event, helper) {
    console.log('submit');
    cmp.set("v.mainContent","optionsSubmitMultiple");

  },
  handleMultiSelect: function (cmp, event, helper) {
    var list = cmp.get("v.bidOptionsFiltered");
    var isSelectionMade = false;
    var bidsSelected = [];
    var okToAdvance = true; 
    list.forEach(function (bid) {
      if (bid.isMultiContract === true) {
        bidsSelected.push(bid);
        isSelectionMade = true;
      }
      if (bid.record.Status__c  === 'Decision' || bid.record.Status__c  === 'In Contracting' || bid.record.Status__c  === 'Contracted' || bid.record.Status__c  === 'Pending Client Signature'){
          okToAdvance = false;
      }
    });
    if(okToAdvance) {
        cmp.set('v.isSelectionMade', isSelectionMade);
        console.log(cmp.get('v.isSelectionMade'));
        if (isSelectionMade){
          cmp.set('v.displaySubmit', true);
        } else {
          cmp.set('v.displaySubmit', false)
        }
        cmp.set('v.bidsSelected', bidsSelected);
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","refreshBidsSelected");
        callToParent.setParam('data', bidsSelected);
        callToParent.fire(); 
    } else {
        cmp.find("review-select-checkbox").forEach(function(cmp) {
            cmp.set("v.checked", false);
        });
        cmp.set('v.openSelectOptionsAlert', true);
    }
  },
  handleShowMessages : function(component, event, helper) {
    component.set('v.showCommunityNote', true);
    var callToParent = component.getEvent("callToParent");
    callToParent.setParam("action","showMessages");
    callToParent.fire();    
  },
  loadTable: function (component, event, helper) {
    console.log("# loadTable()");
    component.find("filterByPrice").set("v.value", "RRRecomendation");
    component.find("filterByDistance").set("v.value", "all");
    component.find("filterByAmenities").set("v.value", "all");
    var bids = component.get("v.bidOptions");
    var bidsToShow = [];
    var bidOptionsHidden = [];
    bids.forEach((item) => {
      if (!item.record.Include_in_option_cover_sheet__c) bidsToShow.push(item);
      else bidOptionsHidden.push(item);
    });
    component.set("v.bidOptionsHidden", bidOptionsHidden);
    helper.filterMethod(component, bidsToShow);
  },
  openOptionDetail: function (component, event, helper) {
    var bidindex = event.currentTarget.dataset.bidindex;
    var list = component.get("v.bidOptionsFiltered");
    component.set("v.optionDetailRecordId", bidindex);
    component.set("v.optionDetailRecordIdReal", parseInt(bidindex) + 1);
    component.set("v.bidOptionsSize", list.length);
    component.set("v.mainContent", "optionsHousingDetail");
  },
  openReviewSubmit: function (component, event, helper) {
    var theURL = window.location.href;
    var isPreview = theURL.includes('VoyajerPreviewApp');
    var okToAdvance = true;

    if (isPreview){
      okToAdvance = false;
      component.set('v.modalTitle', 'Preview Only');
      component.set('v.communityNotes', 'Selection not Allowed in Preview');
    } else if (!isPreview){
      var bidindex = event.currentTarget.dataset.bidindex;
      var recordId = event.currentTarget.dataset.recordid;
      var ismulticontract = event.currentTarget.dataset.ismulticontract === null ? false : event.currentTarget.dataset.ismulticontract;
      var list = component.get("v.bidOptionsFiltered");
      var indexActual;
      var index = 0;
      console.log('first round of logic done ismulticontract :: ' + ismulticontract);

  
      list.forEach(function (bid) {
        console.log(JSON.stringify(bid));
        if (bid.recordId == recordId) {

          indexActual = index;
        }
        index++;
        if (!bid.isEvent){
          console.log('inside not multi');
          if (bid.record.Status__c  === 'Decision' || bid.record.Status__c  === 'In Contracting' || bid.record.Status__c  === 'Contracted' || bid.record.Status__c  === 'Pending Client Signature'){
            console.log('inside status contracted');
            okToAdvance = false;
          }
        }
      });
  
      if ((list[indexActual].record.Status__c === "Decision" || list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
        okToAdvance = false;
      }
    }


    if (okToAdvance) {
      component.set("v.optionDetailRecordId",bidindex);
      component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
      component.set("v.bidOptionsSize",list.length);
      component.set("v.mainContent","optionsHousingReviewSubmit");

    } else {
      component.set('v.openSelectOptionsAlert', true);
    }
  },
  
  handleCompare: function (component, event, helper) {
    var bidsSelected = [];
    component.get("v.bidOptions").forEach(function (bid) {
      if (bid.isCompared) bidsSelected.push(bid);
    });
    //console.log(bidsSelected);
    component.set("v.compareList", bidsSelected);
    component.set("v.mainContent", "optionsHousingCompare");
  },
  handleBack: function (component, event, helper) {
    component.set("v.mainContent", "overview");
  },
  handleFilter: function (component, event, helper) {
    var bids = component.get("v.bidOptions");
    var bidsToShow = [];
    bids.forEach((item) => {
      if (!item.record.Include_in_option_cover_sheet__c) bidsToShow.push(item);
    });
    helper.filterMethod(component, bidsToShow);
  },
  handleShowOtherProperties: function (component, event, helper) {
    component.set("v.openOtherProperties", true);
  },
  handleCloseModal: function (component, event, helper) {
    component.set("v.openSelectOptionsAlert", false);
    component.set("v.openOtherProperties", false);
  },
  generatePDF: function (component, event, helper) {
    window.open("/apex/HousingOptionsPdf?id=" + component.get("v.housingId"));
  }
});
```
### VoyajerOptionsHousing

```
.THIS .label-hidden > label {
    display: none;
}

.THIS .optionBox {
    width: 32%;
    padding: 1.5em 2em 1.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: white;
    margin: 1.5em 1em 1.5em 0;
}

.THIS .optionBoxIcon {
    padding-bottom: 1em;
}

.THIS .optionBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .optionBoxName {
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

.THIS .optionBoxDescription{
    margin-bottom: 1em;
}

.THIS .optionBoxDescription p {
    font-size: 12px;
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    margin-bottom: 0.5em;
    min-height: 1.5em;
}

.THIS .room-type{
    font-weight: bold;
    font-size: 1.4em;
}

.THIS .pageContentForm.header{
    margin-bottom:10px;
}

.THIS .pageContentOptions{
    display: flex;
    flex-flow: wrap;
}

.THIS .info-bluelight{
    color: #00b4ff;
    font-weight: bold;
    text-transform: uppercase;
    font-size: 1.2em;
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

.THIS .btn-option{
    height: 100%;
    text-align: center;
    font-weight: bold;
    font-size: 12px;
    color: grey;
    cursor: pointer;
}

.THIS .btn-option-white{
    background-color: white;
}

.THIS .btn-option-white:hover{
    background-color: #f4f6f9;
}

.THIS .btn-option-blue{
    background-color: #0065ff;
    color: white;
}

.THIS .btn-option-blue:hover{
    background-color: #085ee2;
}


/*--------------------
-----Bid------
----------------------*/

.THIS .slds-section__content{
    overflow-x: auto !important;
}

.THIS .slds-card-bid{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    transition: transform 0.1s ease;
}

.THIS .slds-card-bid:hover{
    -webkit-transform: scale(1.05);
    -moz-transform: scale(1.05);
    -o-transform: scale(1.05);
    transform: scale(1.05);
}

.THIS .slds-card-bid_header{
    padding: 1rem 1em 0.5em 2em;;
    background-color: white;
}

.THIS .slds-card-bid_header h3{
    font-weight: bold;
}

.THIS .slds-card-bid-content{
    background-color: white;
    overflow-y: auto;
    padding: 0 16px 16px 16px;
    word-wrap: break-word;/*warp*/
}

.THIS .slds-card-bid-footer{
    background-color: white;
}

.THIS .slds-card-bid-footer > .slds-grid{
    height: 45px;
}

/*--------------------
-----Inputs------
----------------------*/

.THIS .slds-form-element-filter > .slds-form-element__label{
    display: none;
}

.THIS .slds-checkbox_add-button{
    margin-top: 5px;
    margin-right: 5px;
}


.THIS .slds-checkbox_add-button .slds-checkbox_faux{
    width: 1.5rem;
    height: 1.5rem;
}

.THIS .slds-checkbox_add-button .slds-checkbox_faux:after,
.THIS .slds-checkbox_add-button .slds-checkbox_faux:before{
    background-color: white !important;
}

.THIS .recordTable {
    border: none;
}

.THIS .tableRow > div {
    align-items: center;
    display: flex;
    flex: 1;
    padding: 1em;
}
```
### VoyajerOptionsHousingHelper

```
({
	filterMethod : function(component, bids) {
        console.log('# filterMethod');
        
        var bidsFiltered = [];
        var officePreference = component.get("v.officePreference");
        var filterByPrice = component.find("filterByPrice").get("v.value");
        var filterByDistance = component.find("filterByDistance").get("v.value");
        var filterByAmenities = component.find("filterByAmenities").get("v.value");
        
        function isEmpty(obj) {
            for(var prop in obj) if(obj.hasOwnProperty(prop)) return false;
            return true;
        }
        
        //order...
		if(filterByPrice == 'RRRecomendation') bids.sort((a, b) => parseFloat(a.optionNumber) - parseFloat(b.optionNumber));
        else if(filterByPrice == 'LowToHigh') bids.sort((a, b) => parseFloat(a.avgrate) - parseFloat(b.avgrate));
        else if(filterByPrice == 'HighToLow') bids.sort((a, b) => parseFloat(b.avgrate) - parseFloat(a.avgrate));
        
        var addItem_flag1 = false;
        var addItem_flag2 = false;
        for(var i = 0; i < bids.length; i++) {
            var bid = bids[i];
            if(!isEmpty(bid.rateDetails[0])) {
                var revenue = bid.rateDetails[0];
                if(revenue.hasOwnProperty("CurrencyIsoCode")) {
                    //console.log(revenue.CurrencyIsoCode);
                } else {
                    //console.log(officePreference);
                }
            } else {
                //console.log(officePreference);
            }
            addItem_flag1 = false;
            addItem_flag2 = false;
            
            //filterByDistance
            //console.log("# filterByDistance = " + filterByDistance);
            if(filterByDistance == "all") addItem_flag1 = true;
            else if(filterByDistance == 'w0.5' && parseFloat(bid.distance) <= 0.5) addItem_flag1 = true;
                else if(filterByDistance == '0.5-5' && parseFloat(bid.distance) >= 0.5 && parseFloat(bid.distance) <= 5) addItem_flag1 = true;
                    else if(filterByDistance == '5-10' && parseFloat(bid.distance) >= 5 && parseFloat(bid.distance) <= 10) addItem_flag1 = true;
                        else if(filterByDistance == '10+' && parseFloat(bid.distance) >= 10) addItem_flag1 = true;
            
            //filterByAmenities
            //console.log("# filterByAmenities = " + filterByAmenities);
            if(filterByAmenities == "all") addItem_flag2 = true;
            else if(filterByAmenities == 'Wireless' && bid.connection == 'Wireless') addItem_flag2 = true;
                else if(filterByAmenities == 'Wireless and Wired' && bid.connection == 'Wireless and Wired') addItem_flag2 = true;
                    else if(filterByAmenities == 'Pool' && bid.pool == 'Yes') addItem_flag2 = true;
                        else if(filterByAmenities == 'Pet Allowed' && bid.pets_allowed == 'Yes') addItem_flag2 = true;
                            else if(filterByAmenities == 'Hotel Shuttle' && bid.hotel_shuttle == 'Yes') addItem_flag2 = true;
            
            if(addItem_flag1 && addItem_flag2) bidsFiltered.push(bid);
        }
        component.set("v.bidOptionsFiltered", bidsFiltered);
    }
})
```
### VoyajerOptionsHousing

```
<aura:component
	implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction"
	access="global"
	controller="VoyajerController"
>
	<aura:attribute type="String" name="communityNotes" default="" />
	<aura:attribute type="String" name="modalTitle" default="" />
	<aura:attribute type="Boolean" name="showCommunityNote" default="false" />
	<aura:attribute type="Boolean" name="displaySubmit" default="false" />
	<aura:attribute type="Boolean" name="isSelectionMade" default="false" />
	<aura:attribute type="String" name="housingId" />
	<aura:attribute type="String" name="source" default="" />
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="productionName" />
	<aura:attribute type="String" name="housingType" />
	<aura:attribute type="String" name="officePreference" />
	<aura:attribute type="String" name="userProfile" />
	<aura:attribute type="Boolean" name="openOtherProperties" default="false" />
	<aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
	<aura:attribute type="Object" name="serviceData" />
	<aura:attribute type="List" name="bidOptions" />
	<aura:attribute type="List" name="bidOptionsFiltered" />
	<aura:attribute type="List" name="bidOptionsHidden" />
	<aura:attribute type="List" name="bidsSelected" />
	<aura:attribute type="Integer" name="optionDetailRecordId" />
	<aura:attribute type="Integer" name="optionDetailRecordIdReal" />
	<aura:attribute type="Integer" name="bidOptionsSize" />
	<aura:attribute type="List" name="compareList" />
	<aura:attribute name="startDate" type="String" />
	<aura:attribute name="endDate" type="String" />
	<aura:attribute name="selectedLookupId" type="String" />
    <aura:attribute name="selectedPillText" type="String" />
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
	<aura:handler name="change" value="{!v.bidOptions}" action="{!c.loadTable}" />
	<aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
	<div>
		<div class="pageContent">

			<div class="pageContentSpaces">
				<div class="page-section">
					<div class="page-header">
						<h1 class="page-header-title">
							<i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em"></i>
							Options
						</h1>
						<lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
					</div>
				</div>
				<div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb">
					<div class="page-section">
						<div class="slds-grid slds-gutters slds-wrap">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
								<h3>
									<strong style="color: black">{!v.productionName}</strong>
								</h3>
								<p style="margin-right: 0.5em; font-weight: bold; color: #00b4ff">
									{!v.serviceData.cityName} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}
								</p>
								<p style="margin-right: 0.5em; font-weight: bold; color: #00b4ff">{!v.serviceData.venueName}</p>
							</div>
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right">
								<lightning:layout horizontalAlign="end">
									<lightning:layoutItem padding="around-medium">
										<aura:if isTrue="{!if(v.communityNotes!='',true,false)}">
											<lightning:button
												label="View Messages"
												variant="brand"
												iconName="utility:people"
												iconPosition="left"
												class="formButtonBrandLight"
												onclick="{!c.handleShowMessages}"
											/>
										</aura:if>
									</lightning:layoutItem>
									<aura:if isTrue="{!or(v.housingType=='Corporate_Housing',empty(v.serviceData.releaseDate))}">
										<lightning:layoutItem>
											<div class="box-decisionBy">
												Units Not <br/>
												Being Held
											</div>
										</lightning:layoutItem>
										<aura:set attribute="else"> 									
											<lightning:layoutItem>
											<div class="box-decisionBy">
												DECISION BY <br />
												{!v.serviceData.releaseDate}
											</div>
										</lightning:layoutItem></aura:set>
									</aura:if>
								</lightning:layout>
							</div>
						</div>
					</div>
				</div>
				<div class="pageContentDashboard pageContentDashboard-grey">
					<div class="slds-grid slds-wrap">
						<div class="slds-col slds-size_1-of-1">
							<div class="slds-grid slds-wrap slds-grid_vertical-align-center">
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12">
									Filter by
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_3-of-12 slds-large-size_3-of-12">
									<lightning:select
										label="Filter"
										aura:id="filterByPrice"
										variant="label-hidden"
										class="slds-form-element-filter label-hidden"
										onchange="{!c.handleFilter}"
									>
										<option value="RRRecomendation" selected="true">Road Rebel Recomendation</option>
										<option value="LowToHigh">Price Low to High</option>
										<option value="HighToLow">Price High to Low</option>
									</lightning:select>
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_2-of-12 slds-large-size_2-of-12">
									<lightning:select
										label="Filter"
										aura:id="filterByDistance"
										variant="label-hidden"
										class="slds-form-element-filter label-hidden"
										onchange="{!c.handleFilter}"
									>
										<option value="all" selected="true">Distance to Venue</option>
										<option value="w0.5">Walking (0.5 miles)</option>
										<option value="0.5-5">0.5- 5 Miles</option>
										<option value="5-10">5 - 10 Miles</option>
										<option value="10+">10+ Miles</option>
									</lightning:select>
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_2-of-12 slds-large-size_2-of-12">
									<lightning:select
										label="Filter"
										aura:id="filterByAmenities"
										variant="label-hidden"
										class="slds-form-element-filter label-hidden"
										onchange="{!c.handleFilter}"
									>
										<option value="all">Filter by Amenities</option>
										<option value="Wireless">Wireless</option>
										<option value="Wireless and Wired">Wireless and Wired</option>
										<option value="Pool">Pool</option>
										<option value="Pet Allowed">Pet Allowed</option>
										<option value="Hotel Shuttle">Hotel Shuttle</option>
									</lightning:select>
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
									<lightning:button label="Update" variant="brand" class="btn btn-bluelight" onclick="{!c.doInit}" />
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
									<lightning:button label="Clear" variant="neutral" class="btn btn-white" onclick="{!c.loadTable}" />
								</div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
                                    <lightning:button label="Compare" variant="brand" class="btn" onclick="{!c.handleCompare}" />
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small" style="margin: 0; text-align: right">
									<lightning:button label="PDF" variant="brand" class="btn" onclick="{!c.generatePDF}" />
								</div>
							</div>
						</div>
					</div>
				</div>
				<div class="pageContentDashboard pageContentDashboard-grey" style="padding-top: 0">
					<section class="slds-grid slds-gutters slds-wrap">
						<aura:iteration items="{!v.bidOptionsFiltered}" var="bid" indexVar="bidIndex">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3">
								<article class="slds-card-bid">
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<header class="slds-card-bid_header">
												<div class="">
													<h3 style="text-align: center">{!bid.vendor}</h3>
													<aura:if isTrue="{!not(empty(bid.provider))}">
														<p style="font-size: 1rem; text-align: center">Provider: {!bid.provider}</p>
													</aura:if>
												</div>
											</header>
										</div>
									</div>
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<div class="slds-card-bid-content">
												<div class="slds-grid slds-wrap">
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em">
														<aura:iteration items="{!bid.stars}" var="star">
															<i class="fas fa-star" style="color: #ffa000"></i>
														</aura:iteration>
													</div>
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; font-size: 12px">
														{!if(and(bid.dx_to_venue != null,bid.dx_to_venue != ''),bid.dx_to_venue,'&nbsp;')}
													</div>
													<div
														class="slds-col slds-size_1-of-1"
														style="margin-bottom: 0.5em; font-size: 12px; color: #00b4ff; font-weight: bold"
													>
														{!if(and(bid.physical != null,bid.physical != ''),bid.physical,'&nbsp;')}
													</div>
													<div
														class="slds-col slds-size_1-of-1"
														style="margin-bottom: 0.5em; font-size: 12px; color: #00b4ff; font-weight: bold"
													>
														<aura:if isTrue="{!and(bid.website != null, bid.website != '')}">
															<lightning:formattedText linkify="true" value="{!bid.website}" />
														</aura:if>
													</div>
													<!-- Fix By Clay Dev 31 Jan, 2021 #176367796
                                                    <div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; font-size: 12px">
														{!if(and(bid.phone != null,bid.phone != ''),bid.phone,'&nbsp;')}
													</div> -->
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; min-height: 20px">
														<i
															class="fas fa-wifi"
															style="{!if(or(bid.connection == 'Wireless',bid.connection == 'Wireless and Wired'),'color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
														<i
															class="fas fa-swimming-pool"
															style="{!if(bid.pool == 'Yes','color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
														<i
															class="fas fa-paw"
															style="{!if(bid.pets_allowed == 'Yes','color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
														<i
															class="fas fa-bus"
															style="{!if(bid.hotel_shuttle == 'Yes','color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
													</div>
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; font-size: 12px; min-height: 4em">
														<span style="color: #00b4ff">CONCESSIONS</span>
														<ul class="slds-list_dotted">
															<aura:iteration items="{!bid.concessions}" var="concession">
																<!--<li style="list-style: disc;">{!concession.Concession_Provided__c}</li>-->
																<li style="list-style: disc">
																	<aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
																		{!concession.Concessions_Requested__c+' '+concession.Concession_Provided__c}
																		<aura:set attribute="else"> {!concession.Concession_Provided__c} </aura:set>
																	</aura:if>
																</li>
															</aura:iteration>
														</ul>
													</div>
													<div
														class="slds-col slds-size_1-of-1"
														style="margin-top: 0.5em; margin-bottom: 0.5em; font-size: 12px; min-height: 4em"
													>
														<div class="slds-grid slds-wrap">
															<aura:iteration items="{!bid.roomTypes}" var="roomtype">
																<div class="slds-size_1-of-1 slds-medium-size_2-of-3 slds-large-size_2-of-3">
																	<span style="font-size: 1.2em">{!roomtype.Units__c}</span>
																	-
																	<span style="font-size: 1.2em">{!roomtype.Unit_Type__c}</span>
																</div>
																<div class="slds-size_1-of-1 slds-medium-size_1-of-3 slds-large-size_1-of-3" style="text-align: right">
																	<span class="room-type">
																		<lightning:formattedNumber
																			value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}"
																			style="currency"
																			currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}"
																			currencyDisplayAs="symbol"
																		/>
																		<!--${!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}-->
																	</span>
																</div>
															</aura:iteration>
														</div>
													</div>
												</div>
												<div class="slds-grid slds-gutters slds-wrap slds-deviations" style="text-align: center; padding: 1em 0 0 0">
													<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
														<div style="border-top: 1px solid #eaeaea; font-style: italic; color: #0065ff; padding: 1em 1em 0em 1em">
															<span>
																Weighted Avg Rate:
																<lightning:formattedNumber
																	value="{!bid.avgrate}"
																	style="currency"
																	currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}"
																	currencyDisplayAs="symbol"
																/>
															</span>
															<br/>
															<span>
																Total Cost:
																<lightning:formattedNumber
																	value="{!bid.totalrate}"
																	style="currency"
																	currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}"
																	currencyDisplayAs="symbol"
																/>
															</span>
															<br />

															<!--Weighted Avg Rate: ${!bid.avgrate}-->
														</div>
													</div>
												</div>
											</div>
										</div>
									</div>
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<footer class="slds-card-bid-footer">
												<div class="slds-grid">
													<div
														class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
														style="border-left: 1px solid #eaeaea"
													>
														<lightning:input type="checkbox-button" label="COMPARE" checked="{!bid.isCompared}" /><span>COMPARE</span>
													</div>
													<div
														class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
														style="border-left: 1px solid #eaeaea; color: #00b4ff"
														data-bidindex="{!bidIndex}"
														onclick="{!c.openOptionDetail}"
													>
														DETAILS
													</div>
                                                    <!-- Fix By Clay Dev #178056511-->
                                                        <aura:if isTrue="{!bid.isEvent}">
                                                            <div
                                                            class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
                                                            style="border-left: 1px solid #eaeaea">
                                                            <lightning:input type="checkbox-button" aura:id="review-select-checkbox" label="SELECT" checked="{!bid.isMultiContract}" onchange="{!c.handleMultiSelect}"/><span>SELECT</span>
                                                        </div>
                                                        <aura:set attribute="else">
                                                            <div
                                                            class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-blue"
                                                            style="border-left: 1px solid #eaeaea"
                                                            data-bidindex="{!bidIndex}"
                                                            data-recordId="{!bid.record.Id}"
                                                            onclick="{!c.openReviewSubmit}"
                                                        >
                                                            SELECT
                                                        </div>
                                                        </aura:set>
                                                    </aura:if>
												</div>
											</footer>
										</div>
									</div>
								</article>
							</div>
						</aura:iteration>
					</section>
					<aura:if isTrue="{!v.displaySubmit}">
						<div class="slds-grid slds-wrap">
							<div class="slds-col slds-size_1-of-1" style="margin-top: 2em; text-align: center">
								<lightning:button
									label="SUBMIT"
									variant="success"
									onclick="{!c.submitSelectedOptions}"
								/>
							</div>
						</div>
					</aura:if>
					<aura:if isTrue="{!!v.displaySubmit}">
					<div class="slds-grid slds-wrap">
						<div class="slds-col slds-size_1-of-1" style="margin-top: 2em; text-align: center">
							<lightning:button
								label="OTHERS PROPERTIES CONTACTED"
								variant="brand"
								class="formButtonBrandLight btn-custom"
								onclick="{!c.handleShowOtherProperties}"
							/>
						</div>
					</div>
					</aura:if>

				</div>
			</div>
			<aura:if isTrue="{!v.openOtherProperties}">
				<!--###### MODAL BOX Start######-->
				<section
					role="dialog"
					tabindex="-1"
					aria-labelledby="modal-heading-02"
					aria-modal="true"
					aria-describedby="modal-content-id-2"
					class="slds-modal slds-fade-in-open"
				>
					<div class="slds-modal__container">
						<!-- ###### MODAL BOX HEADER Start ######-->
						<header class="slds-modal__header" style="border-bottom: 0">
							<lightning:buttonIcon
								iconName="utility:close"
								alternativeText="close"
								variant="bare-inverse"
								class="slds-modal__close"
								onclick="{!c.handleCloseModal}"
							/>
							<h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate" style="color: #00b4ff">
								Additional Properties Contacted
							</h2>
						</header>
						<!--###### MODAL BOX BODY Part Start######-->
						<div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1" style="padding-top: 0">
							<aura:if isTrue="{!not(empty(v.bidOptionsHidden))}">
								<div class="recordTable tableList" style="padding: 0 1.5rem; margin: 0">
									<div class="tableRow">
										<div style="white-space: normal; text-align: left">
											<b>Property</b>
										</div>
										<div style="white-space: normal; text-align: left">
											<b>Notes</b>
										</div>
									</div>
									<aura:iteration items="{!v.bidOptionsHidden}" var="bidHidden">
										<div class="tableRow">
											<div style="white-space: normal; text-align: left">{!bidHidden.vendor}</div>
											<div style="white-space: normal; text-align: left; color: red">
												<b>{!bidHidden.noBidReason}</b>
											</div>
											<!--Fix by Clay 22 Jan, 2021 : for User Story #176605416
											<aura:if isTrue="{!bidHidden.record.Status__c=='Sold Out / Not Bidding'}">
            										//<div style="white-space: normal; text-align: left; color: red;"><b>SOLD OUT</b></div>
												<aura:set attribute="else"> </aura:set>
											</aura:if>-->
										</div>
									</aura:iteration>
								</div>
								<aura:set attribute="else">
									<p style="text-align: center">Don’t have others Properties Contacted</p>
								</aura:set>
							</aura:if>
						</div>
					</div>
				</section>
				<div class="slds-backdrop slds-backdrop_open"></div>
				<!--######## MODAL BOX Part END Here ######-->
			</aura:if>
			<aura:if isTrue="{!v.openSelectOptionsAlert}">
				<c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}" />
			</aura:if>
		</div>
	</div>
	
	<aura:if isTrue="{!v.showCommunityNote}">
		<c:VoyajerOptionsModalSelectAlert
			modalTitleText="Message From Your Rebel"
			modalDetailText="{!v.communityNotes}"
			openSelectOptionsAlert="{!v.showCommunityNote}"
		/>
	</aura:if>

</aura:component>
```
### VoyajerOptionsHousing

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingController

```
({
  doInit: function (component, event, helper) {
    var callToParent = component.getEvent("callToParent");
    console.log('source:: ' + component.get('v.source'));
    if (component.get('v.source') === 'preview') {
      callToParent.setParam("action", "loadOptionsHousingPreview");
    } else {
      callToParent.setParam("action", "loadOptionsHousing");
    }
    callToParent.fire();
  },
  submitSelectedOptions: function (cmp, event, helper) {
    console.log('submit');
    cmp.set("v.mainContent","optionsSubmitMultiple");

  },
  handleMultiSelect: function (cmp, event, helper) {
    var list = cmp.get("v.bidOptionsFiltered");
    var isSelectionMade = false;
    var bidsSelected = [];
    var okToAdvance = true; 
    list.forEach(function (bid) {
      if (bid.isMultiContract === true) {
        bidsSelected.push(bid);
        isSelectionMade = true;
      }
      if (bid.record.Status__c  === 'Decision' || bid.record.Status__c  === 'In Contracting' || bid.record.Status__c  === 'Contracted' || bid.record.Status__c  === 'Pending Client Signature'){
          okToAdvance = false;
      }
    });
    if(okToAdvance) {
        cmp.set('v.isSelectionMade', isSelectionMade);
        console.log(cmp.get('v.isSelectionMade'));
        if (isSelectionMade){
          cmp.set('v.displaySubmit', true);
        } else {
          cmp.set('v.displaySubmit', false)
        }
        cmp.set('v.bidsSelected', bidsSelected);
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","refreshBidsSelected");
        callToParent.setParam('data', bidsSelected);
        callToParent.fire(); 
    } else {
        cmp.find("review-select-checkbox").forEach(function(cmp) {
            cmp.set("v.checked", false);
        });
        cmp.set('v.openSelectOptionsAlert', true);
    }
  },
  handleShowMessages : function(component, event, helper) {
    component.set('v.showCommunityNote', true);
    var callToParent = component.getEvent("callToParent");
    callToParent.setParam("action","showMessages");
    callToParent.fire();    
  },
  loadTable: function (component, event, helper) {
    console.log("# loadTable()");
    component.find("filterByPrice").set("v.value", "RRRecomendation");
    component.find("filterByDistance").set("v.value", "all");
    component.find("filterByAmenities").set("v.value", "all");
    var bids = component.get("v.bidOptions");
    var bidsToShow = [];
    var bidOptionsHidden = [];
    bids.forEach((item) => {
      if (!item.record.Include_in_option_cover_sheet__c) bidsToShow.push(item);
      else bidOptionsHidden.push(item);
    });
    component.set("v.bidOptionsHidden", bidOptionsHidden);
    helper.filterMethod(component, bidsToShow);
  },
  openOptionDetail: function (component, event, helper) {
    var bidindex = event.currentTarget.dataset.bidindex;
    var list = component.get("v.bidOptionsFiltered");
    component.set("v.optionDetailRecordId", bidindex);
    component.set("v.optionDetailRecordIdReal", parseInt(bidindex) + 1);
    component.set("v.bidOptionsSize", list.length);
    component.set("v.mainContent", "optionsHousingDetail");
  },
  openReviewSubmit: function (component, event, helper) {
    var theURL = window.location.href;
    var isPreview = theURL.includes('VoyajerPreviewApp');
    var okToAdvance = true;

    if (isPreview){
      okToAdvance = false;
      component.set('v.modalTitle', 'Preview Only');
      component.set('v.communityNotes', 'Selection not Allowed in Preview');
    } else if (!isPreview){
      var bidindex = event.currentTarget.dataset.bidindex;
      var recordId = event.currentTarget.dataset.recordid;
      var ismulticontract = event.currentTarget.dataset.ismulticontract === null ? false : event.currentTarget.dataset.ismulticontract;
      var list = component.get("v.bidOptionsFiltered");
      var indexActual;
      var index = 0;
      console.log('first round of logic done ismulticontract :: ' + ismulticontract);

  
      list.forEach(function (bid) {
        console.log(JSON.stringify(bid));
        if (bid.recordId == recordId) {

          indexActual = index;
        }
        index++;
        if (!bid.isEvent){
          console.log('inside not multi');
          if (bid.record.Status__c  === 'Decision' || bid.record.Status__c  === 'In Contracting' || bid.record.Status__c  === 'Contracted' || bid.record.Status__c  === 'Pending Client Signature'){
            console.log('inside status contracted');
            okToAdvance = false;
          }
        }
      });
  
      if ((list[indexActual].record.Status__c === "Decision" || list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
        okToAdvance = false;
      }
    }


    if (okToAdvance) {
      component.set("v.optionDetailRecordId",bidindex);
      component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
      component.set("v.bidOptionsSize",list.length);
      component.set("v.mainContent","optionsHousingReviewSubmit");

    } else {
      component.set('v.openSelectOptionsAlert', true);
    }
  },
  
  handleCompare: function (component, event, helper) {
    var bidsSelected = [];
    component.get("v.bidOptions").forEach(function (bid) {
      if (bid.isCompared) bidsSelected.push(bid);
    });
    //console.log(bidsSelected);
    component.set("v.compareList", bidsSelected);
    component.set("v.mainContent", "optionsHousingCompare");
  },
  handleBack: function (component, event, helper) {
    component.set("v.mainContent", "overview");
  },
  handleFilter: function (component, event, helper) {
    var bids = component.get("v.bidOptions");
    var bidsToShow = [];
    bids.forEach((item) => {
      if (!item.record.Include_in_option_cover_sheet__c) bidsToShow.push(item);
    });
    helper.filterMethod(component, bidsToShow);
  },
  handleShowOtherProperties: function (component, event, helper) {
    component.set("v.openOtherProperties", true);
  },
  handleCloseModal: function (component, event, helper) {
    component.set("v.openSelectOptionsAlert", false);
    component.set("v.openOtherProperties", false);
  },
  generatePDF: function (component, event, helper) {
    window.open("/apex/HousingOptionsPdf?id=" + component.get("v.housingId"));
  }
});
```
### VoyajerOptionsHousing

```
.THIS .label-hidden > label {
    display: none;
}

.THIS .optionBox {
    width: 32%;
    padding: 1.5em 2em 1.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: white;
    margin: 1.5em 1em 1.5em 0;
}

.THIS .optionBoxIcon {
    padding-bottom: 1em;
}

.THIS .optionBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .optionBoxName {
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

.THIS .optionBoxDescription{
    margin-bottom: 1em;
}

.THIS .optionBoxDescription p {
    font-size: 12px;
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    margin-bottom: 0.5em;
    min-height: 1.5em;
}

.THIS .room-type{
    font-weight: bold;
    font-size: 1.4em;
}

.THIS .pageContentForm.header{
    margin-bottom:10px;
}

.THIS .pageContentOptions{
    display: flex;
    flex-flow: wrap;
}

.THIS .info-bluelight{
    color: #00b4ff;
    font-weight: bold;
    text-transform: uppercase;
    font-size: 1.2em;
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

.THIS .btn-option{
    height: 100%;
    text-align: center;
    font-weight: bold;
    font-size: 12px;
    color: grey;
    cursor: pointer;
}

.THIS .btn-option-white{
    background-color: white;
}

.THIS .btn-option-white:hover{
    background-color: #f4f6f9;
}

.THIS .btn-option-blue{
    background-color: #0065ff;
    color: white;
}

.THIS .btn-option-blue:hover{
    background-color: #085ee2;
}


/*--------------------
-----Bid------
----------------------*/

.THIS .slds-section__content{
    overflow-x: auto !important;
}

.THIS .slds-card-bid{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    transition: transform 0.1s ease;
}

.THIS .slds-card-bid:hover{
    -webkit-transform: scale(1.05);
    -moz-transform: scale(1.05);
    -o-transform: scale(1.05);
    transform: scale(1.05);
}

.THIS .slds-card-bid_header{
    padding: 1rem 1em 0.5em 2em;;
    background-color: white;
}

.THIS .slds-card-bid_header h3{
    font-weight: bold;
}

.THIS .slds-card-bid-content{
    background-color: white;
    overflow-y: auto;
    padding: 0 16px 16px 16px;
    word-wrap: break-word;/*warp*/
}

.THIS .slds-card-bid-footer{
    background-color: white;
}

.THIS .slds-card-bid-footer > .slds-grid{
    height: 45px;
}

/*--------------------
-----Inputs------
----------------------*/

.THIS .slds-form-element-filter > .slds-form-element__label{
    display: none;
}

.THIS .slds-checkbox_add-button{
    margin-top: 5px;
    margin-right: 5px;
}


.THIS .slds-checkbox_add-button .slds-checkbox_faux{
    width: 1.5rem;
    height: 1.5rem;
}

.THIS .slds-checkbox_add-button .slds-checkbox_faux:after,
.THIS .slds-checkbox_add-button .slds-checkbox_faux:before{
    background-color: white !important;
}

.THIS .recordTable {
    border: none;
}

.THIS .tableRow > div {
    align-items: center;
    display: flex;
    flex: 1;
    padding: 1em;
}
```
### VoyajerOptionsHousingHelper

```
({
	filterMethod : function(component, bids) {
        console.log('# filterMethod');
        
        var bidsFiltered = [];
        var officePreference = component.get("v.officePreference");
        var filterByPrice = component.find("filterByPrice").get("v.value");
        var filterByDistance = component.find("filterByDistance").get("v.value");
        var filterByAmenities = component.find("filterByAmenities").get("v.value");
        
        function isEmpty(obj) {
            for(var prop in obj) if(obj.hasOwnProperty(prop)) return false;
            return true;
        }
        
        //order...
		if(filterByPrice == 'RRRecomendation') bids.sort((a, b) => parseFloat(a.optionNumber) - parseFloat(b.optionNumber));
        else if(filterByPrice == 'LowToHigh') bids.sort((a, b) => parseFloat(a.avgrate) - parseFloat(b.avgrate));
        else if(filterByPrice == 'HighToLow') bids.sort((a, b) => parseFloat(b.avgrate) - parseFloat(a.avgrate));
        
        var addItem_flag1 = false;
        var addItem_flag2 = false;
        for(var i = 0; i < bids.length; i++) {
            var bid = bids[i];
            if(!isEmpty(bid.rateDetails[0])) {
                var revenue = bid.rateDetails[0];
                if(revenue.hasOwnProperty("CurrencyIsoCode")) {
                    //console.log(revenue.CurrencyIsoCode);
                } else {
                    //console.log(officePreference);
                }
            } else {
                //console.log(officePreference);
            }
            addItem_flag1 = false;
            addItem_flag2 = false;
            
            //filterByDistance
            //console.log("# filterByDistance = " + filterByDistance);
            if(filterByDistance == "all") addItem_flag1 = true;
            else if(filterByDistance == 'w0.5' && parseFloat(bid.distance) <= 0.5) addItem_flag1 = true;
                else if(filterByDistance == '0.5-5' && parseFloat(bid.distance) >= 0.5 && parseFloat(bid.distance) <= 5) addItem_flag1 = true;
                    else if(filterByDistance == '5-10' && parseFloat(bid.distance) >= 5 && parseFloat(bid.distance) <= 10) addItem_flag1 = true;
                        else if(filterByDistance == '10+' && parseFloat(bid.distance) >= 10) addItem_flag1 = true;
            
            //filterByAmenities
            //console.log("# filterByAmenities = " + filterByAmenities);
            if(filterByAmenities == "all") addItem_flag2 = true;
            else if(filterByAmenities == 'Wireless' && bid.connection == 'Wireless') addItem_flag2 = true;
                else if(filterByAmenities == 'Wireless and Wired' && bid.connection == 'Wireless and Wired') addItem_flag2 = true;
                    else if(filterByAmenities == 'Pool' && bid.pool == 'Yes') addItem_flag2 = true;
                        else if(filterByAmenities == 'Pet Allowed' && bid.pets_allowed == 'Yes') addItem_flag2 = true;
                            else if(filterByAmenities == 'Hotel Shuttle' && bid.hotel_shuttle == 'Yes') addItem_flag2 = true;
            
            if(addItem_flag1 && addItem_flag2) bidsFiltered.push(bid);
        }
        component.set("v.bidOptionsFiltered", bidsFiltered);
    }
})
```
### VoyajerOptionsHousing

```
<aura:component
	implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction"
	access="global"
	controller="VoyajerController"
>
	<aura:attribute type="String" name="communityNotes" default="" />
	<aura:attribute type="String" name="modalTitle" default="" />
	<aura:attribute type="Boolean" name="showCommunityNote" default="false" />
	<aura:attribute type="Boolean" name="displaySubmit" default="false" />
	<aura:attribute type="Boolean" name="isSelectionMade" default="false" />
	<aura:attribute type="String" name="housingId" />
	<aura:attribute type="String" name="source" default="" />
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="productionName" />
	<aura:attribute type="String" name="housingType" />
	<aura:attribute type="String" name="officePreference" />
	<aura:attribute type="String" name="userProfile" />
	<aura:attribute type="Boolean" name="openOtherProperties" default="false" />
	<aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
	<aura:attribute type="Object" name="serviceData" />
	<aura:attribute type="List" name="bidOptions" />
	<aura:attribute type="List" name="bidOptionsFiltered" />
	<aura:attribute type="List" name="bidOptionsHidden" />
	<aura:attribute type="List" name="bidsSelected" />
	<aura:attribute type="Integer" name="optionDetailRecordId" />
	<aura:attribute type="Integer" name="optionDetailRecordIdReal" />
	<aura:attribute type="Integer" name="bidOptionsSize" />
	<aura:attribute type="List" name="compareList" />
	<aura:attribute name="startDate" type="String" />
	<aura:attribute name="endDate" type="String" />
	<aura:attribute name="selectedLookupId" type="String" />
    <aura:attribute name="selectedPillText" type="String" />
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
	<aura:handler name="change" value="{!v.bidOptions}" action="{!c.loadTable}" />
	<aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
	<div>
		<div class="pageContent">

			<div class="pageContentSpaces">
				<div class="page-section">
					<div class="page-header">
						<h1 class="page-header-title">
							<i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em"></i>
							Options
						</h1>
						<lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
					</div>
				</div>
				<div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb">
					<div class="page-section">
						<div class="slds-grid slds-gutters slds-wrap">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
								<h3>
									<strong style="color: black">{!v.productionName}</strong>
								</h3>
								<p style="margin-right: 0.5em; font-weight: bold; color: #00b4ff">
									{!v.serviceData.cityName} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}
								</p>
								<p style="margin-right: 0.5em; font-weight: bold; color: #00b4ff">{!v.serviceData.venueName}</p>
							</div>
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right">
								<lightning:layout horizontalAlign="end">
									<lightning:layoutItem padding="around-medium">
										<aura:if isTrue="{!if(v.communityNotes!='',true,false)}">
											<lightning:button
												label="View Messages"
												variant="brand"
												iconName="utility:people"
												iconPosition="left"
												class="formButtonBrandLight"
												onclick="{!c.handleShowMessages}"
											/>
										</aura:if>
									</lightning:layoutItem>
									<aura:if isTrue="{!or(v.housingType=='Corporate_Housing',empty(v.serviceData.releaseDate))}">
										<lightning:layoutItem>
											<div class="box-decisionBy">
												Units Not <br/>
												Being Held
											</div>
										</lightning:layoutItem>
										<aura:set attribute="else"> 									
											<lightning:layoutItem>
											<div class="box-decisionBy">
												DECISION BY <br />
												{!v.serviceData.releaseDate}
											</div>
										</lightning:layoutItem></aura:set>
									</aura:if>
								</lightning:layout>
							</div>
						</div>
					</div>
				</div>
				<div class="pageContentDashboard pageContentDashboard-grey">
					<div class="slds-grid slds-wrap">
						<div class="slds-col slds-size_1-of-1">
							<div class="slds-grid slds-wrap slds-grid_vertical-align-center">
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12">
									Filter by
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_3-of-12 slds-large-size_3-of-12">
									<lightning:select
										label="Filter"
										aura:id="filterByPrice"
										variant="label-hidden"
										class="slds-form-element-filter label-hidden"
										onchange="{!c.handleFilter}"
									>
										<option value="RRRecomendation" selected="true">Road Rebel Recomendation</option>
										<option value="LowToHigh">Price Low to High</option>
										<option value="HighToLow">Price High to Low</option>
									</lightning:select>
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_2-of-12 slds-large-size_2-of-12">
									<lightning:select
										label="Filter"
										aura:id="filterByDistance"
										variant="label-hidden"
										class="slds-form-element-filter label-hidden"
										onchange="{!c.handleFilter}"
									>
										<option value="all" selected="true">Distance to Venue</option>
										<option value="w0.5">Walking (0.5 miles)</option>
										<option value="0.5-5">0.5- 5 Miles</option>
										<option value="5-10">5 - 10 Miles</option>
										<option value="10+">10+ Miles</option>
									</lightning:select>
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_2-of-12 slds-large-size_2-of-12">
									<lightning:select
										label="Filter"
										aura:id="filterByAmenities"
										variant="label-hidden"
										class="slds-form-element-filter label-hidden"
										onchange="{!c.handleFilter}"
									>
										<option value="all">Filter by Amenities</option>
										<option value="Wireless">Wireless</option>
										<option value="Wireless and Wired">Wireless and Wired</option>
										<option value="Pool">Pool</option>
										<option value="Pet Allowed">Pet Allowed</option>
										<option value="Hotel Shuttle">Hotel Shuttle</option>
									</lightning:select>
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
									<lightning:button label="Update" variant="brand" class="btn btn-bluelight" onclick="{!c.doInit}" />
								</div>
								<div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
									<lightning:button label="Clear" variant="neutral" class="btn btn-white" onclick="{!c.loadTable}" />
								</div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
                                    <lightning:button label="Compare" variant="brand" class="btn" onclick="{!c.handleCompare}" />
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small" style="margin: 0; text-align: right">
									<lightning:button label="PDF" variant="brand" class="btn" onclick="{!c.generatePDF}" />
								</div>
							</div>
						</div>
					</div>
				</div>
				<div class="pageContentDashboard pageContentDashboard-grey" style="padding-top: 0">
					<section class="slds-grid slds-gutters slds-wrap">
						<aura:iteration items="{!v.bidOptionsFiltered}" var="bid" indexVar="bidIndex">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3">
								<article class="slds-card-bid">
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<header class="slds-card-bid_header">
												<div class="">
													<h3 style="text-align: center">{!bid.vendor}</h3>
													<aura:if isTrue="{!not(empty(bid.provider))}">
														<p style="font-size: 1rem; text-align: center">Provider: {!bid.provider}</p>
													</aura:if>
												</div>
											</header>
										</div>
									</div>
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<div class="slds-card-bid-content">
												<div class="slds-grid slds-wrap">
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em">
														<aura:iteration items="{!bid.stars}" var="star">
															<i class="fas fa-star" style="color: #ffa000"></i>
														</aura:iteration>
													</div>
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; font-size: 12px">
														{!if(and(bid.dx_to_venue != null,bid.dx_to_venue != ''),bid.dx_to_venue,'&nbsp;')}
													</div>
													<div
														class="slds-col slds-size_1-of-1"
														style="margin-bottom: 0.5em; font-size: 12px; color: #00b4ff; font-weight: bold"
													>
														{!if(and(bid.physical != null,bid.physical != ''),bid.physical,'&nbsp;')}
													</div>
													<div
														class="slds-col slds-size_1-of-1"
														style="margin-bottom: 0.5em; font-size: 12px; color: #00b4ff; font-weight: bold"
													>
														<aura:if isTrue="{!and(bid.website != null, bid.website != '')}">
															<lightning:formattedText linkify="true" value="{!bid.website}" />
														</aura:if>
													</div>
													<!-- Fix By Clay Dev 31 Jan, 2021 #176367796
                                                    <div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; font-size: 12px">
														{!if(and(bid.phone != null,bid.phone != ''),bid.phone,'&nbsp;')}
													</div> -->
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; min-height: 20px">
														<i
															class="fas fa-wifi"
															style="{!if(or(bid.connection == 'Wireless',bid.connection == 'Wireless and Wired'),'color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
														<i
															class="fas fa-swimming-pool"
															style="{!if(bid.pool == 'Yes','color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
														<i
															class="fas fa-paw"
															style="{!if(bid.pets_allowed == 'Yes','color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
														<i
															class="fas fa-bus"
															style="{!if(bid.hotel_shuttle == 'Yes','color:#007bff;margin-right: 10px;','display:none;')}"
														></i>
													</div>
													<div class="slds-col slds-size_1-of-1" style="margin-bottom: 0.5em; font-size: 12px; min-height: 4em">
														<span style="color: #00b4ff">CONCESSIONS</span>
														<ul class="slds-list_dotted">
															<aura:iteration items="{!bid.concessions}" var="concession">
																<!--<li style="list-style: disc;">{!concession.Concession_Provided__c}</li>-->
																<li style="list-style: disc">
																	<aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
																		{!concession.Concessions_Requested__c+' '+concession.Concession_Provided__c}
																		<aura:set attribute="else"> {!concession.Concession_Provided__c} </aura:set>
																	</aura:if>
																</li>
															</aura:iteration>
														</ul>
													</div>
													<div
														class="slds-col slds-size_1-of-1"
														style="margin-top: 0.5em; margin-bottom: 0.5em; font-size: 12px; min-height: 4em"
													>
														<div class="slds-grid slds-wrap">
															<aura:iteration items="{!bid.roomTypes}" var="roomtype">
																<div class="slds-size_1-of-1 slds-medium-size_2-of-3 slds-large-size_2-of-3">
																	<span style="font-size: 1.2em">{!roomtype.Units__c}</span>
																	-
																	<span style="font-size: 1.2em">{!roomtype.Unit_Type__c}</span>
																</div>
																<div class="slds-size_1-of-1 slds-medium-size_1-of-3 slds-large-size_1-of-3" style="text-align: right">
																	<span class="room-type">
																		<lightning:formattedNumber
																			value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}"
																			style="currency"
																			currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}"
																			currencyDisplayAs="symbol"
																		/>
																		<!--${!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}-->
																	</span>
																</div>
															</aura:iteration>
														</div>
													</div>
												</div>
												<div class="slds-grid slds-gutters slds-wrap slds-deviations" style="text-align: center; padding: 1em 0 0 0">
													<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
														<div style="border-top: 1px solid #eaeaea; font-style: italic; color: #0065ff; padding: 1em 1em 0em 1em">
															<span>
																Weighted Avg Rate:
																<lightning:formattedNumber
																	value="{!bid.avgrate}"
																	style="currency"
																	currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}"
																	currencyDisplayAs="symbol"
																/>
															</span>
															<br/>
															<span>
																Total Cost:
																<lightning:formattedNumber
																	value="{!bid.totalrate}"
																	style="currency"
																	currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}"
																	currencyDisplayAs="symbol"
																/>
															</span>
															<br />

															<!--Weighted Avg Rate: ${!bid.avgrate}-->
														</div>
													</div>
												</div>
											</div>
										</div>
									</div>
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<footer class="slds-card-bid-footer">
												<div class="slds-grid">
													<div
														class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
														style="border-left: 1px solid #eaeaea"
													>
														<lightning:input type="checkbox-button" label="COMPARE" checked="{!bid.isCompared}" /><span>COMPARE</span>
													</div>
													<div
														class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
														style="border-left: 1px solid #eaeaea; color: #00b4ff"
														data-bidindex="{!bidIndex}"
														onclick="{!c.openOptionDetail}"
													>
														DETAILS
													</div>
                                                    <!-- Fix By Clay Dev #178056511-->
                                                        <aura:if isTrue="{!bid.isEvent}">
                                                            <div
                                                            class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
                                                            style="border-left: 1px solid #eaeaea">
                                                            <lightning:input type="checkbox-button" aura:id="review-select-checkbox" label="SELECT" checked="{!bid.isMultiContract}" onchange="{!c.handleMultiSelect}"/><span>SELECT</span>
                                                        </div>
                                                        <aura:set attribute="else">
                                                            <div
                                                            class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-blue"
                                                            style="border-left: 1px solid #eaeaea"
                                                            data-bidindex="{!bidIndex}"
                                                            data-recordId="{!bid.record.Id}"
                                                            onclick="{!c.openReviewSubmit}"
                                                        >
                                                            SELECT
                                                        </div>
                                                        </aura:set>
                                                    </aura:if>
												</div>
											</footer>
										</div>
									</div>
								</article>
							</div>
						</aura:iteration>
					</section>
					<aura:if isTrue="{!v.displaySubmit}">
						<div class="slds-grid slds-wrap">
							<div class="slds-col slds-size_1-of-1" style="margin-top: 2em; text-align: center">
								<lightning:button
									label="SUBMIT"
									variant="success"
									onclick="{!c.submitSelectedOptions}"
								/>
							</div>
						</div>
					</aura:if>
					<aura:if isTrue="{!!v.displaySubmit}">
					<div class="slds-grid slds-wrap">
						<div class="slds-col slds-size_1-of-1" style="margin-top: 2em; text-align: center">
							<lightning:button
								label="OTHERS PROPERTIES CONTACTED"
								variant="brand"
								class="formButtonBrandLight btn-custom"
								onclick="{!c.handleShowOtherProperties}"
							/>
						</div>
					</div>
					</aura:if>

				</div>
			</div>
			<aura:if isTrue="{!v.openOtherProperties}">
				<!--###### MODAL BOX Start######-->
				<section
					role="dialog"
					tabindex="-1"
					aria-labelledby="modal-heading-02"
					aria-modal="true"
					aria-describedby="modal-content-id-2"
					class="slds-modal slds-fade-in-open"
				>
					<div class="slds-modal__container">
						<!-- ###### MODAL BOX HEADER Start ######-->
						<header class="slds-modal__header" style="border-bottom: 0">
							<lightning:buttonIcon
								iconName="utility:close"
								alternativeText="close"
								variant="bare-inverse"
								class="slds-modal__close"
								onclick="{!c.handleCloseModal}"
							/>
							<h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate" style="color: #00b4ff">
								Additional Properties Contacted
							</h2>
						</header>
						<!--###### MODAL BOX BODY Part Start######-->
						<div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1" style="padding-top: 0">
							<aura:if isTrue="{!not(empty(v.bidOptionsHidden))}">
								<div class="recordTable tableList" style="padding: 0 1.5rem; margin: 0">
									<div class="tableRow">
										<div style="white-space: normal; text-align: left">
											<b>Property</b>
										</div>
										<div style="white-space: normal; text-align: left">
											<b>Notes</b>
										</div>
									</div>
									<aura:iteration items="{!v.bidOptionsHidden}" var="bidHidden">
										<div class="tableRow">
											<div style="white-space: normal; text-align: left">{!bidHidden.vendor}</div>
											<div style="white-space: normal; text-align: left; color: red">
												<b>{!bidHidden.noBidReason}</b>
											</div>
											<!--Fix by Clay 22 Jan, 2021 : for User Story #176605416
											<aura:if isTrue="{!bidHidden.record.Status__c=='Sold Out / Not Bidding'}">
            										//<div style="white-space: normal; text-align: left; color: red;"><b>SOLD OUT</b></div>
												<aura:set attribute="else"> </aura:set>
											</aura:if>-->
										</div>
									</aura:iteration>
								</div>
								<aura:set attribute="else">
									<p style="text-align: center">Don’t have others Properties Contacted</p>
								</aura:set>
							</aura:if>
						</div>
					</div>
				</section>
				<div class="slds-backdrop slds-backdrop_open"></div>
				<!--######## MODAL BOX Part END Here ######-->
			</aura:if>
			<aura:if isTrue="{!v.openSelectOptionsAlert}">
				<c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}" />
			</aura:if>
		</div>
	</div>
	
	<aura:if isTrue="{!v.showCommunityNote}">
		<c:VoyajerOptionsModalSelectAlert
			modalTitleText="Message From Your Rebel"
			modalDetailText="{!v.communityNotes}"
			openSelectOptionsAlert="{!v.showCommunityNote}"
		/>
	</aura:if>

</aura:component>
```
### VoyajerOptionsHousing

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

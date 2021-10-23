---
layout: default
title: VoyajerOptionsGT
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsGT
## Fields
### VoyajerOptionsGT

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsGTHelper

```
({
	filterMethod : function(bids, filterByPrice) {
        console.log('# filterMethod');
        
        //order...
		if(filterByPrice == 'RRRecomendation'){
            //console.log('# RRRecomendation');
        	bids.sort((a, b) => parseFloat(a.optionNumber) - parseFloat(b.optionNumber));
        }else if(filterByPrice == 'LowToHigh'){
            //console.log('# LowToHigh');
        	bids.sort((a, b) => parseFloat(a.totalPrice) - parseFloat(b.totalPrice));
        }else if(filterByPrice == 'HighToLow'){
            //console.log('# HighToLow');
        	bids.sort((a, b) => parseFloat(b.totalPrice) - parseFloat(a.totalPrice));
        }
        
		return bids;
	}
})
```
### VoyajerOptionsGT

```
.THIS .label-hidden > label {
    display: none;
}

.THIS .optionBox {
    width: 32%;
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
    background-color: #022066;
    color: white;
    font-weight: 600;
    font-size: 1.25em;
    display: flex;
    align-items: center;
    justify-content: left;
    padding: 0.8em;
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

.THIS .optionBoxButtons{
    padding: 1em;
    text-align: center;
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .optionBoxDescription{
    text-align: center;
}

.THIS .optionBoxDescription .total{
    background-color: #f6f7fc;
}
.THIS .optionBoxDescription .total-price-number{
    font-weight: bold;
    font-size: 18px;
    color: black;
    padding: 1em 1em 1em 1em;
    text-align: right;
}

.THIS .optionBoxDescription .total-price{
    padding: 1.5em 1em 1em 2.5em;
    text-align: left;
}

.THIS .optionBoxDescription .travel{
    padding: 1.5em 1em 1em 1em;
}

.THIS .optionBoxDescription .travel-other-description{
    margin-bottom: 1em;
}

.THIS .optionBoxDescription .travel .title{
    font-weight: bold;
    font-size: 16px;
}

.THIS .optionBoxDescription .travel .sub{
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .optionBoxDescription p {
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

.THIS .optionBoxDescription .icon{
    font-size:20px;
}

.THIS .optionBoxButtons{
    padding: 1em;
}

.THIS .optionBoxButtons .button{
    padding: 1em;
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
    padding: 1rem;
    background-color: #022066;
}

.THIS .slds-card-bid_header h3{
    color: white;
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
```
### VoyajerOptionsGT

```
<aura:component>
	<aura:attribute type="String" name="communityNotes" default="" />
	<aura:attribute type="String" name="modalTitle" default="" />
	<aura:attribute type="Boolean" name="showCommunityNote" default="false" />
	<aura:attribute type="String" name="groundId" />
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="productionName" />
	<aura:attribute type="Object" name="serviceData" />
	<aura:attribute type="List" name="bidOptions" />
	<aura:attribute type="List" name="bidOptionsFiltered" />
	<aura:attribute type="Integer" name="optionDetailRecordId" />
	<aura:attribute type="Integer" name="optionDetailRecordIdReal" />
	<aura:attribute type="Integer" name="bidOptionsSize" />
	<aura:attribute type="List" name="compareList" />
	<aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
	<aura:attribute type="String" name="source" default="" />

	<aura:handler name="init" value="{!this}" action="{!c.doInit}" />
	<aura:handler name="change" value="{!v.bidOptions}" action="{!c.loadTable}" />
	<aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

	<div>
		<div class="pageContent">
			<div class="pageContentSpaces">
				<div class="page-section">
					<div class="page-header">
						<h1 class="page-header-title"><i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em"></i>Options</h1>
						<lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
					</div>
				</div>
				<div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb">
					<div class="page-section">
						<div class="slds-grid slds-gutters slds-wrap">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
								<h3><strong style="color: black">{!v.productionName}</strong></h3>
								<p style="margin-right: 0.5em; font-weight: bold; color: #00b4ff">
									{!v.serviceData.cityName} {!if(and(v.serviceData.endCityName != null, v.serviceData.endCityName != ''),' to ' +
									v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}
								</p>
								<!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
								<p>Group Type: {!v.serviceData.groupType}</p>
							</div>
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right">
								<div style="text-align: right">
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
										<lightning:layoutItem>
											<div class="box-decisionBy">
												DECISION BY <br />
												{!v.serviceData.releaseDate}
											</div>
										</lightning:layoutItem>
									</lightning:layout>
								</div>
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
								<div
									class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
								>
									<lightning:button label="Update" variant="brand" class="btn btn-bluelight" onclick="{!c.doInit}" />
								</div>
								<div
									class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
								>
									<lightning:button label="Clear" variant="neutral" class="btn btn-white" onclick="{!c.loadTable}" />
								</div>
								<div
									class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_4-of-12 slds-large-size_6-of-12 slds-p-horizontal_x-small"
									style="margin: 0; text-align: right"
								>
									<lightning:button label="Compare" variant="brand" class="btn" onclick="{!c.handleCompare}" />
								</div>
							</div>
						</div>
					</div>
				</div>
				<!--<div class="pageContentOptions" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">-->
				<div class="pageContentDashboard pageContentDashboard-grey" style="padding-top: 0; border-bottom: 1px solid #dbdbdb">
					<section class="slds-grid slds-gutters slds-wrap">
						<aura:iteration items="{!v.bidOptionsFiltered}" var="bid" indexVar="bidIndex">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3">
								<article class="slds-card-bid">
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<header class="slds-card-bid_header">
												<div class="">
													<h3 style="text-align: center">{!bid.vendor}</h3>
												</div>
											</header>
										</div>
									</div>
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<div class="slds-card-bid-content">
												<div>
													<aura:iteration items="{!bid.travels}" var="travel">
														<!--<div class="travel">-->
														<div class="slds-grid slds-gutters slds-wrap slds-text-align_center" style="padding: 1em 0 0">
															<div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
																<span style="font-size: 2em">
																	<i class="fas fa-bus icon"></i>
																</span>
															</div>
															<div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color: #022066">
																<strong style="font-size: 1.5em"><!--{!travel.startCity}-->{!travel.startCityShortName}</strong><br />
																<span style="text-transform: uppercase">{!travel.locationType}</span><br /> {!travel.startDateTime}<br />
															</div>
															<div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
																<lightning:icon iconName="utility:forward" size="x-small" />
															</div>
															<div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color: #022066">
																<strong style="font-size: 1.5em"><!--{!travel.endCity}-->{!travel.endCityShortName}</strong><br />
																<span style="text-transform: uppercase">{!travel.locationDropOffType}</span
																><br /> {!travel.endDateTime}<br />
															</div>
														</div>
														<div
															class="slds-grid slds-gutters slds-wrap"
															style="text-align: center; padding: 1em 0; border-bottom: 1px solid #eaeaea"
														>
															<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="border-right: 1px solid #eaeaea">
																{!if(and(travel.capacity != null,travel.capacity != ''),travel.capacity + ' PAX','&nbsp;')}
															</div>
															<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
																{!if(and(travel.vehicleType != null,travel.vehicleType != ''),travel.vehicleType,'&nbsp;')}
															</div>
														</div>

														<!--<div style="display:flex;">
                                                                    <div style="flex:1;">
                                                                        <i class="fas fa-bus icon"></i>
                                                                    </div>
                                                                    <div style="flex:1;" class="title">
                                                                        {!travel.startCityShortName}
                                                                    </div>
                                                                    <div style="flex:1; color:darkgray;">
                                                                        <i class="fas fa-arrow-right"></i>
                                                                    </div>
                                                                    <div style="flex:1;" class="title">
                                                                        {!travel.endCityShortName}
                                                                    </div>                                            
                                                                </div>
                                                                <div style="display:flex;">
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.locationType}
                                                                    </div>
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.locationDropOffType}
                                                                    </div>
                                                                </div>
                                                                <div style="display:flex;">
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.startDateTime}
                                                                    </div>
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.endDateTime}
                                                                    </div>
                                                                </div>
                                                        	</div>
															<div class="travel-other-description">
                                                                <div style="display:flex;">
                                                                    <div style="flex:1;" class="sub">
                                                                        {!if(and(travel.capacity != null,travel.capacity != ''),travel.capacity + ' PAX','&nbsp;')}
                                                                        <span class="slds-p-horizontal_small" style="color:darkgray;">|</span>
                                                                        {!if(and(travel.vehicleType != null,travel.vehicleType != ''),travel.vehicleType,'&nbsp;')}
                                                                    </div>
                                                                </div>
                                                            </div>-->
													</aura:iteration>
													<!--<div style="display:flex;" class="total">
                                                        <div style="flex:1;" class="total-price">Total Price</div>
                                                        <div style="flex:1;" class="total-price-number">${!bid.totalPrice}</div>
                                                    </div>-->
												</div>
											</div>
										</div>
									</div>
									<!--<div class="optionBoxButtons">
                                        <div style="display:flex;">
                                            <div style="flex:1;" class="button">
                                                Compare
                                            </div>
                                            <div style="flex:1;" class="button">
                                                <a href="javascript:void(0)" data-bidindex="{!bixIndex}" onclick="{!c.openOptionDetail}">
                                                    Details
                                                </a>
                                            </div>
                                            <div style="flex:1;" class="button">
                                                <a href="javascript:void(0)" data-bidindex="{!bixIndex}" onclick="{!c.openReviewSubmit}">
                                                    Select
                                                </a>
                                            </div>
                                        </div>
                                    </div>-->
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<footer class="slds-card-bid-footer">
												<div class="slds-grid" style="background: content-box#f6f7fc">
													<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
														<strong style="font-size: 13px; color: grey">Total Price</strong>
													</div>
													<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
														<strong style="font-size: 18px"
															><lightning:formattedNumber value="{!bid.totalPrice}" style="currency" currencyCode="{!bid.currencyIsoCode}"
														/></strong>
														<!--<strong style="font-size:18px;">${!if(and(bid.totalPrice != null,bid.totalPrice != ''),bid.totalPrice,'0.00')}</strong>-->
													</div>
												</div>

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
													<div
														class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-blue"
														style="border-left: 1px solid #eaeaea"
														data-bidindex="{!bidIndex}"
														data-recordid="{!bid.recordId}"
														onclick="{!c.openReviewSubmit}"
													>
														SELECT
													</div>
												</div>
											</footer>
										</div>
									</div>
								</article>
							</div>
						</aura:iteration>
					</section>
				</div>
			</div>
		</div>
	</div>
	<aura:if isTrue="{!v.showCommunityNote}">
		<c:VoyajerOptionsModalSelectAlert
			modalTitleText="{!v.modalTitle}"
			modalDetailText="{!v.communityNotes}"
			openSelectOptionsAlert="{!v.showCommunityNote}"
		/>
	</aura:if>
</aura:component>
```
### VoyajerOptionsGTController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        if (component.get('v.source') === 'preview') {
          callToParent.setParam("action", "loadOptionsGTPreview");
        } else {
          callToParent.setParam("action", "loadOptionsGT");
        }
        callToParent.fire();
	},
  loadTable : function(component, event, helper) {
      console.log('# loadTable()');
      component.find("filterByPrice").set("v.value","RRRecomendation");
      var bids = component.get("v.bidOptions");
      
      var bidsFiltered = helper.filterMethod(bids, "RRRecomendation");
      component.set("v.bidOptionsFiltered", bidsFiltered);
  },
  handleShowMessages : function(component, event, helper) {
    component.set('v.showCommunityNote', true);
    var callToParent = component.getEvent("callToParent");
    callToParent.setParam("action","showMessages");
    callToParent.fire();    
  },
  openOptionDetail: function(component,event,helper){
      var bidindex = event.currentTarget.dataset.bidindex;
      var list = component.get("v.bidOptions");
      component.set("v.optionDetailRecordId",bidindex);
      component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
      component.set("v.bidOptionsSize",list.length);
      component.set("v.mainContent","optionsGTDetail");
  },
  openReviewSubmit: function(component,event,helper){
    console.log('in review submit');
    var theURL = window.location.href;
    var isPreview = theURL.includes('VoyajerPreviewApp');
    var okToAdvance = true;

    if (isPreview){
      okToAdvance = false;
      component.set('v.modalTitle', 'Preview Only');
      component.set('v.communityNotes', 'Selection not Allowed in Preview');
      component.set('v.openSelectOptionsAlert', true);
      component.set('v.showCommunityNote', true);
    } else if (!isPreview){
      var bidindex = event.currentTarget.dataset.bidindex;
      var recordId = event.currentTarget.dataset.recordid;
      var list = component.get("v.bidOptions");
      var indexActual;
      var index = 0;
      list.forEach(function (bid) {
        //console.log(JSON.stringify(recordId));
        if (bid.recordId == recordId) {
          console.log('had a match');
          indexActual = index;
        }
        index++;
      });

      console.log('list ::' + JSON.stringify(list[indexActual].record.Status__c));
  
      if ((list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
        okToAdvance = false;
      }
    }


    if (okToAdvance) {
      component.set("v.optionDetailRecordId",bidindex);
      component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
      component.set("v.bidOptionsSize",list.length);
      component.set("v.mainContent","optionsGTReviewSubmit");
    } else if (okToAdvance && !isPreview) {
      component.set('v.showCommunityNote', true);
      component.set('v.modalTitle', 'Invalid Status');
      component.set('v.communityNotes', 'Need to make a change? Contact your Rebel!');
    }
    console.log('done :: okToAdvance :: ' + okToAdvance);



  },
	handleCompare : function(component, event, helper){
		var bidsSelected = [];
		component.get("v.bidOptions").forEach(function(bid){
			if(bid.isCompared) bidsSelected.push(bid);
		});
        console.log(bidsSelected);
		component.set("v.compareList", bidsSelected);
		component.set("v.mainContent", "optionsGTCompare");
	},
    handleBack : function(component, event, helper){
		component.set("v.mainContent", "actions");
	},
    
    handleFilter : function(component, event, helper) {
        var bids = component.get("v.bidOptions");
        var filterByPrice = component.find("filterByPrice").get("v.value");
        
        var bidsFiltered = helper.filterMethod(bids, filterByPrice);
		component.set("v.bidOptionsFiltered", bidsFiltered);
    }
})
```
### VoyajerOptionsGT

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsGTHelper

```
({
	filterMethod : function(bids, filterByPrice) {
        console.log('# filterMethod');
        
        //order...
		if(filterByPrice == 'RRRecomendation'){
            //console.log('# RRRecomendation');
        	bids.sort((a, b) => parseFloat(a.optionNumber) - parseFloat(b.optionNumber));
        }else if(filterByPrice == 'LowToHigh'){
            //console.log('# LowToHigh');
        	bids.sort((a, b) => parseFloat(a.totalPrice) - parseFloat(b.totalPrice));
        }else if(filterByPrice == 'HighToLow'){
            //console.log('# HighToLow');
        	bids.sort((a, b) => parseFloat(b.totalPrice) - parseFloat(a.totalPrice));
        }
        
		return bids;
	}
})
```
### VoyajerOptionsGT

```
.THIS .label-hidden > label {
    display: none;
}

.THIS .optionBox {
    width: 32%;
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
    background-color: #022066;
    color: white;
    font-weight: 600;
    font-size: 1.25em;
    display: flex;
    align-items: center;
    justify-content: left;
    padding: 0.8em;
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

.THIS .optionBoxButtons{
    padding: 1em;
    text-align: center;
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .optionBoxDescription{
    text-align: center;
}

.THIS .optionBoxDescription .total{
    background-color: #f6f7fc;
}
.THIS .optionBoxDescription .total-price-number{
    font-weight: bold;
    font-size: 18px;
    color: black;
    padding: 1em 1em 1em 1em;
    text-align: right;
}

.THIS .optionBoxDescription .total-price{
    padding: 1.5em 1em 1em 2.5em;
    text-align: left;
}

.THIS .optionBoxDescription .travel{
    padding: 1.5em 1em 1em 1em;
}

.THIS .optionBoxDescription .travel-other-description{
    margin-bottom: 1em;
}

.THIS .optionBoxDescription .travel .title{
    font-weight: bold;
    font-size: 16px;
}

.THIS .optionBoxDescription .travel .sub{
    text-transform: uppercase;
    font-size: 12px;
}

.THIS .optionBoxDescription p {
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

.THIS .optionBoxDescription .icon{
    font-size:20px;
}

.THIS .optionBoxButtons{
    padding: 1em;
}

.THIS .optionBoxButtons .button{
    padding: 1em;
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
    padding: 1rem;
    background-color: #022066;
}

.THIS .slds-card-bid_header h3{
    color: white;
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
```
### VoyajerOptionsGT

```
<aura:component>
	<aura:attribute type="String" name="communityNotes" default="" />
	<aura:attribute type="String" name="modalTitle" default="" />
	<aura:attribute type="Boolean" name="showCommunityNote" default="false" />
	<aura:attribute type="String" name="groundId" />
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="productionName" />
	<aura:attribute type="Object" name="serviceData" />
	<aura:attribute type="List" name="bidOptions" />
	<aura:attribute type="List" name="bidOptionsFiltered" />
	<aura:attribute type="Integer" name="optionDetailRecordId" />
	<aura:attribute type="Integer" name="optionDetailRecordIdReal" />
	<aura:attribute type="Integer" name="bidOptionsSize" />
	<aura:attribute type="List" name="compareList" />
	<aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
	<aura:attribute type="String" name="source" default="" />

	<aura:handler name="init" value="{!this}" action="{!c.doInit}" />
	<aura:handler name="change" value="{!v.bidOptions}" action="{!c.loadTable}" />
	<aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

	<div>
		<div class="pageContent">
			<div class="pageContentSpaces">
				<div class="page-section">
					<div class="page-header">
						<h1 class="page-header-title"><i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em"></i>Options</h1>
						<lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
					</div>
				</div>
				<div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb">
					<div class="page-section">
						<div class="slds-grid slds-gutters slds-wrap">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
								<h3><strong style="color: black">{!v.productionName}</strong></h3>
								<p style="margin-right: 0.5em; font-weight: bold; color: #00b4ff">
									{!v.serviceData.cityName} {!if(and(v.serviceData.endCityName != null, v.serviceData.endCityName != ''),' to ' +
									v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}
								</p>
								<!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
								<p>Group Type: {!v.serviceData.groupType}</p>
							</div>
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right">
								<div style="text-align: right">
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
										<lightning:layoutItem>
											<div class="box-decisionBy">
												DECISION BY <br />
												{!v.serviceData.releaseDate}
											</div>
										</lightning:layoutItem>
									</lightning:layout>
								</div>
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
								<div
									class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
								>
									<lightning:button label="Update" variant="brand" class="btn btn-bluelight" onclick="{!c.doInit}" />
								</div>
								<div
									class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
								>
									<lightning:button label="Clear" variant="neutral" class="btn btn-white" onclick="{!c.loadTable}" />
								</div>
								<div
									class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_4-of-12 slds-large-size_6-of-12 slds-p-horizontal_x-small"
									style="margin: 0; text-align: right"
								>
									<lightning:button label="Compare" variant="brand" class="btn" onclick="{!c.handleCompare}" />
								</div>
							</div>
						</div>
					</div>
				</div>
				<!--<div class="pageContentOptions" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">-->
				<div class="pageContentDashboard pageContentDashboard-grey" style="padding-top: 0; border-bottom: 1px solid #dbdbdb">
					<section class="slds-grid slds-gutters slds-wrap">
						<aura:iteration items="{!v.bidOptionsFiltered}" var="bid" indexVar="bidIndex">
							<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3">
								<article class="slds-card-bid">
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<header class="slds-card-bid_header">
												<div class="">
													<h3 style="text-align: center">{!bid.vendor}</h3>
												</div>
											</header>
										</div>
									</div>
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<div class="slds-card-bid-content">
												<div>
													<aura:iteration items="{!bid.travels}" var="travel">
														<!--<div class="travel">-->
														<div class="slds-grid slds-gutters slds-wrap slds-text-align_center" style="padding: 1em 0 0">
															<div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
																<span style="font-size: 2em">
																	<i class="fas fa-bus icon"></i>
																</span>
															</div>
															<div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color: #022066">
																<strong style="font-size: 1.5em"><!--{!travel.startCity}-->{!travel.startCityShortName}</strong><br />
																<span style="text-transform: uppercase">{!travel.locationType}</span><br /> {!travel.startDateTime}<br />
															</div>
															<div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
																<lightning:icon iconName="utility:forward" size="x-small" />
															</div>
															<div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color: #022066">
																<strong style="font-size: 1.5em"><!--{!travel.endCity}-->{!travel.endCityShortName}</strong><br />
																<span style="text-transform: uppercase">{!travel.locationDropOffType}</span
																><br /> {!travel.endDateTime}<br />
															</div>
														</div>
														<div
															class="slds-grid slds-gutters slds-wrap"
															style="text-align: center; padding: 1em 0; border-bottom: 1px solid #eaeaea"
														>
															<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="border-right: 1px solid #eaeaea">
																{!if(and(travel.capacity != null,travel.capacity != ''),travel.capacity + ' PAX','&nbsp;')}
															</div>
															<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
																{!if(and(travel.vehicleType != null,travel.vehicleType != ''),travel.vehicleType,'&nbsp;')}
															</div>
														</div>

														<!--<div style="display:flex;">
                                                                    <div style="flex:1;">
                                                                        <i class="fas fa-bus icon"></i>
                                                                    </div>
                                                                    <div style="flex:1;" class="title">
                                                                        {!travel.startCityShortName}
                                                                    </div>
                                                                    <div style="flex:1; color:darkgray;">
                                                                        <i class="fas fa-arrow-right"></i>
                                                                    </div>
                                                                    <div style="flex:1;" class="title">
                                                                        {!travel.endCityShortName}
                                                                    </div>                                            
                                                                </div>
                                                                <div style="display:flex;">
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.locationType}
                                                                    </div>
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.locationDropOffType}
                                                                    </div>
                                                                </div>
                                                                <div style="display:flex;">
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.startDateTime}
                                                                    </div>
                                                                    <div style="flex:1;"></div>
                                                                    <div style="flex:1;" class="sub">
                                                                        {!travel.endDateTime}
                                                                    </div>
                                                                </div>
                                                        	</div>
															<div class="travel-other-description">
                                                                <div style="display:flex;">
                                                                    <div style="flex:1;" class="sub">
                                                                        {!if(and(travel.capacity != null,travel.capacity != ''),travel.capacity + ' PAX','&nbsp;')}
                                                                        <span class="slds-p-horizontal_small" style="color:darkgray;">|</span>
                                                                        {!if(and(travel.vehicleType != null,travel.vehicleType != ''),travel.vehicleType,'&nbsp;')}
                                                                    </div>
                                                                </div>
                                                            </div>-->
													</aura:iteration>
													<!--<div style="display:flex;" class="total">
                                                        <div style="flex:1;" class="total-price">Total Price</div>
                                                        <div style="flex:1;" class="total-price-number">${!bid.totalPrice}</div>
                                                    </div>-->
												</div>
											</div>
										</div>
									</div>
									<!--<div class="optionBoxButtons">
                                        <div style="display:flex;">
                                            <div style="flex:1;" class="button">
                                                Compare
                                            </div>
                                            <div style="flex:1;" class="button">
                                                <a href="javascript:void(0)" data-bidindex="{!bixIndex}" onclick="{!c.openOptionDetail}">
                                                    Details
                                                </a>
                                            </div>
                                            <div style="flex:1;" class="button">
                                                <a href="javascript:void(0)" data-bidindex="{!bixIndex}" onclick="{!c.openReviewSubmit}">
                                                    Select
                                                </a>
                                            </div>
                                        </div>
                                    </div>-->
									<div class="slds-grid slds-gutters slds-wrap">
										<div class="slds-col slds-size_1-of-1">
											<footer class="slds-card-bid-footer">
												<div class="slds-grid" style="background: content-box#f6f7fc">
													<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
														<strong style="font-size: 13px; color: grey">Total Price</strong>
													</div>
													<div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
														<strong style="font-size: 18px"
															><lightning:formattedNumber value="{!bid.totalPrice}" style="currency" currencyCode="{!bid.currencyIsoCode}"
														/></strong>
														<!--<strong style="font-size:18px;">${!if(and(bid.totalPrice != null,bid.totalPrice != ''),bid.totalPrice,'0.00')}</strong>-->
													</div>
												</div>

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
													<div
														class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-blue"
														style="border-left: 1px solid #eaeaea"
														data-bidindex="{!bidIndex}"
														data-recordid="{!bid.recordId}"
														onclick="{!c.openReviewSubmit}"
													>
														SELECT
													</div>
												</div>
											</footer>
										</div>
									</div>
								</article>
							</div>
						</aura:iteration>
					</section>
				</div>
			</div>
		</div>
	</div>
	<aura:if isTrue="{!v.showCommunityNote}">
		<c:VoyajerOptionsModalSelectAlert
			modalTitleText="{!v.modalTitle}"
			modalDetailText="{!v.communityNotes}"
			openSelectOptionsAlert="{!v.showCommunityNote}"
		/>
	</aura:if>
</aura:component>
```
### VoyajerOptionsGTController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        if (component.get('v.source') === 'preview') {
          callToParent.setParam("action", "loadOptionsGTPreview");
        } else {
          callToParent.setParam("action", "loadOptionsGT");
        }
        callToParent.fire();
	},
  loadTable : function(component, event, helper) {
      console.log('# loadTable()');
      component.find("filterByPrice").set("v.value","RRRecomendation");
      var bids = component.get("v.bidOptions");
      
      var bidsFiltered = helper.filterMethod(bids, "RRRecomendation");
      component.set("v.bidOptionsFiltered", bidsFiltered);
  },
  handleShowMessages : function(component, event, helper) {
    component.set('v.showCommunityNote', true);
    var callToParent = component.getEvent("callToParent");
    callToParent.setParam("action","showMessages");
    callToParent.fire();    
  },
  openOptionDetail: function(component,event,helper){
      var bidindex = event.currentTarget.dataset.bidindex;
      var list = component.get("v.bidOptions");
      component.set("v.optionDetailRecordId",bidindex);
      component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
      component.set("v.bidOptionsSize",list.length);
      component.set("v.mainContent","optionsGTDetail");
  },
  openReviewSubmit: function(component,event,helper){
    console.log('in review submit');
    var theURL = window.location.href;
    var isPreview = theURL.includes('VoyajerPreviewApp');
    var okToAdvance = true;

    if (isPreview){
      okToAdvance = false;
      component.set('v.modalTitle', 'Preview Only');
      component.set('v.communityNotes', 'Selection not Allowed in Preview');
      component.set('v.openSelectOptionsAlert', true);
      component.set('v.showCommunityNote', true);
    } else if (!isPreview){
      var bidindex = event.currentTarget.dataset.bidindex;
      var recordId = event.currentTarget.dataset.recordid;
      var list = component.get("v.bidOptions");
      var indexActual;
      var index = 0;
      list.forEach(function (bid) {
        //console.log(JSON.stringify(recordId));
        if (bid.recordId == recordId) {
          console.log('had a match');
          indexActual = index;
        }
        index++;
      });

      console.log('list ::' + JSON.stringify(list[indexActual].record.Status__c));
  
      if ((list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
        okToAdvance = false;
      }
    }


    if (okToAdvance) {
      component.set("v.optionDetailRecordId",bidindex);
      component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
      component.set("v.bidOptionsSize",list.length);
      component.set("v.mainContent","optionsGTReviewSubmit");
    } else if (okToAdvance && !isPreview) {
      component.set('v.showCommunityNote', true);
      component.set('v.modalTitle', 'Invalid Status');
      component.set('v.communityNotes', 'Need to make a change? Contact your Rebel!');
    }
    console.log('done :: okToAdvance :: ' + okToAdvance);



  },
	handleCompare : function(component, event, helper){
		var bidsSelected = [];
		component.get("v.bidOptions").forEach(function(bid){
			if(bid.isCompared) bidsSelected.push(bid);
		});
        console.log(bidsSelected);
		component.set("v.compareList", bidsSelected);
		component.set("v.mainContent", "optionsGTCompare");
	},
    handleBack : function(component, event, helper){
		component.set("v.mainContent", "actions");
	},
    
    handleFilter : function(component, event, helper) {
        var bids = component.get("v.bidOptions");
        var filterByPrice = component.find("filterByPrice").get("v.value");
        
        var bidsFiltered = helper.filterMethod(bids, filterByPrice);
		component.set("v.bidOptionsFiltered", bidsFiltered);
    }
})
```

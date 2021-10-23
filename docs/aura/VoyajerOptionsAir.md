---
layout: default
title: VoyajerOptionsAir
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsAir
## Fields
### VoyajerOptionsAirController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        console.log(component.get('v.source'));
        if (component.get('v.source') === 'preview') {
          callToParent.setParam("action", "loadOptionsAirPreview");
          console.log('using preview');
        } else {
          callToParent.setParam("action", "loadOptionsAir");
          console.log('using non preview');

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
    openOptionDetail: function(component,event,helper){
        var bidindex = event.currentTarget.dataset.bidindex;
        var list = component.get("v.bidOptions");
        component.set("v.optionDetailRecordId",bidindex);
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.bidOptionsSize",list.length);
        component.set("v.mainContent","optionsAirDetail");
    },
    handleShowMessages : function(component, event, helper) {
      component.set('v.showCommunityNote', true);
      var callToParent = component.getEvent("callToParent");
      callToParent.setParam("action","showMessages");
      callToParent.fire();    
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
          console.log(JSON.stringify(bid));
          //console.log(JSON.stringify(recordId));
          if (bid.recordId == recordId) {
            console.log('had a match');
            indexActual = index;
          }
          index++;
        });
  
        console.log('list ::' + JSON.stringify(list[indexActual]));

        if ((list[indexActual].status === "In Contracting" || list[indexActual].status === "Contracted" || list[indexActual].status === "Pending Client Signature")) {
          okToAdvance = false;
        }
      }
  
      if (okToAdvance && !isPreview) {
        component.set('v.openSelectOptionsAlert', true);
        component.set('v.showCommunityNote', true);
        component.set('v.modalTitle', 'Invalid Status');
        component.set('v.communityNotes', 'Need to make a change? Contact your Rebel!');
      } 
  
  
  
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
### VoyajerOptionsAir

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

.THIS .date-info{
	margin-bottom: 1em;    
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
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
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
```
### VoyajerOptionsAir

```
<aura:component>
    <aura:attribute type="String" name="communityNotes" default="" />
    <aura:attribute type="String" name="modalTitle" default="" />
    <aura:attribute type="String" name="source" default="" />
    <aura:attribute type="Boolean" name="showCommunityNote" default="false" /> 
    <aura:attribute type="String" name="airId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="List" name="bidOptionsFiltered" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />
    <aura:attribute type="List" name="compareList" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bidOptions}" action="{!c.loadTable}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>Options
                        </h1>
                        <lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-3">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(and(v.serviceData.endCityName != null, v.serviceData.tripType != 'Round Trip'),' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="text-align:right;">
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
                <div class="pageContentDashboard pageContentDashboard-grey">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1">
                            <div class="slds-grid slds-wrap slds-grid_vertical-align-center">
                                <div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12">
                                    Filter by
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_3-of-12 slds-large-size_3-of-12">
                                    <lightning:select label="Filter" aura:id="filterByPrice" variant="label-hidden" class="slds-form-element-filter label-hidden" onchange="{!c.handleFilter}">
                                        <option value="RRRecomendation" selected="true">Road Rebel Recomendation</option>
                                        <option value="LowToHigh">Price Low to High</option>
                                        <option value="HighToLow">Price High to Low</option>
                                    </lightning:select>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
                                    <lightning:button label="Update" variant="brand" class="btn btn-bluelight" onclick="{!c.doInit}"/>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
                                    <lightning:button label="Clear" variant="neutral" class="btn btn-white" onclick="{!c.loadTable}"/>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard pageContentDashboard-grey" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <section class="slds-grid slds-gutters slds-wrap">
                        <aura:iteration items="{!v.bidOptionsFiltered}" var="bid" indexVar="bidIndex">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3">
                                <article class="slds-card-bid">
                                    <div class="slds-grid slds-gutters slds-wrap">
                                        <div class="slds-col slds-size_1-of-1">
                                            <header class="slds-card-bid_header">
                                                <div class="">
                                                    <h3 style="text-align: center;">{!bid.vendor}</h3>
                                                </div>
                                            </header>                    
                                        </div>                    
                                    </div>
                                    <div class="slds-grid slds-gutters slds-wrap">
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-card-bid-content">
                                                <div>
                                                    <aura:iteration items="{!bid.travels}" var="travel" indexVar="travelIndex">
                                                        <div class="slds-grid slds-gutters slds-wrap" style="text-align:center;margin: 1em 0;">
                                                            <div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-1">
                                                                <span class="info-bluelight">
                                                                    <span>{!travel.dayStart}</span><span style="margin-left:1em;">{!travel.startDate}</span>
                                                                </span>
                                                            </div>
                                                        </div>
                                                        <div class="slds-grid slds-gutters slds-wrap">
                                                            <div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
                                                                <span style="font-size: 2em;">
                                                                    <aura:if isTrue="{!if(v.serviceData.tripType != 'Round Trip',true,false)}">
                                                                        <i class="fas fa-plane icon"></i>
                                                                    </aura:if>
                                                                    <aura:if isTrue="{!if(v.serviceData.tripType == 'Round Trip',true,false)}">
                                                                        <aura:if isTrue="{!if(travelIndex == bid.travelsSize,true,false)}">
                                                                            <i class="fas fa-plane fa-flip-horizontal icon" style="color: green;"></i>
                                                                        </aura:if>
                                                                        <aura:if isTrue="{!if(travelIndex == bid.travelsSize,false,true)}">
                                                                            <i class="fas fa-plane icon"></i>
                                                                        </aura:if>
                                                                    </aura:if>
                                                                </span>
                                                            </div>
                                                            <div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color:#022066">
                                                                <strong style="font-size:1.5em">{!travel.startCity}</strong> <br/>
                                                                {!travel.startDateTime} <br/>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
                                                                <lightning:icon iconName="utility:forward" size="x-small"/>
                                                            </div>
                                                            <div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color:#022066">
                                                                <strong style="font-size:1.5em">{!travel.endCity}</strong> <br/>
                                                                {!travel.endDateTime} <br/>
                                                            </div>
                                                        </div>
                                                        <div class="slds-grid slds-gutters slds-wrap" style="text-align:center;padding: 1em 0;border-bottom:1px solid #eaeaea;">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="border-right: 1px solid #eaeaea;">
                                                                {!travel.flightDuration}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3">
                                                                {!if(travel.stops > 0, travel.stops + ' Stop','Nonstop')}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="border-left: 1px solid #eaeaea;">
                                                                {!if(and(travel.classAir != null,travel.classAir != ''),travel.classAir,'&nbsp;')}
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <aura:if isTrue="{!!empty(bid.deviations)}">
                                                    <div class="slds-grid slds-gutters slds-wrap slds-deviations" style="text-align:center;padding: 1em 0 0 0;">
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="border-right: 1px solid #eaeaea;font-style: italic;color: slateblue; font-weight: bold;">
                                                            <i class="fas fa-exclamation" style="font-size:1em;"></i> <span style="margin-left:0.5em;">Flight Deviations</span>
                                                        </div>
                                                    </div>
                                                </aura:if>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="slds-grid slds-gutters slds-wrap">
                                        <div class="slds-col slds-size_1-of-1">
                                            <footer class="slds-card-bid-footer">
                                                <div class="slds-grid" style="background:content-box#f6f7fc;">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
                                                        <strong style="font-size:13px;color:grey;">Price Per ticket</strong>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
                                                        <strong style="font-size:18px;">${!if(and(bid.totalPrice != null,bid.totalPrice != ''),bid.totalPrice,'0.00')}</strong>
                                                    </div>
                                                </div>
                                                <div class="slds-grid">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center btn-option btn-option-white" style="border-left:1px solid #eaeaea;" data-bidindex="{!bidIndex}" onclick="{!c.openOptionDetail}">
                                                        DETAILS
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center btn-option btn-option-blue" style="border-left:1px solid #eaeaea;" data-bidindex="{!bidIndex}" data-recordid="{!bid.recordId}" onclick="{!c.openReviewSubmit}">
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
### VoyajerOptionsAirHelper

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
### VoyajerOptionsAir

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsAirController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        console.log(component.get('v.source'));
        if (component.get('v.source') === 'preview') {
          callToParent.setParam("action", "loadOptionsAirPreview");
          console.log('using preview');
        } else {
          callToParent.setParam("action", "loadOptionsAir");
          console.log('using non preview');

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
    openOptionDetail: function(component,event,helper){
        var bidindex = event.currentTarget.dataset.bidindex;
        var list = component.get("v.bidOptions");
        component.set("v.optionDetailRecordId",bidindex);
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.bidOptionsSize",list.length);
        component.set("v.mainContent","optionsAirDetail");
    },
    handleShowMessages : function(component, event, helper) {
      component.set('v.showCommunityNote', true);
      var callToParent = component.getEvent("callToParent");
      callToParent.setParam("action","showMessages");
      callToParent.fire();    
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
          console.log(JSON.stringify(bid));
          //console.log(JSON.stringify(recordId));
          if (bid.recordId == recordId) {
            console.log('had a match');
            indexActual = index;
          }
          index++;
        });
  
        console.log('list ::' + JSON.stringify(list[indexActual]));

        if ((list[indexActual].status === "In Contracting" || list[indexActual].status === "Contracted" || list[indexActual].status === "Pending Client Signature")) {
          okToAdvance = false;
        }
      }
  
      if (okToAdvance && !isPreview) {
        component.set('v.openSelectOptionsAlert', true);
        component.set('v.showCommunityNote', true);
        component.set('v.modalTitle', 'Invalid Status');
        component.set('v.communityNotes', 'Need to make a change? Contact your Rebel!');
      } 
  
  
  
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
### VoyajerOptionsAir

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

.THIS .date-info{
	margin-bottom: 1em;    
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
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
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
```
### VoyajerOptionsAir

```
<aura:component>
    <aura:attribute type="String" name="communityNotes" default="" />
    <aura:attribute type="String" name="modalTitle" default="" />
    <aura:attribute type="String" name="source" default="" />
    <aura:attribute type="Boolean" name="showCommunityNote" default="false" /> 
    <aura:attribute type="String" name="airId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="List" name="bidOptionsFiltered" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />
    <aura:attribute type="List" name="compareList" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bidOptions}" action="{!c.loadTable}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>Options
                        </h1>
                        <lightning:button label="Back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom: 1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_2-of-3">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} {!if(and(v.serviceData.endCityName != null, v.serviceData.tripType != 'Round Trip'),' to ' + v.serviceData.endCityName,'')} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                                <!--<p>Trip Type: {!v.serviceData.tripType}</p>-->
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="text-align:right;">
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
                <div class="pageContentDashboard pageContentDashboard-grey">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1">
                            <div class="slds-grid slds-wrap slds-grid_vertical-align-center">
                                <div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12">
                                    Filter by
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_3-of-12 slds-large-size_3-of-12">
                                    <lightning:select label="Filter" aura:id="filterByPrice" variant="label-hidden" class="slds-form-element-filter label-hidden" onchange="{!c.handleFilter}">
                                        <option value="RRRecomendation" selected="true">Road Rebel Recomendation</option>
                                        <option value="LowToHigh">Price Low to High</option>
                                        <option value="HighToLow">Price High to Low</option>
                                    </lightning:select>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
                                    <lightning:button label="Update" variant="brand" class="btn btn-bluelight" onclick="{!c.doInit}"/>
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small">
                                    <lightning:button label="Clear" variant="neutral" class="btn btn-white" onclick="{!c.loadTable}"/>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard pageContentDashboard-grey" style="padding-top:0;border-bottom: 1px solid #dbdbdb;">
                    <section class="slds-grid slds-gutters slds-wrap">
                        <aura:iteration items="{!v.bidOptionsFiltered}" var="bid" indexVar="bidIndex">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3">
                                <article class="slds-card-bid">
                                    <div class="slds-grid slds-gutters slds-wrap">
                                        <div class="slds-col slds-size_1-of-1">
                                            <header class="slds-card-bid_header">
                                                <div class="">
                                                    <h3 style="text-align: center;">{!bid.vendor}</h3>
                                                </div>
                                            </header>                    
                                        </div>                    
                                    </div>
                                    <div class="slds-grid slds-gutters slds-wrap">
                                        <div class="slds-col slds-size_1-of-1">
                                            <div class="slds-card-bid-content">
                                                <div>
                                                    <aura:iteration items="{!bid.travels}" var="travel" indexVar="travelIndex">
                                                        <div class="slds-grid slds-gutters slds-wrap" style="text-align:center;margin: 1em 0;">
                                                            <div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-1">
                                                                <span class="info-bluelight">
                                                                    <span>{!travel.dayStart}</span><span style="margin-left:1em;">{!travel.startDate}</span>
                                                                </span>
                                                            </div>
                                                        </div>
                                                        <div class="slds-grid slds-gutters slds-wrap">
                                                            <div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
                                                                <span style="font-size: 2em;">
                                                                    <aura:if isTrue="{!if(v.serviceData.tripType != 'Round Trip',true,false)}">
                                                                        <i class="fas fa-plane icon"></i>
                                                                    </aura:if>
                                                                    <aura:if isTrue="{!if(v.serviceData.tripType == 'Round Trip',true,false)}">
                                                                        <aura:if isTrue="{!if(travelIndex == bid.travelsSize,true,false)}">
                                                                            <i class="fas fa-plane fa-flip-horizontal icon" style="color: green;"></i>
                                                                        </aura:if>
                                                                        <aura:if isTrue="{!if(travelIndex == bid.travelsSize,false,true)}">
                                                                            <i class="fas fa-plane icon"></i>
                                                                        </aura:if>
                                                                    </aura:if>
                                                                </span>
                                                            </div>
                                                            <div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color:#022066">
                                                                <strong style="font-size:1.5em">{!travel.startCity}</strong> <br/>
                                                                {!travel.startDateTime} <br/>
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6">
                                                                <lightning:icon iconName="utility:forward" size="x-small"/>
                                                            </div>
                                                            <div class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6" style="color:#022066">
                                                                <strong style="font-size:1.5em">{!travel.endCity}</strong> <br/>
                                                                {!travel.endDateTime} <br/>
                                                            </div>
                                                        </div>
                                                        <div class="slds-grid slds-gutters slds-wrap" style="text-align:center;padding: 1em 0;border-bottom:1px solid #eaeaea;">
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="border-right: 1px solid #eaeaea;">
                                                                {!travel.flightDuration}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3">
                                                                {!if(travel.stops > 0, travel.stops + ' Stop','Nonstop')}
                                                            </div>
                                                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3" style="border-left: 1px solid #eaeaea;">
                                                                {!if(and(travel.classAir != null,travel.classAir != ''),travel.classAir,'&nbsp;')}
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <aura:if isTrue="{!!empty(bid.deviations)}">
                                                    <div class="slds-grid slds-gutters slds-wrap slds-deviations" style="text-align:center;padding: 1em 0 0 0;">
                                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="border-right: 1px solid #eaeaea;font-style: italic;color: slateblue; font-weight: bold;">
                                                            <i class="fas fa-exclamation" style="font-size:1em;"></i> <span style="margin-left:0.5em;">Flight Deviations</span>
                                                        </div>
                                                    </div>
                                                </aura:if>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="slds-grid slds-gutters slds-wrap">
                                        <div class="slds-col slds-size_1-of-1">
                                            <footer class="slds-card-bid-footer">
                                                <div class="slds-grid" style="background:content-box#f6f7fc;">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
                                                        <strong style="font-size:13px;color:grey;">Price Per ticket</strong>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center">
                                                        <strong style="font-size:18px;">${!if(and(bid.totalPrice != null,bid.totalPrice != ''),bid.totalPrice,'0.00')}</strong>
                                                    </div>
                                                </div>
                                                <div class="slds-grid">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center btn-option btn-option-white" style="border-left:1px solid #eaeaea;" data-bidindex="{!bidIndex}" onclick="{!c.openOptionDetail}">
                                                        DETAILS
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center btn-option btn-option-blue" style="border-left:1px solid #eaeaea;" data-bidindex="{!bidIndex}" data-recordid="{!bid.recordId}" onclick="{!c.openReviewSubmit}">
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
### VoyajerOptionsAirHelper

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
### VoyajerOptionsAir

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

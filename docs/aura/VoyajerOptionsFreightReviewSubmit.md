---
layout: default
title: VoyajerOptionsFreightReviewSubmit
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsFreightReviewSubmit
## Fields
### VoyajerOptionsFreightReviewSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsFreightReviewSubmitController

```
({
	onInit : function(component, event, helper){
		component.set("v.index", component.get("v.bidIndex"));
	},
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	},
	handleViewAllOptions : function(component, event, helper){
        /*$A.get("e.c:VoyajerCallToParent").setParams({
        	"action" : "mainContent",
        	"data" : {'content' : 'options'}
        }).fire();*/
		component.set("v.content", "all");
	},
    submitSelection: function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","testCommunication");
        var bid = component.get("v.bids")[component.get("v.index")-1].record;
        callToParent.setParam("data",{
            serviceType: "air",
            serviceId: bid.Freight__c,
            serviceName: bid.Freight__r.Name,
            bidVendorName: bid.Vendor__r.Name,
            bidVendorId: bid.Vendor__c,
            bidId: bid.Id,
            comments: component.get("v.comments")
        });
        callToParent.fire();
    }
})
```
### VoyajerOptionsFreightReviewSubmit

```
/*
	Version:	    V1.0
	Create Date:	2/12/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}


/*--------------------
-----BidOption------
----------------------*/

.THIS .slds-card-bidOption_header{
    background-color: #f6f7fc;
}

.THIS .slds-card-bidOption_header .slds-card-bidOption_header_text{
    background-color: white;
    color: #022066;
    font-weight: bold;
}

.THIS .slds-card-bidOption_header .slds-card-bidOption_header_text h3{
    padding: 1rem;
}

.THIS .slds-card-bidOption_item{
    margin-top: .1rem;
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    background-color: #022066;
    transition: transform 0.1s ease;
}

.THIS .slds-card-bidOption_item:hover{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    -webkit-transform: scale(1.01);
    -moz-transform: scale(1.01);
    -o-transform: scale(1.01);
    transform: scale(1.01);
}

.THIS .slds-card-bidOption_item-leftside{
    margin-top: 1.3rem;
    text-align: center;
    color: white;
    font-weight: bold;
}

.THIS .slds-card-bidOption_item-content{
    min-height: 150px;
    background-color: white;
    border-bottom: 1px solid #eaeaea;
}

.THIS .slds-card-bidOption_item-content .slds-card-bidOption_item-content_text{
    margin:1.3rem 0;
    text-align: center;
}

.THIS .slds-card-bidOption_item header{
    margin-top: .5rem;
}

.THIS .slds-card-bidOption_item header h3{
    font-weight: bold;
    color: #022066;
}

.THIS .slds-card-bidOption_item footer{
    background-color: #f6f7fc;
    padding: 1.3rem 1.5rem;
    text-align: right;
}

.THIS .slds-card-bidOption_item footer .totalPrice{
    background-color: #f6f7fc;
}

.THIS .slds-card-bidOption_item footer .totalPrice > span{
    font-weight: bold;
    color: grey;
}

.THIS .slds-card-bidOption_item footer .totalPrice > strong{
    margin-left: .8rem;
    font-weight: bold;
    font-size: 1.4rem;
}

/*--------------------
-----Button------
----------------------*/

.THIS button.btn{
    width: auto;
}

.THIS button.btn-bluelight{
    padding-left: 2rem;
    padding-right: 2rem;
    background-color: #00b4ff;
    border-color: #09b7ff;
}

.THIS button.btn-bluelight:active,
.THIS button.btn-bluelight:visited,
.THIS button.btn-bluelight:focus {
    background-color: #009cf1;
    border-color: #00a4fb;
}

.THIS button.btn-blue{
	margin-left: 1rem !important;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    background-color: #0065ff;
}

.THIS button.btn-blue:active,
.THIS button.btn-blue:visited,
.THIS button.btn-blue:focus {
    background-color: #0453cc;
}

.THIS button.btn-white{
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    border: 1px solid #333;
    color: #333;
}

.THIS .buttonIcon-bluelight{
    color:#00b4ff;
}

.THIS .option_pagination{
    position: relative;
    width: 7rem;
    height: 2.3rem;
    margin-top: .2rem;
    margin-left: 1rem;
    border: 1px solid #09b7ff;
    border-radius: 3em;
    background-color: white;
    text-align: center;
}

.THIS .option_pagination .option_pagination_button-left{
    position: absolute;
    left: 0;
    padding: .4em .5em;
    border-top-left-radius: 3em;
    border-bottom-left-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_button-right{
    position: absolute;
    right: 0;
    padding: .4em .5em;
    border-top-right-radius: 3em;
    border-bottom-right-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_counter{
    display: inline-block;
    margin: .6em;
}

/*--------------------
-----Inputs------
----------------------*/

.THIS .slds-form-element-filter > .slds-form-element__label{
    display: none;
}

.THIS lightning-textarea > .slds-form-element__label{
    display: none;
}

/*--------------------
-----Blocks------
----------------------*/

.THIS .pageContentDashboard-grey{
    background-color: #f0f0f0 !important;
    box-shadow: none !important;
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

/*--------------------
-----Medias queries------
----------------------*/

@media (max-width: 480px){

    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn{
        /*margin: 5px 0 !important;*/
    }

    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: 100%;
        white-space: normal;
    }
}

@media (min-width: 480px){
    
    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn{
        /*margin: 5px 0 !important;*/
    }

    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: 100%;
        white-space: normal;
    }
}

@media (min-width: 768px){
    
    /*--------------------
    -----Button------
    ----------------------*/

    .THIS button.btn{
        width: auto;
        /*margin: 0 5px;*/
    }

    .THIS button.btn-bluelight,
    .THIS button.btn-bluelight:active,
    .THIS button.btn-bluelight:visited,
    .THIS button.btn-bluelight:focus {
        width: 100%;
        white-space: normal;
    }
    
    .THIS button.btn-white,
    .THIS button.btn-white:active,
    .THIS button.btn-white:visited,
    .THIS button.btn-white:focus {
        width: 100%;
        white-space: normal;
    }
}

@media (min-width: 1024px){
    
    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn{
        width: auto;
    }
}
```
### VoyajerOptionsFreightReviewSubmit

```
<aura:component>
    <aura:attribute name="content" type="String"/>
    <aura:attribute name="itinerary" type="Object"/>
    <aura:attribute name="bids" type="List"/>
    <aura:attribute name="bidIndex" type="Integer"/>
    <aura:attribute name="bid" type="Object" access="private"/>
    <aura:attribute type="Integer" name="index" access="private"/>
    <aura:attribute type="String" name="roomRateDate" access="private"/>
    <aura:attribute type="String" name="comments" default="" />
    <ltng:require scripts="{!$Resource.UltimateUtils + '/js/jquery-3.3.1.min.js'}"/>
    
    <aura:handler name="init" value="{!this}" action="{!c.onInit}" />
    <aura:handler name="render" value="{!this}" action="{!c.onRender}"/>
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    <div>
        <lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
        <div class="pageContent" style="min-height:680px;">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">Review &amp; Submit</h1>
                        <lightning:button label="BACK TO OPTIONS" variant="brand" class="btn btn-bluelight" onclick="{!c.handleViewAllOptions}"/>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom:1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i><strong style="color:black;">{!!empty(v.itinerary.Production__r) ? v.itinerary.Production__r.Name : ''}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!(!empty(v.itinerary.Start_city__r) ? ((!empty(v.itinerary.Start_city__r.City__c) ? v.itinerary.Start_city__r.City__c : '') + (!empty(v.itinerary.Start_city__r.State__c) ? ', ' + v.itinerary.Start_city__r.State__c : '')) : '') + ' to ' + (!empty(v.itinerary.End_city__r) ? ((!empty(v.itinerary.End_city__r.City__c) ? v.itinerary.End_city__r.City__c : '') + (!empty(v.itinerary.End_city__r.State__c) ? ', ' + v.itinerary.End_city__r.State__c : '')) : '') + ' | '}<c:auraFormattedDate date="{!v.itinerary.Start_Date__c}" dateFormat="MM/dd/yy"/> - <c:auraFormattedDate date="{!v.itinerary.End_Date__c}" dateFormat="MM/dd/yy"/></p>
                                <p style="margin-right: 0.5em;">Freight Type: {!!empty(v.itinerary.Service_Type__c) ? ' - ' + v.itinerary.Service_Type__c : ''}</p>
                                <p style="margin-right: 0.5em;">Contents: {!!empty(v.itinerary.Freight_Trip_Contents__c) ? ' - ' + v.itinerary.Freight_Trip_Contents__c : ''}</p>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.roomRateDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <section class="page-section slds-card-bidOption">
                        <aura:iteration items="{!v.bids}" var="bid" start="{!v.index - 1}" end="{!v.index}">
                            <header class="slds-grid slds-gutters slds-wrap slds-card-bidOption_header">
                              <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-align_absolute-center" style="text-align:center;">
                                  <div class="slds-media slds-media_responsive">
                                      <div class="slds-media__figure" style="margin-top:10px;margin-right:0;">
                                        <span class="slds-avatar slds-avatar_large">
                                            <img src="{!$Resource.CommunityImages + '/SelectServiceIcons/service_freight_icons_blue.png'}" width="35" title="freight"/>
                                        </span>
                                      </div>
                                  </div>
                              </div>
                              <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-bidOption_header_text">
                                  <h3>
                                      {!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Name : ''}
                                  </h3>
                              </div>
                            </header>
                            <aura:iteration items="{!bid.relatedRecords}" var="subtrip">
                                <aura:if isTrue="{!!empty(subtrip.FreightEquipments__r)}">
                                    <aura:iteration items="{!subtrip.FreightEquipments__r.records}" var="travel" indexVar="i">
                                        <article class="slds-grid slds-gutters slds-wrap slds-card-bidOption_item">
                                          <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-bidOption_item-leftside">
                                              <p><c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="EEE"/></p>
                                              <p style="font-size:2.2em;"><c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="dd"/></p>
                                              <p><c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="MMM"/></p>
                                          </div>
                                          <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-bidOption_item-content">
                                            <div class="slds-grid slds-gutters slds-wrap slds-grid_align-center slds-card-bidOption_item-content_text">
                                                <div class="slds-col slds-size_3-of-12 slds-medium-size_3-of-12" style="margin-bottom:1rem;color:#022066">
                                                    <strong style="font-size:1.4rem;">{!!empty(travel.Location_Details__c) ? travel.Location_Details__c : ''}</strong> <br/>
                                                    {!!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c : ''} <br/>
                                                    {!!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : ''}
                                                </div>
                                                <div class="slds-col slds-grow-none" style="margin-top:.4rem;">
                                                    <lightning:icon iconName="utility:forward" size="x-small"/>
                                                </div>
                                                <div class="slds-col slds-size_3-of-12 slds-medium-size_3-of-12" style="margin-bottom:1rem;color:#022066">
                                                    <strong style="font-size:1.4rem;">{!(!empty(travel.Location_Details_Drop_Off__c) ? travel.Location_Details_Drop_Off__c : '')}</strong> <br/>
                                                    {!!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c : ''} <br/>
                                                    {!!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : ''}
                                                </div>
                                                <div class="slds-col slds-size_5-of-12 slds-medium-size_5-of-12" style="margin-top: 1rem;color:#333;">
                                                    <strong style="font-size:14px">Freight Truck sq ft: </strong> 
                                                    {!!empty(travel.Freight_Truck_Sq_Ft__c) ? travel.Freight_Truck_Sq_Ft__c : ''} 
                                                </div>
                                                <div class="slds-col slds-size_12-of-12 slds-medium-size_12-of-12 slds-grid slds-gutters slds-wrap " style="padding-top:1rem;border-top:1px solid #dbdbdb;color:#333;">
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_1-of-6" style="text-align:right;">
                                                        <strong>PICK UP</strong>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_5-of-6" style="text-align:left;">
                                                        {!(!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c : '') + (!empty(travel.Start_Date_Time_Text__c) ? ' | ' +travel.Start_Date_Time_Text__c : '') + (!empty(travel.Location_Details__c) ? ' from ' + travel.Location_Details__c : '')}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_1-of-6" style="text-align:right;">
                                                        <strong>DROP OFF</strong>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_5-of-6" style="text-align:left;">
                                                        {!(!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c : '') + (!empty(travel.End_Date_Time_Text__c) ? ' | ' +travel.End_Date_Time_Text__c : '') + (!empty(travel.Location_Details_Drop_Off__c) ? ' ' + travel.Location_Details_Drop_Off__c : '')}
                                                    </div>
                                                </div>
                                            </div>
                                            <aura:if isTrue="{!subtrip.FreightEquipments__r.totalSize - 1 == i}">
                                                <footer class="slds-grid slds-gutters slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12"></div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12 totalPrice">
                                                        <span>Total Price</span>
                                                        <aura:if isTrue="{!!empty(bid.record.Rate_Commission__r)}">
                                                            <aura:iteration items="{!bid.record.Rate_Commission__r.records}" var="revenue">
                                                                <strong>${!revenue.Total_Price__c}</strong>
                                                            </aura:iteration>
                                                        </aura:if>
                                                    </div>
                                                </footer>
                                            </aura:if>
                                          </div>
                                        </article>                    
                                    </aura:iteration>
                                </aura:if>
                            </aura:iteration>
                            <footer class="slds-grid slds-gutters slds-wrap" style="padding:1em;">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1 slds-grid slds-gutters slds-wrap" style="color:#333;">
                                    <aura:if isTrue="{!!empty(bid.record.Concessions__r)}">
                                        <aura:iteration items="{!bid.record.Concessions__r.records}" var="concession">
                                            <div class="slds-col slds-size_1-of-2 slds-medium-size_1-of-6" style="text-align:right;">
                                                <strong>{!concession.Concessions_Requested__c}</strong>
                                            </div>
                                            <div class="slds-col slds-size_1-of-2 slds-medium-size_5-of-6">
                                                {!concession.Included_Excluded__c}
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                </div>
                            </footer>
                            <section style="padding: 2em;border-left: 1px solid #dbdbdb;border-bottom: 1px solid #dbdbdb;border-right: 1px solid #dbdbdb;">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="margin-top:1rem;">
                                    <h4><strong style="color:black;">ADITIONAL INFORMATION</strong></h4>
                                    <p style="text-align;justify;">{!!empty(bid.record.Bid_Options_Notes__c) ? bid.record.Bid_Options_Notes__c : ''}</p>
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
                            </section>
                            <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                                <div class="slds-col slds-size_1-of-1" style="text-align: right;">
                                    <lightning:button label="CANCEL" variant="neutral" onclick="{!c.handleViewAllOptions}" />
                                    <lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
                                </div>
                            </div>
                        </aura:iteration>
                    </section>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerOptionsFreightReviewSubmit

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsFreightReviewSubmitController

```
({
	onInit : function(component, event, helper){
		component.set("v.index", component.get("v.bidIndex"));
	},
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	},
	handleViewAllOptions : function(component, event, helper){
        /*$A.get("e.c:VoyajerCallToParent").setParams({
        	"action" : "mainContent",
        	"data" : {'content' : 'options'}
        }).fire();*/
		component.set("v.content", "all");
	},
    submitSelection: function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","testCommunication");
        var bid = component.get("v.bids")[component.get("v.index")-1].record;
        callToParent.setParam("data",{
            serviceType: "air",
            serviceId: bid.Freight__c,
            serviceName: bid.Freight__r.Name,
            bidVendorName: bid.Vendor__r.Name,
            bidVendorId: bid.Vendor__c,
            bidId: bid.Id,
            comments: component.get("v.comments")
        });
        callToParent.fire();
    }
})
```
### VoyajerOptionsFreightReviewSubmit

```
/*
	Version:	    V1.0
	Create Date:	2/12/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}


/*--------------------
-----BidOption------
----------------------*/

.THIS .slds-card-bidOption_header{
    background-color: #f6f7fc;
}

.THIS .slds-card-bidOption_header .slds-card-bidOption_header_text{
    background-color: white;
    color: #022066;
    font-weight: bold;
}

.THIS .slds-card-bidOption_header .slds-card-bidOption_header_text h3{
    padding: 1rem;
}

.THIS .slds-card-bidOption_item{
    margin-top: .1rem;
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    background-color: #022066;
    transition: transform 0.1s ease;
}

.THIS .slds-card-bidOption_item:hover{
    border-top: 1px solid #eaeaea;
    border-bottom: 1px solid #eaeaea;
    -webkit-transform: scale(1.01);
    -moz-transform: scale(1.01);
    -o-transform: scale(1.01);
    transform: scale(1.01);
}

.THIS .slds-card-bidOption_item-leftside{
    margin-top: 1.3rem;
    text-align: center;
    color: white;
    font-weight: bold;
}

.THIS .slds-card-bidOption_item-content{
    min-height: 150px;
    background-color: white;
    border-bottom: 1px solid #eaeaea;
}

.THIS .slds-card-bidOption_item-content .slds-card-bidOption_item-content_text{
    margin:1.3rem 0;
    text-align: center;
}

.THIS .slds-card-bidOption_item header{
    margin-top: .5rem;
}

.THIS .slds-card-bidOption_item header h3{
    font-weight: bold;
    color: #022066;
}

.THIS .slds-card-bidOption_item footer{
    background-color: #f6f7fc;
    padding: 1.3rem 1.5rem;
    text-align: right;
}

.THIS .slds-card-bidOption_item footer .totalPrice{
    background-color: #f6f7fc;
}

.THIS .slds-card-bidOption_item footer .totalPrice > span{
    font-weight: bold;
    color: grey;
}

.THIS .slds-card-bidOption_item footer .totalPrice > strong{
    margin-left: .8rem;
    font-weight: bold;
    font-size: 1.4rem;
}

/*--------------------
-----Button------
----------------------*/

.THIS button.btn{
    width: auto;
}

.THIS button.btn-bluelight{
    padding-left: 2rem;
    padding-right: 2rem;
    background-color: #00b4ff;
    border-color: #09b7ff;
}

.THIS button.btn-bluelight:active,
.THIS button.btn-bluelight:visited,
.THIS button.btn-bluelight:focus {
    background-color: #009cf1;
    border-color: #00a4fb;
}

.THIS button.btn-blue{
	margin-left: 1rem !important;
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    background-color: #0065ff;
}

.THIS button.btn-blue:active,
.THIS button.btn-blue:visited,
.THIS button.btn-blue:focus {
    background-color: #0453cc;
}

.THIS button.btn-white{
    padding-left: 1.5rem;
    padding-right: 1.5rem;
    border: 1px solid #333;
    color: #333;
}

.THIS .buttonIcon-bluelight{
    color:#00b4ff;
}

.THIS .option_pagination{
    position: relative;
    width: 7rem;
    height: 2.3rem;
    margin-top: .2rem;
    margin-left: 1rem;
    border: 1px solid #09b7ff;
    border-radius: 3em;
    background-color: white;
    text-align: center;
}

.THIS .option_pagination .option_pagination_button-left{
    position: absolute;
    left: 0;
    padding: .4em .5em;
    border-top-left-radius: 3em;
    border-bottom-left-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_button-right{
    position: absolute;
    right: 0;
    padding: .4em .5em;
    border-top-right-radius: 3em;
    border-bottom-right-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_counter{
    display: inline-block;
    margin: .6em;
}

/*--------------------
-----Inputs------
----------------------*/

.THIS .slds-form-element-filter > .slds-form-element__label{
    display: none;
}

.THIS lightning-textarea > .slds-form-element__label{
    display: none;
}

/*--------------------
-----Blocks------
----------------------*/

.THIS .pageContentDashboard-grey{
    background-color: #f0f0f0 !important;
    box-shadow: none !important;
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

/*--------------------
-----Medias queries------
----------------------*/

@media (max-width: 480px){

    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn{
        /*margin: 5px 0 !important;*/
    }

    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: 100%;
        white-space: normal;
    }
}

@media (min-width: 480px){
    
    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn{
        /*margin: 5px 0 !important;*/
    }

    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: 100%;
        white-space: normal;
    }
}

@media (min-width: 768px){
    
    /*--------------------
    -----Button------
    ----------------------*/

    .THIS button.btn{
        width: auto;
        /*margin: 0 5px;*/
    }

    .THIS button.btn-bluelight,
    .THIS button.btn-bluelight:active,
    .THIS button.btn-bluelight:visited,
    .THIS button.btn-bluelight:focus {
        width: 100%;
        white-space: normal;
    }
    
    .THIS button.btn-white,
    .THIS button.btn-white:active,
    .THIS button.btn-white:visited,
    .THIS button.btn-white:focus {
        width: 100%;
        white-space: normal;
    }
}

@media (min-width: 1024px){
    
    /*--------------------
    -----Button------
    ----------------------*/
    
    .THIS button.btn{
        width: auto;
    }
}
```
### VoyajerOptionsFreightReviewSubmit

```
<aura:component>
    <aura:attribute name="content" type="String"/>
    <aura:attribute name="itinerary" type="Object"/>
    <aura:attribute name="bids" type="List"/>
    <aura:attribute name="bidIndex" type="Integer"/>
    <aura:attribute name="bid" type="Object" access="private"/>
    <aura:attribute type="Integer" name="index" access="private"/>
    <aura:attribute type="String" name="roomRateDate" access="private"/>
    <aura:attribute type="String" name="comments" default="" />
    <ltng:require scripts="{!$Resource.UltimateUtils + '/js/jquery-3.3.1.min.js'}"/>
    
    <aura:handler name="init" value="{!this}" action="{!c.onInit}" />
    <aura:handler name="render" value="{!this}" action="{!c.onRender}"/>
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    <div>
        <lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
        <div class="pageContent" style="min-height:680px;">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">Review &amp; Submit</h1>
                        <lightning:button label="BACK TO OPTIONS" variant="brand" class="btn btn-bluelight" onclick="{!c.handleViewAllOptions}"/>
                    </div>
                </div>
                <div class="pageContentDashboard" style="border-bottom:1px solid #dbdbdb;">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i><strong style="color:black;">{!!empty(v.itinerary.Production__r) ? v.itinerary.Production__r.Name : ''}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!(!empty(v.itinerary.Start_city__r) ? ((!empty(v.itinerary.Start_city__r.City__c) ? v.itinerary.Start_city__r.City__c : '') + (!empty(v.itinerary.Start_city__r.State__c) ? ', ' + v.itinerary.Start_city__r.State__c : '')) : '') + ' to ' + (!empty(v.itinerary.End_city__r) ? ((!empty(v.itinerary.End_city__r.City__c) ? v.itinerary.End_city__r.City__c : '') + (!empty(v.itinerary.End_city__r.State__c) ? ', ' + v.itinerary.End_city__r.State__c : '')) : '') + ' | '}<c:auraFormattedDate date="{!v.itinerary.Start_Date__c}" dateFormat="MM/dd/yy"/> - <c:auraFormattedDate date="{!v.itinerary.End_Date__c}" dateFormat="MM/dd/yy"/></p>
                                <p style="margin-right: 0.5em;">Freight Type: {!!empty(v.itinerary.Service_Type__c) ? ' - ' + v.itinerary.Service_Type__c : ''}</p>
                                <p style="margin-right: 0.5em;">Contents: {!!empty(v.itinerary.Freight_Trip_Contents__c) ? ' - ' + v.itinerary.Freight_Trip_Contents__c : ''}</p>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.roomRateDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <section class="page-section slds-card-bidOption">
                        <aura:iteration items="{!v.bids}" var="bid" start="{!v.index - 1}" end="{!v.index}">
                            <header class="slds-grid slds-gutters slds-wrap slds-card-bidOption_header">
                              <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-align_absolute-center" style="text-align:center;">
                                  <div class="slds-media slds-media_responsive">
                                      <div class="slds-media__figure" style="margin-top:10px;margin-right:0;">
                                        <span class="slds-avatar slds-avatar_large">
                                            <img src="{!$Resource.CommunityImages + '/SelectServiceIcons/service_freight_icons_blue.png'}" width="35" title="freight"/>
                                        </span>
                                      </div>
                                  </div>
                              </div>
                              <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-bidOption_header_text">
                                  <h3>
                                      {!!empty(bid.record.Vendor__r) ? bid.record.Vendor__r.Name : ''}
                                  </h3>
                              </div>
                            </header>
                            <aura:iteration items="{!bid.relatedRecords}" var="subtrip">
                                <aura:if isTrue="{!!empty(subtrip.FreightEquipments__r)}">
                                    <aura:iteration items="{!subtrip.FreightEquipments__r.records}" var="travel" indexVar="i">
                                        <article class="slds-grid slds-gutters slds-wrap slds-card-bidOption_item">
                                          <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-12 slds-card-bidOption_item-leftside">
                                              <p><c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="EEE"/></p>
                                              <p style="font-size:2.2em;"><c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="dd"/></p>
                                              <p><c:auraFormattedDate date="{!travel.Start_Date__c}" dateFormat="MMM"/></p>
                                          </div>
                                          <div class="slds-col slds-size_1-of-1 slds-medium-size_11-of-12 slds-card-bidOption_item-content">
                                            <div class="slds-grid slds-gutters slds-wrap slds-grid_align-center slds-card-bidOption_item-content_text">
                                                <div class="slds-col slds-size_3-of-12 slds-medium-size_3-of-12" style="margin-bottom:1rem;color:#022066">
                                                    <strong style="font-size:1.4rem;">{!!empty(travel.Location_Details__c) ? travel.Location_Details__c : ''}</strong> <br/>
                                                    {!!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c : ''} <br/>
                                                    {!!empty(travel.Start_Date_Time_Text__c) ? travel.Start_Date_Time_Text__c : ''}
                                                </div>
                                                <div class="slds-col slds-grow-none" style="margin-top:.4rem;">
                                                    <lightning:icon iconName="utility:forward" size="x-small"/>
                                                </div>
                                                <div class="slds-col slds-size_3-of-12 slds-medium-size_3-of-12" style="margin-bottom:1rem;color:#022066">
                                                    <strong style="font-size:1.4rem;">{!(!empty(travel.Location_Details_Drop_Off__c) ? travel.Location_Details_Drop_Off__c : '')}</strong> <br/>
                                                    {!!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c : ''} <br/>
                                                    {!!empty(travel.End_Date_Time_Text__c) ? travel.End_Date_Time_Text__c : ''}
                                                </div>
                                                <div class="slds-col slds-size_5-of-12 slds-medium-size_5-of-12" style="margin-top: 1rem;color:#333;">
                                                    <strong style="font-size:14px">Freight Truck sq ft: </strong> 
                                                    {!!empty(travel.Freight_Truck_Sq_Ft__c) ? travel.Freight_Truck_Sq_Ft__c : ''} 
                                                </div>
                                                <div class="slds-col slds-size_12-of-12 slds-medium-size_12-of-12 slds-grid slds-gutters slds-wrap " style="padding-top:1rem;border-top:1px solid #dbdbdb;color:#333;">
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_1-of-6" style="text-align:right;">
                                                        <strong>PICK UP</strong>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_5-of-6" style="text-align:left;">
                                                        {!(!empty(travel.Start_Date_Text__c) ? travel.Start_Date_Text__c : '') + (!empty(travel.Start_Date_Time_Text__c) ? ' | ' +travel.Start_Date_Time_Text__c : '') + (!empty(travel.Location_Details__c) ? ' from ' + travel.Location_Details__c : '')}
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_1-of-6" style="text-align:right;">
                                                        <strong>DROP OFF</strong>
                                                    </div>
                                                    <div class="slds-col slds-size_1-of-2 slds-medium-size_5-of-6" style="text-align:left;">
                                                        {!(!empty(travel.End_Date_Text__c) ? travel.End_Date_Text__c : '') + (!empty(travel.End_Date_Time_Text__c) ? ' | ' +travel.End_Date_Time_Text__c : '') + (!empty(travel.Location_Details_Drop_Off__c) ? ' ' + travel.Location_Details_Drop_Off__c : '')}
                                                    </div>
                                                </div>
                                            </div>
                                            <aura:if isTrue="{!subtrip.FreightEquipments__r.totalSize - 1 == i}">
                                                <footer class="slds-grid slds-gutters slds-wrap">
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12"></div>
                                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_6-of-12 totalPrice">
                                                        <span>Total Price</span>
                                                        <aura:if isTrue="{!!empty(bid.record.Rate_Commission__r)}">
                                                            <aura:iteration items="{!bid.record.Rate_Commission__r.records}" var="revenue">
                                                                <strong>${!revenue.Total_Price__c}</strong>
                                                            </aura:iteration>
                                                        </aura:if>
                                                    </div>
                                                </footer>
                                            </aura:if>
                                          </div>
                                        </article>                    
                                    </aura:iteration>
                                </aura:if>
                            </aura:iteration>
                            <footer class="slds-grid slds-gutters slds-wrap" style="padding:1em;">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1 slds-grid slds-gutters slds-wrap" style="color:#333;">
                                    <aura:if isTrue="{!!empty(bid.record.Concessions__r)}">
                                        <aura:iteration items="{!bid.record.Concessions__r.records}" var="concession">
                                            <div class="slds-col slds-size_1-of-2 slds-medium-size_1-of-6" style="text-align:right;">
                                                <strong>{!concession.Concessions_Requested__c}</strong>
                                            </div>
                                            <div class="slds-col slds-size_1-of-2 slds-medium-size_5-of-6">
                                                {!concession.Included_Excluded__c}
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                </div>
                            </footer>
                            <section style="padding: 2em;border-left: 1px solid #dbdbdb;border-bottom: 1px solid #dbdbdb;border-right: 1px solid #dbdbdb;">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="margin-top:1rem;">
                                    <h4><strong style="color:black;">ADITIONAL INFORMATION</strong></h4>
                                    <p style="text-align;justify;">{!!empty(bid.record.Bid_Options_Notes__c) ? bid.record.Bid_Options_Notes__c : ''}</p>
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
                            </section>
                            <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                                <div class="slds-col slds-size_1-of-1" style="text-align: right;">
                                    <lightning:button label="CANCEL" variant="neutral" onclick="{!c.handleViewAllOptions}" />
                                    <lightning:button label="SUBMIT" variant="brand" class="formButtonBrand" onclick="{!c.submitSelection}" />
                                </div>
                            </div>
                        </aura:iteration>
                    </section>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```

---
layout: default
title: VoyajerOptionsFreight
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsFreight
## Fields
### VoyajerOptionsFreight

```
/*
	Version:	    V1.0
	Create Date:	2/11/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}

/*--------------------
-----Bid------
----------------------*/

.THIS .slds-card-bid{
    margin-top: .8rem;
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
    /*height: 154px;*/
    background-color: white;
    overflow-y: auto;
    /*padding: 16px;*/
    padding: 0 16px 16px 16px;
    word-wrap: break-word;/*warp*/
}

.THIS .slds-card-bid-footer{
    background-color: white;
    padding-bottom: 10px;
}

.THIS .slds-card-bid-footer > .slds-grid{
    min-height: 3.2em;
}

/*--------------------
-----Button------
----------------------*/

.THIS button.btn{
}

.THIS button.btn-bluelight{
    background-color: #00b4ff;
    border-color: #09b7ff;
}

.THIS .buttonIcon-bluelight{
    color: #00b4ff;
}

.THIS .btn-option{
    padding: 1em .75em;
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
        margin: 5px 0;
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
        margin: 5px 0;
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
    
    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: auto;
        margin: 0 5px;
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

    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: auto;
    }
}
```
### VoyajerOptionsFreight

```
<aura:component controller="VoyajerOptionsFreightController">
  <aura:attribute name="mainContent" type="String" />
  <aura:attribute
    name="itinerarySelected"
    type="String"
    default="a0C5600000W2plPEAR"
  />
  <aura:attribute name="data" type="Map" access="private" />
  <aura:attribute name="bids" type="List" access="private" />
  <aura:attribute name="bidsSelected" type="List" access="private" />
  <aura:attribute name="content" type="String" default="all" access="private" />
  <aura:attribute name="itinerary" type="Object" access="private" />
  <aura:attribute name="bidIndex" type="Integer" access="private" />
  <ltng:require
    scripts="{!$Resource.UltimateUtils + '/js/jquery-3.3.1.min.js'}"
  />

  <aura:handler name="init" value="{!this}" action="{!c.onInit}" />
  <aura:handler name="render" value="{!this}" action="{!c.onRender}" />
  <div>
    <lightning:spinner
      aura:id="loading"
      alternativeText="Loading"
      size="large"
    />
    <div class="pageContent" style="min-height: 680px">
      <aura:if isTrue="{!v.content == 'all'}">
        <div class="pageContentSpaces">
          <div class="page-section">
            <div class="page-header">
              <h1 class="page-header-title">Options</h1>
              <lightning:button
                label="Back"
                variant="brand"
                class="formButtonBrandLight"
                onclick="{!c.handleBack}"
              />
            </div>
          </div>
          <div
            class="pageContentDashboard"
            style="border-bottom: 1px solid #dbdbdb"
          >
            <div class="page-section">
              <div class="slds-grid slds-gutters slds-wrap">
                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                  <h3>
                    <i
                      class="fas fa-shield-alt"
                      style="color: #9f9f9f; margin-right: 0.5em"
                    ></i
                    ><strong style="color: black"
                      >{!!empty(v.data.itinerary.Production__r) ?
                      v.data.itinerary.Production__r.Name : ''}</strong
                    >
                  </h3>
                  <p
                    style="
                      margin-right: 0.5em;
                      font-weight: bold;
                      color: #00b4ff;
                    "
                  >
                    {!(!empty(v.data.itinerary.Start_city__r) ?
                    ((!empty(v.data.itinerary.Start_city__r.City__c) ?
                    v.data.itinerary.Start_city__r.City__c : '') +
                    (!empty(v.data.itinerary.Start_city__r.State__c) ? ', ' +
                    v.data.itinerary.Start_city__r.State__c : '')) : '') + ' to
                    ' + (!empty(v.data.itinerary.End_city__r) ?
                    ((!empty(v.data.itinerary.End_city__r.City__c) ?
                    v.data.itinerary.End_city__r.City__c : '') +
                    (!empty(v.data.itinerary.End_city__r.State__c) ? ', ' +
                    v.data.itinerary.End_city__r.State__c : '')) : '') + ' | ' +
                    (!empty(v.data.itinerary.Start_Date__c) ?
                    v.data.itinerary.Start_Date__c : '') +
                    (!empty(v.data.itinerary.End_Date__c) ? ' - ' +
                    v.data.itinerary.End_Date__c : '')}
                  </p>
                  <p style="margin-right: 0.5em">
                    Freight Type: {!!empty(v.data.itinerary.Service_Type__c) ?
                    v.data.itinerary.Service_Type__c : ''}
                  </p>
                  <p style="margin-right: 0.5em">
                    Contents:
                    {!!empty(v.data.itinerary.Freight_Trip_Contents__c) ?
                    v.data.itinerary.Freight_Trip_Contents__c : ''}
                  </p>
                </div>
                <div
                  class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2"
                  style="text-align: right"
                >
                  <div class="box-decisionBy">DECISION BY <br /></div>
                </div>
              </div>
            </div>
          </div>
          <div
            class="pageContentDashboard pageContentDashboard-grey"
            style="border-bottom: 1px solid #dbdbdb"
          >
            <div class="slds-grid slds-wrap">
              <div class="slds-col slds-size_1-of-1">
                <div
                  class="slds-grid slds-wrap slds-grid_vertical-align-center"
                >
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12"
                  >
                    Filter by
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_3-of-12 slds-large-size_3-of-12"
                  >
                    <lightning:select
                      aura:id="filterBy"
                      variant="label-hidden"
                      class="slds-form-element-filter"
                    >
                      <!--<option value="default">Default</option>-->
                      <option value="RRRecomendation" selected="true">
                        Road Rebel Recomendation
                      </option>
                      <option value="lowToHigh">Price Low to High</option>
                      <option value="highToLow">Price High to Low</option>
                    </lightning:select>
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
                  >
                    <lightning:button
                      label="Update"
                      variant="brand"
                      class="btn btn-bluelight"
                      onclick="{!c.handleUpdate}"
                    />
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
                  >
                    <lightning:button
                      label="Clear"
                      variant="neutral"
                      class="btn btn-white"
                      onclick="{!c.handleClear}"
                    />
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_4-of-12 slds-large-size_6-of-12 slds-p-horizontal_x-small"
                    style="margin: 0; text-align: right"
                  >
                    <lightning:button
                      label="Compare"
                      variant="brand"
                      class="btn"
                      onclick="{!c.handleCompare}"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div
            class="pageContentDashboard pageContentDashboard-grey"
            style="padding-top: 0; border-bottom: 1px solid #dbdbdb"
          >
            <section class="slds-grid slds-gutters slds-wrap">
              <aura:iteration
                items="{!v.data.bidOptions}"
                var="bid"
                indexVar="index"
              >
                <div
                  class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3"
                >
                  <article class="slds-card-bid">
                    <div class="slds-grid slds-gutters slds-wrap">
                      <div class="slds-col slds-size_1-of-1">
                        <header class="slds-card-bid_header">
                          <div class="">
                            <h3 style="text-align: center">
                              {!!empty(bid.record.Vendor__r) ?
                              bid.record.Vendor__r.Name : ''}
                            </h3>
                          </div>
                        </header>
                      </div>
                    </div>
                    <div class="slds-grid slds-gutters slds-wrap">
                      <div class="slds-col slds-size_1-of-1">
                        <div class="slds-card-bid-content">
                          <aura:iteration
                            items="{!bid.relatedRecords}"
                            var="subtrip"
                          >
                            <aura:if
                              isTrue="{!!empty(subtrip.FreightEquipments__r)}"
                            >
                              <aura:iteration
                                items="{!subtrip.FreightEquipments__r.records}"
                                var="travel"
                              >
                                <div
                                  class="slds-grid slds-gutters slds-wrap"
                                  style="border-bottom: 1px solid #eaeaea"
                                >
                                  <div
                                    class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6"
                                  >
                                    <div
                                      class="slds-media slds-media_responsive"
                                    >
                                      <div
                                        class="slds-media__figure"
                                        style="margin-right: 0"
                                      >
                                        <span
                                          class="slds-avatar slds-avatar_large"
                                        >
                                          <img
                                            src="{!$Resource.CommunityImages + '/SelectServiceIcons/service_freight_icons_blue.png'}"
                                            width="35"
                                            title="freight"
                                          />
                                        </span>
                                      </div>
                                    </div>
                                  </div>
                                  <div
                                    class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6"
                                    style="color: #022066"
                                  >
                                    <strong style="font-size: 14px"
                                      >{!!empty(travel.Location_Details__c) ?
                                      travel.Location_Details__c : ''}</strong
                                    >
                                    <br /> {!!empty(travel.Start_Date_Text__c) ?
                                    travel.Start_Date_Text__c : ''} <br />
                                    {!!empty(travel.Start_Date_Time_Text__c) ?
                                    travel.Start_Date_Time_Text__c : ''}
                                  </div>
                                  <div
                                    class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6"
                                  >
                                    <lightning:icon
                                      iconName="utility:forward"
                                      size="x-small"
                                    />
                                  </div>
                                  <div
                                    class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6"
                                    style="color: #022066"
                                  >
                                    <strong style="font-size: 14px"
                                      >{!(!empty(travel.Location_Details_Drop_Off__c)
                                      ? travel.Location_Details_Drop_Off__c :
                                      '')}</strong
                                    >
                                    <br /> {!!empty(travel.End_Date_Text__c) ?
                                    travel.End_Date_Text__c : ''} <br />
                                    {!!empty(travel.End_Date_Time_Text__c) ?
                                    travel.End_Date_Time_Text__c : ''}
                                  </div>
                                </div>
                              </aura:iteration>
                            </aura:if>
                          </aura:iteration>
                        </div>
                      </div>
                    </div>
                    <div class="slds-grid slds-gutters slds-wrap">
                      <div class="slds-col slds-size_1-of-1">
                        <footer class="slds-card-bid-footer">
                          <div
                            class="slds-grid slds-wrap"
                            style="background: content-box#f6f7fc"
                          >
                            <div
                              class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center"
                            >
                              <strong style="font-size: 14px; color: grey"
                                >Total Price</strong
                              >
                            </div>
                            <div
                              class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center"
                            >
                              <aura:if
                                isTrue="{!!empty(bid.record.Rate_Commission__r)}"
                              >
                                <aura:iteration
                                  items="{!bid.record.Rate_Commission__r.records}"
                                  var="revenue"
                                >
                                  <strong style="font-size: 18px"
                                    >${!revenue.Total_Price__c}</strong
                                  >
                                </aura:iteration>
                              </aura:if>
                            </div>
                          </div>
                          <div class="slds-grid slds-wrap">
                            <div
                              class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
                            >
                              <lightning:input
                                type="checkbox-button"
                                label="COMPARE"
                                checked="{!bid.isCompared}"
                              /><span>COMPARE</span>
                            </div>
                            <div
                              class="slds-col slds-size_1-of-2 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
                              style="
                                border-left: 1px solid #eaeaea;
                                color: #00b4ff;
                              "
                              data-content="details"
                              data-index="{!index}"
                              onclick="{!c.handleContent}"
                            >
                              DETAILS
                            </div>

                            <div
                              class="slds-col slds-size_1-of-2 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-blue"
                              style="border-left: 1px solid #eaeaea"
                              data-content="reviewsubmit"
                              data-index="{!index}"
                              onclick="{!c.handleContent}"
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
        <aura:set attribute="else">
          <aura:if isTrue="{!v.content == 'details'}">
            <c:VoyajerOptionsFreightDetails
              content="{!v.content}"
              itinerary="{#v.itinerary}"
              bids="{#v.data.bidOptions}"
              bidIndex="{#v.bidIndex + 1}"
            />
            <aura:set attribute="else">
              <aura:if isTrue="{!v.content == 'compare'}">
                <c:VoyajerOptionsFreightCompare
                  content="{!v.content}"
                  itinerary="{#v.itinerary}"
                  bidsSelected="{#v.bidsSelected}"
                />
                <aura:set attribute="else">
                  <aura:if isTrue="{!v.content == 'reviewsubmit'}">
                    <c:VoyajerOptionsFreightReviewSubmit
                      content="{!v.content}"
                      itinerary="{#v.itinerary}"
                      bids="{#v.data.bidOptions}"
                      bidIndex="{#v.bidIndex + 1}"
                    />
                  </aura:if>
                </aura:set>
              </aura:if>
            </aura:set>
          </aura:if>
        </aura:set>
      </aura:if>
    </div>
  </div>
</aura:component>
```
### VoyajerOptionsFreight

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsFreightController

```
({
	onInit : function(component, event, helper){
		helper.getData(component, "searchBidOptions");
	},
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	},
	handleBack : function(component, event, helper){
		component.set("v.mainContent", "actions");
	},
	handleUpdate : function(component, event, helper){
		if(component.find("filterBy").get("v.value") == "default"){
			component.get("v.data").bidOptions = component.get("v.bids");
			component.set("v.data", component.get("v.data"));
		}
		else helper.sortData(component, component.find("filterBy").get("v.value"));
	},
	handleClear : function(component, event, helper){
		component.find('filterBy').set("v.value", "default");
		component.get("v.data").bidOptions = component.get("v.bids");
		component.set("v.data", component.get("v.data"));
	},
	handleCompare : function(component, event, helper){
		var bidsSelected = [];
		var optionsCompared = 0;
		component.get("v.data").bidOptions.forEach(function(bid){
			if(bid.isCompared){bidsSelected.push(bid);optionsCompared++;}
		});
		if(optionsCompared > 0 && optionsCompared < 4){
			component.set("v.itinerary", component.get("v.data").itinerary);
			component.set("v.bidsSelected", bidsSelected);
			component.set("v.content", "compare");
		}
		else{
			var toastEvent = $A.get("e.force:showToast");
			toastEvent.setParams({
				"title": "Message",
				"message": optionsCompared == 0 ? " Please you must select at least one option." : optionsCompared > 3 ? " You can compare up to 3 options." : ""
			}).fire();
		}
	},
	handleContent : function(component, event, helper){
		component.set("v.itinerary", component.get("v.data").itinerary);
		component.set("v.bidIndex", $(event.currentTarget).data('index'));
		component.set("v.content", $(event.currentTarget).data('content'));
	}
})
```
### VoyajerOptionsFreightHelper

```
({
	getData : function(component, method){
		var action = component.get("c." + method);
		if(method == "searchBidOptions") action.setParams({itineraryId: component.get("v.itinerarySelected")});
		action.setCallback(this, function(response){
			var state = response.getState();
			if(state === "SUCCESS"){
				var result = JSON.parse(response.getReturnValue());
				if(method == "searchBidOptions"){
					component.set("v.data", result);
					component.set("v.bids", result.bidOptions);
				}
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
		$A.util.removeClass(component.find("loading"), "slds-hide");
		$A.enqueueAction(action);
	},
	sortData : function(component, filterBy){
		var bidsMap = component.get("v.data").bidOptions.map(function(bid, i){
		  return {index : i, value : bid};
		})
		bidsMap.sort(function(element1, element2){
			if(filterBy == "RRRecomendation"){
                if(!$A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)){
					if(!$A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)) return element1.value.record.Options__c - element2.value.record.Options__c;
					else if($A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)) return 1;
					else if(!$A.util.isEmpty(element1.value.record.Options__c) && $A.util.isEmpty(element2.value.record.Options__c)) return -1;
					return 0;
				}
				else if($A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)) return 1;
				else if(!$A.util.isEmpty(element1.value.record.Options__c) && $A.util.isEmpty(element2.value.record.Options__c)) return -1;
			}
			else if(filterBy == "lowToHigh"){
				if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)){
					if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return element1.value.record.Rate_Commission__r.records[0].Total_Price__c - element2.value.record.Rate_Commission__r.records[0].Total_Price__c;
					else if($A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return 1;
					else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && $A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return -1;
					return 0;
				}
				else if($A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)) return 1;
				else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && $A.util.isEmpty(element2.value.record.Rate_Commission__r)) return -1;
			}
			else if(filterBy == "highToLow"){
				if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)){
					if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return element2.value.record.Rate_Commission__r.records[0].Total_Price__c - element1.value.record.Rate_Commission__r.records[0].Total_Price__c;
					else if($A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return 1;
					else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && $A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return -1;
					return 0;
				}
				else if($A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)) return 1;
				else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && $A.util.isEmpty(element2.value.record.Rate_Commission__r)) return -1;
			}
			return 0;
		});
		var bidsSorted = bidsMap.map(function(element, j){
			return component.get("v.data").bidOptions[element.index];
		});	
		component.get("v.data").bidOptions = bidsSorted;
		component.set("v.data", component.get("v.data"));
	},
})
```
### VoyajerOptionsFreight

```
/*
	Version:	    V1.0
	Create Date:	2/11/2020
*/

/*--------------------
-----All------
----------------------*/

.THIS{
    background-color: #f0f0f0;
}

/*--------------------
-----Bid------
----------------------*/

.THIS .slds-card-bid{
    margin-top: .8rem;
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
    /*height: 154px;*/
    background-color: white;
    overflow-y: auto;
    /*padding: 16px;*/
    padding: 0 16px 16px 16px;
    word-wrap: break-word;/*warp*/
}

.THIS .slds-card-bid-footer{
    background-color: white;
    padding-bottom: 10px;
}

.THIS .slds-card-bid-footer > .slds-grid{
    min-height: 3.2em;
}

/*--------------------
-----Button------
----------------------*/

.THIS button.btn{
}

.THIS button.btn-bluelight{
    background-color: #00b4ff;
    border-color: #09b7ff;
}

.THIS .buttonIcon-bluelight{
    color: #00b4ff;
}

.THIS .btn-option{
    padding: 1em .75em;
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
        margin: 5px 0;
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
        margin: 5px 0;
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
    
    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: auto;
        margin: 0 5px;
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

    .THIS button.btn,
    .THIS button.btn:active,
    .THIS button.btn:visited,
    .THIS button.btn:focus {
        width: auto;
    }
}
```
### VoyajerOptionsFreight

```
<aura:component controller="VoyajerOptionsFreightController">
  <aura:attribute name="mainContent" type="String" />
  <aura:attribute
    name="itinerarySelected"
    type="String"
    default="a0C5600000W2plPEAR"
  />
  <aura:attribute name="data" type="Map" access="private" />
  <aura:attribute name="bids" type="List" access="private" />
  <aura:attribute name="bidsSelected" type="List" access="private" />
  <aura:attribute name="content" type="String" default="all" access="private" />
  <aura:attribute name="itinerary" type="Object" access="private" />
  <aura:attribute name="bidIndex" type="Integer" access="private" />
  <ltng:require
    scripts="{!$Resource.UltimateUtils + '/js/jquery-3.3.1.min.js'}"
  />

  <aura:handler name="init" value="{!this}" action="{!c.onInit}" />
  <aura:handler name="render" value="{!this}" action="{!c.onRender}" />
  <div>
    <lightning:spinner
      aura:id="loading"
      alternativeText="Loading"
      size="large"
    />
    <div class="pageContent" style="min-height: 680px">
      <aura:if isTrue="{!v.content == 'all'}">
        <div class="pageContentSpaces">
          <div class="page-section">
            <div class="page-header">
              <h1 class="page-header-title">Options</h1>
              <lightning:button
                label="Back"
                variant="brand"
                class="formButtonBrandLight"
                onclick="{!c.handleBack}"
              />
            </div>
          </div>
          <div
            class="pageContentDashboard"
            style="border-bottom: 1px solid #dbdbdb"
          >
            <div class="page-section">
              <div class="slds-grid slds-gutters slds-wrap">
                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                  <h3>
                    <i
                      class="fas fa-shield-alt"
                      style="color: #9f9f9f; margin-right: 0.5em"
                    ></i
                    ><strong style="color: black"
                      >{!!empty(v.data.itinerary.Production__r) ?
                      v.data.itinerary.Production__r.Name : ''}</strong
                    >
                  </h3>
                  <p
                    style="
                      margin-right: 0.5em;
                      font-weight: bold;
                      color: #00b4ff;
                    "
                  >
                    {!(!empty(v.data.itinerary.Start_city__r) ?
                    ((!empty(v.data.itinerary.Start_city__r.City__c) ?
                    v.data.itinerary.Start_city__r.City__c : '') +
                    (!empty(v.data.itinerary.Start_city__r.State__c) ? ', ' +
                    v.data.itinerary.Start_city__r.State__c : '')) : '') + ' to
                    ' + (!empty(v.data.itinerary.End_city__r) ?
                    ((!empty(v.data.itinerary.End_city__r.City__c) ?
                    v.data.itinerary.End_city__r.City__c : '') +
                    (!empty(v.data.itinerary.End_city__r.State__c) ? ', ' +
                    v.data.itinerary.End_city__r.State__c : '')) : '') + ' | ' +
                    (!empty(v.data.itinerary.Start_Date__c) ?
                    v.data.itinerary.Start_Date__c : '') +
                    (!empty(v.data.itinerary.End_Date__c) ? ' - ' +
                    v.data.itinerary.End_Date__c : '')}
                  </p>
                  <p style="margin-right: 0.5em">
                    Freight Type: {!!empty(v.data.itinerary.Service_Type__c) ?
                    v.data.itinerary.Service_Type__c : ''}
                  </p>
                  <p style="margin-right: 0.5em">
                    Contents:
                    {!!empty(v.data.itinerary.Freight_Trip_Contents__c) ?
                    v.data.itinerary.Freight_Trip_Contents__c : ''}
                  </p>
                </div>
                <div
                  class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2"
                  style="text-align: right"
                >
                  <div class="box-decisionBy">DECISION BY <br /></div>
                </div>
              </div>
            </div>
          </div>
          <div
            class="pageContentDashboard pageContentDashboard-grey"
            style="border-bottom: 1px solid #dbdbdb"
          >
            <div class="slds-grid slds-wrap">
              <div class="slds-col slds-size_1-of-1">
                <div
                  class="slds-grid slds-wrap slds-grid_vertical-align-center"
                >
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_1-of-12 slds-large-size_1-of-12"
                  >
                    Filter by
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_3-of-3 slds-medium-size_3-of-12 slds-large-size_3-of-12"
                  >
                    <lightning:select
                      aura:id="filterBy"
                      variant="label-hidden"
                      class="slds-form-element-filter"
                    >
                      <!--<option value="default">Default</option>-->
                      <option value="RRRecomendation" selected="true">
                        Road Rebel Recomendation
                      </option>
                      <option value="lowToHigh">Price Low to High</option>
                      <option value="highToLow">Price High to Low</option>
                    </lightning:select>
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
                  >
                    <lightning:button
                      label="Update"
                      variant="brand"
                      class="btn btn-bluelight"
                      onclick="{!c.handleUpdate}"
                    />
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_2-of-12 slds-large-size_1-of-12 slds-p-horizontal_x-small"
                  >
                    <lightning:button
                      label="Clear"
                      variant="neutral"
                      class="btn btn-white"
                      onclick="{!c.handleClear}"
                    />
                  </div>
                  <div
                    class="slds-col slds-size_1-of-1 slds-small-size_1-of-3 slds-medium-size_4-of-12 slds-large-size_6-of-12 slds-p-horizontal_x-small"
                    style="margin: 0; text-align: right"
                  >
                    <lightning:button
                      label="Compare"
                      variant="brand"
                      class="btn"
                      onclick="{!c.handleCompare}"
                    />
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div
            class="pageContentDashboard pageContentDashboard-grey"
            style="padding-top: 0; border-bottom: 1px solid #dbdbdb"
          >
            <section class="slds-grid slds-gutters slds-wrap">
              <aura:iteration
                items="{!v.data.bidOptions}"
                var="bid"
                indexVar="index"
              >
                <div
                  class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-large-size_1-of-3"
                >
                  <article class="slds-card-bid">
                    <div class="slds-grid slds-gutters slds-wrap">
                      <div class="slds-col slds-size_1-of-1">
                        <header class="slds-card-bid_header">
                          <div class="">
                            <h3 style="text-align: center">
                              {!!empty(bid.record.Vendor__r) ?
                              bid.record.Vendor__r.Name : ''}
                            </h3>
                          </div>
                        </header>
                      </div>
                    </div>
                    <div class="slds-grid slds-gutters slds-wrap">
                      <div class="slds-col slds-size_1-of-1">
                        <div class="slds-card-bid-content">
                          <aura:iteration
                            items="{!bid.relatedRecords}"
                            var="subtrip"
                          >
                            <aura:if
                              isTrue="{!!empty(subtrip.FreightEquipments__r)}"
                            >
                              <aura:iteration
                                items="{!subtrip.FreightEquipments__r.records}"
                                var="travel"
                              >
                                <div
                                  class="slds-grid slds-gutters slds-wrap"
                                  style="border-bottom: 1px solid #eaeaea"
                                >
                                  <div
                                    class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6"
                                  >
                                    <div
                                      class="slds-media slds-media_responsive"
                                    >
                                      <div
                                        class="slds-media__figure"
                                        style="margin-right: 0"
                                      >
                                        <span
                                          class="slds-avatar slds-avatar_large"
                                        >
                                          <img
                                            src="{!$Resource.CommunityImages + '/SelectServiceIcons/service_freight_icons_blue.png'}"
                                            width="35"
                                            title="freight"
                                          />
                                        </span>
                                      </div>
                                    </div>
                                  </div>
                                  <div
                                    class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6"
                                    style="color: #022066"
                                  >
                                    <strong style="font-size: 14px"
                                      >{!!empty(travel.Location_Details__c) ?
                                      travel.Location_Details__c : ''}</strong
                                    >
                                    <br /> {!!empty(travel.Start_Date_Text__c) ?
                                    travel.Start_Date_Text__c : ''} <br />
                                    {!!empty(travel.Start_Date_Time_Text__c) ?
                                    travel.Start_Date_Time_Text__c : ''}
                                  </div>
                                  <div
                                    class="slds-col slds-size_1-of-6 slds-medium-size_1-of-6"
                                  >
                                    <lightning:icon
                                      iconName="utility:forward"
                                      size="x-small"
                                    />
                                  </div>
                                  <div
                                    class="slds-col slds-size_2-of-6 slds-medium-size_2-of-6"
                                    style="color: #022066"
                                  >
                                    <strong style="font-size: 14px"
                                      >{!(!empty(travel.Location_Details_Drop_Off__c)
                                      ? travel.Location_Details_Drop_Off__c :
                                      '')}</strong
                                    >
                                    <br /> {!!empty(travel.End_Date_Text__c) ?
                                    travel.End_Date_Text__c : ''} <br />
                                    {!!empty(travel.End_Date_Time_Text__c) ?
                                    travel.End_Date_Time_Text__c : ''}
                                  </div>
                                </div>
                              </aura:iteration>
                            </aura:if>
                          </aura:iteration>
                        </div>
                      </div>
                    </div>
                    <div class="slds-grid slds-gutters slds-wrap">
                      <div class="slds-col slds-size_1-of-1">
                        <footer class="slds-card-bid-footer">
                          <div
                            class="slds-grid slds-wrap"
                            style="background: content-box#f6f7fc"
                          >
                            <div
                              class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center"
                            >
                              <strong style="font-size: 14px; color: grey"
                                >Total Price</strong
                              >
                            </div>
                            <div
                              class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2 slds-align_absolute-center"
                            >
                              <aura:if
                                isTrue="{!!empty(bid.record.Rate_Commission__r)}"
                              >
                                <aura:iteration
                                  items="{!bid.record.Rate_Commission__r.records}"
                                  var="revenue"
                                >
                                  <strong style="font-size: 18px"
                                    >${!revenue.Total_Price__c}</strong
                                  >
                                </aura:iteration>
                              </aura:if>
                            </div>
                          </div>
                          <div class="slds-grid slds-wrap">
                            <div
                              class="slds-col slds-size_1-of-1 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
                            >
                              <lightning:input
                                type="checkbox-button"
                                label="COMPARE"
                                checked="{!bid.isCompared}"
                              /><span>COMPARE</span>
                            </div>
                            <div
                              class="slds-col slds-size_1-of-2 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-white"
                              style="
                                border-left: 1px solid #eaeaea;
                                color: #00b4ff;
                              "
                              data-content="details"
                              data-index="{!index}"
                              onclick="{!c.handleContent}"
                            >
                              DETAILS
                            </div>

                            <div
                              class="slds-col slds-size_1-of-2 slds-medium-size_1-of-3 slds-align_absolute-center btn-option btn-option-blue"
                              style="border-left: 1px solid #eaeaea"
                              data-content="reviewsubmit"
                              data-index="{!index}"
                              onclick="{!c.handleContent}"
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
        <aura:set attribute="else">
          <aura:if isTrue="{!v.content == 'details'}">
            <c:VoyajerOptionsFreightDetails
              content="{!v.content}"
              itinerary="{#v.itinerary}"
              bids="{#v.data.bidOptions}"
              bidIndex="{#v.bidIndex + 1}"
            />
            <aura:set attribute="else">
              <aura:if isTrue="{!v.content == 'compare'}">
                <c:VoyajerOptionsFreightCompare
                  content="{!v.content}"
                  itinerary="{#v.itinerary}"
                  bidsSelected="{#v.bidsSelected}"
                />
                <aura:set attribute="else">
                  <aura:if isTrue="{!v.content == 'reviewsubmit'}">
                    <c:VoyajerOptionsFreightReviewSubmit
                      content="{!v.content}"
                      itinerary="{#v.itinerary}"
                      bids="{#v.data.bidOptions}"
                      bidIndex="{#v.bidIndex + 1}"
                    />
                  </aura:if>
                </aura:set>
              </aura:if>
            </aura:set>
          </aura:if>
        </aura:set>
      </aura:if>
    </div>
  </div>
</aura:component>
```
### VoyajerOptionsFreight

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsFreightController

```
({
	onInit : function(component, event, helper){
		helper.getData(component, "searchBidOptions");
	},
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	},
	handleBack : function(component, event, helper){
		component.set("v.mainContent", "actions");
	},
	handleUpdate : function(component, event, helper){
		if(component.find("filterBy").get("v.value") == "default"){
			component.get("v.data").bidOptions = component.get("v.bids");
			component.set("v.data", component.get("v.data"));
		}
		else helper.sortData(component, component.find("filterBy").get("v.value"));
	},
	handleClear : function(component, event, helper){
		component.find('filterBy').set("v.value", "default");
		component.get("v.data").bidOptions = component.get("v.bids");
		component.set("v.data", component.get("v.data"));
	},
	handleCompare : function(component, event, helper){
		var bidsSelected = [];
		var optionsCompared = 0;
		component.get("v.data").bidOptions.forEach(function(bid){
			if(bid.isCompared){bidsSelected.push(bid);optionsCompared++;}
		});
		if(optionsCompared > 0 && optionsCompared < 4){
			component.set("v.itinerary", component.get("v.data").itinerary);
			component.set("v.bidsSelected", bidsSelected);
			component.set("v.content", "compare");
		}
		else{
			var toastEvent = $A.get("e.force:showToast");
			toastEvent.setParams({
				"title": "Message",
				"message": optionsCompared == 0 ? " Please you must select at least one option." : optionsCompared > 3 ? " You can compare up to 3 options." : ""
			}).fire();
		}
	},
	handleContent : function(component, event, helper){
		component.set("v.itinerary", component.get("v.data").itinerary);
		component.set("v.bidIndex", $(event.currentTarget).data('index'));
		component.set("v.content", $(event.currentTarget).data('content'));
	}
})
```
### VoyajerOptionsFreightHelper

```
({
	getData : function(component, method){
		var action = component.get("c." + method);
		if(method == "searchBidOptions") action.setParams({itineraryId: component.get("v.itinerarySelected")});
		action.setCallback(this, function(response){
			var state = response.getState();
			if(state === "SUCCESS"){
				var result = JSON.parse(response.getReturnValue());
				if(method == "searchBidOptions"){
					component.set("v.data", result);
					component.set("v.bids", result.bidOptions);
				}
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
		$A.util.removeClass(component.find("loading"), "slds-hide");
		$A.enqueueAction(action);
	},
	sortData : function(component, filterBy){
		var bidsMap = component.get("v.data").bidOptions.map(function(bid, i){
		  return {index : i, value : bid};
		})
		bidsMap.sort(function(element1, element2){
			if(filterBy == "RRRecomendation"){
                if(!$A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)){
					if(!$A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)) return element1.value.record.Options__c - element2.value.record.Options__c;
					else if($A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)) return 1;
					else if(!$A.util.isEmpty(element1.value.record.Options__c) && $A.util.isEmpty(element2.value.record.Options__c)) return -1;
					return 0;
				}
				else if($A.util.isEmpty(element1.value.record.Options__c) && !$A.util.isEmpty(element2.value.record.Options__c)) return 1;
				else if(!$A.util.isEmpty(element1.value.record.Options__c) && $A.util.isEmpty(element2.value.record.Options__c)) return -1;
			}
			else if(filterBy == "lowToHigh"){
				if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)){
					if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return element1.value.record.Rate_Commission__r.records[0].Total_Price__c - element2.value.record.Rate_Commission__r.records[0].Total_Price__c;
					else if($A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return 1;
					else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && $A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return -1;
					return 0;
				}
				else if($A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)) return 1;
				else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && $A.util.isEmpty(element2.value.record.Rate_Commission__r)) return -1;
			}
			else if(filterBy == "highToLow"){
				if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)){
					if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return element2.value.record.Rate_Commission__r.records[0].Total_Price__c - element1.value.record.Rate_Commission__r.records[0].Total_Price__c;
					else if($A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return 1;
					else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r.records[0].Total_Price__c) && $A.util.isEmpty(element2.value.record.Rate_Commission__r.records[0].Total_Price__c)) return -1;
					return 0;
				}
				else if($A.util.isEmpty(element1.value.record.Rate_Commission__r) && !$A.util.isEmpty(element2.value.record.Rate_Commission__r)) return 1;
				else if(!$A.util.isEmpty(element1.value.record.Rate_Commission__r) && $A.util.isEmpty(element2.value.record.Rate_Commission__r)) return -1;
			}
			return 0;
		});
		var bidsSorted = bidsMap.map(function(element, j){
			return component.get("v.data").bidOptions[element.index];
		});	
		component.get("v.data").bidOptions = bidsSorted;
		component.set("v.data", component.get("v.data"));
	},
})
```

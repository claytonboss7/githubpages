---
layout: default
title: VoyajerVendorGroundBid
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerVendorGroundBid
## Fields
### VoyajerVendorGroundBidController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        component.set('v.today', today);
        component.set("v.bidData",{});
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorGroundBid");
        callToParent.fire();
	},
    //Changes as per 176506748
    checkLength : function(component, event, helper) {
        component.set('v.lengthDiv', '');
        var notesTxtBoxVal = component.find("notesTxtBox").get("v.value");
        component.set('v.lengthDiv', notesTxtBoxVal.length  + ' of 255');
    },
    
    loadBidData : function(component, event, helper) {
        var bidData = component.get("v.bidData");
        console.log(bidData);
        if(bidData.info != undefined) {
            component.set("v.info",bidData.info);
            component.set("v.revenue",bidData.revenue);
            component.set("v.trips",bidData.trips);
            component.set("v.vehicles",bidData.vehicles);
            component.set("v.fees",bidData.fees);
            component.set("v.reviewName",bidData.reviewName);
            component.set("v.reviewTitle",bidData.reviewTitle);
            component.set("v.reviewEmail",bidData.reviewEmail);
            component.set("v.reviewPhone",bidData.reviewPhone);
        }
    },
    
    handleBack : function(component, event, helper) {
        component.set("v.mainContent","vendorActions");
    },
    
    handleUnableToBid : function(component, event, helper) {
        component.set("v.menuSelected","noBid");
    },
    
    onOptionsYesNoChange : function(component, event, helper) {
        //var newValue = event.getParam("value");
        var index = event.getSource().get("v.label");
        var vehicles = component.get("v.vehicles");
		// fix by Clay - 24 Dec, 2020
		//vehicles[index].available = vehicles[index].available == "Yes"? "No" : "Yes";
    	var value = event.getParam("value");
        if(value == "No") {
        	vehicles[index].available = "No";
        } else if(value == "Yes") {
            vehicles[index].available = "Yes";
        } else {
            if(value && value.length > 1) {
                vehicles[index].available = vehicles[index].available == "Yes" ? "No" : "Yes";
                component.set("v.yesNoValue", vehicles[index].available);
            } else {
                vehicles[index].available = undefined;
            }
        }
        
        //console.log("newValue: "+vehicles[index].available);
        component.set("v.vehicles",vehicles);
    },
    
    onOptionsIncludedExcludedChange : function(component, event, helper) {
        var index = event.getSource().get("v.label");
        var fees = component.get("v.fees");
        
        // fix by Clay - 24 Dec, 2020
        // fees[index].Included_Excluded__c = fees[index].Included_Excluded__c == "Included"? "Excluded" : "Included";
        var value = event.getParam("value");
        if(value == "Excluded") {
        	fees[index].Included_Excluded__c = "Excluded";
        } else if(value == "Included") {
            fees[index].Included_Excluded__c = "Included";
        } else {
            if(value && value.length > 1) {
                fees[index].Included_Excluded__c = undefined;
                fees[index].value = "";
            } else {
                fees[index].Included_Excluded__c = undefined;
            }
        }
        component.set("v.fees",fees);
    },
    
    onCheckboxChange : function(component, event, helper) {
        console.log("onCheckboxChange");
        var basicCommission = event.getSource().get("v.checked");
        var revenue = component.get("v.revenue");
        if(basicCommission) {
            var base = revenue.Base_Cost__c;
            if(typeof(base) === "string") { if(!!base) base = parseFloat(base); else 0; }
            var gratuity = revenue.Gratuity__c;
            if(typeof(gratuity) === "string") { if(!!gratuity) gratuity = parseFloat(gratuity); else 0; }
            var commission = base * 0.1;
            var total = base + commission + gratuity;
            revenue.Base_Cost__c = base.toFixed(2);
            revenue.Gratuity__c = gratuity.toFixed(2);
            revenue.Commission__c = commission.toFixed(2);
            revenue.Total_Price__c = total.toFixed(2);
            component.set("v.revenue",revenue);
        }
        component.set("v.basicCommission",basicCommission);
    },
    
    onCommissionChange : function(component, event, helper) {
        if(component.get("v.basicCommission")) component.set("v.basicCommission",false);
    },
    
    updateTotal : function(component, event, helper) {
        console.log("updateTotal");
        function isEmpty(obj) {
            for(var key in obj) if(obj.hasOwnProperty(key)) return false;
            return true;
        }
        var revenue = component.get("v.revenue");
        if(!isEmpty(revenue)) {
            var base = revenue.Base_Cost__c;
            if(typeof(base) === "string") { if(!!base) base = parseFloat(base); else 0; }
            var gratuity = revenue.Gratuity__c;
            if(typeof(gratuity) === "string") { if(!!gratuity) gratuity = parseFloat(gratuity); else 0; }
            var commission = revenue.Commission__c;
            if(typeof(commission) === "string") { if(!!commission) commission = parseFloat(commission); else 0; }
            var total = base + commission + gratuity;
            revenue.Total_Price__c = total.toFixed(2);
            component.set("v.revenue",revenue);
        }
    },

    handlePlaceBid : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        
        if(allValid) {
            var vehicles = component.get("v.vehicles");
            vehicles.forEach(item => { if(item.available == "No" && item.bidMake == "Other") item.bidMake = item.bidOtherMake; });
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","placeGroundBid");
            callToParent.setParam("data",{
                info: JSON.parse(JSON.stringify(component.get("v.info"))),
                revenue: JSON.parse(JSON.stringify(component.get("v.revenue"))),
                vehicles: JSON.parse(JSON.stringify(component.get("v.vehicles"))),
                fees: JSON.parse(JSON.stringify(component.get("v.fees"))),
                journal: {
                    name: component.get("v.reviewName"),
                    title: component.get("v.reviewTitle"),
                    email: component.get("v.reviewEmail"),
                    phone: component.get("v.reviewPhone")
                }
            });
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({ type: "error", title: "", message: "Please update the invalid form entries and try again." });
            toastEvent.fire();
        }
    },
    
    handleEditBid : function(component, event, helper) {
        component.set("v.menuSelected","edit");
    },
    
    sendNoBid : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var noBidReason = component.get("v.noBidReason");
            if(noBidReason == "Other") noBidReason = component.get("v.noBidNotes");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","unableToBid");
            callToParent.setParam("data",{
                bidId: component.get("v.info").bidId,
                notes: noBidReason,
                journal: {
                    name: component.get("v.noBidFirstName")+" "+component.get("v.noBidLastName"),
                    title: component.get("v.noBidTitle"),
                    email: component.get("v.noBidEmail")
                }
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerVendorGroundBid

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorGroundBid

```
.THIS {
}

.THIS .sideBarProfile .slds-nav-vertical__action {
    cursor: default;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    align-items: center;
    display: flex;
    flex: 1;
    padding: 0.5em 1em;
}

.THIS .lodgingRateField {
    display: flex;
    margin-bottom: 0;
    padding: 0;
}

.THIS .lodgingRateField .condition {
    border-color: rgb(194, 57, 52);
    box-shadow: rgb(194, 57, 52) 0 0 0 1px inset;
    background-clip: padding-box;
    border-right: 0;
}

.THIS .lodgingRateField .slds-form-element__label {
    align-items: center;
    background-color: #f7f9fe;
    border: 1px solid #dbdbdb;
    border-top-left-radius: .5em;
    border-bottom-left-radius: .5em;
    display: flex;
    flex: 1;
    font-size: inherit;
    font-weight: 400;
    margin-bottom: 0;
    min-width: 4em;
    padding: 0;
    padding-left: 1em;
}

.THIS .lodgingRateField .slds-form-element__control {
    margin-left: -0.2em;
    padding: 0;
}

.THIS .formFieldCheckbox {
    align-items: flex-end;
    display: flex;
    max-height: 4rem;
}

.THIS .noErrorMessage .slds-form-element__help {
    display: none;
}

.THIS .checkboxField {
    padding-left: 0.75em;
}

.THIS .checkboxList .slds-form-element__label {
    font-size: 1rem;
    padding-left: 0.25em;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux {
    background-color: black;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux:after {
    border-bottom: 2px solid white;
    border-left: 2px solid white;
}

.THIS .checkboxRequired .slds-required {
    display: none;
}

.THIS .checkboxAgreement .slds-checkbox__label {
    display: flex;
}

.THIS .checkboxAgreement .slds-checkbox_faux {
    height: 1.25em;
    width: 2.75em;
    margin-top: 0.5em;
}

.THIS .checkboxCommission .slds-form-element__help {
    margin-top: -0.25rem;
}

.THIS .formFieldValue {
    margin-top: -0.25em;
}

.THIS .horizontalCheckboxGroup .slds-form-element__control {
    display: flex;
}

.THIS .amenitiesList .slds-form-element__control {
    display: flex;
    flex-flow: column wrap;
    overflow: auto;
    align-content: flex-start;
    max-height: 10em;
}

.THIS .amenitiesList .slds-form-element__control .slds-checkbox {
    min-width: 33%;
}

.THIS .productionCoordinatorInfo {
    padding: 10px 20px;
    background-color: #fff;
}
```
### VoyajerVendorGroundBid

```
<aura:component >
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="yesNoValue" default=""/>
	<aura:attribute type="String" name="yesNoOldValue" default=""/>
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="menuSelected" default="edit" />
    <aura:attribute type="String" name="productionOfficePreference" default="" />
    <aura:attribute type="String" name="productionAssocUserName" />
    <aura:attribute type="String" name="productionAssocUserPhone" />
    <aura:attribute type="String" name="productionAssocUserEmail" />
    <aura:attribute type="String" name="productionAssocRole" />
    <aura:attribute type="String" name="noBidReason" default="No Availability" />
    <aura:attribute type="String" name="noBidNotes" default="" />
    <aura:attribute type="String" name="noBidFirstName" default="" />
    <aura:attribute type="String" name="noBidLastName" default="" />
    <aura:attribute type="String" name="noBidTitle" default="" />
    <aura:attribute type="String" name="noBidEmail" default="" />
    <!-- Changes as per 176506748 -->
    <aura:attribute type="String" name="lengthDiv" default="0 of 255" />
    <aura:attribute type="String" name="agreementText" default="Company agrees to negotaite with Road Rebel ONLY moving forward and not offer lower rates directly. If either is breached, you
                                                                agree to pay Road Rebel commission on any trip booked with your company. This also serves as the commission agreement in 
                                                                the event we go to contract. By selecting Submit, you are signing this agreement electronically.*" />
    <aura:attribute type="String" name="iata" default="IATA #05-56078-5" />
    <aura:attribute type="String" name="iataRRE" default="IATA #96-06295-6" />
    <aura:attribute type="String" name="reviewName" default="" />
    <aura:attribute type="String" name="reviewTitle" default="" />
    <aura:attribute type="String" name="reviewEmail" default="" />
    <aura:attribute type="String" name="reviewPhone" default="" />
    <aura:attribute type="String" name="reviewDate" default="" />
    <aura:attribute type="Object" name="bidData" />
    <aura:attribute type="Object" name="info" />
    <aura:attribute type="Object" name="revenue" />
    <aura:attribute type="Date" name="today" />
    <aura:attribute type="Boolean" name="basicCommission" default="false" />
    <aura:attribute type="List" name="trips" />
    <aura:attribute type="List" name="vehicles" />
    <aura:attribute type="List" name="optionsYesNo" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'No', 'value': 'No'}]" />
    
    <aura:attribute type="List" name="lodgings" />
    <aura:attribute type="List" name="fees" />
    <aura:attribute type="List" name="noBidReasons" default="[{'label': 'No Availability', 'value': 'No Availability'},{'label': 'Other', 'value': 'Other'}]" />
    <aura:attribute type="List" name="optionsIncludedExcluded" default="[{'label': 'Included in rate', 'value': 'Included'},{'label': 'Not included in rate', 'value': 'Excluded'}]" />
    <aura:attribute type="List" name="optionsIncludedExcludedDetails" default="[{'label': 'Agree', 'value': 'Included'},{'label': 'Disagree', 'value': 'Excluded'}]" />
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bidData}" action="{!c.loadBidData}" />
    <aura:handler action="{!c.handleCommunicationEvent}" event="c:VoyajerCallToChild" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="mainMenu">
            <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page" style="margin-top: 1em;">
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='edit'? ' slds-is-active' : '')}">
                    <div class="slds-nav-vertical__action"><span>Ground Travel Bid</span></div>
                </div>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='noBid'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>No Bid</span></div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='review'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='review'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>Review &amp; Submit</span></div>
                    </div>
                </aura:if>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <aura:if isTrue="{!v.menuSelected=='edit'}">
                            <h1 style="display: flex; align-items: flex-end;">Ground Travel Bid</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='noBid'}">
                            <h1 style="display: flex; align-items: flex-end;">Sorry to hear you won't be bidding</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='review'}">
                            <h1 style="display: flex; align-items: flex-end;">Please review and sign your bid below</h1>
                        </aura:if>
                        <div>
                            <div class="slds-text-align_right slds-m-bottom_x-small">
                                <lightning:button label="Back to Actions" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
                            </div>
                            <div class="productionCoordinatorInfo" style="color: #fff;background-color: #0065ff;font-weight: 700;">
                                <i class="fas fa-comments" style="margin-right: 0.5em;"></i>Need assistance?
                            </div>
                            <div class="productionCoordinatorInfo" style="font-weight: 700;">
                                <div>{!v.productionAssocUserName}</div>
                                <div>{!v.productionAssocRole}</div>
                                <div><i class="fas fa-phone-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserPhone}</div>
                                <div><i class="far fa-envelope" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserEmail}</div>
                            </div>
                        </div>
                    </div>
                </div>
                <aura:if isTrue="{!v.menuSelected=='edit'}">
                    <div class="pageContentForm">
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Production</sub></label>
                                <h3>{!v.productionName}</h3>
                            </div>
                            <div class="formField" style="text-align: end;">
                                <span><b>{!v.info.bidName}</b></span>
                            </div>
                        </div>
                        <div class="formColumnThreeChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Company</sub></label>
                                <p style="margin-top: -0.5em;">
                                    <b>{!v.info.vendorName}</b>
                                    <br/><lightning:formattedRichText value="{!v.info.vendorAddress}"/>
                                </p>
                            </div>
                            <div class="formField">
                                <label><sub class="subLabel">Description</sub></label>
                                <p style="margin-top: -0.5em;">{!v.info.travelDescription}</p>
                            </div>
                            <div class="formField">
                                <label><sub class="subLabel">Group</sub></label>
                                <p style="margin-top: -0.5em;">{!v.info.travelGroup}</p>
                            </div>
                        </div>
                        <aura:iteration items="{!v.trips}" var="trip" indexVar="tripIndex">

                            <div class="recordTable tableList">
                                <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb; padding: 0.5em 1em; background-color: #d4ecf4;">
                                    <h3>Trip {!tripIndex+1}</h3>
                                </div>
                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField" style="margin-bottom: 0; padding: 0;">
                                            <p><b>Trip Type:</b>{!' '+trip.type}</p>
                                        </div>
                                        <div class="formField" style="margin-bottom: 0; padding: 0;">
                                            <p><b>Description:</b>{!' '+trip.description}</p>
                                        </div>
                                    </div>
                                </div>

                                
                                <div class="tableHeader" style="background-color: #e6f8ff;">
                                    <div style="flex: 1; white-space: normal; text-align: center;">Vehicle</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">Start Date</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">Spot Time</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">End Date</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">Dep Time</div>
                                    <div style="flex: 1; white-space: normal; text-align: left;">P/U Details</div>
                                    <div style="flex: 1; white-space: normal; text-align: left;">D/O Details</div>

                                </div>
                                <aura:iteration items="{!trip.travels}" var="travel">
                                    <div class="tableRow">
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.vehicle}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.dateStart}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.timeStart}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.dateEnd}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.timeEnd}</div>
                                        <div style="flex: 1; white-space: normal; text-align: left;">{!travel.details}</div>
                                        <div style="flex: 1; white-space: normal; text-align: left;">{!travel.detailsDropOff}</div>

                                    </div>
                                </aura:iteration>
                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                    <div class="formField" style="margin-bottom: 0; white-space: pre-wrap;">
                                        <p><b>Trip Notes:</b>{!' '+trip.additionalNotes}</p>                                       
                                    </div>
                                </div>
                            </div>
                        </aura:iteration>
                        <br/>
                        <aura:iteration items="{!v.vehicles}" var="vehicle" indexVar="vehicleIndex">
                            <div class="formField">
                                <label style="color: black;"><b>Vehicle: {!vehicle.reference}</b></label>
                                <p style="margin-top: -0.5em; font-size: 0.8rem;"><b>The following vehicle has been request</b></p>
                            </div>
                            <div class="recordTable tableList">
                                <div class="tableHeader">
                                    <div style="flex: none; width: 10em;">Vehicle</div>
                                    <div style="flex: none; width: 8em;">Capacity</div>
                                    <div style="white-space: normal; text-align: left;">Make / Model</div>
                                    <div style="flex: none; width: 6em;">Year</div>
                                    <div style="flex: 2;">Amenities</div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: none; width: 10em;">{!vehicle.type}</div>
                                    <div style="flex: none; width: 8em;">{!vehicle.capacity}</div>
                                    <div style="white-space: normal; text-align: left;">{!vehicle.make+' / '+vehicle.model}</div>
                                    <div style="flex: none; width: 6em;">{!vehicle.year}</div>
                                    <div style="flex: 2; white-space: normal; text-align: left;">{!vehicle.amenities}</div>
                                </div>
                            </div>
                            <div class="formField">
                                <label>Requested vehicle available?</label>
                                <lightning:checkboxGroup aura:id="recordField"
                                                         label="{!vehicleIndex}"
                                                         options="{!v.optionsYesNo}"
                                                         value="{!v.yesNoValue}"
                                                         variant="label-hidden"
                                                         onchange="{!c.onOptionsYesNoChange}"
                                                         required="true"
                                                         class="horizontalCheckboxGroup" /> 
                            </div>
                            <aura:if isTrue="{!vehicle.available=='No'}">
                                <lightning:recordEditForm aura:id="profileForm"
                                                          objectApiName="Ground__c"
                                                          recordTypeId="{!vehicle.recordTypeId}"
                                                          density="comfy">
                                    <lightning:messages />
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Vehicle_Type__c">Vehicle Type<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="Vehicle_Type__c" value="{!vehicle.bidType}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <label for="Capacity__c">Capacity<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!vehicle.bidCapacity}" variant="label-hidden" required="true" />
                                        </div>
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Make__c">Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                <lightning:inputField aura:id="recordField" fieldName="Make__c" value="{!vehicle.bidMake}" variant="label-hidden" required="true" />
                                            </div>
                                            <div class="formField">
                                                <aura:if isTrue="{!vehicle.bidMake=='Other'}">
                                                    <label for="Other_make__c">Other Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!vehicle.bidOtherMake}" variant="label-hidden" required="true" />
                                                    <aura:set attribute="else">
                                                        <div class="formColumnBlank"></div>
                                                    </aura:set>
                                                </aura:if>
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Model__c">Model</label>
                                                <lightning:inputField aura:id="recordField" fieldName="Model__c" value="{!vehicle.bidModel}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Year__c">Year</label>
                                                <lightning:input aura:id="recordField" type="text" value="{!vehicle.bidYear}" variant="label-hidden" />
                                            </div>
                                        </div>
                                    </div>
                                    <div class="formField">
                                        <label for="bidAmenities">Available Amenities</label>
                                        <!-- // fix by Clay - 24 Dec, 2020 
                                        <lightning:checkboxGroup label="" options="{!vehicle.amenitiesList}" value="{!vehicle.bidAmenities}" variant="label-hidden" class="amenitiesList"/>-->
                                        <lightning:checkboxGroup label="" aura:id="recordField1" options="{!vehicle.amenitiesList}" value="{!vehicle.bidAmenities}" variant="label-hidden" class="amenitiesList" required="true"/>
                                    </div>
                                    <div class="formField">
                                        <label for="name">Other Amenities</label>
                                        <lightning:input aura:id="recordField" name="Other_Amenities__c" value="{!vehicle.bidOtherAmenities}" label="" variant="label-hidden" />
                                    </div>
                                </lightning:recordEditForm>
                            </aura:if>
                            <br/>
                        </aura:iteration>
                        <div style="padding: 0.5em;"><b>Rate Details - <i>Rate Details are for the entire trip</i></b></div>
                        <lightning:recordEditForm aura:id="revenueForm"
                                                  objectApiName="Revenue__c"
                                                  recordTypeId="{!v.revenue.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="CurrencyIsoCode">Currency</label>
                                    <lightning:inputField aura:id="recordField" fieldName="CurrencyIsoCode" value="{!v.revenue.CurrencyIsoCode}" variant="label-hidden" required="true" />
                                </div>
                                <div class="formColumnBlank"></div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Base_Cost__c">Base Cost</label>
                                    <lightning:input aura:id="recordField" type="number" formatter="decimal" name="Base_Cost__c" value="{!v.revenue.Base_Cost__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" required="true" oncommit="{!c.updateTotal}" />
                                </div>
                                <div class="formField">
                                    <label for="Total_Price__c">Total Price</label>
                                    <lightning:input type="number" formatter="decimal" name="Total_Price__c" value="{!v.revenue.Total_Price__c}" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" disabled="true" class="lodgingRateField noErrorMessage" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Gratuity__c">Gratuity</label>
                                    <lightning:input aura:id="recordField" type="number" formatter="decimal" name="Total_Price__c" value="{!v.revenue.Gratuity__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" required="true" oncommit="{!c.updateTotal}" />
                                </div>
                                <div class="formColumnBlank"></div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Rate__c">Road Rebel Commission</label>
                                    <lightning:input aura:id="recordField" type="number" formatter="decimal" name="lodgingCurrencyISOCode" value="{!v.revenue.Commission__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" required="true" onchange="{!c.onCommissionChange}" oncommit="{!c.updateTotal}" />
                                </div>
                                <div class="formFieldCheckbox">
                                    <lightning:input aura:id="recordField" type="checkbox" name="rrCommission" label="10% basic commission" checked="{!v.basicCommission}" class="checkboxField checkboxList" onchange="{!c.onCheckboxChange}" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <aura:if isTrue="{!v.productionOfficePreference=='RRE'}">
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="VAT_Rate__c">VAT Rate %</label>
                                        <lightning:input aura:id="recordField" type="number" formatter="percent-fixed" name="VAT_Rate__c" value="{!v.revenue.VAT_Rate__c}" step="0.01" label="" min="0" variant="label-hidden" />
                                    </div>
                                    <div class="formFieldCheckbox">
                                        <lightning:input type="checkbox" checked="{!v.revenue.VAT_Included_in_Total__c}" label="Included in rate" name="VAT_Included_in_Total__c" class="checkboxField formCheckbox" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </aura:if>
                            <br/>
                        </lightning:recordEditForm>
                        <aura:if isTrue="{!not(empty(v.fees))}">
                            <br/>
                            <div style="padding: 0.5em;"><b>Additional Fees &amp; Details:</b></div>
                            <aura:iteration items="{!v.fees}" var="fee" indexVar="feeIndex">
                                <aura:if isTrue="{!not(fee.IsFromVendor__c)}">
                                    <div class="formField">
                                        <label>{!fee.Concessions_Requested__c}</label>
                                        <!--// fix by Clay - 24 Dec, 2020
                                        <lightning:checkboxGroup aura:id="recordField"
                                                                 label="{!feeIndex}"
                                                                 options="{!v.optionsIncludedExcluded}"
                                                                 value="{}"	
                                                                 variant="label-hidden"
                                                                 onchange="{!c.onOptionsIncludedExcludedChange}" /> -->
                                        <!--// fix by Clay - 25 Dec, 2020
                                        <lightning:checkboxGroup aura:id="recordField"
                                                                 label="{!feeIndex}"
                                                                 options="{!v.optionsIncludedExcluded}"
                                                                 value="{}"
                                                                 name="Checkbox Group"
                                                                 required="true"	
                                                                 variant="label-hidden"
                                                                 onchange="{!c.onOptionsIncludedExcludedChange}" />-->
                                        <lightning:checkboxGroup aura:id="recordField"
                                                                 label="{!feeIndex}"
                                                                 options="{!if(fee.IsDetailNotFees__c==true,v.optionsIncludedExcludedDetails,v.optionsIncludedExcluded)}"
                                                                 value=""
                                                                 name="Checkbox Group"
                                                                 required="true"	
                                                                 variant="label-hidden"
                                                                 onchange="{!c.onOptionsIncludedExcludedChange}" />
                                    </div>
                                    <aura:if isTrue="{!fee.Included_Excluded__c=='Excluded'}">
                                        <div class="formField">
                                            <label>Fee Details</label>
                                            <lightning:input aura:id="recordField" value="{!fee.Notes__c}" label="" variant="label-hidden" />
                                        </div>
                                    </aura:if>
                                    <br/>
                                </aura:if>
                            </aura:iteration>
                        </aura:if>
                        <div class="formField">
                            <!-- Changes as per 176506748 -->
                            <label for="notes">Anything else we should know?</label>
                            <lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" value="{!v.info.notes}" aura:id="notesTxtBox" class="formTextarea" variant="label-hidden" />
                        	<div style="float:right;">{!v.lengthDiv}</div>
                        </div>
                        <br/>
                        <div class="formFieldRadio">
                            <lightning:input aura:id="recordField" type="checkbox" label="{!v.agreementText}" required="true" class="checkboxField checkboxList checkboxAgreement checkboxRequired" />
                        </div>
                        <br/>
                        <p style="padding-left: 2.75em; font-weight: 600;">{!if(v.productionOfficePreference=='RRE',v.iataRRE,v.iata)}</p>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="name">Full Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewName" value="{!v.reviewName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewTitle" value="{!v.reviewTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewEmail" value="{!v.reviewEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewPhone" value="{!v.reviewPhone}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Unable to bid" class="formButtonPadding" onclick="{!c.handleUnableToBid}" />
                            <!--<lightning:button type="button" label="Place bid" variant="brand" class="formButtonBrand formButtonPadding" />-->
                            <lightning:button type="button" label="Submit bid" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.handlePlaceBid}" />
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="pageContentForm">
                        <p>We understand if you are unable to bid at this time. Tell us why.</p>
                        <div class="formField">
                            <lightning:radioGroup name="radioGroupRequired" label="" variant="label-hidden"
                                                  options="{!v.noBidReasons}" value="{!v.noBidReason}"
                                                  type="radio" />
                        </div>
                        <aura:if isTrue="{!v.noBidReason=='Other'}">
                            <div class="formField">
                                <label for="noBidNotes">Describe in more detail reason for No Bid</label>
                                <lightning:textarea aura:id="recordField" value="{!v.noBidNotes}" class="formTextarea" variant="label-hidden" required="true" />
                            </div>
                        </aura:if>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="firstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="firstName" value="{!v.noBidFirstName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="lastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="lastName" value="{!v.noBidLastName}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="title" value="{!v.noBidTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="email" value="{!v.noBidEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Submit" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.sendNoBid}" />
                        </div>
                    </div>
                </aura:if>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerVendorGroundBidHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerVendorGroundBidController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        component.set('v.today', today);
        component.set("v.bidData",{});
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorGroundBid");
        callToParent.fire();
	},
    //Changes as per 176506748
    checkLength : function(component, event, helper) {
        component.set('v.lengthDiv', '');
        var notesTxtBoxVal = component.find("notesTxtBox").get("v.value");
        component.set('v.lengthDiv', notesTxtBoxVal.length  + ' of 255');
    },
    
    loadBidData : function(component, event, helper) {
        var bidData = component.get("v.bidData");
        console.log(bidData);
        if(bidData.info != undefined) {
            component.set("v.info",bidData.info);
            component.set("v.revenue",bidData.revenue);
            component.set("v.trips",bidData.trips);
            component.set("v.vehicles",bidData.vehicles);
            component.set("v.fees",bidData.fees);
            component.set("v.reviewName",bidData.reviewName);
            component.set("v.reviewTitle",bidData.reviewTitle);
            component.set("v.reviewEmail",bidData.reviewEmail);
            component.set("v.reviewPhone",bidData.reviewPhone);
        }
    },
    
    handleBack : function(component, event, helper) {
        component.set("v.mainContent","vendorActions");
    },
    
    handleUnableToBid : function(component, event, helper) {
        component.set("v.menuSelected","noBid");
    },
    
    onOptionsYesNoChange : function(component, event, helper) {
        //var newValue = event.getParam("value");
        var index = event.getSource().get("v.label");
        var vehicles = component.get("v.vehicles");
		// fix by Clay - 24 Dec, 2020
		//vehicles[index].available = vehicles[index].available == "Yes"? "No" : "Yes";
    	var value = event.getParam("value");
        if(value == "No") {
        	vehicles[index].available = "No";
        } else if(value == "Yes") {
            vehicles[index].available = "Yes";
        } else {
            if(value && value.length > 1) {
                vehicles[index].available = vehicles[index].available == "Yes" ? "No" : "Yes";
                component.set("v.yesNoValue", vehicles[index].available);
            } else {
                vehicles[index].available = undefined;
            }
        }
        
        //console.log("newValue: "+vehicles[index].available);
        component.set("v.vehicles",vehicles);
    },
    
    onOptionsIncludedExcludedChange : function(component, event, helper) {
        var index = event.getSource().get("v.label");
        var fees = component.get("v.fees");
        
        // fix by Clay - 24 Dec, 2020
        // fees[index].Included_Excluded__c = fees[index].Included_Excluded__c == "Included"? "Excluded" : "Included";
        var value = event.getParam("value");
        if(value == "Excluded") {
        	fees[index].Included_Excluded__c = "Excluded";
        } else if(value == "Included") {
            fees[index].Included_Excluded__c = "Included";
        } else {
            if(value && value.length > 1) {
                fees[index].Included_Excluded__c = undefined;
                fees[index].value = "";
            } else {
                fees[index].Included_Excluded__c = undefined;
            }
        }
        component.set("v.fees",fees);
    },
    
    onCheckboxChange : function(component, event, helper) {
        console.log("onCheckboxChange");
        var basicCommission = event.getSource().get("v.checked");
        var revenue = component.get("v.revenue");
        if(basicCommission) {
            var base = revenue.Base_Cost__c;
            if(typeof(base) === "string") { if(!!base) base = parseFloat(base); else 0; }
            var gratuity = revenue.Gratuity__c;
            if(typeof(gratuity) === "string") { if(!!gratuity) gratuity = parseFloat(gratuity); else 0; }
            var commission = base * 0.1;
            var total = base + commission + gratuity;
            revenue.Base_Cost__c = base.toFixed(2);
            revenue.Gratuity__c = gratuity.toFixed(2);
            revenue.Commission__c = commission.toFixed(2);
            revenue.Total_Price__c = total.toFixed(2);
            component.set("v.revenue",revenue);
        }
        component.set("v.basicCommission",basicCommission);
    },
    
    onCommissionChange : function(component, event, helper) {
        if(component.get("v.basicCommission")) component.set("v.basicCommission",false);
    },
    
    updateTotal : function(component, event, helper) {
        console.log("updateTotal");
        function isEmpty(obj) {
            for(var key in obj) if(obj.hasOwnProperty(key)) return false;
            return true;
        }
        var revenue = component.get("v.revenue");
        if(!isEmpty(revenue)) {
            var base = revenue.Base_Cost__c;
            if(typeof(base) === "string") { if(!!base) base = parseFloat(base); else 0; }
            var gratuity = revenue.Gratuity__c;
            if(typeof(gratuity) === "string") { if(!!gratuity) gratuity = parseFloat(gratuity); else 0; }
            var commission = revenue.Commission__c;
            if(typeof(commission) === "string") { if(!!commission) commission = parseFloat(commission); else 0; }
            var total = base + commission + gratuity;
            revenue.Total_Price__c = total.toFixed(2);
            component.set("v.revenue",revenue);
        }
    },

    handlePlaceBid : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        
        if(allValid) {
            var vehicles = component.get("v.vehicles");
            vehicles.forEach(item => { if(item.available == "No" && item.bidMake == "Other") item.bidMake = item.bidOtherMake; });
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","placeGroundBid");
            callToParent.setParam("data",{
                info: JSON.parse(JSON.stringify(component.get("v.info"))),
                revenue: JSON.parse(JSON.stringify(component.get("v.revenue"))),
                vehicles: JSON.parse(JSON.stringify(component.get("v.vehicles"))),
                fees: JSON.parse(JSON.stringify(component.get("v.fees"))),
                journal: {
                    name: component.get("v.reviewName"),
                    title: component.get("v.reviewTitle"),
                    email: component.get("v.reviewEmail"),
                    phone: component.get("v.reviewPhone")
                }
            });
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({ type: "error", title: "", message: "Please update the invalid form entries and try again." });
            toastEvent.fire();
        }
    },
    
    handleEditBid : function(component, event, helper) {
        component.set("v.menuSelected","edit");
    },
    
    sendNoBid : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var noBidReason = component.get("v.noBidReason");
            if(noBidReason == "Other") noBidReason = component.get("v.noBidNotes");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","unableToBid");
            callToParent.setParam("data",{
                bidId: component.get("v.info").bidId,
                notes: noBidReason,
                journal: {
                    name: component.get("v.noBidFirstName")+" "+component.get("v.noBidLastName"),
                    title: component.get("v.noBidTitle"),
                    email: component.get("v.noBidEmail")
                }
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerVendorGroundBid

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorGroundBid

```
.THIS {
}

.THIS .sideBarProfile .slds-nav-vertical__action {
    cursor: default;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    align-items: center;
    display: flex;
    flex: 1;
    padding: 0.5em 1em;
}

.THIS .lodgingRateField {
    display: flex;
    margin-bottom: 0;
    padding: 0;
}

.THIS .lodgingRateField .condition {
    border-color: rgb(194, 57, 52);
    box-shadow: rgb(194, 57, 52) 0 0 0 1px inset;
    background-clip: padding-box;
    border-right: 0;
}

.THIS .lodgingRateField .slds-form-element__label {
    align-items: center;
    background-color: #f7f9fe;
    border: 1px solid #dbdbdb;
    border-top-left-radius: .5em;
    border-bottom-left-radius: .5em;
    display: flex;
    flex: 1;
    font-size: inherit;
    font-weight: 400;
    margin-bottom: 0;
    min-width: 4em;
    padding: 0;
    padding-left: 1em;
}

.THIS .lodgingRateField .slds-form-element__control {
    margin-left: -0.2em;
    padding: 0;
}

.THIS .formFieldCheckbox {
    align-items: flex-end;
    display: flex;
    max-height: 4rem;
}

.THIS .noErrorMessage .slds-form-element__help {
    display: none;
}

.THIS .checkboxField {
    padding-left: 0.75em;
}

.THIS .checkboxList .slds-form-element__label {
    font-size: 1rem;
    padding-left: 0.25em;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux {
    background-color: black;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux:after {
    border-bottom: 2px solid white;
    border-left: 2px solid white;
}

.THIS .checkboxRequired .slds-required {
    display: none;
}

.THIS .checkboxAgreement .slds-checkbox__label {
    display: flex;
}

.THIS .checkboxAgreement .slds-checkbox_faux {
    height: 1.25em;
    width: 2.75em;
    margin-top: 0.5em;
}

.THIS .checkboxCommission .slds-form-element__help {
    margin-top: -0.25rem;
}

.THIS .formFieldValue {
    margin-top: -0.25em;
}

.THIS .horizontalCheckboxGroup .slds-form-element__control {
    display: flex;
}

.THIS .amenitiesList .slds-form-element__control {
    display: flex;
    flex-flow: column wrap;
    overflow: auto;
    align-content: flex-start;
    max-height: 10em;
}

.THIS .amenitiesList .slds-form-element__control .slds-checkbox {
    min-width: 33%;
}

.THIS .productionCoordinatorInfo {
    padding: 10px 20px;
    background-color: #fff;
}
```
### VoyajerVendorGroundBid

```
<aura:component >
	<aura:attribute type="String" name="mainContent" />
	<aura:attribute type="String" name="yesNoValue" default=""/>
	<aura:attribute type="String" name="yesNoOldValue" default=""/>
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="menuSelected" default="edit" />
    <aura:attribute type="String" name="productionOfficePreference" default="" />
    <aura:attribute type="String" name="productionAssocUserName" />
    <aura:attribute type="String" name="productionAssocUserPhone" />
    <aura:attribute type="String" name="productionAssocUserEmail" />
    <aura:attribute type="String" name="productionAssocRole" />
    <aura:attribute type="String" name="noBidReason" default="No Availability" />
    <aura:attribute type="String" name="noBidNotes" default="" />
    <aura:attribute type="String" name="noBidFirstName" default="" />
    <aura:attribute type="String" name="noBidLastName" default="" />
    <aura:attribute type="String" name="noBidTitle" default="" />
    <aura:attribute type="String" name="noBidEmail" default="" />
    <!-- Changes as per 176506748 -->
    <aura:attribute type="String" name="lengthDiv" default="0 of 255" />
    <aura:attribute type="String" name="agreementText" default="Company agrees to negotaite with Road Rebel ONLY moving forward and not offer lower rates directly. If either is breached, you
                                                                agree to pay Road Rebel commission on any trip booked with your company. This also serves as the commission agreement in 
                                                                the event we go to contract. By selecting Submit, you are signing this agreement electronically.*" />
    <aura:attribute type="String" name="iata" default="IATA #05-56078-5" />
    <aura:attribute type="String" name="iataRRE" default="IATA #96-06295-6" />
    <aura:attribute type="String" name="reviewName" default="" />
    <aura:attribute type="String" name="reviewTitle" default="" />
    <aura:attribute type="String" name="reviewEmail" default="" />
    <aura:attribute type="String" name="reviewPhone" default="" />
    <aura:attribute type="String" name="reviewDate" default="" />
    <aura:attribute type="Object" name="bidData" />
    <aura:attribute type="Object" name="info" />
    <aura:attribute type="Object" name="revenue" />
    <aura:attribute type="Date" name="today" />
    <aura:attribute type="Boolean" name="basicCommission" default="false" />
    <aura:attribute type="List" name="trips" />
    <aura:attribute type="List" name="vehicles" />
    <aura:attribute type="List" name="optionsYesNo" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'No', 'value': 'No'}]" />
    
    <aura:attribute type="List" name="lodgings" />
    <aura:attribute type="List" name="fees" />
    <aura:attribute type="List" name="noBidReasons" default="[{'label': 'No Availability', 'value': 'No Availability'},{'label': 'Other', 'value': 'Other'}]" />
    <aura:attribute type="List" name="optionsIncludedExcluded" default="[{'label': 'Included in rate', 'value': 'Included'},{'label': 'Not included in rate', 'value': 'Excluded'}]" />
    <aura:attribute type="List" name="optionsIncludedExcludedDetails" default="[{'label': 'Agree', 'value': 'Included'},{'label': 'Disagree', 'value': 'Excluded'}]" />
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bidData}" action="{!c.loadBidData}" />
    <aura:handler action="{!c.handleCommunicationEvent}" event="c:VoyajerCallToChild" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="mainMenu">
            <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page" style="margin-top: 1em;">
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='edit'? ' slds-is-active' : '')}">
                    <div class="slds-nav-vertical__action"><span>Ground Travel Bid</span></div>
                </div>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='noBid'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>No Bid</span></div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='review'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='review'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>Review &amp; Submit</span></div>
                    </div>
                </aura:if>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <aura:if isTrue="{!v.menuSelected=='edit'}">
                            <h1 style="display: flex; align-items: flex-end;">Ground Travel Bid</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='noBid'}">
                            <h1 style="display: flex; align-items: flex-end;">Sorry to hear you won't be bidding</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='review'}">
                            <h1 style="display: flex; align-items: flex-end;">Please review and sign your bid below</h1>
                        </aura:if>
                        <div>
                            <div class="slds-text-align_right slds-m-bottom_x-small">
                                <lightning:button label="Back to Actions" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
                            </div>
                            <div class="productionCoordinatorInfo" style="color: #fff;background-color: #0065ff;font-weight: 700;">
                                <i class="fas fa-comments" style="margin-right: 0.5em;"></i>Need assistance?
                            </div>
                            <div class="productionCoordinatorInfo" style="font-weight: 700;">
                                <div>{!v.productionAssocUserName}</div>
                                <div>{!v.productionAssocRole}</div>
                                <div><i class="fas fa-phone-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserPhone}</div>
                                <div><i class="far fa-envelope" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserEmail}</div>
                            </div>
                        </div>
                    </div>
                </div>
                <aura:if isTrue="{!v.menuSelected=='edit'}">
                    <div class="pageContentForm">
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Production</sub></label>
                                <h3>{!v.productionName}</h3>
                            </div>
                            <div class="formField" style="text-align: end;">
                                <span><b>{!v.info.bidName}</b></span>
                            </div>
                        </div>
                        <div class="formColumnThreeChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Company</sub></label>
                                <p style="margin-top: -0.5em;">
                                    <b>{!v.info.vendorName}</b>
                                    <br/><lightning:formattedRichText value="{!v.info.vendorAddress}"/>
                                </p>
                            </div>
                            <div class="formField">
                                <label><sub class="subLabel">Description</sub></label>
                                <p style="margin-top: -0.5em;">{!v.info.travelDescription}</p>
                            </div>
                            <div class="formField">
                                <label><sub class="subLabel">Group</sub></label>
                                <p style="margin-top: -0.5em;">{!v.info.travelGroup}</p>
                            </div>
                        </div>
                        <aura:iteration items="{!v.trips}" var="trip" indexVar="tripIndex">

                            <div class="recordTable tableList">
                                <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb; padding: 0.5em 1em; background-color: #d4ecf4;">
                                    <h3>Trip {!tripIndex+1}</h3>
                                </div>
                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField" style="margin-bottom: 0; padding: 0;">
                                            <p><b>Trip Type:</b>{!' '+trip.type}</p>
                                        </div>
                                        <div class="formField" style="margin-bottom: 0; padding: 0;">
                                            <p><b>Description:</b>{!' '+trip.description}</p>
                                        </div>
                                    </div>
                                </div>

                                
                                <div class="tableHeader" style="background-color: #e6f8ff;">
                                    <div style="flex: 1; white-space: normal; text-align: center;">Vehicle</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">Start Date</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">Spot Time</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">End Date</div>
                                    <div style="flex: 1; white-space: normal; text-align: center;">Dep Time</div>
                                    <div style="flex: 1; white-space: normal; text-align: left;">P/U Details</div>
                                    <div style="flex: 1; white-space: normal; text-align: left;">D/O Details</div>

                                </div>
                                <aura:iteration items="{!trip.travels}" var="travel">
                                    <div class="tableRow">
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.vehicle}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.dateStart}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.timeStart}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.dateEnd}</div>
                                        <div style="flex: 1; white-space: normal; text-align: center;">{!travel.timeEnd}</div>
                                        <div style="flex: 1; white-space: normal; text-align: left;">{!travel.details}</div>
                                        <div style="flex: 1; white-space: normal; text-align: left;">{!travel.detailsDropOff}</div>

                                    </div>
                                </aura:iteration>
                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                    <div class="formField" style="margin-bottom: 0; white-space: pre-wrap;">
                                        <p><b>Trip Notes:</b>{!' '+trip.additionalNotes}</p>                                       
                                    </div>
                                </div>
                            </div>
                        </aura:iteration>
                        <br/>
                        <aura:iteration items="{!v.vehicles}" var="vehicle" indexVar="vehicleIndex">
                            <div class="formField">
                                <label style="color: black;"><b>Vehicle: {!vehicle.reference}</b></label>
                                <p style="margin-top: -0.5em; font-size: 0.8rem;"><b>The following vehicle has been request</b></p>
                            </div>
                            <div class="recordTable tableList">
                                <div class="tableHeader">
                                    <div style="flex: none; width: 10em;">Vehicle</div>
                                    <div style="flex: none; width: 8em;">Capacity</div>
                                    <div style="white-space: normal; text-align: left;">Make / Model</div>
                                    <div style="flex: none; width: 6em;">Year</div>
                                    <div style="flex: 2;">Amenities</div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: none; width: 10em;">{!vehicle.type}</div>
                                    <div style="flex: none; width: 8em;">{!vehicle.capacity}</div>
                                    <div style="white-space: normal; text-align: left;">{!vehicle.make+' / '+vehicle.model}</div>
                                    <div style="flex: none; width: 6em;">{!vehicle.year}</div>
                                    <div style="flex: 2; white-space: normal; text-align: left;">{!vehicle.amenities}</div>
                                </div>
                            </div>
                            <div class="formField">
                                <label>Requested vehicle available?</label>
                                <lightning:checkboxGroup aura:id="recordField"
                                                         label="{!vehicleIndex}"
                                                         options="{!v.optionsYesNo}"
                                                         value="{!v.yesNoValue}"
                                                         variant="label-hidden"
                                                         onchange="{!c.onOptionsYesNoChange}"
                                                         required="true"
                                                         class="horizontalCheckboxGroup" /> 
                            </div>
                            <aura:if isTrue="{!vehicle.available=='No'}">
                                <lightning:recordEditForm aura:id="profileForm"
                                                          objectApiName="Ground__c"
                                                          recordTypeId="{!vehicle.recordTypeId}"
                                                          density="comfy">
                                    <lightning:messages />
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Vehicle_Type__c">Vehicle Type<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="Vehicle_Type__c" value="{!vehicle.bidType}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <label for="Capacity__c">Capacity<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!vehicle.bidCapacity}" variant="label-hidden" required="true" />
                                        </div>
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Make__c">Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                <lightning:inputField aura:id="recordField" fieldName="Make__c" value="{!vehicle.bidMake}" variant="label-hidden" required="true" />
                                            </div>
                                            <div class="formField">
                                                <aura:if isTrue="{!vehicle.bidMake=='Other'}">
                                                    <label for="Other_make__c">Other Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!vehicle.bidOtherMake}" variant="label-hidden" required="true" />
                                                    <aura:set attribute="else">
                                                        <div class="formColumnBlank"></div>
                                                    </aura:set>
                                                </aura:if>
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Model__c">Model</label>
                                                <lightning:inputField aura:id="recordField" fieldName="Model__c" value="{!vehicle.bidModel}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Year__c">Year</label>
                                                <lightning:input aura:id="recordField" type="text" value="{!vehicle.bidYear}" variant="label-hidden" />
                                            </div>
                                        </div>
                                    </div>
                                    <div class="formField">
                                        <label for="bidAmenities">Available Amenities</label>
                                        <!-- // fix by Clay - 24 Dec, 2020 
                                        <lightning:checkboxGroup label="" options="{!vehicle.amenitiesList}" value="{!vehicle.bidAmenities}" variant="label-hidden" class="amenitiesList"/>-->
                                        <lightning:checkboxGroup label="" aura:id="recordField1" options="{!vehicle.amenitiesList}" value="{!vehicle.bidAmenities}" variant="label-hidden" class="amenitiesList" required="true"/>
                                    </div>
                                    <div class="formField">
                                        <label for="name">Other Amenities</label>
                                        <lightning:input aura:id="recordField" name="Other_Amenities__c" value="{!vehicle.bidOtherAmenities}" label="" variant="label-hidden" />
                                    </div>
                                </lightning:recordEditForm>
                            </aura:if>
                            <br/>
                        </aura:iteration>
                        <div style="padding: 0.5em;"><b>Rate Details - <i>Rate Details are for the entire trip</i></b></div>
                        <lightning:recordEditForm aura:id="revenueForm"
                                                  objectApiName="Revenue__c"
                                                  recordTypeId="{!v.revenue.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="CurrencyIsoCode">Currency</label>
                                    <lightning:inputField aura:id="recordField" fieldName="CurrencyIsoCode" value="{!v.revenue.CurrencyIsoCode}" variant="label-hidden" required="true" />
                                </div>
                                <div class="formColumnBlank"></div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Base_Cost__c">Base Cost</label>
                                    <lightning:input aura:id="recordField" type="number" formatter="decimal" name="Base_Cost__c" value="{!v.revenue.Base_Cost__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" required="true" oncommit="{!c.updateTotal}" />
                                </div>
                                <div class="formField">
                                    <label for="Total_Price__c">Total Price</label>
                                    <lightning:input type="number" formatter="decimal" name="Total_Price__c" value="{!v.revenue.Total_Price__c}" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" disabled="true" class="lodgingRateField noErrorMessage" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Gratuity__c">Gratuity</label>
                                    <lightning:input aura:id="recordField" type="number" formatter="decimal" name="Total_Price__c" value="{!v.revenue.Gratuity__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" required="true" oncommit="{!c.updateTotal}" />
                                </div>
                                <div class="formColumnBlank"></div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Rate__c">Road Rebel Commission</label>
                                    <lightning:input aura:id="recordField" type="number" formatter="decimal" name="lodgingCurrencyISOCode" value="{!v.revenue.Commission__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" required="true" onchange="{!c.onCommissionChange}" oncommit="{!c.updateTotal}" />
                                </div>
                                <div class="formFieldCheckbox">
                                    <lightning:input aura:id="recordField" type="checkbox" name="rrCommission" label="10% basic commission" checked="{!v.basicCommission}" class="checkboxField checkboxList" onchange="{!c.onCheckboxChange}" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <aura:if isTrue="{!v.productionOfficePreference=='RRE'}">
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="VAT_Rate__c">VAT Rate %</label>
                                        <lightning:input aura:id="recordField" type="number" formatter="percent-fixed" name="VAT_Rate__c" value="{!v.revenue.VAT_Rate__c}" step="0.01" label="" min="0" variant="label-hidden" />
                                    </div>
                                    <div class="formFieldCheckbox">
                                        <lightning:input type="checkbox" checked="{!v.revenue.VAT_Included_in_Total__c}" label="Included in rate" name="VAT_Included_in_Total__c" class="checkboxField formCheckbox" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </aura:if>
                            <br/>
                        </lightning:recordEditForm>
                        <aura:if isTrue="{!not(empty(v.fees))}">
                            <br/>
                            <div style="padding: 0.5em;"><b>Additional Fees &amp; Details:</b></div>
                            <aura:iteration items="{!v.fees}" var="fee" indexVar="feeIndex">
                                <aura:if isTrue="{!not(fee.IsFromVendor__c)}">
                                    <div class="formField">
                                        <label>{!fee.Concessions_Requested__c}</label>
                                        <!--// fix by Clay - 24 Dec, 2020
                                        <lightning:checkboxGroup aura:id="recordField"
                                                                 label="{!feeIndex}"
                                                                 options="{!v.optionsIncludedExcluded}"
                                                                 value="{}"	
                                                                 variant="label-hidden"
                                                                 onchange="{!c.onOptionsIncludedExcludedChange}" /> -->
                                        <!--// fix by Clay - 25 Dec, 2020
                                        <lightning:checkboxGroup aura:id="recordField"
                                                                 label="{!feeIndex}"
                                                                 options="{!v.optionsIncludedExcluded}"
                                                                 value="{}"
                                                                 name="Checkbox Group"
                                                                 required="true"	
                                                                 variant="label-hidden"
                                                                 onchange="{!c.onOptionsIncludedExcludedChange}" />-->
                                        <lightning:checkboxGroup aura:id="recordField"
                                                                 label="{!feeIndex}"
                                                                 options="{!if(fee.IsDetailNotFees__c==true,v.optionsIncludedExcludedDetails,v.optionsIncludedExcluded)}"
                                                                 value=""
                                                                 name="Checkbox Group"
                                                                 required="true"	
                                                                 variant="label-hidden"
                                                                 onchange="{!c.onOptionsIncludedExcludedChange}" />
                                    </div>
                                    <aura:if isTrue="{!fee.Included_Excluded__c=='Excluded'}">
                                        <div class="formField">
                                            <label>Fee Details</label>
                                            <lightning:input aura:id="recordField" value="{!fee.Notes__c}" label="" variant="label-hidden" />
                                        </div>
                                    </aura:if>
                                    <br/>
                                </aura:if>
                            </aura:iteration>
                        </aura:if>
                        <div class="formField">
                            <!-- Changes as per 176506748 -->
                            <label for="notes">Anything else we should know?</label>
                            <lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" value="{!v.info.notes}" aura:id="notesTxtBox" class="formTextarea" variant="label-hidden" />
                        	<div style="float:right;">{!v.lengthDiv}</div>
                        </div>
                        <br/>
                        <div class="formFieldRadio">
                            <lightning:input aura:id="recordField" type="checkbox" label="{!v.agreementText}" required="true" class="checkboxField checkboxList checkboxAgreement checkboxRequired" />
                        </div>
                        <br/>
                        <p style="padding-left: 2.75em; font-weight: 600;">{!if(v.productionOfficePreference=='RRE',v.iataRRE,v.iata)}</p>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="name">Full Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewName" value="{!v.reviewName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewTitle" value="{!v.reviewTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewEmail" value="{!v.reviewEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewPhone" value="{!v.reviewPhone}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Unable to bid" class="formButtonPadding" onclick="{!c.handleUnableToBid}" />
                            <!--<lightning:button type="button" label="Place bid" variant="brand" class="formButtonBrand formButtonPadding" />-->
                            <lightning:button type="button" label="Submit bid" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.handlePlaceBid}" />
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="pageContentForm">
                        <p>We understand if you are unable to bid at this time. Tell us why.</p>
                        <div class="formField">
                            <lightning:radioGroup name="radioGroupRequired" label="" variant="label-hidden"
                                                  options="{!v.noBidReasons}" value="{!v.noBidReason}"
                                                  type="radio" />
                        </div>
                        <aura:if isTrue="{!v.noBidReason=='Other'}">
                            <div class="formField">
                                <label for="noBidNotes">Describe in more detail reason for No Bid</label>
                                <lightning:textarea aura:id="recordField" value="{!v.noBidNotes}" class="formTextarea" variant="label-hidden" required="true" />
                            </div>
                        </aura:if>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="firstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="firstName" value="{!v.noBidFirstName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="lastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="lastName" value="{!v.noBidLastName}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="title" value="{!v.noBidTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="email" value="{!v.noBidEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Submit" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.sendNoBid}" />
                        </div>
                    </div>
                </aura:if>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerVendorGroundBidHelper

```
({
	helperMethod : function() {
		
	}
})
```

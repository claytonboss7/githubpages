---
layout: default
title: VoyajerCustomLookup
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerCustomLookup
## Fields
### VoyajerCustomLookup

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCustomLookupController

```
({
    doInit : function(component, event, helper) {
        var getRecordId = component.get("v.lookupId");
        var objectAPIName = component.get("v.objectAPIName");
        if(!!getRecordId && !!objectAPIName) helper.loadSavedRecord(component,event,getRecordId,objectAPIName);
    },
    
    onLoadLookup : function(component, event, helper) {
        if(component.get("v.loadVenueCityLookup") || component.get("v.loadVenueLookup") || component.get("v.loadCityLookup")) {
            component.set("v.loadVenueCityLookup",false);
            component.set("v.loadVenueLookup",false);
            component.set("v.loadCityLookup",false);
            
            var pillTarget = component.find("lookup-pill");
            var lookUpTarget = component.find("lookupField"); 
            
            $A.util.addClass(pillTarget, 'slds-hide');
            $A.util.removeClass(pillTarget, 'slds-show');
            
            $A.util.addClass(lookUpTarget, 'slds-show');
            $A.util.removeClass(lookUpTarget, 'slds-hide');
            
            component.set("v.searchKeyWord","");
            component.set("v.listOfSearchRecords", null);
            
            var getRecordId = component.get("v.lookupId");
            var objectAPIName = component.get("v.objectAPIName");
            if(!!getRecordId && !!objectAPIName) helper.loadSavedRecord(component,event,getRecordId,objectAPIName);
        }
    },
    
    showError : function(component, event, helper) {
        var getRecordId = component.get("v.lookupId");
        var objectAPIName = component.get("v.objectAPIName");
        if(component.get("v.isDisabled")) {
            if(!!getRecordId && !!objectAPIName) helper.loadSavedRecord(component,event,getRecordId,objectAPIName);
            else {
                var pillTarget = component.find("lookup-pill");
                var lookUpTarget = component.find("lookupField"); 
                
                $A.util.addClass(pillTarget, 'slds-hide');
                $A.util.removeClass(pillTarget, 'slds-show');
                
                $A.util.addClass(lookUpTarget, 'slds-show');
                $A.util.removeClass(lookUpTarget, 'slds-hide');
            }
        }
        component.set("v.checkLookupValidation",true);
    },
    
    onLookupIdEmpty : function(component, event, helper) {
        if(component.get("v.checkLookupValidation")) {
            component.set("v.checkLookupValidation",false);
            var forOpen = component.find("searchRes");
            var message = component.find("requiredMessage");
            if(!component.get("v.lookupId") && !component.get("v.isDisabled")) {
                $A.util.addClass(forOpen, 'slds-has-error');
                $A.util.addClass(message, 'slds-show');
                $A.util.removeClass(message, 'slds-hide');
            }
            else {
                $A.util.removeClass(forOpen, 'slds-has-error');
                $A.util.addClass(message, 'slds-hide');
                $A.util.removeClass(message, 'slds-show');
            }
        }
    },
    
    onfocus : function(component, event, helper) {
        $A.util.addClass(component.find("mySpinner"), "slds-show");
        var forOpen = component.find("searchRes");
        $A.util.addClass(forOpen, 'slds-is-open');
        $A.util.removeClass(forOpen, 'slds-is-close');
        $A.util.removeClass(forOpen, 'slds-has-error');
        
        var message = component.find("requiredMessage");
        $A.util.addClass(message, 'slds-hide');
        $A.util.removeClass(message, 'slds-show');
        // Get Default 5 Records order by createdDate DESC  
        var getInputkeyWord = component.get("v.searchKeyWord");
        helper.searchHelper(component,event,getInputkeyWord);
    },
    
    onBlurInput : function(component, event, helper) {
        var getRecordId = component.get("v.lookupId");
        if(component.get("v.isRequired") && !component.get("v.getRecordId")) component.set("v.checkLookupValidation",true);
    },
    
    onblur : function(component,event,helper) {
        component.set("v.listOfSearchRecords",null);
        var forclose = component.find("searchRes");
        $A.util.addClass(forclose, 'slds-is-close');
        $A.util.removeClass(forclose, 'slds-is-open');
    },
    
    keyPressController : function(component, event, helper) {
        // get the search Input keyword   
        var getInputkeyWord = component.get("v.searchKeyWord");
        // check if getInputKeyWord size id more then 0 then open the lookup result List and 
        // call the helper 
        // else close the lookup result List part.   
        if(getInputkeyWord.length > 0){
            var forOpen = component.find("searchRes");
            $A.util.addClass(forOpen, 'slds-is-open');
            $A.util.removeClass(forOpen, 'slds-is-close');
            helper.searchHelper(component,event,getInputkeyWord);
        } else {
            component.set("v.listOfSearchRecords", null ); 
            var forclose = component.find("searchRes");
            $A.util.addClass(forclose, 'slds-is-close');
            $A.util.removeClass(forclose, 'slds-is-open');
        }
    },
    
    // function for clear the Record Selaction 
    clear :function(component,event,heplper){
        var pillTarget = component.find("lookup-pill");
        var lookUpTarget = component.find("lookupField"); 
        
        $A.util.addClass(pillTarget, 'slds-hide');
        $A.util.removeClass(pillTarget, 'slds-show');
        
        $A.util.addClass(lookUpTarget, 'slds-show');
        $A.util.removeClass(lookUpTarget, 'slds-hide');
        
        component.set("v.searchKeyWord","");
        component.set("v.listOfSearchRecords", null);
        component.set("v.selectedRecord",{});
        if(!!component.get("v.lookupId")) component.set("v.isEdited",true);
        component.set("v.lookupId","");
        if(component.get("v.isRequired")) component.set("v.checkLookupValidation",true);
        if(component.get("v.objectAPIName") == "Airport__c" && !component.get("v.isDisabled")) {
            $A.enqueueAction(component.get("v.airportRoundAux"));
        }
    },
    
    // This function call when the end User Select any record from the result list.   
    handleSelectItemEvent : function(component, event, helper) {
        var selectedRecord = event.getParam("recordByEvent");
        component.set("v.selectedRecord" , selectedRecord); 
        var objectAPIName = component.get("v.objectAPIName");
        var fieldName = component.get("v.fieldName");
        var pillText = "";
        component.set("v.lookupId",selectedRecord.Id);
        if(objectAPIName == "Account" && fieldName == "Venue_City__c") component.set("v.lookupId",selectedRecord.City__c);
        pillText = selectedRecord.Name;
        switch(objectAPIName) {
            case "Account":
                switch(fieldName) {
                    case "Venue_City__c":
                        pillText = selectedRecord.City__r.Name;
                        break;
                    case "Venue__c":
                        break;
                }
                break;
            case "City__c":
                /*
                var city = oRecord.City__c;
                var state = oRecord.hasOwnProperty("State__c")? oRecord.State__c : "";
                var country = oRecord.hasOwnProperty("Country__c")? oRecord.Country__c : "";
                pillText = city + ", " + (!!state? state + ", " + country : country);
                */
                break;
            case "Airport__c":
                break;
            default:
                break;
        }
        component.set("v.pillText",pillText);
        component.set("v.isEdited",true);
        
        var forclose = component.find("lookup-pill");
        $A.util.addClass(forclose, 'slds-show');
        $A.util.removeClass(forclose, 'slds-hide');
        
        var forclose = component.find("searchRes");
        $A.util.addClass(forclose, 'slds-is-close');
        $A.util.removeClass(forclose, 'slds-is-open');
        $A.util.removeClass(forclose, 'slds-has-error');
        
        var message = component.find("requiredMessage");
        $A.util.addClass(message, 'slds-hide');
        $A.util.removeClass(message, 'slds-show');
        
        var lookUpTarget = component.find("lookupField");
        $A.util.addClass(lookUpTarget, 'slds-hide');
        $A.util.removeClass(lookUpTarget, 'slds-show');  
        if(!component.get("v.isDisabled")) {
            switch(objectAPIName) {
                case "Account":
                    switch(fieldName) {
                        case "Venue_City__c":
                            component.set("v.venueId",selectedRecord.Id);
                            component.set("v.cityId",selectedRecord.City__c);
                            $A.enqueueAction(component.get("v.lodgingVenueAux"));
                            $A.enqueueAction(component.get("v.lodgingCityAux"));
                            break;
                        case "Venue__c":
                            if(selectedRecord.hasOwnProperty("City__c")) {
                                component.set("v.venueCityId",selectedRecord.City__c);
                                component.set("v.cityId",selectedRecord.City__c);
                                $A.enqueueAction(component.get("v.lodgingVenueCityAux"));
                                $A.enqueueAction(component.get("v.lodgingCityAux"));
                            }
                            break;
                    }
                    break;
                case "City__c":
                    break;
                case "Airport__c":
                    $A.enqueueAction(component.get("v.airportRoundAux"));
                    break;
                default:
                    break;
            }
        }
    },
})
```
### VoyajerCustomLookup

```
<aura:component controller="VoyajerCustomLookup" implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction" access="global">
	<aura:attribute type="List" name="listOfSearchRecords" description="Use,for store the list of search records which returns from apex class" />
    <aura:attribute type="sObject" name="selectedRecord" default="{}" description="Use,for store SELECTED sObject Record" />
    <aura:attribute type="String" name="lookupId" description="Use for store the recordId used in the form" />
    <aura:attribute type="String" name="venueCityId" description="" />
    <aura:attribute type="String" name="venueId" description="" />
    <aura:attribute type="String" name="cityId" description="" />
    <aura:attribute type="String" name="fieldName" default="" />
    <aura:attribute type="String" name="searchKeyWord" default="" />
    <aura:attribute type="String" name="objectAPIName" default="" />
    <aura:attribute type="String" name="pillText" default="Pill text" />
    <aura:attribute type="String" name="iconName" default="" />
    <aura:attribute type="String" name="label" default="" />
    <aura:attribute type="String" name="inputPlaceholder" default="Search..." />
    <aura:attribute type="String" name="message" default="" />
    <aura:attribute type="Boolean" name="isRequired" default="false" />
    <aura:attribute type="Boolean" name="isEdited" default="false" />
    <aura:attribute type="Boolean" name="isDisabled" default="false" />
    <aura:attribute type="Boolean" name="triggerLookupValidation" default="false" />
    <aura:attribute type="Boolean" name="checkLookupValidation" default="false" />
    <aura:attribute type="Boolean" name="loadVenueCityLookup" default="false" />
    <aura:attribute type="Boolean" name="loadVenueLookup" default="false" />
    <aura:attribute type="Boolean" name="loadCityLookup" default="false" />
    
    <aura:attribute type="Aura.action" name="lodgingVenueCityAux" />
    <aura:attribute type="Aura.action" name="lodgingVenueAux" />
    <aura:attribute type="Aura.action" name="lodgingCityAux" />
    <aura:attribute type="Aura.action" name="airportRoundAux" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:handler name="change" value="{!v.triggerLookupValidation}" action="{!c.showError}" />
    <aura:handler name="change" value="{!v.checkLookupValidation}" action="{!c.onLookupIdEmpty}" />
    <aura:handler name="change" value="{!v.loadVenueCityLookup}" action="{!c.onLoadLookup}" />
    <aura:handler name="change" value="{!v.loadVenueLookup}" action="{!c.onLoadLookup}" />
    <aura:handler name="change" value="{!v.loadCityLookup}" action="{!c.onLoadLookup}" />
    <aura:handler name="callToLookup" action="{!c.handleSelectItemEvent}" event="c:VoyajerCallToLookup" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

    <div aura:id="searchRes" class="slds-form-element slds-lookup slds-is-close" data-select="single" onmouseleave="{!c.onblur}">
        <label class="lookupFieldLabel slds-form-element__label" for="lookup-348">
            {!v.label}
            <aura:if isTrue="{!v.fieldName=='City__c'}"><span> City, State, Country</span></aura:if>
        </label>
        <!--This part is for display search bar for lookup-->  
        <div class="slds-form-element__control">
            <div class="slds-input-has-icon slds-input-has-icon--right">
                <!-- This markup is for when an record is selected -->
                <div aura:id="lookup-pill" class="slds-pill-container slds-hide">
                    <lightning:pill class="{!if(v.isDisabled,'pillSize lookupPill','pillSize')}" label="{!v.pillText}" name="{!v.pillText}" onremove="{!c.clear}">
                        <aura:set attribute="media">
                            <lightning:icon iconName="{!v.iconName}" size="x-small" alternativeText="{!v.iconName}"/>
                        </aura:set>
                    </lightning:pill>
                </div>
                <div aura:id="lookupField" class="slds-show">
                    <aura:if isTrue="{!!v.isDisabled}">
                        <lightning:icon class="slds-input__icon slds-show" iconName="utility:search" size="x-small" alternativeText="search"/>
                    </aura:if>
                    <span class="slds-icon_container  slds-combobox__input-entity-icon" title="record">
                        <lightning:icon class="slds-icon slds-icon slds-icon_small slds-icon-text-default" iconName="{!v.iconName}" size="x-small" alternativeText="icon"/>
                        <span class="slds-assistive-text"></span>
                    </span>
                    <ui:inputText aura:id="lookupInput"
                                  class="slds-lookup__search-input slds-input leftPaddingClass lookupFieldInput" 
                                  click="{!c.onfocus}" 
                                  updateOn="keyup" 
                                  keyup="{!c.keyPressController}" 
                                  blur="{!c.onBlurInput}" 
                                  value="{!v.searchKeyWord}" 
                                  placeholder="{!v.inputPlaceholder}" 
                                  required="{!v.isRequired}" 
                                  requiredIndicatorClass="slds-has-error" 
                                  disabled="{!v.isDisabled}" />
                </div>
            </div>
        </div>
        <!--This part is for Display typehead lookup result List-->  
        <ul style="min-height:40px;margin-top:0px !important" class="slds-listbox slds-listbox_vertical slds-dropdown slds-dropdown_fluid slds-lookup__menu slds" role="listbox">
            <lightning:spinner aura:id="mySpinner" class="slds-hide" variant="brand" size="small" />
            <center> {!v.message}</center>
            <aura:iteration items="{!v.listOfSearchRecords}" var="oRecord">
                <c:VoyajerCustomLookupItem oRecord="{!oRecord}" iconName="{!v.iconName}" objectAPIName="{!v.objectAPIName}" fieldName="{!v.fieldName}" searchKeyWord="{!v.searchKeyWord}" />
            </aura:iteration>
        </ul>
        <div aura:id="requiredMessage" class="slds-form-element__help slds-hide" id="error-message-unique-id">This field is required</div>
    </div>
</aura:component>
```
### VoyajerCustomLookupHelper

```
({
    searchHelper : function(component, event, getInputkeyWord) {
        // call the apex class method 
        var action = component.get("c.fetchLookupValues");
        // set param to method  
        action.setParams({
            'searchKeyWord': getInputkeyWord,
            'sObjectName' : component.get("v.objectAPIName"),
            'fieldName' : component.get("v.fieldName")
        });
        // set a callBack    
        action.setCallback(this, function(response) {
            $A.util.removeClass(component.find("mySpinner"), "slds-show");
            var state = response.getState();
            if (state === "SUCCESS") {
                var storeResponse = response.getReturnValue();
                // if storeResponse size is equal 0 ,display No Result Found... message on screen.                }
                if (storeResponse.length == 0) {
                    var fieldName = component.get("v.fieldName");
                    component.set("v.message", 'No Result Found...');
                    if(fieldName == "Venue_City__c" || fieldName == "Venue__c") component.set("v.message", 'No results were found, please use Other Venue field.');
                } else {
                    component.set("v.message", '');
                }
                // set searchResult list with return value from server.
                component.set("v.listOfSearchRecords", storeResponse);
                //console.log(storeResponse);
            }
        });
        // enqueue the Action  
        $A.enqueueAction(action);
    },
    
    loadSavedRecord : function(component, event, getRecordId, objectAPIName) {
        component.set("v.checkLookupValidation",false);
        var forOpen = component.find("searchRes");
        var message = component.find("requiredMessage");
        $A.util.removeClass(forOpen, 'slds-has-error');
        $A.util.addClass(message, 'slds-hide');
        $A.util.removeClass(message, 'slds-show');
        
        component.set("v.selectedRecord",{});
        var action = component.get("c.loadLookupValues");
        action.setParams({
            'recordId': getRecordId,
            'sObjectName' : component.get("v.objectAPIName"),
            'fieldName' : component.get("v.fieldName")
        });
        action.setCallback(this, function(response) {
            $A.util.removeClass(component.find("mySpinner"), "slds-show");
            var state = response.getState();
            if (state === "SUCCESS") {
                var record = response.getReturnValue();
                component.set("v.selectedRecord" ,record); 
                var objectAPIName = component.get("v.objectAPIName");
                var fieldName = component.get("v.fieldName");
                var pillText = record.Name;
                switch(objectAPIName) {
                    case "Account":
                        switch(fieldName) {
                            case "Venue_City__c":
                                //pillText = recordS.City__r.Name;
                                break;
                            case "Venue__c":
                                break;
                        }
                        break;
                    case 'City__c':
                        break;
                    default:
                        break;
                }
                component.set("v.pillText",pillText);
                var forclose = component.find("lookup-pill");
                $A.util.addClass(forclose, 'slds-show');
                $A.util.removeClass(forclose, 'slds-hide');
                
                var forclose = component.find("searchRes");
                $A.util.addClass(forclose, 'slds-is-close');
                $A.util.removeClass(forclose, 'slds-is-open');
                
                var lookUpTarget = component.find("lookupField");
                $A.util.addClass(lookUpTarget, 'slds-hide');
                $A.util.removeClass(lookUpTarget, 'slds-show'); 
            }
        });
        // enqueue the Action  
        $A.enqueueAction(action);
    }
})
```
### VoyajerCustomLookup

```
.THIS .leftPaddingClass {
    padding-left: 2rem;
}

.THIS .pillSize{
    width:100%;
}

.THIS .lookupFieldInput {
    min-height: calc(1.875rem + 2px);
}

.THIS .lookupFieldLabel > span {
    font-size: 0.8em;
    font-weight: 400;
    padding-left: 0.75em;
}

.THIS .lookupPill .slds-pill__remove {
    display: none !important;
}
```
### VoyajerCustomLookup

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCustomLookupController

```
({
    doInit : function(component, event, helper) {
        var getRecordId = component.get("v.lookupId");
        var objectAPIName = component.get("v.objectAPIName");
        if(!!getRecordId && !!objectAPIName) helper.loadSavedRecord(component,event,getRecordId,objectAPIName);
    },
    
    onLoadLookup : function(component, event, helper) {
        if(component.get("v.loadVenueCityLookup") || component.get("v.loadVenueLookup") || component.get("v.loadCityLookup")) {
            component.set("v.loadVenueCityLookup",false);
            component.set("v.loadVenueLookup",false);
            component.set("v.loadCityLookup",false);
            
            var pillTarget = component.find("lookup-pill");
            var lookUpTarget = component.find("lookupField"); 
            
            $A.util.addClass(pillTarget, 'slds-hide');
            $A.util.removeClass(pillTarget, 'slds-show');
            
            $A.util.addClass(lookUpTarget, 'slds-show');
            $A.util.removeClass(lookUpTarget, 'slds-hide');
            
            component.set("v.searchKeyWord","");
            component.set("v.listOfSearchRecords", null);
            
            var getRecordId = component.get("v.lookupId");
            var objectAPIName = component.get("v.objectAPIName");
            if(!!getRecordId && !!objectAPIName) helper.loadSavedRecord(component,event,getRecordId,objectAPIName);
        }
    },
    
    showError : function(component, event, helper) {
        var getRecordId = component.get("v.lookupId");
        var objectAPIName = component.get("v.objectAPIName");
        if(component.get("v.isDisabled")) {
            if(!!getRecordId && !!objectAPIName) helper.loadSavedRecord(component,event,getRecordId,objectAPIName);
            else {
                var pillTarget = component.find("lookup-pill");
                var lookUpTarget = component.find("lookupField"); 
                
                $A.util.addClass(pillTarget, 'slds-hide');
                $A.util.removeClass(pillTarget, 'slds-show');
                
                $A.util.addClass(lookUpTarget, 'slds-show');
                $A.util.removeClass(lookUpTarget, 'slds-hide');
            }
        }
        component.set("v.checkLookupValidation",true);
    },
    
    onLookupIdEmpty : function(component, event, helper) {
        if(component.get("v.checkLookupValidation")) {
            component.set("v.checkLookupValidation",false);
            var forOpen = component.find("searchRes");
            var message = component.find("requiredMessage");
            if(!component.get("v.lookupId") && !component.get("v.isDisabled")) {
                $A.util.addClass(forOpen, 'slds-has-error');
                $A.util.addClass(message, 'slds-show');
                $A.util.removeClass(message, 'slds-hide');
            }
            else {
                $A.util.removeClass(forOpen, 'slds-has-error');
                $A.util.addClass(message, 'slds-hide');
                $A.util.removeClass(message, 'slds-show');
            }
        }
    },
    
    onfocus : function(component, event, helper) {
        $A.util.addClass(component.find("mySpinner"), "slds-show");
        var forOpen = component.find("searchRes");
        $A.util.addClass(forOpen, 'slds-is-open');
        $A.util.removeClass(forOpen, 'slds-is-close');
        $A.util.removeClass(forOpen, 'slds-has-error');
        
        var message = component.find("requiredMessage");
        $A.util.addClass(message, 'slds-hide');
        $A.util.removeClass(message, 'slds-show');
        // Get Default 5 Records order by createdDate DESC  
        var getInputkeyWord = component.get("v.searchKeyWord");
        helper.searchHelper(component,event,getInputkeyWord);
    },
    
    onBlurInput : function(component, event, helper) {
        var getRecordId = component.get("v.lookupId");
        if(component.get("v.isRequired") && !component.get("v.getRecordId")) component.set("v.checkLookupValidation",true);
    },
    
    onblur : function(component,event,helper) {
        component.set("v.listOfSearchRecords",null);
        var forclose = component.find("searchRes");
        $A.util.addClass(forclose, 'slds-is-close');
        $A.util.removeClass(forclose, 'slds-is-open');
    },
    
    keyPressController : function(component, event, helper) {
        // get the search Input keyword   
        var getInputkeyWord = component.get("v.searchKeyWord");
        // check if getInputKeyWord size id more then 0 then open the lookup result List and 
        // call the helper 
        // else close the lookup result List part.   
        if(getInputkeyWord.length > 0){
            var forOpen = component.find("searchRes");
            $A.util.addClass(forOpen, 'slds-is-open');
            $A.util.removeClass(forOpen, 'slds-is-close');
            helper.searchHelper(component,event,getInputkeyWord);
        } else {
            component.set("v.listOfSearchRecords", null ); 
            var forclose = component.find("searchRes");
            $A.util.addClass(forclose, 'slds-is-close');
            $A.util.removeClass(forclose, 'slds-is-open');
        }
    },
    
    // function for clear the Record Selaction 
    clear :function(component,event,heplper){
        var pillTarget = component.find("lookup-pill");
        var lookUpTarget = component.find("lookupField"); 
        
        $A.util.addClass(pillTarget, 'slds-hide');
        $A.util.removeClass(pillTarget, 'slds-show');
        
        $A.util.addClass(lookUpTarget, 'slds-show');
        $A.util.removeClass(lookUpTarget, 'slds-hide');
        
        component.set("v.searchKeyWord","");
        component.set("v.listOfSearchRecords", null);
        component.set("v.selectedRecord",{});
        if(!!component.get("v.lookupId")) component.set("v.isEdited",true);
        component.set("v.lookupId","");
        if(component.get("v.isRequired")) component.set("v.checkLookupValidation",true);
        if(component.get("v.objectAPIName") == "Airport__c" && !component.get("v.isDisabled")) {
            $A.enqueueAction(component.get("v.airportRoundAux"));
        }
    },
    
    // This function call when the end User Select any record from the result list.   
    handleSelectItemEvent : function(component, event, helper) {
        var selectedRecord = event.getParam("recordByEvent");
        component.set("v.selectedRecord" , selectedRecord); 
        var objectAPIName = component.get("v.objectAPIName");
        var fieldName = component.get("v.fieldName");
        var pillText = "";
        component.set("v.lookupId",selectedRecord.Id);
        if(objectAPIName == "Account" && fieldName == "Venue_City__c") component.set("v.lookupId",selectedRecord.City__c);
        pillText = selectedRecord.Name;
        switch(objectAPIName) {
            case "Account":
                switch(fieldName) {
                    case "Venue_City__c":
                        pillText = selectedRecord.City__r.Name;
                        break;
                    case "Venue__c":
                        break;
                }
                break;
            case "City__c":
                /*
                var city = oRecord.City__c;
                var state = oRecord.hasOwnProperty("State__c")? oRecord.State__c : "";
                var country = oRecord.hasOwnProperty("Country__c")? oRecord.Country__c : "";
                pillText = city + ", " + (!!state? state + ", " + country : country);
                */
                break;
            case "Airport__c":
                break;
            default:
                break;
        }
        component.set("v.pillText",pillText);
        component.set("v.isEdited",true);
        
        var forclose = component.find("lookup-pill");
        $A.util.addClass(forclose, 'slds-show');
        $A.util.removeClass(forclose, 'slds-hide');
        
        var forclose = component.find("searchRes");
        $A.util.addClass(forclose, 'slds-is-close');
        $A.util.removeClass(forclose, 'slds-is-open');
        $A.util.removeClass(forclose, 'slds-has-error');
        
        var message = component.find("requiredMessage");
        $A.util.addClass(message, 'slds-hide');
        $A.util.removeClass(message, 'slds-show');
        
        var lookUpTarget = component.find("lookupField");
        $A.util.addClass(lookUpTarget, 'slds-hide');
        $A.util.removeClass(lookUpTarget, 'slds-show');  
        if(!component.get("v.isDisabled")) {
            switch(objectAPIName) {
                case "Account":
                    switch(fieldName) {
                        case "Venue_City__c":
                            component.set("v.venueId",selectedRecord.Id);
                            component.set("v.cityId",selectedRecord.City__c);
                            $A.enqueueAction(component.get("v.lodgingVenueAux"));
                            $A.enqueueAction(component.get("v.lodgingCityAux"));
                            break;
                        case "Venue__c":
                            if(selectedRecord.hasOwnProperty("City__c")) {
                                component.set("v.venueCityId",selectedRecord.City__c);
                                component.set("v.cityId",selectedRecord.City__c);
                                $A.enqueueAction(component.get("v.lodgingVenueCityAux"));
                                $A.enqueueAction(component.get("v.lodgingCityAux"));
                            }
                            break;
                    }
                    break;
                case "City__c":
                    break;
                case "Airport__c":
                    $A.enqueueAction(component.get("v.airportRoundAux"));
                    break;
                default:
                    break;
            }
        }
    },
})
```
### VoyajerCustomLookup

```
<aura:component controller="VoyajerCustomLookup" implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction" access="global">
	<aura:attribute type="List" name="listOfSearchRecords" description="Use,for store the list of search records which returns from apex class" />
    <aura:attribute type="sObject" name="selectedRecord" default="{}" description="Use,for store SELECTED sObject Record" />
    <aura:attribute type="String" name="lookupId" description="Use for store the recordId used in the form" />
    <aura:attribute type="String" name="venueCityId" description="" />
    <aura:attribute type="String" name="venueId" description="" />
    <aura:attribute type="String" name="cityId" description="" />
    <aura:attribute type="String" name="fieldName" default="" />
    <aura:attribute type="String" name="searchKeyWord" default="" />
    <aura:attribute type="String" name="objectAPIName" default="" />
    <aura:attribute type="String" name="pillText" default="Pill text" />
    <aura:attribute type="String" name="iconName" default="" />
    <aura:attribute type="String" name="label" default="" />
    <aura:attribute type="String" name="inputPlaceholder" default="Search..." />
    <aura:attribute type="String" name="message" default="" />
    <aura:attribute type="Boolean" name="isRequired" default="false" />
    <aura:attribute type="Boolean" name="isEdited" default="false" />
    <aura:attribute type="Boolean" name="isDisabled" default="false" />
    <aura:attribute type="Boolean" name="triggerLookupValidation" default="false" />
    <aura:attribute type="Boolean" name="checkLookupValidation" default="false" />
    <aura:attribute type="Boolean" name="loadVenueCityLookup" default="false" />
    <aura:attribute type="Boolean" name="loadVenueLookup" default="false" />
    <aura:attribute type="Boolean" name="loadCityLookup" default="false" />
    
    <aura:attribute type="Aura.action" name="lodgingVenueCityAux" />
    <aura:attribute type="Aura.action" name="lodgingVenueAux" />
    <aura:attribute type="Aura.action" name="lodgingCityAux" />
    <aura:attribute type="Aura.action" name="airportRoundAux" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:handler name="change" value="{!v.triggerLookupValidation}" action="{!c.showError}" />
    <aura:handler name="change" value="{!v.checkLookupValidation}" action="{!c.onLookupIdEmpty}" />
    <aura:handler name="change" value="{!v.loadVenueCityLookup}" action="{!c.onLoadLookup}" />
    <aura:handler name="change" value="{!v.loadVenueLookup}" action="{!c.onLoadLookup}" />
    <aura:handler name="change" value="{!v.loadCityLookup}" action="{!c.onLoadLookup}" />
    <aura:handler name="callToLookup" action="{!c.handleSelectItemEvent}" event="c:VoyajerCallToLookup" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

    <div aura:id="searchRes" class="slds-form-element slds-lookup slds-is-close" data-select="single" onmouseleave="{!c.onblur}">
        <label class="lookupFieldLabel slds-form-element__label" for="lookup-348">
            {!v.label}
            <aura:if isTrue="{!v.fieldName=='City__c'}"><span> City, State, Country</span></aura:if>
        </label>
        <!--This part is for display search bar for lookup-->  
        <div class="slds-form-element__control">
            <div class="slds-input-has-icon slds-input-has-icon--right">
                <!-- This markup is for when an record is selected -->
                <div aura:id="lookup-pill" class="slds-pill-container slds-hide">
                    <lightning:pill class="{!if(v.isDisabled,'pillSize lookupPill','pillSize')}" label="{!v.pillText}" name="{!v.pillText}" onremove="{!c.clear}">
                        <aura:set attribute="media">
                            <lightning:icon iconName="{!v.iconName}" size="x-small" alternativeText="{!v.iconName}"/>
                        </aura:set>
                    </lightning:pill>
                </div>
                <div aura:id="lookupField" class="slds-show">
                    <aura:if isTrue="{!!v.isDisabled}">
                        <lightning:icon class="slds-input__icon slds-show" iconName="utility:search" size="x-small" alternativeText="search"/>
                    </aura:if>
                    <span class="slds-icon_container  slds-combobox__input-entity-icon" title="record">
                        <lightning:icon class="slds-icon slds-icon slds-icon_small slds-icon-text-default" iconName="{!v.iconName}" size="x-small" alternativeText="icon"/>
                        <span class="slds-assistive-text"></span>
                    </span>
                    <ui:inputText aura:id="lookupInput"
                                  class="slds-lookup__search-input slds-input leftPaddingClass lookupFieldInput" 
                                  click="{!c.onfocus}" 
                                  updateOn="keyup" 
                                  keyup="{!c.keyPressController}" 
                                  blur="{!c.onBlurInput}" 
                                  value="{!v.searchKeyWord}" 
                                  placeholder="{!v.inputPlaceholder}" 
                                  required="{!v.isRequired}" 
                                  requiredIndicatorClass="slds-has-error" 
                                  disabled="{!v.isDisabled}" />
                </div>
            </div>
        </div>
        <!--This part is for Display typehead lookup result List-->  
        <ul style="min-height:40px;margin-top:0px !important" class="slds-listbox slds-listbox_vertical slds-dropdown slds-dropdown_fluid slds-lookup__menu slds" role="listbox">
            <lightning:spinner aura:id="mySpinner" class="slds-hide" variant="brand" size="small" />
            <center> {!v.message}</center>
            <aura:iteration items="{!v.listOfSearchRecords}" var="oRecord">
                <c:VoyajerCustomLookupItem oRecord="{!oRecord}" iconName="{!v.iconName}" objectAPIName="{!v.objectAPIName}" fieldName="{!v.fieldName}" searchKeyWord="{!v.searchKeyWord}" />
            </aura:iteration>
        </ul>
        <div aura:id="requiredMessage" class="slds-form-element__help slds-hide" id="error-message-unique-id">This field is required</div>
    </div>
</aura:component>
```
### VoyajerCustomLookupHelper

```
({
    searchHelper : function(component, event, getInputkeyWord) {
        // call the apex class method 
        var action = component.get("c.fetchLookupValues");
        // set param to method  
        action.setParams({
            'searchKeyWord': getInputkeyWord,
            'sObjectName' : component.get("v.objectAPIName"),
            'fieldName' : component.get("v.fieldName")
        });
        // set a callBack    
        action.setCallback(this, function(response) {
            $A.util.removeClass(component.find("mySpinner"), "slds-show");
            var state = response.getState();
            if (state === "SUCCESS") {
                var storeResponse = response.getReturnValue();
                // if storeResponse size is equal 0 ,display No Result Found... message on screen.                }
                if (storeResponse.length == 0) {
                    var fieldName = component.get("v.fieldName");
                    component.set("v.message", 'No Result Found...');
                    if(fieldName == "Venue_City__c" || fieldName == "Venue__c") component.set("v.message", 'No results were found, please use Other Venue field.');
                } else {
                    component.set("v.message", '');
                }
                // set searchResult list with return value from server.
                component.set("v.listOfSearchRecords", storeResponse);
                //console.log(storeResponse);
            }
        });
        // enqueue the Action  
        $A.enqueueAction(action);
    },
    
    loadSavedRecord : function(component, event, getRecordId, objectAPIName) {
        component.set("v.checkLookupValidation",false);
        var forOpen = component.find("searchRes");
        var message = component.find("requiredMessage");
        $A.util.removeClass(forOpen, 'slds-has-error');
        $A.util.addClass(message, 'slds-hide');
        $A.util.removeClass(message, 'slds-show');
        
        component.set("v.selectedRecord",{});
        var action = component.get("c.loadLookupValues");
        action.setParams({
            'recordId': getRecordId,
            'sObjectName' : component.get("v.objectAPIName"),
            'fieldName' : component.get("v.fieldName")
        });
        action.setCallback(this, function(response) {
            $A.util.removeClass(component.find("mySpinner"), "slds-show");
            var state = response.getState();
            if (state === "SUCCESS") {
                var record = response.getReturnValue();
                component.set("v.selectedRecord" ,record); 
                var objectAPIName = component.get("v.objectAPIName");
                var fieldName = component.get("v.fieldName");
                var pillText = record.Name;
                switch(objectAPIName) {
                    case "Account":
                        switch(fieldName) {
                            case "Venue_City__c":
                                //pillText = recordS.City__r.Name;
                                break;
                            case "Venue__c":
                                break;
                        }
                        break;
                    case 'City__c':
                        break;
                    default:
                        break;
                }
                component.set("v.pillText",pillText);
                var forclose = component.find("lookup-pill");
                $A.util.addClass(forclose, 'slds-show');
                $A.util.removeClass(forclose, 'slds-hide');
                
                var forclose = component.find("searchRes");
                $A.util.addClass(forclose, 'slds-is-close');
                $A.util.removeClass(forclose, 'slds-is-open');
                
                var lookUpTarget = component.find("lookupField");
                $A.util.addClass(lookUpTarget, 'slds-hide');
                $A.util.removeClass(lookUpTarget, 'slds-show'); 
            }
        });
        // enqueue the Action  
        $A.enqueueAction(action);
    }
})
```
### VoyajerCustomLookup

```
.THIS .leftPaddingClass {
    padding-left: 2rem;
}

.THIS .pillSize{
    width:100%;
}

.THIS .lookupFieldInput {
    min-height: calc(1.875rem + 2px);
}

.THIS .lookupFieldLabel > span {
    font-size: 0.8em;
    font-weight: 400;
    padding-left: 0.75em;
}

.THIS .lookupPill .slds-pill__remove {
    display: none !important;
}
```

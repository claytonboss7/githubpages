---
layout: default
title: VoyajerCustomLookupItem
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerCustomLookupItem
## Fields
### VoyajerCustomLookupItem

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCustomLookupItem

```
<aura:component implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction" access="global">
    <aura:attribute type="sObject" name="oRecord" />
    <aura:attribute type="String" name="iconName" />
    <aura:attribute type="String" name="objectAPIName" />
    <aura:attribute type="String" name="fieldName" default="" />
    <aura:attribute type="String" name="searchKeyWord" />
    <aura:attribute type="String" name="iconDescription" default="" />
    <aura:attribute type="String" name="optionText" default="" />
    <aura:attribute type="String" name="optionMeta" default="" />
    
    <!--Register the component level event-->
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:registerEvent type="c:VoyajerCallToLookup" name="callToLookup" />
    
    <li role="presentation" class="slds-listbox__item" onclick="{!c.onSelectRecord}">
        <span class="slds-media slds-listbox__option slds-listbox__option_entity slds-listbox__option_has-meta" role="option">
            <span class="slds-media__figure">
                <span class="slds-icon_container" title="{!v.iconDescription}">
                    <lightning:icon iconName="{!v.iconName}" class="slds-icon slds-icon_small" size="small" alternativeText="icon"/>
                    <span class="slds-assistive-text">{!v.iconDescription}</span>
                </span>
            </span>    
            <span class="slds-media__body"> 
                <span class="slds-listbox__option-text slds-listbox__option-text_entity"><span><lightning:formattedRichText value="{!v.optionText}" /></span></span>
                <span class="slds-listbox__option-meta slds-listbox__option-meta_entity"><span><lightning:formattedRichText value="{!v.optionMeta}" /></span></span>
            </span>
        </span>
    </li>
</aura:component>
```
### VoyajerCustomLookupItemController

```
({
    doInit : function(component, event, helper) {
        var objectAPIName = component.get("v.objectAPIName");
        var fieldName = component.get("v.fieldName");
        var searchKeyWord = component.get("v.searchKeyWord");
        var oRecord = component.get("v.oRecord");
        var optionText = oRecord.Name;
        var optionMeta = objectAPIName;
        switch(objectAPIName) {
            case "City__c":
                component.set("v.iconDescription","City");
                var city = oRecord.City__c;
                var state = oRecord.hasOwnProperty("State__c")? oRecord.State__c : "";
                var country = oRecord.hasOwnProperty("Country__c")? oRecord.Country__c : "";
                if(!!searchKeyWord) {
                    if(city.length >= searchKeyWord.length && city.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) city = "<mark>"+city.substring(0,searchKeyWord.length)+"</mark>"+city.substring(searchKeyWord.length);
                    if(state.length >= searchKeyWord.length && state.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) state = "<mark>"+state.substring(0,searchKeyWord.length)+"</mark>"+state.substring(searchKeyWord.length);
                    if(country.length >= searchKeyWord.length && country.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) country = "<mark>"+country.substring(0,searchKeyWord.length)+"</mark>"+country.substring(searchKeyWord.length);
                }
                optionText = city;
                optionMeta = "City" + " • " + (!!state? state + ", " + country : country);
                /*
                if(!!searchKeyWord) {
                    var city = oRecord.City__c;
                    if(city != null && city.length >= searchKeyWord.length && city.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) {
                        city = "<b>"+city.substring(0,searchKeyWord.length)+"</b>"+city.substring(searchKeyWord.length);
                    }
                } else optionText = oRecord.Name;
                var state = oRecord.State__c;
                var country = oRecord.Country__c;
                */
                break;
            case "Airport__c":
                component.set("v.iconDescription","Airport");
                var airport = oRecord.Name;
                var pax = oRecord.hasOwnProperty("Airport_Code__c")? oRecord.Airport_Code__c : "";
                if(!!searchKeyWord) {
                    if(airport.length >= searchKeyWord.length && airport.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) airport = "<mark>"+airport.substring(0,searchKeyWord.length)+"</mark>"+airport.substring(searchKeyWord.length);
                    if(pax.length >= searchKeyWord.length && pax.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) pax = "<mark>"+pax.substring(0,searchKeyWord.length)+"</mark>"+pax.substring(searchKeyWord.length);
                }
                optionText = airport;
                optionMeta = "Airport" + " • " + (!!pax? pax : "");
                break;
            case "Account":
                switch(fieldName) {
                    case "Venue_City__c":
                        var venueStreet = oRecord.hasOwnProperty("ShippingStreet")? oRecord.ShippingStreet : "";
                        var venueCity = oRecord.hasOwnProperty("ShippingCity")? oRecord.ShippingCity : "";
                        var venueState = oRecord.hasOwnProperty("ShippingState")? oRecord.ShippingState : "";
                        var venuePostalCode = oRecord.hasOwnProperty("ShippingPostalCode")? oRecord.ShippingPostalCode : "";
                        var cityRecord = oRecord.City__r;
                        var city = cityRecord.hasOwnProperty("City__c")? cityRecord.City__c : "";
                        var state = cityRecord.hasOwnProperty("State__c")? cityRecord.State__c : "";
                        var country = cityRecord.hasOwnProperty("Country__c")? cityRecord.Country__c : "";
                        if(!!searchKeyWord) {
                            if(city.length >= searchKeyWord.length && city.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) city = "<mark>"+city.substring(0,searchKeyWord.length)+"</mark>"+city.substring(searchKeyWord.length);
                            if(state.length >= searchKeyWord.length && state.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) state = "<mark>"+state.substring(0,searchKeyWord.length)+"</mark>"+state.substring(searchKeyWord.length);
                            if(country.length >= searchKeyWord.length && country.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) country = "<mark>"+country.substring(0,searchKeyWord.length)+"</mark>"+country.substring(searchKeyWord.length);
                        }
                        optionText = (!!city? city : "") + ", " + (!!state? state : "") + ", " + (!!country? country : "");
                        optionMeta = "Venue City" + " • " + oRecord.Name + " - " + (!!venueStreet? venueStreet + " " : "") + (!!venueCity? venueCity + ", " : "") + (!!venueState? venueState + " " : "") + (!!venuePostalCode? venuePostalCode : "");
                        break;
                    case "Venue__c":
                        break;
                    default:
                        break;
                }
                break;
            default:
                break;
        }
        component.set("v.optionMeta",optionMeta);
        component.set("v.optionText",optionText);
    },
    
    onSelectRecord : function(component, event, helper) {
		var oRecord = component.get("v.oRecord");
        var callToLookup = component.getEvent("callToLookup");
        callToLookup.setParam("recordByEvent",oRecord);
        callToLookup.fire();
	}
})
```
### VoyajerCustomLookupItem

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCustomLookupItem

```
<aura:component implements="force:appHostable,flexipage:availableForAllPageTypes,flexipage:availableForRecordHome,force:hasRecordId,forceCommunity:availableForAllPageTypes,force:lightningQuickAction" access="global">
    <aura:attribute type="sObject" name="oRecord" />
    <aura:attribute type="String" name="iconName" />
    <aura:attribute type="String" name="objectAPIName" />
    <aura:attribute type="String" name="fieldName" default="" />
    <aura:attribute type="String" name="searchKeyWord" />
    <aura:attribute type="String" name="iconDescription" default="" />
    <aura:attribute type="String" name="optionText" default="" />
    <aura:attribute type="String" name="optionMeta" default="" />
    
    <!--Register the component level event-->
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:registerEvent type="c:VoyajerCallToLookup" name="callToLookup" />
    
    <li role="presentation" class="slds-listbox__item" onclick="{!c.onSelectRecord}">
        <span class="slds-media slds-listbox__option slds-listbox__option_entity slds-listbox__option_has-meta" role="option">
            <span class="slds-media__figure">
                <span class="slds-icon_container" title="{!v.iconDescription}">
                    <lightning:icon iconName="{!v.iconName}" class="slds-icon slds-icon_small" size="small" alternativeText="icon"/>
                    <span class="slds-assistive-text">{!v.iconDescription}</span>
                </span>
            </span>    
            <span class="slds-media__body"> 
                <span class="slds-listbox__option-text slds-listbox__option-text_entity"><span><lightning:formattedRichText value="{!v.optionText}" /></span></span>
                <span class="slds-listbox__option-meta slds-listbox__option-meta_entity"><span><lightning:formattedRichText value="{!v.optionMeta}" /></span></span>
            </span>
        </span>
    </li>
</aura:component>
```
### VoyajerCustomLookupItemController

```
({
    doInit : function(component, event, helper) {
        var objectAPIName = component.get("v.objectAPIName");
        var fieldName = component.get("v.fieldName");
        var searchKeyWord = component.get("v.searchKeyWord");
        var oRecord = component.get("v.oRecord");
        var optionText = oRecord.Name;
        var optionMeta = objectAPIName;
        switch(objectAPIName) {
            case "City__c":
                component.set("v.iconDescription","City");
                var city = oRecord.City__c;
                var state = oRecord.hasOwnProperty("State__c")? oRecord.State__c : "";
                var country = oRecord.hasOwnProperty("Country__c")? oRecord.Country__c : "";
                if(!!searchKeyWord) {
                    if(city.length >= searchKeyWord.length && city.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) city = "<mark>"+city.substring(0,searchKeyWord.length)+"</mark>"+city.substring(searchKeyWord.length);
                    if(state.length >= searchKeyWord.length && state.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) state = "<mark>"+state.substring(0,searchKeyWord.length)+"</mark>"+state.substring(searchKeyWord.length);
                    if(country.length >= searchKeyWord.length && country.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) country = "<mark>"+country.substring(0,searchKeyWord.length)+"</mark>"+country.substring(searchKeyWord.length);
                }
                optionText = city;
                optionMeta = "City" + " • " + (!!state? state + ", " + country : country);
                /*
                if(!!searchKeyWord) {
                    var city = oRecord.City__c;
                    if(city != null && city.length >= searchKeyWord.length && city.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) {
                        city = "<b>"+city.substring(0,searchKeyWord.length)+"</b>"+city.substring(searchKeyWord.length);
                    }
                } else optionText = oRecord.Name;
                var state = oRecord.State__c;
                var country = oRecord.Country__c;
                */
                break;
            case "Airport__c":
                component.set("v.iconDescription","Airport");
                var airport = oRecord.Name;
                var pax = oRecord.hasOwnProperty("Airport_Code__c")? oRecord.Airport_Code__c : "";
                if(!!searchKeyWord) {
                    if(airport.length >= searchKeyWord.length && airport.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) airport = "<mark>"+airport.substring(0,searchKeyWord.length)+"</mark>"+airport.substring(searchKeyWord.length);
                    if(pax.length >= searchKeyWord.length && pax.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) pax = "<mark>"+pax.substring(0,searchKeyWord.length)+"</mark>"+pax.substring(searchKeyWord.length);
                }
                optionText = airport;
                optionMeta = "Airport" + " • " + (!!pax? pax : "");
                break;
            case "Account":
                switch(fieldName) {
                    case "Venue_City__c":
                        var venueStreet = oRecord.hasOwnProperty("ShippingStreet")? oRecord.ShippingStreet : "";
                        var venueCity = oRecord.hasOwnProperty("ShippingCity")? oRecord.ShippingCity : "";
                        var venueState = oRecord.hasOwnProperty("ShippingState")? oRecord.ShippingState : "";
                        var venuePostalCode = oRecord.hasOwnProperty("ShippingPostalCode")? oRecord.ShippingPostalCode : "";
                        var cityRecord = oRecord.City__r;
                        var city = cityRecord.hasOwnProperty("City__c")? cityRecord.City__c : "";
                        var state = cityRecord.hasOwnProperty("State__c")? cityRecord.State__c : "";
                        var country = cityRecord.hasOwnProperty("Country__c")? cityRecord.Country__c : "";
                        if(!!searchKeyWord) {
                            if(city.length >= searchKeyWord.length && city.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) city = "<mark>"+city.substring(0,searchKeyWord.length)+"</mark>"+city.substring(searchKeyWord.length);
                            if(state.length >= searchKeyWord.length && state.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) state = "<mark>"+state.substring(0,searchKeyWord.length)+"</mark>"+state.substring(searchKeyWord.length);
                            if(country.length >= searchKeyWord.length && country.substring(0,searchKeyWord.length).toLowerCase() == searchKeyWord.toLowerCase()) country = "<mark>"+country.substring(0,searchKeyWord.length)+"</mark>"+country.substring(searchKeyWord.length);
                        }
                        optionText = (!!city? city : "") + ", " + (!!state? state : "") + ", " + (!!country? country : "");
                        optionMeta = "Venue City" + " • " + oRecord.Name + " - " + (!!venueStreet? venueStreet + " " : "") + (!!venueCity? venueCity + ", " : "") + (!!venueState? venueState + " " : "") + (!!venuePostalCode? venuePostalCode : "");
                        break;
                    case "Venue__c":
                        break;
                    default:
                        break;
                }
                break;
            default:
                break;
        }
        component.set("v.optionMeta",optionMeta);
        component.set("v.optionText",optionText);
    },
    
    onSelectRecord : function(component, event, helper) {
		var oRecord = component.get("v.oRecord");
        var callToLookup = component.getEvent("callToLookup");
        callToLookup.setParam("recordByEvent",oRecord);
        callToLookup.fire();
	}
})
```

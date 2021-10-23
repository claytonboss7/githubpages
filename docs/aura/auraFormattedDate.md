---
layout: default
title: auraFormattedDate
parent: aura
---
# Metadata Type
CustomObject

# Name
auraFormattedDate
## Fields
### auraFormattedDate

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### auraFormattedDateController

```
({
	onInit : function(component, event, helper){
        //console.log('component.get("v.date"): ' + component.get("v.date"));
		if(!$A.util.isEmpty(component.get("v.date"))) component.set("v.dateFormatted", $A.localizationService.formatDate(component.get("v.date"), component.get("v.dateFormat")));
        //console.log('component.get("v.dateFormatted"): ' + component.get("v.dateFormatted"));
	}
})
```
### auraFormattedDate

```
<aura:component >
    <aura:attribute name="date" type="String" required="true"/>	
    <aura:attribute name="dateFormat" type="String" required="true" default="dd MM yyyy"/>	
    <aura:attribute name="dateFormatted" type="String" access="private" default=""/>	
    
    <aura:handler name="init" value="{!this}" action="{!c.onInit}" />    
    {!v.dateFormatted}
</aura:component>
```
### auraFormattedDate

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### auraFormattedDateController

```
({
	onInit : function(component, event, helper){
        //console.log('component.get("v.date"): ' + component.get("v.date"));
		if(!$A.util.isEmpty(component.get("v.date"))) component.set("v.dateFormatted", $A.localizationService.formatDate(component.get("v.date"), component.get("v.dateFormat")));
        //console.log('component.get("v.dateFormatted"): ' + component.get("v.dateFormatted"));
	}
})
```
### auraFormattedDate

```
<aura:component >
    <aura:attribute name="date" type="String" required="true"/>	
    <aura:attribute name="dateFormat" type="String" required="true" default="dd MM yyyy"/>	
    <aura:attribute name="dateFormatted" type="String" access="private" default=""/>	
    
    <aura:handler name="init" value="{!this}" action="{!c.onInit}" />    
    {!v.dateFormatted}
</aura:component>
```

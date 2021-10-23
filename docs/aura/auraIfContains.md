---
layout: default
title: auraIfContains
parent: aura
---
# Metadata Type
CustomObject

# Name
auraIfContains
## Fields
### auraIfContains

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### auraIfContains

```
<aura:component>
    <aura:attribute type="List" name="items" required="true" />
    <aura:attribute type="String" name="element" required="true" />
    <aura:attribute type="Boolean" name="condition" default="default" />
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    
    <aura:if isTrue="{!v.condition}">
        {!v.body}
    </aura:if>
</aura:component>
```
### auraIfContainsController

```
({
	doInit : function(component, event, helper) {
		var items = component.get("v.items");
        var element = component.get("v.element");
        var elementIndex = items.indexOf(element);
        if(elementIndex != -1) component.set("v.condition",true);
        else component.set("v.condition",false);
	}
})
```
### auraIfContains

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### auraIfContains

```
<aura:component>
    <aura:attribute type="List" name="items" required="true" />
    <aura:attribute type="String" name="element" required="true" />
    <aura:attribute type="Boolean" name="condition" default="default" />
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    
    <aura:if isTrue="{!v.condition}">
        {!v.body}
    </aura:if>
</aura:component>
```
### auraIfContainsController

```
({
	doInit : function(component, event, helper) {
		var items = component.get("v.items");
        var element = component.get("v.element");
        var elementIndex = items.indexOf(element);
        if(elementIndex != -1) component.set("v.condition",true);
        else component.set("v.condition",false);
	}
})
```

---
layout: default
title: reportSearchComponent
parent: aura
---
# Metadata Type
CustomObject

# Name
reportSearchComponent
## Fields
### reportSearchComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportSearchComponent

```
<aura:component implements="flexipage:availableForAllPageTypes">
	<aura:registerEvent name="rLoadEvent" type="c:reportLoadEvent"/>   
	<aura:attribute name="report" type="Report"/>
    <li class="ui-screen-hidden">
        <a href="javascript:void(0);" onclick="{!c.showReport}">{!v.report.Name}</a>
    </li>    
</aura:component>
```
### reportSearchComponentController

```
({
    showReport : function(component, event, helper) {
	 	var report = component.get("v.report");        
		var rLoadEvent = $A.get("e.c:reportLoadEvent");
		rLoadEvent.setParams({"report": report});
		rLoadEvent.fire();
    }  
})
```
### reportSearchComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportSearchComponent

```
<aura:component implements="flexipage:availableForAllPageTypes">
	<aura:registerEvent name="rLoadEvent" type="c:reportLoadEvent"/>   
	<aura:attribute name="report" type="Report"/>
    <li class="ui-screen-hidden">
        <a href="javascript:void(0);" onclick="{!c.showReport}">{!v.report.Name}</a>
    </li>    
</aura:component>
```
### reportSearchComponentController

```
({
    showReport : function(component, event, helper) {
	 	var report = component.get("v.report");        
		var rLoadEvent = $A.get("e.c:reportLoadEvent");
		rLoadEvent.setParams({"report": report});
		rLoadEvent.fire();
    }  
})
```

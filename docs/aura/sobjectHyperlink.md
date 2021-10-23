---
layout: default
title: sobjectHyperlink
parent: aura
---
# Metadata Type
CustomObject

# Name
sobjectHyperlink
## Fields
### sobjectHyperlinkController

```
({
	navigateToSObject : function(component, event, helper) {
		var sObjId = component.get("v.sObjectId");          
        var navToSObjEvt = $A.get("e.force:navigateToSObject");
        navToSObjEvt.setParams({
            recordId: sObjId,
            slideDevName: "detail"
        });	
        navToSObjEvt.fire(); 
	}
})
```
### sobjectHyperlink

```
<aura:component >
	<aura:attribute name="sObjectId" type="Id" />
    <aura:attribute name="hyperlinkLabel" type="String" />
	<a href="javascript:void(0);" onclick="{!c.navigateToSObject}">{!v.hyperlinkLabel}</a>
</aura:component>
```
### sobjectHyperlink

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### sobjectHyperlinkController

```
({
	navigateToSObject : function(component, event, helper) {
		var sObjId = component.get("v.sObjectId");          
        var navToSObjEvt = $A.get("e.force:navigateToSObject");
        navToSObjEvt.setParams({
            recordId: sObjId,
            slideDevName: "detail"
        });	
        navToSObjEvt.fire(); 
	}
})
```
### sobjectHyperlink

```
<aura:component >
	<aura:attribute name="sObjectId" type="Id" />
    <aura:attribute name="hyperlinkLabel" type="String" />
	<a href="javascript:void(0);" onclick="{!c.navigateToSObject}">{!v.hyperlinkLabel}</a>
</aura:component>
```
### sobjectHyperlink

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```

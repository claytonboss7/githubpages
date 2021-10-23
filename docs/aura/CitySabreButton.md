---
layout: default
title: CitySabreButton
parent: aura
---
# Metadata Type
CustomObject

# Name
CitySabreButton
## Fields
### CitySabreButton

```
<aura:component controller="SabreWS" implements="flexipage:availableForAllPageTypes,force:hasRecordId,force:lightningQuickAction" >
    <aura:attribute name="messageError" type="String" />
    <aura:attribute name="messageErrorBoolean" type="Boolean" />
    <aura:attribute name="recordId" type="String" />
    
    <aura:handler name="init" value="{!this}" action="{!c.init}" />
    
    <aura:if isTrue="{!v.messageErrorBoolean}">
        <ui:message title="Error" severity="error" closable="false">
            {!v.messageError}
        </ui:message>
    </aura:if>
    <aura:if isTrue="{!!v.messageErrorBoolean}">
        <ui:message title="Information" severity="info" closable="false">
            {!v.messageError}
        </ui:message>
    </aura:if>
</aura:component>
```
### CitySabreButton

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### CitySabreButtonController

```
({
   init : function(component, event, helper) {
      var action = component.get("c.getIATACode");
      action.setParams({"cityId": component.get("v.recordId")});
      action.setCallback(this, function(response) {
         var state = response.getState();
         if(component.isValid() && state == "SUCCESS" && response.getReturnValue() == "Ok"){
            component.set("v.messageError", 'Success.');
			component.set("v.messageErrorBoolean", false);
			$A.get('e.force:refreshView').fire();
         } else {
            component.set("v.messageError", response.getReturnValue());
            component.set("v.messageErrorBoolean", true);
         }
      });
      $A.enqueueAction(action);
   }
})
```
### CitySabreButton

```
<aura:component controller="SabreWS" implements="flexipage:availableForAllPageTypes,force:hasRecordId,force:lightningQuickAction" >
    <aura:attribute name="messageError" type="String" />
    <aura:attribute name="messageErrorBoolean" type="Boolean" />
    <aura:attribute name="recordId" type="String" />
    
    <aura:handler name="init" value="{!this}" action="{!c.init}" />
    
    <aura:if isTrue="{!v.messageErrorBoolean}">
        <ui:message title="Error" severity="error" closable="false">
            {!v.messageError}
        </ui:message>
    </aura:if>
    <aura:if isTrue="{!!v.messageErrorBoolean}">
        <ui:message title="Information" severity="info" closable="false">
            {!v.messageError}
        </ui:message>
    </aura:if>
</aura:component>
```
### CitySabreButton

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### CitySabreButtonController

```
({
   init : function(component, event, helper) {
      var action = component.get("c.getIATACode");
      action.setParams({"cityId": component.get("v.recordId")});
      action.setCallback(this, function(response) {
         var state = response.getState();
         if(component.isValid() && state == "SUCCESS" && response.getReturnValue() == "Ok"){
            component.set("v.messageError", 'Success.');
			component.set("v.messageErrorBoolean", false);
			$A.get('e.force:refreshView').fire();
         } else {
            component.set("v.messageError", response.getReturnValue());
            component.set("v.messageErrorBoolean", true);
         }
      });
      $A.enqueueAction(action);
   }
})
```

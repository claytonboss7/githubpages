---
layout: default
title: OpportunityView
parent: aura
---
# Metadata Type
CustomObject

# Name
OpportunityView
## Fields
### OpportunityViewHelper

```
({
	helperMethod : function() {
		
	}
})
```
### OpportunityView

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### OpportunityView

```
<aura:component controller="ProductionAssociationCtrl" implements="lightning:actionOverride,flexipage:availableForRecordHome,force:hasRecordId,force:lightningQuickAction" access="global" >
    <aura:handler name="render" value="{!this}" action="{!c.doInit}" />
</aura:component>
```
### OpportunityViewController

```
({
	doInit : function(component, event, helper) {
    	var action = component.get("c.getOpportunityId");
		action.setParams({prodAssId: component.get("v.recordId")});
		action.setCallback(this, function(response){
			var state = response.getState();
			if(state === "SUCCESS"){
                var rID = response.getReturnValue();
                console.log(rID);
                var navEvt = $A.get("e.force:navigateToSObject");
                navEvt.setParams({
                  "recordId": rID,
                  "slideDevName": "related"
                });
                navEvt.fire();
                   
			}
        });
		$A.enqueueAction(action);
  	}
})
```
### OpportunityViewHelper

```
({
	helperMethod : function() {
		
	}
})
```
### OpportunityView

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### OpportunityView

```
<aura:component controller="ProductionAssociationCtrl" implements="lightning:actionOverride,flexipage:availableForRecordHome,force:hasRecordId,force:lightningQuickAction" access="global" >
    <aura:handler name="render" value="{!this}" action="{!c.doInit}" />
</aura:component>
```
### OpportunityViewController

```
({
	doInit : function(component, event, helper) {
    	var action = component.get("c.getOpportunityId");
		action.setParams({prodAssId: component.get("v.recordId")});
		action.setCallback(this, function(response){
			var state = response.getState();
			if(state === "SUCCESS"){
                var rID = response.getReturnValue();
                console.log(rID);
                var navEvt = $A.get("e.force:navigateToSObject");
                navEvt.setParams({
                  "recordId": rID,
                  "slideDevName": "related"
                });
                navEvt.fire();
                   
			}
        });
		$A.enqueueAction(action);
  	}
})
```

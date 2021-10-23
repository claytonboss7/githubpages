---
layout: default
title: VoyajerNewProduction
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerNewProduction
## Fields
### VoyajerNewProductionController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        component.set('v.today', today);
	},
    
    newProduction : function(component, event, helper) {
        event.preventDefault();
        var productionName = "";
        var startDate = "";
        var validExpense = component.find('newProduction').reduce(function (validSoFar, inputComponent) {
            // Displays error messages for invalid fields
            if(inputComponent.get("v.name") == "productionName") productionName = inputComponent.get("v.value");
            if(inputComponent.get("v.name") == "startDate") startDate = inputComponent.get("v.value");
            inputComponent.showHelpMessageIfInvalid();
            return validSoFar && inputComponent.get('v.validity').valid;
        }, true);
        // If we pass error checking, do some real work
        
        if(validExpense){
            var data = {};
            data.productionName = productionName;
            data.startDate = startDate;
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","newProduction");
            callToParent.setParam("data",data);
            callToParent.fire();
        }
	},
    
    cancelForm : function(component, event, helper) {
        component.set("v.mainContent","dashboard");
    }
})
```
### VoyajerNewProduction

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerNewProduction

```
<aura:component >
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="Date" name="today" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 style="display: flex; align-items: center;">
                            <lightning:icon iconName="utility:add" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Add New Production</span>
                        </h1>
                    </div>
                </div>
                <div class="pageContentForm">
                    <div class="page-section">
                        <form class="slds-form-password">
                            <div class="formColumnTwoChildsWithDate">
                                <div class="formField">
                                    <label for="Name">Production Name</label>
                                    <lightning:input aura:id="newProduction"
                                                     name="productionName"
                                                     label=""
                                                     variant="label-hidden"
                                                     required="true" 
                                                     autocomplete="off" />
                                </div>
                                <div class="formField">
                                    <label for="Company">Company Name</label>
                                    <lightning:input name="Company"
                                                     label=""
                                                     value="{!v.userLogged.Contact.Account.Name}"
                                                     variant="label-hidden"
                                                     required="true"
                                                     disabled="true" 
                                                     autocomplete="off" />
                                </div>
                                <div class="formField">
                                    <label for="StartDate">Start Date</label>
                                    <lightning:input aura:id="newProduction"
                                                     name="startDate"
                                                     type="date"
                                                     label=""
                                                     min="{!v.today}"
                                                     variant="label-hidden"
                                                     required="true" 
                                                     autocomplete="off" />
                                </div>
                            </div>
                            <br />
                            <div style="text-align: right;">
                                <lightning:button label="Save" type="submit" variant="brand" class="formButtonBrandLight" onclick="{!c.newProduction}" />
                                <lightning:button label="Cancel" onclick="{!c.cancelForm}" />
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerNewProductionController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        component.set('v.today', today);
	},
    
    newProduction : function(component, event, helper) {
        event.preventDefault();
        var productionName = "";
        var startDate = "";
        var validExpense = component.find('newProduction').reduce(function (validSoFar, inputComponent) {
            // Displays error messages for invalid fields
            if(inputComponent.get("v.name") == "productionName") productionName = inputComponent.get("v.value");
            if(inputComponent.get("v.name") == "startDate") startDate = inputComponent.get("v.value");
            inputComponent.showHelpMessageIfInvalid();
            return validSoFar && inputComponent.get('v.validity').valid;
        }, true);
        // If we pass error checking, do some real work
        
        if(validExpense){
            var data = {};
            data.productionName = productionName;
            data.startDate = startDate;
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","newProduction");
            callToParent.setParam("data",data);
            callToParent.fire();
        }
	},
    
    cancelForm : function(component, event, helper) {
        component.set("v.mainContent","dashboard");
    }
})
```
### VoyajerNewProduction

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerNewProduction

```
<aura:component >
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="Date" name="today" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 style="display: flex; align-items: center;">
                            <lightning:icon iconName="utility:add" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Add New Production</span>
                        </h1>
                    </div>
                </div>
                <div class="pageContentForm">
                    <div class="page-section">
                        <form class="slds-form-password">
                            <div class="formColumnTwoChildsWithDate">
                                <div class="formField">
                                    <label for="Name">Production Name</label>
                                    <lightning:input aura:id="newProduction"
                                                     name="productionName"
                                                     label=""
                                                     variant="label-hidden"
                                                     required="true" 
                                                     autocomplete="off" />
                                </div>
                                <div class="formField">
                                    <label for="Company">Company Name</label>
                                    <lightning:input name="Company"
                                                     label=""
                                                     value="{!v.userLogged.Contact.Account.Name}"
                                                     variant="label-hidden"
                                                     required="true"
                                                     disabled="true" 
                                                     autocomplete="off" />
                                </div>
                                <div class="formField">
                                    <label for="StartDate">Start Date</label>
                                    <lightning:input aura:id="newProduction"
                                                     name="startDate"
                                                     type="date"
                                                     label=""
                                                     min="{!v.today}"
                                                     variant="label-hidden"
                                                     required="true" 
                                                     autocomplete="off" />
                                </div>
                            </div>
                            <br />
                            <div style="text-align: right;">
                                <lightning:button label="Save" type="submit" variant="brand" class="formButtonBrandLight" onclick="{!c.newProduction}" />
                                <lightning:button label="Cancel" onclick="{!c.cancelForm}" />
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```

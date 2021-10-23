---
layout: default
title: VoyajerCongaSign
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerCongaSign
## Fields
### VoyajerCongaSign

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCongaSignController

```
({
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	}
})
```
### VoyajerCongaSign

```
<aura:component implements="forceCommunity:availableForAllPageTypes" access="global">
    <aura:attribute name="mainContent" type="String"/>
    <aura:attribute name="parameters" type="String"/>

    <aura:handler name="render" value="{!this}" action="{!c.onRender}" />
    <div>
        <lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
        <div class="pageContent" style="min-height:680px;">
            <iframe src="{!'/apex/APXT_CongaSign__apxt_sendForSignature' + v.parameters}"
                    width="100%"
                    height="680px;"
                    frameBorder="0"
                    scrolling="true"/>	
        </div>
    </div>
</aura:component>
```
### VoyajerCongaSign

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCongaSignController

```
({
	onRender : function(component, event, helper){
		$A.util.addClass(component.find("loading"), "slds-hide");		
	}
})
```
### VoyajerCongaSign

```
<aura:component implements="forceCommunity:availableForAllPageTypes" access="global">
    <aura:attribute name="mainContent" type="String"/>
    <aura:attribute name="parameters" type="String"/>

    <aura:handler name="render" value="{!this}" action="{!c.onRender}" />
    <div>
        <lightning:spinner aura:id="loading" alternativeText="Loading" size="large" />
        <div class="pageContent" style="min-height:680px;">
            <iframe src="{!'/apex/APXT_CongaSign__apxt_sendForSignature' + v.parameters}"
                    width="100%"
                    height="680px;"
                    frameBorder="0"
                    scrolling="true"/>	
        </div>
    </div>
</aura:component>
```

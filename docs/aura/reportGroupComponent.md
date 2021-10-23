---
layout: default
title: reportGroupComponent
parent: aura
---
# Metadata Type
CustomObject

# Name
reportGroupComponent
## Fields
### reportGroupComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportGroupComponent

```
.THIS {}
.THIS .group {
	background-color: #d6d6d6;
}
```
### reportGroupComponent

```
<aura:component >
	<aura:attribute name="group" type="Object"/>
    
    <tr class="slds-line-height_reset" style="background-color: #d6d6d6;">
        <td class="slds-truncate" colspan="{!v.group.fieldsInGroup}">
            <b>{!v.group.fieldName}: </b>
            <aura:renderIf isTrue="{!v.group.isHyperLink}">
                <c:sobjectHyperlink sObjectId="{!v.group.fieldValue}" hyperlinkLabel="{!v.group.fieldLabel}"/>
                <aura:set attribute="else">{!v.group.fieldLabel}</aura:set>                        
            </aura:renderIf>            
        </td>
    </tr>
    
    <aura:iteration var="row" items="{!v.group.fieldDataList}">  
        <tr class="slds-hint-parent">
            <aura:iteration var="cell" items="{!row}">
                <td class="slds-truncate">
                    <aura:renderIf isTrue="{!!cell.isHyperLink}">
                        <c:sobjectHyperlink sObjectId="{!cell.fieldValue}" hyperlinkLabel="{!cell.fieldLabel}"/>
                        <aura:set attribute="else">{!cell.fieldLabel}</aura:set>                        
                    </aura:renderIf>                            
                </td>
            </aura:iteration>
        </tr>
    </aura:iteration>

        

</aura:component>
```
### reportGroupComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportGroupComponent

```
.THIS {}
.THIS .group {
	background-color: #d6d6d6;
}
```
### reportGroupComponent

```
<aura:component >
	<aura:attribute name="group" type="Object"/>
    
    <tr class="slds-line-height_reset" style="background-color: #d6d6d6;">
        <td class="slds-truncate" colspan="{!v.group.fieldsInGroup}">
            <b>{!v.group.fieldName}: </b>
            <aura:renderIf isTrue="{!v.group.isHyperLink}">
                <c:sobjectHyperlink sObjectId="{!v.group.fieldValue}" hyperlinkLabel="{!v.group.fieldLabel}"/>
                <aura:set attribute="else">{!v.group.fieldLabel}</aura:set>                        
            </aura:renderIf>            
        </td>
    </tr>
    
    <aura:iteration var="row" items="{!v.group.fieldDataList}">  
        <tr class="slds-hint-parent">
            <aura:iteration var="cell" items="{!row}">
                <td class="slds-truncate">
                    <aura:renderIf isTrue="{!!cell.isHyperLink}">
                        <c:sobjectHyperlink sObjectId="{!cell.fieldValue}" hyperlinkLabel="{!cell.fieldLabel}"/>
                        <aura:set attribute="else">{!cell.fieldLabel}</aura:set>                        
                    </aura:renderIf>                            
                </td>
            </aura:iteration>
        </tr>
    </aura:iteration>

        

</aura:component>
```

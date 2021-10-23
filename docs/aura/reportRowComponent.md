---
layout: default
title: reportRowComponent
parent: aura
---
# Metadata Type
CustomObject

# Name
reportRowComponent
## Fields
### reportRowComponent

```
<aura:component>
  <aura:attribute name="row" type="Object[]" />
  <aura:attribute name="isHeader" type="Boolean" />

  <tr class="slds-line-height_reset">
    <aura:iteration var="cell" items="{!v.row}">
      <aura:renderIf isTrue="{!v.isHeader}">
        <th class="" scope="row">
          <div class="slds-truncate">{!cell.fieldLabel}</div>
        </th>
        <aura:set attribute="else">
          <td class="slds-truncate">
            <div class="slds-truncate">{!cell.fieldLabel}</div>
          </td>
        </aura:set>
      </aura:renderIf>
    </aura:iteration>
  </tr>
</aura:component>
```
### reportRowComponent

```
.THIS{}
```
### reportRowComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportRowComponent

```
<aura:component>
  <aura:attribute name="row" type="Object[]" />
  <aura:attribute name="isHeader" type="Boolean" />

  <tr class="slds-line-height_reset">
    <aura:iteration var="cell" items="{!v.row}">
      <aura:renderIf isTrue="{!v.isHeader}">
        <th class="" scope="row">
          <div class="slds-truncate">{!cell.fieldLabel}</div>
        </th>
        <aura:set attribute="else">
          <td class="slds-truncate">
            <div class="slds-truncate">{!cell.fieldLabel}</div>
          </td>
        </aura:set>
      </aura:renderIf>
    </aura:iteration>
  </tr>
</aura:component>
```
### reportRowComponent

```
.THIS{}
```
### reportRowComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```

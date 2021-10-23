---
layout: default
title: Product2
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Product2
## Fields
### ExternalId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ExternalId</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### AVSFQB__QB_Error__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QB_Error__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>QB Error</label>
    <length>32000</length>
    <trackHistory>false</trackHistory>
    <type>LongTextArea</type>
    <visibleLines>10</visibleLines>
</CustomField>
```
### AVSFQB__OnHand__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__OnHand__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>OnHand</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### QuantityUnitOfMeasure

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>QuantityUnitOfMeasure</fullName>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
</CustomField>
```
### CurrencyIsoCode

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CurrencyIsoCode</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Description

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### AVSFQB__QuickBooks_ItemType__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QuickBooks_ItemType__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>QuickBooks Item Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>ItemService</fullName>
                <default>true</default>
                <label>ItemService</label>
            </value>
            <value>
                <fullName>ItemNonInventory</fullName>
                <default>false</default>
                <label>ItemNonInventory</label>
            </value>
            <value>
                <fullName>ItemOtherCharge</fullName>
                <default>false</default>
                <label>ItemOtherCharge</label>
            </value>
            <value>
                <fullName>ItemInventory</fullName>
                <default>false</default>
                <label>ItemInventory</label>
            </value>
            <value>
                <fullName>ItemInventoryAssembly</fullName>
                <default>false</default>
                <label>ItemInventoryAssembly</label>
            </value>
            <value>
                <fullName>ItemDiscount</fullName>
                <default>false</default>
                <label>ItemDiscount</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Name

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Name</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### ProductCode

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ProductCode</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### StockKeepingUnit

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>StockKeepingUnit</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Family

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Family</fullName>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
</CustomField>
```
### IsActive

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsActive</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### DisplayUrl

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>DisplayUrl</fullName>
    <trackHistory>false</trackHistory>
</CustomField>
```
### AVSFQB__Quickbooks_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Quickbooks_Id__c</fullName>
    <deprecated>false</deprecated>
    <externalId>true</externalId>
    <label>Quickbooks Id</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### ExternalDataSourceId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ExternalDataSourceId</fullName>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### AVSFQB__COGS__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__COGS__c</fullName>
    <deprecated>false</deprecated>
    <description>Cost of goods sold</description>
    <externalId>false</externalId>
    <label>COGS</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <type>Currency</type>
</CustomField>
```

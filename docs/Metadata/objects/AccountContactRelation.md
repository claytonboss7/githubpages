---
layout: default
title: AccountContactRelation
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
AccountContactRelation
## Fields
### IsDirect

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsDirect</fullName>
</CustomField>
```
### Relationship_Strength__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Relationship_Strength__c</fullName>
    <externalId>false</externalId>
    <label>Relationship Strength</label>
    <required>false</required>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Strong</fullName>
                <default>false</default>
                <label>Strong</label>
            </value>
            <value>
                <fullName>Neutral</fullName>
                <default>false</default>
                <label>Neutral</label>
            </value>
            <value>
                <fullName>Weak</fullName>
                <default>false</default>
                <label>Weak</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### ContactId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ContactId</fullName>
    <type>Lookup</type>
</CustomField>
```
### AccountId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AccountId</fullName>
    <type>Lookup</type>
</CustomField>
```
### Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Order__c</fullName>
    <externalId>false</externalId>
    <label>Order</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### IsActive

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsActive</fullName>
</CustomField>
```
### Association_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Association_Status__c</fullName>
    <externalId>false</externalId>
    <label>Association Status</label>
    <required>false</required>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Active</fullName>
                <default>false</default>
                <label>Active</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### EndDate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>EndDate</fullName>
</CustomField>
```
### Roles

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Roles</fullName>
    <type>Picklist</type>
</CustomField>
```
### StartDate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>StartDate</fullName>
</CustomField>
```

---
layout: default
title: Deployment__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Deployment__c
## Fields
### Package_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Package_Name__c</fullName>
    <externalId>false</externalId>
    <label>Package Name</label>
    <length>255</length>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status__c</fullName>
    <externalId>false</externalId>
    <label>Status</label>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>New</fullName>
                <default>false</default>
                <label>New</label>
            </value>
            <value>
                <fullName>Packaged</fullName>
                <default>false</default>
                <label>Packaged</label>
            </value>
            <value>
                <fullName>Ready to Deploy</fullName>
                <default>false</default>
                <label>Ready to Deploy</label>
            </value>
            <value>
                <fullName>Validated</fullName>
                <default>false</default>
                <label>Validated</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Environment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Environment__c</fullName>
    <externalId>false</externalId>
    <label>Environment</label>
    <length>255</length>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Details__c</fullName>
    <externalId>false</externalId>
    <label>Details</label>
    <length>131072</length>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Validated_Package_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Validated_Package_Id__c</fullName>
    <externalId>false</externalId>
    <label>Validated Package Id</label>
    <length>255</length>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

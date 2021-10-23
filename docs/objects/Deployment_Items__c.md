---
layout: default
title: Deployment_Items__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Deployment_Items__c
## Fields
### Git_Branch__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Git_Branch__c</fullName>
    <externalId>false</externalId>
    <label>Git Branch</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Git_Pull_Request__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Git_Pull_Request__c</fullName>
    <externalId>false</externalId>
    <label>Git Pull Request</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Deployment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deployment__c</fullName>
    <externalId>false</externalId>
    <label>Deployment</label>
    <referenceTo>Deployment__c</referenceTo>
    <relationshipLabel>Deployment Items</relationshipLabel>
    <relationshipName>Deployment_Items</relationshipName>
    <relationshipOrder>0</relationshipOrder>
    <reparentableMasterDetail>false</reparentableMasterDetail>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MasterDetail</type>
    <writeRequiresMasterRead>false</writeRequiresMasterRead>
</CustomField>
```
### Project_Item__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project_Item__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Project Item</label>
    <referenceTo>Project_Item__c</referenceTo>
    <relationshipLabel>Deployment Items</relationshipLabel>
    <relationshipName>Deployment_Items</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>New</fullName>
                <default>true</default>
                <label>New</label>
            </value>
            <value>
                <fullName>Validated</fullName>
                <default>false</default>
                <label>Validated</label>
            </value>
            <value>
                <fullName>Tests Passed</fullName>
                <default>false</default>
                <label>Tests Passed</label>
            </value>
            <value>
                <fullName>Ready for QA</fullName>
                <default>false</default>
                <label>Ready for QA</label>
            </value>
            <value>
                <fullName>Ready for Release</fullName>
                <default>false</default>
                <label>Ready for Release</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```

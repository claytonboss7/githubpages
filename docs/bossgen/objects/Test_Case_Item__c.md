---
layout: default
title: Test_Case_Item__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Test_Case_Item__c
## Fields
### Test_Case__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Case__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Test Case</label>
    <referenceTo>Test_Case__c</referenceTo>
    <relationshipLabel>Test Case Items</relationshipLabel>
    <relationshipName>Test_Case_Items</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Test_Suite__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Suite__c</fullName>
    <externalId>false</externalId>
    <label>Test Suite</label>
    <referenceTo>Test_Suite__c</referenceTo>
    <relationshipLabel>Test Case Items</relationshipLabel>
    <relationshipName>Test_Case_Items</relationshipName>
    <relationshipOrder>0</relationshipOrder>
    <reparentableMasterDetail>false</reparentableMasterDetail>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MasterDetail</type>
    <writeRequiresMasterRead>false</writeRequiresMasterRead>
</CustomField>
```

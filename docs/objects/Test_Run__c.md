---
layout: default
title: Test_Run__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Test_Run__c
## Fields
### Test_Plan__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Plan__c</fullName>
    <externalId>false</externalId>
    <label>Test Plan</label>
    <referenceTo>Test_Plan__c</referenceTo>
    <relationshipLabel>Test Runs</relationshipLabel>
    <relationshipName>Test_Runs</relationshipName>
    <relationshipOrder>0</relationshipOrder>
    <reparentableMasterDetail>false</reparentableMasterDetail>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MasterDetail</type>
    <writeRequiresMasterRead>false</writeRequiresMasterRead>
</CustomField>
```
### Test_Case__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Case__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Test Case</label>
    <referenceTo>Test_Case__c</referenceTo>
    <relationshipLabel>Test Runs</relationshipLabel>
    <relationshipName>Test_Runs</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Test_Run_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Run_Status__c</fullName>
    <externalId>false</externalId>
    <label>Test Run Status</label>
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
                <default>false</default>
                <label>New</label>
            </value>
            <value>
                <fullName>In Progress</fullName>
                <default>false</default>
                <label>In Progress</label>
            </value>
            <value>
                <fullName>Complete (Pass)</fullName>
                <default>false</default>
                <label>Complete (Pass)</label>
            </value>
            <value>
                <fullName>Review (Fail)</fullName>
                <default>false</default>
                <label>Review (Fail)</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Test_Suite__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Suite__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Test Suite</label>
    <referenceTo>Test_Suite__c</referenceTo>
    <relationshipLabel>Test Run (Suite)</relationshipLabel>
    <relationshipName>Test_Runs</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

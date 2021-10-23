---
layout: default
title: Test_Plan__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Test_Plan__c
## Fields
### Test_Plan_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Plan_Status__c</fullName>
    <defaultValue>&quot;New&quot;</defaultValue>
    <externalId>false</externalId>
    <label>Test Plan Status</label>
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
                <fullName>Test Creation</fullName>
                <default>false</default>
                <label>Test Creation</label>
            </value>
            <value>
                <fullName>Test Execution</fullName>
                <default>false</default>
                <label>Test Execution</label>
            </value>
            <value>
                <fullName>Complete</fullName>
                <default>false</default>
                <label>Complete</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Number_of_Test_Runs__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Number_of_Test_Runs__c</fullName>
    <externalId>false</externalId>
    <label>Number of Test Runs</label>
    <summaryForeignKey>Test_Run__c.Test_Plan__c</summaryForeignKey>
    <summaryOperation>count</summaryOperation>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Summary</type>
</CustomField>
```

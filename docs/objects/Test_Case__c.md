---
layout: default
title: Test_Case__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Test_Case__c
## Fields
### Test_Plan__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Plan__c</fullName>
    <description>Master Detail to the Test Plan object to support Test Case and Test management.</description>
    <externalId>false</externalId>
    <inlineHelpText>Help me.</inlineHelpText>
    <label>Test Plan</label>
    <referenceTo>Test_Plan__c</referenceTo>
    <relationshipLabel>Test Cases</relationshipLabel>
    <relationshipName>Test_Cases</relationshipName>
    <relationshipOrder>0</relationshipOrder>
    <reparentableMasterDetail>false</reparentableMasterDetail>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MasterDetail</type>
    <writeRequiresMasterRead>true</writeRequiresMasterRead>
</CustomField>
```
### Test_Case_Title__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Case_Title__c</fullName>
    <description>Description for the specific case being tested</description>
    <externalId>false</externalId>
    <inlineHelpText>Help me again</inlineHelpText>
    <label>Test Case Title</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipLabel>Test Cases</relationshipLabel>
    <relationshipName>Test_Cases</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Test_Case_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Case_Details__c</fullName>
    <description>A Rich text area for us to type in details about the Test Case.</description>
    <externalId>false</externalId>
    <inlineHelpText>Help me 3</inlineHelpText>
    <label>Test Case Details</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Test_Steps__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Steps__c</fullName>
    <externalId>false</externalId>
    <label>Test Steps</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Expected_Outcome__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Expected_Outcome__c</fullName>
    <externalId>false</externalId>
    <label>Expected Outcome</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```

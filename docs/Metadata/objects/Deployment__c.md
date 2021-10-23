---
layout: default
title: Deployment__c
parent: objects
grand_parent: Metadata
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### DiffJSON__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>DiffJSON__c</fullName>
    <externalId>false</externalId>
    <label>DiffJSON</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Deployment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deployment__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Deployment</label>
    <referenceTo>Deployment__c</referenceTo>
    <relationshipLabel>Deployments</relationshipLabel>
    <relationshipName>Deployments</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Deployment_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deployment_Id__c</fullName>
    <externalId>false</externalId>
    <label>Deployment Id</label>
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
    <relationshipLabel>Deployments</relationshipLabel>
    <relationshipName>Deployments</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Build_Source_Branch__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Build_Source_Branch__c</fullName>
    <externalId>false</externalId>
    <label>Build Source Branch</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
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
                <fullName>Validation Failed</fullName>
                <default>false</default>
                <label>Validation Failed</label>
            </value>
            <value>
                <fullName>Tests Passed</fullName>
                <default>false</default>
                <label>Tests Passed</label>
            </value>
            <value>
                <fullName>Tests Failed</fullName>
                <default>false</default>
                <label>Tests Failed</label>
            </value>
            <value>
                <fullName>Coverage Issue</fullName>
                <default>false</default>
                <label>Coverage Issue</label>
            </value>
            <value>
                <fullName>Needs Review</fullName>
                <default>false</default>
                <label>Needs Review</label>
            </value>
            <value>
                <fullName>Ready for Release</fullName>
                <default>false</default>
                <label>Ready for Release</label>
            </value>
            <value>
                <fullName>Deployed</fullName>
                <default>false</default>
                <label>Deployed</label>
            </value>
            <value>
                <fullName>Packaged</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Packaged</label>
            </value>
            <value>
                <fullName>Ready to Deploy</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Ready to Deploy</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Deployment_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deployment_Status__c</fullName>
    <externalId>false</externalId>
    <label>Deployment Status</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Source__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Source__c</fullName>
    <externalId>false</externalId>
    <label>Source</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Validated_Package__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Validated_Package__c</fullName>
    <externalId>false</externalId>
    <label>Validated Package</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Last_Diffs_Email_Summary_Sent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Last_Diffs_Email_Summary_Sent__c</fullName>
    <externalId>false</externalId>
    <label>Last Diffs Email Summary Sent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Async_Job_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Async_Job_Id__c</fullName>
    <externalId>false</externalId>
    <label>Async Job Id</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tag__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tag__c</fullName>
    <externalId>false</externalId>
    <label>Tag</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Commit__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commit__c</fullName>
    <externalId>false</externalId>
    <label>Commit</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Deployment_Category__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deployment_Category__c</fullName>
    <externalId>false</externalId>
    <label>Deployment Category</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
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
    <trackHistory>false</trackHistory>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

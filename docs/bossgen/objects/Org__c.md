---
layout: default
title: Org__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Org__c
## Fields
### Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alias__c</fullName>
    <externalId>false</externalId>
    <label>Alias</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### SFDX_Auth_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>SFDX_Auth_URL__c</fullName>
    <externalId>false</externalId>
    <label>SFDX Auth URL</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Post_to_Slack__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Post_to_Slack__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Post to Slack</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Login_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Login_URL__c</fullName>
    <externalId>false</externalId>
    <formula>Instance_URL__c + &apos;/secur/frontdoor.jsp?sid=&apos;+Access_Token__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Login URL</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Project__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Project</label>
    <referenceTo>Project__c</referenceTo>
    <relationshipLabel>Orgs</relationshipLabel>
    <relationshipName>Orgs</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Connected_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Connected_Status__c</fullName>
    <externalId>false</externalId>
    <label>Connected Status</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Sandbox_Details_JSON__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sandbox_Details_JSON__c</fullName>
    <externalId>false</externalId>
    <label>Sandbox Details JSON</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Client_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Id__c</fullName>
    <externalId>false</externalId>
    <label>Client Id</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Password__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Password__c</fullName>
    <externalId>false</externalId>
    <label>Password</label>
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
                <fullName>Pending</fullName>
                <default>false</default>
                <label>Pending</label>
            </value>
            <value>
                <fullName>Complete</fullName>
                <default>false</default>
                <label>Complete</label>
            </value>
            <value>
                <fullName>Error</fullName>
                <default>false</default>
                <label>Error</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Username__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Username__c</fullName>
    <externalId>false</externalId>
    <label>Username</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Instance_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Instance_URL__c</fullName>
    <externalId>false</externalId>
    <label>Instance URL</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Branch__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Branch__c</fullName>
    <externalId>false</externalId>
    <label>Branch</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### My_Domain_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>My_Domain_URL__c</fullName>
    <externalId>false</externalId>
    <label>My Domain URL</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Org_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Org_Type__c</fullName>
    <externalId>false</externalId>
    <label>Org Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Developer</fullName>
                <default>false</default>
                <label>Developer</label>
            </value>
            <value>
                <fullName>Sandbox</fullName>
                <default>false</default>
                <label>Sandbox</label>
            </value>
            <value>
                <fullName>Prod</fullName>
                <default>false</default>
                <label>Prod</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Access_Token__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Access_Token__c</fullName>
    <externalId>false</externalId>
    <label>Access Token</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

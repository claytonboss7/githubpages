---
layout: default
title: SF_DevOps__mdt
parent: objects
---
# Metadata Type
CustomObject

# Name
SF_DevOps__mdt
## Fields
### Git_Repository_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Git_Repository_URL__c</fullName>
    <description>Will be populated via Setup unless a different URL is specified.</description>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>Git Repository URL</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Devhub_Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Devhub_Alias__c</fullName>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>Devhub Alias</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### UnitTests_Org_Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>UnitTests_Org_Alias__c</fullName>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>UnitTests Org Alias</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Automate_Backups__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Automate_Backups__c</fullName>
    <defaultValue>false</defaultValue>
    <description>Will tell the Nightly Task Scheduler to run a backup on the orgs listed.</description>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>Automate Backups</label>
    <type>Checkbox</type>
</CustomField>
```
### Refresh_UnitTests_Nightly__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Refresh_UnitTests_Nightly__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>Refresh UnitTests Nightly</label>
    <type>Checkbox</type>
</CustomField>
```
### Last_Data_Backup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Last_Data_Backup__c</fullName>
    <description>Will set the LastModifiedDate filter for the backups meaning you get records where the SYSTEM LASTMODIFIEDDATE TIMESTAMPS changed (not indirect formula calculation changes)</description>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>Last Data Backup</label>
    <required>false</required>
    <type>DateTime</type>
</CustomField>
```
### QA_Org_Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>QA_Org_Alias__c</fullName>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>QA Org Alias</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### PT_Project_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PT_Project_Id__c</fullName>
    <description>The Pivotal Tracker Id for the Project for Salesforce Development.</description>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>PT Project Id</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Last_Successful_Backup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Last_Successful_Backup__c</fullName>
    <externalId>false</externalId>
    <fieldManageability>DeveloperControlled</fieldManageability>
    <label>Last Successful Backup</label>
    <required>false</required>
    <type>DateTime</type>
</CustomField>
```

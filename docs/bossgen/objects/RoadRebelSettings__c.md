---
layout: default
title: RoadRebelSettings__c
parent: objects
---
# Metadata Type
CustomObject

# Name
RoadRebelSettings__c
## Fields
### Community_Base_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Community_Base_URL__c</fullName>
    <externalId>false</externalId>
    <label>Community Base URL</label>
    <length>255</length>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Forwarding_Email_Addresses__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Forwarding_Email_Addresses__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Comma separated list of email addresses where Conga sign email service forwarding status will be sent</inlineHelpText>
    <label>Forwarding Email Addresses</label>
    <length>255</length>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Send_Person_Account_Email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Send_Person_Account_Email__c</fullName>
    <defaultValue>false</defaultValue>
    <description>Controls whether or not the Person Account Conversion tool will email after the batch job completes.  The email sends after all the batches executed and the finish method runs.</description>
    <externalId>false</externalId>
    <label>Send Person Account Email</label>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```

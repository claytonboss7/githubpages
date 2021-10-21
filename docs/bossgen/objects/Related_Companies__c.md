---
layout: default
title: Related_Companies__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Related_Companies__c
## Fields
### Journal__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Journal__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Journal</label>
    <referenceTo>Journal__c</referenceTo>
    <relationshipLabel>Companies</relationshipLabel>
    <relationshipName>Related_Companies</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Company__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Company__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Company</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Journal</relationshipLabel>
    <relationshipName>Related_Companies</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

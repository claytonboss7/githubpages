---
layout: default
title: Related_Contact__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Related_Contact__c
## Fields
### Journal_Entry__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Journal_Entry__c</fullName>
    <externalId>false</externalId>
    <label>Journal Entry</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Journal__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Journal__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Journal</label>
    <referenceTo>Journal__c</referenceTo>
    <relationshipLabel>Contacts</relationshipLabel>
    <relationshipName>Related_Contact</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contact__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contact</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Journal</relationshipLabel>
    <relationshipName>Related_Contact</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Type__c</fullName>
    <externalId>false</externalId>
    <label>Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Production Contacts</fullName>
                <default>false</default>
                <label>Production Contacts</label>
            </value>
            <value>
                <fullName>Company Contacts</fullName>
                <default>false</default>
                <label>Company Contacts</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```

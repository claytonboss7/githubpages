---
layout: default
title: Segment_GCQ__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Segment_GCQ__c
## Fields
### GCQ_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCQ_Details__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>GCQ Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Air__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GCQ Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Segments</relationshipLabel>
    <relationshipName>Segments</relationshipName>
    <required>true</required>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Air_Segments__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Segments__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Air Segments</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Air__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Air Segments</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>GCQs</relationshipLabel>
    <relationshipName>GCQs</relationshipName>
    <required>true</required>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

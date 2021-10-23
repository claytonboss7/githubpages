---
layout: default
title: Sub_Trip_GCQ__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Sub_Trip_GCQ__c
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
            <field>Ground__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GCQ Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Sub Trips</relationshipLabel>
    <relationshipName>SubTrips</relationshipName>
    <required>true</required>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### GT_Sub_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Sub_Trip_Details__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>GT Sub Trip Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Ground__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GT Sub Trip Details</value>
        </filterItems>
        <filterItems>
            <field>Ground__c.Bid_Sub_Trip__c</field>
            <operation>notEqual</operation>
            <value/>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>GCQs</relationshipLabel>
    <relationshipName>GCQs</relationshipName>
    <required>true</required>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

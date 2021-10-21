---
layout: default
title: Sub_Trip_FCQ__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Sub_Trip_FCQ__c
## Fields
### FCQ_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>FCQ_Details__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>FCQ Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Freight__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>FCQ Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Sub Trips</relationshipLabel>
    <relationshipName>SubTrips</relationshipName>
    <required>true</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Freight_Sub_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Sub_Trip_Details__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Freight Sub Trip Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Freight__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Sub Trip Details</value>
        </filterItems>
        <filterItems>
            <field>Freight__c.Bid_Sub_Trip__c</field>
            <operation>notEqual</operation>
            <value/>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>FCQs</relationshipLabel>
    <relationshipName>FCQs</relationshipName>
    <required>true</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

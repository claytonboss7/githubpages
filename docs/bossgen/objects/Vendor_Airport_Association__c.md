---
layout: default
title: Vendor_Airport_Association__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Vendor_Airport_Association__c
## Fields
### Distance__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Distance__c</fullName>
    <externalId>false</externalId>
    <label>Distance</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Vendor_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Vendor NAV</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Airport_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airport_City__c</fullName>
    <externalId>false</externalId>
    <formula>Airport__r.City__r.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Airport City</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Transportation_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Type__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>By Vehicle</fullName>
                <default>false</default>
                <label>By Vehicle</label>
            </value>
            <value>
                <fullName>By Walk</fullName>
                <default>false</default>
                <label>By Walk</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Airport__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airport__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Airport</label>
    <referenceTo>Airport__c</referenceTo>
    <relationshipLabel>Vendor Association</relationshipLabel>
    <relationshipName>Vendor_Airport_Association</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Distance_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Distance_Type__c</fullName>
    <externalId>false</externalId>
    <label>Distance Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Across Street</fullName>
                <default>false</default>
                <label>Across Street</label>
            </value>
            <value>
                <fullName>Adjacent</fullName>
                <default>false</default>
                <label>Adjacent</label>
            </value>
            <value>
                <fullName>Block(s)</fullName>
                <default>false</default>
                <label>Block(s)</label>
            </value>
            <value>
                <fullName>Connected</fullName>
                <default>false</default>
                <label>Connected</label>
            </value>
            <value>
                <fullName>Km(s)</fullName>
                <default>false</default>
                <label>Km(s)</label>
            </value>
            <value>
                <fullName>Mile(s)</fullName>
                <default>false</default>
                <label>Mile(s)</label>
            </value>
            <value>
                <fullName>On-Site</fullName>
                <default>false</default>
                <label>On-Site</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Vendor__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Vendor</label>
    <lookupFilter>
        <active>true</active>
        <booleanFilter>1 OR 2 OR 3 OR 4 OR 5 OR 6</booleanFilter>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Airline Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Corporate Housing Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Ground Travel Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Hotel Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Hotel Vendor Chain</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Airport Association</relationshipLabel>
    <relationshipName>Vendor_Airport_Association</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

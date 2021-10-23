---
layout: default
title: Vendor_Venue__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Vendor_Venue__c
## Fields
### Venue_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Venue_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Venue NAV</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
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
### Vendor_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Type__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Vendor__r.Vendor_Type__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
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
### Venue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Venue__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Venue</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Venue</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Vendor - Venue</relationshipLabel>
    <relationshipName>Vendor_Venue</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Recalc_Venue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Recalc_Venue__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Recalc Venue</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
### Venue_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Venue_City__c</fullName>
    <externalId>false</externalId>
    <formula>Venue__r.City__r.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Venue City</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Distance_formula__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Distance_formula__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(ROUND(Distance__c,2)) &amp; &quot; &quot; &amp;  TEXT(Distance_Type__c) &amp; &quot; &quot; &amp;  TEXT(Transportation_Type__c)</formula>
    <label>Distance (formula)</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### Vendor_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Address__c</fullName>
    <externalId>false</externalId>
    <formula>If(ISBLANK(Vendor__r.ShippingStreet),&quot;&quot;,Vendor__r.ShippingStreet &amp; BR()) &amp; 
Vendor__r.ShippingCity &amp; &quot;, &quot; &amp; Vendor__r.ShippingState &amp; &quot; &quot; &amp; Vendor__r.ShippingPostalCode &amp; BR() &amp; 
Vendor__r.ShippingCountry</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Address</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
        <booleanFilter>1 OR 2 OR 3 OR 4 OR 5</booleanFilter>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Hotel Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Hotel Vendor Chain</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Corporate Housing Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Ground Travel Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Freight Vendor</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Venues</relationshipLabel>
    <relationshipName>Vendor_Venue1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

---
layout: default
title: Hotels__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Hotels__c
## Fields
### Rebate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate__c</fullName>
    <externalId>false</externalId>
    <label>Rebate</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Total_Rebate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Rebate__c</fullName>
    <externalId>false</externalId>
    <formula>Rebate__c  *  Room_Nights__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Total Rebate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Room_Nights__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Nights__c</fullName>
    <externalId>false</externalId>
    <label>Room Nights</label>
    <precision>3</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Comments__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Comments__c</fullName>
    <externalId>false</externalId>
    <label>Comments</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Secondary_Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Secondary_Contact__c</fullName>
    <externalId>false</externalId>
    <label>Secondary Contact</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Email</type>
    <unique>false</unique>
</CustomField>
```
### Primary_Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Contact__c</fullName>
    <externalId>false</externalId>
    <label>Primary Contact</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Email</type>
    <unique>false</unique>
</CustomField>
```
### Tournament__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tournament__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Tournament</label>
    <referenceTo>Tournament__c</referenceTo>
    <relationshipLabel>Hotels</relationshipLabel>
    <relationshipName>Hotels</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

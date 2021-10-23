---
layout: default
title: Itinerary__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Itinerary__c
## Fields
### Community_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Community_Notes__c</fullName>
    <description>Used to pass notes from the Coordinator to the Community User</description>
    <externalId>false</externalId>
    <label>Community Notes</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Start_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Start_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Start_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Start_Date__c),
  1, &quot;Jan&quot;,  
  2, &quot;Feb&quot;,
  3, &quot;Mar&quot;,
  4, &quot;Apr&quot;,
  5, &quot;May&quot;,
  6, &quot;Jun&quot;,
  7, &quot;Jul&quot;,
  8, &quot;Aug&quot;,
  9, &quot;Sep&quot;,
  10, &quot;Oct&quot;,
  11, &quot;Nov&quot;,
  &quot;Dec&quot;
) + &quot;-&quot; + TEXT(YEAR(Start_Date__c)), CASE(
  MONTH(Start_Date__c),
  1, &quot;Jan&quot;,  
  2, &quot;Feb&quot;,
  3, &quot;Mar&quot;,
  4, &quot;Apr&quot;,
  5, &quot;May&quot;,
  6, &quot;Jun&quot;,
  7, &quot;Jul&quot;,
  8, &quot;Aug&quot;,
  9, &quot;Sep&quot;,
  10, &quot;Oct&quot;,
  11, &quot;Nov&quot;,
  &quot;Dec&quot;
) + &quot;-&quot; + TEXT(DAY(Start_Date__c)) + &quot;-&quot; + TEXT(YEAR(Start_Date__c))), &quot;&quot;)</formula>
    <label>Start Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### ServiceId__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ServiceId__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(RecordType.DeveloperName,
  &quot;Housing_Itinerary&quot;, Housing__c,
  &quot;GT_Itinerary&quot;, GT__c,
  &quot;Air_Itinerary&quot;, Air__c,
  &quot;Freight_Itinerary&quot;, Freight__c ,
  &quot;None&quot;
)</formula>
    <label>ServiceId</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### End_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(End_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(End_Date__c)) + &quot;-&quot; + CASE(
  MONTH(End_Date__c),
  1, &quot;Jan&quot;,  
  2, &quot;Feb&quot;,
  3, &quot;Mar&quot;,
  4, &quot;Apr&quot;,
  5, &quot;May&quot;,
  6, &quot;Jun&quot;,
  7, &quot;Jul&quot;,
  8, &quot;Aug&quot;,
  9, &quot;Sep&quot;,
  10, &quot;Oct&quot;,
  11, &quot;Nov&quot;,
  &quot;Dec&quot;
) + &quot;-&quot; + TEXT(YEAR(End_Date__c)), CASE(
  MONTH(End_Date__c),
  1, &quot;Jan&quot;,  
  2, &quot;Feb&quot;,
  3, &quot;Mar&quot;,
  4, &quot;Apr&quot;,
  5, &quot;May&quot;,
  6, &quot;Jun&quot;,
  7, &quot;Jul&quot;,
  8, &quot;Aug&quot;,
  9, &quot;Sep&quot;,
  10, &quot;Oct&quot;,
  11, &quot;Nov&quot;,
  &quot;Dec&quot;
) + &quot;-&quot; + TEXT(DAY(End_Date__c)) + &quot;-&quot; + TEXT(YEAR(End_Date__c))), &quot;&quot;)</formula>
    <label>End Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Show_Community_Message__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Show_Community_Message__c</fullName>
    <defaultValue>true</defaultValue>
    <description>Will be used to make sure we don&apos;t pop up the message every time.</description>
    <externalId>false</externalId>
    <label>Show Community Message</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Air__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Air</label>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Itinerary</relationshipLabel>
    <relationshipName>Itinerary</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### ServiceStatus__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ServiceStatus__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(RecordType.DeveloperName,
  &quot;Housing_Itinerary&quot;,TEXT(Housing__r.Status_CC__c),
  &quot;GT_Itinerary&quot;,TEXT(GT__r.Status_Ground__c),
  &quot;Air_Itinerary&quot;,TEXT(Air__r.Status__c),
  &quot;Freight_Itinerary&quot;,TEXT(Freight__r.Status__c),
  &quot;None&quot;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>ServiceStatus</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### isEditable__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isEditable__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Is editable on community?</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### End_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_Date__c</fullName>
    <externalId>false</externalId>
    <label>End Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status__c</fullName>
    <externalId>false</externalId>
    <label>Status</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Bid_Status</valueSetName>
    </valueSet>
</CustomField>
```
### City_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_NAV__c</fullName>
    <externalId>false</externalId>
    <label>City NAV</label>
    <length>20</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>City</label>
    <referenceTo>City__c</referenceTo>
    <relationshipLabel>Itinerary</relationshipLabel>
    <relationshipName>Itinerary</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Service__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(RecordType.DeveloperName,
  &quot;Housing_Itinerary&quot;,&quot;lodging&quot;,
  &quot;GT_Itinerary&quot;,&quot;ground&quot;,
  &quot;Air_Itinerary&quot;,&quot;air&quot;,
  &quot;Freight_Itinerary&quot;,&quot;freight&quot;,
  &quot;None&quot;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Service</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Contract_Resent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Contract_Resent__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Contract_Resent__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing Contract Resent</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Service_Backend_Coordinator_Email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Backend_Coordinator_Email__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(RecordType.DeveloperName,
  &quot;Housing_Itinerary&quot;,Housing__r.Back_end_Coordinator__r.Email,
  &quot;GT_Itinerary&quot;,GT__r.Back_end_Coordinator__r.Email,
  &quot;Air_Itinerary&quot;,Air__r.Back_end_Coordinator__r.Email,
  &quot;Freight_Itinerary&quot;,Freight__r.Back_end_Coordinator__r.Email,
  &quot;&quot;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Service Backend Coordinator Email</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production__c</fullName>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Itinerary</relationshipLabel>
    <relationshipName>Itinerary</relationshipName>
    <relationshipOrder>0</relationshipOrder>
    <reparentableMasterDetail>true</reparentableMasterDetail>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MasterDetail</type>
    <writeRequiresMasterRead>false</writeRequiresMasterRead>
</CustomField>
```
### Freight__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Freight</label>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Itinerary</relationshipLabel>
    <relationshipName>Itinerary</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_Date__c</fullName>
    <externalId>false</externalId>
    <label>Start Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Order__c</fullName>
    <externalId>false</externalId>
    <label>Order #</label>
    <precision>3</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Housing__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Housing</label>
    <lookupFilter>
        <active>true</active>
        <booleanFilter>1 OR 2 OR 3 OR 4</booleanFilter>
        <filterItems>
            <field>Housing__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Hotel Housing</value>
        </filterItems>
        <filterItems>
            <field>Housing__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Corporate Housing</value>
        </filterItems>
        <filterItems>
            <field>Housing__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Individual Reservation</value>
        </filterItems>
        <filterItems>
            <field>Housing__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Tournament</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Itinerary</relationshipLabel>
    <relationshipName>Itinerary</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Service_Backend_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Backend_Coordinator__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(RecordType.DeveloperName,
  &quot;Housing_Itinerary&quot;,Housing__r.Back_end_Coordinator__c,
  &quot;GT_Itinerary&quot;,GT__r.Back_end_Coordinator__c,
  &quot;Air_Itinerary&quot;,Air__r.Back_end_Coordinator__c,
  &quot;Freight_Itinerary&quot;,Freight__r.Back_end_Coordinator__c,
  &quot;&quot;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Service Backend Coordinator</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### GT__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GT</label>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Itinerary</relationshipLabel>
    <relationshipName>Itinerary</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Client_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Client Notes</label>
    <length>1000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```

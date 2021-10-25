---
layout: default
title: Historical_Production__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Historical_Production__c
## Fields
### Housing_Estimate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Estimate__c</fullName>
    <externalId>false</externalId>
    <label>Housing Estimate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Ground_Actual__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ground_Actual__c</fullName>
    <externalId>false</externalId>
    <label>Ground Actual</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Ground_Estimate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ground_Estimate__c</fullName>
    <externalId>false</externalId>
    <label>Ground Estimate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Air_Actual__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Actual__c</fullName>
    <externalId>false</externalId>
    <label>Air Actual</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
### Freight_Actual__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Actual__c</fullName>
    <externalId>false</externalId>
    <label>Freight Actual</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Stage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Stage__c</fullName>
    <externalId>false</externalId>
    <label>Stage</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Bidding</fullName>
                <default>false</default>
                <label>Bidding</label>
            </value>
            <value>
                <fullName>Itinerary</fullName>
                <default>false</default>
                <label>Itinerary</label>
            </value>
            <value>
                <fullName>In Process</fullName>
                <default>false</default>
                <label>In Process</label>
            </value>
            <value>
                <fullName>Approval</fullName>
                <default>false</default>
                <label>Approval</label>
            </value>
            <value>
                <fullName>Contract</fullName>
                <default>false</default>
                <label>Contract</label>
            </value>
            <value>
                <fullName>Completed</fullName>
                <default>false</default>
                <label>Completed</label>
            </value>
            <value>
                <fullName>Lost</fullName>
                <default>false</default>
                <label>Lost</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Total_Estimate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Estimate__c</fullName>
    <externalId>false</externalId>
    <formula>Air_Estimate__c +  Ground_Estimate__c +  Housing_Estimate__c +  Freight_Estimate__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Total Estimate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Freight_Estimate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Estimate__c</fullName>
    <externalId>false</externalId>
    <label>Freight Estimate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
### Housing_Actual__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Actual__c</fullName>
    <externalId>false</externalId>
    <label>Housing Actual</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Cities__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cities__c</fullName>
    <externalId>false</externalId>
    <label>Cities</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Group_Size__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Group_Size__c</fullName>
    <externalId>false</externalId>
    <label>Group Size</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Air_Estimate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Estimate__c</fullName>
    <externalId>false</externalId>
    <label>Air Estimate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Total_Revenue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Revenue__c</fullName>
    <externalId>false</externalId>
    <formula>Air_Actual__c +  Freight_Actual__c +  Ground_Actual__c +  Housing_Actual__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Total Revenue</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Account__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Account__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Account</label>
    <referenceTo>Account</referenceTo>
    <relationshipName>Productions</relationshipName>
    <required>true</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

---
layout: default
title: Production__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Production__c
## Fields
### Confidence__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confidence__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>% of confidence we have in getting the show</inlineHelpText>
    <label>Confidence</label>
    <precision>2</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
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
### Secondary_Account__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Secondary_Account__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Secondary Account</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Productions (Secondary Account)</relationshipLabel>
    <relationshipName>Secondary_Productions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### LP_Title__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Title__c</fullName>
    <externalId>false</externalId>
    <label>LP Title</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>General Manager</fullName>
                <default>false</default>
                <label>General Manager</label>
            </value>
            <value>
                <fullName>Company Manager</fullName>
                <default>false</default>
                <label>Company Manager</label>
            </value>
            <value>
                <fullName>Touring Company Manager</fullName>
                <default>false</default>
                <label>Touring Company Manager</label>
            </value>
            <value>
                <fullName>Producer</fullName>
                <default>false</default>
                <label>Producer</label>
            </value>
            <value>
                <fullName>Partner</fullName>
                <default>false</default>
                <label>Partner</label>
            </value>
            <value>
                <fullName>Assistant General Manager</fullName>
                <default>false</default>
                <label>Assistant General Manager</label>
            </value>
            <value>
                <fullName>Assistant Company Manager</fullName>
                <default>false</default>
                <label>Assistant Company Manager</label>
            </value>
            <value>
                <fullName>Touring Assistant Company Manager</fullName>
                <default>false</default>
                <label>Touring Assistant Company Manager</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
### Live_Performance__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Live_Performance__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Live Performance</label>
    <referenceTo>Live_Performance__c</referenceTo>
    <relationshipLabel>Productions</relationshipLabel>
    <relationshipName>Productions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### LP_Services__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Services__c</fullName>
    <externalId>false</externalId>
    <label>LP Services</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Freight</fullName>
                <default>false</default>
                <label>Freight</label>
            </value>
            <value>
                <fullName>Housing</fullName>
                <default>false</default>
                <label>Housing</label>
            </value>
            <value>
                <fullName>Air</fullName>
                <default>false</default>
                <label>Air</label>
            </value>
            <value>
                <fullName>Ground</fullName>
                <default>false</default>
                <label>Ground</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
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
### LP_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Status__c</fullName>
    <externalId>false</externalId>
    <label>LP Status</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Have</fullName>
                <default>false</default>
                <label>Have</label>
            </value>
            <value>
                <fullName>Want</fullName>
                <default>false</default>
                <label>Want</label>
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
### Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contact__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contact</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Productions</relationshipLabel>
    <relationshipName>Productions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### LP_Touring_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Touring_Status__c</fullName>
    <externalId>false</externalId>
    <label>LP Touring Status</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Not Touring</fullName>
                <default>false</default>
                <label>Not Touring</label>
            </value>
            <value>
                <fullName>Touring</fullName>
                <default>false</default>
                <label>Touring</label>
            </value>
            <value>
                <fullName>Will Tour</fullName>
                <default>false</default>
                <label>Will Tour</label>
            </value>
            <value>
                <fullName>Out of Town</fullName>
                <default>false</default>
                <label>Out of Town</label>
            </value>
            <value>
                <fullName>On Broadway</fullName>
                <default>false</default>
                <label>On Broadway</label>
            </value>
            <value>
                <fullName>Off Broadway</fullName>
                <default>false</default>
                <label>Off Broadway</label>
            </value>
            <value>
                <fullName>Do Not Want</fullName>
                <default>false</default>
                <label>Do Not Want</label>
            </value>
            <value>
                <fullName>In Development</fullName>
                <default>false</default>
                <label>In Development</label>
            </value>
            <value>
                <fullName>Potentially Touring</fullName>
                <default>false</default>
                <label>Potentially Touring</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### LP_Primary__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Primary__c</fullName>
    <externalId>false</externalId>
    <label>LP Primary</label>
    <length>30</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### LP_Lost_To__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Lost_To__c</fullName>
    <externalId>false</externalId>
    <label>LP Lost To</label>
    <length>30</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Notes__c</fullName>
    <externalId>false</externalId>
    <label>Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
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
### LP_Itinerary__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Itinerary__c</fullName>
    <externalId>false</externalId>
    <formula>Start_Date__c - 180</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>LP Itinerary</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <relationshipLabel>Productions</relationshipLabel>
    <relationshipName>CustomProductions</relationshipName>
    <required>true</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

---
layout: default
title: Freight__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Freight__c
## Fields
### Loading_charges__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loading_charges__c</fullName>
    <externalId>false</externalId>
    <label>Loading charges</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Sales_Freight_details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sales_Freight_details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Sales Freight details</label>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Freight</relationshipLabel>
    <relationshipName>Freight</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Unloading_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Unloading_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Unloading Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Duties__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Duties__c</fullName>
    <externalId>false</externalId>
    <label>Duties</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Vehicle_registration__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vehicle_registration__c</fullName>
    <externalId>false</externalId>
    <label>Vehicle registration</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Loading_Unloading__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loading_Unloading__c</fullName>
    <externalId>false</externalId>
    <label>Loading Unloading</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Estimated_Volume__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Estimated_Volume__c</fullName>
    <externalId>false</externalId>
    <label>Estimated Volume</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Driving_permits_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driving_permits_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Driving permits Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Payment_Information__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Payment_Information__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Payment Information</label>
    <referenceTo>Credit_Card__c</referenceTo>
    <relationshipLabel>Freight</relationshipLabel>
    <relationshipName>Freight</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Vehicle_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vehicle_Type__c</fullName>
    <externalId>false</externalId>
    <label>Vehicle Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Hockey Sleeper</fullName>
                <default>false</default>
                <label>Hockey Sleeper</label>
            </value>
            <value>
                <fullName>Sleeper</fullName>
                <default>false</default>
                <label>Sleeper</label>
            </value>
            <value>
                <fullName>Coach</fullName>
                <default>false</default>
                <label>Coach</label>
            </value>
            <value>
                <fullName>Mini Coach</fullName>
                <default>false</default>
                <label>Mini Coach</label>
            </value>
            <value>
                <fullName>Executive Coach</fullName>
                <default>false</default>
                <label>Executive Coach</label>
            </value>
            <value>
                <fullName>Sedan</fullName>
                <default>false</default>
                <label>Sedan</label>
            </value>
            <value>
                <fullName>Executive Sedan</fullName>
                <default>false</default>
                <label>Executive Sedan</label>
            </value>
            <value>
                <fullName>Luxury Sedan</fullName>
                <default>false</default>
                <label>Luxury Sedan</label>
            </value>
            <value>
                <fullName>12 PAX Van</fullName>
                <default>false</default>
                <label>12 PAX Van</label>
            </value>
            <value>
                <fullName>15 PAX Van</fullName>
                <default>false</default>
                <label>15 PAX Van</label>
            </value>
            <value>
                <fullName>Luggage Van</fullName>
                <default>false</default>
                <label>Luggage Van</label>
            </value>
            <value>
                <fullName>SUV</fullName>
                <default>false</default>
                <label>SUV</label>
            </value>
            <value>
                <fullName>Limo</fullName>
                <default>false</default>
                <label>Limo</label>
            </value>
            <value>
                <fullName>Compact</fullName>
                <default>false</default>
                <label>Compact</label>
            </value>
            <value>
                <fullName>Intermediate</fullName>
                <default>false</default>
                <label>Intermediate</label>
            </value>
            <value>
                <fullName>Standard</fullName>
                <default>false</default>
                <label>Standard</label>
            </value>
            <value>
                <fullName>Full Size</fullName>
                <default>false</default>
                <label>Full Size</label>
            </value>
            <value>
                <fullName>Standard SUV</fullName>
                <default>false</default>
                <label>Standard SUV</label>
            </value>
            <value>
                <fullName>Full Size SUV</fullName>
                <default>false</default>
                <label>Full Size SUV</label>
            </value>
            <value>
                <fullName>Luxury SUV</fullName>
                <default>false</default>
                <label>Luxury SUV</label>
            </value>
            <value>
                <fullName>Mini Van</fullName>
                <default>false</default>
                <label>Mini Van</label>
            </value>
            <value>
                <fullName>Hybrid Car</fullName>
                <default>false</default>
                <label>Hybrid Car</label>
            </value>
            <value>
                <fullName>Hybrid SUV</fullName>
                <default>false</default>
                <label>Hybrid SUV</label>
            </value>
            <value>
                <fullName>Production Motorhome</fullName>
                <default>false</default>
                <label>Production Motorhome</label>
            </value>
            <value>
                <fullName>Honeywagon</fullName>
                <default>false</default>
                <label>Honeywagon</label>
            </value>
            <value>
                <fullName>Star Motorhome</fullName>
                <default>false</default>
                <label>Star Motorhome</label>
            </value>
            <value>
                <fullName>Luxury</fullName>
                <default>false</default>
                <label>Luxury</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### End_Date_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_Date_Time__c</fullName>
    <externalId>false</externalId>
    <label>End Date Time</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### Driver_Name_1__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_Name_1__c</fullName>
    <externalId>false</externalId>
    <label>Driver Name 1</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### isFromCommunity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isFromCommunity__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>isFromCommunity</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
### Internal_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Internal Notes</label>
    <length>1000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Start_city__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_city__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Start city</label>
    <referenceTo>City__c</referenceTo>
    <relationshipLabel>Freight</relationshipLabel>
    <relationshipName>Freight</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Driver_Mobile_1__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_Mobile_1__c</fullName>
    <externalId>false</externalId>
    <label>Driver Mobile 1</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Start_Date_Time_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_Date_Time_Text__c</fullName>
    <externalId>false</externalId>
    <label>Start Date Time Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Freight_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Trip_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Freight Trip Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Freight__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Freight Sub Trips/Vehicles</relationshipLabel>
    <relationshipName>FreightSubTrips</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Assistance_for_international_customers__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Assistance_for_international_customers__c</fullName>
    <externalId>false</externalId>
    <label>Assistance for international customers</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Duties_and_taxes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Duties_and_taxes__c</fullName>
    <externalId>false</externalId>
    <label>Duties and taxes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Amenities__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Amenities__c</fullName>
    <externalId>false</externalId>
    <label>Amenities</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>WiFi</fullName>
                <default>false</default>
                <label>WiFi</label>
            </value>
            <value>
                <fullName>DVD</fullName>
                <default>false</default>
                <label>DVD</label>
            </value>
            <value>
                <fullName>Satellite TV</fullName>
                <default>false</default>
                <label>Satellite TV</label>
            </value>
            <value>
                <fullName>Outlets In Rows</fullName>
                <default>false</default>
                <label>Outlets In Rows</label>
            </value>
            <value>
                <fullName>Table</fullName>
                <default>false</default>
                <label>Table</label>
            </value>
            <value>
                <fullName>Trailer Hitch</fullName>
                <default>false</default>
                <label>Trailer Hitch</label>
            </value>
            <value>
                <fullName>Trailer</fullName>
                <default>false</default>
                <label>Trailer</label>
            </value>
            <value>
                <fullName>Restroom</fullName>
                <default>false</default>
                <label>Restroom</label>
            </value>
            <value>
                <fullName>Executive Coach</fullName>
                <default>false</default>
                <label>Executive Coach</label>
            </value>
            <value>
                <fullName>Sleepers</fullName>
                <default>false</default>
                <label>Sleepers</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### End_Date_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_Date_Text__c</fullName>
    <externalId>false</externalId>
    <label>End Date Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Demurrage_storage_and_detention_charges__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Demurrage_storage_and_detention_charges__c</fullName>
    <externalId>false</externalId>
    <label>Demurrage, storage and detention charges</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Do_you_have_itinerary__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Do_you_have_itinerary__c</fullName>
    <externalId>false</externalId>
    <label>Do you have itinerary?</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Yes_No</valueSetName>
    </valueSet>
</CustomField>
```
### Back_end_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Back_end_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Back-end Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Freight</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Time__c</fullName>
    <externalId>false</externalId>
    <label>Time</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### GT_Preferences__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Preferences__c</fullName>
    <externalId>false</externalId>
    <label>GT Preferences</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Office_Location</valueSetName>
    </valueSet>
</CustomField>
```
### Documentation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Documentation__c</fullName>
    <externalId>false</externalId>
    <label>Documentation</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Status_Change_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Change_Date__c</fullName>
    <description>Field used to capture the business days each Freight trip record stays in a status.</description>
    <externalId>false</externalId>
    <label>Status - Change Date</label>
    <required>false</required>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Budget__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budget__c</fullName>
    <externalId>false</externalId>
    <label>Budget</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Options_Sent_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Options_Sent_to_Client__c</fullName>
    <externalId>false</externalId>
    <label>Options Sent to Client</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Email_Body_Release_Bid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Body_Release_Bid__c</fullName>
    <externalId>false</externalId>
    <label>Email Body Release Bid</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Start_Date_Full__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_Date_Full__c</fullName>
    <externalId>false</externalId>
    <label>Start Date Full</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Bid_Sub_Trip__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Sub_Trip__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <description>Bid for Freight Sub Trip Details</description>
    <externalId>false</externalId>
    <label>Bid</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Bid__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Bid</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Freight Sub Trips</relationshipLabel>
    <relationshipName>FreightSubTrips</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Past_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Past_Due__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Today()&gt; Deadline_Date__c &amp;&amp; (ISPICKVAL( Status__c , &quot;Itinerary Received&quot;) || ISPICKVAL(Status__c, &quot;Bid Request Stage&quot;) || ISPICKVAL(Status__c, &quot;Send to Client&quot;) || ISPICKVAL(Status__c, &quot;Rework&quot;)), true, false)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Past Due</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Type_of_Equipment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Type_of_Equipment__c</fullName>
    <externalId>false</externalId>
    <label>Type of Equipment</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Email_Subject_Release_Bid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Subject_Release_Bid__c</fullName>
    <externalId>false</externalId>
    <label>Email Subject Release Bid</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Client_speak_to_any_carriers_agencies__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_speak_to_any_carriers_agencies__c</fullName>
    <externalId>false</externalId>
    <label>Client speak to any carriers/agencies?</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Trip_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Trip Notes</label>
    <length>1000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Import_and_export_charges_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Import_and_export_charges_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Import and export charges Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date__c</fullName>
    <externalId>false</externalId>
    <label>Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### ATA_Carnet_raising_and_processing_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ATA_Carnet_raising_and_processing_Rate__c</fullName>
    <externalId>false</externalId>
    <label>ATA Carnet raising and processing Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Deadline_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deadline_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Deadline_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Deadline_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Deadline_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Deadline_Date__c)), CASE(
  MONTH(Deadline_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Deadline_Date__c)) + &quot;-&quot; + TEXT(YEAR(Deadline_Date__c))), &quot;&quot;)</formula>
    <label>Deadline Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Last_Modified_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Last_Modified_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(DATEVALUE(LastModifiedDate)), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(DATEVALUE(LastModifiedDate))) + &quot;-&quot; + CASE(
  MONTH(DATEVALUE(LastModifiedDate)),
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
) + &quot;-&quot; + TEXT(YEAR(DATEVALUE(LastModifiedDate))), CASE(
  MONTH(DATEVALUE(LastModifiedDate)),
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
) + &quot;-&quot; + TEXT(DAY(DATEVALUE(LastModifiedDate))) + &quot;-&quot; + TEXT(YEAR(DATEVALUE(LastModifiedDate)))), &quot;&quot;)</formula>
    <label>Last Modified Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Manifest_Commercial_invoice__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Manifest_Commercial_invoice__c</fullName>
    <externalId>false</externalId>
    <label>Manifest/Commercial invoice</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Yes_No</valueSetName>
    </valueSet>
</CustomField>
```
### Which_carrier_where_in_negotiation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Which_carrier_where_in_negotiation__c</fullName>
    <externalId>false</externalId>
    <label>Which carrier/where in negotiation?</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Customs_clearance_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Customs_clearance_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Customs clearance Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Parking__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Parking__c</fullName>
    <externalId>false</externalId>
    <label>Parking</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Customs__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Customs__c</fullName>
    <externalId>false</externalId>
    <label>Customs</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Trip_Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Order__c</fullName>
    <externalId>false</externalId>
    <label>Trip Order</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
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
### Model__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Model__c</fullName>
    <externalId>false</externalId>
    <label>Model</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>417</fullName>
                <default>false</default>
                <label>417</label>
            </value>
            <value>
                <fullName>9700</fullName>
                <default>false</default>
                <label>9700</label>
            </value>
            <value>
                <fullName>CX45</fullName>
                <default>false</default>
                <label>CX45</label>
            </value>
            <value>
                <fullName>E model</fullName>
                <default>false</default>
                <label>E model</label>
            </value>
            <value>
                <fullName>H341</fullName>
                <default>false</default>
                <label>H341</label>
            </value>
            <value>
                <fullName>H345</fullName>
                <default>false</default>
                <label>H345</label>
            </value>
            <value>
                <fullName>J model</fullName>
                <default>false</default>
                <label>J model</label>
            </value>
            <value>
                <fullName>Renaissance</fullName>
                <default>false</default>
                <label>Renaissance</label>
            </value>
            <value>
                <fullName>T2100</fullName>
                <default>false</default>
                <label>T2100</label>
            </value>
            <value>
                <fullName>T2145</fullName>
                <default>false</default>
                <label>T2145</label>
            </value>
            <value>
                <fullName>XL2</fullName>
                <default>false</default>
                <label>XL2</label>
            </value>
            <value>
                <fullName>XL3</fullName>
                <default>false</default>
                <label>XL3</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Parking_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Parking_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Parking Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Flight_info__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Flight_info__c</fullName>
    <externalId>false</externalId>
    <label>Flight info</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Today_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Today_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(TODAY()), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(TODAY())) + &quot;-&quot; + CASE(
  MONTH(TODAY()),
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
) + &quot;-&quot; + TEXT(YEAR(TODAY())), CASE(
  MONTH(TODAY()),
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
) + &quot;-&quot; + TEXT(DAY(TODAY())) + &quot;-&quot; + TEXT(YEAR(TODAY()))), &quot;&quot;)</formula>
    <label>Today Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Taxes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Taxes__c</fullName>
    <externalId>false</externalId>
    <label>Taxes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Toll_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Toll_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Toll Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Trip_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Type__c</fullName>
    <externalId>false</externalId>
    <label>Trip Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <controllingField>Service_Type__c</controllingField>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>RT</fullName>
                <default>false</default>
                <label>RT</label>
            </value>
            <value>
                <fullName>One Way</fullName>
                <default>false</default>
                <label>One Way</label>
            </value>
            <value>
                <fullName>LTL</fullName>
                <default>false</default>
                <label>LTL</label>
            </value>
            <value>
                <fullName>Hot Shot</fullName>
                <default>false</default>
                <label>Hot Shot</label>
            </value>
            <value>
                <fullName>Dedicated</fullName>
                <default>false</default>
                <label>Dedicated</label>
            </value>
            <value>
                <fullName>PTL</fullName>
                <default>false</default>
                <label>PTL</label>
            </value>
            <value>
                <fullName>TBD 1</fullName>
                <default>false</default>
                <label>TBD 1</label>
            </value>
            <value>
                <fullName>TBD 2</fullName>
                <default>false</default>
                <label>TBD 2</label>
            </value>
            <value>
                <fullName>LCL</fullName>
                <default>false</default>
                <label>LCL</label>
            </value>
            <value>
                <fullName>Port to Port</fullName>
                <default>false</default>
                <label>Port to Port</label>
            </value>
            <value>
                <fullName>Door to Door</fullName>
                <default>false</default>
                <label>Door to Door</label>
            </value>
            <value>
                <fullName>Flatbed</fullName>
                <default>false</default>
                <label>Flatbed</label>
            </value>
        </valueSetDefinition>
        <valueSettings>
            <controllingFieldValue>Ocean</controllingFieldValue>
            <valueName>TBD 1</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Ocean</controllingFieldValue>
            <valueName>LCL</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Ocean</controllingFieldValue>
            <valueName>Port to Port</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Ocean</controllingFieldValue>
            <valueName>Door to Door</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Trucking</controllingFieldValue>
            <valueName>LTL</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Trucking</controllingFieldValue>
            <valueName>Hot Shot</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Trucking</controllingFieldValue>
            <valueName>Dedicated</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Trucking</controllingFieldValue>
            <valueName>PTL</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Trucking</controllingFieldValue>
            <valueName>Flatbed</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>RT</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>One Way</valueName>
        </valueSettings>
    </valueSet>
</CustomField>
```
### Equipment_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Equipment_Type__c</fullName>
    <externalId>false</externalId>
    <label>Equipment Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>28 Foot Van Hill Trailers</fullName>
                <default>false</default>
                <label>28 Foot Van Hill Trailers</label>
            </value>
            <value>
                <fullName>Drop Deck Van Trailers</fullName>
                <default>false</default>
                <label>Drop Deck Van Trailers</label>
            </value>
            <value>
                <fullName>53-Foot Van Trailers</fullName>
                <default>false</default>
                <label>53-Foot Van Trailers</label>
            </value>
            <value>
                <fullName>Expandable Trailers</fullName>
                <default>false</default>
                <label>Expandable Trailers</label>
            </value>
            <value>
                <fullName>Gooseneck Equipped Tractors</fullName>
                <default>false</default>
                <label>Gooseneck Equipped Tractors</label>
            </value>
            <value>
                <fullName>53-Foot Drop Deck Curtain-side Trailers</fullName>
                <default>false</default>
                <label>53-Foot Drop Deck Curtain-side Trailers</label>
            </value>
            <value>
                <fullName>Vending Trailers</fullName>
                <default>false</default>
                <label>Vending Trailers</label>
            </value>
            <value>
                <fullName>Climate Controlled Trailers</fullName>
                <default>false</default>
                <label>Climate Controlled Trailers</label>
            </value>
            <value>
                <fullName>Auto Transport Trailers</fullName>
                <default>false</default>
                <label>Auto Transport Trailers</label>
            </value>
            <value>
                <fullName>Drop Deck Flatbed Trailers</fullName>
                <default>false</default>
                <label>Drop Deck Flatbed Trailers</label>
            </value>
            <value>
                <fullName>Gooseneck Trailers</fullName>
                <default>false</default>
                <label>Gooseneck Trailers</label>
            </value>
            <value>
                <fullName>Rollback trucks</fullName>
                <default>false</default>
                <label>Rollback trucks</label>
            </value>
            <value>
                <fullName>Belly Box Trailers</fullName>
                <default>false</default>
                <label>Belly Box Trailers</label>
            </value>
            <value>
                <fullName>Hospitality Trailers</fullName>
                <default>false</default>
                <label>Hospitality Trailers</label>
            </value>
            <value>
                <fullName>Lift gate Van Trailers</fullName>
                <default>false</default>
                <label>Lift gate Van Trailers</label>
            </value>
            <value>
                <fullName>Tag Trailers</fullName>
                <default>false</default>
                <label>Tag Trailers</label>
            </value>
            <value>
                <fullName>Motorsports Trailers</fullName>
                <default>false</default>
                <label>Motorsports Trailers</label>
            </value>
            <value>
                <fullName>Long Wheelbase Trailers</fullName>
                <default>false</default>
                <label>Long Wheelbase Trailers</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Travel_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Travel_Type__c</fullName>
    <externalId>false</externalId>
    <label>Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Spot</fullName>
                <default>false</default>
                <label>Spot</label>
            </value>
            <value>
                <fullName>Arrive</fullName>
                <default>false</default>
                <label>Arrive</label>
            </value>
            <value>
                <fullName>Stop</fullName>
                <default>false</default>
                <label>Stop</label>
            </value>
            <value>
                <fullName>Drop Off</fullName>
                <default>false</default>
                <label>Drop Off</label>
            </value>
            <value>
                <fullName>Pick Up</fullName>
                <default>false</default>
                <label>Pick Up</label>
            </value>
            <value>
                <fullName>Depart</fullName>
                <default>false</default>
                <label>Depart</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Freight_Trip_Contents__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Trip_Contents__c</fullName>
    <externalId>false</externalId>
    <label>Freight Trip Contents</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Capacity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Capacity__c</fullName>
    <externalId>false</externalId>
    <label>Capacity</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Trailer_information__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trailer_information__c</fullName>
    <externalId>false</externalId>
    <label>Trailer information</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Airline_collection__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airline_collection__c</fullName>
    <externalId>false</externalId>
    <label>Airline collection</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Duties_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Duties_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Duties Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Demurrage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Demurrage__c</fullName>
    <externalId>false</externalId>
    <label>Demurrage</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Freight_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Type__c</fullName>
    <externalId>false</externalId>
    <label>Freight Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Sea</fullName>
                <default>false</default>
                <label>Sea</label>
            </value>
            <value>
                <fullName>Ground</fullName>
                <default>false</default>
                <label>Ground</label>
            </value>
            <value>
                <fullName>Air</fullName>
                <default>false</default>
                <label>Air</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Confirm_size__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirm_size__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Confirm size</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### ATA_carnet_expenses_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ATA_carnet_expenses_Rate__c</fullName>
    <externalId>false</externalId>
    <label>ATA carnet expenses Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Location_Details_Drop_Off__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Details_Drop_Off__c</fullName>
    <externalId>false</externalId>
    <label>Location Details Drop Off</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Show_included_rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Show_included_rate__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Show included rate</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Taxes_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Taxes_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Taxes Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Storage_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Storage_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Storage Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Considerations_Concessions_important__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Considerations_Concessions_important__c</fullName>
    <externalId>false</externalId>
    <label>Considerations/Concessions important</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Billing_Options__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Billing_Options__c</fullName>
    <externalId>false</externalId>
    <label>Billing Options</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Check to Drive day of travel</fullName>
                <default>false</default>
                <label>Check to Drive day of travel</label>
            </value>
            <value>
                <fullName>Check must be mailed and received the Friday before Travel</fullName>
                <default>false</default>
                <label>Check must be mailed and received the Friday before Travel</label>
            </value>
            <value>
                <fullName>Credit card to be charged day of travel</fullName>
                <default>false</default>
                <label>Credit card to be charged day of travel</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Transport_insurance_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transport_insurance_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Transport insurance Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### End_Date_Time_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_Date_Time_Text__c</fullName>
    <externalId>false</externalId>
    <label>End Date Time Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Service_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Type__c</fullName>
    <externalId>false</externalId>
    <label>Service Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Ocean</fullName>
                <default>false</default>
                <label>Ocean</label>
            </value>
            <value>
                <fullName>Trucking</fullName>
                <default>false</default>
                <label>Trucking</label>
            </value>
            <value>
                <fullName>Air</fullName>
                <default>false</default>
                <label>Air</label>
            </value>
            <value>
                <fullName>Luggage truck</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Luggage truck</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
### Import_and_export_charges__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Import_and_export_charges__c</fullName>
    <externalId>false</externalId>
    <label>Import and export charges</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Vendor_Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Contact__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Vendor Contact</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Freight (Vendor Contact)</relationshipLabel>
    <relationshipName>Freight1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Is_it_an_exclusive_shipment_or_LTL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Is_it_an_exclusive_shipment_or_LTL__c</fullName>
    <externalId>false</externalId>
    <label>Is it an exclusive shipment or LTL?</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Exclusive</fullName>
                <default>false</default>
                <label>Exclusive</label>
            </value>
            <value>
                <fullName>LTL</fullName>
                <default>false</default>
                <label>LTL</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Make_Model__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Make_Model__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Make__c) &amp; &quot;/&quot; &amp; TEXT(Model__c)</formula>
    <label>Make/Model</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Carnet_info__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Carnet_info__c</fullName>
    <externalId>false</externalId>
    <label>Carnet info</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Start_Date_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_Date_Time__c</fullName>
    <externalId>false</externalId>
    <label>Start Date Time</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
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
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Bid_Status</valueSetName>
    </valueSet>
</CustomField>
```
### Total_Price__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Price__c</fullName>
    <externalId>false</externalId>
    <label>Total Price</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Vehicle_Ref__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vehicle_Ref__c</fullName>
    <externalId>false</externalId>
    <label>Vehicle Ref</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Documentation_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Documentation_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Documentation Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Insurances__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Insurances__c</fullName>
    <externalId>false</externalId>
    <label>Insurances</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Airline_Info_Special_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airline_Info_Special_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Coach will meet group in front of Hotel</fullName>
                <default>false</default>
                <label>Coach will meet group in front of Hotel</label>
            </value>
            <value>
                <fullName>Coach will meet group in front of Venue</fullName>
                <default>false</default>
                <label>Coach will meet group in front of Venue</label>
            </value>
            <value>
                <fullName>Coach will meet group curbside of Baggage Claim</fullName>
                <default>false</default>
                <label>Coach will meet group curbside of Baggage Claim</label>
            </value>
            <value>
                <fullName>Coach will be in a holding area, please call dispatch</fullName>
                <default>false</default>
                <label>Coach will be in a holding area, please call dispatch</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Storage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Storage__c</fullName>
    <externalId>false</externalId>
    <label>Storage</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Estimated_weight__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Estimated_weight__c</fullName>
    <externalId>false</externalId>
    <label>Estimated weight</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contracting_Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Terms__c</fullName>
    <externalId>false</externalId>
    <label>Contracting Terms</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Make__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Make__c</fullName>
    <externalId>false</externalId>
    <label>Make</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Dina</fullName>
                <default>false</default>
                <label>Dina</label>
            </value>
            <value>
                <fullName>Eagle</fullName>
                <default>false</default>
                <label>Eagle</label>
            </value>
            <value>
                <fullName>Ford</fullName>
                <default>false</default>
                <label>Ford</label>
            </value>
            <value>
                <fullName>Freightliner</fullName>
                <default>false</default>
                <label>Freightliner</label>
            </value>
            <value>
                <fullName>Irizar</fullName>
                <default>false</default>
                <label>Irizar</label>
            </value>
            <value>
                <fullName>MCI</fullName>
                <default>false</default>
                <label>MCI</label>
            </value>
            <value>
                <fullName>Neoplan</fullName>
                <default>false</default>
                <label>Neoplan</label>
            </value>
            <value>
                <fullName>Prevost</fullName>
                <default>false</default>
                <label>Prevost</label>
            </value>
            <value>
                <fullName>Setra</fullName>
                <default>false</default>
                <label>Setra</label>
            </value>
            <value>
                <fullName>Vanhool</fullName>
                <default>false</default>
                <label>Vanhool</label>
            </value>
            <value>
                <fullName>Volvo</fullName>
                <default>false</default>
                <label>Volvo</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Vendor_lookup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_lookup__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Vendor</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Vendor</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Freight</relationshipLabel>
    <relationshipName>Freight</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Any_specific_info_need_for_entering_the__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Any_specific_info_need_for_entering_the__c</fullName>
    <externalId>false</externalId>
    <label>Any specific info need for entering the</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tolls__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tolls__c</fullName>
    <externalId>false</externalId>
    <label>Tolls</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Email_Body_Bid_Request_Link__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Body_Bid_Request_Link__c</fullName>
    <externalId>false</externalId>
    <label>Email Body Bid Request Link</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Freight_Sub_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Sub_Trip_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Freight Sub Trip Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Freight__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Sub Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Freight Equipment Information</relationshipLabel>
    <relationshipName>FreightEquipments</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Confirm_all_permits_ATA_Carnets_Import__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirm_all_permits_ATA_Carnets_Import__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Confirm all permits (ATA Carnets, Import</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Duties_and_taxes_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Duties_and_taxes_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Duties and taxes Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Client_Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Contact__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Client Contact</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Freight</relationshipLabel>
    <relationshipName>Freight</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Airline_collection_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airline_collection_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Airline collection Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### ATA_carnet_expenses__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ATA_carnet_expenses__c</fullName>
    <externalId>false</externalId>
    <label>ATA carnet expenses</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Location_Pick_up__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Pick_up__c</fullName>
    <externalId>false</externalId>
    <label>Location Pick up</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Airport</fullName>
                <default>false</default>
                <label>Airport</label>
            </value>
            <value>
                <fullName>Hotel</fullName>
                <default>false</default>
                <label>Hotel</label>
            </value>
            <value>
                <fullName>Venue</fullName>
                <default>false</default>
                <label>Venue</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Freight</relationshipLabel>
    <relationshipName>Freight</relationshipName>
    <required>true</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Trace_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trace_Date__c</fullName>
    <externalId>false</externalId>
    <label>Trace Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Insurances_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Insurances_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Insurances Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Bid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Bid</label>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Vehicle Details</relationshipLabel>
    <relationshipName>Vehicles</relationshipName>
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
### Custom_exam_charges__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Custom_exam_charges__c</fullName>
    <externalId>false</externalId>
    <label>Custom exam charges</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Start_Date_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_Date_Text__c</fullName>
    <externalId>false</externalId>
    <label>Start Date Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Unloading__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Unloading__c</fullName>
    <externalId>false</externalId>
    <label>Unloading</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Custom_exam_charges_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Custom_exam_charges_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Custom exam charges Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Customs_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Customs_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Customs Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### ProdName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ProdName__c</fullName>
    <externalId>false</externalId>
    <label>ProdName</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Other_Amenities__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Other_Amenities__c</fullName>
    <externalId>false</externalId>
    <label>Other Amenities</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Email_Body_Bid_Request__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Body_Bid_Request__c</fullName>
    <externalId>false</externalId>
    <label>Email Body Bid Request</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Equipment_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Equipment_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Coach will meet group in front of Hotel</fullName>
                <default>false</default>
                <label>Coach will meet group in front of Hotel</label>
            </value>
            <value>
                <fullName>Coach will meet group in front of Venue</fullName>
                <default>false</default>
                <label>Coach will meet group in front of Venue</label>
            </value>
            <value>
                <fullName>Coach will meet group curbside of Baggage Claim</fullName>
                <default>false</default>
                <label>Coach will meet group curbside of Baggage Claim</label>
            </value>
            <value>
                <fullName>Coach will be in a holding area, please call dispatch</fullName>
                <default>false</default>
                <label>Coach will be in a holding area, please call dispatch</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Demurrage_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Demurrage_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Demurrage Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### End_Date_Full__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_Date_Full__c</fullName>
    <externalId>false</externalId>
    <label>End Date Full</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Sub_Trip_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sub_Trip_Type__c</fullName>
    <externalId>false</externalId>
    <label>Trip Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Airport Transfer</fullName>
                <default>false</default>
                <label>Airport Transfer</label>
            </value>
            <value>
                <fullName>City to City</fullName>
                <default>false</default>
                <label>City to City</label>
            </value>
            <value>
                <fullName>Inter-City</fullName>
                <default>false</default>
                <label>Inter-City</label>
            </value>
            <value>
                <fullName>Lay Off</fullName>
                <default>false</default>
                <label>Lay Off</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Notes__c</fullName>
    <externalId>false</externalId>
    <label>Notes</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Status_Business_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Business_Days__c</fullName>
    <description>Business days Freight Trip record stays in a status.</description>
    <externalId>false</externalId>
    <formula>(5 * ( FLOOR( ( Today() - DATE( 1900, 1, 8) ) / 7 ) ) + MIN( 5, MOD( Today() - DATE( 1900, 1, 8), 7 ) ) )
-
(5 * ( FLOOR( ( Status_Change_Date__c - DATE( 1900, 1, 8) ) / 7 ) ) + MIN( 5, MOD( Status_Change_Date__c - DATE( 1900, 1, 8), 7 ) ) )</formula>
    <label>Status - Business Days</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Equipment_requested__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Equipment_requested__c</fullName>
    <externalId>false</externalId>
    <label>Equipment requested</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>52 ft&apos;</fullName>
                <default>false</default>
                <label>52 ft&apos;</label>
            </value>
            <value>
                <fullName>TBD1</fullName>
                <default>false</default>
                <label>TBD1</label>
            </value>
            <value>
                <fullName>Loading Gate</fullName>
                <default>false</default>
                <label>Loading Gate</label>
            </value>
            <value>
                <fullName>Lift Gate</fullName>
                <default>false</default>
                <label>Lift Gate</label>
            </value>
            <value>
                <fullName>Straps</fullName>
                <default>false</default>
                <label>Straps</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Airport_handling__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airport_handling__c</fullName>
    <externalId>false</externalId>
    <label>Airport handling</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Deadline_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deadline_Date__c</fullName>
    <externalId>false</externalId>
    <label>Deadline Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Sub_Trip_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sub_Trip_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Trip Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Driving_permits__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driving_permits__c</fullName>
    <externalId>false</externalId>
    <label>Driving permits</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### EndCityName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>EndCityName__c</fullName>
    <externalId>false</externalId>
    <label>EndCityName</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### ATA_Carnet_raising_and_processing__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ATA_Carnet_raising_and_processing__c</fullName>
    <externalId>false</externalId>
    <label>ATA Carnet raising and processing</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### StartCityName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>StartCityName__c</fullName>
    <externalId>false</externalId>
    <label>StartCityName</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Demurrage_storage_and_detention_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Demurrage_storage_and_detention_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Demurrage, storage and detention Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Estimated_Value__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Estimated_Value__c</fullName>
    <externalId>false</externalId>
    <label>Estimated Value</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Number_of_Days_Past_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Number_of_Days_Past_Due__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Past_Due__c = true, Today()- Deadline_Date__c, 0)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Number of Days Past Due</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### End_city__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>End_city__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>End city</label>
    <referenceTo>City__c</referenceTo>
    <relationshipLabel>Freight (End city)</relationshipLabel>
    <relationshipName>Freight1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Vessel_number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vessel_number__c</fullName>
    <externalId>false</externalId>
    <label>Vessel number</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Freight_Truck_Sq_Ft__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Truck_Sq_Ft__c</fullName>
    <externalId>false</externalId>
    <label>Freight Truck Sq Ft</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Location_Drop_Off_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Drop_Off_Type__c</fullName>
    <externalId>false</externalId>
    <label>Location Drop Off Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Airport</fullName>
                <default>false</default>
                <label>Airport</label>
            </value>
            <value>
                <fullName>Hotel</fullName>
                <default>false</default>
                <label>Hotel</label>
            </value>
            <value>
                <fullName>Venue</fullName>
                <default>false</default>
                <label>Venue</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Customs_clearance__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Customs_clearance__c</fullName>
    <externalId>false</externalId>
    <label>Customs clearance</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Transport_insurance__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transport_insurance__c</fullName>
    <externalId>false</externalId>
    <label>Transport insurance</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Line__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Line__c</fullName>
    <externalId>false</externalId>
    <label>Line #</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Local_transport__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Local_transport__c</fullName>
    <externalId>false</externalId>
    <label>Local transport</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description__c</fullName>
    <externalId>false</externalId>
    <label>Description</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Loading_charges_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loading_charges_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Loading charges Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Local_transport_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Local_transport_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Local transport Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Freight_Preferences__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Preferences__c</fullName>
    <externalId>false</externalId>
    <label>Freight Preferences</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Office_Location</valueSetName>
    </valueSet>
</CustomField>
```
### Loading_Unloading_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loading_Unloading_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Loading Unloading Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Equipment_FCQ__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Equipment_FCQ__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Equipment (FCQ)</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Group_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Group_Type__c</fullName>
    <externalId>false</externalId>
    <label>Group Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Cast</fullName>
                <default>false</default>
                <label>Cast</label>
            </value>
            <value>
                <fullName>Cast - Crew</fullName>
                <default>false</default>
                <label>Cast - Crew</label>
            </value>
            <value>
                <fullName>Crew</fullName>
                <default>false</default>
                <label>Crew</label>
            </value>
            <value>
                <fullName>Favor</fullName>
                <default>false</default>
                <label>Favor</label>
            </value>
            <value>
                <fullName>Scouts</fullName>
                <default>false</default>
                <label>Scouts</label>
            </value>
            <value>
                <fullName>Team</fullName>
                <default>false</default>
                <label>Team</label>
            </value>
            <value>
                <fullName>VIP</fullName>
                <default>false</default>
                <label>VIP</label>
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
    <externalId>false</externalId>
    <label>Vendor</label>
    <length>100</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Turn_over_relationship_for_best_rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Turn_over_relationship_for_best_rate__c</fullName>
    <externalId>false</externalId>
    <label>Turn over relationship for best rate?</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Confirm_Address_Route__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirm_Address_Route__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Confirm Address + Route</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Location_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Details__c</fullName>
    <externalId>false</externalId>
    <label>Location Details</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Equipment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Equipment__c</fullName>
    <externalId>false</externalId>
    <label>Equipment</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Location_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Type__c</fullName>
    <externalId>false</externalId>
    <label>Location Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Airport</fullName>
                <default>false</default>
                <label>Airport</label>
            </value>
            <value>
                <fullName>Hotel</fullName>
                <default>false</default>
                <label>Hotel</label>
            </value>
            <value>
                <fullName>Venue</fullName>
                <default>false</default>
                <label>Venue</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Airport_handling_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airport_handling_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Airport handling Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Status_Previous__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Previous__c</fullName>
    <externalId>false</externalId>
    <label>Status Previous</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Year__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Year__c</fullName>
    <externalId>false</externalId>
    <label>Year</label>
    <length>4</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Location_Drop_off__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Drop_off__c</fullName>
    <externalId>false</externalId>
    <label>Location Drop off</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Airport</fullName>
                <default>false</default>
                <label>Airport</label>
            </value>
            <value>
                <fullName>Hotel</fullName>
                <default>false</default>
                <label>Hotel</label>
            </value>
            <value>
                <fullName>Venue</fullName>
                <default>false</default>
                <label>Venue</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```

---
layout: default
title: Ground__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Ground__c
## Fields
### Date_Entered__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_Entered__c</fullName>
    <externalId>false</externalId>
    <label>Date Entered</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Billing_options_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Billing_options_Text__c</fullName>
    <externalId>false</externalId>
    <label>Billing options Text</label>
    <length>1000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Commission__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission__c</fullName>
    <externalId>false</externalId>
    <label>Commission %</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Rework_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rework_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Rework Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <relationshipLabel>Ground</relationshipLabel>
    <relationshipName>Ground</relationshipName>
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
        <valueSetDefinition>
            <sorted>false</sorted>
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
                <fullName>Star Coach</fullName>
                <default>false</default>
                <label>Star Coach</label>
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
### Trip_Vehicle__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Vehicle__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Trip Vehicle</label>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Prospect Vehicles</relationshipLabel>
    <relationshipName>bidVehicles</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Vehicles__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vehicles__c</fullName>
    <externalId>false</externalId>
    <label>Vehicles</label>
    <precision>10</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Sub_Trips__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sub_Trips__c</fullName>
    <externalId>false</externalId>
    <label>Sub-Trips</label>
    <precision>10</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Location__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location__c</fullName>
    <externalId>false</externalId>
    <label>Location</label>
    <length>100</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Community_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Community_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Community Notes</label>
    <length>131072</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
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
### Send_to_Client_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Send_to_Client_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Send to Client Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### To_PCC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_PCC__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(Send_to_Client__c), NULL , 

IF(ISBLANK(PCC__c), 

CASE(MOD( Send_to_Client__c - DATE(1985,6,24),7), 

0 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( TODAY () - Send_to_Client__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( TODAY() - Send_to_Client__c )/7)*5) , 

CASE(MOD( Send_to_Client__c - DATE(1985,6,24),7), 

0 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( PCC__c - Send_to_Client__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( PCC__c - Send_to_Client__c )/7)*5)))</formula>
    <label>To PCC</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Confirm_airport_pick_up_location__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirm_airport_pick_up_location__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Confirm airport pick up location</label>
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
    <length>5000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### To_Bid_Request__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_Bid_Request__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(Bid_Request__c), 

CASE(MOD( Date_Entered__c - DATE(1985,6,24),7), 

0 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( TODAY() - Date_Entered__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( TODAY() - Date_Entered__c )/7)*5) , 

CASE(MOD( Date_Entered__c - DATE(1985,6,24),7), 

0 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( Bid_Request__c - Date_Entered__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( Bid_Request__c - Date_Entered__c )/7)*5))</formula>
    <label>To Bid Request</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Total_Cost__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Cost__c</fullName>
    <externalId>false</externalId>
    <label>Total Cost</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Start_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Start_City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Start City</label>
    <referenceTo>City__c</referenceTo>
    <relationshipLabel>Ground</relationshipLabel>
    <relationshipName>Ground</relationshipName>
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
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Phone</type>
</CustomField>
```
### In_Contracting_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>In_Contracting_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>In Contracting Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Budgeting_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budgeting_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Budgeting Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
            <value>
                <fullName>Toilet / WC</fullName>
                <default>false</default>
                <label>Toilet / WC</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Special_Instructions__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Special_Instructions__c</fullName>
    <externalId>false</externalId>
    <label>Special Instructions</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Lead_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Lead_Time__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(MOD( Date_Entered__c - DATE(1985,6,24),7), 

0 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( Start_Date__c - Date_Entered__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( Start_Date__c - Date_Entered__c )/7)*5)</formula>
    <label>Lead Time</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Pending_Hotel_Counter_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Hotel_Counter_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Hotel Counter Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Final_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Status__c</fullName>
    <externalId>false</externalId>
    <label>Final Status</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Office__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Office__c</fullName>
    <externalId>false</externalId>
    <label>Office</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>RRU</fullName>
                <default>false</default>
                <label>RRU</label>
            </value>
            <value>
                <fullName>RRE</fullName>
                <default>false</default>
                <label>RRE</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Arriving_city__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arriving_city__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Arriving city</label>
    <referenceTo>City__c</referenceTo>
    <relationshipLabel>Ground (Arriving city)</relationshipLabel>
    <relationshipName>Ground1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Confirm_Trip_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirm_Trip_Notes__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Confirm Trip Notes</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Luggage_bays_need_to_be_completely_empty__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Luggage_bays_need_to_be_completely_empty__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <inlineHelpText>Luggage bays need to be completely empty – including any supplies you may store. Please confirm.</inlineHelpText>
    <label>Luggage bays need to be completely empty</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Status_Change_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Change_Date__c</fullName>
    <description>Field used to capture the business days each Ground record stays in a status.</description>
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
### Pieces_of_Luggage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pieces_of_Luggage__c</fullName>
    <externalId>false</externalId>
    <label>Pieces of Luggage</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### Contracting__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting__c</fullName>
    <externalId>false</externalId>
    <label>Contracting</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Gina Adams</fullName>
                <default>false</default>
                <label>Gina Adams</label>
            </value>
            <value>
                <fullName>Linda Cockrell</fullName>
                <default>false</default>
                <label>Linda Cockrell</label>
            </value>
            <value>
                <fullName>Jenevive Mendoza</fullName>
                <default>false</default>
                <label>Jenevive Mendoza</label>
            </value>
            <value>
                <fullName>Catherine Martin</fullName>
                <default>false</default>
                <label>Catherine Martin</label>
            </value>
            <value>
                <fullName>Stephanie Hester</fullName>
                <default>false</default>
                <label>Stephanie Hester</label>
            </value>
            <value>
                <fullName>Leslie Blevins</fullName>
                <default>false</default>
                <label>Leslie Blevins</label>
            </value>
            <value>
                <fullName>Amanda Byrne</fullName>
                <default>false</default>
                <label>Amanda Byrne</label>
            </value>
            <value>
                <fullName>Gregory Stillwell</fullName>
                <default>false</default>
                <label>Gregory Stillwell</label>
            </value>
            <value>
                <fullName>Dana Tun</fullName>
                <default>false</default>
                <label>Dana Tun</label>
            </value>
            <value>
                <fullName>Jana Leighty</fullName>
                <default>false</default>
                <label>Jana Leighty</label>
            </value>
            <value>
                <fullName>Tina Loera-Buxton</fullName>
                <default>false</default>
                <label>Tina Loera-Buxton</label>
            </value>
            <value>
                <fullName>Kate Hawn</fullName>
                <default>false</default>
                <label>Kate Hawn</label>
            </value>
            <value>
                <fullName>Lily McGuire</fullName>
                <default>false</default>
                <label>Lily McGuire</label>
            </value>
            <value>
                <fullName>Rhiannon Lewis</fullName>
                <default>false</default>
                <label>Rhiannon Lewis</label>
            </value>
            <value>
                <fullName>Sarah Bennett</fullName>
                <default>false</default>
                <label>Sarah Bennett</label>
            </value>
            <value>
                <fullName>Liandi Fourie</fullName>
                <default>false</default>
                <label>Liandi Fourie</label>
            </value>
            <value>
                <fullName>Jennifer Han</fullName>
                <default>false</default>
                <label>Jennifer Han</label>
            </value>
            <value>
                <fullName>Aline Rovella</fullName>
                <default>false</default>
                <label>Aline Rovella</label>
            </value>
            <value>
                <fullName>Margot van Erck</fullName>
                <default>false</default>
                <label>Margot van Erck</label>
            </value>
            <value>
                <fullName>Anna Visciano</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Anna Visciano</label>
            </value>
            <value>
                <fullName>Catherine Coutoux</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Catherine Coutoux</label>
            </value>
            <value>
                <fullName>Cristina Padilla</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Cristina Padilla</label>
            </value>
            <value>
                <fullName>Erica Murello</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Erica Murello</label>
            </value>
            <value>
                <fullName>Rene Granados</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Rene Granados</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Pending_Trip_Info_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Trip_Info_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Trip Info Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <description>Bid for GT Sub Trip Details</description>
    <externalId>false</externalId>
    <label>Bid</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Bid__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GT Bid</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>GT Sub Trips</relationshipLabel>
    <relationshipName>GTSubTrips</relationshipName>
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
    <formula>IF(Today()&gt; Deadline_Date__c &amp;&amp; (ISPICKVAL(  Status__c , &quot;Itinerary Received&quot;) || ISPICKVAL(Status__c , &quot;Bid Request Stage&quot;) || ISPICKVAL(Status__c , &quot;Send to Client&quot;) || ISPICKVAL(Status__c , &quot;Rework&quot;)), true, false)</formula>
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
### Base_Cost__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Base_Cost__c</fullName>
    <externalId>false</externalId>
    <label>Base Cost</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Production_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Type__c</fullName>
    <externalId>false</externalId>
    <label>Production Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>General</fullName>
                <default>false</default>
                <label>General</label>
            </value>
            <value>
                <fullName>Non-Union</fullName>
                <default>false</default>
                <label>Non-Union</label>
            </value>
            <value>
                <fullName>Special Equity</fullName>
                <default>false</default>
                <label>Special Equity</label>
            </value>
            <value>
                <fullName>Union</fullName>
                <default>false</default>
                <label>Union</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### In_Contracting__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>In_Contracting__c</fullName>
    <externalId>false</externalId>
    <label>In Contracting</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
### Coordinating_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Coordinating_Days__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK( Contracted__c ), 

CASE(MOD( Date_Entered__c - DATE(1985,6,24),7), 

0 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( TODAY () - Date_Entered__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( TODAY() - Date_Entered__c )/7)*5) , 

CASE(MOD( Date_Entered__c - DATE(1985,6,24),7), 

0 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( Contracted__c - Date_Entered__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( Contracted__c - Date_Entered__c )/7)*5))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Coordinating Days</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Client_Spend__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Spend__c</fullName>
    <externalId>false</externalId>
    <label>Client Spend</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
### Zip_Code__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Zip_Code__c</fullName>
    <externalId>false</externalId>
    <label>Zip Code</label>
    <length>20</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Market__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Market__c</fullName>
    <externalId>false</externalId>
    <label>Market</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Family Entertainment</fullName>
                <default>false</default>
                <label>Family Entertainment</label>
            </value>
            <value>
                <fullName>Theatrical</fullName>
                <default>false</default>
                <label>Theatrical</label>
            </value>
            <value>
                <fullName>Fine Arts</fullName>
                <default>false</default>
                <label>Fine Arts</label>
            </value>
            <value>
                <fullName>Sports</fullName>
                <default>false</default>
                <label>Sports</label>
            </value>
            <value>
                <fullName>Film</fullName>
                <default>false</default>
                <label>Film</label>
            </value>
            <value>
                <fullName>TV</fullName>
                <default>false</default>
                <label>TV</label>
            </value>
            <value>
                <fullName>Music</fullName>
                <default>false</default>
                <label>Music</label>
            </value>
            <value>
                <fullName>Miscellaneous</fullName>
                <default>false</default>
                <label>Miscellaneous</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Send_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Send_to_Client__c</fullName>
    <externalId>false</externalId>
    <label>Send to Client</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
### Rework_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rework_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Rework Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Deleted_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deleted_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Deleted Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Trip_Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Order__c</fullName>
    <description>Order for GT Sub Trip Details</description>
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
### Qty_of_Buses__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Qty_of_Buses__c</fullName>
    <externalId>false</externalId>
    <label>Qty of Buses</label>
    <precision>3</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Country__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Country__c</fullName>
    <externalId>false</externalId>
    <label>Country</label>
    <length>30</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### To_Contracting__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_Contracting__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(PCC__c), NULL , 

IF(ISBLANK( In_Contracting__c ), 

CASE(MOD( PCC__c - DATE(1985,6,24),7), 

0 , CASE( MOD( TODAY () - PCC__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( TODAY () - PCC__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( TODAY () - PCC__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( TODAY () - PCC__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( TODAY () - PCC__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( TODAY () - PCC__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( TODAY () - PCC__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( TODAY() - PCC__c )/7)*5) , 

CASE(MOD( PCC__c - DATE(1985,6,24),7), 

0 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( In_Contracting__c - PCC__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( In_Contracting__c - PCC__c )/7)*5)))</formula>
    <label>To Contracting</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Commission_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Due__c</fullName>
    <externalId>false</externalId>
    <label>Commission Due</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
### Pending_Airport_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Airport_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Airport Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Spoke_with__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Spoke_with__c</fullName>
    <externalId>false</externalId>
    <label>Spoke with</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>One way</fullName>
                <default>false</default>
                <label>One way</label>
            </value>
            <value>
                <fullName>RT</fullName>
                <default>false</default>
                <label>RT</label>
            </value>
            <value>
                <fullName>Shuttle</fullName>
                <default>false</default>
                <label>Shuttle</label>
            </value>
            <value>
                <fullName>Tour</fullName>
                <default>false</default>
                <label>Tour</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Bid_ID_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_ID_Conga__c</fullName>
    <description>Trip&apos;s Contracted Bid Id used in Conga</description>
    <externalId>false</externalId>
    <label>Bid ID</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
                <fullName>Start</fullName>
                <default>false</default>
                <label>Start</label>
            </value>
            <value>
                <fullName>End</fullName>
                <default>false</default>
                <label>End</label>
            </value>
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
            <value>
                <fullName>Shuttle</fullName>
                <default>false</default>
                <label>Shuttle</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Pending_Client_Signature_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Client_Signature_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Client Signature Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Capacity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Capacity__c</fullName>
    <externalId>false</externalId>
    <label>Capacity</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Commission_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Type__c</fullName>
    <externalId>false</externalId>
    <label>Commission Type</label>
    <length>5</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Preferred_Company__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Preferred_Company__c</fullName>
    <externalId>false</externalId>
    <label>Preferred Company</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Itinerary_notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Itinerary_notes__c</fullName>
    <externalId>false</externalId>
    <label>Itinerary notes</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Location_Details_Drop_Off__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Details_Drop_Off__c</fullName>
    <externalId>false</externalId>
    <label>Location Details Drop Off</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Driver_stay_with_Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_stay_with_Production__c</fullName>
    <externalId>false</externalId>
    <label>Driver stay with Production</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Yes</fullName>
                <default>false</default>
                <label>Yes</label>
            </value>
            <value>
                <fullName>No</fullName>
                <default>false</default>
                <label>No</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Itinerary__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Itinerary__c</fullName>
    <externalId>false</externalId>
    <label>Itinerary</label>
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
            <value>
                <fullName>Prepayment via bank transfer</fullName>
                <default>false</default>
                <label>Prepayment via bank transfer</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Sales_GT_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sales_GT_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Sales GT Details</label>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Preferred Vehicle Types</relationshipLabel>
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### To_Send_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_Send_to_Client__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(Bid_Request__c), NULL , 

IF(ISBLANK(Send_to_Client__c), 

CASE(MOD( Bid_Request__c - DATE(1985,6,24),7), 

0 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( TODAY () - Bid_Request__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( TODAY() - Bid_Request__c )/7)*5) , 

CASE(MOD( Bid_Request__c - DATE(1985,6,24),7), 

0 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( Send_to_Client__c - Bid_Request__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( Send_to_Client__c - Bid_Request__c )/7)*5)))</formula>
    <label>To Send to Client</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
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
    <type>MultiselectPicklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Coach</fullName>
                <default>false</default>
                <label>Coach</label>
            </value>
            <value>
                <fullName>Chauffeured</fullName>
                <default>false</default>
                <label>Chauffeured</label>
            </value>
            <value>
                <fullName>Rentals</fullName>
                <default>false</default>
                <label>Rentals</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Vehicle_Lookup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vehicle_Lookup__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Vehicle Ref.</label>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Ground (Vehicle Ref.)</relationshipLabel>
    <relationshipName>TravelVehicles</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### PCC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PCC__c</fullName>
    <externalId>false</externalId>
    <label>PCC</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
### Presenter_Provided_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Presenter_Provided_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Presenter Provided Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Bid_Request__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Request__c</fullName>
    <externalId>false</externalId>
    <label>Bid Request</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <relationshipLabel>Ground</relationshipLabel>
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contracted_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Contracted Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Deadline__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deadline__c</fullName>
    <externalId>false</externalId>
    <label>Deadline</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Make_Model__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Make_Model__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Make__c) &amp; &quot;/&quot; &amp;  TEXT(Model__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Make/Model</label>
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
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Bid Request Stage</fullName>
                <default>false</default>
                <label>Bid Request Stage</label>
            </value>
            <value>
                <fullName>Contracted</fullName>
                <default>false</default>
                <label>Contracted</label>
            </value>
            <value>
                <fullName>In Contracting</fullName>
                <default>false</default>
                <label>In Contracting</label>
            </value>
            <value>
                <fullName>Itinerary Received</fullName>
                <default>false</default>
                <label>Itinerary Received</label>
            </value>
            <value>
                <fullName>Pending Client Choice</fullName>
                <default>false</default>
                <label>Pending Client Choice</label>
            </value>
            <value>
                <fullName>Pending Client Signature</fullName>
                <default>false</default>
                <label>Pending Client Signature</label>
            </value>
            <value>
                <fullName>Pending Hotel Counter</fullName>
                <default>false</default>
                <label>Pending Hotel Counter</label>
            </value>
            <value>
                <fullName>Pending Update</fullName>
                <default>false</default>
                <label>Pending Update</label>
            </value>
            <value>
                <fullName>Budgeting</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Budgeting</label>
            </value>
            <value>
                <fullName>Cancelled</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Cancelled</label>
            </value>
            <value>
                <fullName>Confirmed</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Confirmed</label>
            </value>
            <value>
                <fullName>Contracted on Own</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Contracted on Own</label>
            </value>
            <value>
                <fullName>Delete</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Delete</label>
            </value>
            <value>
                <fullName>Pending Airport Confirmation</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Pending Airport Confirmation</label>
            </value>
            <value>
                <fullName>Pending Counter</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Pending Counter</label>
            </value>
            <value>
                <fullName>Pending Trip Information</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Pending Trip Information</label>
            </value>
            <value>
                <fullName>Presenter/Promoter Provided</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Presenter/Promoter Provided</label>
            </value>
            <value>
                <fullName>Rework</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Rework</label>
            </value>
            <value>
                <fullName>Send to Client</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Send to Client</label>
            </value>
        </valueSetDefinition>
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
### Service_Type_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Type_Text__c</fullName>
    <externalId>false</externalId>
    <label>Service Type Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Vehicle_Ref__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vehicle_Ref__c</fullName>
    <externalId>false</externalId>
    <label>Vehicle Ref. text</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Status_Ground__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Ground__c</fullName>
    <externalId>false</externalId>
    <label>Status Ground</label>
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
### Carrying_Equipment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Carrying_Equipment__c</fullName>
    <externalId>false</externalId>
    <label>Carrying Equipment</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Bid_Request_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Request_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Bid Request Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### How_will_the_coaches_be_labeled__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>How_will_the_coaches_be_labeled__c</fullName>
    <externalId>false</externalId>
    <label>How will the coaches be labeled?</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Airline_Info_Special_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airline_Info_Special_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Airline Info/Special  Notes</label>
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
### Community_Note_Available__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Community_Note_Available__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Community Note Available</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Send_to_Client_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Send_to_Client_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Send to Client Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Confirmed_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirmed_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Confirmed Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Presenter_Provided_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Presenter_Provided_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Presenter Provided Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Bid_Request_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Request_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Bid Request Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Contracting_Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Terms__c</fullName>
    <externalId>false</externalId>
    <label>Contracting Terms</label>
    <length>10000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Coordinator</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Stephanie Hester</fullName>
                <default>false</default>
                <label>Stephanie Hester</label>
            </value>
            <value>
                <fullName>Jesse Cook</fullName>
                <default>false</default>
                <label>Jesse Cook</label>
            </value>
            <value>
                <fullName>Gregory Stillwell</fullName>
                <default>false</default>
                <label>Gregory Stillwell</label>
            </value>
            <value>
                <fullName>Kate Hawn</fullName>
                <default>false</default>
                <label>Kate Hawn</label>
            </value>
            <value>
                <fullName>Amy Thatcher Fahey</fullName>
                <default>false</default>
                <label>Amy Thatcher Fahey</label>
            </value>
            <value>
                <fullName>Dana Tun</fullName>
                <default>false</default>
                <label>Dana Tun</label>
            </value>
            <value>
                <fullName>Madison Chackel</fullName>
                <default>false</default>
                <label>Madison Chackel</label>
            </value>
            <value>
                <fullName>Jenevive Mendoza</fullName>
                <default>false</default>
                <label>Jenevive Mendoza</label>
            </value>
            <value>
                <fullName>Gina Adams</fullName>
                <default>false</default>
                <label>Gina Adams</label>
            </value>
            <value>
                <fullName>Lisa Ohara</fullName>
                <default>false</default>
                <label>Lisa Ohara</label>
            </value>
            <value>
                <fullName>Nick Adams</fullName>
                <default>false</default>
                <label>Nick Adams</label>
            </value>
            <value>
                <fullName>Jennifer Han</fullName>
                <default>false</default>
                <label>Jennifer Han</label>
            </value>
            <value>
                <fullName>Rhiannon Lewis</fullName>
                <default>false</default>
                <label>Rhiannon Lewis</label>
            </value>
            <value>
                <fullName>Sarah Bennett</fullName>
                <default>false</default>
                <label>Sarah Bennett</label>
            </value>
            <value>
                <fullName>Amy Mallin</fullName>
                <default>false</default>
                <label>Amy Mallin</label>
            </value>
            <value>
                <fullName>Liandi Fourie</fullName>
                <default>false</default>
                <label>Liandi Fourie</label>
            </value>
            <value>
                <fullName>Arcadius Wojkowiak</fullName>
                <default>false</default>
                <label>Arcadius Wojkowiak</label>
            </value>
            <value>
                <fullName>Aline Rovella</fullName>
                <default>false</default>
                <label>Aline Rovella</label>
            </value>
            <value>
                <fullName>Sam Ruddick</fullName>
                <default>false</default>
                <label>Sam Ruddick</label>
            </value>
            <value>
                <fullName>Kyle Biebel</fullName>
                <default>false</default>
                <label>Kyle Biebel</label>
            </value>
            <value>
                <fullName>Margot van Erck</fullName>
                <default>false</default>
                <label>Margot van Erck</label>
            </value>
            <value>
                <fullName>Erica Murello</fullName>
                <default>false</default>
                <label>Erica Murello</label>
            </value>
            <value>
                <fullName>Ashton Smith</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Ashton Smith</label>
            </value>
            <value>
                <fullName>Cristina Padilla</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Cristina Padilla</label>
            </value>
            <value>
                <fullName>Douglas Hudson</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Douglas Hudson</label>
            </value>
            <value>
                <fullName>Emma Battey</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Emma Battey</label>
            </value>
            <value>
                <fullName>Rene Granados</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Rene Granados</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
            <value>
                <fullName>Other</fullName>
                <default>false</default>
                <label>Other</label>
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
            <value>Ground Travel Vendor</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Ground</relationshipLabel>
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Itinerary_Received_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Itinerary_Received_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Itinerary Received Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Invoiced_Amount__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoiced_Amount__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Invoiced__c = NULL, NULL,  Commission_Due__c )</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Invoiced Amount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
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
    <relationshipLabel>Ground (Client Contact)</relationshipLabel>
    <relationshipName>GroundGCQ</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Contracted__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted__c</fullName>
    <externalId>false</externalId>
    <label>Contracted</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production__c</fullName>
    <externalId>false</externalId>
    <label>Production</label>
    <length>100</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### To_Contracted__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_Contracted__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(In_Contracting__c), NULL , 

IF(ISBLANK(Contracted__c), 

CASE(MOD( In_Contracting__c - DATE(1985,6,24),7), 

0 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( TODAY () - In_Contracting__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( TODAY() - In_Contracting__c )/7)*5) , 

CASE(MOD( In_Contracting__c - DATE(1985,6,24),7), 

0 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( Contracted__c - In_Contracting__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( Contracted__c - In_Contracting__c )/7)*5)))</formula>
    <label>To Contracted</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Please_confirm_your_driver_GPS__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Please_confirm_your_driver_GPS__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Please confirm your driver is prepared with GPS and that you will be tracking flight information day of travel (if applicable):</inlineHelpText>
    <label>Please confirm your driver GPS</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### Charter__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Charter__c</fullName>
    <externalId>false</externalId>
    <label>Charter #</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contracted_On_Own_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted_On_Own_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Contracted On Own Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Paid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Paid__c</fullName>
    <externalId>false</externalId>
    <label>Paid</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Pending_Client_Choice_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Client_Choice_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Client Choice Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### In_Contracting_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>In_Contracting_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>In Contracting Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Pending_Client_Choice_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Client_Choice_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Client Choice Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Pending_Trip_info_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Trip_info_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Trip info Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Company__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Company__c</fullName>
    <externalId>false</externalId>
    <label>Company</label>
    <length>100</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Ground_Travel_Confirmation_Created_On__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ground_Travel_Confirmation_Created_On__c</fullName>
    <externalId>false</externalId>
    <label>Ground Travel Confirmation - Created On</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### GT_Freight__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Freight__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GT Freight</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>$Source.Production_Ground__c</field>
            <operation>equals</operation>
            <valueField>Freight__c.Production__c</valueField>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Ground</relationshipLabel>
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Options_by__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Options_by__c</fullName>
    <externalId>false</externalId>
    <label>Options by</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
### Number_of_Passengers__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Number_of_Passengers__c</fullName>
    <externalId>false</externalId>
    <label>Number of Passengers?</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Method_of_Payment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Method_of_Payment__c</fullName>
    <externalId>false</externalId>
    <label>Method of Payment</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Pending_Update_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Update_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Update Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Pending_Hotel_Counter_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Hotel_Counter_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Hotel Counter Initial Timestamp</label>
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
            <value>
                <fullName>Shuttling</fullName>
                <default>false</default>
                <label>Shuttling</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Status_Business_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Business_Days__c</fullName>
    <description>Business days Ground record stays in a status.</description>
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
### Deleted_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deleted_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Deleted Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Contracted_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Contracted Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <length>5000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>5</visibleLines>
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
### GT_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Trip_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GT Trip Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Ground__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GT Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>GT Sub Trips</relationshipLabel>
    <relationshipName>GTSubTrips</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Pipeline_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pipeline_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Pipeline Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Pending_Counter_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Counter_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Counter Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Bus_Company_s_24_Hour_Number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bus_Company_s_24_Hour_Number__c</fullName>
    <externalId>false</externalId>
    <label>Bus Company’s 24 Hour Number</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Phone</type>
</CustomField>
```
### GT_Sub_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Sub_Trip_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GT Sub Trip Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Ground__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GT Sub Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>GT Travel Information</relationshipLabel>
    <relationshipName>GTTravels</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Can_you_read_me_the_Trip_information__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Can_you_read_me_the_Trip_information__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Can you read me the Trip information including Date/Time(s)/Addresses/Airline Info?</inlineHelpText>
    <label>Can you read me the Trip information?</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Date</fullName>
                <default>false</default>
                <label>Date</label>
            </value>
            <value>
                <fullName>Time</fullName>
                <default>false</default>
                <label>Time</label>
            </value>
            <value>
                <fullName>Address</fullName>
                <default>false</default>
                <label>Address</label>
            </value>
            <value>
                <fullName>Airline info</fullName>
                <default>false</default>
                <label>Airline info</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Bids__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bids__c</fullName>
    <externalId>false</externalId>
    <label>Bids</label>
    <precision>10</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Cancelled_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cancelled_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Cancelled Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### All_Amenities__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>All_Amenities__c</fullName>
    <externalId>false</externalId>
    <formula>IF(INCLUDES(Amenities__c, &quot;WiFi&quot;),&quot;WiFi, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;DVD&quot;),&quot;DVD, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Satellite TV&quot;),&quot;Satellite TV, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Outlets In Rows&quot;),&quot;Outlets In Rows, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Table&quot;),&quot;Table, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Trailer Hitch&quot;),&quot;Trailer Hitch, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Trailer&quot;),&quot;Trailer, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Restroom&quot;),&quot;Restroom, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Executive Coach&quot;),&quot;Executive Coach, &quot;,NULL) &amp; 
IF(INCLUDES(Amenities__c, &quot;Sleepers&quot;),&quot;Sleepers, &quot;,NULL)
&amp;  Other_Amenities__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>All Amenities</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Service_Type_Ground__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Type_Ground__c</fullName>
    <externalId>false</externalId>
    <label>Service Type Ground</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Coach</fullName>
                <default>false</default>
                <label>Coach</label>
            </value>
            <value>
                <fullName>Chauffeured</fullName>
                <default>false</default>
                <label>Chauffeured</label>
            </value>
            <value>
                <fullName>Rentals</fullName>
                <default>false</default>
                <label>Rentals</label>
            </value>
            <value>
                <fullName>Charter</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Charter</label>
            </value>
            <value>
                <fullName>Freight</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Freight</label>
            </value>
            <value>
                <fullName>Full Tour</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Full Tour</label>
            </value>
            <value>
                <fullName>Production Vehicles</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Production Vehicles</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Cancelled_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cancelled_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Cancelled Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Pending_Counter_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Counter_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Counter Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Please_verify_the_size_year_brand_number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Please_verify_the_size_year_brand_number__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Please verify the size/year/brand/number of coaches</inlineHelpText>
    <label>Please verify the size/year/brand/number</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Size</fullName>
                <default>false</default>
                <label>Size</label>
            </value>
            <value>
                <fullName>Year</fullName>
                <default>false</default>
                <label>Year</label>
            </value>
            <value>
                <fullName>Brand</fullName>
                <default>false</default>
                <label>Brand</label>
            </value>
            <value>
                <fullName># of Coaches</fullName>
                <default>false</default>
                <label># of Coaches</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Invoiced__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoiced__c</fullName>
    <externalId>false</externalId>
    <label>Invoiced</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Budgeting_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budgeting_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Budgeting Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Driver_is_aware_that_he_she_will_be__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_is_aware_that_he_she_will_be__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <inlineHelpText>Driver is aware that he/she will be assisting with luggage in and out of the luggage bays. This is a requirement for our groups.</inlineHelpText>
    <label>Driver is aware that he/she will be</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Give_the_Bus_Company_the_group_leader_s__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Give_the_Bus_Company_the_group_leader_s__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <inlineHelpText>Give the Bus Company the group leader’s contact name and phone number</inlineHelpText>
    <label>Give the Bus Company the group leader’s</label>
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
### Production_Ground__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Ground__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Production Ground</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Ground Travel</relationshipLabel>
    <relationshipName>Ground</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Gear_Luggage_Space__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Gear_Luggage_Space__c</fullName>
    <externalId>false</externalId>
    <label>Gear/Luggage Space</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Itinerary_Received_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Itinerary_Received_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Itinerary Received Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Ground_Travel_Confirmation_Created_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ground_Travel_Confirmation_Created_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Ground_Travel_Confirmation_Created_On__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Ground_Travel_Confirmation_Created_On__c)) + &quot;-&quot; + CASE(
  MONTH(Ground_Travel_Confirmation_Created_On__c),
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
) + &quot;-&quot; + TEXT(YEAR(Ground_Travel_Confirmation_Created_On__c)), CASE(
  MONTH(Ground_Travel_Confirmation_Created_On__c),
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
) + &quot;-&quot; + TEXT(DAY(Ground_Travel_Confirmation_Created_On__c)) + &quot;-&quot; + TEXT(YEAR(Ground_Travel_Confirmation_Created_On__c))), &quot;&quot;)</formula>
    <label>Ground Travel Confirmation-Created Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Type_of_GT__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Type_of_GT__c</fullName>
    <externalId>false</externalId>
    <label>Type of GT</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Buses</fullName>
                <default>false</default>
                <label>Buses</label>
            </value>
            <value>
                <fullName>Car</fullName>
                <default>false</default>
                <label>Car</label>
            </value>
            <value>
                <fullName>Nightliner</fullName>
                <default>false</default>
                <label>Nightliner</label>
            </value>
            <value>
                <fullName>Vans</fullName>
                <default>false</default>
                <label>Vans</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Pending_Update_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Update_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Update Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Requested_Vehicle__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Requested_Vehicle__c</fullName>
    <externalId>false</externalId>
    <label>Requested Vehicle</label>
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
### Location_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Location_Details__c</fullName>
    <externalId>false</externalId>
    <label>Location Details</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### NAV_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>NAV_ID__c</fullName>
    <externalId>false</externalId>
    <label>NAV ID</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Pending_Client_Signature_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Client_Signature_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Client Signature Most Recent</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Confirmed_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirmed_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Confirmed Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Pending_Airport_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Airport_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Airport Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Travel_Information_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Travel_Information_Conga__c</fullName>
    <defaultValue>&quot;&lt;table width=&apos;100%&apos; cellspacing=&apos;0&apos; cellpadding=&apos;0&apos; border=&apos;0&apos; align=&apos;left&apos; valign=&apos;middle&apos;&gt;&lt;thead&gt;&lt;tr&gt;&lt;th width=&apos;55&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;VEHICLE&lt;/th&gt;&lt;th width=&apos;80&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;START DATE&lt;/th&gt;&lt;th width=&apos;45&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;TIME&lt;/th&gt;&lt;th width=&apos;70&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;END DATE&lt;/th&gt;&lt;th width=&apos;50&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;TIME&lt;/th&gt;&lt;th width=&apos;50&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;TYPE&lt;/th&gt;&lt;th width=&apos;50&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;GROUP&lt;/th&gt;&lt;th width=&apos;85&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;LOCATION &lt;br/&gt;PICK UP&lt;/th&gt;&lt;th width=&apos;85&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;LOCATION DROP OFF&lt;/th&gt;&lt;th width=&apos;85&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;LOCATION DETAILS&lt;/th&gt;&lt;th width=&apos;100&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black&apos;&gt;AIRLINE INFO/&lt;br/&gt;SPECIAL NOTES&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;&lt;tbody&gt;&lt;tr&gt;&lt;td width=&apos;55&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;80&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;45&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;70&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;50&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;50&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;50&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;85&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;85&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;85&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;td width=&apos;100&apos; height=&apos;20&apos; align=&apos;left&apos; style=&apos;padding:3px 4px;border-bottom:1px dashed black&apos;&gt;&lt;/td&gt;&lt;/tr&gt;&lt;/tbody&gt;&lt;/table&gt;&quot;</defaultValue>
    <description>Sub trips details for Conga.</description>
    <externalId>false</externalId>
    <label>Travel Information</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>25</visibleLines>
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
### Contracted_On_Own_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted_On_Own_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Contracted On Own Initial Timestamp</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Year__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Year__c</fullName>
    <externalId>false</externalId>
    <label>Year</label>
    <length>15</length>
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

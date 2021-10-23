---
layout: default
title: Housing__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Housing__c
## Fields
### Other_Venue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Other_Venue__c</fullName>
    <externalId>false</externalId>
    <label>Other Venue</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Date_Entered__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_Entered__c</fullName>
    <externalId>false</externalId>
    <label>Date Entered</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Vendor_Group__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Group__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Vendor</label>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Housing (Vendor)</relationshipLabel>
    <relationshipName>Vendors_Group</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Market_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Market_Type__c</fullName>
    <externalId>false</externalId>
    <label>Market Type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
                <fullName>Film</fullName>
                <default>false</default>
                <label>Film</label>
            </value>
            <value>
                <fullName>Fine Arts</fullName>
                <default>false</default>
                <label>Fine Arts</label>
            </value>
            <value>
                <fullName>Miscellaneous</fullName>
                <default>false</default>
                <label>Miscellaneous</label>
            </value>
            <value>
                <fullName>Music</fullName>
                <default>false</default>
                <label>Music</label>
            </value>
            <value>
                <fullName>Sports</fullName>
                <default>false</default>
                <label>Sports</label>
            </value>
            <value>
                <fullName>Theatrical</fullName>
                <default>false</default>
                <label>Theatrical</label>
            </value>
            <value>
                <fullName>TV</fullName>
                <default>false</default>
                <label>TV</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Commission__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission__c</fullName>
    <externalId>false</externalId>
    <label>Commission %</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Contracting_timeframe_after_options_sent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_timeframe_after_options_sent__c</fullName>
    <externalId>false</externalId>
    <label>Contracting timeframe after options sent</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Venue_Formula__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Venue_Formula__c</fullName>
    <externalId>false</externalId>
    <formula>IF(RecordType.DeveloperName == &quot;Tournament&quot;,Tournament_Name__c,Venue__r.Name)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Venue Formula</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### No_of_bids__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_of_bids__c</fullName>
    <externalId>false</externalId>
    <label>No. of bids</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Count_Active_Bid_Traces__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Count_Active_Bid_Traces__c</fullName>
    <externalId>false</externalId>
    <label>Count Active Bid Traces</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### CityName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CityName__c</fullName>
    <externalId>false</externalId>
    <label>CityName</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Close_Out__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Close_Out__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Close Out</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Nights_CC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Nights_CC__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Date_Out__c == Date_In__c, 1, Date_Out__c -  Date_In__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Nights</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Status_CC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_CC__c</fullName>
    <externalId>false</externalId>
    <label>Status</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Bid_Status</valueSetName>
    </valueSet>
</CustomField>
```
### Date_In_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_In_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Date_In__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Date_In__c)) + &quot;-&quot; + CASE(
  MONTH(Date_In__c),
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
) + &quot;-&quot; + TEXT(YEAR(Date_In__c)), CASE(
  MONTH(Date_In__c),
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
) + &quot;-&quot; + TEXT(DAY(Date_In__c)) + &quot;-&quot; + TEXT(YEAR(Date_In__c))), &quot;&quot;)</formula>
    <label>Date In Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Venue_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Venue_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Venue NAV</label>
    <length>20</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipLabel>Housing</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Segment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Segment__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(Market_Type__c,
&quot;Theatrical&quot;, &quot;Live Performance&quot;,
&quot;Family Entertainment&quot;, &quot;Live Performance&quot;,
&quot;Fine Arts&quot;, &quot;Live Performance&quot;,
&quot;Music&quot;, &quot;Live Performance&quot;,
&quot;Sports&quot;, &quot;Sports&quot;,
&quot;TV&quot;, &quot;Film&quot;,
&quot;Film&quot;, &quot;Film&quot;,
NULL)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Segment</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Date_In__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_In__c</fullName>
    <externalId>false</externalId>
    <label>Date In</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Historical_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Historical_Name__c</fullName>
    <externalId>false</externalId>
    <label>Historical Name</label>
    <length>60</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Total_Nights__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Nights__c</fullName>
    <externalId>false</externalId>
    <formula>Units__c * Nights__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Total Nights</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Total_Rebate_to_RR__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Rebate_to_RR__c</fullName>
    <externalId>false</externalId>
    <label>Total Rebate to RR</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Conf_s_Sent_to_Client_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Conf_s_Sent_to_Client_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Conf #s Sent to Client Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Internal_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Internal Notes</label>
    <length>2000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Booked_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Booked_Name__c</fullName>
    <externalId>false</externalId>
    <label>Booked Name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Projected_Units__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Projected_Units__c</fullName>
    <externalId>false</externalId>
    <label>Projected # Units</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Payment_type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Payment_type__c</fullName>
    <externalId>false</externalId>
    <label>Payment type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Individual</fullName>
                <default>true</default>
                <label>Individual</label>
            </value>
            <value>
                <fullName>Master Pay</fullName>
                <default>false</default>
                <label>Master Pay</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Tournament_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tournament_Status__c</fullName>
    <externalId>false</externalId>
    <label>Tournament Status</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>New</fullName>
                <default>false</default>
                <label>New</label>
            </value>
            <value>
                <fullName>In progress</fullName>
                <default>false</default>
                <label>In progress</label>
            </value>
            <value>
                <fullName>Contracted</fullName>
                <default>false</default>
                <label>Contracted</label>
            </value>
            <value>
                <fullName>Inactive</fullName>
                <default>false</default>
                <label>Inactive</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Lead_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Lead_Time__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(MOD( Date_Entered__c - DATE(1985,6,24),7), 

0 , CASE( MOD( Check_In__c  - Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( Check_In__c  - Date_Entered__c  ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( Check_In__c  - Date_Entered__c  ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( Check_In__c  - Date_Entered__c  ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( Check_In__c  - Date_Entered__c  ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( Check_In__c  - Date_Entered__c  ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( Check_In__c  - Date_Entered__c  ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( Check_In__c  - Date_Entered__c  )/7)*5)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Deadline_Trace_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deadline_Trace_Date__c</fullName>
    <externalId>false</externalId>
    <label>Deadline Trace Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
### Concessions_Requested__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Concessions_Requested__c</fullName>
    <externalId>false</externalId>
    <label>Concessions Requested</label>
    <length>5000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Nights__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Nights__c</fullName>
    <externalId>false</externalId>
    <label>Nights</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Total_Rebate_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Rebate_to_Client__c</fullName>
    <externalId>false</externalId>
    <label>Total Rebate to Client</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Status_Change_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Change_Date__c</fullName>
    <description>Field used to capture the business days each housing record stays in a status.</description>
    <externalId>false</externalId>
    <label>Status - Change Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Options_sent_to_client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Options_sent_to_client__c</fullName>
    <externalId>false</externalId>
    <label>Options sent to client</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### PCC_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PCC_Days__c</fullName>
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

0 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
1 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
2 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
3 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
4 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
5 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
6 , CASE( MOD( PCC__c  -  Send_to_Client__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
999) 
+ 
(FLOOR(( PCC__c  -  Send_to_Client__c )/7)*5)))</formula>
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
### Past_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Past_Due__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Today()&gt; Deadline_Date__c &amp;&amp; (ISPICKVAL( Status_CC__c , &quot;Itinerary Received&quot;) || ISPICKVAL(Status_CC__c , &quot;Bid Request Stage&quot;) || ISPICKVAL(Status_CC__c , &quot;Send to Client&quot;) || ISPICKVAL(Status_CC__c , &quot;Rework&quot;)), true, false)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Past Due</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Avg_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Avg_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Avg Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Star_Preference__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Star_Preference__c</fullName>
    <externalId>false</externalId>
    <label>Star Preference</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>1</fullName>
                <default>false</default>
                <label>1</label>
            </value>
            <value>
                <fullName>2</fullName>
                <default>false</default>
                <label>2</label>
            </value>
            <value>
                <fullName>3</fullName>
                <default>false</default>
                <label>3</label>
            </value>
            <value>
                <fullName>4</fullName>
                <default>false</default>
                <label>4</label>
            </value>
            <value>
                <fullName>5</fullName>
                <default>false</default>
                <label>5</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Group__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Group__c</fullName>
    <externalId>false</externalId>
    <label>Group</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
                <fullName>Team</fullName>
                <default>false</default>
                <label>Team</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Production_CC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_CC__c</fullName>
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Housing</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>true</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Special_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Special_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Special Notes</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Check_In__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Check_In__c</fullName>
    <externalId>false</externalId>
    <label>Check-In</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
                <fullName>Union</fullName>
                <default>false</default>
                <label>Union</label>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Date_Out_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_Out_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Date_Out__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Date_Out__c)) + &quot;-&quot; + CASE(
  MONTH(Date_Out__c),
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
) + &quot;-&quot; + TEXT(YEAR(Date_Out__c)), CASE(
  MONTH(Date_Out__c),
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
) + &quot;-&quot; + TEXT(DAY(Date_Out__c)) + &quot;-&quot; + TEXT(YEAR(Date_Out__c))), &quot;&quot;)</formula>
    <label>Date Out Conga</label>
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
    <formula>IF(ISBLANK(  Contracted__c  ), 

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
### Zip_Code__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Zip_Code__c</fullName>
    <externalId>false</externalId>
    <label>Zip Code</label>
    <length>20</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Days_In_Pending_Client_Choice__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Days_In_Pending_Client_Choice__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISPICKVAL(Status_CC__c, &quot;Pending Client Choice&quot;), DATETIMEVALUE(Today())- DATETIMEVALUE(Pending_Client_Choice_Initial_Timestamp__c), 

IF(NOT(ISBLANK(In_Contracting_Initial_Timestamp__c)), DATETIMEVALUE(In_Contracting_Initial_Timestamp__c)- DATETIMEVALUE(Pending_Client_Choice_Initial_Timestamp__c),

IF(NOT(ISBLANK(Cancelled_Initial_Timestamp__c )), DATETIMEVALUE(Cancelled_Initial_Timestamp__c )- DATETIMEVALUE(Pending_Client_Choice_Initial_Timestamp__c),0)))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Days In Pending Client Choice</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Rate_Symbol_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Symbol_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Bid__r.is_Vendor_European__c, &quot;€&quot;, &quot;$&quot;)</formula>
    <label>Rate Symbol</label>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Property_Chain__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Property_Chain__c</fullName>
    <externalId>false</externalId>
    <label>Property Chain</label>
    <length>100</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tentative_Dates_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tentative_Dates_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Tentative Dates Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Country__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Country__c</fullName>
    <externalId>false</externalId>
    <label>Country</label>
    <length>100</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Venue</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Housing</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Which_properties_where_in_negotiation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Which_properties_where_in_negotiation__c</fullName>
    <externalId>false</externalId>
    <label>Which properties/where in negotiation</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Days_In_Pending_Client_Signature__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Days_In_Pending_Client_Signature__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISPICKVAL(Status_CC__c, &quot;Pending Client Signature&quot;), DATETIMEVALUE(Today())- DATETIMEVALUE(Pending_Client_Signature_Timestamp__c),

IF(NOT(ISBLANK(Contracted_Initial_Timestamp__c)), DATETIMEVALUE(Contracted_Initial_Timestamp__c)- DATETIMEVALUE(Pending_Client_Signature_Timestamp__c),

IF(NOT(ISBLANK(Pending_Hotel_Counter_Initial_Timestamp__c)), DATETIMEVALUE(Pending_Hotel_Counter_Initial_Timestamp__c)- DATETIMEVALUE(Pending_Client_Signature_Timestamp__c),0)))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Days In Pending Client Signature</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Group_Block_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Group_Block_Status__c</fullName>
    <defaultValue>true</defaultValue>
    <externalId>false</externalId>
    <label>Group Block Status</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Contracting_Back__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Back__c</fullName>
    <externalId>false</externalId>
    <label>Contracting (Back)</label>
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Unit__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Unit__c</fullName>
    <externalId>false</externalId>
    <label>Unit</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Team__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Team__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Team</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Housing (Team)</relationshipLabel>
    <relationshipName>Teams</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Commission_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Type__c</fullName>
    <externalId>false</externalId>
    <label>Commission Type</label>
    <length>10</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Dates_of_travel__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dates_of_travel__c</fullName>
    <externalId>false</externalId>
    <label>Dates of travel</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### In_Contracting_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>In_Contracting_Days__c</fullName>
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
### Rate_Period__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Period__c</fullName>
    <externalId>false</externalId>
    <label>Rate Period</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Per Day</fullName>
                <default>false</default>
                <label>Per Day</label>
            </value>
            <value>
                <fullName>Per Hour</fullName>
                <default>false</default>
                <label>Per Hour</label>
            </value>
            <value>
                <fullName>Per Month</fullName>
                <default>false</default>
                <label>Per Month</label>
            </value>
            <value>
                <fullName>Per Night</fullName>
                <default>false</default>
                <label>Per Night</label>
            </value>
            <value>
                <fullName>Per Stay</fullName>
                <default>false</default>
                <label>Per Stay</label>
            </value>
            <value>
                <fullName>Per Week</fullName>
                <default>false</default>
                <label>Per Week</label>
            </value>
            <value>
                <fullName>Per Year</fullName>
                <default>false</default>
                <label>Per Year</label>
            </value>
            <value>
                <fullName>Quarterly</fullName>
                <default>false</default>
                <label>Quarterly</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### How_many_rooms_are_needed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>How_many_rooms_are_needed__c</fullName>
    <externalId>false</externalId>
    <label>How many rooms are needed?</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Check_Out__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Check_Out__c</fullName>
    <externalId>false</externalId>
    <label>Check-Out</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>CAMI</fullName>
                <default>false</default>
                <label>CAMI</label>
            </value>
            <value>
                <fullName>Union Tours</fullName>
                <default>false</default>
                <label>Union Tours</label>
            </value>
            <value>
                <fullName>SET Tours</fullName>
                <default>false</default>
                <label>SET Tours</label>
            </value>
            <value>
                <fullName>Non Union Tours (Incidentals Guaranteed)</fullName>
                <default>false</default>
                <label>Non Union Tours (Incidentals Guaranteed)</label>
            </value>
            <value>
                <fullName>Non Union Tours (incidentals OFF)</fullName>
                <default>false</default>
                <label>Non Union Tours (incidentals OFF)</label>
            </value>
            <value>
                <fullName>Different Credit Card at Check In</fullName>
                <default>false</default>
                <label>Different Credit Card at Check In</label>
            </value>
            <value>
                <fullName>Film (Direct Bill)</fullName>
                <default>false</default>
                <label>Film (Direct Bill)</label>
            </value>
            <value>
                <fullName>Film (Master Account)</fullName>
                <default>false</default>
                <label>Film (Master Account)</label>
            </value>
            <value>
                <fullName>RRE</fullName>
                <default>false</default>
                <label>RRE</label>
            </value>
            <value>
                <fullName>IPO</fullName>
                <default>false</default>
                <label>IPO</label>
            </value>
            <value>
                <fullName>Sports</fullName>
                <default>false</default>
                <label>Sports</label>
            </value>
            <value>
                <fullName>Sports Billing Info</fullName>
                <default>false</default>
                <label>Sports Billing Info</label>
            </value>
            <value>
                <fullName>TBD1</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>TBD1</label>
            </value>
            <value>
                <fullName>TBD2</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>TBD2</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Conf_s_Sent_to_Client_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Conf_s_Sent_to_Client_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Conf #s Sent to Client Most Recent</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### is_Vendor_European__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>is_Vendor_European__c</fullName>
    <externalId>false</externalId>
    <formula>OR(CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Albania&quot;), 
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Germany&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Andorra&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Armenia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Austria&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Azerbaijan&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Belgium&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Belarus&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Bosnia and Herzegovina&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Bulgaria&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Cyprus&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Holy See (Vatican City State)&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Croatia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Denmark&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Slovakia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Slovenia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Spain&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Estonia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Finland&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;France&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Georgia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Greece&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Hungary&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Ireland&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Iceland&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Italy&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Kazakhstan&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Latvia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Liechtenstein&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Lithuania&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Luxembourg&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Macedonia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Malta&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Moldova&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Monaco&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Montenegro&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Norway&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Netherlands&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Poland&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Portugal&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;United Kingdom&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Czech Republic&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Romania&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Russia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;San Marino&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Serbia&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Sweden&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Switzerland&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Turkey&quot;),
	CONTAINS(Vendor_lookup__r.ShippingCountry, &quot;Ukraine&quot;)
)</formula>
    <label>is Vendor European</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Date_Out_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_Out_Text__c</fullName>
    <externalId>false</externalId>
    <label>Date Out Text</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Sales_Housing__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sales_Housing__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Sales Housing</label>
    <lookupFilter>
        <active>false</active>
        <filterItems>
            <field>Housing__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Sales Housing</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Room Rates &amp; Ops</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Room_Types_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Types_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Units__c), TEXT(Units__c) + &quot; - &quot;, &quot;&quot;) + IF(!ISPICKVAL(Unit_Type__c, &quot;&quot;), TEXT(Unit_Type__c) + &quot; &quot;, &quot;&quot;) + IF(!ISNULL(Special_Notes__c), &quot;(&quot; + Special_Notes__c + &quot;)&quot;, &quot;&quot;) + IF(!ISNULL(Rate__c), BR() + &quot;Rate: &quot; + Rate_Symbol_Conga__c + Text(Rate__c) + &quot; + tax&quot;, &quot;&quot;)</formula>
    <label>Room Types Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Unit_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Unit_Type__c</fullName>
    <externalId>false</externalId>
    <label>Unit Type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>1-Bedroom</fullName>
                <default>false</default>
                <label>1-Bedroom</label>
            </value>
            <value>
                <fullName>1-Bedroom w/Den</fullName>
                <default>false</default>
                <label>1-Bedroom w/Den</label>
            </value>
            <value>
                <fullName>2-Bedroom / 1-Bath</fullName>
                <default>false</default>
                <label>2-Bedroom / 1-Bath</label>
            </value>
            <value>
                <fullName>2-Bedroom / 2-Bath</fullName>
                <default>false</default>
                <label>2-Bedroom / 2-Bath</label>
            </value>
            <value>
                <fullName>3-Bedroom</fullName>
                <default>false</default>
                <label>3-Bedroom</label>
            </value>
            <value>
                <fullName>4-Bedroom</fullName>
                <default>false</default>
                <label>4-Bedroom</label>
            </value>
            <value>
                <fullName>5-Bedroom</fullName>
                <default>false</default>
                <label>5-Bedroom</label>
            </value>
            <value>
                <fullName>Bed &amp; Breakfast</fullName>
                <default>false</default>
                <label>Bed &amp; Breakfast</label>
            </value>
            <value>
                <fullName>Double Room - 2 bed (Twin)</fullName>
                <default>false</default>
                <label>Double Room - 2 bed (Twin)</label>
            </value>
            <value>
                <fullName>Double Room - Double Use</fullName>
                <default>false</default>
                <label>Double Room - Double Use</label>
            </value>
            <value>
                <fullName>Double Room - Single Use</fullName>
                <default>false</default>
                <label>Double Room - Single Use</label>
            </value>
            <value>
                <fullName>Double Rooms / 2 Beds</fullName>
                <default>false</default>
                <label>Double Rooms / 2 Beds</label>
            </value>
            <value>
                <fullName>Junior Suites</fullName>
                <default>false</default>
                <label>Junior Suites</label>
            </value>
            <value>
                <fullName>Lofts</fullName>
                <default>false</default>
                <label>Lofts</label>
            </value>
            <value>
                <fullName>Meeting Room</fullName>
                <default>false</default>
                <label>Meeting Room</label>
            </value>
            <value>
                <fullName>Mixed Rooms</fullName>
                <default>false</default>
                <label>Mixed Rooms</label>
            </value>
            <value>
                <fullName>Mixed Suites</fullName>
                <default>false</default>
                <label>Mixed Suites</label>
            </value>
            <value>
                <fullName>Offices</fullName>
                <default>false</default>
                <label>Offices</label>
            </value>
            <value>
                <fullName>Penthouse Suites</fullName>
                <default>false</default>
                <label>Penthouse Suites</label>
            </value>
            <value>
                <fullName>Single Room - Single Use</fullName>
                <default>false</default>
                <label>Single Room - Single Use</label>
            </value>
            <value>
                <fullName>Single Rooms / 1 Bed</fullName>
                <default>false</default>
                <label>Single Rooms / 1 Bed</label>
            </value>
            <value>
                <fullName>Studios</fullName>
                <default>false</default>
                <label>Studios</label>
            </value>
            <value>
                <fullName>Suites</fullName>
                <default>false</default>
                <label>Suites</label>
            </value>
            <value>
                <fullName>Triples</fullName>
                <default>false</default>
                <label>Triples</label>
            </value>
            <value>
                <fullName>Twin/Twin</fullName>
                <default>false</default>
                <label>Twin/Twin</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Pending_Confirmation_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Confirmation_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Pending Confirmation # Most Recent</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### VenueName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VenueName__c</fullName>
    <externalId>false</externalId>
    <label>VenueName</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Commission_Per_Room__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Per_Room__c</fullName>
    <externalId>false</externalId>
    <label>Commission Per Room</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Itinerary Received</fullName>
                <default>false</default>
                <label>Itinerary Received</label>
            </value>
            <value>
                <fullName>Bid Request Stage</fullName>
                <default>false</default>
                <label>Bid Request Stage</label>
            </value>
            <value>
                <fullName>Pending Client Choice</fullName>
                <default>false</default>
                <label>Pending Client Choice</label>
            </value>
            <value>
                <fullName>In Contracting</fullName>
                <default>false</default>
                <label>In Contracting</label>
            </value>
            <value>
                <fullName>Pending Client Signature</fullName>
                <default>false</default>
                <label>Pending Client Signature</label>
            </value>
            <value>
                <fullName>Contracted</fullName>
                <default>false</default>
                <label>Contracted</label>
            </value>
            <value>
                <fullName>Pending Update</fullName>
                <default>false</default>
                <label>Pending Update</label>
            </value>
            <value>
                <fullName>Pending Hotel Counter</fullName>
                <default>false</default>
                <label>Pending Hotel Counter</label>
            </value>
            <value>
                <fullName>Cancelled</fullName>
                <default>false</default>
                <label>Cancelled</label>
            </value>
            <value>
                <fullName>Deleted</fullName>
                <default>false</default>
                <label>Deleted</label>
            </value>
            <value>
                <fullName>Decision</fullName>
                <default>false</default>
                <label>Decision</label>
            </value>
            <value>
                <fullName>Budgeting</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Budgeting</label>
            </value>
            <value>
                <fullName>Confirmation Numbers Sent to Client</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Confirmation Numbers Sent to Client</label>
            </value>
            <value>
                <fullName>Contracted On Own</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Contracted On Own</label>
            </value>
            <value>
                <fullName>Layoff</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Layoff</label>
            </value>
            <value>
                <fullName>No Rooms Picked-Up</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>No Rooms Picked-Up</label>
            </value>
            <value>
                <fullName>Pending Confirmation Numbers</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Pending Confirmation Numbers</label>
            </value>
            <value>
                <fullName>Presenter Provided</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Presenter Provided</label>
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
            <value>
                <fullName>Tentative Dates</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Tentative Dates</label>
            </value>
            <value>
                <fullName>Travel Dates</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Travel Dates</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Update_RoomTypes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Update_RoomTypes__c</fullName>
    <defaultValue>true</defaultValue>
    <externalId>false</externalId>
    <label>Update RoomTypes</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Budgeting__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budgeting__c</fullName>
    <externalId>false</externalId>
    <label>Budgeting Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Housing_Preference__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Preference__c</fullName>
    <externalId>false</externalId>
    <label>Housing Preference</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Office_Location</valueSetName>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Pending_Confirmation_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Confirmation_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Pending Confirmation # Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Tournament_Additional_Information__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tournament_Additional_Information__c</fullName>
    <externalId>false</externalId>
    <label>Tournament Additional Information</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <relationshipLabel>Housing (City)</relationshipLabel>
    <relationshipName>Housing1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Total_Night_Rev__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Night_Rev__c</fullName>
    <externalId>false</externalId>
    <formula>Total_Nights__c *  Est_Per_Night_Rev__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Total Night Rev</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### IR__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IR__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>IR</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Comps__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Comps__c</fullName>
    <externalId>false</externalId>
    <label>Comps</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Budget_numbers__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budget_numbers__c</fullName>
    <externalId>false</externalId>
    <label>Budget numbers</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Yes_No</valueSetName>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Confirmations__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirmations__c</fullName>
    <externalId>false</externalId>
    <label>Confirmation #(s)</label>
    <length>200</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Proj_Invoice_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Proj_Invoice_Date__c</fullName>
    <externalId>false</externalId>
    <formula>Check_Out__c  + 10</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Proj Invoice Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <relationshipLabel>Housing</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Total_Room_Nights__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Room_Nights__c</fullName>
    <externalId>false</externalId>
    <label>Total # Room Nights</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Pending_client_choice__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_client_choice__c</fullName>
    <externalId>false</externalId>
    <label>Pending client choice</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Coordinator</label>
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
        <active>false</active>
        <booleanFilter>1 OR 2</booleanFilter>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Corporate Housing Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordTypeId</field>
            <operation>equals</operation>
            <value>Hotel Vendor</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Housing (Vendor)</relationshipLabel>
    <relationshipName>Housing1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Layoff_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Layoff_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Layoff Most Recent</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Rate_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Type__c</fullName>
    <externalId>false</externalId>
    <label>Rate Type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Daily</fullName>
                <default>false</default>
                <label>Daily</label>
            </value>
            <value>
                <fullName>Monthly</fullName>
                <default>false</default>
                <label>Monthly</label>
            </value>
            <value>
                <fullName>Nightly</fullName>
                <default>false</default>
                <label>Nightly</label>
            </value>
            <value>
                <fullName>Per Day</fullName>
                <default>false</default>
                <label>Per Day</label>
            </value>
            <value>
                <fullName>Per Month</fullName>
                <default>false</default>
                <label>Per Month</label>
            </value>
            <value>
                <fullName>Per Night</fullName>
                <default>false</default>
                <label>Per Night</label>
            </value>
            <value>
                <fullName>Per Stay</fullName>
                <default>false</default>
                <label>Per Stay</label>
            </value>
            <value>
                <fullName>Weekly</fullName>
                <default>false</default>
                <label>Weekly</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Room_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Type__c</fullName>
    <externalId>false</externalId>
    <label>Room Type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Preferred</fullName>
                <default>false</default>
                <label>Preferred</label>
            </value>
            <value>
                <fullName>Bid</fullName>
                <default>false</default>
                <label>Bid</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Billing_Options_Verbiage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Billing_Options_Verbiage__c</fullName>
    <externalId>false</externalId>
    <label>Billing Options Verbiage</label>
    <length>1000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Layoff_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Layoff_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Layoff Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <label>Invoiced Amount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Trace_Date_Priority__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trace_Date_Priority__c</fullName>
    <externalId>false</externalId>
    <label>Trace Date Priority</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>No Follow up</fullName>
                <default>true</default>
                <label>No Follow up</label>
            </value>
            <value>
                <fullName>Normal Follow up</fullName>
                <default>false</default>
                <label>Normal Follow up</label>
            </value>
            <value>
                <fullName>Urgent Follow Up</fullName>
                <default>false</default>
                <label>Urgent Follow Up</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <relationshipLabel>Room Types</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Venue_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Venue_City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Venue City</label>
    <referenceTo>City__c</referenceTo>
    <relationshipLabel>Housing</relationshipLabel>
    <relationshipName>Housing</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Units__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Units__c</fullName>
    <externalId>false</externalId>
    <label>Units</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Special_Notes_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Special_Notes_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Special Notes NAV</label>
    <length>1000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### No_Rooms_Picked_Up_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Rooms_Picked_Up_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>No Rooms Picked-Up Most Recent</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Housing (Tournament)</relationshipLabel>
    <relationshipName>Housing1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Projected_Room_nights__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Projected_Room_nights__c</fullName>
    <externalId>false</externalId>
    <label>Projected # Room nights</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Travel_Dates_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Travel_Dates_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Travel Dates Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Booking_Link__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Booking_Link__c</fullName>
    <externalId>false</externalId>
    <label>Booking Link</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Invoiced_Units__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoiced_Units__c</fullName>
    <externalId>false</externalId>
    <label>Invoiced Units</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Travel_Dates_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Travel_Dates_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Travel Dates Most Recent</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate__c</fullName>
    <externalId>false</externalId>
    <label>Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### No_Rooms_Picked_Up_Initial_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Rooms_Picked_Up_Initial_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>No Rooms Picked-Up Initial Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Contract_Resent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Resent__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Contract Resent</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Distance_to_Venue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Distance_to_Venue__c</fullName>
    <externalId>false</externalId>
    <label>Distance to Venue</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Walking (0.5 miles)</fullName>
                <default>false</default>
                <label>Walking (0.5 miles)</label>
            </value>
            <value>
                <fullName>0.5 -  5 Miles</fullName>
                <default>false</default>
                <label>0.5 -  5 Miles</label>
            </value>
            <value>
                <fullName>5 - 10 Miles</fullName>
                <default>false</default>
                <label>5 - 10 Miles</label>
            </value>
            <value>
                <fullName>10+ Miles</fullName>
                <default>false</default>
                <label>10+ Miles</label>
            </value>
            <value>
                <fullName>Walking (0.5 kms)</fullName>
                <default>false</default>
                <label>Walking (0.5 kms)</label>
            </value>
            <value>
                <fullName>0.5 - 5 kms</fullName>
                <default>false</default>
                <label>0.5 - 5 kms</label>
            </value>
            <value>
                <fullName>5 - 10 kms</fullName>
                <default>false</default>
                <label>5 - 10 kms</label>
            </value>
            <value>
                <fullName>10+ kms</fullName>
                <default>false</default>
                <label>10+ kms</label>
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
    <description>Business days housing record stays in a status.</description>
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
### Considerations_important__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Considerations_important__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Considerations/concessions important to them</inlineHelpText>
    <label>Considerations important</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Status_Note__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Note__c</fullName>
    <externalId>false</externalId>
    <label>Status Note</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Coordinator_Back__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Coordinator_Back__c</fullName>
    <externalId>false</externalId>
    <label>Coordinator (Back)</label>
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Date_In_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_In_Text__c</fullName>
    <externalId>false</externalId>
    <label>Date In Text</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tentative_Dates_Most_Recent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tentative_Dates_Most_Recent__c</fullName>
    <externalId>false</externalId>
    <label>Tentative Dates Most Recent</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
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
### Units_Pickup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Units_Pickup__c</fullName>
    <externalId>false</externalId>
    <formula>Invoiced_Units__c  / Total_Nights__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Units Pickup</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Date_Out__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_Out__c</fullName>
    <externalId>false</externalId>
    <label>Date Out</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### New_Journal_RecordType__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>New_Journal_RecordType__c</fullName>
    <externalId>false</externalId>
    <label>New Journal RecordType</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### isEvent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isEvent__c</fullName>
    <externalId>false</externalId>
    <formula>IF( OR(Production_CC__r.RecordType.DeveloperName = &apos;Collegiate_and_Tournament&apos;,  ISPICKVAL(Production_CC__r.Production_type__c,&apos;Union&apos;)),  true, false)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>isEvent</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Locked__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Locked__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Locked</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Bids__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bids__c</fullName>
    <externalId>false</externalId>
    <label>Bids</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Contracted_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted_Days__c</fullName>
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
### Brand_Preference__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Brand_Preference__c</fullName>
    <externalId>false</externalId>
    <label>Brand Preference</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Marriott</fullName>
                <default>false</default>
                <label>Marriott</label>
            </value>
            <value>
                <fullName>Hilton Hotel and Resorts</fullName>
                <default>false</default>
                <label>Hilton Hotel and Resorts</label>
            </value>
            <value>
                <fullName>Hyatt Hotel Corporation</fullName>
                <default>false</default>
                <label>Hyatt Hotel Corporation</label>
            </value>
            <value>
                <fullName>InterContinental Hotels Group (IHG)</fullName>
                <default>false</default>
                <label>InterContinental Hotels Group (IHG)</label>
            </value>
            <value>
                <fullName>Wyndham Hotels &amp; Resorts</fullName>
                <default>false</default>
                <label>Wyndham Hotels &amp; Resorts</label>
            </value>
            <value>
                <fullName>Best Western</fullName>
                <default>false</default>
                <label>Best Western</label>
            </value>
            <value>
                <fullName>Choice Hotels</fullName>
                <default>false</default>
                <label>Choice Hotels</label>
            </value>
            <value>
                <fullName>AccorHotels</fullName>
                <default>false</default>
                <label>AccorHotels</label>
            </value>
            <value>
                <fullName>Extended Stay America</fullName>
                <default>false</default>
                <label>Extended Stay America</label>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Total_Commission__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Commission__c</fullName>
    <externalId>false</externalId>
    <label>Total Commission</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description__c</fullName>
    <externalId>false</externalId>
    <label>Description</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Housing Stay</fullName>
                <default>false</default>
                <label>Housing Stay</label>
            </value>
            <value>
                <fullName>Individual Reservation</fullName>
                <default>false</default>
                <label>Individual Reservation</label>
            </value>
            <value>
                <fullName>Layoff</fullName>
                <default>false</default>
                <label>Layoff</label>
            </value>
            <value>
                <fullName>Travel Day</fullName>
                <default>false</default>
                <label>Travel Day</label>
            </value>
            <value>
                <fullName>Venue and City are TBD</fullName>
                <default>false</default>
                <label>Venue and City are TBD</label>
            </value>
            <value>
                <fullName>Venue is TBD</fullName>
                <default>false</default>
                <label>Venue is TBD</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Booked_Discount__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Booked_Discount__c</fullName>
    <externalId>false</externalId>
    <formula>(VALUE(Bid__r.OLR__c) - Rate__c)/value(Bid__r.OLR__c)</formula>
    <label>Booked Discount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Hotel_Class__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Hotel_Class__c</fullName>
    <externalId>false</externalId>
    <label>Hotel Class</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Limited</fullName>
                <default>false</default>
                <label>Limited</label>
            </value>
            <value>
                <fullName>Full Service</fullName>
                <default>false</default>
                <label>Full Service</label>
            </value>
            <value>
                <fullName>Select Service</fullName>
                <default>false</default>
                <label>Select Service</label>
            </value>
            <value>
                <fullName>Extended Stay</fullName>
                <default>false</default>
                <label>Extended Stay</label>
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
### Vendor__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor__c</fullName>
    <externalId>false</externalId>
    <label>Vendor</label>
    <length>200</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <inlineHelpText>Turn over relationship for best rate? If no why?</inlineHelpText>
    <label>Turn over relationship for best rate?</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Stay_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Stay_Type__c</fullName>
    <externalId>false</externalId>
    <label>Stay Type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Housing</fullName>
                <default>false</default>
                <label>Housing</label>
            </value>
            <value>
                <fullName>Corp Housing</fullName>
                <default>false</default>
                <label>Corp Housing</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Locations__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Locations__c</fullName>
    <externalId>false</externalId>
    <label>Locations</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Bid_Request_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Request_Days__c</fullName>
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

0 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,2,2,3,3,4,4,5,5,5,6,5,1), 
  1 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,2,2,3,3,4,4,4,5,4,6,5,1), 
  2 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,2,2,3,3,3,4,3,5,4,6,5,1), 
  3 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,2,2,2,3,2,4,3,5,4,6,5,1), 
  4 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,1,2,1,3,2,4,3,5,4,6,5,1), 
  5 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,0,2,1,3,2,4,3,5,4,6,5,0), 
  6 , CASE( MOD( Bid_Request__c -  Date_Entered__c ,7),1,1,2,2,3,3,4,4,5,5,6,5,0), 
 999) 
  + 
  (FLOOR(( Bid_Request__c -  Date_Entered__c )/7)*5))</formula>
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
### Room_Nights_x_Rate_Pickup_Report__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Nights_x_Rate_Pickup_Report__c</fullName>
    <externalId>false</externalId>
    <formula>(Total_Room_Nights__c - Comps__c) * Rate__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Room Nights x Rate Pickup Report</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Est_Per_Night_Rev__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Est_Per_Night_Rev__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(Market_Type__c, 
&quot;Family Entertainment&quot;, 7, 
&quot;Film&quot;, 4, 
&quot;Fine Arts&quot;, 10, 
&quot;Miscellaneous&quot;, 6, 
&quot;Music&quot;, 10,
&quot;Sports&quot;, 8, 
&quot;Theatrical&quot;, 5, 
&quot;TV&quot;, 10, 
NULL)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Est. Per Night Rev</label>
    <precision>18</precision>
    <required>false</required>
    <scale>1</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Contracting_Requirements__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Requirements__c</fullName>
    <externalId>false</externalId>
    <label>Contracting Requirements</label>
    <length>6000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>10</visibleLines>
</CustomField>
```
### NAV_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>NAV_ID__c</fullName>
    <caseSensitive>false</caseSensitive>
    <externalId>true</externalId>
    <label>NAV ID</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>true</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### New_Journal_Entry__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>New_Journal_Entry__c</fullName>
    <externalId>false</externalId>
    <label>New Journal Entry</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tournament_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tournament_Name__c</fullName>
    <externalId>false</externalId>
    <label>Tournament Name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### isRoomTypeHotelHousingStay__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isRoomTypeHotelHousingStay__c</fullName>
    <externalId>false</externalId>
    <formula>IF( Bid__r.Housing__r.RecordType.DeveloperName=&apos;Hotel_Housing&apos;,true,false)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>isRoomTypeHotelHousingStay</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Email_Body_Bid_Request_PDF__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Body_Bid_Request_PDF__c</fullName>
    <externalId>false</externalId>
    <label>Email Body Bid Request PDF</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```

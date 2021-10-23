---
layout: default
title: Air__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Air__c
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
### Flight_Duration_Mins__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Flight_Duration_Mins__c</fullName>
    <externalId>false</externalId>
    <label>Flight Duration Mins</label>
    <precision>2</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Air_Charter_Trip_Contents__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Charter_Trip_Contents__c</fullName>
    <externalId>false</externalId>
    <label>Air Charter Trip Contents</label>
    <length>255</length>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Segment_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Segment_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Segment Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Charter_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Charter_Type__c</fullName>
    <externalId>false</externalId>
    <label>Charter Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Light Jets</fullName>
                <default>false</default>
                <label>Light Jets</label>
            </value>
            <value>
                <fullName>Turbo Prop Planes</fullName>
                <default>false</default>
                <label>Turbo Prop Planes</label>
            </value>
            <value>
                <fullName>Mid-Size Jets</fullName>
                <default>false</default>
                <label>Mid-Size Jets</label>
            </value>
            <value>
                <fullName>Super Mid-Size Jets</fullName>
                <default>false</default>
                <label>Super Mid-Size Jets</label>
            </value>
            <value>
                <fullName>Large Cabin Jets or Heavy Jets</fullName>
                <default>false</default>
                <label>Large Cabin Jets or Heavy Jets</label>
            </value>
            <value>
                <fullName>Regional Jet</fullName>
                <default>false</default>
                <label>Regional Jet</label>
            </value>
            <value>
                <fullName>Airline Air Charter</fullName>
                <default>false</default>
                <label>Airline Air Charter</label>
            </value>
            <value>
                <fullName>VIP Air Charter</fullName>
                <default>false</default>
                <label>VIP Air Charter</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Arrival_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arrival_Date__c</fullName>
    <externalId>false</externalId>
    <label>Arrival Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### GCQ_Deviation_Travel_Information_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCQ_Deviation_Travel_Information_Conga__c</fullName>
    <externalId>false</externalId>
    <label>GCQ Deviation Travel Information</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### What_length_of_check_in_for_this_airport__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>What_length_of_check_in_for_this_airport__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>What length of check in is the airline advising for this airport?</inlineHelpText>
    <label>What length of check in for this airport</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>1.5Hrs</fullName>
                <default>false</default>
                <label>1.5Hrs</label>
            </value>
            <value>
                <fullName>2Hrs</fullName>
                <default>false</default>
                <label>2Hrs</label>
            </value>
            <value>
                <fullName>3Hrs</fullName>
                <default>false</default>
                <label>3Hrs</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Flight_No__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Flight_No__c</fullName>
    <externalId>false</externalId>
    <label>Flight No</label>
    <length>15</length>
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
### Return_Date_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Return_Date_Text__c</fullName>
    <externalId>false</externalId>
    <label>Return Date Text</label>
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
### Preferred_Carrier__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Preferred_Carrier__c</fullName>
    <externalId>false</externalId>
    <label>Preferred Carrier</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Return_Departure_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Return_Departure_City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Return Departure City</label>
    <referenceTo>Airport__c</referenceTo>
    <relationshipLabel>Air (Return Departure City)</relationshipLabel>
    <relationshipName>Air2</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Air_Preferences__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Preferences__c</fullName>
    <externalId>false</externalId>
    <label>Air Preferences</label>
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
### Decision_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Decision_Due__c</fullName>
    <externalId>false</externalId>
    <label>Decision Due</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Class__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Class__c</fullName>
    <externalId>false</externalId>
    <label>Class</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Economy</fullName>
                <default>false</default>
                <label>Economy</label>
            </value>
            <value>
                <fullName>First class</fullName>
                <default>false</default>
                <label>First class</label>
            </value>
            <value>
                <fullName>Business class</fullName>
                <default>false</default>
                <label>Business class</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
### Positioning_from_time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Positioning_from_time__c</fullName>
    <externalId>false</externalId>
    <label>Positioning from &amp; time</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipName>Air</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Baggage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Baggage__c</fullName>
    <externalId>false</externalId>
    <label>Baggage</label>
    <length>200</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Decision_Due_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Decision_Due_Date__c</fullName>
    <externalId>false</externalId>
    <label>Decision Due Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Does_the_airline_have_the_ticket_number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Does_the_airline_have_the_ticket_number__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Does the airline have the ticket numbers and dates of birth?</inlineHelpText>
    <label>Does the airline have the ticket number?</label>
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
### Status_Change_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Change_Date__c</fullName>
    <description>Field used to capture the business days each Air trip record stays in a status.</description>
    <externalId>false</externalId>
    <label>Status - Change Date</label>
    <required>false</required>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Preferred_Airline__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Preferred_Airline__c</fullName>
    <externalId>false</externalId>
    <label>Preferred Airline</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>American Airlines</fullName>
                <default>false</default>
                <label>American Airlines</label>
            </value>
            <value>
                <fullName>Delta Airlines</fullName>
                <default>false</default>
                <label>Delta Airlines</label>
            </value>
            <value>
                <fullName>JetBlue Airways</fullName>
                <default>false</default>
                <label>JetBlue Airways</label>
            </value>
            <value>
                <fullName>Other</fullName>
                <default>false</default>
                <label>Other</label>
            </value>
            <value>
                <fullName>Southwest Airlines</fullName>
                <default>false</default>
                <label>Southwest Airlines</label>
            </value>
            <value>
                <fullName>United Airlines</fullName>
                <default>false</default>
                <label>United Airlines</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
### Additional_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Additional_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Additional Notes</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
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
### Checked_Back_Cut_Off_Hours__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Checked_Back_Cut_Off_Hours__c</fullName>
    <description>What is checked bag cut off hours?</description>
    <externalId>false</externalId>
    <label>Checked Back Cut Off Hours</label>
    <precision>2</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Return_Arrival_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Return_Arrival_City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Return Arrival City</label>
    <referenceTo>Airport__c</referenceTo>
    <relationshipLabel>Air (Return Arrival City)</relationshipLabel>
    <relationshipName>Air3</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Decision_Due_Date_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Decision_Due_Date_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Decision Due Date - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Past_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Past_Due__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Today()&gt; Deadline_Date__c &amp;&amp; (ISPICKVAL(  Status__c  , &quot;Itinerary Received&quot;) || ISPICKVAL(Status__c  , &quot;Bid Request Stage&quot;) || ISPICKVAL(Status__c  , &quot;Send to Client&quot;) || ISPICKVAL(Status__c  , &quot;Rework&quot;)), true, false)</formula>
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
### Dep_Time_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dep_Time_Text__c</fullName>
    <externalId>false</externalId>
    <label>Dep Time Text</label>
    <length>255</length>
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
### Dep_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dep_City__c</fullName>
    <externalId>false</externalId>
    <label>Dep City</label>
    <length>5</length>
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
### Are_the_names_still_the_same__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Are_the_names_still_the_same__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Are the names, dates, times, flight numbers, cities and seats still the same?</inlineHelpText>
    <label>Are the names still the same?</label>
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
### Arrival_Date_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arrival_Date_Text__c</fullName>
    <externalId>false</externalId>
    <label>Arrival Date Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Air_Internal_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Internal_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Air Internal Notes</label>
    <length>5000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Air_Charter__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Charter__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Air Charter</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
            <value>
                <fullName>General</fullName>
                <default>false</default>
                <label>General</label>
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
### Flight_Duration_hrs__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Flight_Duration_hrs__c</fullName>
    <externalId>false</externalId>
    <label>Flight Duration hrs</label>
    <precision>2</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Arr_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arr_Time__c</fullName>
    <externalId>false</externalId>
    <label>Arr Time</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
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
                <fullName>Sports</fullName>
                <default>false</default>
                <label>Sports</label>
            </value>
            <value>
                <fullName>Event</fullName>
                <default>false</default>
                <label>Event</label>
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
                <fullName>TV</fullName>
                <default>false</default>
                <label>TV</label>
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
### Number_of_Seats__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Number_of_Seats__c</fullName>
    <externalId>false</externalId>
    <label># of Seats</label>
    <precision>4</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Air_Deviation_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Deviation_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Air Deviation Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Air__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Air Deviation Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Air Travel Information</relationshipLabel>
    <relationshipName>AirDeviationTravels</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Turn_over_relatiionship_for_best_rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Turn_over_relatiionship_for_best_rate__c</fullName>
    <externalId>false</externalId>
    <label>Turn over relatiionship for best rate?</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Departure_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Departure_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Departure_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Departure_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Departure_Date__c)), CASE(
  MONTH(Departure_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Departure_Date__c)) + &quot;-&quot; + TEXT(YEAR(Departure_Date__c))), &quot;&quot;)</formula>
    <label>Departure Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Origin_destination__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Origin_destination__c</fullName>
    <externalId>false</externalId>
    <label>Origin destination</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### RT_Dep_Arr__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>RT_Dep_Arr__c</fullName>
    <externalId>false</externalId>
    <formula>IF(OR(Return_Departure_City__r.Airport_Code__c &lt;&gt; NULL,Return_Arrival_City__r.Airport_Code__c &lt;&gt; NULL),Return_Departure_City__r.Airport_Code__c &amp; &quot;/&quot; &amp; Return_Arrival_City__r.Airport_Code__c,&quot;&quot;)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>RT Dep/Arr</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Air_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Type__c</fullName>
    <externalId>false</externalId>
    <label>Air Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Commercial</fullName>
                <default>false</default>
                <label>Commercial</label>
            </value>
            <value>
                <fullName>Charted</fullName>
                <default>false</default>
                <label>Charted</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Departure_Date_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_Date_Text__c</fullName>
    <externalId>false</externalId>
    <label>Departure Date Text</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Gate_Terminal_Info__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Gate_Terminal_Info__c</fullName>
    <externalId>false</externalId>
    <label>Gate/Terminal Info?</label>
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
### Departure_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Departure City</label>
    <referenceTo>Airport__c</referenceTo>
    <relationshipLabel>Air</relationshipLabel>
    <relationshipName>Air</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Arr_Time_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arr_Time_Text__c</fullName>
    <externalId>false</externalId>
    <label>Arr Time Text</label>
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
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>One Way</fullName>
                <default>false</default>
                <label>One Way</label>
            </value>
            <value>
                <fullName>Round Trip</fullName>
                <default>false</default>
                <label>Round Trip</label>
            </value>
            <value>
                <fullName>Multi-City</fullName>
                <default>false</default>
                <label>Multi-City</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Preferred_Plane_size__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Preferred_Plane_size__c</fullName>
    <externalId>false</externalId>
    <label>Preferred Plane size</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Operated_by__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Operated_by__c</fullName>
    <externalId>false</externalId>
    <label>Operated by</label>
    <length>255</length>
    <required>false</required>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Travel_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Travel_Date_Conga__c</fullName>
    <description>Used in Conga Preview options to populate the actual departure date of the itinerary segments.</description>
    <externalId>false</externalId>
    <label>Travel Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Bid_Aircraft__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Aircraft__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Bid</label>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Air (Bid)</relationshipLabel>
    <relationshipName>BidAircrafts</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Arrival_Time_Start__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arrival_Time_Start__c</fullName>
    <externalId>false</externalId>
    <label>Arrival Time Start</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### Decision_Due_Date_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Decision_Due_Date_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Decision Due Date - Last Send Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Form_Decision_Due_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Decision_Due_Date__c</fullName>
    <externalId>false</externalId>
    <label>Form Decision Due Date</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Confirm_you_have_given_the_carrier_name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Confirm_you_have_given_the_carrier_name__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <inlineHelpText>Confirm you have given the carrier the group leaders name and phone number. Make sure they have Road Rebel&apos;s info as well.</inlineHelpText>
    <label>Confirm you have given the carrier name</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Arrival_Time_End__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arrival_Time_End__c</fullName>
    <externalId>false</externalId>
    <label>Arrival Time End</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### Flight_tracking__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Flight_tracking__c</fullName>
    <externalId>false</externalId>
    <label>Flight tracking?</label>
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
### Cargo_capacity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cargo_capacity__c</fullName>
    <externalId>false</externalId>
    <label>Cargo capacity</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### Segment_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Segment_Type__c</fullName>
    <externalId>false</externalId>
    <label>Segment Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Standard</fullName>
                <default>false</default>
                <label>Standard</label>
            </value>
            <value>
                <fullName>Deviation</fullName>
                <default>false</default>
                <label>Deviation</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
### GCQ_Main_Travel_Information_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCQ_Main_Travel_Information_Conga__c</fullName>
    <externalId>false</externalId>
    <label>GCQ Main Travel Information</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Date_options_are_needed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_options_are_needed__c</fullName>
    <externalId>false</externalId>
    <label>Date options are needed</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Vendor_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Text__c</fullName>
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
### DepCityName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>DepCityName__c</fullName>
    <externalId>false</externalId>
    <label>DepCityName</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### Checked_Back_Cut_Off_Minutes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Checked_Back_Cut_Off_Minutes__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>What is checked bag cut off minutes?</inlineHelpText>
    <label>Checked Back Cut Off Minutes</label>
    <precision>2</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
### Departure_Time_Start__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_Time_Start__c</fullName>
    <externalId>false</externalId>
    <label>Departure Time Start</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
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
### Air_Trip_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Trip_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Air Trip Details</label>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Air Segments</relationshipLabel>
    <relationshipName>Air_Segments</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Deviation_Order_Formula_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deviation_Order_Formula_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>Text(Deviation_Order_Conga__c)</formula>
    <label>Deviation Order Formula</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Coordinator</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Bag_Fees_and_Policies__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bag_Fees_and_Policies__c</fullName>
    <externalId>false</externalId>
    <label>Bag Fees and Policies</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>4</visibleLines>
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
### Dep_Arr__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dep_Arr__c</fullName>
    <externalId>false</externalId>
    <formula>IF(OR(Departure_City__r.Airport_Code__c &lt;&gt; NULL,Arrival_City__r.Airport_Code__c &lt;&gt; NULL),Departure_City__r.Airport_Code__c &amp; &quot;/&quot; &amp; Arrival_City__r.Airport_Code__c,&quot;&quot;)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Dep/Arr</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Dep_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dep_Time__c</fullName>
    <externalId>false</externalId>
    <label>Dep Time</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### Air_Crafts_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Crafts_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Air Crafts Details</label>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Air (Air Crafts Details)</relationshipLabel>
    <relationshipName>AirCrafts</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Have_any_special_seats_been_added__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Have_any_special_seats_been_added__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Have any special seats assignments, meal requirements, pets traveling, and/or known traveler/frequent flyer numbers been added?</inlineHelpText>
    <label>Have any special seats been added?</label>
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
### Aircraft_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Aircraft_Type__c</fullName>
    <externalId>false</externalId>
    <label>Aircraft Type</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Equip_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Equip_Type__c</fullName>
    <externalId>false</externalId>
    <label>Equip. Type</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Air</relationshipLabel>
    <relationshipName>Air</relationshipName>
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
### Departure_Arrival_info__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_Arrival_info__c</fullName>
    <externalId>false</externalId>
    <label>Departure/Arrival info?</label>
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
### Departure_Time_End__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_Time_End__c</fullName>
    <externalId>false</externalId>
    <label>Departure Time End</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
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
### Bid_Deviation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Deviation__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <description>Bid for Air Deviation Details</description>
    <externalId>false</externalId>
    <label>Bid</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Bid__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Air Bid</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Air Deviations</relationshipLabel>
    <relationshipName>AirDeviations</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Order__c</fullName>
    <externalId>false</externalId>
    <label>Order #</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
### Arrival_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arrival_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Arrival_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Arrival_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Arrival_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Arrival_Date__c)), CASE(
  MONTH(Arrival_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Arrival_Date__c)) + &quot;-&quot; + TEXT(YEAR(Arrival_Date__c))), &quot;&quot;)</formula>
    <label>Arrival Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### PAX__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PAX__c</fullName>
    <externalId>false</externalId>
    <label>#PAX</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
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
### Arrival_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arrival_City__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Arrival City</label>
    <referenceTo>Airport__c</referenceTo>
    <relationshipLabel>Air (Arrival City)</relationshipLabel>
    <relationshipName>Air1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Bid_Itinerary__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Itinerary__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <description>Bid for Air Itinerary Details</description>
    <externalId>false</externalId>
    <label>Bid</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Bid__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Air Bid</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Air Itineraries</relationshipLabel>
    <relationshipName>AirItineraries</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Verify_tail_number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Verify_tail_number__c</fullName>
    <externalId>false</externalId>
    <label>Verify tail number?</label>
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
### Agent_Spoken_To_Gcq__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Agent_Spoken_To_Gcq__c</fullName>
    <externalId>false</externalId>
    <label>Agent Spoken To</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Return_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Return_Date__c</fullName>
    <externalId>false</externalId>
    <label>Return Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Status_Business_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_Business_Days__c</fullName>
    <description>Business days Air Trip record stays in a status.</description>
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
### of_Seats__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>of_Seats__c</fullName>
    <externalId>false</externalId>
    <label># of Seats</label>
    <precision>5</precision>
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
### Contact_Gcq__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contact_Gcq__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contact</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Gcqs</relationshipLabel>
    <relationshipName>Gcqs</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### ArrCityName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ArrCityName__c</fullName>
    <externalId>false</externalId>
    <label>ArrCityName</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Seat_pitch__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Seat_pitch__c</fullName>
    <externalId>false</externalId>
    <label>Seat pitch</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Deviation_Order_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deviation_Order_Conga__c</fullName>
    <description>Used in Conga to populate the order of the deviation segments.</description>
    <externalId>false</externalId>
    <label>Deviation Order</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
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
### Trip_ID_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_ID_Text__c</fullName>
    <externalId>false</externalId>
    <label>Trip ID Text</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Additional_Fees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Additional_Fees__c</fullName>
    <externalId>false</externalId>
    <label>Additional Fees</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
### Service_Fees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Fees__c</fullName>
    <externalId>false</externalId>
    <label>Service Fees</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### economy_seats__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>economy_seats__c</fullName>
    <externalId>false</externalId>
    <label># economy seats</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
### Return_Time_Start__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Return_Time_Start__c</fullName>
    <externalId>false</externalId>
    <label>Return Time Start</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description__c</fullName>
    <externalId>false</externalId>
    <label>Description</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Arr_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Arr_City__c</fullName>
    <externalId>false</externalId>
    <label>Arr City</label>
    <length>5</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Other_considerations_important__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Other_considerations_important__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Other considerations/concessions important</inlineHelpText>
    <label>Other considerations important</label>
    <length>250</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Departure_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Departure_Date__c</fullName>
    <externalId>false</externalId>
    <label>Departure Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
                <fullName>Team</fullName>
                <default>false</default>
                <label>Team</label>
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
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Air (Vendor)</relationshipLabel>
    <relationshipName>Air1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Air_Itinerary_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Itinerary_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Air Itinerary Details</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Air__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Air Itinerary Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Air Travel Information</relationshipLabel>
    <relationshipName>AirItineraryTravels</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Airline__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Airline__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Airline</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Air (Airline)</relationshipLabel>
    <relationshipName>AircraftAirline</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Production_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Text__c</fullName>
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
### Nav_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Nav_ID__c</fullName>
    <caseSensitive>false</caseSensitive>
    <externalId>true</externalId>
    <label>Nav ID</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>true</unique>
</CustomField>
```
### Decision_Due_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Decision_Due_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Decision_Due_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Decision_Due_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Decision_Due_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Decision_Due_Date__c)), CASE(
  MONTH(Decision_Due_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Decision_Due_Date__c)) + &quot;-&quot; + TEXT(YEAR(Decision_Due_Date__c))), &quot;&quot;)</formula>
    <label>Decision Due Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### of_Bids__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>of_Bids__c</fullName>
    <externalId>false</externalId>
    <label># of Bids</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Final_Travel_Information_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Travel_Information_Conga__c</fullName>
    <externalId>false</externalId>
    <label>Final Travel Information</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Travel_Information_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Travel_Information_Conga__c</fullName>
    <externalId>false</externalId>
    <label>Travel Information</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
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
### Return_Time_End__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Return_Time_End__c</fullName>
    <externalId>false</externalId>
    <label>Return Time End</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Time</type>
</CustomField>
```
### Is_there_a_special_check_in_to_go_to__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Is_there_a_special_check_in_to_go_to__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Is there a special group check in area that they need to go to?</inlineHelpText>
    <label>Is there a special check in to go to?</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```

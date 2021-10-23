---
layout: default
title: Contact
parent: objects
---
# Metadata Type
CustomObject

# Name
Contact
## Fields
### OtherAddress

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OtherAddress</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Role__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Role__c</fullName>
    <externalId>false</externalId>
    <label>Role</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Assistant Tour Manager</fullName>
                <default>false</default>
                <label>Assistant Tour Manager</label>
            </value>
            <value>
                <fullName>Assistant Compay Manager</fullName>
                <default>false</default>
                <label>Assistant Compay Manager</label>
            </value>
            <value>
                <fullName>Assistant General Manager</fullName>
                <default>false</default>
                <label>Assistant General Manager</label>
            </value>
            <value>
                <fullName>Assistant Production Coordinator</fullName>
                <default>false</default>
                <label>Assistant Production Coordinator</label>
            </value>
            <value>
                <fullName>Assistant Travel Coordinator</fullName>
                <default>false</default>
                <label>Assistant Travel Coordinator</label>
            </value>
            <value>
                <fullName>Associate Producer</fullName>
                <default>false</default>
                <label>Associate Producer</label>
            </value>
            <value>
                <fullName>Company Manager</fullName>
                <default>false</default>
                <label>Company Manager</label>
            </value>
            <value>
                <fullName>Executive In Charge</fullName>
                <default>false</default>
                <label>Executive In Charge</label>
            </value>
            <value>
                <fullName>General Manager</fullName>
                <default>false</default>
                <label>General Manager</label>
            </value>
            <value>
                <fullName>Line Producer</fullName>
                <default>false</default>
                <label>Line Producer</label>
            </value>
            <value>
                <fullName>On-Site Contact</fullName>
                <default>false</default>
                <label>On-Site Contact</label>
            </value>
            <value>
                <fullName>Producer</fullName>
                <default>false</default>
                <label>Producer</label>
            </value>
            <value>
                <fullName>Production Assistant</fullName>
                <default>false</default>
                <label>Production Assistant</label>
            </value>
            <value>
                <fullName>Production Coordinator</fullName>
                <default>false</default>
                <label>Production Coordinator</label>
            </value>
            <value>
                <fullName>Production Manager</fullName>
                <default>false</default>
                <label>Production Manager</label>
            </value>
            <value>
                <fullName>Production Secretary</fullName>
                <default>false</default>
                <label>Production Secretary</label>
            </value>
            <value>
                <fullName>Production Supervisor</fullName>
                <default>false</default>
                <label>Production Supervisor</label>
            </value>
            <value>
                <fullName>Tour Manager</fullName>
                <default>false</default>
                <label>Tour Manager</label>
            </value>
            <value>
                <fullName>Travel and Lodging Coordinator</fullName>
                <default>false</default>
                <label>Travel and Lodging Coordinator</label>
            </value>
            <value>
                <fullName>Travel Coordinator</fullName>
                <default>false</default>
                <label>Travel Coordinator</label>
            </value>
            <value>
                <fullName>Unit Production Manager</fullName>
                <default>false</default>
                <label>Unit Production Manager</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### AVSFQB__QBName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QBName__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <formula>FirstName &amp;&quot; &quot;&amp; LastName &amp;&quot;-&quot;&amp; Account.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>QBName</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__QB_Error__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QB_Error__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>QB Error</label>
    <length>32000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>LongTextArea</type>
    <visibleLines>10</visibleLines>
</CustomField>
```
### Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Name__c</fullName>
    <externalId>false</externalId>
    <label>Name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Last_Activity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Last_Activity__c</fullName>
    <externalId>false</externalId>
    <formula>LastActivityDate</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Last Activity</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Date</type>
</CustomField>
```
### Inactive__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Inactive__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Inactive</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### CurrencyIsoCode

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CurrencyIsoCode</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### LastCUUpdateDate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LastCUUpdateDate</fullName>
</CustomField>
```
### Country_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Country_Id__c</fullName>
    <externalId>false</externalId>
    <label>Country Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Description

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Work_Phone_Extension__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Work_Phone_Extension__c</fullName>
    <externalId>false</externalId>
    <label>Work Phone Extension</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Account_Record_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Account_Record_Type__c</fullName>
    <externalId>false</externalId>
    <formula>Account.RecordType.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Account Record Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Alternate_Email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alternate_Email__c</fullName>
    <externalId>false</externalId>
    <label>Alternate Email</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Email</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__ORDI__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__ORDI__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Other Residential Delivery Indicator</label>
    <length>12</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Account_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Account_Name__c</fullName>
    <externalId>false</externalId>
    <label>Account Name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Name

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Name</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### State__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>State__c</fullName>
    <externalId>false</externalId>
    <label>State</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Email

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### rcsfl__SMS_Number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__SMS_Number__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>SMS Number</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Phone</type>
</CustomField>
```
### State_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>State_Id__c</fullName>
    <externalId>false</externalId>
    <label>State Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__OAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__OAV__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Other Address Vacancy</label>
    <length>1</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipLabel>Contacts</relationshipLabel>
    <relationshipName>Contacts</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### CloudingoAgent__MAS__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__MAS__c</fullName>
    <defaultValue>0</defaultValue>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Mailing Address Status</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Number</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Theatrical</fullName>
                <default>false</default>
                <label>Theatrical</label>
            </value>
            <value>
                <fullName>Family</fullName>
                <default>false</default>
                <label>Family</label>
            </value>
            <value>
                <fullName>Film/TV</fullName>
                <default>false</default>
                <label>Film/TV</label>
            </value>
            <value>
                <fullName>Film</fullName>
                <default>false</default>
                <label>Film</label>
            </value>
            <value>
                <fullName>Film/ TV/ Commercials</fullName>
                <default>false</default>
                <label>Film/ TV/ Commercials</label>
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
### State_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>State_NAV__c</fullName>
    <externalId>false</externalId>
    <label>State_NAV</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### IndividualId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IndividualId</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### Currency_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Currency_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Currency NAV</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__OAS__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__OAS__c</fullName>
    <defaultValue>0</defaultValue>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Other Address Status</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
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
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__MAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__MAV__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Mailing Address Vacancy</label>
    <length>1</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### To_Be_Removed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_Be_Removed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>To be Removed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### Supress_Person_Acc_Conversion__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Supress_Person_Acc_Conversion__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Supress Person Acc Conversion</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### AssistantPhone

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AssistantPhone</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Actual_Contact_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Actual_Contact_ID__c</fullName>
    <externalId>false</externalId>
    <label>Actual Contact ID</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### PersonAccountConversion__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PersonAccountConversion__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>PersonAccountConversion</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### CloudingoAgent__MTZ__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__MTZ__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Mailing Timezone</label>
    <length>48</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__MAR__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__MAR__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Mailing Address Record Type</label>
    <length>1</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### ReportsToId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ReportsToId</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### CloudingoAgent__OTZ__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__OTZ__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Other Timezone</label>
    <length>48</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Options_Preferred__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Options_Preferred__c</fullName>
    <externalId>false</externalId>
    <label>Housing Options Preferred</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Rooms / Suites #</fullName>
                <default>false</default>
                <label>Rooms / Suites #</label>
            </value>
            <value>
                <fullName>Star Rating</fullName>
                <default>false</default>
                <label>Star Rating</label>
            </value>
            <value>
                <fullName>Year Built / Renovated</fullName>
                <default>false</default>
                <label>Year Built / Renovated</label>
            </value>
            <value>
                <fullName>100% Non-Smoking</fullName>
                <default>false</default>
                <label>100% Non-Smoking</label>
            </value>
            <value>
                <fullName>Lift / Elevator</fullName>
                <default>false</default>
                <label>Lift / Elevator</label>
            </value>
            <value>
                <fullName>Property Entry</fullName>
                <default>false</default>
                <label>Property Entry</label>
            </value>
            <value>
                <fullName>Porterage</fullName>
                <default>false</default>
                <label>Porterage</label>
            </value>
            <value>
                <fullName>Windows that open</fullName>
                <default>false</default>
                <label>Windows that open</label>
            </value>
            <value>
                <fullName>Air conditioning</fullName>
                <default>false</default>
                <label>Air conditioning</label>
            </value>
            <value>
                <fullName>High Speed Internet</fullName>
                <default>false</default>
                <label>High Speed Internet</label>
            </value>
            <value>
                <fullName>Pets Allowed</fullName>
                <default>false</default>
                <label>Pets Allowed</label>
            </value>
            <value>
                <fullName>Microwave</fullName>
                <default>false</default>
                <label>Microwave</label>
            </value>
            <value>
                <fullName>Oven</fullName>
                <default>false</default>
                <label>Oven</label>
            </value>
            <value>
                <fullName>Burners</fullName>
                <default>false</default>
                <label>Burners</label>
            </value>
            <value>
                <fullName>Hobs</fullName>
                <default>false</default>
                <label>Hobs</label>
            </value>
            <value>
                <fullName>Refrigerator</fullName>
                <default>false</default>
                <label>Refrigerator</label>
            </value>
            <value>
                <fullName>Coffee maker</fullName>
                <default>false</default>
                <label>Coffee maker</label>
            </value>
            <value>
                <fullName>Hairdryer</fullName>
                <default>false</default>
                <label>Hairdryer</label>
            </value>
            <value>
                <fullName>Bathtub</fullName>
                <default>false</default>
                <label>Bathtub</label>
            </value>
            <value>
                <fullName>Safe</fullName>
                <default>false</default>
                <label>Safe</label>
            </value>
            <value>
                <fullName>Washer/Dryer</fullName>
                <default>false</default>
                <label>Washer/Dryer</label>
            </value>
            <value>
                <fullName>Hotel Restaurant(s)</fullName>
                <default>false</default>
                <label>Hotel Restaurant(s)</label>
            </value>
            <value>
                <fullName>Hotel Bar(s)</fullName>
                <default>false</default>
                <label>Hotel Bar(s)</label>
            </value>
            <value>
                <fullName>Fitness Room</fullName>
                <default>false</default>
                <label>Fitness Room</label>
            </value>
            <value>
                <fullName>On-site Day Spa</fullName>
                <default>false</default>
                <label>On-site Day Spa</label>
            </value>
            <value>
                <fullName>Hotel Shuttle</fullName>
                <default>false</default>
                <label>Hotel Shuttle</label>
            </value>
            <value>
                <fullName>Airport Shuttle</fullName>
                <default>false</default>
                <label>Airport Shuttle</label>
            </value>
            <value>
                <fullName>Comp Breakfast</fullName>
                <default>false</default>
                <label>Comp Breakfast</label>
            </value>
            <value>
                <fullName>Room Service</fullName>
                <default>false</default>
                <label>Room Service</label>
            </value>
            <value>
                <fullName>Self-Parking</fullName>
                <default>false</default>
                <label>Self-Parking</label>
            </value>
            <value>
                <fullName>Valet parking</fullName>
                <default>false</default>
                <label>Valet parking</label>
            </value>
            <value>
                <fullName>Bus Parking</fullName>
                <default>false</default>
                <label>Bus Parking</label>
            </value>
            <value>
                <fullName>Walk to Dining #</fullName>
                <default>false</default>
                <label>Walk to Dining #</label>
            </value>
            <value>
                <fullName>Laundromat Nearby</fullName>
                <default>false</default>
                <label>Laundromat Nearby</label>
            </value>
            <value>
                <fullName>Restaurants Nearby</fullName>
                <default>false</default>
                <label>Restaurants Nearby</label>
            </value>
            <value>
                <fullName>Shopping Centers Nearby</fullName>
                <default>false</default>
                <label>Shopping Centers Nearby</label>
            </value>
            <value>
                <fullName>Gyms Nearby</fullName>
                <default>false</default>
                <label>Gyms Nearby</label>
            </value>
            <value>
                <fullName>Grocery Stores Nearby</fullName>
                <default>false</default>
                <label>Grocery Stores Nearby</label>
            </value>
            <value>
                <fullName>Shows Previously housed</fullName>
                <default>false</default>
                <label>Shows Previously housed</label>
            </value>
            <value>
                <fullName>Airports</fullName>
                <default>false</default>
                <label>Airports</label>
            </value>
            <value>
                <fullName>24 Hour Doorman</fullName>
                <default>false</default>
                <label>24 Hour Doorman</label>
            </value>
            <value>
                <fullName>24 Hour FD</fullName>
                <default>false</default>
                <label>24 Hour FD</label>
            </value>
            <value>
                <fullName>Washer Dryer</fullName>
                <default>false</default>
                <label>Washer Dryer</label>
            </value>
            <value>
                <fullName>Pool</fullName>
                <default>false</default>
                <label>Pool</label>
            </value>
            <value>
                <fullName>Hot Tub</fullName>
                <default>false</default>
                <label>Hot Tub</label>
            </value>
            <value>
                <fullName>Parking On-Site</fullName>
                <default>false</default>
                <label>Parking On-Site</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### CloudingoAgent__OAR__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__OAR__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Other Address Record Type</label>
    <length>1</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### LastCURequestDate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LastCURequestDate</fullName>
</CustomField>
```
### Has_Existing_Person_Account__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Has_Existing_Person_Account__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Has Existing Person Account</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### Alternate_mobile_phone__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alternate_mobile_phone__c</fullName>
    <externalId>false</externalId>
    <label>Alternate mobile phone</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Phone</type>
</CustomField>
```
### Phone_2__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Phone_2__c</fullName>
    <externalId>false</externalId>
    <label>Phone 2</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__MRDI__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__MRDI__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Mailing Residential Delivery Indicator</label>
    <length>12</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Mailing_State_Province__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Mailing_State_Province__c</fullName>
    <externalId>false</externalId>
    <label>Mailing State/Province</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloudingoAgent__CES__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloudingoAgent__CES__c</fullName>
    <defaultValue>0</defaultValue>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Contact Email Status</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Number</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Lead</fullName>
                <default>true</default>
                <label>Lead</label>
            </value>
            <value>
                <fullName>Prospect</fullName>
                <default>false</default>
                <label>Prospect</label>
            </value>
            <value>
                <fullName>Contact</fullName>
                <default>false</default>
                <label>Contact</label>
            </value>
            <value>
                <fullName>Relationship</fullName>
                <default>false</default>
                <label>Relationship</label>
            </value>
            <value>
                <fullName>Partner</fullName>
                <default>false</default>
                <label>Partner</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### To_Be_Deleted__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>To_Be_Deleted__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>To Be Deleted</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### AccountId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AccountId</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <type>Lookup</type>
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
    <relationshipLabel>Contacts</relationshipLabel>
    <relationshipName>Contacts</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### FCQ_Driver__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>FCQ_Driver__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>FCQ Driver</label>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Drivers</relationshipLabel>
    <relationshipName>Drivers</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### AssistantName

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AssistantName</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### MobilePhone

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>MobilePhone</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Phone

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Phone</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### LeadSource

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LeadSource</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
</CustomField>
```
### Home_Address_line_1__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Home_Address_line_1__c</fullName>
    <externalId>false</externalId>
    <label>Home Address line 1</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Jigsaw

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Jigsaw</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Designation_title__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Designation_title__c</fullName>
    <externalId>false</externalId>
    <label>Designation/title</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Assistant Coach</fullName>
                <default>false</default>
                <label>Assistant Coach</label>
            </value>
            <value>
                <fullName>Assistant Company Manager</fullName>
                <default>false</default>
                <label>Assistant Company Manager</label>
            </value>
            <value>
                <fullName>Assistant Director of Operations</fullName>
                <default>false</default>
                <label>Assistant Director of Operations</label>
            </value>
            <value>
                <fullName>Assistant General Manager</fullName>
                <default>false</default>
                <label>Assistant General Manager</label>
            </value>
            <value>
                <fullName>Assistant Production Coordinator</fullName>
                <default>false</default>
                <label>Assistant Production Coordinator</label>
            </value>
            <value>
                <fullName>Assistant Tour Manager</fullName>
                <default>false</default>
                <label>Assistant Tour Manager</label>
            </value>
            <value>
                <fullName>Assistant Travel Coordinator</fullName>
                <default>false</default>
                <label>Assistant Travel Coordinator</label>
            </value>
            <value>
                <fullName>Associate Producer</fullName>
                <default>false</default>
                <label>Associate Producer</label>
            </value>
            <value>
                <fullName>Athletic Department</fullName>
                <default>false</default>
                <label>Athletic Department</label>
            </value>
            <value>
                <fullName>Company Manager</fullName>
                <default>false</default>
                <label>Company Manager</label>
            </value>
            <value>
                <fullName>Director of Operations</fullName>
                <default>false</default>
                <label>Director of Operations</label>
            </value>
            <value>
                <fullName>Director of Sales</fullName>
                <default>false</default>
                <label>Director of Sales</label>
            </value>
            <value>
                <fullName>Executive In Charge</fullName>
                <default>false</default>
                <label>Executive In Charge</label>
            </value>
            <value>
                <fullName>Front Desk</fullName>
                <default>false</default>
                <label>Front Desk</label>
            </value>
            <value>
                <fullName>General Manager</fullName>
                <default>false</default>
                <label>General Manager</label>
            </value>
            <value>
                <fullName>Head Coach</fullName>
                <default>false</default>
                <label>Head Coach</label>
            </value>
            <value>
                <fullName>Line Producer</fullName>
                <default>false</default>
                <label>Line Producer</label>
            </value>
            <value>
                <fullName>On-Site Contact</fullName>
                <default>false</default>
                <label>On-Site Contact</label>
            </value>
            <value>
                <fullName>Producer</fullName>
                <default>false</default>
                <label>Producer</label>
            </value>
            <value>
                <fullName>Production Assistant</fullName>
                <default>false</default>
                <label>Production Assistant</label>
            </value>
            <value>
                <fullName>Production Coordinator</fullName>
                <default>false</default>
                <label>Production Coordinator</label>
            </value>
            <value>
                <fullName>Production Manager</fullName>
                <default>false</default>
                <label>Production Manager</label>
            </value>
            <value>
                <fullName>Production Secretary</fullName>
                <default>false</default>
                <label>Production Secretary</label>
            </value>
            <value>
                <fullName>Production Supervisor</fullName>
                <default>false</default>
                <label>Production Supervisor</label>
            </value>
            <value>
                <fullName>Sales Manager</fullName>
                <default>false</default>
                <label>Sales Manager</label>
            </value>
            <value>
                <fullName>Tour Manager</fullName>
                <default>false</default>
                <label>Tour Manager</label>
            </value>
            <value>
                <fullName>Travel and Lodging Coordinator</fullName>
                <default>false</default>
                <label>Travel and Lodging Coordinator</label>
            </value>
            <value>
                <fullName>Travel Coordinator</fullName>
                <default>false</default>
                <label>Travel Coordinator</label>
            </value>
            <value>
                <fullName>Unit Production Manager</fullName>
                <default>false</default>
                <label>Unit Production Manager</label>
            </value>
            <value>
                <fullName>University Travel Coordinator</fullName>
                <default>false</default>
                <label>University Travel Coordinator</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Personal_Email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Personal_Email__c</fullName>
    <externalId>false</externalId>
    <label>Personal Email</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Email</type>
    <unique>false</unique>
</CustomField>
```
### Skype__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Skype__c</fullName>
    <externalId>false</externalId>
    <label>Skype</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Url</type>
</CustomField>
```
### Postal_Code__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Postal_Code__c</fullName>
    <externalId>false</externalId>
    <label>Postal Code</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### OtherPhone

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OtherPhone</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Test_Record__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Test_Record__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Test Record</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### Birthday__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Birthday__c</fullName>
    <externalId>false</externalId>
    <label>Birthday</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### No_Existing_Person_Account__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Existing_Person_Account__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>No Existing Person Account</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### Work_Email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Work_Email__c</fullName>
    <externalId>false</externalId>
    <label>Work Email</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Email</type>
    <unique>false</unique>
</CustomField>
```
### Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Order__c</fullName>
    <externalId>false</externalId>
    <label>Order</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Birthdate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Birthdate</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### National_Rep__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>National_Rep__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>National Rep</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### DoNotCall

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>DoNotCall</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Alternate_mobile_phone_2__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alternate_mobile_phone_2__c</fullName>
    <externalId>false</externalId>
    <label>Alternate mobile phone 2</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Mailing_Country__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Mailing_Country__c</fullName>
    <externalId>false</externalId>
    <label>Mailing Country</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Fax

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Fax</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Notes__c</fullName>
    <externalId>false</externalId>
    <label>Notes</label>
    <length>3000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>LongTextArea</type>
    <visibleLines>5</visibleLines>
</CustomField>
```
### Department

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Department</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### OwnerId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OwnerId</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### MailingAddress

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>MailingAddress</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### AVSFQB__Quickbooks_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Quickbooks_Id__c</fullName>
    <deprecated>false</deprecated>
    <externalId>true</externalId>
    <label>Quickbooks Id</label>
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### rcsfl__SendSMS__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__SendSMS__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <formula>HYPERLINK(&quot;javascript:sendCTIMessage(&apos;/CLICK_TO_DIAL?OBJECT_NAME=SMS&amp;DN=&quot; + rcsfl__SMS_Number__c + &quot;&apos;)&quot;, rcsfl__SMS_Number__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>SendSMS</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Account_Market__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Account_Market__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Account.Market__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Account Market</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Alternate_Email_2__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alternate_Email_2__c</fullName>
    <externalId>false</externalId>
    <label>Alternate Email 2</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Status_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Status_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Status NAV</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### HasOptedOutOfFax

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>HasOptedOutOfFax</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Decision_Maker__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Decision_Maker__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Decision Maker</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Checkbox</type>
</CustomField>
```
### Extension_Number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Extension_Number__c</fullName>
    <externalId>false</externalId>
    <label>Extension Number</label>
    <precision>5</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### HomePhone

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>HomePhone</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Title

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Title</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```
### GCQ_Driver__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCQ_Driver__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GCQ Driver</label>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Drivers</relationshipLabel>
    <relationshipName>Drivers</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Lookup</type>
</CustomField>
```
### Home_Address_line_2__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Home_Address_line_2__c</fullName>
    <externalId>false</externalId>
    <label>Home Address line 2</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Text</type>
    <unique>false</unique>
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
    <type>Text</type>
    <unique>true</unique>
</CustomField>
```
### Office_location__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Office_location__c</fullName>
    <externalId>false</externalId>
    <label>Office location</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Office_Location</valueSetName>
    </valueSet>
</CustomField>
```
### HasOptedOutOfEmail

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>HasOptedOutOfEmail</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
</CustomField>
```

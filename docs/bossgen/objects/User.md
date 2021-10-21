---
layout: default
title: User
parent: objects
---
# Metadata Type
CustomObject

# Name
User
## Fields
### Housing_Tab_Default__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Tab_Default__c</fullName>
    <externalId>false</externalId>
    <label>Housing Tab Default</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Sales</fullName>
                <default>false</default>
                <label>Sales</label>
            </value>
            <value>
                <fullName>Itinerary</fullName>
                <default>false</default>
                <label>Itinerary</label>
            </value>
            <value>
                <fullName>Stay</fullName>
                <default>false</default>
                <label>Stay</label>
            </value>
            <value>
                <fullName>Bid</fullName>
                <default>false</default>
                <label>Bid</label>
            </value>
            <value>
                <fullName>Contracts</fullName>
                <default>false</default>
                <label>Contracts</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### User_Profile__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>User_Profile__c</fullName>
    <externalId>false</externalId>
    <formula>CASE($Profile.Name,
  &apos;Road Rebel Customer&apos;, &apos;Customer&apos;,
  &apos;System Administrator&apos;, &apos;Customer&apos;,
  &apos;Customer Community Plus(Custom)&apos;, &apos;Customer&apos;,
  &apos;Road Rebel Vendor&apos;, Community_Account_Type__c,
  &apos;Voyajer Profile&apos;, &apos;HousingVendor&apos;,
  &apos;Forbidden&apos;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>User Profile</label>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Community_Account_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Community_Account_Type__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(Contact.Account.RecordType.Name,
  &apos;Hotel Vendor&apos;,&apos;HousingVendor&apos;,
  &apos;Corporate Housing Provider&apos;,&apos;CorporateVendor&apos;,
  &apos;Corporate Housing Vendor&apos;,&apos;CorporateVendor&apos;,
  &apos;Ground Travel Vendor&apos;,&apos;GroundVendor&apos;,
  &apos;Freight Vendor&apos;,&apos;FreightVendor&apos;,
  &apos;Forbidden&apos;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Community Account Type</label>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### ManagerId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ManagerId</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <type>Hierarchy</type>
</CustomField>
```
### Initials__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Initials__c</fullName>
    <externalId>false</externalId>
    <formula>IF(NOT(ISBLANK(ContactId)),LEFT(Contact.FirstName,1)+LEFT(Contact.LastName,1),LEFT($User.FirstName,1)+LEFT($User.LastName,1))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Initials</label>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Preference__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Preference__c</fullName>
    <externalId>false</externalId>
    <label>Office Preference</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Office_Location</valueSetName>
    </valueSet>
</CustomField>
```
### AVSFQB__QBOE_DBSync_Server__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QBOE_DBSync_Server__c</fullName>
    <deprecated>false</deprecated>
    <description>DBSync Server URL</description>
    <externalId>false</externalId>
    <inlineHelpText>DBSync Server URL</inlineHelpText>
    <label>DBSync Server URL</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__DBSync_Profile__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__DBSync_Profile__c</fullName>
    <deprecated>false</deprecated>
    <description>DBSync Profile Name</description>
    <externalId>false</externalId>
    <inlineHelpText>DBSync Profile Name</inlineHelpText>
    <label>DBSync Profile</label>
    <length>100</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__QB_SalesRep_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QB_SalesRep_ID__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>QB SalesRep ID</label>
    <length>100</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__QBOE_Connection_Ticket__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QBOE_Connection_Ticket__c</fullName>
    <defaultValue>&apos;V1-253-$n4Jb_vmujjJWx7f8gvS0Q:163331652&apos;</defaultValue>
    <deprecated>false</deprecated>
    <description>QuickBooks Online Connection Ticket for DBSync</description>
    <externalId>false</externalId>
    <inlineHelpText>QuickBooks Online Connection Ticket for DBSync</inlineHelpText>
    <label>QBOE Connection Ticket</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### User_License__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>User_License__c</fullName>
    <externalId>false</externalId>
    <formula>Profile.UserLicense.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>User License</label>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Community_Account_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Community_Account_Type__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(Contact.Account.RecordType.Name,
  &apos;Hotel Vendor&apos;,&apos;HousingVendor&apos;,
  &apos;Hotel Vendor Chain&apos;,&apos;HotelVendorChain&apos;,
  &apos;Corporate Housing Provider&apos;,&apos;CorporateVendor&apos;,
  &apos;Corporate Housing Vendor&apos;,&apos;CorporateVendor&apos;,
  &apos;Ground Travel Vendor&apos;,&apos;GroundVendor&apos;,
  &apos;Freight Vendor&apos;,&apos;FreightVendor&apos;,
  &apos;Forbidden&apos;
)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Community Account Type</label>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__DBSync_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__DBSync_Id__c</fullName>
    <deprecated>false</deprecated>
    <description>DBSync Username</description>
    <externalId>false</externalId>
    <inlineHelpText>DBSync UserName</inlineHelpText>
    <label>DBSync Id</label>
    <length>150</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__DBSync_Passwd__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__DBSync_Passwd__c</fullName>
    <deprecated>false</deprecated>
    <description>DBSync Login Password</description>
    <externalId>false</externalId>
    <inlineHelpText>DBSync Login Password</inlineHelpText>
    <label>DBSync Passwd</label>
    <length>100</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

---
layout: default
title: Bid__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Bid__c
## Fields
### Housing_Date_In__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Date_In__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Date_In__c</formula>
    <label>Housing Date In</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Bid_Has_Duplicate_Traces__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Has_Duplicate_Traces__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Bid Has Duplicate Traces</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Room_Rate_Release_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Rate_Release_date__c</fullName>
    <externalId>false</externalId>
    <label>Bid Release date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Trip_Details_Update_Created_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Created_Date__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Created Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Terms__c</fullName>
    <externalId>false</externalId>
    <label>Terms</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### GCIP_Created_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Created_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GCIP Created By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid2</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### GCIP_last_modified_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_last_modified_date__c</fullName>
    <externalId>false</externalId>
    <label>GCIP last modified date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Parent_End_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Parent_End_Date__c</fullName>
    <externalId>false</externalId>
    <formula>IF(RecordType.DeveloperName == &apos;Housing_Bid&apos;, Housing__r.Date_Out__c, 
      IF(RecordType.DeveloperName == &apos;GT_Bid&apos;, GT__r.End_Date__c, 
						      IF(RecordType.DeveloperName == &apos;Freight_Bid&apos;, Freight__r.End_Date__c, 
												      IF(RecordType.DeveloperName == &apos;Air_Bid&apos;, Air__r.Arrival_Date__c, null)
												) 
						) 
)</formula>
    <label>Parent End Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Form_Utilization__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Utilization__c</fullName>
    <externalId>false</externalId>
    <label>Form Utilization</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Permits__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Permits__c</fullName>
    <externalId>false</externalId>
    <label>Permits</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Transportation_Contract_Created_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Created_Date__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract - Created Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Wait_Time_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Wait_Time_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Wait Time Notes</label>
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
                <fullName>Wait time billed at $_____</fullName>
                <default>false</default>
                <label>Wait time billed at $_____</label>
            </value>
            <value>
                <fullName>Wait time included</fullName>
                <default>false</default>
                <label>Wait time included</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Rate_Plan_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Plan_Name__c</fullName>
    <externalId>false</externalId>
    <label>Rate Plan Name</label>
    <length>1000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Email_Confirmation_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Confirmation_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Email Confirmation - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### VAT_added_or_changed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT_added_or_changed__c</fullName>
    <externalId>false</externalId>
    <label>VAT # added or changed?</label>
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
### Sabre_Response__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sabre_Response__c</fullName>
    <externalId>false</externalId>
    <label>Sabre Response</label>
    <length>1000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Rooming_List_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_List_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Rooming List is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Internal_Utilization_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Utilization_Date__c</fullName>
    <externalId>false</externalId>
    <label>Internal Utilization Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Final_Contract_form_is_emailed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Contract_form_is_emailed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Final Contract form is emailed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Cancellation_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cancellation_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Cancellation - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Vendor_Bid_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Bid_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Vendor Bid Notes</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Counter_Needed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Counter_Needed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Counter Needed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Housing_Record_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Record_Type__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.RecordType.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing Record Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Transportation_Contract_Created_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Created_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Transportation Contract - Created By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid8</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Internal_notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_notes__c</fullName>
    <externalId>false</externalId>
    <label>Internal notes</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### GT_Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Start_Date__c</fullName>
    <externalId>false</externalId>
    <formula>GT__r.Start_Date__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>GT Start Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Tolls_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tolls_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Tolls Notes</label>
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
                <fullName>Tolls included up to ___________</fullName>
                <default>false</default>
                <label>Tolls included up to ___________</label>
            </value>
            <value>
                <fullName>Tolls will be an additional charge</fullName>
                <default>false</default>
                <label>Tolls will be an additional charge</label>
            </value>
            <value>
                <fullName>Tolls included</fullName>
                <default>false</default>
                <label>Tolls included</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Client_Contract_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Contract_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Client_Contract_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Client_Contract_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Client_Contract_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Client_Contract_Date__c)), CASE(
  MONTH(Client_Contract_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Client_Contract_Date__c)) + &quot;-&quot; + TEXT(YEAR(Client_Contract_Date__c))), &quot;&quot;)</formula>
    <label>Client Contract Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Vendor_Comments__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Comments__c</fullName>
    <externalId>false</externalId>
    <label>Vendor Comments</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Client_Utilization_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Utilization_Date__c</fullName>
    <externalId>false</externalId>
    <label>Client Utilization Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Housing_Options_Sent_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Options_Sent_to_Client__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Options_sent_to_client__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing Options Sent to Client</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Housing_Preference_Formula__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Preference_Formula__c</fullName>
    <externalId>false</externalId>
    <formula>Text(Housing__r.Housing_Preference__c)</formula>
    <label>Housing Preference</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Contract_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Contract_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Housing Contract - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Dead_Head_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dead_Head_Days__c</fullName>
    <externalId>false</externalId>
    <label>Dead Head Days</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Contract_Created_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Created_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contract Created By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid4</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Cover__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cover__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Cover</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Cancelled</fullName>
                <default>false</default>
                <label>Cancelled</label>
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
                <fullName>No Rooms Picked-Up</fullName>
                <default>false</default>
                <label>No Rooms Picked-Up</label>
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
                <fullName>Deleted</fullName>
                <default>false</default>
                <label>Deleted</label>
            </value>
            <value>
                <fullName>Pending Update</fullName>
                <default>false</default>
                <label>Pending Update</label>
            </value>
            <value>
                <fullName>Decision</fullName>
                <default>false</default>
                <label>Decision</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Memorialization_Data__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Memorialization_Data__c</fullName>
    <externalId>false</externalId>
    <label>Memorialization Data</label>
    <length>131072</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Freight_Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Start_Date__c</fullName>
    <externalId>false</externalId>
    <formula>Freight__r.Start_Date__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Freight Start Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Fuel_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Fuel_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Fuel Notes</label>
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
                <fullName>Fuel is based on _______ miles at $____/mile</fullName>
                <default>false</default>
                <label>Fuel is based on _______ miles at $____/mile</label>
            </value>
            <value>
                <fullName>Fuel is included</fullName>
                <default>false</default>
                <label>Fuel is included</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Rate_Agreement_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Last_Send_Date__c</fullName>
    <description>Last Conga Send Date</description>
    <externalId>false</externalId>
    <label>Rate Agreement - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Air_Group_Type_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Group_Type_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>Text(Air__r.Group_Type__c)</formula>
    <label>Air Group Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Selected_option_comments__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Selected_option_comments__c</fullName>
    <externalId>false</externalId>
    <label>Selected option comments</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Trip_Details_Update_Last_Modified_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Last_Modified_Date__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Last Modified Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Vendor_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <formula>Vendor_Contact__r.Id</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Contact Id</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
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
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>3p Check-out Guaranteed</fullName>
                <default>false</default>
                <label>3p Check-out Guaranteed</label>
            </value>
            <value>
                <fullName>All rooms must be non-smoking.</fullName>
                <default>false</default>
                <label>All rooms must be non-smoking.</label>
            </value>
            <value>
                <fullName>All single rooms must have king beds.</fullName>
                <default>false</default>
                <label>All single rooms must have king beds.</label>
            </value>
            <value>
                <fullName>Bathtubs in all group rooms.</fullName>
                <default>false</default>
                <label>Bathtubs in all group rooms.</label>
            </value>
            <value>
                <fullName>Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment section</fullName>
                <default>false</default>
                <label>Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment section</label>
            </value>
            <value>
                <fullName>Breakfast included in rate - Please specify cost of breakfast if not included. ___________</fullName>
                <default>false</default>
                <label>Breakfast included in rate - Please specify cost of breakfast if not included. ___________</label>
            </value>
            <value>
                <fullName>Check-in at 00:00 for the whole group guaranteed.</fullName>
                <default>false</default>
                <label>Check-in at 00:00 for the whole group guaranteed.</label>
            </value>
            <value>
                <fullName>CHeck-out at 00:00 for the whole group guaranteed.</fullName>
                <default>false</default>
                <label>CHeck-out at 00:00 for the whole group guaranteed.</label>
            </value>
            <value>
                <fullName>Comp hospitality room with microwave and fridge for group, if not in all rooms</fullName>
                <default>false</default>
                <label>Comp hospitality room with microwave and fridge for group, if not in all rooms</label>
            </value>
            <value>
                <fullName>Complimentary High Speed internet in the rooms.</fullName>
                <default>false</default>
                <label>Complimentary High Speed internet in the rooms.</label>
            </value>
            <value>
                <fullName>Complimentary local &amp; 800 calls.</fullName>
                <default>false</default>
                <label>Complimentary local &amp; 800 calls.</label>
            </value>
            <value>
                <fullName>Complimentary microwave and fridges in all rooms.</fullName>
                <default>false</default>
                <label>Complimentary microwave and fridges in all rooms.</label>
            </value>
            <value>
                <fullName>Complimentary parking. If not complimentary, please indicate discounted parking.</fullName>
                <default>false</default>
                <label>Complimentary parking. If not complimentary, please indicate discounted parking.</label>
            </value>
            <value>
                <fullName>Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.</fullName>
                <default>false</default>
                <label>Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.</label>
            </value>
            <value>
                <fullName>CONTRACTED CALL IN RATE FOR A TV SHOW. No room night guarantee, rate for individuals coming in a out. Rate must be guaranteed regardless of pick-up.</fullName>
                <default>false</default>
                <label>CONTRACTED CALL IN RATE FOR A TV SHOW. No room night guarantee, rate for individuals coming in a out. Rate must be guaranteed regardless of pick-up.</label>
            </value>
            <value>
                <fullName>F&amp;B discount.</fullName>
                <default>false</default>
                <label>F&amp;B discount.</label>
            </value>
            <value>
                <fullName>Hotel contact to sign a location agreement (agreeing to shoot an interview in the room, no hotel photograph logos or signage)</fullName>
                <default>false</default>
                <label>Hotel contact to sign a location agreement (agreeing to shoot an interview in the room, no hotel photograph logos or signage)</label>
            </value>
            <value>
                <fullName>Hotel is WAIVING all cancellation and attrition penalties. Group will prioritize properties that can accommodate this request.</fullName>
                <default>false</default>
                <label>Hotel is WAIVING all cancellation and attrition penalties. Group will prioritize properties that can accommodate this request.</label>
            </value>
            <value>
                <fullName>If you can not take all the rooms, please note how many you can take if you are interested in a partial block.</fullName>
                <default>false</default>
                <label>If you can not take all the rooms, please note how many you can take if you are interested in a partial block.</label>
            </value>
            <value>
                <fullName>Include rates for all suite types.</fullName>
                <default>false</default>
                <label>Include rates for all suite types.</label>
            </value>
            <value>
                <fullName>Laundry discount.</fullName>
                <default>false</default>
                <label>Laundry discount.</label>
            </value>
            <value>
                <fullName>Micro&apos;s &amp; Fridges very important- how many can you acommodate? Is there and additional charge?</fullName>
                <default>false</default>
                <label>Micro&apos;s &amp; Fridges very important- how many can you acommodate? Is there and additional charge?</label>
            </value>
            <value>
                <fullName>Mini bars must be emptied for the group, fee of charge.</fullName>
                <default>false</default>
                <label>Mini bars must be emptied for the group, fee of charge.</label>
            </value>
            <value>
                <fullName>Need a COMP meeting room on GROUND FLOOR for tech gear.</fullName>
                <default>false</default>
                <label>Need a COMP meeting room on GROUND FLOOR for tech gear.</label>
            </value>
            <value>
                <fullName>Option date to be no earlier than X.</fullName>
                <default>false</default>
                <label>Option date to be no earlier than X.</label>
            </value>
            <value>
                <fullName>Please provide a weekly/monthly parking rate for group (if not complimentary).</fullName>
                <default>false</default>
                <label>Please provide a weekly/monthly parking rate for group (if not complimentary).</label>
            </value>
            <value>
                <fullName>Please see attached rooming list and quote based on that. The hotel acknowledges offer is based on the attached rooming list.</fullName>
                <default>false</default>
                <label>Please see attached rooming list and quote based on that. The hotel acknowledges offer is based on the attached rooming list.</label>
            </value>
            <value>
                <fullName>Production is interested in hotel points, if applicable</fullName>
                <default>false</default>
                <label>Production is interested in hotel points, if applicable</label>
            </value>
            <value>
                <fullName>Rate and all terms of contract are guaranteed regardless of pick up. At time of rooming list any rooms not picked up are released at no penalty to group.</fullName>
                <default>false</default>
                <label>Rate and all terms of contract are guaranteed regardless of pick up. At time of rooming list any rooms not picked up are released at no penalty to group.</label>
            </value>
            <value>
                <fullName>Rate must exclude breakfast, but please offer discounted breakfast price.</fullName>
                <default>false</default>
                <label>Rate must exclude breakfast, but please offer discounted breakfast price.</label>
            </value>
            <value>
                <fullName>Rates to include cooked breakfast.</fullName>
                <default>false</default>
                <label>Rates to include cooked breakfast.</label>
            </value>
            <value>
                <fullName>Rooms counts and dates are soft and may change.</fullName>
                <default>false</default>
                <label>Rooms counts and dates are soft and may change.</label>
            </value>
            <value>
                <fullName>Rooms may or may not be continuous throughout the length of stay. May need rooms pre and post day.</fullName>
                <default>false</default>
                <label>Rooms may or may not be continuous throughout the length of stay. May need rooms pre and post day.</label>
            </value>
            <value>
                <fullName>Suite upgrade for company manager, if available.</fullName>
                <default>false</default>
                <label>Suite upgrade for company manager, if available.</label>
            </value>
            <value>
                <fullName>This group is a SPECIAL EQUITY tour. Individuals will have 1 official hotel option. Rate and all terms of contract are guaranteed regardless of pick up. At time of rooming list, any rooms not picked up are released at no penalty to group.</fullName>
                <default>false</default>
                <label>This group is a SPECIAL EQUITY tour. Individuals will have 1 official hotel option. Rate and all terms of contract are guaranteed regardless of pick up. At time of rooming list, any rooms not picked up are released at no penalty to group.</label>
            </value>
            <value>
                <fullName>This group is a UNION TOUR. Individuals will have 2 official hotel options to select from. No pick up is guaranteed.</fullName>
                <default>false</default>
                <label>This group is a UNION TOUR. Individuals will have 2 official hotel options to select from. No pick up is guaranteed.</label>
            </value>
            <value>
                <fullName>Would like for the hotel bar to stay open late night for group</fullName>
                <default>false</default>
                <label>Would like for the hotel bar to stay open late night for group</label>
            </value>
            <value>
                <fullName>X suite upgrades.</fullName>
                <default>false</default>
                <label>X suite upgrades.</label>
            </value>
            <value>
                <fullName>XX room night(s) of every XX room nights picked up cumulative per stay is complementary</fullName>
                <default>false</default>
                <label>XX room night(s) of every XX room nights picked up cumulative per stay is complementary</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Contracting_Coordinator_Final__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Coordinator_Final__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contracting Coordinator Final</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid3d2R</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Rate_Agreement_Created_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Created_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Rate Agreement Created By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Concessions_Provided__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Concessions_Provided__c</fullName>
    <externalId>false</externalId>
    <label>Concessions Provided</label>
    <length>10000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Form_Ticketed_Confirmation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Ticketed_Confirmation__c</fullName>
    <externalId>false</externalId>
    <label>Form Ticketed Confirmation</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Trips_Details_Update_Created_On_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trips_Details_Update_Created_On_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Trips_Details_Update_Created_On__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Trips_Details_Update_Created_On__c)) + &quot;-&quot; + CASE(
  MONTH(Trips_Details_Update_Created_On__c),
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
) + &quot;-&quot; + TEXT(YEAR(Trips_Details_Update_Created_On__c)), CASE(
  MONTH(Trips_Details_Update_Created_On__c),
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
) + &quot;-&quot; + TEXT(DAY(Trips_Details_Update_Created_On__c)) + &quot;-&quot; + TEXT(YEAR(Trips_Details_Update_Created_On__c))), &quot;&quot;)</formula>
    <label>Trips Details Update - Created On Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Rooming_List_Reminder__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Rooming_List_Reminder__c</fullName>
    <externalId>false</externalId>
    <label>Form Rooming List Reminder</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Live_Days_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Live_Days_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Live Days Notes</label>
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
                <fullName>Live Days _________</fullName>
                <default>false</default>
                <label>Live Days _________</label>
            </value>
            <value>
                <fullName>Total Days _________</fullName>
                <default>false</default>
                <label>Total Days _________</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### GT_End_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_End_Date__c</fullName>
    <externalId>false</externalId>
    <formula>GT__r.End_Date__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>GT End Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Use_Credit_Card__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Use_Credit_Card__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Use Credit Card</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Form_Create_GCIP__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Create_GCIP__c</fullName>
    <externalId>false</externalId>
    <label>Form Create GCIP</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contract_to_Client_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_to_Client_Last_Send_Date__c</fullName>
    <description>Last Conga Send Date</description>
    <externalId>false</externalId>
    <label>Contract to Client - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Provider__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Provider__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Provider</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Bid (Provider)</relationshipLabel>
    <relationshipName>Bid2</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Form_Room_Changes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Room_Changes__c</fullName>
    <externalId>false</externalId>
    <label>Form Room Changes</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### coVendorEmail__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>coVendorEmail__c</fullName>
    <externalId>false</externalId>
    <label>coVendorEmail</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Trips_Details_Update_Created_On__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trips_Details_Update_Created_On__c</fullName>
    <externalId>false</externalId>
    <label>Trips Details Update - Created On</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Sync_to_QB__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sync_to_QB__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Sync to QB</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Form_No_Pick_Up__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_No_Pick_Up__c</fullName>
    <externalId>false</externalId>
    <label>Form No Pick-Up</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Contract_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Contract_to_Client__c</fullName>
    <externalId>false</externalId>
    <label>Form Contract to Client</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Final_Choice_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Choice_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Final Choice - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Trip_Details_Update_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Contract_last_modified_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_last_modified_date__c</fullName>
    <externalId>false</externalId>
    <label>Contract last modified date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Final_Choice_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Choice_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Final Choice - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Form_Contract_Date_Change__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Contract_Date_Change__c</fullName>
    <externalId>false</externalId>
    <label>Form Contract Date Change</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Fuel__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Fuel__c</fullName>
    <externalId>false</externalId>
    <label>Fuel</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Client_Utilization_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Utilization_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Client_Utilization_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Client_Utilization_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Client_Utilization_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Client_Utilization_Date__c)), CASE(
  MONTH(Client_Utilization_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Client_Utilization_Date__c)) + &quot;-&quot; + TEXT(YEAR(Client_Utilization_Date__c))), &quot;&quot;)</formula>
    <label>Client Utilization Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Air_Charter__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air_Charter__c</fullName>
    <externalId>false</externalId>
    <formula>Air__r.Air_Charter__c</formula>
    <label>Air Charter</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Transportation_Contract_Cancel_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Cancel_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract - Cancel Policy</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### No_Bid_reason_conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Bid_reason_conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(No_Bid_reason__c), BR() + &quot;&lt;span style=&apos;color:red;&apos;&gt;&quot; + No_Bid_reason__c + &quot;&lt;/span&gt;&quot;, &quot;&quot;)</formula>
    <label>No Bid reason conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Final_Contract__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Final_Contract__c</fullName>
    <externalId>false</externalId>
    <label>Form Final Contract</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Contract_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Contract_Last_Send_Date__c</fullName>
    <description>Last Conga Send Date</description>
    <externalId>false</externalId>
    <label>Housing Contract - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### No_Pick_Up_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Pick_Up_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>No Pick Up - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Utilization_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Utilization - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Utilization_Penalty_Currency_Symbol__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Penalty_Currency_Symbol__c</fullName>
    <externalId>false</externalId>
    <label>Utilization Penalty - Currency Symbol</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### responseVendorTitle__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>responseVendorTitle__c</fullName>
    <externalId>false</externalId>
    <label>responseVendorTitle</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Lead_Sent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Lead_Sent__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Lead Sent</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### ServiceId__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ServiceId__c</fullName>
    <externalId>false</externalId>
    <formula>IF(RecordType.DeveloperName == &apos;Housing_Bid&apos;, Housing__c, 
      IF(RecordType.DeveloperName == &apos;GT_Bid&apos;, GT__c, 
						      IF(RecordType.DeveloperName == &apos;Freight_Bid&apos;, Freight__c, 
												      IF(RecordType.DeveloperName == &apos;Air_Bid&apos;, Air__c, null)
												) 
						) 
)</formula>
    <label>ServiceId</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Final_Air_Confirmation_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Air_Confirmation_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Final Air Confirmation - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Transportation_Contract_LastModifiedDate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_LastModifiedDate__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract-LastModifiedDate</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Form_Email_Confirmation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Email_Confirmation__c</fullName>
    <externalId>false</externalId>
    <label>Form Email Confirmation</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### GT_Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT_Description__c</fullName>
    <externalId>false</externalId>
    <formula>GT__r.Description__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>GT Description</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rate_Agreement_Production_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Production_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement Production Contact Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Cancellation_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cancellation_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Cancellation is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Form_Names_Final_Payment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Names_Final_Payment__c</fullName>
    <externalId>false</externalId>
    <label>Form Names &amp; Final Payment</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### OLR__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OLR__c</fullName>
    <externalId>false</externalId>
    <label>OLR</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contract_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_ID__c</fullName>
    <externalId>false</externalId>
    <label>Contract ID</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Room_Changes_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Changes_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Room Changes - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### ContractToClientCorrelative__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ContractToClientCorrelative__c</fullName>
    <externalId>false</externalId>
    <label>ContractToClientCorrelative</label>
    <precision>3</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Gratuity_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Gratuity_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Gratuity Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Permits_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Permits_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Permits Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Driver_Lodging_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_Lodging_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Driver Lodging Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Final_Contract_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Contract_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Final Contract - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Client_Deposit_Due_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Deposit_Due_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Client_Deposit_Due_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Client_Deposit_Due_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Client_Deposit_Due_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Client_Deposit_Due_Date__c)), CASE(
  MONTH(Client_Deposit_Due_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Client_Deposit_Due_Date__c)) + &quot;-&quot; + TEXT(YEAR(Client_Deposit_Due_Date__c))), &quot;&quot;)</formula>
    <label>Client Deposit Due Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Room_Changes_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Changes_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Room Changes - Last Send By</label>
    <length>255</length>
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
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Bid (Venue)</relationshipLabel>
    <relationshipName>Bid1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Internal_Deposit_Due_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Deposit_Due_Date__c</fullName>
    <externalId>false</externalId>
    <label>Internal Deposit Due Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Parent_Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Parent_Start_Date__c</fullName>
    <externalId>false</externalId>
    <formula>IF(RecordType.DeveloperName == &apos;Housing_Bid&apos;, Housing__r.Date_In__c, 
      IF(RecordType.DeveloperName == &apos;GT_Bid&apos;, GT__r.Start_Date__c, 
						      IF(RecordType.DeveloperName == &apos;Freight_Bid&apos;, Freight__r.Start_Date__c, 
												      IF(RecordType.DeveloperName == &apos;Air_Bid&apos;, Air__r.Departure_Date__c, null)
												) 
						) 
)</formula>
    <label>Parent Start Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Client_Deposit_Due_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Deposit_Due_Date__c</fullName>
    <externalId>false</externalId>
    <label>Client Deposit Due Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Ticketed_Confirmation_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ticketed_Confirmation_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Ticketed Confirmation - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Bid_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Bid Notes</label>
    <length>300</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Trips_Details_Update_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trips_Details_Update_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <label>Trips Details Update Contact Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Dead_Head_notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dead_Head_notes__c</fullName>
    <externalId>false</externalId>
    <label>Dead Head notes</label>
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
                <fullName>Dead Head days _________</fullName>
                <default>false</default>
                <label>Dead Head days _________</label>
            </value>
            <value>
                <fullName>Dead Head day not included</fullName>
                <default>false</default>
                <label>Dead Head day not included</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Counter_Needed_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Counter_Needed_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Counter Needed - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
### Email_Confirmation_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Email_Confirmation_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Email Confirmation - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Housing_Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Start_Date__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Date_In__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing Start Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Rate_Agreement_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Client_Names_Final_Payment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Names_Final_Payment__c</fullName>
    <externalId>false</externalId>
    <label>Client Names &amp; Final Payment</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Corporate_Concessions_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Corporate_Concessions_Conga__c</fullName>
    <externalId>false</externalId>
    <label>Corporate Concessions</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Total_Miles_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Miles_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Total Miles Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Customs_exam_charges__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Customs_exam_charges__c</fullName>
    <externalId>false</externalId>
    <label>Customs exam charges</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Rooming_List_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_List_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Rooming List - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Freight_End_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_End_Date__c</fullName>
    <externalId>false</externalId>
    <formula>Freight__r.End_Date__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Freight End Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Final_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Final is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Include_in_option_cover_sheet__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Include_in_option_cover_sheet__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Include in option cover sheet</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Internal_Names_Final_Payment__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Names_Final_Payment__c</fullName>
    <externalId>false</externalId>
    <label>Internal Names &amp; Final Payment</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Contract_first_only__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_first_only__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Contract (first only)</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Permits_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Permits_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Permits Notes</label>
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
                <fullName>Permit fees included up to __________</fullName>
                <default>false</default>
                <label>Permit fees included up to __________</label>
            </value>
            <value>
                <fullName>Permit fees included</fullName>
                <default>false</default>
                <label>Permit fees included</label>
            </value>
            <value>
                <fullName>Permit fees will be an additional charge</fullName>
                <default>false</default>
                <label>Permit fees will be an additional charge</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Trip_Details_Update_Cancel_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Cancel_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Cancel Policy</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Transportation_Contract_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Driver_Lodging_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_Lodging_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Driver Lodging Notes</label>
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
                <fullName>Is Driver Lodging included in the rate?</fullName>
                <default>false</default>
                <label>Is Driver Lodging included in the rate?</label>
            </value>
            <value>
                <fullName>If not included, please list dates group is responsible for: Check In ____  Check Out ____</fullName>
                <default>false</default>
                <label>If not included, please list dates group is responsible for: Check In ____  Check Out ____</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### coVendorPhone__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>coVendorPhone__c</fullName>
    <externalId>false</externalId>
    <label>coVendorPhone</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### GCIP_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>GCIP - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Counter_Needed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Counter_Needed__c</fullName>
    <externalId>false</externalId>
    <label>Form Counter Needed</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rooming_List_Reminder_Form_is_emailed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_List_Reminder_Form_is_emailed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Rooming List Reminder Form is emailed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Names_Final_Payment_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Names_Final_Payment_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Names &amp; Final Payment - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Total_Miles__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Miles__c</fullName>
    <externalId>false</externalId>
    <label>Total Miles</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Form_Final_Air_Confirmation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Final_Air_Confirmation__c</fullName>
    <externalId>false</externalId>
    <label>Form Final Air Confirmation</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Insurance_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Insurance_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Insurance Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### GCIP_last_modified_by__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_last_modified_by__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GCIP last modified by</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid3</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Trip_Details_Update_Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Terms__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Terms</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>20</visibleLines>
</CustomField>
```
### Names_Final_Payment_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Names_Final_Payment_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Names &amp; Final Payment - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Billing_Options__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Billing_Options__c</fullName>
    <externalId>false</externalId>
    <label>Billing Options</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>10</visibleLines>
</CustomField>
```
### Rate_agreement_last_modified_by__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_agreement_last_modified_by__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Rate agreement last modified by</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contract_create_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_create_date__c</fullName>
    <externalId>false</externalId>
    <label>Contract create date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Transport_Insurance_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transport_Insurance_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Transport Insurance Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Utilization_Percentage_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Percentage_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Utilization_Percentage__c) &amp;&amp; Utilization_Percentage__c != 0, TEXT(Utilization_Percentage__c * 100) + &quot;%&quot;, &quot;&quot;)</formula>
    <label>Utilization Percentage</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Utilization_Percentage__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Percentage__c</fullName>
    <externalId>false</externalId>
    <label>Utilization %: Percentage</label>
    <precision>5</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Live_Days__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Live_Days__c</fullName>
    <externalId>false</externalId>
    <label>Live Days</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Tolls_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tolls_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Tolls Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Contract_last_modified_by__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_last_modified_by__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contract last modified by</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid5</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Trip_Details_Update_Last_Modified_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Last_Modified_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Trip Details Update - Last Modified By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid7</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### is_Vendor_European__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>is_Vendor_European__c</fullName>
    <externalId>false</externalId>
    <formula>OR(CONTAINS(Vendor__r.ShippingCountry, &quot;Albania&quot;), 
	CONTAINS(Vendor__r.ShippingCountry, &quot;Germany&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Andorra&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Armenia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Austria&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Azerbaijan&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Belgium&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Belarus&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Bosnia and Herzegovina&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Bulgaria&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Cyprus&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Holy See (Vatican City State)&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Croatia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Denmark&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Slovakia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Slovenia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Spain&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Estonia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Finland&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;France&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Georgia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Greece&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Hungary&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Ireland&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Iceland&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Italy&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Kazakhstan&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Latvia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Liechtenstein&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Lithuania&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Luxembourg&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Macedonia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Malta&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Moldova&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Monaco&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Montenegro&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Norway&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Netherlands&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Poland&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Portugal&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;United Kingdom&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Czech Republic&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Romania&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Russia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;San Marino&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Serbia&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Sweden&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Switzerland&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Turkey&quot;),
	CONTAINS(Vendor__r.ShippingCountry, &quot;Ukraine&quot;)
)</formula>
    <label>is Vendor European</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Customs_exam_charges_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Customs_exam_charges_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Customs exam charges Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Options__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Options__c</fullName>
    <externalId>false</externalId>
    <label>Options #</label>
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
### Import_and_export_charges__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Import_and_export_charges__c</fullName>
    <externalId>false</externalId>
    <label>Import and export charges</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Stay_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Stay_ID__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Stay ID</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Additional_GT_Fees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Additional_GT_Fees__c</fullName>
    <externalId>false</externalId>
    <label>Additional GT Fees</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Driver Lodging</fullName>
                <default>false</default>
                <label>Driver Lodging</label>
            </value>
            <value>
                <fullName>Gratuity</fullName>
                <default>false</default>
                <label>Gratuity</label>
            </value>
            <value>
                <fullName>Tolls</fullName>
                <default>false</default>
                <label>Tolls</label>
            </value>
            <value>
                <fullName>Parking</fullName>
                <default>false</default>
                <label>Parking</label>
            </value>
            <value>
                <fullName>Fuel</fullName>
                <default>false</default>
                <label>Fuel</label>
            </value>
            <value>
                <fullName>Double Driver</fullName>
                <default>false</default>
                <label>Double Driver</label>
            </value>
            <value>
                <fullName>Over Drive</fullName>
                <default>false</default>
                <label>Over Drive</label>
            </value>
            <value>
                <fullName>Dead Head Days</fullName>
                <default>false</default>
                <label>Dead Head Days</label>
            </value>
            <value>
                <fullName>Live Days</fullName>
                <default>false</default>
                <label>Live Days</label>
            </value>
            <value>
                <fullName>Permits</fullName>
                <default>false</default>
                <label>Permits</label>
            </value>
            <value>
                <fullName>Total Miles</fullName>
                <default>false</default>
                <label>Total Miles</label>
            </value>
            <value>
                <fullName>Wait Time</fullName>
                <default>false</default>
                <label>Wait Time</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
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
    <lookupFilter>
        <active>false</active>
        <filterItems>
            <field>Contact.AccountId</field>
            <operation>equals</operation>
            <valueField>$Source.Vendor__c</valueField>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Housing_Date_Out__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Date_Out__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Date_Out__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing Date Out</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Loading__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loading__c</fullName>
    <externalId>false</externalId>
    <label>Loading</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Trip_Details_Update_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Transportation_Contract_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract Contact Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Wait_Time_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Wait_Time_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Wait Time Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Transportation_Contract_Last_Modified_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Last_Modified_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Transportation Contract-Last Modified By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid9</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
        <valueSetName>Bid_Status</valueSetName>
    </valueSet>
</CustomField>
```
### Credit_Card_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Credit Card - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Transportation_Contract_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Deposit_Amount_Currency_Symbol__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deposit_Amount_Currency_Symbol__c</fullName>
    <externalId>false</externalId>
    <label>Deposit Amount - Currency Symbol</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Over_Drive__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Over_Drive__c</fullName>
    <externalId>false</externalId>
    <label>Over Drive</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Contract_to_Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_to_Client__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Contract to Client</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### responseVendorEmail__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>responseVendorEmail__c</fullName>
    <externalId>false</externalId>
    <label>responseVendorEmail</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Loading_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loading_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Loading Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Corporate_Concessions_Total_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Corporate_Concessions_Total_Conga__c</fullName>
    <externalId>false</externalId>
    <label>Corporate Concessions Total</label>
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
### Cancellation_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cancellation_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Cancellation - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contract_Due_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Due_Date__c</fullName>
    <externalId>false</externalId>
    <label>Internal Contract Due Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### DX_to_Venue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>DX_to_Venue__c</fullName>
    <externalId>false</externalId>
    <label>DX to Venue</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Deposit_Due_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deposit_Due_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Deposit_Due - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Gratuity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Gratuity__c</fullName>
    <externalId>false</externalId>
    <label>Gratuity</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
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
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### URL_Landing_Page_Submission__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>URL_Landing_Page_Submission__c</fullName>
    <externalId>false</externalId>
    <formula>HYPERLINK($Setup.RoadRebelSettings__c.Community_Base_URL__c + &apos;/s/voyajer-bid-submission?lptype=submission&amp;b=&apos;&amp; UUID_for_Landing_Page__c &amp;&apos;&amp;hco=&apos;&amp;Housing__c&amp;&apos;&amp;service=lodging&amp;record=&apos;+CASESAFEID(Id), &apos;Submit Bid&apos;)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>URL Landing Page Submission</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Pick_Up_Report_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pick_Up_Report_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Pick Up Report is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Room_Rate_Release_date_conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Rate_Release_date_conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Room_Rate_Release_date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Room_Rate_Release_date__c)) + &quot;-&quot; + CASE(
  MONTH(Room_Rate_Release_date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Room_Rate_Release_date__c)), CASE(
  MONTH(Room_Rate_Release_date__c),
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
) + &quot;-&quot; + TEXT(DAY(Room_Rate_Release_date__c)) + &quot;-&quot; + TEXT(YEAR(Room_Rate_Release_date__c))), &quot;&quot;)</formula>
    <label>Bid Release date conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Vendor_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Id__c</fullName>
    <externalId>false</externalId>
    <formula>Vendor__r.Id</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Id</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Rooming_list_due_by_conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_list_due_by_conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Rooming_list_due_by__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Rooming_list_due_by__c)) + &quot;-&quot; + CASE(
  MONTH(Rooming_list_due_by__c),
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
) + &quot;-&quot; + TEXT(YEAR(Rooming_list_due_by__c)), CASE(
  MONTH(Rooming_list_due_by__c),
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
) + &quot;-&quot; + TEXT(DAY(Rooming_list_due_by__c)) + &quot;-&quot; + TEXT(YEAR(Rooming_list_due_by__c))), &quot;&quot;)</formula>
    <label>Rooming list due by conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Record_locator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Record_locator__c</fullName>
    <externalId>false</externalId>
    <label>Record locator</label>
    <length>15</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Pending_Client_Choice__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pending_Client_Choice__c</fullName>
    <externalId>false</externalId>
    <label>Pending Client Choice</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Commission_and_Revenue_Text__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_and_Revenue_Text__c</fullName>
    <externalId>false</externalId>
    <label>Commission and Revenue Text</label>
    <length>131072</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Final_Air_Confirmation_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Air_Confirmation_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Final Air Confirmation - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Form_GCIP__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_GCIP__c</fullName>
    <externalId>false</externalId>
    <label>Form GCIP</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### GCIP_create_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_create_date__c</fullName>
    <externalId>false</externalId>
    <label>GCIP create date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### No_Pick_Up_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Pick_Up_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>No Pick Up - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### GCIP_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>GCIP is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### No_Bid_reason__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Bid_reason__c</fullName>
    <externalId>false</externalId>
    <label>No Bid reason</label>
    <length>100</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Credit_Card_Details_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Details_Id__c</fullName>
    <externalId>false</externalId>
    <formula>Credit_Card_Details__r.Id</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Credit Card Details Id</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### isHousingCloseOutAvailable__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isHousingCloseOutAvailable__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>isHousingCloseOutAvailable</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Include_in_options__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Include_in_options__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Include in options</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Date_Change_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Date_Change_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Date Change is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
### Over_Drive_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Over_Drive_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Over Drive Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Sold_out__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sold_out__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Sold out</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### OLR_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OLR_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(OLR__c), BR() + &quot;Online Rate: &quot; + OLR__c, &quot;&quot;)</formula>
    <label>OLR Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Pick_Up_Report__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Pick_Up_Report__c</fullName>
    <externalId>false</externalId>
    <label>Form Pick-Up Report</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Contract_Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Contract_Terms__c</fullName>
    <externalId>false</externalId>
    <label>Housing Contract - Terms</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
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
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### UUID_for_Landing_Page__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>UUID_for_Landing_Page__c</fullName>
    <externalId>false</externalId>
    <label>UUID for Landing Page</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rooming_list_due_by__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_list_due_by__c</fullName>
    <externalId>false</externalId>
    <label>Rooming list due by</label>
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
    <deleteConstraint>Restrict</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>true</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Sabre_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sabre_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Sabre Rate</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Production_Office_Location__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Office_Location__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Production__r.Office_Location__c)</formula>
    <label>Production Office Location</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contract_Due_Date_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Due_Date_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Contract_Due_Date__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Contract_Due_Date__c)) + &quot;-&quot; + CASE(
  MONTH(Contract_Due_Date__c),
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
) + &quot;-&quot; + TEXT(YEAR(Contract_Due_Date__c)), CASE(
  MONTH(Contract_Due_Date__c),
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
) + &quot;-&quot; + TEXT(DAY(Contract_Due_Date__c)) + &quot;-&quot; + TEXT(YEAR(Contract_Due_Date__c))), &quot;&quot;)</formula>
    <label>Internal Contract Due Date Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Pick_Up_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pick_Up_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Pick Up - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### GCIP_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>GCIP - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Contract_Date_Change_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Date_Change_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Contract Date Change - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### coVendorName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>coVendorName__c</fullName>
    <externalId>false</externalId>
    <label>coVendorName</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Trip_Details_Update_Payment_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Payment_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Trip Details Update - Payment Policy</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Rooming_List_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_List_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Rooming List - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### ContractCorrelative__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ContractCorrelative__c</fullName>
    <externalId>false</externalId>
    <label>ContractCorrelative</label>
    <precision>3</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Utilization_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Utilization - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Over_Drive_notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Over_Drive_notes__c</fullName>
    <externalId>false</externalId>
    <label>Over Drive notes</label>
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
                <fullName>Number of overdrives included __________</fullName>
                <default>false</default>
                <label>Number of overdrives included __________</label>
            </value>
            <value>
                <fullName>Additional overdrives at rate of __________</fullName>
                <default>false</default>
                <label>Additional overdrives at rate of __________</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Show_Include_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Show_Include_Rate__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Show Include Rate</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Cover_Information_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cover_Information_Conga__c</fullName>
    <externalId>false</externalId>
    <label>Cover Information_Conga</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>10</visibleLines>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Trip_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_ID__c</fullName>
    <externalId>false</externalId>
    <formula>IF(RecordType.DeveloperName == &quot;GT_Bid&quot;,GT__r.Name,IF(RecordType.DeveloperName == &quot;Freight_Bid&quot;,Freight__r.Name,IF(RecordType.DeveloperName == &quot;Air_Bid&quot;,Air__r.Name,&quot;&quot;)))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Trip ID</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rate_Agreement_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement Contact Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Client_Contract_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Contract_Date__c</fullName>
    <externalId>false</externalId>
    <label>Client Contract Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Form_Trip_Details_Update__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Trip_Details_Update__c</fullName>
    <externalId>false</externalId>
    <label>Form Trip Details Update</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rate_Agreement_Payment_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Payment_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement - Payment Policy</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Vendor_Contact_Email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Contact_Email__c</fullName>
    <externalId>false</externalId>
    <formula>HYPERLINK(&quot;&lt;a href=&apos;mailto:&quot; &amp; Vendor_Contact__r.Email &amp; &quot;&apos;&gt;&quot; &amp; Vendor_Contact__r.Email &amp; &quot;&lt;/a&gt;&quot;, Vendor_Contact__r.Email)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Contact Email</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Final_Status_Previous__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Status_Previous__c</fullName>
    <description>Field used to save the status when the &apos;Pending Update&apos; trace date is updated.</description>
    <externalId>false</externalId>
    <label>Final Status - Previous</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Deposit_Amount_per_seat__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deposit_Amount_per_seat__c</fullName>
    <externalId>false</externalId>
    <label>Deposit Amount $ (per seat)</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Rate_agreement_create_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_agreement_create_date__c</fullName>
    <externalId>false</externalId>
    <label>Rate agreement create date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Double_Driver__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Double_Driver__c</fullName>
    <externalId>false</externalId>
    <label>Double Driver</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### GCIP_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Status__c</fullName>
    <externalId>false</externalId>
    <label>GCIP Status</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Form_Status</valueSetName>
    </valueSet>
</CustomField>
```
### Fuel_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Fuel_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Fuel Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Credit_Card_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Credit Card - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Double_Driver_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Double_Driver_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Double Driver Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
### Ticketed_Confirmation_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ticketed_Confirmation_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Ticketed Confirmation - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rate_Agreement_LastModifiedDate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_LastModifiedDate__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement - Last Modified Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Gratuity_notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Gratuity_notes__c</fullName>
    <externalId>false</externalId>
    <label>Gratuity notes</label>
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
                <fullName>Please include gratuity in rate</fullName>
                <default>false</default>
                <label>Please include gratuity in rate</label>
            </value>
            <value>
                <fullName>Gratuity will be paid directly to driver</fullName>
                <default>false</default>
                <label>Gratuity will be paid directly to driver</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Deposit_Amount_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deposit_Amount_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Deposit Amount - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### isFromTournament__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isFromTournament__c</fullName>
    <externalId>false</externalId>
    <formula>NOT(ISBLANK(Housing__r.Tournament__c))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>isFromTournament</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Property_Agrees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Property_Agrees__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Property Agrees</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Internal_Contract_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Contract_Date__c</fullName>
    <externalId>false</externalId>
    <label>Internal Contract Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### FinalCorrelative__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>FinalCorrelative__c</fullName>
    <externalId>false</externalId>
    <label>FinalCorrelative</label>
    <precision>3</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Contract_Date_Change_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Date_Change_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Contract Date Change - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Utilization_Penalty_per_seat__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Penalty_per_seat__c</fullName>
    <externalId>false</externalId>
    <label>Utilization Penalty: $ (per seat)</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Utilization_Penalty_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Utilization_Penalty_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Utilization Penalty - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_End_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_End_Date__c</fullName>
    <externalId>false</externalId>
    <formula>Housing__r.Date_Out__c</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing End Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
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
### responseVendorPhone__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>responseVendorPhone__c</fullName>
    <externalId>false</externalId>
    <label>responseVendorPhone</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Rate_Agreement__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Rate_Agreement__c</fullName>
    <externalId>false</externalId>
    <label>Form Rate Agreement</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Housing_Contract__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Housing_Contract__c</fullName>
    <externalId>false</externalId>
    <label>Form Housing Contract</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Final_Choice__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Final_Choice__c</fullName>
    <externalId>false</externalId>
    <label>Form Final Choice</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### URL_Landing_Page_Close__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>URL_Landing_Page_Close__c</fullName>
    <externalId>false</externalId>
    <formula>HYPERLINK( $Setup.RoadRebelSettings__c.Community_Base_URL__c + &apos;/s/voyajer-bid-submission?lptype=close&amp;b=&apos;&amp; UUID_for_Landing_Page__c &amp;&apos;&amp;hco=&apos;&amp;Housing__c&amp;&apos;&amp;service=lodging&amp;record=&apos;&amp;Id, &apos;Submit Close Out&apos;)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>URL Landing Page Close</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Cancellation_Letter__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Cancellation_Letter__c</fullName>
    <externalId>false</externalId>
    <label>Form Cancellation Letter</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Bid_Options_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Options_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Bid Options Notes</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Dead_Head_Days_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Dead_Head_Days_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Dead Head Days Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Deposit_Due_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deposit_Due_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Deposit Due - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
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
### Rooming_list_ASAP__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rooming_list_ASAP__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Rooming list ASAP</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### GCIP_form_is_emailed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_form_is_emailed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>GCIP form is emailed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Transport_Insurance__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transport_Insurance__c</fullName>
    <externalId>false</externalId>
    <label>Transport Insurance</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
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
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Pick_Up_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pick_Up_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Pick Up - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Double_Driver_notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Double_Driver_notes__c</fullName>
    <externalId>false</externalId>
    <label>Double Driver notes</label>
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
                <fullName>Please include Double Driver in rate</fullName>
                <default>false</default>
                <label>Please include Double Driver in rate</label>
            </value>
            <value>
                <fullName>Double Driver not included</fullName>
                <default>false</default>
                <label>Double Driver not included</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Close_Out_has_been_sent_by_Vendor__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Close_Out_has_been_sent_by_Vendor__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Close Out has been sent by Vendor?</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Contracted_date_time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracted_date_time__c</fullName>
    <externalId>false</externalId>
    <label>Contracted date/time</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Rate_agreement_Created_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_agreement_Created_Date__c</fullName>
    <externalId>false</externalId>
    <label>Rate agreement - Created Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Transportation_Contract_Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Terms__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract - Terms</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Vendor_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Address__c</fullName>
    <externalId>false</externalId>
    <formula>Vendor__r.ShippingStreet &amp; BR() &amp;
Vendor__r.ShippingCity &amp; &quot;, &quot; &amp; Vendor__r.ShippingState &amp; &quot; &quot; &amp; Vendor__r.ShippingPostalCode &amp; BR() &amp;
Vendor__r.ShippingCountry</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Address</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Vendor_Contact_Phone__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Contact_Phone__c</fullName>
    <externalId>false</externalId>
    <formula>Vendor_Contact__r.Phone</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Contact Phone</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Freight_Tolls__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Tolls__c</fullName>
    <externalId>false</externalId>
    <label>Freight Tolls</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Insurance__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Insurance__c</fullName>
    <externalId>false</externalId>
    <label>Insurance</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### ORL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ORL__c</fullName>
    <externalId>false</externalId>
    <label>ORL</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Form_Create_GCIP_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Create_GCIP_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Form Create GCIP Last Send Date</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Total_Miles_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Miles_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Total Miles Notes</label>
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
                <fullName>Total Miles ______</fullName>
                <default>false</default>
                <label>Total Miles ______</label>
            </value>
            <value>
                <fullName>Not limit</fullName>
                <default>false</default>
                <label>Not limit</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Credit_Card_Details__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Details__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Credit Card Details</label>
    <referenceTo>Credit_Card__c</referenceTo>
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Rate_agreement_last_modified_date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_agreement_last_modified_date__c</fullName>
    <externalId>false</externalId>
    <label>Rate agreement last modified date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Commission_Revenue__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Revenue__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Commission Revenue</label>
    <referenceTo>Revenue__c</referenceTo>
    <relationshipLabel>Bid Commission</relationshipLabel>
    <relationshipName>BidCommission</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contract_to_Client_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_to_Client_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Contract to Client - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Form_Transportation_Contract__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Transportation_Contract__c</fullName>
    <externalId>false</externalId>
    <label>Form Transportation Contract</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Use_Check__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Use_Check__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Use Check</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### isHousingCloseOutEditable__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isHousingCloseOutEditable__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>isHousingCloseOutEditable</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Parking_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Parking_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Parking Notes</label>
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
                <fullName>Parking is an additional cost</fullName>
                <default>false</default>
                <label>Parking is an additional cost</label>
            </value>
            <value>
                <fullName>Parking is included</fullName>
                <default>false</default>
                <label>Parking is included</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Rate_Agreement_Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Terms__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement - Terms</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>20</visibleLines>
</CustomField>
```
### Bid_request_date_time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_request_date_time__c</fullName>
    <externalId>false</externalId>
    <label>Bid request date/time</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### QB_Error__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>QB_Error__c</fullName>
    <externalId>false</externalId>
    <label>QB Error</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
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
    <relationshipLabel>Bid</relationshipLabel>
    <relationshipName>Bid</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contract_Client_Signed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Client_Signed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Contract Client Signed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Final_Contract_Last_Send_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Final_Contract_Last_Send_By__c</fullName>
    <externalId>false</externalId>
    <label>Final Contract - Last Send By</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Is_Inside_Cutoff__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Is_Inside_Cutoff__c</fullName>
    <externalId>false</externalId>
    <formula>IF(RecordType.Name != &apos;Housing Bid&apos;,true,IF(Housing_Date_In__c &gt; DATE(2020,11,01),true,false))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Is Inside Cutoff</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Room_Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Description__c</fullName>
    <externalId>false</externalId>
    <label>Room Description</label>
    <length>1000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Trip_Details_Update_Created_By__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Trip_Details_Update_Created_By__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Trip Details Update - Created By</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Bid6</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Counter_Needed_Last_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Counter_Needed_Last_Send_Date__c</fullName>
    <externalId>false</externalId>
    <label>Counter Needed - Last Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Form_Deposit_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Deposit_Due__c</fullName>
    <externalId>false</externalId>
    <label>Form Deposit Due</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contracting_Back_End_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Back_End_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Contracting Back-End Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>ContractedBids</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Client_Names_Final_Payment_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client_Names_Final_Payment_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Client_Names_Final_Payment__c), IF(ISPICKVAL($User.Housing_Preference__c, &quot;RRE&quot;), TEXT(DAY(Client_Names_Final_Payment__c)) + &quot;-&quot; + CASE(
  MONTH(Client_Names_Final_Payment__c),
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
) + &quot;-&quot; + TEXT(YEAR(Client_Names_Final_Payment__c)), CASE(
  MONTH(Client_Names_Final_Payment__c),
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
) + &quot;-&quot; + TEXT(DAY(Client_Names_Final_Payment__c)) + &quot;-&quot; + TEXT(YEAR(Client_Names_Final_Payment__c))), &quot;&quot;)</formula>
    <label>Client Names &amp; Final Payment Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Wait_Time__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Wait_Time__c</fullName>
    <externalId>false</externalId>
    <label>Wait Time</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
</CustomField>
```
### Housing_Contract_First_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Contract_First_Send_Date__c</fullName>
    <description>First Conga Send Date</description>
    <externalId>false</externalId>
    <label>Housing Contract - First Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Production_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_ID__c</fullName>
    <description>Used on Conga Button Housing Contract</description>
    <externalId>false</externalId>
    <formula>Production__r.Id</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Production ID</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### NAV_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>NAV_ID__c</fullName>
    <externalId>false</externalId>
    <label>NAV_ID</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Internal_Notes_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Internal_Notes_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Internal Notes NAV</label>
    <length>1000</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Freight_Tolls_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight_Tolls_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Freight Tolls Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Form_GT_GCIP__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_GT_GCIP__c</fullName>
    <externalId>false</externalId>
    <label>Form GT GCIP</label>
    <length>20</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Driver_Lodging__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Driver_Lodging__c</fullName>
    <externalId>false</externalId>
    <label>Driver Lodging</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Included_Excluded</valueSetName>
    </valueSet>
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
### Deactivate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deactivate__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Deactivate</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Rate_Agreement_First_Send_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_First_Send_Date__c</fullName>
    <description>First Conga Send Date</description>
    <externalId>false</externalId>
    <label>Rate Agreement - First Send Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### coVendorTitle__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>coVendorTitle__c</fullName>
    <externalId>false</externalId>
    <label>coVendorTitle</label>
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
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Live_Days_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Live_Days_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Live Days Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### responseVendorName__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>responseVendorName__c</fullName>
    <externalId>false</externalId>
    <label>responseVendorName</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Transportation_Contract_Payment_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Transportation_Contract_Payment_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Transportation Contract - Payment Policy</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Form_Credit_Card_Change__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Form_Credit_Card_Change__c</fullName>
    <externalId>false</externalId>
    <label>Form Credit Card Change</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rate_Agreement_Cancellation_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_Agreement_Cancellation_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Rate Agreement - Cancellation Policy</label>
    <length>32768</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Invoiced_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoiced_Date__c</fullName>
    <externalId>false</externalId>
    <label>Invoiced Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Conga_Update_Fields__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Conga_Update_Fields__c</fullName>
    <externalId>false</externalId>
    <label>Conga Update Fields</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### No_Rooms_PU_is_uploaded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>No_Rooms_PU_is_uploaded__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>No Rooms PU is uploaded</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```

---
layout: default
title: Activity
parent: objects
---
# Metadata Type
CustomObject

# Name
Activity
## Fields
### rcsfl__hvs_disposition__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__hvs_disposition__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>HVS Disposition</label>
    <required>false</required>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Call Back Later</fullName>
                <default>false</default>
                <label>Call Back Later</label>
            </value>
            <value>
                <fullName>Left Voicemail</fullName>
                <default>false</default>
                <label>Left Voicemail</label>
            </value>
            <value>
                <fullName>Meaningful Connect</fullName>
                <default>false</default>
                <label>Meaningful Connect</label>
            </value>
            <value>
                <fullName>Not Interested</fullName>
                <default>false</default>
                <label>Not Interested</label>
            </value>
            <value>
                <fullName>Unqualified</fullName>
                <default>false</default>
                <label>Unqualified</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### IsForStayOrTrip__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsForStayOrTrip__c</fullName>
    <defaultValue>false</defaultValue>
    <description>Used for create traces from stay or trip tab.</description>
    <externalId>false</externalId>
    <label>IsForStayOrTrip</label>
    <type>Checkbox</type>
</CustomField>
```
### rcsfl__CALL_UUID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__CALL_UUID__c</fullName>
    <deprecated>false</deprecated>
    <externalId>true</externalId>
    <label>CALL_UUID</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### IsForCloseOut__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsForCloseOut__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>IsForCloseOut</label>
    <type>Checkbox</type>
</CustomField>
```
### Service_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Id__c</fullName>
    <externalId>false</externalId>
    <label>Service Id</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Task_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Task_Type__c</fullName>
    <externalId>false</externalId>
    <label>Task Type</label>
    <required>false</required>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Tournament Status Trace</fullName>
                <default>false</default>
                <label>Tournament Status Trace</label>
            </value>
            <value>
                <fullName>Housing Status Trace</fullName>
                <default>false</default>
                <label>Housing Status Trace</label>
            </value>
            <value>
                <fullName>Ground Status Trace</fullName>
                <default>false</default>
                <label>Ground Status Trace</label>
            </value>
            <value>
                <fullName>Freight Status Trace</fullName>
                <default>false</default>
                <label>Freight Status Trace</label>
            </value>
            <value>
                <fullName>Air Status Trace</fullName>
                <default>false</default>
                <label>Air Status Trace</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Contracting_Coordinator_Final__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Coordinator_Final__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <description>This will use the PA and the Contracting Back End Coordinator to decide who the in charge coordinator is.</description>
    <externalId>false</externalId>
    <label>Contracting Coordinator Final</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Activities</relationshipName>
    <required>false</required>
    <type>Lookup</type>
</CustomField>
```
### rcsfl__RC_Logging_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__RC_Logging_Type__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>RC Logging Type</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### rcsfl__Recording_Information__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__Recording_Information__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Recording Information</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Bid_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_Id__c</fullName>
    <externalId>false</externalId>
    <label>Bid Id</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### rcsfl__key__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__key__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>key</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contract_Task__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Task__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Contract Task</label>
    <type>Checkbox</type>
</CustomField>
```
### GCIP_Additional_Information__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Additional_Information__c</fullName>
    <externalId>false</externalId>
    <label>GCIP Additional Information</label>
    <required>false</required>
    <type>TextArea</type>
</CustomField>
```
### Calc_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Calc_Coordinator__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Calc Coordinator</label>
    <type>Checkbox</type>
</CustomField>
```
### IsForAudit__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsForAudit__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>IsForAudit</label>
    <type>Checkbox</type>
</CustomField>
```
### rcsfl__CALL_UNIQUE_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__CALL_UNIQUE_ID__c</fullName>
    <caseSensitive>false</caseSensitive>
    <deprecated>false</deprecated>
    <externalId>true</externalId>
    <label>CALL_UNIQUE_ID</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>true</unique>
</CustomField>
```
### Primary_Contract_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Contract_Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Primary Contract Coordinator</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Primary_Service_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Service_Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Primary Service Coordinator</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Bid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid__c</fullName>
    <externalId>false</externalId>
    <label>Bid</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Primary_Service_Coordinator_Final__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Service_Coordinator_Final__c</fullName>
    <externalId>false</externalId>
    <label>Primary Service Coordinator Final</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
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
    <precision>2</precision>
    <required>false</required>
    <scale>0</scale>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### CASESAFEID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CASESAFEID__c</fullName>
    <externalId>false</externalId>
    <formula>CASESAFEID(Id)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>CASESAFEID</label>
    <required>false</required>
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
    <type>Date</type>
</CustomField>
```
### Service_Backend_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Backend_Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Service Backend Coordinator</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### rcsfl__external_whoid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__external_whoid__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>external_whoid</label>
    <length>255</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Priority__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Priority__c</fullName>
    <externalId>false</externalId>
    <label>Priority</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### rcsfl__Call_Recording__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>rcsfl__Call_Recording__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <formula>IF(NOT(ISBLANK(rcsfl__Recording_Information__c)),HYPERLINK(&quot;http://apps.ringcentral.com/integrations/recording/test/index.html?id=&quot;+ rcsfl__Recording_Information__c, &quot;http://apps.ringcentral.com/integrations/recording/test/index.html?id=&quot; + rcsfl__Recording_Information__c),NULL)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Call Recording</label>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contracting_Back_End_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contracting_Back_End_Coordinator__c</fullName>
    <externalId>false</externalId>
    <label>Contracting Back End Coordinator</label>
    <length>255</length>
    <required>false</required>
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
    <label>NAV ID</label>
    <length>30</length>
    <required>false</required>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

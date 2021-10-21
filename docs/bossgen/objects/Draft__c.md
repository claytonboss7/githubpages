---
layout: default
title: Draft__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Draft__c
## Fields
### Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Terms__c</fullName>
    <externalId>false</externalId>
    <label>Terms</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### Closing__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Closing__c</fullName>
    <externalId>false</externalId>
    <label>Closing</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Attention__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Attention__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Attention</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Drafts</relationshipLabel>
    <relationshipName>Drafts</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### GCIP_Arrival__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Arrival__c</fullName>
    <externalId>false</externalId>
    <label>GCIP Arrival</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Production_Assoc_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Assoc_Type__c</fullName>
    <externalId>false</externalId>
    <label>Production_Assoc Type</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
### BCC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>BCC__c</fullName>
    <externalId>false</externalId>
    <label>BCC</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Body__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Body__c</fullName>
    <externalId>false</externalId>
    <label>Body</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Html</type>
    <visibleLines>25</visibleLines>
</CustomField>
```
### CC__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CC__c</fullName>
    <externalId>false</externalId>
    <label>CC</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Payment_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Payment_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Payment Policy</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Production_Assoc_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Assoc_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <label>Production Assoc Contact Id</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Cancellation_Policy__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Cancellation_Policy__c</fullName>
    <externalId>false</externalId>
    <label>Cancellation Policy</label>
    <length>32768</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### GCIP_Departure__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GCIP_Departure__c</fullName>
    <externalId>false</externalId>
    <label>GCIP Departure</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Salutation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Salutation__c</fullName>
    <externalId>false</externalId>
    <label>Salutation</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Credit_Card_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Id__c</fullName>
    <externalId>false</externalId>
    <label>Credit Card Id</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Primary_Contact_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Contact_Id__c</fullName>
    <externalId>false</externalId>
    <label>Primary Contact Id</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Subject__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Subject__c</fullName>
    <externalId>false</externalId>
    <label>Subject</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

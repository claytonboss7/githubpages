---
layout: default
title: Vendor_Vendor__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Vendor_Vendor__c
## Fields
### Vendor_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_City__c</fullName>
    <externalId>false</externalId>
    <formula>Vendor__r.City__r.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor City</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Address__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(Housing_Provider__r.ShippingStreet),&quot;&quot;,Housing_Provider__r.ShippingStreet &amp; BR()) &amp; 
Housing_Provider__r.ShippingCity &amp; &quot;, &quot; &amp; Housing_Provider__r.ShippingState &amp; &quot; &quot; &amp; Housing_Provider__r.ShippingPostalCode &amp; BR() &amp; 
Housing_Provider__r.ShippingCountry</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Housing Address</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Vendor_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Type__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Vendor__r.Vendor_Type__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Vendor_Full_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Vendor_Full_Address__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISBLANK(Vendor__r.ShippingStreet),&quot;&quot;,Vendor__r.ShippingStreet &amp; BR()) &amp; 
Vendor__r.ShippingCity &amp; &quot;, &quot; &amp; Vendor__r.ShippingState &amp; &quot; &quot; &amp; Vendor__r.ShippingPostalCode &amp; BR() &amp; 
Vendor__r.ShippingCountry</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Vendor Full Address</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Housing_Provider__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing_Provider__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Housing Provider</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Corporate Housing Vendors</relationshipLabel>
    <relationshipName>Vendor_Vendor</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Provider_Phone__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Provider_Phone__c</fullName>
    <externalId>false</externalId>
    <formula>Housing_Provider__r.Phone</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Provider Phone</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Provider_Website__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Provider_Website__c</fullName>
    <externalId>false</externalId>
    <formula>Housing_Provider__r.Website</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Provider Website</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipLabel>Corporate Housing Providers</relationshipLabel>
    <relationshipName>Vendor_Vendor1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

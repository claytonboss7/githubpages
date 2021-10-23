---
layout: default
title: Credit_Card__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Credit_Card__c
## Fields
### Billing_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Billing_Address__c</fullName>
    <externalId>false</externalId>
    <label>Billing Address</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Expiration_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Expiration_Date__c</fullName>
    <externalId>false</externalId>
    <label>Expiration Date</label>
    <length>5</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Purpose__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Purpose__c</fullName>
    <externalId>false</externalId>
    <label>Purpose</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Air Only</fullName>
                <default>false</default>
                <label>Air Only</label>
            </value>
            <value>
                <fullName>All</fullName>
                <default>false</default>
                <label>All</label>
            </value>
            <value>
                <fullName>Deposit</fullName>
                <default>false</default>
                <label>Deposit</label>
            </value>
            <value>
                <fullName>Final Payment</fullName>
                <default>false</default>
                <label>Final Payment</label>
            </value>
            <value>
                <fullName>Freight Only</fullName>
                <default>false</default>
                <label>Freight Only</label>
            </value>
            <value>
                <fullName>Ground Transportation Only</fullName>
                <default>false</default>
                <label>Ground Transportation Only</label>
            </value>
            <value>
                <fullName>Guarantee</fullName>
                <default>false</default>
                <label>Guarantee</label>
            </value>
            <value>
                <fullName>Housing Only</fullName>
                <default>false</default>
                <label>Housing Only</label>
            </value>
            <value>
                <fullName>Secondary</fullName>
                <default>false</default>
                <label>Secondary</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Credit_Card_Full_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Full_Name__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Credit_card_number__c) &amp; &quot; - &quot; &amp;  IF(!ISBLANK(Contact__r.FirstName),Contact__r.FirstName &amp; &quot; &quot;,&quot;&quot;) + Contact__r.LastName</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Credit Card Full Name</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Card_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Card_Type__c</fullName>
    <externalId>false</externalId>
    <label>Card Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>AMEX</fullName>
                <default>false</default>
                <label>AMEX</label>
            </value>
            <value>
                <fullName>DinersClub</fullName>
                <default>false</default>
                <label>DinersClub</label>
            </value>
            <value>
                <fullName>Discover</fullName>
                <default>false</default>
                <label>Discover</label>
            </value>
            <value>
                <fullName>MasterCard</fullName>
                <default>false</default>
                <label>MasterCard</label>
            </value>
            <value>
                <fullName>Visa</fullName>
                <default>false</default>
                <label>Visa</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Name_on_Card__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Name_on_Card__c</fullName>
    <externalId>false</externalId>
    <label>Name on Card</label>
    <length>100</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <relationshipLabel>Credit Cards</relationshipLabel>
    <relationshipName>Credit_Cards</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Credit_card_number_conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_card_number_conga__c</fullName>
    <externalId>false</externalId>
    <formula>TEXT(Credit_card_number__c)</formula>
    <label>Credit card number conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CID__c</fullName>
    <externalId>false</externalId>
    <label>CID</label>
    <length>4</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Credit_card_number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_card_number__c</fullName>
    <externalId>false</externalId>
    <label>Credit card number</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <securityClassification>Confidential</securityClassification>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
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
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Credit_Card_Number_Encrypted__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Credit_Card_Number_Encrypted__c</fullName>
    <externalId>false</externalId>
    <label>Credit Card Number Encrypted</label>
    <length>19</length>
    <maskChar>X</maskChar>
    <maskType>creditCard</maskType>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>EncryptedText</type>
</CustomField>
```

---
layout: default
title: Revenue__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Revenue__c
## Fields
### Commission__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission__c</fullName>
    <externalId>false</externalId>
    <label>Commission $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Rate_currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_currency__c</fullName>
    <externalId>false</externalId>
    <label>Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Rebate_to_RR_due_lookup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_to_RR_due_lookup__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Rebate to RR due</label>
    <referenceTo>Revenue__c</referenceTo>
    <relationshipLabel>Revenue (Rebate to RR due)</relationshipLabel>
    <relationshipName>Revenue1</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### For_Dollar__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>For_Dollar__c</fullName>
    <externalId>false</externalId>
    <label>For $</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <controllingField>Charge_Type__c</controllingField>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Room Nights(housing)</fullName>
                <default>false</default>
                <label>Room Nights(housing)</label>
            </value>
            <value>
                <fullName>Per Room (Unit-Housing)</fullName>
                <default>false</default>
                <label>Per Room (Unit-Housing)</label>
            </value>
            <value>
                <fullName>Flat Fee – All (Corp housing)</fullName>
                <default>false</default>
                <label>Flat Fee – All (Corp housing)</label>
            </value>
            <value>
                <fullName>Flat Fee per month (Corp housing)</fullName>
                <default>false</default>
                <label>Flat Fee per month (Corp housing)</label>
            </value>
            <value>
                <fullName>Per Ticket (Air)</fullName>
                <default>false</default>
                <label>Per Ticket (Air)</label>
            </value>
            <value>
                <fullName>Per Ticket – Per name (air)</fullName>
                <default>false</default>
                <label>Per Ticket – Per name (air)</label>
            </value>
            <value>
                <fullName>Per Ticket – Ticket exchange (air)</fullName>
                <default>false</default>
                <label>Per Ticket – Ticket exchange (air)</label>
            </value>
            <value>
                <fullName>Per Ticket – Name change (air)</fullName>
                <default>false</default>
                <label>Per Ticket – Name change (air)</label>
            </value>
            <value>
                <fullName>Per Ticket – Debit Memos (air)</fullName>
                <default>false</default>
                <label>Per Ticket – Debit Memos (air)</label>
            </value>
            <value>
                <fullName>Per Ticket – Deviations (air)</fullName>
                <default>false</default>
                <label>Per Ticket – Deviations (air)</label>
            </value>
        </valueSetDefinition>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Room Nights(housing)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Room (Unit-Housing)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Flat Fee – All (Corp housing)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Flat Fee per month (Corp housing)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Ticket (Air)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Ticket – Per name (air)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Ticket – Ticket exchange (air)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Ticket – Name change (air)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Ticket – Debit Memos (air)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Amount</controllingFieldValue>
            <valueName>Per Ticket – Deviations (air)</valueName>
        </valueSettings>
    </valueSet>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Item__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Item__c</fullName>
    <externalId>false</externalId>
    <label>Item</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Room Nights</fullName>
                <default>false</default>
                <label>Room Nights</label>
            </value>
            <value>
                <fullName>Corporate</fullName>
                <default>false</default>
                <label>Corporate</label>
            </value>
            <value>
                <fullName>Team Rebate</fullName>
                <default>false</default>
                <label>Team Rebate</label>
            </value>
            <value>
                <fullName>Nights</fullName>
                <default>false</default>
                <label>Nights</label>
            </value>
            <value>
                <fullName>Freight</fullName>
                <default>false</default>
                <label>Freight</label>
            </value>
            <value>
                <fullName>Motorcoach</fullName>
                <default>false</default>
                <label>Motorcoach</label>
            </value>
            <value>
                <fullName>Sedan/Limo</fullName>
                <default>false</default>
                <label>Sedan/Limo</label>
            </value>
            <value>
                <fullName>Tax/Shuttle</fullName>
                <default>false</default>
                <label>Tax/Shuttle</label>
            </value>
            <value>
                <fullName>Individual Rooms</fullName>
                <default>false</default>
                <label>Individual Rooms</label>
            </value>
            <value>
                <fullName>Comp</fullName>
                <default>false</default>
                <label>Comp</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### VAT_Number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT_Number__c</fullName>
    <externalId>false</externalId>
    <label>VAT Number</label>
    <length>50</length>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### City_Tax_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(City_Tax_Rate__c) &amp;&amp; City_Tax_Rate__c != 0, Currency_Symbol__c + TEXT(City_Tax_Rate__c) + &apos;, &apos;, IF(!ISNULL(City_Tax_Rate_percent__c) &amp;&amp; City_Tax_Rate_percent__c != 0, TEXT(City_Tax_Rate_percent__c * 100) + &quot; %, &quot;, &quot;&quot;)) + IF(City_Tax__c, &quot;Included&quot;, &quot;Not Included&quot;) + &quot; &quot; + TEXT(City_Tax_Type__c)</formula>
    <label>City Tax</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Service_Fees_Percent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Fees_Percent__c</fullName>
    <externalId>false</externalId>
    <label>Service Fees %</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Conga_Payments_Accepted__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Conga_Payments_Accepted__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISPICKVAL(Bid__r.Vendor__r.Visa_Accepted__c, &apos;Yes&apos;), &apos;Visa&apos; + IF(!ISNULL(Bid__r.Vendor__r.Visa_Surcharge__c), &apos; (&apos; + TEXT(Bid__r.Vendor__r.Visa_Surcharge__c * 100) + &apos;%)&apos;, &apos;&apos;)  , &apos;&apos;) + 
IF(ISPICKVAL(Bid__r.Vendor__r.Master_Card_Accepted__c, &apos;Yes&apos;), &apos;, Master Card&apos; + IF(!ISNULL(Bid__r.Vendor__r.Master_Card_Surcharge__c), &apos; (&apos; + TEXT(Bid__r.Vendor__r.Master_Card_Surcharge__c * 100) + &apos;%)&apos;, &apos;&apos;)  , &apos;&apos;) + 
IF(ISPICKVAL(Bid__r.Vendor__r.American_Express_Accepted__c, &apos;Yes&apos;), &apos;, American Express&apos; + IF(!ISNULL(Bid__r.Vendor__r.American_Express_Surcharge__c), &apos; (&apos; + TEXT(Bid__r.Vendor__r.American_Express_Surcharge__c * 100) + &apos;%)&apos;, &apos;&apos;)  , &apos;&apos;) + 
IF(ISPICKVAL(Bid__r.Vendor__r.Discover_Accepted__c, &apos;Yes&apos;), &apos;, Discover&apos; + IF(!ISNULL(Bid__r.Vendor__r.Discover_Surcharge__c), &apos; (&apos; + TEXT(Bid__r.Vendor__r.Discover_Surcharge__c * 100) + &apos;%)&apos;, &apos;&apos;)  , &apos;&apos;) + 
IF(ISPICKVAL(Bid__r.Vendor__r.Check_Payment__c, &apos;Yes&apos;), &apos;, Check&apos;, &apos;&apos;) + 
IF(ISPICKVAL(Bid__r.Vendor__r.Wire_Transfer_Bank_Draft__c, &apos;Yes&apos;), &apos;, Wire Transfer/Bank Draft&apos;, &apos;&apos;)</formula>
    <label>Payments Accepted</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rebate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate__c</fullName>
    <externalId>false</externalId>
    <label>Rebate %</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### of_vehicles__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>of_vehicles__c</fullName>
    <externalId>false</externalId>
    <label># of vehicles</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Invoice_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoice_Date__c</fullName>
    <externalId>false</externalId>
    <label>Invoice Date</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Sign_email__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sign_email__c</fullName>
    <externalId>false</externalId>
    <label>Sign email</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Email</type>
    <unique>false</unique>
</CustomField>
```
### Rebate_Per__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_Per__c</fullName>
    <externalId>false</externalId>
    <label>Rebate Per</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Person</fullName>
                <default>false</default>
                <label>Person</label>
            </value>
            <value>
                <fullName>Night</fullName>
                <default>false</default>
                <label>Night</label>
            </value>
            <value>
                <fullName>TBD</fullName>
                <default>false</default>
                <label>TBD</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Tax_Included__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tax_Included__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Tax Included</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### VAT_Rate_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT_Rate_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(VAT_Rate__c) &amp;&amp; VAT_Rate__c != 0, TEXT(VAT_Rate__c * 100), &quot; &quot;) + &quot;%&quot;</formula>
    <label>VAT Rate</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Base_Cost__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Base_Cost__c</fullName>
    <externalId>false</externalId>
    <label>Base Cost $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Room_Nights__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Nights__c</fullName>
    <externalId>false</externalId>
    <label>Room Nights</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Does_this_match_amount_on_pick_up_report__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Does_this_match_amount_on_pick_up_report__c</fullName>
    <externalId>false</externalId>
    <label>Does this match amount on pick up report</label>
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
### Total_Price_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Price_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Total Price - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Total_Taxes_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Taxes_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Total Taxes - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Breakfast_Rate_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Breakfast_Rate_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Breakfast_Rate__c) &amp;&amp; Breakfast_Rate__c != 0, Currency_Symbol__c + TEXT(Breakfast_Rate__c), &quot;&quot;)</formula>
    <label>Breakfast Rate</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Breakfast_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Breakfast_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Breakfast Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Bid_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid_ID__c</fullName>
    <externalId>false</externalId>
    <formula>Bid__r.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Bid ID</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Close_Out_Reference__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Close_Out_Reference__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Close Out Reference</label>
    <referenceTo>Revenue__c</referenceTo>
    <relationshipLabel>Revenue (Close Out Reference)</relationshipLabel>
    <relationshipName>CommunitySign</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Breakfast__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Breakfast__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Breakfast</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Tax_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tax_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Tax__c) &amp;&amp; Tax__c != 0, TEXT(Tax__c * 100) + &quot;%&quot;, &quot;&quot;)</formula>
    <label>Tax</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Monthly_Pickup_Rebate_Created__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Monthly_Pickup_Rebate_Created__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Monthly Pickup Rebate Created</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### City_Tax_Rate_percent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax_Rate_percent__c</fullName>
    <externalId>false</externalId>
    <label>City Tax Rate %</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### City_Tax__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>City Tax</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Deviation__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deviation__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Deviation</label>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Revenue</relationshipLabel>
    <relationshipName>Revenue</relationshipName>
    <required>false</required>
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
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Percentage</fullName>
                <default>false</default>
                <label>Percentage</label>
            </value>
            <value>
                <fullName>Amount</fullName>
                <default>false</default>
                <label>Amount</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Rebate_Note__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_Note__c</fullName>
    <externalId>false</externalId>
    <label>Rebate Note</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### VAT_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(VAT_Rate__c) &amp;&amp; VAT_Rate__c != 0, TEXT(VAT_Rate__c * 100) + &quot;%, &quot;, &quot;&quot;) + IF(VAT__c, &quot;Included&quot;, &quot;Not Included&quot;)</formula>
    <label>VAT</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### For_Percent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>For_Percent__c</fullName>
    <externalId>false</externalId>
    <label>For %</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <controllingField>Charge_Type__c</controllingField>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>F&amp;B (housing)</fullName>
                <default>false</default>
                <label>F&amp;B (housing)</label>
            </value>
            <value>
                <fullName>Base Rate (GT)</fullName>
                <default>false</default>
                <label>Base Rate (GT)</label>
            </value>
            <value>
                <fullName>Base Rate (Freight)</fullName>
                <default>false</default>
                <label>Base Rate (Freight)</label>
            </value>
            <value>
                <fullName>Room Nights x Rate (housing)</fullName>
                <default>false</default>
                <label>Room Nights x Rate (housing)</label>
            </value>
        </valueSetDefinition>
        <valueSettings>
            <controllingFieldValue>Percent</controllingFieldValue>
            <valueName>F&amp;B (housing)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Percent</controllingFieldValue>
            <valueName>Base Rate (GT)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Percent</controllingFieldValue>
            <valueName>Base Rate (Freight)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Percent</controllingFieldValue>
            <valueName>Room Nights x Rate (housing)</valueName>
        </valueSettings>
    </valueSet>
</CustomField>
```
### VAT__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>VAT</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### QB_Item_Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>QB_Item_Description__c</fullName>
    <externalId>false</externalId>
    <label>QB Item Description</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Transportation Department Services</fullName>
                <default>false</default>
                <label>Transportation Department Services</label>
            </value>
            <value>
                <fullName>Transportation of equipment/baggage</fullName>
                <default>false</default>
                <label>Transportation of equipment/baggage</label>
            </value>
            <value>
                <fullName>Commission for Coach Transportation</fullName>
                <default>false</default>
                <label>Commission for Coach Transportation</label>
            </value>
            <value>
                <fullName>Arrange for Driver &amp; Transportation</fullName>
                <default>false</default>
                <label>Arrange for Driver &amp; Transportation</label>
            </value>
            <value>
                <fullName>Arrange for taxi/shuttle services</fullName>
                <default>false</default>
                <label>Arrange for taxi/shuttle services</label>
            </value>
            <value>
                <fullName>Complimentary room night</fullName>
                <default>false</default>
                <label>Complimentary room night</label>
            </value>
            <value>
                <fullName>Corporate Room night</fullName>
                <default>false</default>
                <label>Corporate Room night</label>
            </value>
            <value>
                <fullName>Room reservations for individuals</fullName>
                <default>false</default>
                <label>Room reservations for individuals</label>
            </value>
            <value>
                <fullName>Commissions for group housing</fullName>
                <default>false</default>
                <label>Commissions for group housing</label>
            </value>
            <value>
                <fullName>Rebate for housing</fullName>
                <default>false</default>
                <label>Rebate for housing</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Sign_name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sign_name__c</fullName>
    <externalId>false</externalId>
    <label>Sign name</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Sign_Phone__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sign_Phone__c</fullName>
    <externalId>false</externalId>
    <label>Sign Phone</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
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
    <type>Picklist</type>
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
                <fullName>Chauffeaured</fullName>
                <default>false</default>
                <label>Chauffeaured</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### VAT_Included_in_Total__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT_Included_in_Total__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Included in Total</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Currency_Symbol__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Currency_Symbol__c</fullName>
    <externalId>false</externalId>
    <label>Currency Symbol</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Stay_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Stay_ID__c</fullName>
    <externalId>false</externalId>
    <label>Stay ID</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Commission_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISPICKVAL(Commission_Type__c, &quot;Amount&quot;),
			IF(!ISNULL(Commission__c) &amp;&amp; Commission__c != 0, IF(Bid__r.is_Vendor_European__c, &quot;€&quot;, &quot;$&quot;) + TEXT(Commission__c), &quot;&quot;), 
			IF(!ISNULL(Commission_Percent__c) &amp;&amp; Commission_Percent__c != 0, TEXT(Commission_Percent__c * 100) + &quot;%&quot;, &quot;&quot;)
		)</formula>
    <label>Commission</label>
    <required>false</required>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Tax_Included_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tax_Included_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(Tax_Included__c, &apos;Included&apos;, &apos;Excluded&apos;)</formula>
    <label>Tax Included Conga</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Total_Price__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Price__c</fullName>
    <externalId>false</externalId>
    <label>Total Price $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Gratuity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Gratuity__c</fullName>
    <externalId>false</externalId>
    <label>Gratuity $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Rebate_For__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_For__c</fullName>
    <externalId>false</externalId>
    <label>Rebate For</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Client</fullName>
                <default>false</default>
                <label>Client</label>
            </value>
            <value>
                <fullName>Road Rebel</fullName>
                <default>false</default>
                <label>Road Rebel</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Record_Locator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Record_Locator__c</fullName>
    <externalId>false</externalId>
    <label>Record Locator</label>
    <length>50</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rebate_invoiced_Amount__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_invoiced_Amount__c</fullName>
    <externalId>false</externalId>
    <label>Rebate invoiced Amount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Base_Rate_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Base_Rate_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Base Rate - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tax__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tax__c</fullName>
    <externalId>false</externalId>
    <label>Tax %</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Rebate_to_client_due_lookup__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_to_client_due_lookup__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Rebate to client due</label>
    <referenceTo>Revenue__c</referenceTo>
    <relationshipLabel>Revenue</relationshipLabel>
    <relationshipName>Revenue</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Client__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Client__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Client</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Company</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Revenue (Client)</relationshipLabel>
    <relationshipName>Revenue_Client</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### QB_Amount__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>QB_Amount__c</fullName>
    <externalId>false</externalId>
    <formula>IF(ISPICKVAL(Commission_Type__c , &quot;Percentage&quot;), Commission_Per_Room__c, Commission__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>QB Amount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Room Type</label>
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Revenue</relationshipLabel>
    <relationshipName>Revenue</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Indicate_Dates__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Indicate_Dates__c</fullName>
    <externalId>false</externalId>
    <label>Indicate Dates</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Invoice_Amount__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoice_Amount__c</fullName>
    <externalId>false</externalId>
    <label>Invoice Amount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Revenue</relationshipLabel>
    <relationshipName>Revenue</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Invoice_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoice_Rate__c</fullName>
    <externalId>false</externalId>
    <label>Invoice Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
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
    <relationshipName>Rate_Commission</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Commission_Percent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Percent__c</fullName>
    <externalId>false</externalId>
    <label>Commission %</label>
    <precision>5</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Charter__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Charter__c</fullName>
    <externalId>false</externalId>
    <label>Charter #</label>
    <length>200</length>
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
    <type>DateTime</type>
</CustomField>
```
### Fee_Percent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Fee_Percent__c</fullName>
    <externalId>false</externalId>
    <label>Fee %</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Do_you_need_invoice_sent__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Do_you_need_invoice_sent__c</fullName>
    <externalId>false</externalId>
    <label>Do you need invoice sent?</label>
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
### Rebate_currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_currency__c</fullName>
    <externalId>false</externalId>
    <label>Rebate $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Surcharge__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Surcharge__c</fullName>
    <externalId>false</externalId>
    <label>Surcharge $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Invoice_Units__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoice_Units__c</fullName>
    <externalId>false</externalId>
    <label>Invoice Units</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate__c</fullName>
    <externalId>false</externalId>
    <label>Rate %</label>
    <precision>5</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
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
### City_Tax_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax_Rate__c</fullName>
    <externalId>false</externalId>
    <label>City Tax Rate $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### of_seats__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>of_seats__c</fullName>
    <externalId>false</externalId>
    <label># of seats</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### City_Tax_Rate_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax_Rate_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>Currency_Symbol__c + IF(!ISNULL(City_Tax_Rate__c) &amp;&amp; City_Tax_Rate__c != 0, TEXT(City_Tax_Rate__c), &quot;&quot;)</formula>
    <label>City Tax Rate</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Invoice_Description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoice_Description__c</fullName>
    <externalId>false</externalId>
    <formula>IF(CONTAINS(RecordType.Name,&quot;Freight&quot;),&quot;&quot;,&quot;Vehicle Count: &quot; &amp; TEXT(of_vehicles__c) &amp; &quot;;&quot; &amp;  Charter__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Invoice Description</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### City_Tax_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax_Type__c</fullName>
    <externalId>false</externalId>
    <label>City Tax Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>No City Tax</fullName>
                <default>false</default>
                <label>No City Tax</label>
            </value>
            <value>
                <fullName>Per Person Per Night</fullName>
                <default>false</default>
                <label>Per Person Per Night</label>
            </value>
            <value>
                <fullName>Per Room Per Night</fullName>
                <default>false</default>
                <label>Per Room Per Night</label>
            </value>
            <value>
                <fullName>Service Charge</fullName>
                <default>false</default>
                <label>Service Charge</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Fee_Dollar__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Fee_Dollar__c</fullName>
    <externalId>false</externalId>
    <label>Fee $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Additional_Fees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Additional_Fees__c</fullName>
    <externalId>false</externalId>
    <label>Additional Fees $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Service_Fees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Fees__c</fullName>
    <externalId>false</externalId>
    <label>Service Fees $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Is_this_a_monthly_Pick_Up__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Is_this_a_monthly_Pick_Up__c</fullName>
    <externalId>false</externalId>
    <label>Is this a monthly Pick Up:</label>
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
### Rate_per_person__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate_per_person__c</fullName>
    <externalId>false</externalId>
    <label>Rate per person</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Invoiced__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Invoiced__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Invoiced?</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Room_Type_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Room_Type_Name__c</fullName>
    <externalId>false</externalId>
    <label>Room Type</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Sign_title__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sign_title__c</fullName>
    <externalId>false</externalId>
    <label>Sign title</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Rebate_to_RR_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_to_RR_Due__c</fullName>
    <externalId>false</externalId>
    <label>Rebate to RR Due</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Or__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Or__c</fullName>
    <externalId>false</externalId>
    <label>Or %</label>
    <precision>5</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Service_Fees_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Fees_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Service Fees - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Total__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total__c</fullName>
    <externalId>false</externalId>
    <label>Total #</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Breakfast_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Breakfast_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Breakfast_Rate__c) &amp;&amp; Breakfast_Rate__c != 0, Currency_Symbol__c + TEXT(Breakfast_Rate__c) + &apos;, &apos;, &quot;&quot;) + IF(Breakfast__c, &quot;Included&quot;, &quot;Not Included&quot;)</formula>
    <label>Breakfast</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Revenue_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Revenue_Type__c</fullName>
    <externalId>false</externalId>
    <label>Revenue Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Rebate</fullName>
                <default>false</default>
                <label>Rebate</label>
            </value>
            <value>
                <fullName>Commission</fullName>
                <default>false</default>
                <label>Commission</label>
            </value>
            <value>
                <fullName>Service fee</fullName>
                <default>false</default>
                <label>Service fee</label>
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
    <lookupFilter>
        <active>false</active>
        <booleanFilter>1 OR 2 OR 3 OR 4 OR 5 OR 6 OR 7</booleanFilter>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Hotel Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Ground Travel Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Hotel Vendor Chain</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Corporate Housing Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Airline Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Freight Vendor</value>
        </filterItems>
        <filterItems>
            <field>Account.RecordType.Name</field>
            <operation>equals</operation>
            <value>Corporate Housing Provider</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Revenue</relationshipLabel>
    <relationshipName>Revenue_Vendor</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Monthly_Pick_Up__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Monthly_Pick_Up__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Monthly Pick Up</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Commission_Agreed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Commission_Agreed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Commission Agreed</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Rebate_to_client_Due__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rebate_to_client_Due__c</fullName>
    <externalId>false</externalId>
    <label>Rebate to client Due</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Charge_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Charge_Type__c</fullName>
    <externalId>false</externalId>
    <label>Charge Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Amount</fullName>
                <default>false</default>
                <label>Amount</label>
            </value>
            <value>
                <fullName>Percent</fullName>
                <default>false</default>
                <label>Percent</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Production_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_ID__c</fullName>
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
### Surcharge_included__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Surcharge_included__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Surcharge included</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Additional_Fees_Currency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Additional_Fees_Currency__c</fullName>
    <externalId>false</externalId>
    <label>Additional Fees - Currency</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Surcharge_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Surcharge_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(Surcharge__c) &amp;&amp; Surcharge__c != 0, IF(!ISNULL(Bid__r.Commission_Revenue__r.Currency_Symbol__c) &amp;&amp; TRIM(Bid__r.Commission_Revenue__r.Currency_Symbol__c) != &apos;&apos;, Bid__r.Commission_Revenue__r.Currency_Symbol__c,&quot;$&quot;) + TEXT(Surcharge__c), &quot;&quot;)</formula>
    <label>Surcharge</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### VAT_Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>VAT_Rate__c</fullName>
    <externalId>false</externalId>
    <label>VAT Rate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Percent</type>
</CustomField>
```
### Total_Taxes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Total_Taxes__c</fullName>
    <externalId>false</externalId>
    <label>Total Taxes $</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### City_Tax_Rate_Percent_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>City_Tax_Rate_Percent_Conga__c</fullName>
    <externalId>false</externalId>
    <formula>IF(!ISNULL(City_Tax_Rate_percent__c) &amp;&amp; City_Tax_Rate_percent__c != 0, TEXT(City_Tax_Rate_percent__c * 100), &quot;&quot;) + &quot; %&quot;</formula>
    <label>City Tax Rate %</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```

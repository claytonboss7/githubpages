---
layout: default
title: Opportunity
parent: objects
---
# Metadata Type
CustomObject

# Name
Opportunity
## Fields
### Market_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Market_Type__c</fullName>
    <externalId>false</externalId>
    <label>Market Type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>TV</fullName>
                <default>false</default>
                <label>TV</label>
            </value>
            <value>
                <fullName>Commercials</fullName>
                <default>false</default>
                <label>Commercials</label>
            </value>
            <value>
                <fullName>Movie</fullName>
                <default>false</default>
                <label>Movie</label>
            </value>
            <value>
                <fullName>Choir</fullName>
                <default>false</default>
                <label>Choir</label>
            </value>
            <value>
                <fullName>Dance</fullName>
                <default>false</default>
                <label>Dance</label>
            </value>
            <value>
                <fullName>Opera</fullName>
                <default>false</default>
                <label>Opera</label>
            </value>
            <value>
                <fullName>Orchestra</fullName>
                <default>false</default>
                <label>Orchestra</label>
            </value>
            <value>
                <fullName>Collegiate</fullName>
                <default>false</default>
                <label>Collegiate</label>
            </value>
            <value>
                <fullName>Family Entertainment</fullName>
                <default>false</default>
                <label>Family Entertainment</label>
            </value>
            <value>
                <fullName>Fine Arts</fullName>
                <default>false</default>
                <label>Fine Arts</label>
            </value>
            <value>
                <fullName>Music</fullName>
                <default>false</default>
                <label>Music</label>
            </value>
            <value>
                <fullName>Theater</fullName>
                <default>false</default>
                <label>Theater</label>
            </value>
            <value>
                <fullName>Convention – Public attendees</fullName>
                <default>false</default>
                <label>Convention – Public attendees</label>
            </value>
            <value>
                <fullName>Conference – Industry Insiders</fullName>
                <default>false</default>
                <label>Conference – Industry Insiders</label>
            </value>
            <value>
                <fullName>Tournament</fullName>
                <default>false</default>
                <label>Tournament</label>
            </value>
            <value>
                <fullName>Weddings</fullName>
                <default>false</default>
                <label>Weddings</label>
            </value>
            <value>
                <fullName>Youth</fullName>
                <default>false</default>
                <label>Youth</label>
            </value>
            <value>
                <fullName>Professional</fullName>
                <default>false</default>
                <label>Professional</label>
            </value>
            <value>
                <fullName>Convention</fullName>
                <default>false</default>
                <label>Convention</label>
            </value>
            <value>
                <fullName>Conference</fullName>
                <default>false</default>
                <label>Conference</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### AVSFQB__Sales_Rep__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Sales_Rep__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Sales Rep</label>
    <length>5</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Sports_Team_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sports_Team_Name__c</fullName>
    <externalId>false</externalId>
    <label>Sports Team Name</label>
    <length>250</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Lost_Reason__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Lost_Reason__c</fullName>
    <externalId>false</externalId>
    <label>Lost Reason</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <controllingField>StageName</controllingField>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Client booked on own</fullName>
                <default>false</default>
                <label>Client booked on own</label>
            </value>
            <value>
                <fullName>Could not secure rates</fullName>
                <default>false</default>
                <label>Could not secure rates</label>
            </value>
            <value>
                <fullName>Had to use in house travel</fullName>
                <default>false</default>
                <label>Had to use in house travel</label>
            </value>
            <value>
                <fullName>Lack of client response</fullName>
                <default>false</default>
                <label>Lack of client response</label>
            </value>
            <value>
                <fullName>Lost to competitor</fullName>
                <default>false</default>
                <label>Lost to competitor</label>
            </value>
            <value>
                <fullName>No Travel Needed</fullName>
                <default>false</default>
                <label>No Travel Needed</label>
            </value>
            <value>
                <fullName>Production cancelled</fullName>
                <default>false</default>
                <label>Production cancelled</label>
            </value>
            <value>
                <fullName>Production Pushed</fullName>
                <default>false</default>
                <label>Production Pushed</label>
            </value>
            <value>
                <fullName>Service problem</fullName>
                <default>false</default>
                <label>Service problem</label>
            </value>
            <value>
                <fullName>Too Late</fullName>
                <default>false</default>
                <label>Too Late</label>
            </value>
            <value>
                <fullName>Used our rates to negotiate</fullName>
                <default>false</default>
                <label>Used our rates to negotiate</label>
            </value>
        </valueSetDefinition>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Client booked on own</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Could not secure rates</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Had to use in house travel</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Lack of client response</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Lost to competitor</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>No Travel Needed</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Production cancelled</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Production Pushed</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Service problem</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Too Late</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Archived Lost</controllingFieldValue>
            <valueName>Used our rates to negotiate</valueName>
        </valueSettings>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### AVSFQB__Shipping_State__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Shipping_State__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Shipping State</label>
    <length>21</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Itinerary_Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Itinerary_Start_Date__c</fullName>
    <externalId>false</externalId>
    <label>Itinerary Start Date</label>
    <summarizedField>Itinerary__c.Start_Date__c</summarizedField>
    <summaryForeignKey>Itinerary__c.Production__c</summaryForeignKey>
    <summaryOperation>min</summaryOperation>
    <trackTrending>false</trackTrending>
    <type>Summary</type>
</CustomField>
```
### Tour_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tour_Status__c</fullName>
    <externalId>false</externalId>
    <label>Tour Status</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Touring</fullName>
                <default>false</default>
                <label>Touring</label>
            </value>
            <value>
                <fullName>Will Tour</fullName>
                <default>false</default>
                <label>Will Tour</label>
            </value>
            <value>
                <fullName>Out of Town</fullName>
                <default>false</default>
                <label>Out of Town</label>
            </value>
            <value>
                <fullName>In Development</fullName>
                <default>false</default>
                <label>In Development</label>
            </value>
            <value>
                <fullName>Not Touring</fullName>
                <default>false</default>
                <label>Not Touring</label>
            </value>
            <value>
                <fullName>On Broadway</fullName>
                <default>false</default>
                <label>On Broadway</label>
            </value>
            <value>
                <fullName>Do Not Want</fullName>
                <default>false</default>
                <label>Do Not Want</label>
            </value>
            <value>
                <fullName>Potentially Touring</fullName>
                <default>false</default>
                <label>Potentially Touring</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### AVSFQB__Generate_Object__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Generate_Object__c</fullName>
    <deprecated>false</deprecated>
    <description>Request to generate Estimate, invoice or sales order</description>
    <externalId>false</externalId>
    <label>Generate</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>None</fullName>
                <default>true</default>
                <label>None</label>
            </value>
            <value>
                <fullName>Estimate</fullName>
                <default>false</default>
                <label>Estimate</label>
            </value>
            <value>
                <fullName>Invoice</fullName>
                <default>false</default>
                <label>Invoice</label>
            </value>
            <value>
                <fullName>SalesOrder</fullName>
                <default>false</default>
                <label>SalesOrder</label>
            </value>
            <value>
                <fullName>SalesReceipt</fullName>
                <default>false</default>
                <label>SalesReceipt</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>10</visibleLines>
</CustomField>
```
### Tour_Start__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tour_Start__c</fullName>
    <externalId>false</externalId>
    <label>Tour Start</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Lost_To__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Lost_To__c</fullName>
    <externalId>false</externalId>
    <label>Lost To</label>
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__Due_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Due_Date__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Due Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alias__c</fullName>
    <externalId>false</externalId>
    <label>Alias</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__Billing_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Billing_Address__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Billing Address</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### AVSFQB__Product_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Product_Name__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Product Name</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>DBSync</fullName>
                <default>false</default>
                <label>DBSync</label>
            </value>
            <value>
                <fullName>AppMashup (Salesforce.com &amp; QuickBooks)</fullName>
                <default>false</default>
                <label>AppMashup (Salesforce.com &amp; QuickBooks)</label>
            </value>
            <value>
                <fullName>AssessRight</fullName>
                <default>false</default>
                <label>AssessRight</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Website__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Website__c</fullName>
    <externalId>false</externalId>
    <label>Website</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Url</type>
</CustomField>
```
### CurrencyIsoCode

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CurrencyIsoCode</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### AVSFQB__Total_Amount__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Total_Amount__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Total Amount</label>
    <precision>18</precision>
    <required>false</required>
    <scale>2</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Description

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### Primary_Air_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Air_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Primary Air Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Productions2</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### AVSFQB__QuickBooks_ItemType__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__QuickBooks_ItemType__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>QuickBooks ItemType</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>ItemService</fullName>
                <default>false</default>
                <label>ItemService</label>
            </value>
            <value>
                <fullName>ItemNonInventory</fullName>
                <default>false</default>
                <label>ItemNonInventory</label>
            </value>
            <value>
                <fullName>ItemOtherCharge</fullName>
                <default>false</default>
                <label>ItemOtherCharge</label>
            </value>
            <value>
                <fullName>ItemInventory</fullName>
                <default>false</default>
                <label>ItemInventory</label>
            </value>
            <value>
                <fullName>ItemInventoryAssembly</fullName>
                <default>false</default>
                <label>ItemInventoryAssembly</label>
            </value>
            <value>
                <fullName>ItemFixedAsset</fullName>
                <default>false</default>
                <label>ItemFixedAsset</label>
            </value>
            <value>
                <fullName>ItemSubtotal</fullName>
                <default>false</default>
                <label>ItemSubtotal</label>
            </value>
            <value>
                <fullName>ItemDiscount</fullName>
                <default>false</default>
                <label>ItemDiscount</label>
            </value>
            <value>
                <fullName>ItemPayment</fullName>
                <default>false</default>
                <label>ItemPayment</label>
            </value>
            <value>
                <fullName>ItemGroup</fullName>
                <default>false</default>
                <label>ItemGroup</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### IqScore

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IqScore</fullName>
    <trackTrending>false</trackTrending>
</CustomField>
```
### Month_Four__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Month_Four__c</fullName>
    <externalId>false</externalId>
    <label>Month Four</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### AVSFQB__PO_Number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__PO_Number__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>PO Number</label>
    <length>20</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Primary_Freight_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Freight_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Primary Freight Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Productions3</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Budget_Confirmed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budget_Confirmed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Budget Confirmed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Name

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Name</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### Automations__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Automations__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Automations</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Sales_Excecutive_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sales_Excecutive_ID__c</fullName>
    <externalId>false</externalId>
    <label>Sales Excecutive ID</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Sales_Alerts__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sales_Alerts__c</fullName>
    <externalId>false</externalId>
    <label>Sales Alerts</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Options sent</fullName>
                <default>false</default>
                <label>Options sent</label>
            </value>
            <value>
                <fullName>Decision made</fullName>
                <default>false</default>
                <label>Decision made</label>
            </value>
            <value>
                <fullName>Contracted</fullName>
                <default>false</default>
                <label>Contracted</label>
            </value>
            <value>
                <fullName>Cancelled/Booked On Own</fullName>
                <default>false</default>
                <label>Cancelled/Booked On Own</label>
            </value>
            <value>
                <fullName>New Contact</fullName>
                <default>false</default>
                <label>New Contact</label>
            </value>
            <value>
                <fullName>Sales Journal</fullName>
                <default>false</default>
                <label>Sales Journal</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Contract_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Name__c</fullName>
    <externalId>false</externalId>
    <formula>if(LLC_Alias__c != null, LLC_Alias__r.Name, Account.Name)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Contract Name</label>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__Transaction_Number__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Transaction_Number__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Transaction Number</label>
    <length>31</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Production_type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_type__c</fullName>
    <externalId>false</externalId>
    <label>Production type</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
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
            <value>
                <fullName>General</fullName>
                <default>false</default>
                <label>General</label>
            </value>
            <value>
                <fullName>GTContractingTerms</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>GTContractingTerms</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### AVSFQB__Billing_Country__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Billing_Country__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Billing Country</label>
    <length>31</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Service_Sought__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Service_Sought__c</fullName>
    <externalId>false</externalId>
    <label>Service Sought</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
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
                <fullName>Ground Travel</fullName>
                <default>false</default>
                <label>Ground Travel</label>
            </value>
            <value>
                <fullName>Air</fullName>
                <default>false</default>
                <label>Air</label>
            </value>
            <value>
                <fullName>Individual Reservations</fullName>
                <default>false</default>
                <label>Individual Reservations</label>
            </value>
            <value>
                <fullName>Freight</fullName>
                <default>false</default>
                <label>Freight</label>
            </value>
            <value>
                <fullName>Charter</fullName>
                <default>false</default>
                <label>Charter</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Alias_Default__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alias_Default__c</fullName>
    <externalId>false</externalId>
    <formula>if(Alias__c != null, Alias__c, Name)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Alias Default</label>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CampaignId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CampaignId</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Sports__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Sports__c</fullName>
    <externalId>false</externalId>
    <label>Sports</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Baseball</fullName>
                <default>false</default>
                <label>Baseball</label>
            </value>
            <value>
                <fullName>Football</fullName>
                <default>false</default>
                <label>Football</label>
            </value>
            <value>
                <fullName>Lacrosse</fullName>
                <default>false</default>
                <label>Lacrosse</label>
            </value>
            <value>
                <fullName>Track and field</fullName>
                <default>false</default>
                <label>Track and field</label>
            </value>
            <value>
                <fullName>Rowing</fullName>
                <default>false</default>
                <label>Rowing</label>
            </value>
            <value>
                <fullName>Hockey</fullName>
                <default>false</default>
                <label>Hockey</label>
            </value>
            <value>
                <fullName>Basketball</fullName>
                <default>false</default>
                <label>Basketball</label>
            </value>
            <value>
                <fullName>MMA</fullName>
                <default>false</default>
                <label>MMA</label>
            </value>
            <value>
                <fullName>Wrestling</fullName>
                <default>false</default>
                <label>Wrestling</label>
            </value>
            <value>
                <fullName>Gymnastics</fullName>
                <default>false</default>
                <label>Gymnastics</label>
            </value>
            <value>
                <fullName>Rugby</fullName>
                <default>false</default>
                <label>Rugby</label>
            </value>
            <value>
                <fullName>Marathon</fullName>
                <default>false</default>
                <label>Marathon</label>
            </value>
            <value>
                <fullName>Frisbee</fullName>
                <default>false</default>
                <label>Frisbee</label>
            </value>
            <value>
                <fullName>Golf</fullName>
                <default>false</default>
                <label>Golf</label>
            </value>
            <value>
                <fullName>Tennis</fullName>
                <default>false</default>
                <label>Tennis</label>
            </value>
            <value>
                <fullName>Softball</fullName>
                <default>false</default>
                <label>Softball</label>
            </value>
            <value>
                <fullName>Water polo</fullName>
                <default>false</default>
                <label>Water polo</label>
            </value>
            <value>
                <fullName>Triathlon</fullName>
                <default>false</default>
                <label>Triathlon</label>
            </value>
            <value>
                <fullName>Soccer</fullName>
                <default>false</default>
                <label>Soccer</label>
            </value>
            <value>
                <fullName>Other</fullName>
                <default>false</default>
                <label>Other</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### AVSFQB__Transaction_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Transaction_Date__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Transaction Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### AVSFQB__Ship_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Ship_Date__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Ship Date</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Parent_Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Parent_Production__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Parent Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Opportunities</relationshipLabel>
    <relationshipName>Opportunities</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
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
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tour_End__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tour_End__c</fullName>
    <externalId>false</externalId>
    <label>Tour End</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Amount

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Amount</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### LP_Contact_Title__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LP_Contact_Title__c</fullName>
    <externalId>false</externalId>
    <label>LP Contact Title</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>General Manager</fullName>
                <default>false</default>
                <label>General Manager</label>
            </value>
            <value>
                <fullName>Company Manager</fullName>
                <default>false</default>
                <label>Company Manager</label>
            </value>
            <value>
                <fullName>Touring Company Manager</fullName>
                <default>false</default>
                <label>Touring Company Manager</label>
            </value>
            <value>
                <fullName>Producer</fullName>
                <default>false</default>
                <label>Producer</label>
            </value>
            <value>
                <fullName>Partner</fullName>
                <default>false</default>
                <label>Partner</label>
            </value>
            <value>
                <fullName>Assistant General Manager</fullName>
                <default>false</default>
                <label>Assistant General Manager</label>
            </value>
            <value>
                <fullName>Assistant Company Manager</fullName>
                <default>false</default>
                <label>Assistant Company Manager</label>
            </value>
            <value>
                <fullName>Touring Assistant Company Manager</fullName>
                <default>false</default>
                <label>Touring Assistant Company Manager</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Primary_Contracting_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Contracting_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Primary Contracting Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Productions4</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contract_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contract_Address__c</fullName>
    <externalId>false</externalId>
    <formula>if(LLC_Alias__c != null, LLC_Alias__r.Physical_Address__c, Account.Physical_Address__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Contract Address</label>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__Terms__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Terms__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Terms</label>
    <length>30</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Created_Date_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Created_Date_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Created Date NAV</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Month_One__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Month_One__c</fullName>
    <description>First month&apos;s amount</description>
    <externalId>false</externalId>
    <inlineHelpText>First month&apos;s amount</inlineHelpText>
    <label>Month One</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Month_Three__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Month_Three__c</fullName>
    <externalId>false</externalId>
    <label>Month Three</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Primary_Housing_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_Housing_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Primary Housing Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Productions</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### LLC_Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LLC_Alias__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>LLC Alias</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Productions (LLC Alias)</relationshipLabel>
    <relationshipName>Productions1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### TotalOpportunityQuantity

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>TotalOpportunityQuantity</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### Tour_Itinerary__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tour_Itinerary__c</fullName>
    <externalId>false</externalId>
    <label>Tour Itinerary</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Month_Two__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Month_Two__c</fullName>
    <externalId>false</externalId>
    <label>Month Two</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### AVSFQB__Primary_Contact__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Primary_Contact__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Primary Contact</label>
    <referenceTo>Contact</referenceTo>
    <relationshipLabel>Opportunities</relationshipLabel>
    <relationshipName>Opportunities</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Itinerary_End_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Itinerary_End_Date__c</fullName>
    <externalId>false</externalId>
    <label>Itinerary End Date</label>
    <summarizedField>Itinerary__c.End_Date__c</summarizedField>
    <summaryForeignKey>Itinerary__c.Production__c</summaryForeignKey>
    <summaryOperation>max</summaryOperation>
    <trackTrending>false</trackTrending>
    <type>Summary</type>
</CustomField>
```
### AccountId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AccountId</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### ContractId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ContractId</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Pricebook2Id

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Pricebook2Id</fullName>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### LeadSource

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LeadSource</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
</CustomField>
```
### AVSFQB__Shipping_Country__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Shipping_Country__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Shipping Country</label>
    <length>31</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Primary_GT_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Primary_GT_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Primary GT Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Productions1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### AVSFQB__Billing_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Billing_City__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Billing City</label>
    <length>31</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Discovery_Completed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Discovery_Completed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Discovery Completed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### StageName

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>StageName</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
</CustomField>
```
### AVSFQB__Shipping_Zip__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Shipping_Zip__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Shipping Zip</label>
    <length>13</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
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
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Company__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Company__c</fullName>
    <externalId>false</externalId>
    <formula>Account.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Company</label>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__Billing_State__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Billing_State__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Billing State</label>
    <length>21</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Loss_Reason__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Loss_Reason__c</fullName>
    <externalId>false</externalId>
    <label>Loss Reason</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Lost to Competitor</fullName>
                <default>false</default>
                <label>Lost to Competitor</label>
            </value>
            <value>
                <fullName>No Budget / Lost Funding</fullName>
                <default>false</default>
                <label>No Budget / Lost Funding</label>
            </value>
            <value>
                <fullName>No Decision / Non-Responsive</fullName>
                <default>false</default>
                <label>No Decision / Non-Responsive</label>
            </value>
            <value>
                <fullName>Price</fullName>
                <default>false</default>
                <label>Price</label>
            </value>
            <value>
                <fullName>Other</fullName>
                <default>false</default>
                <label>Other</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### AVSFQB__Shipping_City__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Shipping_City__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Shipping City</label>
    <length>31</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### NextStep

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>NextStep</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### Alert_Me__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alert_Me__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Alert Me</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### AVSFQB__Shipping_Address__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Shipping_Address__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Shipping Address</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Additional_Production_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Additional_Production_Name__c</fullName>
    <externalId>false</externalId>
    <inlineHelpText>Its a field for DBSYNC and to be used as unique identifier across productions.</inlineHelpText>
    <label>QB Unique Field</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Selected_Production_Title_in_Conga__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Selected_Production_Title_in_Conga__c</fullName>
    <externalId>false</externalId>
    <label>Selected Production Title in Conga</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### AVSFQB__Billing_Zip__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Billing_Zip__c</fullName>
    <deprecated>false</deprecated>
    <externalId>false</externalId>
    <label>Billing Zip</label>
    <length>13</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### IR_Coordinator__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IR_Coordinator__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>IR Coordinator</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Productions5</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### OwnerId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OwnerId</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Amount_Frequency__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Amount_Frequency__c</fullName>
    <description>Use this to determine whether you need additional fields for monthly amounts.</description>
    <externalId>false</externalId>
    <inlineHelpText>Use this to determine whether you need additional fields for monthly amounts.</inlineHelpText>
    <label>Amount Frequency</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>One Time</fullName>
                <default>true</default>
                <label>One Time</label>
            </value>
            <value>
                <fullName>Monthly</fullName>
                <default>false</default>
                <label>Monthly</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### ExpectedRevenue

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ExpectedRevenue</fullName>
    <trackTrending>false</trackTrending>
</CustomField>
```
### AVSFQB__Quickbooks_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Quickbooks_Id__c</fullName>
    <deprecated>false</deprecated>
    <description>QuickBooks Id</description>
    <externalId>true</externalId>
    <label>Quickbooks Id</label>
    <length>50</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Probability

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Probability</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### AVSFQB__Products_Count__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>AVSFQB__Products_Count__c</fullName>
    <deprecated>false</deprecated>
    <description>Roll up Count of Opportunity Products for an opportunity</description>
    <externalId>false</externalId>
    <label>Products Count</label>
    <summaryForeignKey>OpportunityLineItem.OpportunityId</summaryForeignKey>
    <summaryOperation>count</summaryOperation>
    <trackTrending>false</trackTrending>
    <type>Summary</type>
</CustomField>
```
### ROI_Analysis_Completed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>ROI_Analysis_Completed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>ROI Analysis Completed</label>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Season__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Season__c</fullName>
    <externalId>false</externalId>
    <label>Season</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Winter</fullName>
                <default>false</default>
                <label>Winter</label>
            </value>
            <value>
                <fullName>Spring</fullName>
                <default>false</default>
                <label>Spring</label>
            </value>
            <value>
                <fullName>Summer</fullName>
                <default>false</default>
                <label>Summer</label>
            </value>
            <value>
                <fullName>Fall</fullName>
                <default>false</default>
                <label>Fall</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Type

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Type</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
</CustomField>
```
### SyncedQuoteId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>SyncedQuoteId</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Secondary_Account2__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Secondary_Account2__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Secondary Account</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Opportunities (Secondary)</relationshipLabel>
    <relationshipName>SecondaryOpportunities</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Alias_with_Production_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alias_with_Production_Name__c</fullName>
    <externalId>false</externalId>
    <formula>IF( Alias__c != null, Alias__c + &apos; (&apos; + Name + &apos;)&apos;, Name)</formula>
    <label>Alias with Production name</label>
    <required>false</required>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Opp_Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Opp_Notes__c</fullName>
    <externalId>false</externalId>
    <label>Opp Notes</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>TextArea</type>
</CustomField>
```
### Production_ID__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_ID__c</fullName>
    <displayFormat>P-{000000}</displayFormat>
    <externalId>false</externalId>
    <label>Production ID</label>
    <trackTrending>false</trackTrending>
    <type>AutoNumber</type>
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
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>true</unique>
</CustomField>
```
### IsPrivate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsPrivate</fullName>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```
### Office_Location__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Office_Location__c</fullName>
    <externalId>false</externalId>
    <label>Office Location</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetName>Office_Location</valueSetName>
    </valueSet>
</CustomField>
```
### Year__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Year__c</fullName>
    <externalId>false</externalId>
    <label>Year</label>
    <length>4</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### CloseDate

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CloseDate</fullName>
    <trackFeedHistory>true</trackFeedHistory>
    <trackTrending>false</trackTrending>
</CustomField>
```

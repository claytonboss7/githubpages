---
layout: default
title: Production_Associations__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Production_Associations__c
## Fields
### Role__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Role__c</fullName>
    <externalId>false</externalId>
    <label>Role</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Accounting</fullName>
                <default>false</default>
                <label>Accounting</label>
            </value>
            <value>
                <fullName>Contract Signer</fullName>
                <default>false</default>
                <label>Contract Signer</label>
            </value>
            <value>
                <fullName>Primary Housing</fullName>
                <default>false</default>
                <label>Primary Housing</label>
            </value>
            <value>
                <fullName>Primary GT</fullName>
                <default>false</default>
                <label>Primary GT</label>
            </value>
            <value>
                <fullName>Primary Freight</fullName>
                <default>false</default>
                <label>Primary Freight</label>
            </value>
            <value>
                <fullName>Primary Air</fullName>
                <default>false</default>
                <label>Primary Air</label>
            </value>
            <value>
                <fullName>CC: Housing</fullName>
                <default>false</default>
                <label>CC: Housing</label>
            </value>
            <value>
                <fullName>CC: GT</fullName>
                <default>false</default>
                <label>CC: GT</label>
            </value>
            <value>
                <fullName>CC: Freight</fullName>
                <default>false</default>
                <label>CC: Freight</label>
            </value>
            <value>
                <fullName>CC: Air</fullName>
                <default>false</default>
                <label>CC: Air</label>
            </value>
            <value>
                <fullName>Other</fullName>
                <default>false</default>
                <label>Other</label>
            </value>
            <value>
                <fullName>Options</fullName>
                <default>false</default>
                <label>Options</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
</CustomField>
```
### Ground__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Ground__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Ground</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Ground__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>GT Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Alias__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Alias__c</fullName>
    <externalId>true</externalId>
    <label>Alias</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Compay_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Compay_Name__c</fullName>
    <externalId>false</externalId>
    <formula>Production_Opp__r.Account.Name</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Compay Name</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Team_Roles__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Team_Roles__c</fullName>
    <externalId>false</externalId>
    <label>Team Roles</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MultiselectPicklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Primary Housing Coordinator</fullName>
                <default>false</default>
                <label>Primary Housing Coordinator</label>
            </value>
            <value>
                <fullName>Primary GT Coordinator</fullName>
                <default>false</default>
                <label>Primary GT Coordinator</label>
            </value>
            <value>
                <fullName>Primary Air Coordinator</fullName>
                <default>false</default>
                <label>Primary Air Coordinator</label>
            </value>
            <value>
                <fullName>Primary Freight Coordinator</fullName>
                <default>false</default>
                <label>Primary Freight Coordinator</label>
            </value>
            <value>
                <fullName>Primary Contract Coordinator</fullName>
                <default>false</default>
                <label>Primary Contract Coordinator</label>
            </value>
            <value>
                <fullName>Account Manager</fullName>
                <default>false</default>
                <label>Account Manager</label>
            </value>
            <value>
                <fullName>Air back-end Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Air back-end Coordinator</label>
            </value>
            <value>
                <fullName>Backend Contracting Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Backend Contracting Coordinator</label>
            </value>
            <value>
                <fullName>Contracting Back End</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Contracting Back End</label>
            </value>
            <value>
                <fullName>Freight back-end Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Freight back-end Coordinator</label>
            </value>
            <value>
                <fullName>Ground Travel back-end Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Ground Travel back-end Coordinator</label>
            </value>
            <value>
                <fullName>Housing back-end Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Housing back-end Coordinator</label>
            </value>
            <value>
                <fullName>IR Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>IR Coordinator</label>
            </value>
            <value>
                <fullName>Individual Reservations back-end Coordinator</fullName>
                <default>false</default>
                <isActive>false</isActive>
                <label>Individual Reservations back-end Coordinator</label>
            </value>
        </valueSetDefinition>
    </valueSet>
    <visibleLines>4</visibleLines>
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
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Air__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Air Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Production_Opp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Opp__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### User__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>User__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>User</label>
    <referenceTo>User</referenceTo>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Associated</fullName>
                <default>true</default>
                <label>Associated</label>
            </value>
            <value>
                <fullName>Disassociated</fullName>
                <default>false</default>
                <label>Disassociated</label>
            </value>
        </valueSetDefinition>
    </valueSet>
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
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
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
### Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Historical_Production__c</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Freight__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Freight Trip Details</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
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
### Housing__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Housing</label>
    <lookupFilter>
        <active>true</active>
        <filterItems>
            <field>Housing__c.RecordTypeId</field>
            <operation>equals</operation>
            <value>Corporate Housing, Hotel Housing, Individual Reservation, Tournament</value>
        </filterItems>
        <isOptional>false</isOptional>
    </lookupFilter>
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>true</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Company__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Company__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Company</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Production Associations</relationshipLabel>
    <relationshipName>Production_Associations</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Contact_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contact_Name__c</fullName>
    <externalId>false</externalId>
    <formula>Contact__r.FirstName+&apos; &apos;+ Company__r.LastName</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Contact Name</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Contact_Title__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Contact_Title__c</fullName>
    <externalId>false</externalId>
    <formula>Contact__r.Title</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Contact Title</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Company_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Company_Type__c</fullName>
    <externalId>false</externalId>
    <label>Company Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>LLC</fullName>
                <default>false</default>
                <label>LLC</label>
            </value>
            <value>
                <fullName>Management Company</fullName>
                <default>false</default>
                <label>Management Company</label>
            </value>
            <value>
                <fullName>Promoter</fullName>
                <default>false</default>
                <label>Promoter</label>
            </value>
            <value>
                <fullName>Presenter</fullName>
                <default>false</default>
                <label>Presenter</label>
            </value>
            <value>
                <fullName>Production Company</fullName>
                <default>false</default>
                <label>Production Company</label>
            </value>
            <value>
                <fullName>Distribution Company</fullName>
                <default>false</default>
                <label>Distribution Company</label>
            </value>
            <value>
                <fullName>Sales Agent</fullName>
                <default>false</default>
                <label>Sales Agent</label>
            </value>
            <value>
                <fullName>Production Service Company</fullName>
                <default>false</default>
                <label>Production Service Company</label>
            </value>
            <value>
                <fullName>School</fullName>
                <default>false</default>
                <label>School</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```

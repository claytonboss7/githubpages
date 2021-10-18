---
layout: default
title: Account
parent: workflows
---

```<?xml version="1.0" encoding="UTF-8"?>
<Workflow xmlns="http://soap.sforce.com/2006/04/metadata">
    <fieldUpdates>
        <fullName>Update_Billing_City</fullName>
        <field>BillingCity</field>
        <formula>ShippingCity</formula>
        <name>Update Billing City</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Billing_Country</fullName>
        <field>BillingCountry</field>
        <formula>ShippingCountry</formula>
        <name>Update Billing Country</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Billing_Postal_Code</fullName>
        <field>BillingPostalCode</field>
        <formula>ShippingPostalCode</formula>
        <name>Update Billing Postal Code</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Billing_State</fullName>
        <field>BillingState</field>
        <formula>ShippingState</formula>
        <name>Update Billing State</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Billing_Street</fullName>
        <field>BillingStreet</field>
        <formula>ShippingStreet</formula>
        <name>Update Billing Street</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_From_Workflow</fullName>
        <field>Update_From_Workflow__c</field>
        <literalValue>1</literalValue>
        <name>Update From Workflow</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Literal</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Physical_City</fullName>
        <field>ShippingCity</field>
        <formula>City__r.City__c</formula>
        <name>Update Physical City</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Physical_Country</fullName>
        <field>ShippingCountry</field>
        <formula>TEXT(City__r.Country__c)</formula>
        <name>Update Physical Country</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Update_Physical_State</fullName>
        <field>ShippingState</field>
        <formula>TEXT(City__r.State__c)</formula>
        <name>Update Physical State</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <rules>
        <fullName>Account City to Physical Address</fullName>
        <actions>
            <name>Update_From_Workflow</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Physical_City</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Physical_Country</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Physical_State</name>
            <type>FieldUpdate</type>
        </actions>
        <active>true</active>
        <formula>AND(City__c &lt;&gt; null, ISBLANK(Sabre_Hotel_Code__c) )</formula>
        <triggerType>onAllChanges</triggerType>
    </rules>
    <rules>
        <fullName>Copy Shipping Address</fullName>
        <actions>
            <name>Update_Billing_City</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Billing_Country</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Billing_Postal_Code</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Billing_State</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_Billing_Street</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Update_From_Workflow</name>
            <type>FieldUpdate</type>
        </actions>
        <active>true</active>
        <criteriaItems>
            <field>Account.Physical_Address_Same_as_Billing__c</field>
            <operation>equals</operation>
            <value>True</value>
        </criteriaItems>
        <triggerType>onAllChanges</triggerType>
    </rules>
</Workflow>```

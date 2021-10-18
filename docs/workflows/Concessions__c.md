---
layout: default
title: Concessions__c
parent: workflows
---

```<?xml version="1.0" encoding="UTF-8"?>
<Workflow xmlns="http://soap.sforce.com/2006/04/metadata">
    <fieldUpdates>
        <fullName>Pass_Concessions_to_Indexed_Field</fullName>
        <field>Concessions_Requested_Index__c</field>
        <formula>TEXT(Concessions_Requested__c)</formula>
        <name>Pass Concessions to Indexed Field</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <rules>
        <fullName>Update Concession for Index</fullName>
        <actions>
            <name>Pass_Concessions_to_Indexed_Field</name>
            <type>FieldUpdate</type>
        </actions>
        <active>true</active>
        <criteriaItems>
            <field>Concessions__c.CreatedById</field>
            <operation>notEqual</operation>
        </criteriaItems>
        <triggerType>onAllChanges</triggerType>
    </rules>
</Workflow>```

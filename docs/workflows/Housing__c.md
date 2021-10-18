---
layout: default
title: Housing__c
parent: workflows
---

```<?xml version="1.0" encoding="UTF-8"?>
<Workflow xmlns="http://soap.sforce.com/2006/04/metadata">
    <alerts>
        <fullName>Deadline_Missed_Alert</fullName>
        <description>Deadline Missed Alert</description>
        <protected>false</protected>
        <recipients>
            <recipient>yellie@roadrebel.com</recipient>
            <type>user</type>
        </recipients>
        <senderType>CurrentUser</senderType>
        <template>unfiled$public/Housing_Deadline_Missed</template>
    </alerts>
    <rules>
        <fullName>Housing Deadline Missed</fullName>
        <actions>
            <name>Deadline_Missed_Alert</name>
            <type>Alert</type>
        </actions>
        <active>true</active>
        <criteriaItems>
            <field>Housing__c.Past_Due__c</field>
            <operation>equals</operation>
            <value>True</value>
        </criteriaItems>
        <triggerType>onCreateOrTriggeringUpdate</triggerType>
    </rules>
</Workflow>```

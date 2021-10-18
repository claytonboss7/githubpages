---
layout: default
title: Opportunity
parent: workflows
---

```<?xml version="1.0" encoding="UTF-8"?>
<Workflow xmlns="http://soap.sforce.com/2006/04/metadata">
    <alerts>
        <fullName>New_Community_Production_Entered</fullName>
        <ccEmails>claytonboss@roadrebel.com,sarah@roadrebel.com</ccEmails>
        <description>New Community Production Entered</description>
        <protected>false</protected>
        <recipients>
            <recipient>jana@roadrebel.com</recipient>
            <type>user</type>
        </recipients>
        <recipients>
            <recipient>sydney.maisel@roadrebel.com</recipient>
            <type>user</type>
        </recipients>
        <recipients>
            <recipient>yellie@roadrebel.com</recipient>
            <type>user</type>
        </recipients>
        <senderType>CurrentUser</senderType>
        <template>unfiled$public/Production_Entered_Email</template>
    </alerts>
    <fieldUpdates>
        <fullName>Rename_Additional_Name</fullName>
        <field>Additional_Production_Name__c</field>
        <formula>RecordType.Name &amp; &apos; &apos; &amp; IF(!ISPICKVAL(Market_Type__c, &apos;&apos;), TEXT(Market_Type__c), &apos;&apos;) &amp; &apos; &apos; &amp; Account.Name &amp; &apos; &apos; &amp; Name</formula>
        <name>Rename Additional Name</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <fieldUpdates>
        <fullName>Rename_Name</fullName>
        <field>Name</field>
        <formula>Name &amp; &quot; (&quot; &amp;  TEXT(Season__c) &amp; &quot; &quot; &amp;  Year__c &amp; &quot;)&quot;</formula>
        <name>Rename Name</name>
        <notifyAssignee>false</notifyAssignee>
        <operation>Formula</operation>
        <protected>false</protected>
        <reevaluateOnChange>false</reevaluateOnChange>
    </fieldUpdates>
    <rules>
        <fullName>Rename Opportunity</fullName>
        <actions>
            <name>Rename_Additional_Name</name>
            <type>FieldUpdate</type>
        </actions>
        <actions>
            <name>Rename_Name</name>
            <type>FieldUpdate</type>
        </actions>
        <active>true</active>
        <criteriaItems>
            <field>Opportunity.Season__c</field>
            <operation>notEqual</operation>
        </criteriaItems>
        <criteriaItems>
            <field>Opportunity.Year__c</field>
            <operation>notEqual</operation>
        </criteriaItems>
        <triggerType>onCreateOrTriggeringUpdate</triggerType>
    </rules>
</Workflow>```

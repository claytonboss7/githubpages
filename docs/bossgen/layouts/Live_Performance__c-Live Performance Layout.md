---
layout: default
title: Live_Performance__c-Live Performance Layout
parent: layouts
---
# Metadata Type
layouts


# Filename 
Live_Performance__c-Live Performance Layout


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Layout xmlns="http://soap.sforce.com/2006/04/metadata">
    <excludeButtons>Submit</excludeButtons>
    <layoutSections>
        <customLabel>false</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>true</editHeading>
        <label>Information</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Required</behavior>
                <field>Name</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Primary_Objective__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Total_Opportunity__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Captured_Opportunity__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>OwnerId</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Short_Term_Goals__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Long_Term_Goals__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Touch_Points__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsTopToBottom</style>
    </layoutSections>
    <layoutSections>
        <customLabel>false</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>true</editHeading>
        <label>System Information</label>
        <layoutColumns/>
        <layoutColumns/>
        <style>TwoColumnsTopToBottom</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>true</editHeading>
        <label>Custom Links</label>
        <layoutColumns/>
        <layoutColumns/>
        <layoutColumns/>
        <style>CustomLinks</style>
    </layoutSections>
    <relatedLists>
        <fields>NAME</fields>
        <fields>Contact__c</fields>
        <fields>LP_Title__c</fields>
        <fields>LP_Status__c</fields>
        <fields>LP_Services__c</fields>
        <relatedList>Production__c.Live_Performance__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>FULL_NAME</fields>
        <fields>CONTACT.TITLE</fields>
        <fields>Notes__c</fields>
        <relatedList>Contact.Live_Performance__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>TASK.SUBJECT</fields>
        <fields>TASK.WHO_NAME</fields>
        <fields>ACTIVITY.TASK</fields>
        <fields>TASK.DUE_DATE</fields>
        <fields>TASK.STATUS</fields>
        <fields>TASK.PRIORITY</fields>
        <fields>CORE.USERS.FULL_NAME</fields>
        <relatedList>RelatedActivityList</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>TASK.SUBJECT</fields>
        <fields>TASK.WHO_NAME</fields>
        <fields>ACTIVITY.TASK</fields>
        <fields>TASK.DUE_DATE</fields>
        <fields>CORE.USERS.FULL_NAME</fields>
        <fields>TASK.LAST_UPDATE</fields>
        <relatedList>RelatedHistoryList</relatedList>
    </relatedLists>
    <relatedLists>
        <relatedList>RelatedNoteList</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h1V00000ck7Lh</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

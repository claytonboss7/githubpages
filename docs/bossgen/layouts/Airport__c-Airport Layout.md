---
layout: default
title: Airport__c-Airport Layout
parent: layouts
---
# Metadata Type
layouts


# Filename 
Airport__c-Airport Layout


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
                <field>of_Terminals__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Sabre_Name__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Street_Address__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Street_Address_2__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>City__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Time_Zone__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Phone__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Website__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>CTXScanner__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Check_in_counter_hours__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Notes__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Airport_Code__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>InfoSource__c</field>
            </layoutItems>
            <layoutItems>
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Zipcode__c</field>
            </layoutItems>
            <layoutItems>
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Fax__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Airport_Loading_Instructions__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Check_in_Domestic__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Check_in_International__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsTopToBottom</style>
    </layoutSections>
    <layoutSections>
        <customLabel>false</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>true</editHeading>
        <label>System Information</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>CreatedById</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>LastModifiedById</field>
            </layoutItems>
        </layoutColumns>
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
        <fields>Vendor__c</fields>
        <fields>Distance__c</fields>
        <fields>Distance_Type__c</fields>
        <fields>Transportation_Type__c</fields>
        <relatedList>Vendor_Airport_Association__c.Airport__c</relatedList>
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
        <masterLabel>00h1V00000cy6Jc</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

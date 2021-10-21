---
layout: default
title: Freight__c-Freight Trip Details
parent: layouts
---
# Metadata Type
layouts


# Filename 
Freight__c-Freight Trip Details


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Layout xmlns="http://soap.sforce.com/2006/04/metadata">
    <excludeButtons>Submit</excludeButtons>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>false</editHeading>
        <label>Fields</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Required</behavior>
                <field>Production__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_lookup__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trace_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Service_Type__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Freight_Preferences__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_city__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_Date_Time_Text__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Group_Type__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Back_end_Coordinator__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>Past_Due__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>Number_of_Days_Past_Due__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>RecordTypeId</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Status__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>End_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Deadline_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Description__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsTopToBottom</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>false</editHeading>
        <label>Custom Links</label>
        <layoutColumns/>
        <layoutColumns/>
        <layoutColumns/>
        <style>CustomLinks</style>
    </layoutSections>
    <relatedLists>
        <fields>NAME</fields>
        <fields>Vendor__c</fields>
        <fields>Status__c</fields>
        <relatedList>Bid__c.Freight__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <fields>RECORDTYPE</fields>
        <fields>Sub_Trip_Type__c</fields>
        <fields>Description__c</fields>
        <relatedList>Freight__c.Freight_Trip_Details__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <fields>Journal_Entry__c</fields>
        <fields>CREATED_DATE</fields>
        <relatedList>Journal__c.Freight__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h56000000iVjb</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

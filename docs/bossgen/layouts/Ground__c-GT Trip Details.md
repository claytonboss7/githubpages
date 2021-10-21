---
layout: default
title: Ground__c-GT Trip Details
parent: layouts
---
# Metadata Type
layouts


# Filename 
Ground__c-GT Trip Details


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
                <field>Production_Ground__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_City__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>GT_Preferences__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trace_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_lookup__c</field>
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
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>RecordTypeId</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>End_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Description__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Status_Ground__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Deadline_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Service_Type_Ground__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsTopToBottom</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Additional Information</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Itinerary__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Group_Type__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsLeftToRight</style>
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
        <relatedList>Bid__c.GT__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <fields>RECORDTYPE</fields>
        <fields>Sub_Trip_Type__c</fields>
        <fields>Description__c</fields>
        <relatedList>Ground__c.GT_Trip_Details__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <fields>Journal_Entry__c</fields>
        <fields>CREATED_DATE</fields>
        <relatedList>Journal__c.G__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h1V00000cy6PT</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

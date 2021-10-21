---
layout: default
title: Ground__c-GT Sub Trip Details
parent: layouts
---
# Metadata Type
layouts


# Filename 
Ground__c-GT Sub Trip Details


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
                <field>GT_Trip_Details__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Sub_Trip_Type__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trip_Order__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Bid_Sub_Trip__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>GT_Freight__c</field>
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
                <field>Description__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Sub_Trip_Notes__c</field>
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
                <field>isFromCommunity__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns/>
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
        <fields>Line__c</fields>
        <fields>Vehicle_Ref__c</fields>
        <fields>Travel_Type__c</fields>
        <fields>Start_Date__c</fields>
        <fields>Start_Date_Time__c</fields>
        <fields>End_Date__c</fields>
        <fields>End_Date_Time__c</fields>
        <relatedList>Ground__c.GT_Sub_Trip_Details__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <relatedList>Sub_Trip_GCQ__c.GT_Sub_Trip_Details__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h56000000k87q</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

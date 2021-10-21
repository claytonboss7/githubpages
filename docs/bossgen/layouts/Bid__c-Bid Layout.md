---
layout: default
title: Bid__c-Bid Layout
parent: layouts
---
# Metadata Type
layouts


# Filename 
Bid__c-Bid Layout


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
                <behavior>Readonly</behavior>
                <field>Name</field>
            </layoutItems>
            <layoutItems>
                <behavior>Required</behavior>
                <field>Production__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_Comments__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trip_Details_Update_Terms__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_Bid_Notes__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Property_Agrees__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>Housing_Start_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>Housing_End_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>GT_Start_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>GT_End_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>Freight_Start_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>NAV_ID__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>isFromTournament__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Bid_Has_Duplicate_Traces__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Memorialization_Data__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>CurrencyIsoCode</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Housing__c</field>
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
        <fields>NAME</fields>
        <fields>Vehicle_Ref__c</fields>
        <fields>Vehicle_Type__c</fields>
        <fields>Capacity__c</fields>
        <fields>Make_Model__c</fields>
        <fields>Year__c</fields>
        <fields>All_Amenities__c</fields>
        <relatedList>Ground__c.Bid__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h56000000iQGK</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

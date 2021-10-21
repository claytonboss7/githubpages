---
layout: default
title: Freight__c-Freight Layout
parent: layouts
---
# Metadata Type
layouts


# Filename 
Freight__c-Freight Layout


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Layout xmlns="http://soap.sforce.com/2006/04/metadata">
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
                <field>Bid__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_lookup__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>GT_Preferences__c</field>
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
                <field>CurrencyIsoCode</field>
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
        <customLabel>false</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>true</editHeading>
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
        <relatedList>Freight__c.Sales_Freight_details__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <relatedList>Production_Associations__c.Freight__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
</Layout>
```


# Last Modified


# Usage

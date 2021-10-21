---
layout: default
title: Ground__c-Sales GT Details
parent: layouts
---
# Metadata Type
layouts


# Filename 
Ground__c-Sales GT Details


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
                <field>Sales_GT_Details__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_lookup__c</field>
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
                <field>Office__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Start_Date_Full__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsLeftToRight</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Other Defaults</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Contracting_Terms__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Payment_Information__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Billing_Options__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Billing_options_Text__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Internal_Notes__c</field>
            </layoutItems>
        </layoutColumns>
        <style>OneColumn</style>
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
        <fields>Vehicle_Ref__c</fields>
        <fields>Vehicle_Type__c</fields>
        <fields>Capacity__c</fields>
        <fields>Make_Model__c</fields>
        <fields>Year__c</fields>
        <fields>All_Amenities__c</fields>
        <relatedList>Ground__c.Sales_GT_Details__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>Production__c</fields>
        <fields>Concession_Type__c</fields>
        <fields>Concessions_Requested__c</fields>
        <fields>Concession_Provided__c</fields>
        <relatedList>Concessions__c.GT__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h1V00000cy6PU</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

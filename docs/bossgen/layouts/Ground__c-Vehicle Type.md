---
layout: default
title: Ground__c-Vehicle Type
parent: layouts
---
# Metadata Type
layouts


# Filename 
Ground__c-Vehicle Type


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
                <field>Vehicle_Type__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Make__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Year__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Amenities__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vendor_lookup__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>CreatedById</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Requested_Vehicle__c</field>
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
                <field>Vehicle_Ref__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Capacity__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Model__c</field>
            </layoutItems>
            <layoutItems>
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Other_Amenities__c</field>
            </layoutItems>
            <layoutItems>
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trip_Vehicle__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsLeftToRight</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Additional Information</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Sales_GT_Details__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>isFromCommunity__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Gear_Luggage_Space__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Bid__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Qty_of_Buses__c</field>
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
        <fields>Production__c</fields>
        <fields>Concession_Type__c</fields>
        <fields>Concessions_Requested__c</fields>
        <fields>Concession_Provided__c</fields>
        <relatedList>Concessions__c.GT__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <relatedList>Itinerary__c.GT__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <fields>Journal_Entry__c</fields>
        <fields>CREATED_DATE</fields>
        <relatedList>Journal__c.G__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <relatedList>Ground__c.Trip_Vehicle__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h56000000jeC7</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

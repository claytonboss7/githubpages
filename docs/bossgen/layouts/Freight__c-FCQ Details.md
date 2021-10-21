---
layout: default
title: Freight__c-FCQ Details
parent: layouts
---
# Metadata Type
layouts


# Filename 
Freight__c-FCQ Details


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
                <field>Confirm_Address_Route__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Is_it_an_exclusive_shipment_or_LTL__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trailer_information__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Any_specific_info_need_for_entering_the__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vehicle_registration__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Confirm_size__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Equipment_FCQ__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Flight_info__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Carnet_info__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Vessel_number__c</field>
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
                <field>RecordTypeId</field>
            </layoutItems>
            <layoutItems>
                <emptySpace>true</emptySpace>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Confirm_all_permits_ATA_Carnets_Import__c</field>
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
        <fields>Freight_Sub_Trip_Details__c</fields>
        <relatedList>Sub_Trip_FCQ__c.FCQ_Details__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>FULL_NAME</fields>
        <fields>ACCOUNT.NAME</fields>
        <fields>CONTACT.PHONE1</fields>
        <relatedList>Contact.FCQ_Driver__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h56000000lbFv</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

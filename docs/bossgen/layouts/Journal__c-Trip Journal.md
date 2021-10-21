---
layout: default
title: Journal__c-Trip Journal
parent: layouts
---
# Metadata Type
layouts


# Filename 
Journal__c-Trip Journal


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Layout xmlns="http://soap.sforce.com/2006/04/metadata">
    <excludeButtons>Submit</excludeButtons>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Categories Section</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>OwnerId</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Production_checkbox__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>G__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Readonly</behavior>
                <field>CreatedById</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Parent_Journal__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsLeftToRight</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Filters</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Issue__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Sales__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsLeftToRight</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Trip Details</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Housing__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Air__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Freight__c</field>
            </layoutItems>
        </layoutColumns>
        <style>TwoColumnsLeftToRight</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>true</editHeading>
        <label>Entry</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Journal_Entry__c</field>
            </layoutItems>
        </layoutColumns>
        <style>OneColumn</style>
    </layoutSections>
    <layoutSections>
        <customLabel>true</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Trace Details</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trace_Coordinator__c</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Trace_Date__c</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>Mark_Journal_trace_complete__c</field>
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
        <fields>Contact__c</fields>
        <fields>Type__c</fields>
        <relatedList>Related_Contact__c.Journal__c</relatedList>
    </relatedLists>
    <relatedLists>
        <fields>NAME</fields>
        <fields>Company__c</fields>
        <relatedList>Related_Companies__c.Journal__c</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showHighlightsPanel>false</showHighlightsPanel>
    <showInteractionLogPanel>false</showInteractionLogPanel>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
    <summaryLayout>
        <masterLabel>00h1V00000cy6Nf</masterLabel>
        <sizeX>4</sizeX>
        <sizeY>0</sizeY>
        <summaryLayoutStyle>Default</summaryLayoutStyle>
    </summaryLayout>
</Layout>
```


# Last Modified


# Usage

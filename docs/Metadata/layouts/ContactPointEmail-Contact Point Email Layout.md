---
layout: default
title: ContactPointEmail-Contact Point Email Layout
parent: layouts
grand_parent: Metadata
---
# Metadata Type
layouts


# Filename 
ContactPointEmail-Contact Point Email Layout


# Raw XML
```
<?xml version="1.0" encoding="UTF-8"?>
<Layout xmlns="http://soap.sforce.com/2006/04/metadata">
    <layoutSections>
        <customLabel>false</customLabel>
        <detailHeading>true</detailHeading>
        <editHeading>true</editHeading>
        <label>Information</label>
        <layoutColumns>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>IsPrimary</field>
            </layoutItems>
            <layoutItems>
                <behavior>Required</behavior>
                <field>EmailAddress</field>
            </layoutItems>
            <layoutItems>
                <behavior>Edit</behavior>
                <field>ParentId</field>
            </layoutItems>
        </layoutColumns>
        <layoutColumns/>
        <style>TwoColumnsTopToBottom</style>
    </layoutSections>
    <layoutSections>
        <customLabel>false</customLabel>
        <detailHeading>false</detailHeading>
        <editHeading>false</editHeading>
        <layoutColumns/>
        <style>CustomLinks</style>
    </layoutSections>
    <relatedLists>
        <fields>Name</fields>
        <fields>ContactPoint</fields>
        <fields>DataUsePurpose</fields>
        <fields>PrivacyConsentStatus</fields>
        <relatedList>ContactPointConsents</relatedList>
    </relatedLists>
    <relatedLists>
        <relatedList>RelatedEntityHistoryList</relatedList>
    </relatedLists>
    <showEmailCheckbox>false</showEmailCheckbox>
    <showRunAssignmentRulesCheckbox>false</showRunAssignmentRulesCheckbox>
    <showSubmitAndAttachButton>false</showSubmitAndAttachButton>
</Layout>
```


# Last Modified


# Usage

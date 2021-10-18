---
layout: default
title: Related_Contact__c
parent: sharingRules
---

```<?xml version="1.0" encoding="UTF-8"?>
<SharingRules xmlns="http://soap.sforce.com/2006/04/metadata">
    <sharingGuestRules>
        <fullName>Share_Contacts</fullName>
        <accessLevel>Read</accessLevel>
        <label>Share Contacts</label>
        <sharedTo>
            <guestUser>Road_Rebel</guestUser>
        </sharedTo>
        <criteriaItems>
            <field>CreatedById</field>
            <operation>notEqual</operation>
            <value/>
        </criteriaItems>
        <includeHVUOwnedRecords>false</includeHVUOwnedRecords>
    </sharingGuestRules>
    <sharingGuestRules>
        <fullName>Share_with_Voyajer_guest_user</fullName>
        <accessLevel>Read</accessLevel>
        <label>Share with Voyajer guest user</label>
        <sharedTo>
            <guestUser>Voyajer</guestUser>
        </sharedTo>
        <criteriaItems>
            <field>CreatedById</field>
            <operation>notEqual</operation>
            <value/>
        </criteriaItems>
        <includeHVUOwnedRecords>false</includeHVUOwnedRecords>
    </sharingGuestRules>
</SharingRules>```

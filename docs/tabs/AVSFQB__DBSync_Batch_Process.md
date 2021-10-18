---
layout: default
title: AVSFQB__DBSync_Batch_Process
parent: tabs
---

```<?xml version="1.0" encoding="UTF-8"?>
<CustomTab xmlns="http://soap.sforce.com/2006/04/metadata">
    <description>DBSync Integration for QuickBooks Online and Salesforce.com. This tab is used for batch processing of records.</description>
    <frameHeight>600</frameHeight>
    <hasSidebar>true</hasSidebar>
    <label>Batch Updates</label>
    <motif>Custom55: Books</motif>
    <url>https://app03.mydbsync.com/appcenter/serverRouter?sessionId={!API.Session_ID}&amp;sfUrl={!API.Partner_Server_URL_320}&amp;dbsyncId={!User.AVSFQB__DBSync_Id__c}&amp;dbsyncPasswd={!User.AVSFQB__DBSync_Passwd__c}&amp;profileName={!User.AVSFQB__DBSync_Profile__c}&amp;target=batchupdate</url>
    <urlEncodingKey>UTF-8</urlEncodingKey>
</CustomTab>```

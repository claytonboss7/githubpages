---
layout: default
title: AVSFQB__DbSyncSetup
parent: tabs
---

```<?xml version="1.0" encoding="UTF-8"?>
<CustomTab xmlns="http://soap.sforce.com/2006/04/metadata">
    <frameHeight>800</frameHeight>
    <hasSidebar>false</hasSidebar>
    <label>Setup</label>
    <motif>Custom33: Desk</motif>
    <url>https://app03.mydbsync.com/appcenter/serverRouter?email={!User.Email}&amp;un={!User.Username}&amp;fn={!User.FirstName}&amp;ln={!User.LastName}&amp;comp={!User.CompanyName}&amp;phone={!User.Phone}&amp;sfUrl={!API.Partner_Server_URL_320}&amp;dbsyncId={!User.AVSFQB__DBSync_Id__c}&amp;returnUrl=repo/1/page/sf_qb_redirect&amp;target=setup</url>
    <urlEncodingKey>UTF-8</urlEncodingKey>
</CustomTab>```

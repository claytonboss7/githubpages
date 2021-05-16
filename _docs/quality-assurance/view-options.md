---
title: View Options
description: Details on View Options Functionality
badges:
 - type: warning
   tag: warning-badge
 - type: danger
   tag: danger-badge
---
# QA / Exception Report


<br/>

## View Options for Stay 

**Details:** When the options are sent to the client from the dashboard, there are a few criteria for the data for it to show the client.  This report has the fields from the query so we can figure out what condition it didn't meet.
<br/>

**Usage** Report can be used to troubleshoot options and if removing criteria shows the Stay we are investigating.

### Details
 * **Scheduled:**  Run on Demand
  * **Filter**: 
```
      FROM Bid__c
      WHERE
        Housing__c = :housingId
        AND Status__c != 'Deactivated Bid'
        AND Housing__r.Options_sent_to_client__c != NULL
        AND (Include_in_options__c = TRUE
        OR Include_in_option_cover_sheet__c = TRUE)
      ORDER BY Options__c ASC
```
The query is doing the following:

| Field/Value | Description |
| --- | --- |
| Housing__c = housingId | Passed in from the page, can be replaced with ID in Quotes ex: 'a01ae3030292WW3'|
| Status__c != 'Deactivated Bid' | Bid status can not include Deactivated Bid
| Housing__r.Options_sent_to_client__c != NULL | Bid Stay value for 'Options Sent to Client' has to have a value
|Include_in_options__c = TRUE OR Include_in_option_cover_sheet__c = TRUE | Values for one of the two fields listed has to be true to make it return

<br/>

### Link
[Option Details Report (edit filters to troubleshoot)](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zK6TEAU/edit)

<br/>

### Screenshots 
  * **Viewing Options in Community:**
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/options.gif)
  * **Non Exception State (What you see as results is what Community would bring back)**
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/options.jpg)
<hr>
---
title: View Options
description: Details on View Options Functionality
badges:
 - type: warning
   tag: warning-badge
 - type: danger
   tag: danger-badge
---
# View Options for Stay 

**Details:** When the options are sent to the client from the dashboard, there are a few criteria for the data for it to show the client.  This report has the fields from the query so we can figure out what condition it didn't meet.
<br/>

**Usage** Report can be used to troubleshoot options and if removing criteria shows the Stay we are investigating.

## Details
 * **Scheduled:**  Run on Demand
  * **Filter**: 
```
      FROM Bid__c
      WHERE
        AND Status__c != 'Deactivated Bid'
        AND Housing__r.Options_sent_to_client__c != NULL
        AND (Include_in_options__c = TRUE
        OR Include_in_option_cover_sheet__c = TRUE)
      ORDER BY Options__c ASC
```
The query is doing the following:

| Field/Value | Description |
| --- | --- |
| Status__c != 'Deactivated Bid' | Bid status can not include Deactivated Bid
| Housing__r.Options_sent_to_client__c != NULL | Bid Stay value for 'Options Sent to Client' has to have a value
|Include_in_options__c = TRUE OR Include_in_option_cover_sheet__c = TRUE | Values for one of the two fields listed has to be true to make it return

<br/>

| Field | When is it set? |
| --- | --- |
| Status__c != 'Deactivated Bid' | Bid status can not include Deactivated Bid. |
| Housing__r.Options_sent_to_client__c != NULL | With any of the Send Options buttons, this should stamp after it sends. |
| Include_in_options__c OR Include_in_option_cover_sheet__c | These are set in the dashboard on the Bid tab.  Also has logic where if the `Option__c` field has a number in it to set this to true. |


## Link
[Option Details Report (edit filters to troubleshoot)](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zK6TEAU/edit)

<br/>

## Screenshots 
  Viewing Options in Community:
  <br/>
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/options.gif)
  <br/>
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/view-options-report.gif)
  <br/>
  ![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/options.jpg)
<hr>
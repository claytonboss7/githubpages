---
title: View Options
description: Details on View Options Functionality
---
# Exception Report

## View Options for Stay
**Details:** When the options are sent to the client from the dashboard, there are a few criteria for the data for it to show the client.  This report has the fields from the query so we can figure out what condition it didn't meet.

**Problem Solved:** An answer to a missing option can be narrowed down and not have the wait time on dev resources.

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
* Status not Deactivated Bid
* The Options Sent to Client field on the stay is not blank (timestamp exists)
* Include in Options OR Include in Option Cover Sheet fields are true  
* **Link:** [Option Details Report (edit filters to troubleshoot)](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zK6TEAU/edit)

#### Screenshots 
  * **Non Exception State (What you see as results is what Community would bring back)**
  ![DupeReport](.../assets/img/options.jpg)
<hr>
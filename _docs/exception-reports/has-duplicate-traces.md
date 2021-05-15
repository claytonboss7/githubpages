---
title: Duplicate Traces
description: Details on Duplicates Functionality
---

<hr width="50%">

# QA / Exception Report
## Has Duplicate Traces Report
**Background:** When traces are created (Tasks inserted) we do a check at the end to see if we have more traces than we should for a particular bid.  ** This does not currently include old data, only new records going forward.

**Problem Solved:** Duplicate Traces that might be "sporadic" would notify us and be less mysterious. 
### Details
  * **Scheduled:**  Nightly 2am
  * **Filter**: 
    * Has_Duplicate_Traces__c on the Bid__c record is TRUE
  * **Link:** [Has Duplicate Traces Report](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zJHzEAM/edit)

#### Screenshots 
  * **Non Exception State**![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/ExceptionDupeTraces.jpg)
  * **Exception State**![DupeReport](https://claytonboss7.github.io/voyajerwiki/assets/img/exception_report_not_empty.jpg)

<hr>
---
title: Quality Assurance
description: A page for Quality Assurance
---
# Quality Assurance

Several Quality checks can be done to proactively find things that are problematic.  These include running Automated Tests, and watching reports to see if we can spot a data condition that would tell us something is broken.   

The categories for QA focused on in the Voyajer system are:
* *Automated Tests* - These are required to be written to deploy regardless, but Apex Unit tests that specifically setup data to replicate speciifc scenarios is a time investment that can make a huge difference.  When written properly and brainstormed these can be an autoamtic way to check for regression issues that your deployment created, and how your code will behave in Production
* *Exception Reports* - These reports will only email us when they return data,  and allow meaningful emails to alert us to problems.  They are normal reports which can be viewed on demand but also will run on a schedule to have some type of automated checks in place.

## Exception Reports
* **Has Duplicate Traces Report** - When traces are created (Tasks inserted) we do a check at the end to see if we have more traces than we should for a particular bid.  ** This does not currently include old data, only new records going forward.  
  * **Scheduled:**  Nightly 2am
  * **Filter**: 
    * Has_Duplicate_Traces__c on the Bid__c record is TRUE
  * **Link:** https://roadrebel.lightning.force.com/lightning/r/Report/00O3w000005zJHzEAM/edit



## Automated Tests

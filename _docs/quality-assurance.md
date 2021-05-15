---
title: Quality Assurance
description: A page for Quality Assurance
---
# Quality Assurance

<hr>
Several Quality checks can be done to proactively find things that are problematic.  These include running Automated Tests, and watching reports to see if we can spot a data condition that would tell us something is broken.   

The categories for QA focused on in the Voyajer system are:
* *QA/Exception Reports* - These reports will only email us when they return data,  and allow meaningful emails to alert us to problems.  They are normal reports which can be viewed on demand but also will run on a schedule to have some type of automated checks in place.
  * View Options Details [View Options Report](exception-reports/view-options)
  * Has Duplicate Traces [View Options Report](exception-reports/has-duplicate-traces)
* *Automated Tests* - These are required to be written to deploy regardless, but Apex Unit tests that specifically setup data to replicate speciifc scenarios is a time investment that can make a huge difference.  When written properly and brainstormed these can be an autoamtic way to check for regression issues that your deployment created, and how your code will behave in Production
  * Test Thing 1
<hr width="50%">
---
layout: default
title: Report Component
parent: User Guide
---

# Report Component
{: .no_toc }


A component that allows for embedding of reports on Account (currently only Account) and the specification of the report data to display.   Also has a second field for filtering if the Account Id you need to use is on a separate object.

{: .fs-6 .fw-300 }

## Scope
The reportComponent and how to use on Lightning Pages.   Includes steps to setup and description of what it expects for configuration inputs.  Does not cover Lightning Page Editor assignments and Activation, just component configuration.

## User Details
- Create report to be displayed on a per Account basis
    - Any report can be used as long as it contains filter for Account Id
    - If the Account.Id field is not a filter (top level Account filtering in Report), filter field must be specified in Lightning Page Editor
        - Top Level Account Filter means in the List of Objects in the Field Selections object it is the "Id" field from the "Account" object fields
        - ![report fields example1](https://github.com/sfdcboss/voyajerwiki/blob/gh-pages/assets/images/reportComponentEx1.jpg)
        - ![report fields example2](https://github.com/sfdcboss/voyajerwiki/blob/gh-pages/assets/images/reportComponentEx2.jpg)
- Drag reportComponent onto Lightning Record Page and click once to get configuration options:
    - ![report lightning page editor details](https://github.com/sfdcboss/voyajerwiki/blob/gh-pages/assets/images/reportComponentOverview.jpg)
- Save Lightning Record Page and confirm expected Report shows with filtering
- A Summary Report will show the details in groupings
    - Note the grey row headers listing the Bid Name above
- A Tabular Report will show the details without grouping rows.
    - White rows with no header

## Technical Details
- Aura Component
    - reportComponent
    - reportSearchComponent
- Apex Classes
    - AnalyticsUtils
    - LightningReportController
    - LightningReportControllerTest
- Tests
    - LightningReportControllerTest
        - Ex test
        - Ex test

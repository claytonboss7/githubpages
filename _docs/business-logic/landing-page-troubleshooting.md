---
title: Troubleshooting Landing Pages
description: Diagrams and Documentation for Pickup Report Landing Page.
---

# Troubleshooting Landing Pages

## Reports
### [UUIDs for Bids](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBOEA2/view?queryScope=userFolders)
View the Bids that were modified Today, and their associated Landing Page URLs.  These URLs are in the Bid Request Email and the Pickup Report email, and this report would be for reference purposes only.  There is no expectations that users would use this report, only Admins.  The UUID for the Bid is generated at Bid creation and it an identifier used as an alternate to the Bid ID so that we can group multiple objects that potentially match on this UUID if we have more complex entries to the landing page.
![reportsbidsuuids](https://claytonboss7.github.io/voyajerwiki/assets/img/report-bids-uuids.jpg)

### [Force.com Site Usage Reports](https://roadrebel.lightning.force.com/lightning/r/Folder/00l3w000002ODcoAAG/view?queryScope=userFolders)
Force.com Sites have limits like bandwidth, time spent processing, etc.  The reports in the folder linked give access to show the metrics and if we are in danger of coming close to any of the threshholds.  Once we have daily traffic to the Sites it will be important to catch anything in danger of stopping serving the Page, and we can set up alerts to track this.
#### Report Descriptions

| Report Name | Description of Report |
| --- | --- |
|[Current Period Page Views](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows data for the current Month which is the period that the Limits use to reset their counts. |
|[Daily Total Bandwidth Usage](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows daily data for the Bandwidth used to serve the Landing Pages to Customers. |
|[Daily Total Page Views](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows daily page view data for the Landing Pages |
|[Site Daily Origin Bandwidth Usage](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows the Daily Bandwidth for the origin Server (not cached) |
|[Site Daily Request Time Usage](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows data for the time spent processing requests by Vendors via the Landing Page. |
|[Top Bandwidth Consuming Sites](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows what sites are the Top consumers of Bandwidth |
|[Top Resource Consuming Sites](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Shows what sites are the Top consumers of Resources |
|[Top Sites by Page Views](https://roadrebel.lightning.force.com/lightning/r/Report/00O3w0000052BBTEA2/view?queryScope=userFolders) | Top Sites by Page Views |

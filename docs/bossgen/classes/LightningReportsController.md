---
layout: default
title: LightningReportsController
parent: classes
---
# Metadata Type
classes


# Filename 
LightningReportsController


# Raw XML
```
/**
 * @description       : used with the report component for bid history to get default reports for the page builder dropdown
 * @author            : sfdc cb
 * @group             : report embed
 * @last modified on  : 09-07-2021
 * @last modified by  : sfdc cb
 **/
global without sharing class LightningReportsController {
  @AuraEnabled
  public static String getReportResponse(String reportId, String accountId) {
    system.debug('accountId :: ' + accountId);
    system.debug('reportId :: ' + reportId);
    return JSON.serialize(
      AnalyticsUtils.getReportResponse(reportId, accountId)
    );
  }

  @AuraEnabled
  public static List<Report> getReportsForSearch() {
    Report defaultReport = [SELECT Id, Name FROM Report LIMIT 1];
    Report[] theReports = [
      SELECT Id, Name
      FROM Report
      WHERE Name = 'Vendors with Bids with RoomTypes'
      ORDER BY Name
    ];
    if (theReports.size() > 0) {
      return theReports;
    } else {
      return new List<Report>{ defaultReport };
    }
  }
}
```


# Last Modified


# Usage

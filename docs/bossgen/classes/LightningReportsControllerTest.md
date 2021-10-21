---
layout: default
title: LightningReportsControllerTest
parent: classes
---
# Metadata Type
classes


# Filename 
LightningReportsControllerTest


# Raw XML
```
@isTest
public without sharing class LightningReportsControllerTest {

    @isTest(SeeAllData='true')
    public static void testAsyncReportWithTestData() {

      List <Report> reportList = [SELECT Id,DeveloperName FROM Report where
          DeveloperName LIKE '%RoomTypes%'];
      String reportId = (String)reportList.get(0).get('Id');

      Reports.ReportMetadata reportMetadata =
          Reports.ReportManager.describeReport(reportId).getReportMetadata();

      // Add a filter.
      List<Reports.ReportFilter> filters = new List<Reports.ReportFilter>();
      Reports.ReportFilter newFilter = new Reports.ReportFilter();
      newFilter.setColumn('Account.Id');
      newFilter.setOperator('equals');
      newFilter.setValue([SELECT Id FROM Account LIMIT 1]?.Id);
      filters.add(newFilter);
      reportMetadata.setReportFilters(filters);

      Test.startTest();

      Reports.ReportInstance instanceObj =
          Reports.ReportManager.runAsyncReport(reportId,reportMetadata,false);
      String instanceId = instanceObj.getId();

      LightningReportsController.getReportResponse(reportId, [SELECT Id FROM Account LIMIT 1]?.Id);

      // Report instance is not available yet.
      Test.stopTest();
      // After the stopTest method, the report has finished executing
      // and the instance is available.

      instanceObj = Reports.ReportManager.getReportInstance(instanceId);
      System.assertEquals(instanceObj.getStatus(),'Success');
      Reports.ReportResults result = instanceObj.getReportResults();
      Reports.ReportFact grandTotal = (Reports.ReportFact)result.getFactMap().get('T!T');
    //  System.assertEquals(1,(Decimal)grandTotal.getAggregates().get(1).getValue());
    }

    @isTest(SeeAllData='true')
    public static void testTabularAsyncReportWithTestData() {

      List <Report> reportList = [SELECT Id,DeveloperName FROM Report where
          DeveloperName LIKE '%Test_Tabular_Report%'];
      String reportId = (String)reportList.get(0).get('Id');

      Reports.ReportMetadata reportMetadata =
          Reports.ReportManager.describeReport(reportId).getReportMetadata();

      system.debug ('report filters ::: ' + reportMetadata.getStandardDateFilter());
      // Add a filter.
      List<Reports.ReportFilter> filters = new List<Reports.ReportFilter>();
      Reports.ReportFilter newFilter = new Reports.ReportFilter();
      newFilter.setColumn('CREATED_DATE');
      newFilter.setOperator('equals');
      newFilter.setValue(String.valueOf(system.today()));
      filters.add(newFilter);
      reportMetadata.setReportFilters(filters);

      Test.startTest();

      Reports.ReportInstance instanceObj =
          Reports.ReportManager.runAsyncReport(reportId,reportMetadata,false);
      String instanceId = instanceObj.getId();

      LightningReportsController.getReportResponse(reportId, [SELECT Id FROM Account LIMIT 1]?.Id);

      // Report instance is not available yet.
      Test.stopTest();
      // After the stopTest method, the report has finished executing
      // and the instance is available.

      instanceObj = Reports.ReportManager.getReportInstance(instanceId);
      System.assertEquals(instanceObj.getStatus(),'Success');
      Reports.ReportResults result = instanceObj.getReportResults();
      Reports.ReportFact grandTotal = (Reports.ReportFact)result.getFactMap().get('T!T');
    //  System.assertEquals(1,(Decimal)grandTotal.getAggregates().get(1).getValue());
    }

    @isTest(SeeAllData='true')
    public static void testSummaryAsyncReportWithTestData() {

      List <Report> reportList = [SELECT Id,DeveloperName FROM Report where
          DeveloperName LIKE '%Test_Summary_Report%'];
      String reportId = (String)reportList.get(0).get('Id');

      Reports.ReportMetadata reportMetadata =
          Reports.ReportManager.describeReport(reportId).getReportMetadata();

      system.debug ('report filters ::: ' + reportMetadata.getStandardDateFilter());
      // Add a filter.
      List<Reports.ReportFilter> filters = new List<Reports.ReportFilter>();
      Reports.ReportFilter newFilter = new Reports.ReportFilter();
      newFilter.setColumn('CREATED_DATE');
      newFilter.setOperator('equals');
      newFilter.setValue(String.valueOf(system.today()));
      filters.add(newFilter);
      reportMetadata.setReportFilters(filters);

      Test.startTest();

      Reports.ReportInstance instanceObj =
          Reports.ReportManager.runAsyncReport(reportId,reportMetadata,false);
      String instanceId = instanceObj.getId();

      LightningReportsController.getReportResponse(reportId, [SELECT Id FROM Account LIMIT 1]?.Id);

      // Report instance is not available yet.
      Test.stopTest();
      // After the stopTest method, the report has finished executing
      // and the instance is available.

      instanceObj = Reports.ReportManager.getReportInstance(instanceId);
      System.assertEquals(instanceObj.getStatus(),'Success');
      Reports.ReportResults result = instanceObj.getReportResults();
      Reports.ReportFact grandTotal = (Reports.ReportFact)result.getFactMap().get('T!T');
    //  System.assertEquals(1,(Decimal)grandTotal.getAggregates().get(1).getValue());
    }

    @isTest(SeeAllData='true')
    public static void testReturnVendorRoomTypesReport(){
        Report[] returnReports = LightningReportsController.getReportsForSearch();
        system.assertNotEquals(returnReports.size(),0);
    }

    @isTest
    public static void testIsHyperlink(){
        Boolean isLink = AnalyticsUtils.isHyperlink(Date.newInstance(1,1,2020));
    }

    @isTest
    public static void testReportPicklistValues(){
        ReportPickListValues rplv = new ReportPickListValues();
        rplv.getDefaultValue();
        rplv.getValues();
    }
}
```


# Last Modified


# Usage

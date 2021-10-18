---
layout: default
title: Dashboard_SearchBoxController_Test
parent: classes
---

```@isTest
public class Dashboard_SearchBoxController_Test {
    private static Account accountRecord;
    private static Opportunity productionRecord;
    static void generateData(){
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountRecord;
        
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), AccountId = accountRecord.Id);
        insert productionRecord;
    }
    public static testMethod void searchProdTest(){
        generateData();
        Test.startTest();
        Dashboard_SearchBoxController.searchProd('Te',true);
        Test.stopTest();
    }
}```

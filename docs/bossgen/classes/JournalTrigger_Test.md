---
layout: default
title: JournalTrigger_Test
parent: classes
---
# Metadata Type
classes


# Filename 
JournalTrigger_Test


# Raw XML
```
@isTest
public class JournalTrigger_Test {
    private static Account accountRecord;
    private static Opportunity productionRecord;
    private static Ground__c groundDetail;
    static void generateData(){
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountRecord;

        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), Office_Location__c = 'RRU', StageName = 'Closed Won', RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), AccountId = accountRecord.Id);
        insert productionRecord;

        groundDetail = new Ground__c(Status_Ground__c = 'Unsent',Start_Date__c = system.today(), Status__c = 'Itinerary Received', Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId());
        insert groundDetail;
    }
    public static testMethod void Test_insertJournal(){
        generateData();
        Test.startTest();
        Journal__c j = new Journal__c(G__c = groundDetail.Id, RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId());
        insert j;
        Test.stopTest();
        system.assertEquals(1,[SELECT Id FROM Journal__c WHERE RecordType.DeveloperName = 'Trip_Journal'].size());
    }
    public static testMethod void Test_updateJournal(){
        generateData();
        Journal__c j = new Journal__c(G__c = groundDetail.Id, RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId());
        insert j;
        Test.startTest();
        j.Journal_Entry__c = 'update';
        update j;
        Test.stopTest();
        system.assertEquals('update',[SELECT Id, Journal_Entry__c FROM Journal__c WHERE Id =: j.Id].Journal_Entry__c);
    }
}
```


# Last Modified


# Usage

---
layout: default
title: JournalCreation_Test
parent: classes
---
# Metadata Type
classes


# Filename 
JournalCreation_Test


# Raw XML
```
@isTest
public class JournalCreation_Test {
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
        List<JournalCreation.JournalEntry> journals = new List<JournalCreation.JournalEntry>();
        journals.add(new JournalCreation.JournalEntry('ground',groundDetail.Id, Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId(),'test'));
        JournalCreation.insertJournal(journals);
        Test.stopTest();
        system.assertEquals(1,[SELECT Id FROM Journal__c WHERE RecordType.DeveloperName = 'Trip_Journal'].size());
    }
}
```


# Last Modified


# Usage

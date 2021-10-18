---
layout: default
title: Dashboard_Journals_Test
parent: classes
---

```@isTest
public class Dashboard_Journals_Test {
    private static Account accountRecord;
    private static Opportunity productionRecord;
    private static Journal__c journalRecord;
    private static Ground__c groundRecord;
    private static Bid__c bidRecordGT;
    private static Freight__c freightRecord;
    private static Bid__c bidRecordFreight;
    private static Air__c airRecord;
    private static Bid__c bidRecordAir;
    //
    static void generateData(){
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountRecord;
        
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), AccountId = accountRecord.Id);
        insert productionRecord;
        
        List<Production_Associations__c> paList = new List<Production_Associations__c>();
        Production_Associations__c pa1 = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary Housing Coordinator;', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        paList.add(pa1);
        insert paList;
        
        journalRecord = new Journal__c(Production__c = productionRecord.Id, Journal_Entry__c = 'test', RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Journal').getRecordTypeId()); insert journalRecord;
        Journal__c journalChildren = new Journal__c(Production__c = productionRecord.Id,Parent_Journal__c = journalRecord.Id, Journal_Entry__c = 'test children'); insert journalChildren;
        
        groundRecord = new Ground__c(Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId());
        insert groundRecord;
        bidRecordGT = new Bid__c(GT__c = groundRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId());
        insert bidRecordGT;
        
        freightRecord = new Freight__c(Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId());
        insert freightRecord;
        bidRecordFreight = new Bid__c(Freight__c = freightRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId());
        insert bidRecordFreight;
        
        airRecord = new Air__c(Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId());
        insert airRecord;
        bidRecordAir = new Bid__c(Air__c = airRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId());
        insert bidRecordAir;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }
    public static testMethod void loadJournalsProdTest(){
        generateData();
        Test.startTest();
        Dashboard_Journals controller = new Dashboard_Journals();
        Dashboard_Journals.verifyWideAddress('jcerdan@cloudcreations.com');
        controller.relativeSObjectName = 'Production';
        controller.relativeRecordId = productionRecord.Id;
        controller.loadJournals();
        controller.journalId = journalRecord.Id;
        controller.openJournal();
        controller.journalParentId = journalRecord.Id;
        controller.openJournalReply();
        controller.opportunityId = productionRecord.Id;
        controller.productionType = 'Housing';
        controller.journalJSON = '{"id":"'+journalRecord.Id+'","issue":false,"sales":false,"categoryProduction":true,"categoryHousingVendor":false,"journalContacts":[],"journalCompanyContacts":[],"journalEntry":"test","journalCoordinator":"'+UserInfo.getUserId()+'","traceDate":"","alertAll":true,"markComplete":false}';
        controller.upsertJournal();
        Test.stopTest();
    }
    public static testMethod void loadJournalsBidTest(){
        generateData();
        Test.startTest();
        Dashboard_Journals controller = new Dashboard_Journals();
        controller.relativeSObjectName = 'Bid';
        controller.relativeRecordId = bidRecordGT.Id;
        controller.loadJournals();
        controller.relativeRecordId = bidRecordFreight.Id;
        controller.loadJournals();
        controller.relativeRecordId = bidRecordAir.Id;
        controller.loadJournals();
        controller.relativeSObjectName = 'Housing';
        controller.loadJournals();
        controller.relativeSObjectName = 'Ground';
        controller.loadJournals();
        controller.relativeSObjectName = 'FCQ';
        controller.loadJournals();
        controller.relativeSObjectName = 'ACQ';
        controller.loadJournals();
        Test.stopTest();
    }
}```

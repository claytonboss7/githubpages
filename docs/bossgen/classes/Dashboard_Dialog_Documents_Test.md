---
layout: default
title: Dashboard_Dialog_Documents_Test
parent: classes
---
# Metadata Type
classes


# Filename 
Dashboard_Dialog_Documents_Test


# Raw XML
```
@isTest
public class Dashboard_Dialog_Documents_Test {
    private static Account accountRecord;
    private static Opportunity productionRecord;
    private static Ground__c groundRecord;
    private static Bid__c bidRecordGT;
    private static Air__c airRecord;
    private static Bid__c bidRecordAir;
    private static Housing__c housingRecord;
    private static Bid__c bidRecordHousing;
    private static Housing__c housingRecordC;
    private static Bid__c bidRecordHousingC;
    //
    static void generateData(){
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountRecord;
        
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), AccountId = accountRecord.Id);
        insert productionRecord;
        
        groundRecord = new Ground__c(Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId());
        insert groundRecord;
        bidRecordGT = new Bid__c(GT__c = groundRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId());
        insert bidRecordGT;
        
        airRecord = new Air__c(Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId());
        insert airRecord;
        bidRecordAir = new Bid__c(Air__c = airRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId());
        insert bidRecordAir;
        
        housingRecord = new Housing__c(Production_CC__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Hotel_Housing').getRecordTypeId());
        insert housingRecord;
        bidRecordHousing = new Bid__c(Housing__c = housingRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId());
        insert bidRecordHousing;
        housingRecordC = new Housing__c(Production_CC__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Corporate_Housing').getRecordTypeId());
        insert housingRecordC;
        bidRecordHousingC = new Bid__c(Housing__c = housingRecordC.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId());
        insert bidRecordHousingC;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }
    public static testMethod void getDocumentsGroundTest(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        Dashboard_Dialog_Documents.VerifyWideAddress('test@cloudcreations.com');
        controller.relativeRecordId = bidRecordGT.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Ground';
        controller.getDocuments();
        controller.documentUploadAction = 'Contract';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        controller.documentUploadAction = 'ContractToClient';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        ContentDocument cd = [SELECT Id, Title FROM ContentDocument LIMIT 1];
        controller.fileId = cd.Id;
        controller.fileName = cd.Title;
        controller.RenameDocument();
        ContentDocumentLink cdl = [SELECT Id FROM ContentDocumentLink WHERE ContentDocumentId =: cd.Id LIMIT 1];
        controller.emailJSON = '{"emailTo":"test@cloudcreations.com","emailCC":"test@cloudcreations.com","emailBCC":"test@cloudcreations.com","emailSubject":"Test Subject","emailBody":"Test Body","emailAttachment":["'+cd.Id+'"]}';
        controller.SendEmail();
        controller.linkId = cdl.Id;
        controller.isShared = true;
        controller.fileId = cd.Id;
        controller.ShareWithCustomers();
        controller.linkId = cdl.Id;
        controller.isShared = true;
        controller.fileId = cd.Id;
        controller.shareId = [SELECT Id FROM Share__c LIMIT 1].Id;
        controller.ShareWithVendors();
        controller.fileId = cd.Id;
        controller.DeleteDocument();
        Test.stopTest();
    }
    public static testMethod void getDocumentsAirTest(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        system.debug(bidRecordAir.Id);
        controller.relativeRecordId = bidRecordAir.Id;
        controller.relativeParentId = airRecord.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Air';
        controller.getDocuments();
        controller.documentUploadAction = 'Contract';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        Test.stopTest();
    }
    public static testMethod void getDocumentsHousingHotelTest(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        controller.relativeRecordId = bidRecordHousing.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Housing';
        controller.getDocuments();
        controller.documentUploadAction = 'Contract';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        Test.stopTest();
    }
    public static testMethod void getDocumentsHousingCorporateTest(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        controller.relativeRecordId = bidRecordHousingC.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Housing';
        controller.getDocuments();
        controller.documentUploadAction = 'ContractToClient';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        Test.stopTest();
    }
    public static testMethod void getDocumentsHousingCorporateTestFinal(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        controller.relativeRecordId = bidRecordHousingC.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Housing';
        controller.getDocuments();
        controller.documentUploadAction = 'Final';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        Test.stopTest();
    }
    public static testMethod void getDocumentsHousingCorporateTestDateChange(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        controller.relativeRecordId = bidRecordHousingC.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Housing';
        controller.getDocuments();
        controller.documentUploadAction = 'DateChange';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        Test.stopTest();
    }
    public static testMethod void getDocumentsHousingCorporateTestNoRoomsPU(){
        generateData();
        Test.startTest();
        Dashboard_Dialog_Documents controller = new Dashboard_Dialog_Documents();
        controller.relativeRecordId = bidRecordHousingC.Id;
        controller.isBidContract = true;
        controller.relativeParentSObjectName = 'Housing';
        controller.getDocuments();
        controller.documentUploadAction = 'NoRoomsPU';
        controller.fileName = 'test.txt';
        controller.fileBody = 'data:text/plain;base64,dGVzdA==';
        controller.UploadDocument();
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

---
layout: default
title: Dashboard_Tab_Close_Out_Test
parent: classes
---
# Metadata Type
classes


# Filename 
Dashboard_Tab_Close_Out_Test


# Raw XML
```
@isTest
public class Dashboard_Tab_Close_Out_Test {
    private static City__c cityRecord;
    private static Airport__c airportRecord;
    private static Contact contactRecord;
    private static Account accountRecord;
    private static Opportunity productionRecord;
    private static Ground__c groundRecord;
    private static Bid__c bidRecordGT;
    private static Freight__c freightRecord;
    private static Bid__c bidRecordFreight;
    private static Production_Associations__c prodAssoc;
    static void generateData(){
        cityRecord = new City__c(Name = 'Test City');
        insert cityRecord;
        
        airportRecord = new Airport__c(Name = 'Test Airport', Airport_Code__c = 'LAX');
        insert airportRecord;
        
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountRecord;
        
        contactRecord = new Contact(LastName = 'Test', AccountId = accountRecord.Id);
        insert contactRecord;
        
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), AccountId = accountRecord.Id);
        insert productionRecord;
        
        prodAssoc = new Production_Associations__c(Production_Opp__c = productionRecord.Id, Contact__c = contactRecord.Id, Role__c = 'Accounting;', RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId());
        insert prodAssoc;
        
        prodAssoc = new Production_Associations__c(Production_Opp__c = productionRecord.Id, User__c = UserInfo.getUserId(), Team_Roles__c = 'IR Coordinator;', RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        insert prodAssoc;
        
        groundRecord = new Ground__c(Start_Date__c = system.today(),Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId());
        insert groundRecord;
        bidRecordGT = new Bid__c(Status__c = 'Contracted', GT__c = groundRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId());
        insert bidRecordGT;
        
        freightRecord = new Freight__c(Start_Date__c = system.today(), Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId());
        insert freightRecord;
        bidRecordFreight = new Bid__c(Status__c = 'Contracted', Freight__c = freightRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId());
        insert bidRecordFreight;
    }

    public static testMethod void Test_ClooseOut(){
        generateData();
        Test.startTest();
        Dashboard_Tab_Close_Out controller = new Dashboard_Tab_Close_Out();
        List<SelectOption> options = controller.getCurrencyValues();
        system.assert(options.size() > 0);
        controller.vfpConfiguration = new DashboardConfigurationWrapper();
        controller.vfpConfiguration.bidId = bidRecordGT.Id;
        controller.vfpConfiguration.productionId = productionRecord.Id;
        controller.vfpConfiguration.parentSObject = 'Ground';
        controller.vfpConfiguration.productionName = 'Test';
        controller.vfpConfiguration.parentId = groundRecord.Id;
        controller.getBidRevenue();
        system.assert(controller.symbolMap.size() > 0);
        controller.readyToInvoice();
        system.assert(controller.bidData.Sync_to_QB__c);
    	Test.stopTest();
    }
}
```


# Last Modified


# Usage

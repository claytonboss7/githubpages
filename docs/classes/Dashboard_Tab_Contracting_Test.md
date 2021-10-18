---
layout: default
title: Dashboard_Tab_Contracting_Test
parent: classes
---

```@isTest
public class Dashboard_Tab_Contracting_Test {
    private static City__c cityRecord;
    private static Airport__c airportRecord;
    private static Contact contactRecord;
    private static Account accountRecord;
    private static Opportunity productionRecord;
    private static Housing__c housingRecord;
    private static Bid__c bidRecordHousing;
    private static Ground__c groundRecord;
    private static Bid__c bidRecordGT;
    private static Air__c airRecord;
    private static Bid__c bidRecordAir;
    private static Freight__c freightRecord;
    private static Bid__c bidRecordFreight;
    private static Production_Associations__c prodAssoc;
    //
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
        
        housingRecord = new Housing__c(Production_CC__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Hotel_Housing').getRecordTypeId());
        insert housingRecord;
        bidRecordHousing = new Bid__c(Status__c = 'Contracted', Housing__c = housingRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId());
        insert bidRecordHousing;
        
        groundRecord = new Ground__c(Start_Date__c = system.today(),Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId());
        insert groundRecord;
        bidRecordGT = new Bid__c(Status__c = 'Contracted', GT__c = groundRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId());
        insert bidRecordGT;
        
        airRecord = new Air__c(Departure_Date__c = system.today(), Departure_City__c = airportRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId());
        insert airRecord;
        bidRecordAir = new Bid__c(Air__c = airRecord.Id, Status__c = 'Contracted', Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId());
        insert bidRecordAir;
        
        freightRecord = new Freight__c(Start_Date__c = system.today(), Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId());
        insert freightRecord;
        bidRecordFreight = new Bid__c(Status__c = 'Contracted', Freight__c = freightRecord.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId());
        insert bidRecordFreight;
    }
    public static testMethod void housingTest(){
        generateData();
        Test.startTest();
        Dashboard_Tab_Contracting controller = new Dashboard_Tab_Contracting();
        Dashboard_Tab_Contracting.searchCity('Test');
        Dashboard_Tab_Contracting.searchAirport('Test');
        Dashboard_Tab_Contracting.searchAccount('Test','Airline Vendor');
        controller.vfpConfiguration = new DashboardConfigurationWrapper();
        controller.vfpConfiguration.bidId = bidRecordHousing.Id;
        controller.vfpConfiguration.productionId = productionRecord.Id;
        controller.vfpConfiguration.parentSObject = 'Housing';
        controller.vfpConfiguration.productionName = 'Test';
        controller.vfpConfiguration.parentId = housingRecord.Id;
        controller.parentId = String.valueOf(housingRecord.Id);
        controller.orderFieldBidContract = 'Status__c';
        controller.loadBidContracts();
        controller.bidContractedGTAssociations();
        controller.bidId = bidRecordHousing.Id;
        controller.viewBidContracted();
        controller.contactClientValue = contactRecord.Id;
        controller.changeClientContract();
        Test.stopTest();
    }
    public static testMethod void groundTest(){
        generateData();
        Test.startTest();
        Dashboard_Tab_Contracting controller = new Dashboard_Tab_Contracting();
        controller.vfpConfiguration = new DashboardConfigurationWrapper();
        controller.vfpConfiguration.bidId = bidRecordGT.Id;
        controller.vfpConfiguration.productionId = productionRecord.Id;
        controller.vfpConfiguration.parentSObject = 'Ground';
        controller.vfpConfiguration.productionName = 'Test';
        controller.vfpConfiguration.parentId = groundRecord.Id;
        controller.parentId = String.valueOf(groundRecord.Id);
        controller.orderFieldBidContract = 'Status__c';
        controller.loadBidContracts();
        controller.bidContractedGTAssociations();
        controller.contactClientValue = contactRecord.Id;
        controller.changeClientContract();
        Test.stopTest();
    }
    public static testMethod void airTest(){
        generateData();
        Test.startTest();
        Dashboard_Tab_Contracting controller = new Dashboard_Tab_Contracting();
        controller.vfpConfiguration = new DashboardConfigurationWrapper();
        controller.vfpConfiguration.bidId = bidRecordAir.Id;
        controller.vfpConfiguration.productionId = productionRecord.Id;
        controller.vfpConfiguration.parentSObject = 'Air';
        controller.vfpConfiguration.productionName = 'Test';
        controller.orderFieldBidContract = 'Status__c';
        controller.vfpConfiguration.parentId = airRecord.Id;
        controller.parentId = String.valueOf(airRecord.Id);
        controller.search_city = 'LAX - New York - United States';
        controller.loadBidContracts();
        controller.bidContractedGTAssociations();
        controller.contactClientValue = contactRecord.Id;
        controller.changeClientContract();
        Test.stopTest();
    }
    public static testMethod void airTestCity(){
        generateData();
        Test.startTest();
        Dashboard_Tab_Contracting controller = new Dashboard_Tab_Contracting();
        controller.vfpConfiguration = new DashboardConfigurationWrapper();
        controller.vfpConfiguration.bidId = bidRecordAir.Id;
        controller.vfpConfiguration.productionId = productionRecord.Id;
        controller.vfpConfiguration.parentSObject = 'Air';
        controller.vfpConfiguration.productionName = 'Test';
        controller.vfpConfiguration.parentId = airRecord.Id;
        controller.parentId = String.valueOf(airRecord.Id);
        controller.orderFieldBidContract = 'Status__c';
        controller.search_city = 'New York City - United States';
        controller.loadBidContracts();
        controller.bidContractedGTAssociations();
        controller.contactClientValue = contactRecord.Id;
        controller.changeClientContract();
        Test.stopTest();
    }
    public static testMethod void freightTest(){
        generateData();
        Test.startTest();
        Dashboard_Tab_Contracting controller = new Dashboard_Tab_Contracting();
        controller.vfpConfiguration = new DashboardConfigurationWrapper();
        controller.vfpConfiguration.bidId = bidRecordFreight.Id;
        controller.vfpConfiguration.productionId = productionRecord.Id;
        controller.vfpConfiguration.parentSObject = 'Freight';
        controller.vfpConfiguration.productionName = 'Test';
        controller.vfpConfiguration.parentId = freightRecord.Id;
        controller.parentId = String.valueOf(freightRecord.Id);
        controller.orderFieldBidContract = 'Status__c';
        controller.loadBidContracts();
        controller.bidContractedGTAssociations();
        controller.contactClientValue = contactRecord.Id;
        controller.changeClientContract();
        controller.contractingbackendcoordinatorGT = UserInfo.getUserId();
        controller.saveContractingBackEndCoordinator();
        controller.bidContractStatusOptions = null;
        List<SelectOption> bidContractStatusOptions = controller.bidContractStatusOptions;
        controller.bidSelected = bidRecordFreight;
        controller.changeFinalStatus();
        controller.changeContactContract();
        Test.stopTest();
    }
}```

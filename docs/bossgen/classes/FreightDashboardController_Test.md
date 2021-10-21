---
layout: default
title: FreightDashboardController_Test
parent: classes
---
# Metadata Type
classes


# Filename 
FreightDashboardController_Test


# Raw XML
```
@isTest
public class FreightDashboardController_Test {
	private static Account accountRecord;
    private static Account accountAirlineRecord;
    private static Account otherAccountRecord;
    private static Opportunity productionRecord;
    private static Airport__c airport1;
    private static Airport__c airport2;
    private static Contact contactRecord;
    private static Contact contactRecord2;
    private static Contact contactRecord3;
    private static Freight__c freightDetail;
    private static Itinerary__c itineraryDetail;
    private static Bid__c bidRecord;
    private static City__c cityRecord;

    static void generateData(){
        cityRecord = new City__c(Name = 'New York', City__c = 'New York', Country__c = 'United States');
        insert cityRecord;
        
        List<Airport__c> airports = new List<Airport__c>();
        airport1 = new Airport__c(Name = 'Los Angeles International Airport', Airport_Code__c='LAX');airports.add(airport1);
        airport2 = new Airport__c(Name = 'San Diego International Airport', Airport_Code__c='DIE');airports.add(airport2);
        insert airports;
        
		Account parentRecord = new Account(Name = 'Test Parent',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Freight_Vendor').getRecordTypeId());
        insert parentRecord;
        
        Contact contactParentRecord = new Contact(AccountId = parentRecord.Id, FirstName = 'Robint', LastName = 'Hood', Email = 'jcerdan@cloudcreations.com', Order__c = 2, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactParentRecord;
        
        accountRecord = new Account(Name = 'Test', Child_Seat__c = 'Yes', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Freight_Vendor').getRecordTypeId(),ParentId = parentRecord.Id);
        insert accountRecord;
        
        otherAccountRecord = new Account(Name = 'Test Other Account', City__c = cityRecord.Id, Child_Seat__c = 'Yes', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Freight_Vendor').getRecordTypeId(),ParentId = parentRecord.Id);
        insert otherAccountRecord;
        
        Associated_Cities__c assoc_city = new Associated_Cities__c(Vendor__c = otherAccountRecord.Id, City__c = cityRecord.Id);
        insert assoc_city;
        Vendor_Airport_Association__c vendorAirport_assoc = new Vendor_Airport_Association__c(Vendor__c = otherAccountRecord.Id, Airport__c = airport1.Id);
        insert vendorAirport_assoc;
        Account venueRecord = new Account(Name = 'Test Venue',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Venue').getRecordTypeId());
        insert venueRecord;
        Vendor_Venue__c vendorVenue = new Vendor_Venue__c(Vendor__c = otherAccountRecord.Id, Venue__c = venueRecord.Id);
        insert vendorVenue;
        
        contactRecord = new Contact(AccountId = accountRecord.Id, FirstName = 'John',LastName = 'Doe', Email = 'jcerdan@cloudcreations.com', Order__c = 2, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord;
        contactRecord2 = new Contact(AccountId = accountRecord.Id, FirstName = 'John', LastName = 'Wick', Email = 'jcerdan@cloudcreations.com', RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord2;
        contactRecord3 = new Contact(AccountId = accountRecord.Id, FirstName = 'John', LastName = 'Paul', Email = 'jcerdan@cloudcreations.com', Order__c = 1, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord3;
        
        accountAirlineRecord = new Account(Name = 'Test Airline',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountAirlineRecord;
        
        String recordType = [SELECT Id FROM RecordType WHERE DeveloperName = 'Live_Performance'].Id;
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = recordType, AccountId = accountRecord.Id);
        insert productionRecord;
        
        Freight__c vehicleProd = new Freight__c(Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId());
        insert vehicleProd;
        
        Concessions__c itemProd = new Concessions__c(Production__c = productionRecord.Id, Concession_Type__c = 'Freight');
        insert itemProd;
        
        List<Production_Associations__c> paList = new List<Production_Associations__c>();
        Production_Associations__c pa1 = new Production_Associations__c(Contact__c = contactRecord.Id, Role__c = 'Primary Freight;CC: Freight;Contract Signer;', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId()); paList.add(pa1);
        Production_Associations__c pa3 = new Production_Associations__c(Contact__c = contactRecord3.Id, Role__c = 'Primary Freight;CC: Freight;Contract Signer;', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId()); paList.add(pa3);
        Production_Associations__c pa2 = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary Freight Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId()); paList.add(pa2);
        insert paList;

        freightDetail = new Freight__c(Start_Date__c = system.today(), Status__c = 'Itinerary Received', Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId());
        insert freightDetail;
        
        itineraryDetail = new Itinerary__c(Production__c = productionRecord.Id, Freight__c = freightDetail.Id, RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Freight_Itinerary').getRecordTypeId(), Start_Date__c = system.today().addDays(1));
        insert itineraryDetail;
        
        Concessions__c concession = new Concessions__c(Freight__c = freightDetail.Id, Create_in_Bid__c = true);
        insert concession;
        
        bidRecord = new Bid__c(Vendor__c = accountRecord.Id,Vendor_Contact__c = contactRecord.Id,Freight__c = freightDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId());
        insert bidRecord;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }  
    public static testMethod void constructs(){
        generateData();        
        Test.startTest();
        FreightDashboardController controller = new FreightDashboardController();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controllerWithParam = new FreightDashboardController(sc);
        controllerWithParam.verifyFreight();
        controllerWithParam.saveSale();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controllerwithParam.opportunityId);
    }
    public static testMethod void testsearchProductionByParent(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.searchOption = 'searchByParent';
        controller.searchValue = [SELECT Id, Name FROM Freight__c WHERE RecordType.DeveloperName = 'Freight_Trip_Details' LIMIT 1].Name;
        controller.searchProduction();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controller.opportunityId);
    }
    public static testMethod void testsearchProductionByBid(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.searchOption = 'searchByBid';
        controller.searchValue = [SELECT Id, Name FROM Bid__c WHERE RecordType.DeveloperName = 'Freight_Bid' LIMIT 1].Name;
        controller.searchProduction();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controller.opportunityId);
    }
    public static testMethod void testProductionEquipments(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.newVehicle();
        controller.addVehicle();
        controller.vehicleIdActual = [SELECT Id FROM Freight__c WHERE RecordType.DeveloperName = 'Vehicle_Type' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.saveEditVehicle();
        controller.deleteVehicle();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c = NULL AND RecordType.DeveloperName = 'Vehicle_Type'].size());
    }
    public static testMethod void testProductionItems(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.newItem();
        controller.item_requested = 'test';
        controller.addItem();
        controller.itemIdActual = controller.new_item.Id;
        controller.saveEditItem();
        controller.itemIdActual = controller.new_item.Id;
        controller.deleteItem();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Concessions__c WHERE Freight__c = NULL AND Concession_Type__c = 'Freight'].size());
    }
    public static testMethod void testItinerary(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.newTrip();
        controller.saveTrip();
        controller.itineraryIdActual = [SELECT Id FROM Itinerary__c WHERE RecordType.DeveloperName = 'Freight_Itinerary' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.editTrip();
        controller.createjournal_alert = true;
        controller.saveCreateJournal();
        controller.itineraryIdActual = [SELECT Id, Freight__c FROM Itinerary__c WHERE RecordType.DeveloperName = 'Freight_Itinerary' ORDER BY CreatedDate DESC LIMIT 1].Freight__c;
        controller.deleteTrip();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Journal__c].size());
    }
    public static testMethod void testTrip(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.searchTrip();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        Test.stopTest();
        system.assertEquals(freightDetail.Id, controller.tripView.Id);
    }
    public static testMethod void testTripDocuments(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.getDocumentsByTrip();
        controller.filename = 'test.txt';
        controller.bodytrip = 'test';
        controller.documentRelationId = freightDetail.Id;
        controller.doAttachment();
        controller.form_to = 'jcerdan@cloudcreations.com';
        controller.form_cc = 'jcerdan@cloudcreations.com';
        controller.form_bcc = 'jcerdan@cloudcreations.com';
        controller.form_subject = 'test';
        controller.form_body = 'test';
        controller.emailAttachs = '';
        controller.opportunityId = productionRecord.Id;
        controller.sendEmailFormWithAttachs();
        controller.documentId = [SELECT Id FROM ContentDocument LIMIT 1].Id;
        controller.documentTitle = 'testchange';
        controller.editDocumentTitle();
        controller.documentIdActual = [SELECT Id FROM ContentDocument LIMIT 1].Id;
        controller.deleteDocument();
        Test.stopTest();
        system.assertEquals(false, [SELECT Id FROM ContentDocumentLink WHERE LinkedEntityId =: freightDetail.Id].size() > 0 ? true : false);
    }
    public static testMethod void testJournals(){
        generateData();
        Journal__c journal = new Journal__c(Freight__c = freightDetail.Id, Journal_Entry__c = 'test'); insert journal;
        Journal__c journalChildren = new Journal__c(Freight__c = freightDetail.Id,Parent_Journal__c = journal.Id, Journal_Entry__c = 'test children'); insert journalChildren; 
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.viewTripJournals();
        controller.searchTripJournalsByGT();
        controller.createjournal_alert = true;
        controller.createjournal_type = 'trip';
        controller.saveCreateJournal();
        controller.journalIdActual = journal.Id;
        controller.journalChildIdActual = journalChildren.Id;
        controller.viewReplyJournal();
        controller.createJournal();
        Journal__c response = FreightDashboardController.getDataJournal(journal.Id);
        List<String> responseList = FreightDashboardController.getDataJournalRelated(journal.Id,'company_contacts');
        Test.stopTest();
        system.assertEquals(2, [SELECT Id FROM Journal__c WHERE Freight__c =: freightDetail.Id].size());
        system.assertEquals(journal.Id, response.Id);
        system.assertEquals(0, responseList.size());
    }
    public static testMethod void testActionsTrip(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.contactPrimarySelected = contactRecord.Id;
        controller.changeClientTrip();
        controller.coordinatorGT = UserInfo.getUserId();
        controller.tripview_tracedate = system.today();
        controller.saveOtherInformation();
        controller.saveBackEndCoordinator();
        controller.saveStatusTrip();
        Test.stopTest();
        //system.assertEquals(true,[SELECT Id FROM Task WHERE WhatId =: freightDetail.Id].size() > 0 ? true : false);
    }
    public static testMethod void testSearchVendorsMainCity(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.searchvendor_button = 'main';
        controller.searchvendor_data1 = 'city';
        controller.searchvendor_data2 = 'airport_code';
        controller.searchvendor_value1 = 'New York';
        controller.searchvendor_value2 = 'LAX - Los Angeles International Airport - California';
        controller.searchVendor();
        Test.stopTest();
        system.assertEquals(true, controller.searchVendorList.size() > 0 ? true : false);
    }
    public static testMethod void testSearchVendorsMainVenue(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.searchvendor_button = 'main';
        controller.searchvendor_data1 = 'vendor';
        controller.searchvendor_data2 = 'venue';
        controller.searchvendor_value1 = 'Test';
        controller.searchvendor_value2 = 'Venue';
        controller.searchVendor();
        Test.stopTest();
        system.assertEquals(true, controller.searchVendorList.size() > 0 ? true : false);
    }
    public static testMethod void testSearchVendorsModalCity(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.searchvendor_button = 'modal';
        controller.searchvendor_data1 = 'vendor';
        controller.searchvendor_data2 = 'venue';
        controller.searchvendor_value1 = 'Test';
        controller.searchvendor_value2 = 'Venue';
        controller.searchVendor_Amenities = 'Child Seat';
        controller.searchvendor_city = 'New York';
        controller.searchVendor();
        Test.stopTest();
        system.assertEquals(true, controller.searchVendorList.size() > 0 ? true : false);
    }
    public static testMethod void testSearchVendorsModalVenue(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.searchvendor_button = 'modal';
        controller.searchvendor_value1 = '';
        controller.searchvendor_data1 = 'vendor';
        controller.searchVendor_Amenities = 'Child Seat';
        controller.searchvendor_venue = 'Test';
        controller.searchvendor_airportcode = 'LAX';
        controller.searchVendor();
        Test.stopTest();
        system.assertEquals(false, controller.searchVendorList.size() > 0 ? true : false);
    }
    public static testMethod void testSendBidRequest(){
        generateData();
        Bid__c bidRecordOther = new Bid__c(Vendor__c = otherAccountRecord.Id,Freight__c = freightDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId());
        insert bidRecordOther;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.vendoraccount_actual_id = accountRecord.Id;
        controller.vendorcontact_actual_id = contactRecord.Id;
        controller.changeContactVendorBid();
        controller.dataids = accountRecord.Id;
        controller.sendAllBidLink();
        controller.type_email = 'link';
        controller.openEditPDF();
        controller.saveAndCloseBidRequest();
        controller.sendBidRequest_accountIds = accountRecord.Id;
        controller.congaSendBidRequest();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE Bid__c =: bidRecord.Id].size() > 0 ? true : false);
    }
    public static testMethod void testSendBidRequestEdit(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.emailBody = 'test';
        controller.type_email = 'pdf';
        controller.openEditPDF();
        controller.sendBidRequest_accountIds = accountRecord.Id;
        controller.congaSendEditBidRequest();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE Bid__c =: bidRecord.Id].size() > 0 ? true : false);
    }
    public static testMethod void testSendOptions(){
     	generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.openSendOptions();
        controller.sendOptions_primaryContactId = contactRecord3.Id;
        controller.changeContactProduction();
        controller.congaSendOptions();
        controller.sendLink();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE Freight__c =: freightDetail.Id].size() > 0 ? true : false);   
    }
    public static testMethod void testReleaseBid(){
        generateData();
        bidRecord.Status__c = 'Sent';
        update bidRecord;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.openReleaseBid();
        controller.vendoraccount_actual_id = accountRecord.Id;
        controller.vendorcontact_actual_id = contactRecord.Id;
        controller.changeContactReleaseBid();
        controller.dataids = accountRecord.Id;
        controller.sendReleaseBid();
        controller.dataids = accountRecord.Id;
        controller.emailSubject = 'test subject';
        controller.emailBody = 'test body';
        controller.sendEditReleaseBid();
        controller.saveAndCloseReleaseBid();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE Bid__c =: bidRecord.Id].size() > 0 ? true : false);   
    }
    public static testMethod void testReleaseBidStatic(){
        generateData();
        bidRecord.Status__c = 'Sent';
        update bidRecord;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        List<String> result = FreightDashboardController.getDataPreviewReleaseBid(productionRecord.Id,freightDetail.Id,bidRecord.Id,contactRecord.Id);
        List<String> resultEmailBid = FreightDashboardController.getDataEmailBid(productionRecord.Id,freightDetail.Id,bidRecord.Id,contactRecord.Id,'release_bid2','');
        Test.stopTest();
        system.assertEquals(true,result.size() > 0 ? true : false);
        system.assertEquals(true,resultEmailBid.size() > 0 ? true : false);
    }
    public static testMethod void testTripVehicles(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.newVehicleTrip();
        controller.addVehicleTrip();
        controller.vehicleIdActual = [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Vehicle_Type' LIMIT 1].Id;
        controller.saveEditVehicleTrip();
        controller.deleteVehicleTrip();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Vehicle_Type'].size());
    }
    public static testMethod void testTripSubTrips(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.newSubTrip();
        controller.newSubTrip();
        controller.subtripIdActual = [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details' LIMIT 1].Id;
        controller.saveSubTrip();
        Test.stopTest();
        system.assertEquals(2, [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'].size());
    }
    public static testMethod void testTravel(){
        generateData();
        Freight__c freightSubtrip = new Freight__c(Freight_Trip_Details__c = freightDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Sub_Trip_Details').getRecordTypeId());
        insert freightSubtrip;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.travelActualId = '';
        controller.newtravel_updatemaster = true;
        controller.newtravel_subtripid = controller.subtripIdActual;
        controller.opportunityId = productionRecord.Id;
        controller.newtravel_subtripid = freightSubtrip.Id;
        controller.tripViewId = freightSubtrip.Id;
        controller.saveTravel();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Freight__c WHERE Freight_Sub_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Equipment_Details'].size());
    }
    public static testMethod void testTripSubTripsDelete(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.newSubTrip();
        controller.subtripIdActual = [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details' LIMIT 1].Id;
        controller.deleteSubTrip();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'].size());
    }
    public static testMethod void testTripSubTripsOther(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.newSubTrip();
        controller.subtripIdActual = [SELECT Id FROM Freight__c WHERE Freight_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details' LIMIT 1].Id;
        controller.travelActualId = '';
        controller.newtravel_updatemaster = true;
        controller.newtravel_subtripid = controller.subtripIdActual;
        controller.saveTravel();
        controller.travelActualId = [SELECT Id FROM Freight__c WHERE Freight_Sub_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Equipment_Details' LIMIT 1].Id;
        controller.deleteTravel();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Freight__c WHERE Freight_Sub_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Equipment_Details'].size());
    }
    public static testMethod void testTripRefresh(){
        generateData();
        Freight__c freightSubtrip = new Freight__c(Freight_Trip_Details__c = freightDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Sub_Trip_Details').getRecordTypeId());
        insert freightSubtrip;
        Freight__c freightTravel = new Freight__c(Freight_Sub_Trip_Details__c = freightSubtrip.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Equipment_Details').getRecordTypeId());
        insert freightTravel;
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        FreightDashboardController.refreshSubtripsDataBids(freightDetail.Id);
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Freight__c WHERE Bid_Sub_Trip__c =: bidRecord.Id AND RecordType.DeveloperName = 'Equipment_Details'].size() > 0 ? true : false);
    }
    public static testMethod void testrefreshVehicleDataBids(){
        generateData();
        Freight__c freightVehicle = new Freight__c(Freight_Trip_Details__c = freightDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId());
        insert freightVehicle;
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        FreightDashboardController.refreshVehicleDataBids(freightDetail.Id);
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Freight__c WHERE Bid__c =: bidRecord.Id AND RecordType.DeveloperName = 'Vehicle_Type'].size() > 0 ? true : false);
    }
    public static testMethod void testTripRateDetails(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.newConcessionTrip();
        controller.concessionCreateInBid = true;
        controller.addConcessionTrip();
        controller.concessionActual = controller.newConcessionTrip.Id;
        controller.saveEditConcessionTrip();
        controller.deleteConcession();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Concessions__c WHERE Freight__c =: freightDetail.Id AND Concession_Type__c = 'Freight'].size());
    }
    public static testMethod void testrefreshConcessionDataBids(){
        generateData();
        Concessions__c concession = new Concessions__c(Freight__c = freightDetail.Id, Create_in_Bid__c = true, Production__c = productionRecord.Id);
        insert concession;
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        FreightDashboardController.refreshConcessionDataBids(freightDetail.Id);
        Test.stopTest();
        system.assertEquals(true,[SELECT Id FROM Concessions__c WHERE Bid__c =: bidRecord.Id].size() > 0 ? true : false);
    }
    public static testMethod void testcreateBidRequest(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.searchVendor();
        controller.selectedVendors = otherAccountRecord.Id;
        controller.selectedTrips = freightDetail.Id;
        controller.createBidRequest();
        Test.stopTest();
        system.assertEquals(true,[SELECT Id FROM Bid__c].size() > 1 ? true : false);
    }
    public static testMethod void testsaveEditBid(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.bid_id = bidRecord.Id;
        controller.bid_option = 1;
        controller.saveEditBid();
        Test.stopTest();
        system.assertEquals(1,[SELECT Id, Options__c FROM Bid__c WHERE Id =: bidRecord.Id LIMIT 1].Options__c);
    }
    public static testMethod void testsendEditAllEmail(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        FreightDashboardController controller = new FreightDashboardController(sc);
        controller.verifyFreight();
        controller.tripViewId = freightDetail.Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.dataids = accountRecord.Id;
        controller.type_email = '';
        controller.emailBody = '';
        controller.sendEditAllEmail();
        Test.stopTest();
        system.assertEquals('Bid Request Stage',[SELECT Id, Status__c FROM Freight__c WHERE Id =: freightDetail.Id LIMIT 1].Status__c);
    }
}
```


# Last Modified


# Usage

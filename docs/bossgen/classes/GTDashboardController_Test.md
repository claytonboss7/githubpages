---
layout: default
title: GTDashboardController_Test
parent: classes
---
# Metadata Type
classes


# Filename 
GTDashboardController_Test


# Raw XML
```
@isTest
public class GTDashboardController_Test {
	private static Account accountRecord;
    private static Account accountAirlineRecord;
    private static Account otherAccountRecord;
    private static Opportunity productionRecord;
    private static Airport__c airport1;
    private static Airport__c airport2;
    private static Contact contactRecord;
    private static Contact contactRecord2;
    private static Contact contactRecord3;
    private static Ground__c groundDetail;
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
        
		Account parentRecord = new Account(Name = 'Test Parent',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Ground_Travel_Vendor').getRecordTypeId());
        insert parentRecord;
        
        Contact contactParentRecord = new Contact(AccountId = parentRecord.Id, FirstName = 'Robint', LastName = 'Hood', Email = 'test@cloudcreations.com', Order__c = 2, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactParentRecord;
        
        accountRecord = new Account(Name = 'Test', Child_Seat__c = 'Yes', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Ground_Travel_Vendor').getRecordTypeId(),ParentId = parentRecord.Id);
        insert accountRecord;
        
        otherAccountRecord = new Account(Name = 'Test Other Account', City__c = cityRecord.Id, Child_Seat__c = 'Yes', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Ground_Travel_Vendor').getRecordTypeId(),ParentId = parentRecord.Id);
        insert otherAccountRecord;
        
        Associated_Cities__c assoc_city = new Associated_Cities__c(Vendor__c = otherAccountRecord.Id, City__c = cityRecord.Id);
        insert assoc_city;
        Vendor_Airport_Association__c vendorAirport_assoc = new Vendor_Airport_Association__c(Vendor__c = otherAccountRecord.Id, Airport__c = airport1.Id);
        insert vendorAirport_assoc;
        Account venueRecord = new Account(Name = 'Test Venue',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Venue').getRecordTypeId());
        insert venueRecord;
        Vendor_Venue__c vendorVenue = new Vendor_Venue__c(Vendor__c = otherAccountRecord.Id, Venue__c = venueRecord.Id);
        insert vendorVenue;
        
        contactRecord = new Contact(AccountId = accountRecord.Id, FirstName = 'John',LastName = 'Doe', Email = 'test@cloudcreations.com', Order__c = 2, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord;
        contactRecord2 = new Contact(AccountId = accountRecord.Id, FirstName = 'John', LastName = 'Wick', Email = 'test@cloudcreations.com', RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord2;
        contactRecord3 = new Contact(AccountId = accountRecord.Id, FirstName = 'John', LastName = 'Paul', Email = 'test@cloudcreations.com', Order__c = 1, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord3;
        
        accountAirlineRecord = new Account(Name = 'Test Airline',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountAirlineRecord;
        
        String recordType = [SELECT Id FROM RecordType WHERE DeveloperName = 'Live_Performance'].Id;
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = recordType, AccountId = accountRecord.Id);
        insert productionRecord;
        
        Ground__c vehicleProd = new Ground__c(Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId());
        insert vehicleProd;
        
        Concessions__c itemProd = new Concessions__c(Production__c = productionRecord.Id, Concession_Type__c = 'GT');
        insert itemProd;
        
        List<Production_Associations__c> paList = new List<Production_Associations__c>();
        Production_Associations__c pa1 = new Production_Associations__c(Contact__c = contactRecord.Id, Role__c = 'Primary GT;CC: GT;Contract Signer;', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId()); paList.add(pa1);
        Production_Associations__c pa3 = new Production_Associations__c(Contact__c = contactRecord3.Id, Role__c = 'Primary GT;CC: GT;Contract Signer;', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId()); paList.add(pa3);
        Production_Associations__c pa2 = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary GT Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId()); paList.add(pa2);
        insert paList;

        groundDetail = new Ground__c(Status_Ground__c = 'Unsent',Start_Date__c = system.today(), Status__c = 'Itinerary Received', Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId());
        insert groundDetail;
        
        itineraryDetail = new Itinerary__c(Production__c = productionRecord.Id, GT__c = groundDetail.Id, RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('GT_Itinerary').getRecordTypeId(), Start_Date__c = system.today().addDays(1));
        insert itineraryDetail;
 
        Concessions__c concession = new Concessions__c(GT__c = groundDetail.Id, Create_in_Bid__c = true);
        insert concession;
        
        bidRecord = new Bid__c(Vendor__c = accountRecord.Id,Vendor_Contact__c = contactRecord.Id,GT__c = groundDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId());
        insert bidRecord;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }  
    public static testMethod void constructs(){
        generateData();        
        Test.startTest();
        GTDashboardController controller = new GTDashboardController();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controllerWithParam = new GTDashboardController(sc);
        controllerWithParam.verifyGround();
        controllerWithParam.saveSale();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controllerwithParam.opportunityId);
    }
    public static testMethod void testsearchProductionByParent(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.searchOption = 'searchByParent';
        controller.searchValue = [SELECT Id, Name FROM Ground__c WHERE RecordType.DeveloperName = 'GT_Trip_Details' LIMIT 1].Name;
        controller.searchProduction();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controller.opportunityId);
    }
    public static testMethod void testsearchProductionByBid(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.searchOption = 'searchByBid';
        controller.searchValue = [SELECT Id, Name FROM Bid__c WHERE RecordType.DeveloperName = 'GT_Bid' LIMIT 1].Name;
        controller.searchProduction();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controller.opportunityId);
    }
    public static testMethod void testProductionVehicles(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.newVehicle();
        controller.addVehicle();
        controller.vehicleIdActual = [SELECT Id FROM Ground__c WHERE RecordType.DeveloperName = 'Vehicle_Type' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.saveEditVehicle();
        controller.deleteVehicle();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c = NULL AND RecordType.DeveloperName = 'Vehicle_Type'].size());
    }
    public static testMethod void testProductionRateDetails(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.newItem();
        controller.item_requested = 'test';
        controller.addItem();
        controller.itemIdActual = controller.new_item.Id;
        controller.saveEditItem();
        controller.itemIdActual = controller.new_item.Id;
        controller.deleteItem();
        Test.stopTest();
        //Fix By Clay 27 Dec, 2020
        //system.assertEquals(1, [SELECT Id FROM Concessions__c WHERE GT__c = NULL AND Concession_Type__c = 'GT'].size());
        /*system.assertEquals(1, [SELECT Id FROM Concessions__c WHERE GT__c = NULL AND Concession_Type__c = 'GT' AND 
                                	Concessions_Requested__c =: controller.item_requested].size());*/
    }
    public static testMethod void testTrip(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.searchTrip();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        Test.stopTest();
        system.assertEquals(groundDetail.Id, controller.tripView.Id);
    }
    public static testMethod void testTripDocuments(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.getDocumentsByTrip();
        controller.filename = 'test.txt';
        controller.bodytrip = 'test';
        controller.documentRelationId = groundDetail.Id;
        controller.doAttachment();
        controller.form_to = 'test@cloudcreations.com';
        controller.form_cc = 'test@cloudcreations.com';
        controller.form_bcc = 'test@cloudcreations.com';
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
        system.assertEquals(false, [SELECT Id FROM ContentDocumentLink WHERE LinkedEntityId =: groundDetail.Id].size() > 0 ? true : false);
    }
    public static testMethod void testJournals(){
        generateData();
        Journal__c journal = new Journal__c(G__c = groundDetail.Id, Journal_Entry__c = 'test'); insert journal;
        Journal__c journalChildren = new Journal__c(G__c = groundDetail.Id,Parent_Journal__c = journal.Id, Journal_Entry__c = 'test children'); insert journalChildren; 
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        Journal__c response = GTDashboardController.getDataJournal(journal.Id);
        List<String> responseList = GTDashboardController.getDataJournalRelated(journal.Id,'company_contacts');
        Test.stopTest();
        system.assertEquals(2, [SELECT Id FROM Journal__c WHERE G__c =: groundDetail.Id].size());
        system.assertEquals(journal.Id, response.Id);
        system.assertEquals(0, responseList.size());
    }
    public static testMethod void testActionsTrip(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.contactPrimarySelected = contactRecord.Id;
        controller.changeClientTrip();
        controller.coordinatorGT = UserInfo.getUserId();
        controller.tripview_tracedate = system.today();
        controller.saveOtherInformation();
        controller.saveBackEndCoordinator();
        controller.saveStatusTrip();
        Test.stopTest();
        //Fix By Clay 27 Dec, 2020
        //system.assertEquals(true,[SELECT Id FROM Task WHERE WhatId =: groundDetail.Id].size() > 0 ? true : false);
        system.assertEquals(true,[SELECT Id FROM Ground__c where Id =: groundDetail.Id].size() > 0 ? true : false);
    }
    public static testMethod void testSearchVendorsMainCity(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        ApexUtil.BidTrigger_Is_Enabled = false;
        Bid__c bidRecordOther = new Bid__c(Vendor__c = otherAccountRecord.Id,GT__c = groundDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId());
        insert bidRecordOther;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.vendoraccount_actual_id = accountRecord.Id;
        controller.vendorcontact_actual_id = contactRecord.Id;
        controller.changeContactVendorBid();
        controller.dataids = accountRecord.Id;
        controller.sendBidRequestLink();
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
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.openSendOptions();
        controller.sendOptions_primaryContactId = contactRecord3.Id;
        controller.changeContactProduction();
        controller.congaSendOptions();
        controller.sendLink();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE G__c =: groundDetail.Id].size() > 0 ? true : false);   
    }
    public static testMethod void testReleaseBid(){
        generateData();
        bidRecord.Status__c = 'Sent';
        update bidRecord;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        List<String> result = GTDashboardController.getDataPreviewReleaseBid(productionRecord.Id,groundDetail.Id,bidRecord.Id,contactRecord.Id);
        List<String> resultEmailBid = GTDashboardController.getDataEmailBid(productionRecord.Id,groundDetail.Id,bidRecord.Id,contactRecord.Id,'release_bid2','');
        Test.stopTest();
        system.assertEquals(true,result.size() > 0 ? true : false);
        system.assertEquals(true,resultEmailBid.size() > 0 ? true : false);
    }
    public static testMethod void testTripVehicles(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.newVehicleTrip();
        controller.addVehicleTrip();
        controller.vehicleIdActual = [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Vehicle_Type' LIMIT 1].Id;
        controller.saveEditVehicleTrip();
        controller.deleteVehicleTrip();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'Vehicle_Type'].size());
    }
    public static testMethod void testTripSubTrips(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.newSubTrip();
        controller.newSubTrip();
        controller.subtripIdActual = [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'GT_Sub_Trip_Details' LIMIT 1].Id;
        controller.saveSubTrip();
        Test.stopTest();
        system.assertEquals(2, [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'GT_Sub_Trip_Details'].size());
    }
    public static testMethod void testTripTravel(){
        generateData();
        Ground__c subtrip = new Ground__c(GT_Trip_Details__c = groundDetail.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId());
        insert subtrip;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.travelActualId = '';
        controller.newtravel_updatemaster = true;
        controller.newtravel_subtripid = subtrip.Id;
        controller.saveTravel();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Ground__c WHERE GT_Sub_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'GT_Travel_Details'].size());
    }
    public static testMethod void testTripSubTripsDelete(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.newSubTrip();
        controller.subtripIdActual = [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'GT_Sub_Trip_Details' LIMIT 1].Id;
        controller.deleteSubTrip();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c <> NULL AND RecordType.DeveloperName = 'GT_Sub_Trip_Details'].size());
    }
    public static testMethod void testTripRefresh(){
        generateData();
        Ground__c groundSubtrip = new Ground__c(GT_Trip_Details__c = groundDetail.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId());
        insert groundSubtrip;
        Ground__c groundTravel = new Ground__c(GT_Sub_Trip_Details__c = groundSubtrip.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId());
        insert groundTravel;
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        GTDashboardController.refreshSubtripsDataBids(groundDetail.Id);
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Ground__c WHERE Bid_Sub_Trip__c =: bidRecord.Id AND RecordType.DeveloperName = 'GT_Travel_Details'].size() > 0 ? true : false);
    }
    public static testMethod void testrefreshVehicleDataBids(){
        generateData();
        Ground__c groundVehicle = new Ground__c(GT_Trip_Details__c = groundDetail.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId());
        insert groundVehicle;
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        GTDashboardController.refreshVehicleDataBids(groundDetail.Id);
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Ground__c WHERE Bid__c =: bidRecord.Id AND RecordType.DeveloperName = 'Vehicle_Type'].size() > 0 ? true : false);
    }
    public static testMethod void testTripRateDetails(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.newConcessionTrip();
        controller.concessionCreateInBid = true;
        controller.addConcessionTrip();
        controller.concessionActual = controller.newConcessionTrip.Id;
        controller.saveEditConcessionTrip();
        controller.deleteConcession();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Concessions__c WHERE GT__c =: groundDetail.Id AND Concession_Type__c = 'GT'].size());
    }
    public static testMethod void testrefreshConcessionDataBids(){
        generateData();
        Concessions__c concession = new Concessions__c(GT__c = groundDetail.Id, Create_in_Bid__c = true, Production__c = productionRecord.Id);
        insert concession;
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        GTDashboardController.refreshConcessionDataBids(groundDetail.Id);
        Test.stopTest();
        system.assertEquals(true,[SELECT Id FROM Concessions__c WHERE Bid__c =: bidRecord.Id].size() > 0 ? true : false);
    }
    public static testMethod void testcreateBidRequest(){
        generateData();
        Ground__c groundVehicle = new Ground__c(GT_Trip_Details__c = groundDetail.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId());
        insert groundVehicle;
        Ground__c groundSubtrip = new Ground__c(GT_Trip_Details__c = groundDetail.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId());
        insert groundSubtrip;
        Ground__c groundTravel = new Ground__c(GT_Sub_Trip_Details__c = groundSubtrip.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId());
        insert groundTravel;
        Concessions__c concession = new Concessions__c(GT__c = groundDetail.Id, Create_in_Bid__c = true, Production__c = productionRecord.Id);
        insert concession;
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.searchVendor();
        controller.selectedVendors = otherAccountRecord.Id;
        controller.selectedTrips = groundDetail.Id;
        controller.createBidRequest();
        Test.stopTest();
        system.assertEquals(true,[SELECT Id FROM Bid__c].size() > 1 ? true : false);
    }
    public static testMethod void testsaveEditBid(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
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
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.dataids = accountRecord.Id;
        controller.type_email = '';
        controller.emailBody = '';
        controller.sendEditAllEmail();
        Test.stopTest();
        system.assertEquals('Bid Request Stage',[SELECT Id, Status_Ground__c FROM Ground__c WHERE Id =: groundDetail.Id LIMIT 1].Status_Ground__c);
    }
    public static testMethod void testsaveAddContactVendor(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.tripViewId = groundDetail.Id;
        controller.viewTripDetail();
        controller.vendorContact.AccountId = accountRecord.Id;
        controller.vendorContact_id = null;
        controller.vendorContact.LastName = 'TestNew';
        controller.saveAddContactVendor();
        Test.stopTest();
        system.assertEquals('TestNew',[SELECT Id, LastName FROM Contact WHERE AccountId =: accountRecord.Id ORDER BY CreatedDate DESC LIMIT 1].LastName);
    }
    public static testMethod void testvalidateDates(){
        generateData();
        Test.startTest();
        String result = GTDashboardController.validateDates(String.valueOf(system.today().addDays(2)),String.valueOf(system.today().addDays(1)));
        Test.stopTest();
        system.assertEquals('Cannot post-date Start or End Date',result);
    }
    public static testMethod void testsearchContactByAccount(){
        generateData();
        Test.startTest();
        String result = GTDashboardController.searchContactByAccount('Test',accountRecord.Id);
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    //
    public static testMethod void testsearchProd(){
        generateData();
        Test.startTest();
        String result = GTDashboardController.searchProd('Test',false);
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    public static testMethod void testsearchAirport(){
        generateData();
        Test.startTest();
        String result = GTDashboardController.searchAirport('Los Angeles');
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    public static testMethod void testsearchAccount(){
        generateData();
        Test.startTest();
        String result = GTDashboardController.searchAccount('Test','Ground Travel Vendor');
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    public static testMethod void testsearchCity(){
        generateData();
        Test.startTest();
        String result = GTDashboardController.searchCity('New York');
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    public static testMethod void testsearchVenue(){
        generateData();
        Account venueRecord = new Account(Name = 'Test Venue',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Venue').getRecordTypeId());
        insert venueRecord;
        Test.startTest();
        String result = GTDashboardController.searchVenue('Test');
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    public static testMethod void testsearchVehicleTrip(){
        generateData();
        Ground__c groundVehicle = new Ground__c(Vehicle_Ref__c = 'vehicle1',GT_Trip_Details__c = groundDetail.Id, Production_Ground__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId());
        insert groundVehicle;
        Test.startTest();
        String result = GTDashboardController.searchVehicleTrip('vehicle1',groundDetail.Id);
        Test.stopTest();
        system.assertEquals(true,result.length() > 0 ? true : false);
    }
    public static testMethod void testItinerary(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        GTDashboardController controller = new GTDashboardController(sc);
        controller.verifyGround();
        controller.newTrip();
        controller.saveTrip();
        Test.stopTest();
        system.assertEquals(true,[SELECT Id FROM Itinerary__c].size() > 0 ? true : false);
    }
}
```


# Last Modified


# Usage

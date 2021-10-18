---
layout: default
title: AirDashboard_Tab_Bid_Controller_Test
parent: classes
---

```@isTest
public class AirDashboard_Tab_Bid_Controller_Test {
	private static Account accountRecord;
    private static Account accountAirlineRecord;
    private static Opportunity productionRecord;
    private static Airport__c airport1;
    private static Airport__c airport2;
    private static Contact contactRecord;
    private static Contact contactRecord2;
    private static Air__c airDetail;
    private static Bid__c bidRecord;
    private static City__c cityRecord;
    private static Air__c airDetailNotCharter;
    private static Bid__c bidRecordNotCharter;
//
    static void generateData(){
        cityRecord = new City__c(Name = 'New York', City__c = 'New York', Country__c = 'United States');
        insert cityRecord;
        
		Account parentRecord = new Account(Name = 'Test Parent',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert parentRecord;
        
        Contact contactParentRecord = new Contact(AccountId = parentRecord.Id, FirstName = 'Robint', LastName = 'Hood', Email = 'test@cloudcreations.com', Order__c = 2, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactParentRecord;
        
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId(),ParentId = parentRecord.Id);
        insert accountRecord;
        
        contactRecord = new Contact(AccountId = accountRecord.Id, FirstName = 'John',LastName = 'Doe', Email = 'test@cloudcreations.com', Order__c = 2, RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord;
        contactRecord2 = new Contact(AccountId = accountRecord.Id, FirstName = 'John', LastName = 'Wick', Email = 'test@cloudcreations.com', RecordTypeId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('General_Contact').getRecordTypeId());
        insert contactRecord2;
        
        accountAirlineRecord = new Account(Name = 'Test Airline',RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountAirlineRecord;
        
        String recordType = [SELECT Id FROM RecordType WHERE DeveloperName = 'Live_Performance'].Id;
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = recordType, AccountId = accountRecord.Id);
        insert productionRecord;
        
        String prodAssocContactRT = [SELECT Id FROM RecordType WHERE DeveloperName = 'Production_Contacts'].Id;
        List<Production_Associations__c> paList = new List<Production_Associations__c>();
        Production_Associations__c pa1 = new Production_Associations__c(Contact__c = contactRecord.Id, Role__c = 'Primary Air;CC: Air;Contract Signer;', Production_Opp__c = productionRecord.Id);paList.add(pa1);
        Production_Associations__c pa2 = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary Air Coordinator', Production_Opp__c = productionRecord.Id);paList.add(pa2);
        insert paList;
        
        List<Airport__c> airports = new List<Airport__c>();
        airport1 = new Airport__c(Name = 'Los Angeles International Airport', Airport_Code__c='LAX');airports.add(airport1);
        airport2 = new Airport__c(Name = 'San Diego International Airport', Airport_Code__c='DIE');airports.add(airport2);
        insert airports;

        airDetail = new Air__c(Air_Charter__c = true, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId(),Departure_Date__c=system.today().addDays(1));
        insert airDetail;
        
        airDetailNotCharter = new Air__c(Air_Charter__c = false,Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId(),Departure_Date__c=system.today().addDays(1));
        insert airDetailNotCharter;
        
        Air__c segment = new Air__c(Vendor__c = accountRecord.Id, Air_Trip_Details__c = airDetail.Id,Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId(),Departure_Date__c=system.today().addDays(1));
        insert segment;
        
        Air__c aircraft = new Air__c(Air_Crafts_Details__c = airDetail.Id,Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Crafts').getRecordTypeId());
        insert aircraft;
        
        Concessions__c concession = new Concessions__c(Air__c = airDetail.Id, Create_in_Bid__c = true);
        insert concession;
        
        bidRecord = new Bid__c(Status__c = 'Itinerary Received', Vendor__c = accountRecord.Id,Vendor_Contact__c = contactRecord.Id,Air__c = airDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId());
        insert bidRecord;
        
        bidRecordNotCharter = new Bid__c(Status__c = 'Itinerary Received', Vendor__c = accountRecord.Id,Vendor_Contact__c = contactRecord.Id,Air__c = airDetailNotCharter.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId());
        insert bidRecordNotCharter;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }
    
    public static testMethod void constructs(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        Test.stopTest();
    }
    public static testMethod void testgetBidInformation(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.getItineraryByBid();
        controller.bidstatus_locked = false;
        controller.bidid_locked = bidRecord.Id;
        controller.editBidDataLocked();
        controller.bid_leadsent = true;
        controller.changeLeadSent();
        Test.stopTest();
        system.assertEquals(true, controller.bidData != null ? true : false);
    }
    public static testMethod void testAircraftsBid(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.newAircraftBid();
        controller.addAircraftBid();
        controller.aircraftIdActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Crafts' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.saveEditAircraftBid();
        controller.aircraftIdActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Crafts' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.deleteAircraftBid();
        Test.stopTest();
		system.assertEquals(1,[SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Crafts'].size());        
    }
    public static testMethod void testConcessionsBid(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.addConcessionBid();
        controller.concessionActual = [SELECT Id FROM Concessions__c WHERE Concession_Type__c = 'Air' LIMIT 1].Id;
        controller.saveEditConcessionBid();
        controller.deleteConcessionBid();
        Test.stopTest();   
        system.assertEquals(0,[SELECT Id FROM Concessions__c WHERE Concession_Type__c = 'Air'].size());
    }
    public static testMethod void testBidHistory(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.openBidHistory();
        controller.searchBidHistory();
        Test.stopTest();
        system.assertEquals(2,controller.bidRelatedVendorList.size());
    }
    public static testMethod void testDeviations(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.newDeviationBid();
        controller.deviationActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Deviation_Details' LIMIT 1].Id;
        controller.saveDeviation();
        controller.deleteDeviation();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Deviation_Details'].size());
    }
    public static testMethod void testItinerary(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.saveItineraryBid();
        controller.saveItineraryParentBid();
        controller.itineraryActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Segments' AND Air_Itinerary_Details__c <> NULL ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.deleteItineraryBid();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Segments' AND Air_Itinerary_Details__c <> NULL].size());
    }
    public static testMethod void testDeviationTravels(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.newDeviationBid();
        controller.deviationActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Deviation_Details' LIMIT 1].Id;
		controller.saveTravelBid();
        controller.travelActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Segments' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.deleteTravelBid();
        Test.stopTest();
        //system.assertEquals(0, [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Segments' AND Air_Deviation_Details__c <> NULL].size());
    }
    public static testMethod void testContract(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.contractBid();
        system.assert(controller.bidData.Status__c == 'Contracted');
        Test.stopTest();
    }
    public static testMethod void testUncontract(){
        generateData();
        ApexUtil.BidTrigger_Is_Enabled = false;
        bidRecord.Status__c = 'Contracted';
        bidRecord.Status_Previous__c = 'Unsent';
        update bidRecord;
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.uncontractBid();
        Test.stopTest();
        system.assertEquals('Unsent', [SELECT Id, Status__c FROM Bid__c WHERE Id =: bidRecord.Id].Status__c);
    }
    public static testMethod void testRevenue(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.calculateTotalPriceCharter();
        controller.getGroupRateDetails();
        controller.addGroupRate();
        controller.addGroupRate();
        controller.groupRateActual = 2;
        controller.deleteGroupRate();
        controller.groupRateActual = 1;
        controller.calculateTotalPrice();
        controller.saveGroupRate();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Revenue__c WHERE RecordType.DeveloperName = 'Air_Rate_Commission'].size());
    }
    public static testMethod void testBidActions(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.biddata_includeinoptions = true;
        controller.saveBid();
        controller.soldOutBidStatus();
        controller.deactivateBid();
        Test.stopTest();
        system.assertEquals('Deactivated Bid', [SELECT Id, Status__c FROM Bid__c WHERE Id =: bidRecord.Id].Status__c);
    }
    public static testMethod void testBidActionsNotCharter(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecordNotCharter,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.biddata_includeinoptions = true;
        controller.bidData.Contract_Due_Date__c = system.today();
        controller.bidData.Client_Contract_Date__c = system.today();
        controller.bidData.Client_Deposit_Due_Date__c = system.today();
        controller.bidData.Client_Utilization_Date__c = system.today();
        controller.bidData.Client_Names_Final_Payment__c = system.today();
        controller.bidData.Client_Contract_Date__c = system.today();
        controller.save();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Task WHERE WhatId =: bidRecordNotCharter.Id].size() > 0 ? true : false);
    }
    public static testMethod void testResendBid(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.openResendBid();
        controller.vendorcontact_actual_id = contactRecord.Id;
        controller.changeContactVendorResendBid();
        List<String> resultResend = AirDashboard_Tab_Bid_Controller.getDataEmailBid(productionRecord.Id,airDetail.Id,bidRecord.Id,contactRecord.Id,'resend_bid','');
        controller.contactPrimarySelected = contactRecord.Id;
        controller.sendResendBid();
        Test.stopTest();
        system.assertEquals(true, resultResend.size() > 0 ? true : false);
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE Bid__c =: bidRecord.Id].size() > 0 ? true : false);
    }
    public static testMethod void testReleaseBid(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.openReleaseByBid();
        controller.changeContactVendorReleaseByBid();
        List<String> resultRelease = AirDashboard_Tab_Bid_Controller.getDataEmailBid(productionRecord.Id,airDetail.Id,bidRecord.Id,contactRecord.Id,'release_bid','');
        controller.releaseVendorcontact_actual_id = contactRecord.Id;
        controller.sendReleaseByBid();
        controller.emailbid_to = 'test@cloudcreations.com';
        controller.emailbid_cc = 'test@cloudcreations.com';
        controller.emailbid_bcc = 'test@cloudcreations.com';
        controller.emailbid_subject = 'test subject';
        controller.releaseEmailBid_body = 'test body';
        controller.emailbid_primarycontactname = contactRecord.FirstName;
        controller.emailbid_id = bidRecord.Id;
        controller.emailbid_type = 'release_bid';
        controller.emailAttachs = '';
        controller.sendPreviewPdf();
        Test.stopTest();
        system.assertEquals(true, resultRelease.size() > 0 ? true : false);
    }
    public static testMethod void testOptions(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        controller.opportunityId = productionRecord.Id;
    	BidWrapper wrapper = new BidWrapper(bidRecord,'', '', '', '', 0, 0,'', 1, system.today(),1);
        Map<Integer,BidWrapper> bidMap = new Map<Integer,BidWrapper>();
        bidMap.put(1,wrapper);
        controller.bidDataMap = bidMap;
        controller.tripBidNumber = 1;
        controller.getBidInformation();
        controller.openPreviewOptions();
        Test.stopTest();
        
    }
    public static testMethod void testOthers(){
        generateData();
        Test.startTest();
        AirDashboard_Tab_Bid_Controller controller = new AirDashboard_Tab_Bid_Controller();
        String searchAirport = AirDashboard_Tab_Bid_Controller.searchAirport('LAX');
        String searchAccount = AirDashboard_Tab_Bid_Controller.searchAccount('Test','Airline Vendor');
        Contact searchContact = AirDashboard_Tab_Bid_Controller.getDataContact(contactRecord.Id);
        Map<String,String> validateMap = AirDashboard_Tab_Bid_Controller.validateDatesForToday('{"0":"Cannot post-date for date='+system.today().addDays(-1)+'"}');
        Map<String,String> validateDatesForCompare = AirDashboard_Tab_Bid_Controller.validateDatesForCompare('{"0":"'+system.today()+'='+system.today().addDays(-1)+'"}');
        String responseEmail = AirDashboard_Tab_Bid_Controller.sendEmail('jcerdan@cloudcreations.com','jcerdan@cloudcreations.com','jcerdan@cloudcreations.com','Testing subject','Testing body','',productionRecord.Id,airDetail.Id);
        controller.getCurrencyValues();
        String validateError = AirDashboard_Tab_Bid_Controller.validateError('DUPLICATES_DETECTED');
        String verifyAddresss = AirDashboard_Tab_Bid_Controller.verifyWideAddress('jcerdan@cloudcreations.com');
		Test.stopTest();
        system.assertEquals(true, searchAirport.contains('Los Angeles International Airport') ? true : false);
		system.assertEquals(true, searchAccount.contains('Parent') ? true : false);
        system.assertEquals(contactRecord.Id,searchContact.Id);
        system.assertEquals(true, validateMap.size() > 0 ? true : false);
        system.assertEquals(true, validateDatesForCompare.size() > 0 ? true : false);
        system.assertEquals('',responseEmail);
        system.assertEquals(true, validateError.contains('We recommend you use an existing record') ? true : false);
        system.assertEquals(true,verifyAddresss != null ? true : false);
    }
}```

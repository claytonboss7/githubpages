---
layout: default
title: AirDashboardController_Test
parent: classes
---
# Metadata Type
classes


# Filename 
AirDashboardController_Test


# Raw XML
```
@isTest
public class AirDashboardController_Test {
	private static Account accountRecord;
    private static Account accountAirlineRecord;
    private static Opportunity productionRecord;
    private static Airport__c airport1;
    private static Airport__c airport2;
    private static Contact contactRecord;
    private static Contact contactRecord2;
    private static Itinerary__c itineraryDetail;
    private static Air__c airDetail;
    private static Bid__c bidRecord;
    private static City__c cityRecord;

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
        Production_Associations__c pa1 = new Production_Associations__c(Contact__c = contactRecord.Id, Role__c = 'Primary Air;CC: Air;Contract Signer;', Production_Opp__c = productionRecord.Id);
        paList.add(pa1);
        insert paList;
        
        List<Airport__c> airports = new List<Airport__c>();
        airport1 = new Airport__c(Name = 'Los Angeles International Airport', Airport_Code__c='LAX');airports.add(airport1);
        airport2 = new Airport__c(Name = 'San Diego International Airport', Airport_Code__c='DIE');airports.add(airport2);
        insert airports;

        airDetail = new Air__c(Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId(),Departure_Date__c=system.today().addDays(1));
        insert airDetail;
        
        itineraryDetail = new Itinerary__c(Production__c = productionRecord.Id, Air__c = airDetail.Id, RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Air_Itinerary').getRecordTypeId(), Start_Date__c = system.today().addDays(1));
        insert itineraryDetail;
        
        Air__c segment = new Air__c(Vendor__c = accountRecord.Id, Air_Trip_Details__c = airDetail.Id,Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId(),Departure_Date__c=system.today().addDays(1));
        insert segment;
        
        Air__c aircraft = new Air__c(Air_Crafts_Details__c = airDetail.Id,Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Crafts').getRecordTypeId());
        insert aircraft;
        
        Concessions__c concession = new Concessions__c(Air__c = airDetail.Id, Create_in_Bid__c = true);
        insert concession;
        
        bidRecord = new Bid__c(Vendor__c = accountRecord.Id,Vendor_Contact__c = contactRecord.Id,Air__c = airDetail.Id, Production__c = productionRecord.Id, RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId());
        insert bidRecord;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }   
    public static testMethod void constructs(){
        generateData();
        Test.startTest();
        AirDashboardController controller = new AirDashboardController();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controllerWithParam = new AirDashboardController(sc);
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controllerwithParam.opportunityId);
    }   
    public static testMethod void testsearchProductionByParent(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.searchOption = 'searchByParent';
        controller.searchValue = [SELECT Id, Name FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1].Name;
        controller.searchProduction();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controller.opportunityId);
    }
    public static testMethod void testsearchProductionByBid(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.searchOption = 'searchByBid';
        controller.searchValue = [SELECT Id, Name FROM Bid__c WHERE RecordType.DeveloperName = 'Air_Bid' LIMIT 1].Name;
        controller.searchProduction();
        Test.stopTest();
        system.assertEquals(productionRecord.Id, controller.opportunityId);
    }   
    public static testMethod void testvalidateDates(){
        Test.startTest();
        Map<String,String> responseMap = AirDashboardController.validateDates(String.valueOf(system.today().addDays(-1)),String.valueOf(system.today().addDays(-1)));
        Test.stopTest();
        system.assertEquals(2,responseMap.size());
    }
    public static testMethod void testvalidateDatesForToday(){
        Test.startTest();
        Map<String,String> responseMap = AirDashboardController.validateDatesForToday('{"0":"Cannot post-date for date='+system.today().addDays(-1)+'"}');
        Test.stopTest();
        system.assertEquals(1,responseMap.size());
    }
    public static testMethod void testvalidateDatesCompare(){
        Test.startTest();
        Boolean response = AirDashboardController.validateDatesCompare(String.valueOf(system.today()),String.valueOf(system.today().addDays(-1)));
        Test.stopTest();
        system.assertEquals(true,response);
    }
    public static testMethod void testgetDataContact(){
        generateData();
        Test.startTest();
        Contact response = AirDashboardController.getDataContact(contactRecord.Id);
        Test.stopTest();
        system.assertEquals(contactRecord.Id,response.Id);
    }
    public static testMethod void testsearchContactByAccount(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.searchContactByAccount('',accountRecord.Id);
        Test.stopTest();
        system.assertEquals(true, response.contains('John Wick'));
    }
    public static testMethod void testsearchProd(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.searchProd('Test',true);
        Test.stopTest();
        system.assertEquals(true, response.contains('Test'));
    }
    public static testMethod void testsearchAccount(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.searchAccount('Test','Airline Vendor');
        Test.stopTest();
        system.assertEquals(true, response.contains('Test'));
    }
    public static testMethod void testsearchAirport(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.searchAirport('LAX');
        Test.stopTest();
        system.assertEquals(true, response.contains(airport1.Id));
    }
    public static testMethod void testsearchCity(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.searchCity('New');
        Test.stopTest();
        system.assertEquals(true, response.contains('New York'));
    }
    public static testMethod void testsearchCreditCard(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.searchCreditCard('test',productionRecord.Id);
        Test.stopTest();
        system.assertEquals('[]', response);
    }
    public static testMethod void testverifyWideAddress(){
        generateData();
        Test.startTest();
        String response = AirDashboardController.verifyWideAddress('test@cloudcreations.com');
        Test.stopTest();
    }
    public static testMethod void testDataJournal(){
        generateData();
        Journal__c journal = new Journal__c(Air__c = airDetail.Id,Journal_Entry__c = 'Test',RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId());
        insert journal;
        Test.startTest();
        Journal__c response = AirDashboardController.getDataJournal(journal.Id);
        List<String> responseList = AirDashboardController.getDataJournalRelated(journal.Id,'company_contacts');
        Test.stopTest();
        system.assertEquals(journal.Id, response.Id);
        system.assertEquals(0, responseList.size());
    }
    public static testMethod void testSearchItinerary(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.verifySales();
        controller.itinerary_city = '';
        controller.searchItinerary();
        controller.itinerary_city = 'LAX - Los Angeles International Airport - Los Angeles, CA, USA';
        controller.searchItinerary();
        controller.itinerary_city = 'Los Angeles International Airport - Los Angeles, CA, USA';
        controller.searchItinerary();
        controller.itinerary_city = 'Los Angeles, CA, USA';
        controller.searchItinerary();
        Test.stopTest();
        system.assertEquals(false, controller.itineraryList.size() > 0 ? true : false);
    }
    public static testMethod void testMethodsItinerary(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.verifySales();
        controller.saveSale();
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        controller.newTrip();
        controller.newTripRecordType = 'round-trip';
        controller.changeTripType();
        controller.departure_cities = airport1.Id + ',' + airport2.Id;
        controller.arrival_cities = airport2.Id + ',' + airport1.Id;
        controller.saveTrip();
        controller.newTrip();
        controller.newTripRecordType = 'round-trip';
        controller.changeTripType();
        controller.addSegment();
        controller.segmentListActual = 1;
        controller.deleteSegment();
        controller.newTrip();
        controller.newTripRecordType = 'multi-city';
        controller.changeTripType();
        controller.departure_cities = airport1.Id + ',' + airport2.Id;
        controller.arrival_cities = airport2.Id + ',' + airport1.Id;
        controller.saveTrip();
        List<Itinerary__c> itineraryList = [SELECT Id FROM Itinerary__c LIMIT 1];
        controller.itineraryIdActual = itineraryList[0].Id;
        controller.editTrip();
        Test.stopTest();
        system.assertEquals(4, [SELECT Id FROM Itinerary__c].size());
    }    
    public static testMethod void testDeleteItinerary(){
        generateData();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.verifySales();
        controller.itineraryIdActual = airList[0].Id;
        controller.deleteTrip();
        controller.createjournal_alert = true;
        controller.saveCreateJournal();
        Test.stopTest();
        system.assertEquals(0, [SELECT Id FROM Itinerary__c].size());
    }
    public static testMethod void testcloneItinerary(){
        generateData();
        Test.startTest();    
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        controller.itineraryIdActual = [SELECT Id FROM Itinerary__c LIMIT 1].Id;
        controller.cloneItinerary();
        Test.stopTest();
        system.assertEquals(3, [SELECT Id FROM Itinerary__c].size());
    }
    public static testMethod void testMethodsTrip(){
        generateData();
        Test.startTest();   
        //Trip
        ApexUtil.BidTrigger_Is_Enabled = false;
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.trip_city = 'LAX - Los Angeles International Airport - Los Angeles, CA, USA';
        controller.searchTrip();
        controller.trip_city = 'Los Angeles International Airport - Los Angeles, CA, USA';
        controller.searchTrip();
        controller.trip_city = 'Los Angeles, CA, USA';
        controller.searchTrip();
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        Journal__c journal = new Journal__c(Air__c = controller.tripViewId, Journal_Entry__c = 'test'); insert journal;
        Journal__c journalChildren = new Journal__c(Air__c = controller.tripViewId,Parent_Journal__c = journal.Id, Journal_Entry__c = 'test children'); insert journalChildren;
        controller.viewTripJournals();
        controller.searchTripJournalsByGT();
        controller.backendcoordinatorGT = UserInfo.getUserId();
        controller.saveBackEndCoordinator();
        controller.saveBackEndCoordinator();
        controller.tripview_status = 'Sent';
        controller.saveStatusTrip();
        controller.contactPrimarySelected = contactRecord.Id;
        controller.changeClientTrip();
        controller.saveOtherInformation();
        controller.searchVendor();
        controller.selectedVendors = accountAirlineRecord.Id;
        controller.selectedTrips = airList[0].Id;
        controller.createBidRequest();
        controller.bid_id = bidRecord.Id;
        controller.bid_option = 1;
        controller.saveEditBid();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id, Options__c FROM Bid__c WHERE Id =: bidRecord.Id].Options__c);
    }    
    public static testMethod void testDocumentsTrip(){
        generateData();
        Test.startTest();  
        ApexUtil.BidTrigger_Is_Enabled = false;
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.getDocumentsByTrip();
        controller.filename = 'test.txt';
        controller.bodytrip = 'test';
        controller.documentRelationId = controller.tripViewId;
        controller.doAttachment();
        controller.filename = 'test.txt';
        controller.body = 'test';
        controller.documentRelationId = controller.tripViewId;
        controller.doAttachmentTrip();
        controller.form_to = 'test@cloudcreations.com';
        controller.form_cc = 'test@cloudcreations.com';
        controller.form_bcc = 'test@cloudcreations.com';
        controller.form_subject = 'test';
        controller.form_body = 'test';
        controller.emailAttachs = controller.newattachment_id;
        controller.opportunityId = productionRecord.Id;
        controller.sendEmailFormWithAttachs();
        controller.documentId = controller.newattachment_id;
        controller.documentTitle = 'testchange';
        controller.editDocumentTitle();
        controller.documentIdActual = controller.newattachment_id;
        controller.deleteDocument();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id, LinkedEntityId, ContentDocumentId FROM ContentDocumentLink WHERE LinkedEntityId =: airList[0].Id].size());
    }
    public static testMethod void testMethodsTripOther(){
        generateData();
        Test.startTest(); 
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.tripViewId = airDetail.Id;
        controller.viewTripDetail();
        controller.saveItinerarySegmentTrip();
        controller.newitinerary_id = [SELECT Id FROM Air__c WHERE RecordTypeId =: Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId() ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.deleteItineraryTrip();
        Test.stopTest();
        system.assertEquals(1, [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Segments'].size());
    }
    public static testMethod void testMethodsTripSecond(){
        generateData();
        Test.startTest();   
        //Trip
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        controller.reRenderTripFields();
        controller.newAircraftTrip();
        controller.addAircraftTrip();
        controller.aircraftIdActual = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Crafts' LIMIT 1].Id;
        controller.saveEditAircraftTrip();
        controller.newConcessionTrip();
        controller.concessionCreateInBid = true;
        controller.addConcessionTrip();
        controller.concessionActual = [SELECT Id FROM Concessions__c WHERE Concession_Type__c = 'Air' ORDER BY CreatedDate DESC LIMIT 1].Id;
        controller.saveEditConcessionTrip();
        controller.deleteConcession();
        Test.stopTest();
        system.assertNotEquals(null, [SELECT Id FROM Concessions__c WHERE Concession_Type__c = 'Air'].size());
    }    
    public static testMethod void testMethodsTripSendBidRequest(){
        generateData();
        Test.startTest();   
        //Trip
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.vendoraccount_actual_id = accountRecord.Id;
        controller.vendorcontact_actual_id = contactRecord.Id;
        controller.changeContactVendorBid();
        controller.vendorContact.LastName = 'testing';
        controller.vendorContact.Email = 'testing@cloudcreations.com';
        controller.saveAddContactVendor();
        controller.dataids = accountRecord.Id;
        controller.sendBidRequest();
        controller.type_email = 'pdf';
        controller.openEditPDF();
        controller.saveAndCloseBidRequest();
        controller.emailBody = 'test';
        controller.sendBidRequestEdit();
        controller.tripViewId = airList[0].Id;
        Test.stopTest();
        system.assertEquals(true, [SELECT Id FROM Journal__c WHERE Bid__c <> NULL].size() > 0 ? true :false);
    }
    public static testMethod void testMethodsTripPreviewOptions(){
        generateData();
        Test.startTest();   
        //Trip
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        controller.openPreviewOptions();
        controller.openSendOptions();
        controller.congaSendOptions();
        controller.sendOptions_primaryContactId = controller.contactWrapperByProduction[0].c.Id;
        controller.changeContactProduction();
        controller.contactWrapperByProduction[0].selected = true;
        controller.sendLink();
        Test.stopTest();
        system.assertEquals('Pending Client Choice', [SELECT Id, Status__c FROM Air__c WHERE Id =: airDetail.Id].Status__c);
    }
    public static testMethod void testMethodsTripReleaseBid(){
        generateData();
        Test.startTest();   
        //Trip
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        bidRecord.Status__c = 'Lead Sent';
        update bidRecord;
        controller.openReleaseBid();
        controller.vendoraccount_actual_id = accountRecord.Id;
        controller.vendorcontact_actual_id = contactRecord.Id;
        controller.changeContactReleaseBid();
        controller.dataids = accountRecord.Id;
        controller.sendReleaseBid();
        AirDashboardController.getDataEmailBid(productionRecord.Id,airDetail.Id,bidRecord.Id,contactRecord.Id,'release_bid','');
        controller.emailSubject = 'test';
        controller.emailBody = 'body';
        controller.saveAndCloseReleaseBid();
        Test.stopTest();
        system.assertEquals('test', [SELECT Id, Email_Subject_Release_Bid__c FROM Air__c WHERE Id =: airDetail.Id].Email_Subject_Release_Bid__c);
    }
    public static testMethod void testMethodsTripReleaseBidOther(){
        generateData();
        Test.startTest();   
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        bidRecord.Status__c = 'Lead Sent';
        update bidRecord;
        controller.openReleaseBid();
        controller.dataids = accountRecord.Id;
        controller.emailSubject = 'test';
        controller.emailBody = 'test';
        controller.sendEditReleaseBid();
        Test.stopTest();
        system.assertEquals(true, [SELECT Id, Journal_Entry__c FROM Journal__c WHERE Bid__c =: bidRecord.Id LIMIT 1].Journal_Entry__c.contains('Release Bid') ? true : false);
    }
    public static testMethod void testMethodsTripgetDataEmailBid(){
        generateData();
        Test.startTest();   
        List<String> result1 = AirDashboardController.getDataEmailBid(productionRecord.Id,airDetail.Id,bidRecord.Id,contactRecord.Id,'release_bid2','');
        List<String> result2 = AirDashboardController.getDataEmailBid(productionRecord.Id,airDetail.Id,bidRecord.Id,contactRecord.Id,'send_bid_request','');
        Test.stopTest();
        system.assertEquals(true,result1.size() > 0 ? true : false);
        system.assertEquals(true,result2.size() > 0 ? true : false);
    }
    public static testMethod void testMethodsTripDecisionDueDate(){
        generateData();
        Test.startTest();   
        //Trip
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.newTrip();
        controller.newTripRecordType = 'one-way';
        controller.saveTrip();
        List<Air__c> airList = [SELECT Id FROM Air__c WHERE RecordType.DeveloperName = 'Air_Trip_Details' LIMIT 1];
        controller.tripViewId = airList[0].Id;
        controller.viewTripDetail();
        controller.openDecisionDueDate();
        controller.decisionduedate_attention = contactRecord.Id;
        controller.changeAttention();
        controller.saveDecisionDueDate();
        controller.deactivateDecisionDueDate();
        controller.emailbid_to = 'test@cloudcreations.com';
        controller.emailbid_cc = '';
        controller.emailbid_bcc = '';
        controller.emailbid_subject = 'test subject';
        controller.decisionduedate_body = 'test body';
        controller.decisionduedate_closing = 'test';
        controller.emailAttachs = '';
        controller.sendEmailDecisionDueDate();
        Test.stopTest();
        //system.assertEquals(system.now(), [SELECT Id, Decision_Due_Date_Last_Send_Date__c FROM Air__c WHERE Id =: airList[0].Id LIMIT 1].Decision_Due_Date_Last_Send_Date__c);
    }
    /*public static testMethod void testsendEditAllEmail(){
        generateData();
        Test.startTest();
        Apexpages.StandardController sc = new Apexpages.StandardController(productionRecord);
        AirDashboardController controller = new AirDashboardController(sc);
        controller.verifySales();
        controller.tripViewId = airDetail.Id;
        controller.viewTripDetail();
        controller.openSendBidRequest();
        controller.dataids = accountRecord.Id;
        controller.type_email = '';
        controller.emailBody = '';
        controller.sendEditAllEmail();
        Test.stopTest();
        system.assertEquals('Bid Request Stage',[SELECT Id, Status__c FROM Air__c WHERE Id =: airDetail.Id LIMIT 1].Status__c);
    }*/
}
```


# Last Modified


# Usage

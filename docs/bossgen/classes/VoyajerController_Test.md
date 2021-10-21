---
layout: default
title: VoyajerController_Test
parent: classes
---
# Metadata Type
classes


# Filename 
VoyajerController_Test


# Raw XML
```
@isTest
public class VoyajerController_Test {
  @testSetup
  static void setup() {
    Test.startTest();

    Id customerProfile = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Customer'].Id;
    Id vendorProfile = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Vendor'].Id;
    List<Account> accounts = new List<Account>();
    accounts.add(
      new Account(
        Name = 'Company',
        RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Company').getRecordTypeId(),
        Status__c = 'Active',
        Market__c = 'Other',
        CurrencyIsoCode = 'USD'
      )
    );
    accounts.add(
      new Account(
        Name = 'Vendor Housing',
        RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Vendor')
          .getRecordTypeId(),
        Status__c = 'Active',
        Market__c = 'Other',
        CurrencyIsoCode = 'USD'
      )
    );
    accounts.add(
      new Account(
        Name = 'Vendor Ground',
        RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
          .get('Ground_Travel_Vendor')
          .getRecordTypeId(),
        Status__c = 'Active',
        Market__c = 'Other',
        CurrencyIsoCode = 'USD'
      )
    );
    insert accounts;
    List<Contact> contacts = new List<Contact>();
    contacts.add(
      new Contact(
        AccountId = accounts.get(0).Id,
        FirstName = 'Johnny',
        LastName = 'Test',
        Email = 'jhonny.test@rrtest.com'
      )
    );
    contacts.add(
      new Contact(
        AccountId = accounts.get(1).Id,
        FirstName = 'Vendor',
        LastName = 'Housing',
        Email = 'vendor.housing@rrtest.com'
      )
    );
    contacts.add(
      new Contact(
        AccountId = accounts.get(2).Id,
        FirstName = 'Vendor',
        LastName = 'Ground',
        Email = 'vendor.ground@rrtest.com'
      )
    );
    contacts.add(
      new Contact(
        AccountId = accounts.get(0).Id,
        FirstName = 'extra',
        LastName = 'contact',
        Email = 'extra.contact@rrtest.com'
      )
    );
    insert contacts;

    List<User> users = new List<User>();
    users.add(
      new User(
        ProfileId = customerProfile,
        ContactId = contacts.get(0).Id,
        Username = contacts.get(0).Email,
        FirstName = contacts.get(0).FirstName,
        LastName = contacts.get(0).LastName,
        Housing_Preference__c = 'RRU',
        alias = 'jtestrr',
        CommunityNickname = 'jtestrr',
        Email = contacts.get(0).Email,
        EmailEncodingKey = 'UTF-8',
        country = 'United States',
        LocaleSidKey = 'en_US',
        TimeZoneSidKey = 'America/Los_Angeles',
        LanguageLocaleKey = 'en_US'
      )
    );
    users.add(
      new User(
        ProfileId = vendorProfile,
        ContactId = contacts.get(1).Id,
        Username = contacts.get(1).Email,
        FirstName = contacts.get(1).FirstName,
        LastName = contacts.get(1).LastName,
        Housing_Preference__c = 'RRU',
        alias = 'vhtestrr',
        CommunityNickname = 'vhtestrr',
        Email = contacts.get(1).Email,
        EmailEncodingKey = 'UTF-8',
        country = 'United States',
        LocaleSidKey = 'en_US',
        TimeZoneSidKey = 'America/Los_Angeles',
        LanguageLocaleKey = 'en_US'
      )
    );
    users.add(
      new User(
        ProfileId = vendorProfile,
        ContactId = contacts.get(2).Id,
        Username = contacts.get(2).Email,
        FirstName = contacts.get(2).FirstName,
        LastName = contacts.get(2).LastName,
        Housing_Preference__c = 'RRU',
        alias = 'vgtestrr',
        CommunityNickname = 'vgtestrr',
        Email = contacts.get(2).Email,
        EmailEncodingKey = 'UTF-8',
        country = 'United States',
        LocaleSidKey = 'en_US',
        TimeZoneSidKey = 'America/Los_Angeles',
        LanguageLocaleKey = 'en_US'
      )
    );
    insert users;

    Opportunity opportunity = new Opportunity(
      Name = 'test First',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      StageName = 'Active',
      AccountId = accounts.get(0).Id,
      CurrencyIsoCode = 'USD',
      CloseDate = Date.today().addDays(30)
    );
    insert opportunity;

    List<Production_Associations__c> associations = new List<Production_Associations__c>();
    associations.add(
      new Production_Associations__c(
        RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
          .get('Production_Contacts')
          .getRecordTypeId(),
        Contact__c = contacts.get(0).Id,
        Production_Opp__c = opportunity.Id,
        Role__c = 'Other'
      )
    );
    associations.add(
      new Production_Associations__c(
        RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
          .get('Production_Coordinators')
          .getRecordTypeId(),
        User__c = UserInfo.getUserId(),
        Production_Opp__c = opportunity.Id,
        Status__c = 'Associated',
        Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator; Primary Freight Coordinator; Primary Contract Coordinator; Individual Reservations back-end Coordinator; IR Coordinator; Account Manager'
      )
    );
    insert associations;

    Housing__c housingSalesDetails = new Housing__c(
      RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Sales_Housing')
        .getRecordTypeId(),
      Production_CC__c = opportunity.Id,
      Housing_Preference__c = users.get(0).Housing_Preference__c
    );
    insert housingSalesDetails;

    Housing__c housingStay = new Housing__c(
      RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Hotel_Housing')
        .getRecordTypeId(),
      Production_CC__c = opportunity.Id,
      Production__c = opportunity.Id,
      Housing_Preference__c = users.get(0).Housing_Preference__c,
      Options_sent_to_client__c = Date.today().addDays(5),
      Trace_Date__c = Date.Today() + 10,
      Status_CC__c = 'Bid Request Stage'
    );
    insert housingStay;

    List<Housing__c> rooms = new List<Housing__c>();
    rooms.add(
      new Housing__c(
        isFromCommunity__c = true,
        RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId(),
        Date_In__c = Date.today().addDays(15),
        Date_Out__c = Date.today().addDays(16),
        Unit_Type__c = '1-Bedroom',
        Units__c = 2,
        Production_CC__c = opportunity.Id
      )
    );
    rooms.add(
      new Housing__c(
        isFromCommunity__c = true,
        RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId(),
        Date_In__c = Date.today().addDays(15),
        Date_Out__c = Date.today().addDays(16),
        Unit_Type__c = '1-Bedroom',
        Units__c = 2,
        Sales_Housing__c = housingStay.Id,
        Production_CC__c = opportunity.Id
      )
    );
    insert rooms;

    Ground__c groundSalesDetails = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('Sales_GT_Details')
        .getRecordTypeId(),
      Production_Ground__c = opportunity.Id
    );
    insert groundSalesDetails;
    Ground__c groundTrip = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Trip_Details')
        .getRecordTypeId(),
      Production_Ground__c = opportunity.Id,
      Options_sent_to_client__c = Date.today().addDays(5)
    );
    insert groundTrip;
    Ground__c groundSubTrip = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Sub_Trip_Details')
        .getRecordTypeId(),
      Production_Ground__c = opportunity.Id,
      GT_Trip_Details__c = groundTrip.Id
    );
    insert groundSubTrip;
    Ground__c groundTravel = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Travel_Details')
        .getRecordTypeId(),
      Production_Ground__c = opportunity.Id,
      GT_Sub_Trip_Details__c = groundSubTrip.Id
    );
    insert groundTravel;

    Air__c air = new Air__C(
      RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Trip_Details')
        .getRecordTypeId(),
      Production__c = opportunity.Id,
      Options_Sent_to_Client__c = Date.today().addDays(5)
    );
    insert air;
    Air__c segment = new Air__c(
      RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Segments')
        .getRecordTypeId(),
      Production__c = opportunity.Id,
      Air_Trip_Details__c = air.Id
    );
    insert segment;

    Freight__c freightTrip = new Freight__c(
      RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName()
        .get('Freight_Trip_Details')
        .getRecordTypeId(),
      Production__c = opportunity.Id
    );
    insert freightTrip;
    Freight__c freightSubTrip = new Freight__c(
      RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName()
        .get('Freight_Sub_Trip_Details')
        .getRecordTypeId(),
      Production__c = opportunity.Id,
      Freight_Trip_Details__c = freightTrip.Id,
      isFromCommunity__c = true
    );
    insert freightSubTrip;
    Freight__c freightTravel = new Freight__c(
      RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName()
        .get('Equipment_Details')
        .getRecordTypeId(),
      Production__c = opportunity.Id,
      Freight_Sub_Trip_Details__c = freightSubTrip.Id
    );
    insert freightTravel;

    List<Ground__c> vehicles = new List<Ground__c>();
    vehicles.add(
      new Ground__c(
        RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('Vehicle_Type')
          .getRecordTypeId(),
        Production_Ground__c = opportunity.Id,
        isFromCommunity__c = true
      )
    );
    vehicles.add(
      new Ground__c(
        RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('Vehicle_Type')
          .getRecordTypeId(),
        GT_Trip_Details__c = groundTrip.Id,
        Production_Ground__c = opportunity.Id
      )
    );
    vehicles.add(
      new Ground__c(
        RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('Vehicle_Type')
          .getRecordTypeId(),
        GT_Trip_Details__c = groundTrip.Id,
        Production_Ground__c = opportunity.Id,
        isFromCommunity__c = true
      )
    );
    insert vehicles;

    List<Concessions__c> concessions = new List<Concessions__c>();
    concessions.add(
      new Concessions__c(
        isFromCommunity__c = true,
        Concession_Type__c = 'Housing',
        Concessions_Requested__c = 'All single rooms must have king beds',
        Notes__c = 'Yes please',
        Production__c = opportunity.Id
      )
    );
    concessions.add(
      new Concessions__c(
        isFromCommunity__c = true,
        Concession_Type__c = 'Housing',
        Concessions_Requested__c = 'All single rooms must have king beds',
        Notes__c = 'Yes please',
        Housing__c = housingStay.Id,
        Production__c = opportunity.Id
      )
    );
    concessions.add(
      new Concessions__c(
        isFromCommunity__c = true,
        Concession_Type__c = 'GT',
        Concessions_Requested__c = 'Fuel',
        Production__c = opportunity.Id
      )
    );
    insert concessions;

    List<Itinerary__c> itineraries = new List<Itinerary__c>();
    itineraries.add(
      new Itinerary__c(
        RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
          .get('Housing_Itinerary')
          .getRecordTypeId(),
        Housing__c = housingStay.Id,
        Production__c = opportunity.Id,
        Status__c = 'Itinerary Received'
      )
    );

    itineraries.add(
      new Itinerary__c(
        RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
          .get('GT_Itinerary')
          .getRecordTypeId(),
        GT__c = groundTrip.Id,
        Production__c = opportunity.Id,
        Status__c = 'Itinerary Received'
      )
    );
    itineraries.add(
      new Itinerary__c(
        RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
          .get('Air_Itinerary')
          .getRecordTypeId(),
        Air__c = air.Id,
        Production__c = opportunity.Id,
        Status__c = 'Itinerary Received'
      )
    );
    itineraries.add(
      new Itinerary__c(
        RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
          .get('Freight_Itinerary')
          .getRecordTypeId(),
        Freight__c = freightTrip.Id,
        Production__c = opportunity.Id,
        Status__c = 'Itinerary Received'
      )
    );
    insert itineraries;
    system.debug('itineraries :: ' + itineraries);
    Test.stopTest();

    /* create some of the shared config objects */
    insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    insert new Dashboard_Session__c(
      Production_ID__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      SetupOwnerId = UserInfo.getUserId()
    );
  }

  /**
   * testSubmitMultipleOptions - used to test the multiple submissions of bid options when you are in a Tournament record
   *
   */
  @isTest
  static void testSubmitMultipleOptionsOneOption() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    //Test.startTest();

    /* get the original "Stay" record that represents a hotel stay */
    String originalStay = [
      SELECT Id, Status__c, Status_CC__c, Production__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ]
    .Id;

    /* record type action for Room Types */
    String roomTypesRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();

    /* create bids that will be mock data for what came from the community submission */
    Bid__c theBid = new Bid__c(
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Housing__c = originalStay,
      Selected_option_comments__c = 'Test Comments 123',
      Vendor_Contact__c = [SELECT Id FROM Contact LIMIT 1]
      .Id,
      Vendor__c = [SELECT Id FROM Account LIMIT 1]
      .Id
    );

    insert theBid;

    /* here we need to simulate a data structure coming from the Community that would be the VoyajerController.BidOption type */
    List<VoyajerController.BidOption> theBidOptions = new List<VoyajerController.BidOption>();
    theBidOptions = populateBidOptions(new List<Bid__c>{ theBid });

    /* serialize it and attempt to simulate the submit action from the Lightning Component */
    String theBidOptionJSON = JSON.serialize(theBidOptions);

    /* before we do the work let's make sure we have the base details */
    List<Housing__c> theHousings = [
      SELECT Status__c, Status_CC__c, Id, Name, RecordType.DeveloperName, CreatedDate
      FROM Housing__c
      ORDER BY CreatedDate DESC
    ];

    /* lets call the method Voyajer component would call directly with the JSON "from the page" */
    /* we would expect from our test data that there is one bid in this list */
    /* we also would expect that since the stay is not in a Contracting status it shouldnt duplicate the stay */
    system.assertNotEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertNotEquals(
      [SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay]
      .Status_CC__c,
      'In Contracting'
    );
    system.assertNotEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.startTest();
    Map<String, Object> submitMultipleOptions = VoyajerController.saveMultipleOptionsSelected(
      (List<Object>) theBidOptions
    );
    Test.stopTest();
    theHousings = [SELECT Id, Name, RecordType.DeveloperName, CreatedDate FROM Housing__c ORDER BY CreatedDate DESC];

    /* need to confirm: */
    /* 1 - no duplicate stays */
    /* 2 - no extra room types */
    /* 3 - existing stay went into In Contracting status */
    /* - */
    system.assertEquals(theHousings.size(), 4);
    //system.assertEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertEquals([SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay].Status_CC__c, 'Decision');
    system.assertEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );

    String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
      .get('Bid_Journal')
      .getRecordTypeId();
    List<Journal__c> journalsCreated = [SELECT Id, Journal_Entry__c FROM Journal__c WHERE RecordTypeId = :bidJournalRT];
    system.debug(journalsCreated);
    system.assertEquals(journalsCreated.size(), 1);
  }

  @isTest
  static void testSubmitMultipleOptionsTwoOptions() {
    /* get the original "Stay" record that represents a hotel stay */
    String originalStay = [
      SELECT Id, Status__c, Status_CC__c, Production__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ]
    .Id;

    /* record type action for Room Types */
    String roomTypesRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();
    String stayRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Housing')
      .getRecordTypeId();
    String bidHousingRT = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Bid')
      .getRecordTypeId();

    /* create bids that will be mock data for what came from the community submission */
    Bid__c theBid = new Bid__c(
      RecordTypeId = bidHousingRT,
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Housing__c = originalStay
    );
    Bid__c theBid2 = new Bid__c(
      RecordTypeId = bidHousingRT,
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Housing__c = originalStay
    );
    insert theBid;
    insert theBid2;

    /* here we need to simulate a data structure coming from the Community that would be the VoyajerController.BidOption type */
    List<VoyajerController.BidOption> theBidOptions = new List<VoyajerController.BidOption>();
    theBidOptions = populateBidOptions(new List<Bid__c>{ theBid, theBid2 });

    /* serialize it and attempt to simulate the submit action from the Lightning Component */
    String theBidOptionJSON = JSON.serialize(theBidOptions);

    /* before we do the work let's make sure we have the base details */
    List<Housing__c> theHousings = [
      SELECT Status__c, Status_CC__c, Id, Name, RecordType.DeveloperName, CreatedDate
      FROM Housing__c
      ORDER BY CreatedDate DESC
    ];

    /* lets call the method Voyajer component would call directly with the JSON "from the page" */
    /* we would expect from our test data that there is one bid in this list */
    /* we also would expect that since the stay is not in a Contracting status it shouldnt duplicate the stay */
    system.assertNotEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertNotEquals(
      [SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay]
      .Status_CC__c,
      'In Contracting'
    );
    system.assertNotEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );
    system.assertEquals([SELECT COUNT() FROM Bid__c WHERE Housing__c = :originalStay], 2);
    system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Hotel_Housing'], 1);
    system.assertEquals([SELECT COUNT() FROM Bid__c WHERE RecordType.DeveloperName = 'Housing_Bid'], 2);

    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    Map<String, Object> submitMultipleOptions = VoyajerController.saveMultipleOptionsSelected(
      (List<Object>) theBidOptions
    );

    /* assertions:
        /*  first bid was submitted normally and is In Contracting 
        /*  second bid triggered duplicate stay and created new stay and associated bid 
        /*  second stay goes to In Contracting 
        /*  new itinerary created
        /*  duplicate stay put on new itinerary */
    Test.StopTest();

    theHousings = [SELECT Id, Name, RecordType.DeveloperName, CreatedDate FROM Housing__c ORDER BY CreatedDate DESC];
    system.assertEquals(theHousings.size(), 6); /* new Stay and new Room Types + Ops */
    //system.assertEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertEquals([SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay].Status_CC__c, 'Decision');
    system.assertEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );
    system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Hotel_Housing'], 2);
    //system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Hotel_Housing' AND Status__c = 'In Contracting'], 2);
    //system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Room_Types_Ops'], 3);
    //system.assertEquals([SELECT COUNT() FROM Bid__c WHERE RecordType.DeveloperName = 'Housing_Bid'], 2);
    //system.assertEquals([SELECT Housing__c FROM Bid__c WHERE RecordType.DeveloperName = 'Housing_Bid' ORDER BY CreatedDate ASC LIMIT 1].Housing__c, [SELECT Id FROM Housing__c WHERE RecordTypeId =: stayRT ORDER BY CreatedDate ASC LIMIT 1].Id);
  }

  @isTest
  static void testSubmitMultipleOptionsTwoOptionsDecision() {
    /* get the original "Stay" record that represents a hotel stay */
    String originalStay = [
      SELECT Id, Status__c, Status_CC__c, Production__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ]
    .Id;

    /* record type action for Room Types */
    String roomTypesRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();
    String stayRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Housing')
      .getRecordTypeId();
    String bidHousingRT = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Bid')
      .getRecordTypeId();

    /* create bids that will be mock data for what came from the community submission */
    Bid__c theBid = new Bid__c(
      RecordTypeId = bidHousingRT,
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Housing__c = originalStay
    );
    Bid__c theBid2 = new Bid__c(
      RecordTypeId = bidHousingRT,
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Housing__c = originalStay
    );
    insert theBid;
    insert theBid2;

    /* here we need to simulate a data structure coming from the Community that would be the VoyajerController.BidOption type */
    List<VoyajerController.BidOption> theBidOptions = new List<VoyajerController.BidOption>();
    theBidOptions = populateBidOptions(new List<Bid__c>{ theBid, theBid2 });

    /* serialize it and attempt to simulate the submit action from the Lightning Component */
    String theBidOptionJSON = JSON.serialize(theBidOptions);

    /* before we do the work let's make sure we have the base details */
    List<Housing__c> theHousings = [
      SELECT Status__c, Status_CC__c, Id, Name, RecordType.DeveloperName, CreatedDate
      FROM Housing__c
      ORDER BY CreatedDate DESC
    ];

    /* lets call the method Voyajer component would call directly with the JSON "from the page" */
    /* we would expect from our test data that there is one bid in this list */
    /* we also would expect that since the stay is not in a Contracting status it shouldnt duplicate the stay */
    system.assertNotEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertNotEquals(
      [SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay]
      .Status_CC__c,
      'In Contracting'
    );
    system.assertNotEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );
    system.assertEquals([SELECT COUNT() FROM Bid__c WHERE Housing__c = :originalStay], 2);
    system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Hotel_Housing'], 1);
    system.assertEquals([SELECT COUNT() FROM Bid__c WHERE RecordType.DeveloperName = 'Housing_Bid'], 2);

    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    Map<String, Object> submitMultipleOptions = VoyajerController.saveMultipleOptionsSelected(
      (List<Object>) theBidOptions
    );

    /* assertions:
        /*  first bid was submitted normally and is In Contracting 
        /*  second bid triggered duplicate stay and created new stay and associated bid 
        /*  second stay goes to In Contracting 
        /*  new itinerary created
        /*  duplicate stay put on new itinerary */
    Test.StopTest();

    theHousings = [SELECT Id, Name, RecordType.DeveloperName, CreatedDate FROM Housing__c ORDER BY CreatedDate DESC];
    system.assertEquals(theHousings.size(), 6); /* new Stay and new Room Types + Ops */
    //system.assertEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertEquals([SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay].Status_CC__c, 'Decision');
    system.assertEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );
    system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Hotel_Housing'], 2);

    Task[] theTraces = [SELECT Id, ActivityDate, Subject, Status, Priority FROM Task WHERE What.Type = 'Housing__c'];
    system.debug(theTraces);
    //system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Hotel_Housing' AND Status__c = 'In Contracting'], 2);
    //system.assertEquals([SELECT COUNT() FROM Housing__c WHERE RecordType.DeveloperName = 'Room_Types_Ops'], 3);
    //system.assertEquals([SELECT COUNT() FROM Bid__c WHERE RecordType.DeveloperName = 'Housing_Bid'], 2);
    //system.assertEquals([SELECT Housing__c FROM Bid__c WHERE RecordType.DeveloperName = 'Housing_Bid' ORDER BY CreatedDate ASC LIMIT 1].Housing__c, [SELECT Id FROM Housing__c WHERE RecordTypeId =: stayRT ORDER BY CreatedDate ASC LIMIT 1].Id);
  }
  /**
   * testSubmitMultipleOptions - used to test the multiple submissions of bid options when you are in a Tournament record
   *
   */
  @isTest
  static void testSubmitMultipleOptionsOneOptionDecisionTask() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    //Test.startTest();

    /* get the original "Stay" record that represents a hotel stay */
    String originalStay = [
      SELECT Id, Status__c, Status_CC__c, Production__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ]
    .Id;

    /* record type action for Room Types */
    String roomTypesRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();

    /* create bids that will be mock data for what came from the community submission */
    Bid__c theBid = new Bid__c(
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Housing__c = originalStay,
      Selected_option_comments__c = 'Test Comments 123',
      Vendor_Contact__c = [SELECT Id FROM Contact LIMIT 1]
      .Id,
      Vendor__c = [SELECT Id FROM Account LIMIT 1]
      .Id
    );

    insert theBid;

    /* here we need to simulate a data structure coming from the Community that would be the VoyajerController.BidOption type */
    List<VoyajerController.BidOption> theBidOptions = new List<VoyajerController.BidOption>();
    theBidOptions = populateBidOptions(new List<Bid__c>{ theBid });

    /* serialize it and attempt to simulate the submit action from the Lightning Component */
    String theBidOptionJSON = JSON.serialize(theBidOptions);

    /* before we do the work let's make sure we have the base details */
    List<Housing__c> theHousings = [
      SELECT Status__c, Status_CC__c, Id, Name, RecordType.DeveloperName, CreatedDate
      FROM Housing__c
      ORDER BY CreatedDate DESC
    ];

    /* lets call the method Voyajer component would call directly with the JSON "from the page" */
    /* we would expect from our test data that there is one bid in this list */
    /* we also would expect that since the stay is not in a Contracting status it shouldnt duplicate the stay */
    system.assertNotEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertNotEquals(
      [SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay]
      .Status_CC__c,
      'In Contracting'
    );
    system.assertNotEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.startTest();
    Map<String, Object> submitMultipleOptions = VoyajerController.saveMultipleOptionsSelected(
      (List<Object>) theBidOptions
    );
    Test.stopTest();
    theHousings = [SELECT Id, Name, RecordType.DeveloperName, CreatedDate FROM Housing__c ORDER BY CreatedDate DESC];

    /* need to confirm: */
    /* 1 - no duplicate stays */
    /* 2 - no extra room types */
    /* 3 - existing stay went into In Contracting status */
    /* - */
    system.assertEquals(theHousings.size(), 4);
    //system.assertEquals([SELECT Status__c FROM Housing__c WHERE Id = :originalStay].Status__c, 'In Contracting');
    system.assertEquals([SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay].Status_CC__c, 'Decision');
    system.assertEquals([SELECT Status_CC__c FROM Housing__c WHERE Id = :originalStay].Status_CC__c, 'Decision');
    system.assertEquals(
      [SELECT Status__c FROM Itinerary__c WHERE Housing__c = :originalStay]
      .Status__c,
      'In Contracting'
    );

    String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
      .get('Bid_Journal')
      .getRecordTypeId();
    List<Journal__c> journalsCreated = [SELECT Id, Journal_Entry__c FROM Journal__c WHERE RecordTypeId = :bidJournalRT];
    system.debug(journalsCreated);
    system.assertEquals(journalsCreated.size(), 1);

    Task[] theTraces = [SELECT Id, ActivityDate, Subject, Status, Priority FROM Task WHERE What.Type = 'Housing__c'];
    system.debug('theTraces : : : ' + theTraces);
  }

  /**
   * populateBidOptions used to populate a BidOption type with the relevant information it needs given just the bid record.  t
   * @param  theBids theBids description
   * @return         return list of VoyajerBidOptions populated
   */
  static List<VoyajerController.BidOption> populateBidOptions(List<Bid__c> theBids) {
    List<VoyajerController.BidOption> theBidOptions = new List<VoyajerController.BidOption>();
    for (Bid__c b : theBids) {
      VoyajerController.BidOption theBO = new VoyajerController.BidOption(
        b.Id /* recordId */,
        'ClayVend' /* vendor */,
        new List<Integer>{ 1, 2, 3, 4, 5 } /* stars */,
        '' /* dx_to_venue */,
        '' /* physical */,
        '' /* website */,
        '' /* phone */,
        '' /* connection */,
        '' /* pool */,
        '' /* pets_allowed */,
        '' /* hotel_shuttle */,
        null /* concessions */,
        [
          SELECT Id
          FROM Housing__c
          WHERE RecordType.DeveloperName != 'Hotel_Housing'
          ORDER BY CreatedDate DESC
        ] /* roomTypes */,
        '' /* avgrate */,
        null /* rateDetails */,
        null /* vendorData */,
        '' /* bidName */,
        '' /* status */,
        '' /* startDate */,
        '' /* endDate */,
        '' /* city */,
        '' /* venueCity */,
        '' /* additionalInformation */,
        '' /* roomReleaseDate */,
        false /* isClouseOutAvailable */,
        ''
      ) /* totalrate */;
      theBO.record = b;
      theBidOptions.add(theBO);
    }

    return theBidOptions;
  }

  @isTest
  static void testItineraryLookup() {
    User user = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    System.runAs(user) {
      System.assertEquals(null, VoyajerCustomLookup.loadLookupValues('', '', ''));
      List<Airport__c> airports = new List<Airport__c>{
        new Airport__c(Name = 'Airport 1'),
        new Airport__c(Name = 'Airport 2')
      };
      insert airports;
      System.assertEquals(2, VoyajerCustomLookup.fetchLookupValues('Airport', 'Airport__c', '').size());
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(airports.get(0).Id, 'Airport__c', ''));
      City__c city = new City__c(Name = 'City to test', City__c = 'City', Country__c = 'United States');
      insert city;
      System.assertEquals(1, VoyajerCustomLookup.fetchLookupValues('City', 'City__c', '').size());
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(city.Id, 'City__c', ''));
      String venueAccountRT = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
        .get('Venue')
        .getRecordTypeId();
      Account venue = new Account(RecordTypeId = venueAccountRT, Name = 'Venue', City__c = city.Id);
      insert venue;
      System.assertEquals(1, VoyajerCustomLookup.fetchLookupValues('City', 'Account', 'Venue_City__c').size());
      System.assertEquals(1, VoyajerCustomLookup.fetchLookupValues('Venue', 'Account', 'Venue__c').size());
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(city.Id, 'Account', 'Venue_City__c'));
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(venue.Id, 'Account', 'Venue__c'));
    }
  }
  @isTest
  static void testGetOptionsHousing() {
    Bid__c theBid = new Bid__c();
    theBid.Production__c = [SELECT Id FROM Opportunity LIMIT 1].Id;
    theBid.Housing__c = [SELECT Id FROM Housing__c LIMIT 1].Id;
    insert theBid;
    Housing__c updateHousing = [SELECT Id, Bid__c FROM Housing__c LIMIT 1];
    updateHousing.Bid__c = theBid.Id;
    update updateHousing;
    VoyajerController.getOptionsHousing([SELECT Id FROM Housing__c LIMIT 1].Id);
    VoyajerController.getOptionsHousingPreview([SELECT Id FROM Housing__c LIMIT 1].Id);
    VoyajerController.getPropertyProfile([SELECT Id FROM Account LIMIT 1].Id);
    VoyajerController.getPropertyProfile('');
    VoyajerController.upsertCloseOutHousing(
      '{"test":"test","productionRooms":[{"blah":"blah"},{"blah":"blah"}],"lodgingRooms":[{"blah":"blah"},{"blah":"blah"}],"revenues":[{"blah":"blah"},{"blah":"blah"}],"communitySign":{"blah":"blah"},"journal":{"blah":"blah"}}'
    );
    Account myAcct = new Account(Name = 'Test Account');
    insert myAcct;
    VoyajerController.getPropertyInRoom(myAcct.Id);
    User user = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    System.runAs(user) {
      System.assertEquals(null, VoyajerCustomLookup.loadLookupValues('', '', ''));
      List<Airport__c> airports = new List<Airport__c>{
        new Airport__c(Name = 'Airport 1'),
        new Airport__c(Name = 'Airport 2')
      };
      insert airports;
      System.assertEquals(2, VoyajerCustomLookup.fetchLookupValues('Airport', 'Airport__c', '').size());
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(airports.get(0).Id, 'Airport__c', ''));
      City__c city = new City__c(Name = 'City to test', City__c = 'City', Country__c = 'United States');
      insert city;
      System.assertEquals(1, VoyajerCustomLookup.fetchLookupValues('City', 'City__c', '').size());
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(city.Id, 'City__c', ''));
      String venueAccountRT = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
        .get('Venue')
        .getRecordTypeId();
      Account venue = new Account(RecordTypeId = venueAccountRT, Name = 'Venue', City__c = city.Id);
      insert venue;
      System.assertEquals(1, VoyajerCustomLookup.fetchLookupValues('City', 'Account', 'Venue_City__c').size());
      System.assertEquals(1, VoyajerCustomLookup.fetchLookupValues('Venue', 'Account', 'Venue__c').size());
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(city.Id, 'Account', 'Venue_City__c'));
      System.assertNotEquals(null, VoyajerCustomLookup.loadLookupValues(venue.Id, 'Account', 'Venue__c'));
    }
  }

  @isTest
  static void testCustomerActions() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    System.runAs(user) {
      User customerUser = VoyajerController.getClient().userInfo;
      System.assertEquals(user.Id, customerUser.Id);
      Map<String, Object> newProduction = new Map<String, Object>{
        'Name' => 'test Live',
        'ContactId' => user.ContactId,
        'AccountId' => user.Contact.AccountId,
        'CloseDate' => String.valueOf(Date.today().addDays(30))
      };
      System.assertEquals(
        (String) newProduction.get('Name'),
        VoyajerController.createProduction(JSON.serialize(newProduction))
      );
      List<VoyajerController.Production> customerProductions = VoyajerController.getProductions(
          user.ContactId,
          user.Housing_Preference__c
        )
        .clone();
      System.assertEquals(2, customerProductions.size());
      System.debug(customerProductions.get(0).recordId);
      Housing__c theHousing = new Housing__c();
      theHousing.Production_CC__c = [SELECT Id FROM Opportunity LIMIT 1].Id;
      insert theHousing;
      Bid__c theBid = new Bid__c();
      theBid.Production__c = [SELECT Id FROM Opportunity LIMIT 1].Id;
      theBid.Housing__c = theHousing.Id;
      insert theBid;
      String theHousingId = theHousing.Id;
      Ground__c theGround = new Ground__c();
      theGround.Production_Ground__c = theBid.Production__c;
      insert theGround;
      String theGroundId = theGround.Id;
      Freight__c theFreight = new Freight__c();
      theFreight.Production__c = [SELECT Id FROM Opportunity LIMIT 1].Id;
      insert theFreight;
      String theFreightId = theFreight.Id;
      Air__c theAir = new Air__c();
      theAir.Production__c = [SELECT Id FROM Opportunity LIMIT 1].Id;
      insert theAir;
      String theAirId = theAir.Id;
        VoyajerController.getPropertyInRoom('');
        String myReplace = VoyajerController.replaceIgnoreCase('asdfasd', 'asdf', 'asdf');
        Id accId = [Select id from account limit 1].Id;
        VoyajerController.getFleetRental(accId);
        VoyajerController.getFleetChauffeured(accId);
        VoyajerController.upsertCloseOutHousing(
          '{"test":"test","productionRooms":[{"blah":"blah"},{"blah":"blah"}],"lodgingRooms":[{"blah":"blah"},{"blah":"blah"}],"revenues":[{"blah":"blah"},{"blah":"blah"}],"communitySign":{"blah":"blah"},"journal":{"blah":"blah"}}'
        );
        try {
            VoyajerController.submitBidSelected(
              '{"serviceId":"' +
              theHousing.Id +
              '","bidId":"' +
              theBid.Id +
              '","serviceType":"housing","productionRooms":[{"blah":"blah"},{"blah":"blah"}],"lodgingRooms":[{"blah":"blah"},{"blah":"blah"}],"revenues":[{"blah":"blah"},{"blah":"blah"}],"communitySign":{"blah":"blah"},"journal":{"blah":"blah"}}'
            );
        } catch(Exception e) {
            
        }
        try{
            VoyajerController.submitBidSelected(
              '{"serviceId":"' +
              theGround.Id +
              '", "bidId":"' +
              theBid.Id +
              '","serviceType":"ground","productionRooms":[{"blah":"blah"},{"blah":"blah"}],"lodgingRooms":[{"blah":"blah"},{"blah":"blah"}],"revenues":[{"blah":"blah"},{"blah":"blah"}],"communitySign":{"blah":"blah"},"journal":{"blah":"blah"}}'
            );
        } catch(Exception e) {
            
        }
        try{
            VoyajerController.submitBidSelected(
              '{"serviceId":"' +
              theFreight.Id +
              '","bidId":"' +
              theBid.Id +
              '","serviceType":"air","productionRooms":[{"blah":"blah"},{"blah":"blah"}],"lodgingRooms":[{"blah":"blah"},{"blah":"blah"}],"revenues":[{"blah":"blah"},{"blah":"blah"}],"communitySign":{"blah":"blah"},"journal":{"blah":"blah"}}'
            );
        } catch(Exception e) {
            
        }
        try{
            VoyajerController.submitBidSelected(
              '{"serviceId":"' +
              theAir.Id +
              '","bidId":"' +
              theBid.Id +
              '","serviceType":"freight","productionRooms":[{"blah":"blah"},{"blah":"blah"}],"lodgingRooms":[{"blah":"blah"},{"blah":"blah"}],"revenues":[{"blah":"blah"},{"blah":"blah"}],"communitySign":{"blah":"blah"},"journal":{"blah":"blah"}}'
            );
        } catch(Exception e) {
            
        }
        VoyajerController.VerifyOptionAccess('optionsHousing', '123', '123');
        VoyajerController.VerifyOptionAccess('optionsGT', '123', '123');
        VoyajerController.Room theRoom = new VoyajerController.Room('1', '3', 2.00, 2.00, 2.00, 2.00, '2');
        VoyajerController.RoomRevenue theRoomRevenue = new VoyajerController.RoomRevenue();
        VoyajerController.Revenue theRevenue = new VoyajerController.Revenue('1', '1', '1', 1.00, '1', 1.00, 1.00);
        VoyajerController.BidData theBidData = new VoyajerController.BidData();
        VoyajerController.MonthlyPickup monthlyPickUp = new VoyajerController.MonthlyPickup(
          '1',
          '1',
          '1',
          1.00,
          1.00,
          1.00,
          '1'
        );
        VoyajerController.Itinerary theItinerary = new VoyajerController.Itinerary('1', '1', '1', '1', '1', '1', '1');
    }
  }

  @isTest
  static void testVendorProfile() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];
    Contact extra = new Contact(
      AccountId = user.Contact.AccountId,
      FirstName = 'My extra',
      LastName = 'contact test',
      Email = 'myextra.contacttest@rrtest.com'
    );
    insert extra;
    System.runAs(user) {
      System.assertEquals(true, VoyajerController.getVendorProfile(user.Contact.AccountId).containsKey('accountId'));
      Map<String, Object> updateVendorHousingProfile = new Map<String, Object>{
        'userProfile' => 'HousingVendor',
        'accountId' => user.Contact.AccountId,
        'ShippingStreet' => '',
        'City__c' => '',
        'ShippingState' => '',
        'ShippingPostalCode' => '',
        'ShippingCountry' => '',
        'Phone' => '',
        'Fax' => '',
        'Website' => '',
        'Vendor_Type__c' => '',
        'Management_Company_lookup__c' => '',
        'Metro_Area__c' => ''
      };
      Map<String, Object> updateVendorGroundProfile = new Map<String, Object>{
        'userProfile' => 'GroundVendor',
        'accountId' => user.Contact.AccountId,
        'ShippingStreet' => '',
        'City__c' => '',
        'ShippingState' => '',
        'ShippingPostalCode' => '',
        'ShippingCountry' => '',
        'Phone' => '',
        'Fax' => '',
        'Website' => '',
        'X24_hr_Emergency_Phone__c' => '',
        'GT_Vendor_Type__c' => '',
        'Service_Areas_Cities_and_notes__c' => '',
        'DOT__c' => '',
        'IFTA__c' => '',
        'Insurance__c' => '',
        'Associations__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updateVendorProfile(JSON.serialize(updateVendorHousingProfile)).containsKey('accountId')
      );
      Map<String, Object> extraVendorContact = new Map<String, Object>{
        'contactId' => extra.Id,
        'accountId' => extra.AccountId,
        'firstName' => 'My new extra',
        'lastName' => extra.LastName,
        'title' => '',
        'phone' => '',
        'ext' => '',
        'mobile' => '',
        'email' => ''
      };
      System.assertEquals(2, VoyajerController.upsertVendorContact(JSON.serialize(extraVendorContact)).size());
      System.assertEquals(
        true,
        VoyajerController.deleteVendorContact(extra.AccountId, extra.Id).containsKey('records')
      );
    }
  }

  @isTest
  static void testVendorHousingProfile() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];
    System.runAs(user) {
      Map<String, Object> propertyProfile = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'Check_In_Time__c' => '',
        'Check_out_time__c' => '',
        'X100_Non_Smoking__c' => '',
        'Lift_Elevator__c' => '',
        'Property_Entry__c' => '',
        'Porterage__c' => '',
        'Porterage_Charge__c' => '',
        'Porterage_add_l_Info__c' => '',
        'Number_of_rooms__c' => '',
        'Number_of_suites__c' => '',
        'Single_Rooms__c' => '',
        'Single_Room_Bed_Size__c' => '',
        'Single_Room_Area__c' => '',
        'Double_Rooms__c' => '',
        'Double_Room_Bed_Size__c' => '',
        'Double_Room_Area__c' => '',
        'Extended_Stay__c' => '',
        'Studios__c' => '',
        'Studios_Bed_Size__c' => '',
        'Studio_Area__c' => '',
        'X1_bedrooms__c' => '',
        'X1_bedroom_bed_size__c' => '',
        'X1_bedrooms_Area__c' => '',
        'X1_bedrooms_w_Den__c' => '',
        'X1_bedroom_w_Den_bed_size__c' => '',
        'X1_bedrooms_w_Den_Area__c' => '',
        'X2_bedroom_1_bath__c' => '',
        'X2_bedroom_1_bath_bed_size__c' => '',
        'X2_bedroom_1_bath_Area__c' => '',
        'X2_bedroom_2_bath__c' => '',
        'X2_bedroom_2_bath_bed_size__c' => '',
        'X2_bedroom_2_bath_Area__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updatePropertyProfile(JSON.serialize(propertyProfile)).containsKey('accountId')
      );
      Map<String, Object> propertyInRoom = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'Windows_Open__c' => '',
        'Air_conditioning__c' => '',
        'High_Speed_Internet__c' => '',
        'Connection__c' => '',
        'Internet_Charge__c' => '',
        'Internet_Charge_Type__c' => '',
        'Pets_Allowed__c' => '',
        'Pets_max_LBS__c' => '',
        'Pets_charge__c' => '',
        'Pets_charge_type__c' => '',
        'Refrigerator__c' => '',
        'Refrigerator_Size__c' => '',
        'Refrigerator_charge__c' => '',
        'Refrigerator_charge_type__c' => '',
        'Refrigerator_Location__c' => '',
        'Avail_refrigerators__c' => '',
        'Microwave__c' => '',
        'Microwave_charge__c' => '',
        'Microwave_charge_type__c' => '',
        'Microwave_Location__c' => '',
        'Avail_Microwave__c' => '',
        'Oven__c' => '',
        'Oven_Location__c' => '',
        'Burners__c' => '',
        'Burners_location__c' => '',
        'Coffee_Maker__c' => '',
        'Bathtub__c' => '',
        'Washer_Dryer__c' => '',
        'Washer_Dryer_Type__c' => '',
        'Hairdryers__c' => '',
        'Safe__c' => '',
        'Safe_Comments__c' => '',
        'Other_Resources_Amenities__c' => ''
      };
      VoyajerController.getPropertyInRoom(JSON.serialize(propertyInRoom));
      VoyajerController.getPropertyOnSite(JSON.serialize(propertyInRoom));
      System.assertEquals(
        true,
        VoyajerController.updatePropertyInRoom(JSON.serialize(propertyInRoom)).containsKey('accountId')
      );
      Map<String, Object> propertyOnSite = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'Pool__c' => '',
        'Pool_Seasonal__c' => '',
        'Hot_Tub__c' => '',
        'Hot_tub_seasonal__c' => '',
        'Fitness_room__c' => '',
        'Hotel_Shuttle__c' => '',
        'Airport_Shuttle__c' => '',
        'Hotel_Bars__c' => '',
        'hotel_bars_2__c' => '',
        'Hotel_bar_hours__c' => '',
        'Restaurants__c' => '',
        'Restaurants_2__c' => '',
        'Restaurants_hours__c' => '',
        'Breakfast__c' => '',
        'Breakfast_type__c' => '',
        'Room_Service__c' => '',
        'Room_Service_hours__c' => '',
        'Managers_Reception__c' => '',
        'Managers_Reception_Hours__c' => '',
        'Self_Parking__c' => '',
        'Self_Parking_Charge__c' => '',
        'Self_Parking_Charge_Type__c' => '',
        'Self_Parking_Add_l_info__c' => '',
        'Valet_Parking__c' => '',
        'Valet_Parking_Charge__c' => '',
        'Valet_Parking_Charge_Type__c' => '',
        'Valet_Parking_Add_l_info__c' => '',
        'Coach_Bus_Parking__c' => '',
        'Coach_Bus_Charge__c' => '',
        'Coach_Bus_Charge_Type__c' => '',
        'Coach_Bus_Add_l_info__c' => '',
        'Coach_Bus_parking_spots__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updatePropertyOnSite(JSON.serialize(propertyOnSite)).containsKey('accountId')
      );
    }
  }

  @isTest
  static void testVendorGroundProfile() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];
    Fleet__c fleet = new Fleet__c(Vendor__c = user.Contact.AccountId);
    insert fleet;
    System.runAs(user) {
      Map<String, Object> vendorVehicle = new Map<String, Object>{
        'vehicleId' => fleet.Id,
        'accountId' => user.Contact.AccountId,
        'vehicleType' => '',
        'quantity' => '',
        'capacity' => '',
        'make' => '',
        'otherMake' => '',
        'model' => '',
        'year' => ''
      };
      System.assertEquals(1, VoyajerController.upsertVendorVehicle(JSON.serialize(vendorVehicle)).size());
      System.assertEquals(
        true,
        VoyajerController.deleteVendorVehicle(user.Contact.AccountId, fleet.Id).containsKey('isDeleted')
      );
      Map<String, Object> fleetCoach = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'WiFi_coach__c' => '',
        'WiFi_Qty__c' => '',
        'DVD__c' => '',
        'DVD_Qty__c' => '',
        'Satellite_TV__c' => '',
        'Satellite_TV_Qty__c' => '',
        'Table__c' => '',
        'Table_Qty__c' => '',
        'Trailer_Hitch__c' => '',
        'Trailer_Hitch_Qty__c' => '',
        'Trailer__c' => '',
        'Trailer_Qty__c' => '',
        'Restroom__c' => '',
        'Restroom_Qty__c' => '',
        'Outlets_in_Rows__c' => '',
        'Outlets_in_Rows_Qty__c' => '',
        'Outlets_position__c' => '',
        'Executive_Coach__c' => '',
        'Executive_Coach_Qty__c' => '',
        'Kitchenettes__c' => false,
        'Sleepers__c' => '',
        'Sleepers_Qty__c' => '',
        'Sleepers_Amenities__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updateFleetCoach(JSON.serialize(fleetCoach)).containsKey('accountId')
      );
      System.assertEquals(true, VoyajerController.getFleetCoach(user.Contact.AccountId).containsKey('vehicles'));
      Map<String, Object> fleetChauffeured = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'Sedan__c' => '',
        'Sedan_Notes__c' => '',
        'Executive_Sedan__c' => '',
        'Executive_Sedan_Notes__c' => '',
        'Luxury_Sedan__c' => '',
        'Luxury_Sedan_Notes__c' => '',
        'X12_PAX_Van__c' => '',
        'X12_PAX_Van_Notes__c' => '',
        'X15_PAX_Van__c' => '',
        'X15_PAX_Van_Notes__c' => '',
        'Luggage_Van__c' => '',
        'Luggage_Van_Notes__c' => '',
        'SUV__c' => '',
        'SUV_Notes__c' => '',
        'Limo__c' => '',
        'Limo_notes__c' => '',
        'Mini_Coach__c' => '',
        'Mini_Coach_notes__c' => '',
        'Leather_Seats__c' => '',
        'WiFi_CV__c' => '',
        'Meet_Greet_Service__c' => '',
        'DVD_CV__c' => '',
        'Mini_Bar_CV__c' => '',
        'Airport_Services__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updateFleetChauffeured(JSON.serialize(fleetChauffeured)).containsKey('accountId')
      );
      Map<String, Object> fleetRental = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'Compact__c' => '',
        'Compact_notes__c' => '',
        'Intermediate__c' => '',
        'Intermediate_notes__c' => '',
        'Standard__c' => '',
        'Standard_notes__c' => '',
        'Full_Size__c' => '',
        'Full_Size_notes__c' => '',
        'Luxury__c' => '',
        'Luxury_notes__c' => '',
        'Standard_SUV__c' => '',
        'Standard_SUV_notes__c' => '',
        'Luxury_SUV__c' => '',
        'Luxury_SUV_notes__c' => '',
        'Mini_Van__c' => '',
        'Mini_Van_notes__c' => '',
        'X12_PAX_Van_Rental__c' => '',
        'X12_PAX_Van_Notes_Rental__c' => '',
        'X15_PAX_Van_Rental__c' => '',
        'X15_PAX_Van_Notes_Rental__c' => '',
        'Hybrid_Car__c' => '',
        'Hybrid_Car_notes__c' => '',
        'Hybrid_SUV__c' => '',
        'Hybrid_SUV_notes__c' => '',
        'Delivery__c' => '',
        'Pick_up__c' => '',
        'Direct_Bill__c' => '',
        'Master_Bill_Account_w_Credit_Card__c' => '',
        'Age_Requirement_yrs__c' => '',
        'Rental_Insurance_Options__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updateFleetRental(JSON.serialize(fleetRental)).containsKey('accountId')
      );
      Map<String, Object> vendorPayment = new Map<String, Object>{
        'accountId' => user.Contact.AccountId,
        'Visa_Accepted__c' => '',
        'Visa_Surcharge__c' => '',
        'Master_Card_Accepted__c' => '',
        'Master_Card_Surcharge__c' => '',
        'American_Express_Accepted__c' => '',
        'American_Express_Surcharge__c' => '',
        'Discover_Accepted__c' => '',
        'Discover_Surcharge__c' => '',
        'Surcharge_Negotiable__c' => '',
        'Check_Payment__c' => '',
        'Wire_Transfer_Bank_Draft__c' => '',
        'Bank_Name__c' => '',
        'IBAN__c' => '',
        'Swift__c' => '',
        'Other_Payment__c' => '',
        'Other_payment_notes__c' => '',
        'Payment_policy__c' => '',
        'Cancellation_Policy__c' => ''
      };
      System.assertEquals(
        true,
        VoyajerController.updateVendorPayment(JSON.serialize(vendorPayment)).containsKey('accountId')
      );
    }
  }

  @isTest
  static void testProductionConfiguration() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = [
      SELECT Id, RecordType.DeveloperName, Name, Account.Name, StageName, Service_Sought__c
      FROM Opportunity
      LIMIT 1
    ];
    System.runAs(user) {
      Map<String, Object> productionServices = new Map<String, Object>{
        'productionId' => customerProduction.Id,
        'services' => 'Housing;Ground Travel;Air;Freight'
      };
      System.assertEquals(
        'Housing;Ground Travel;Air;Freight',
        VoyajerController.saveProductionServices(JSON.serialize(productionServices))
      );
      System.assertEquals(true, VoyajerController.getProductionServices(customerProduction.Id).containsKey('services'));
      System.assertEquals(
        true,
        VoyajerController.getProductionItineraries(customerProduction.Id).containsKey('productionName')
      );
    }
  }

  @isTest
  static void testItineraryPages1() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = [
      SELECT Id, RecordType.DeveloperName, Name, Account.Name, StageName, Service_Sought__c
      FROM Opportunity
      LIMIT 1
    ];
    System.runAs(user) {
      System.assertEquals(
        true,
        VoyajerController.getLodgingPage(customerProduction.Id, user.Housing_Preference__c)
          .containsKey('lodgingRecords')
      );
      System.assertEquals(
        true,
        VoyajerController.getGroundPage(customerProduction.Id, user.Housing_Preference__c).containsKey('groundRecords')
      );
    }
  }

  @isTest
  static void testGetMultipleOptions() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = [
      SELECT Id, RecordType.DeveloperName, Name, Account.Name, StageName, Service_Sought__c
      FROM Opportunity
      LIMIT 1
    ];
    System.runAs(user) {
      System.assertEquals(
        true,
        VoyajerController.getMultipleOptions(customerProduction.Id, user.Housing_Preference__c)
          .containsKey('lodgingRecords')
      );
      System.assertEquals(
        true,
        VoyajerController.getGroundPage(customerProduction.Id, user.Housing_Preference__c).containsKey('groundRecords')
      );
    }
  }

  @isTest
  static void testItineraryPages2() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = [
      SELECT Id, RecordType.DeveloperName, Name, Account.Name, StageName, Service_Sought__c
      FROM Opportunity
      LIMIT 1
    ];
    System.runAs(user) {
      System.assertEquals(
        true,
        VoyajerController.getAirPage(customerProduction.Id, user.Housing_Preference__c).containsKey('flightRecords')
      );
      System.assertEquals(
        true,
        VoyajerController.getFreightPage(customerProduction.Id, user.Housing_Preference__c)
          .containsKey('freightRecords')
      );
    }
  }

  @isTest
  static void testDeleteItineraries() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = [
      SELECT Id, RecordType.DeveloperName, Name, Account.Name, StageName, Service_Sought__c
      FROM Opportunity
      LIMIT 1
    ];
    List<Itinerary__c> itineraries = [
      SELECT Id, RecordType.DeveloperName, Production__c
      FROM Itinerary__c
      WHERE Production__c = :customerProduction.Id
    ];
    System.runAs(user) {
      Map<String, Object> deleteHousing = new Map<String, Object>();
      Map<String, Object> deleteGround = new Map<String, Object>();
      Map<String, Object> deleteAir = new Map<String, Object>();
      Map<String, Object> deleteFreight = new Map<String, Object>();
      for (Itinerary__c itinerary : itineraries) {
        if (itinerary.RecordType.DeveloperName.equals('Housing_Itinerary'))
          deleteHousing = new Map<String, Object>{
            'recordType' => 'housing',
            'recordId' => itinerary.Id,
            'productionId' => itinerary.Production__c
          };
        if (itinerary.RecordType.DeveloperName.equals('GT_Itinerary'))
          deleteGround = new Map<String, Object>{
            'recordType' => 'ground',
            'recordId' => itinerary.Id,
            'productionId' => itinerary.Production__c
          };
        if (itinerary.RecordType.DeveloperName.equals('Air_Itinerary'))
          deleteAir = new Map<String, Object>{
            'recordType' => 'air',
            'recordId' => itinerary.Id,
            'productionId' => itinerary.Production__c
          };
        if (itinerary.RecordType.DeveloperName.equals('Freight_Itinerary'))
          deleteFreight = new Map<String, Object>{
            'recordType' => 'freight',
            'recordId' => itinerary.Id,
            'productionId' => itinerary.Production__c
          };
      }
      if (deleteHousing.containsKey('recordId'))
        System.assertEquals(
          true,
          VoyajerController.deleteItineraryRecord(JSON.serialize(deleteHousing)).containsKey('action')
        );
      if (deleteGround.containsKey('recordId'))
        System.assertEquals(
          true,
          VoyajerController.deleteItineraryRecord(JSON.serialize(deleteGround)).containsKey('action')
        );
      if (deleteAir.containsKey('recordId'))
        System.assertEquals(
          true,
          VoyajerController.deleteItineraryRecord(JSON.serialize(deleteAir)).containsKey('action')
        );
      if (deleteFreight.containsKey('recordId'))
        System.assertEquals(
          true,
          VoyajerController.deleteItineraryRecord(JSON.serialize(deleteFreight)).containsKey('action')
        );
    }
  }

  @isTest
  static void testSubmitResendContract() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Housing__c stay = [
      SELECT Id
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
      LIMIT 1
    ];
    Opportunity customerProduction = new Opportunity(
      Name = 'test customer production',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      StageName = 'Active',
      AccountId = user.Contact.AccountId,
      CurrencyIsoCode = 'USD',
      CloseDate = Date.today().addDays(30)
    );
    insert customerProduction;
    Production_Associations__c prodAssociation = new Production_Associations__c(
      RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
        .get('Production_Coordinators')
        .getRecordTypeId(),
      User__c = UserInfo.getUserId(),
      Production_Opp__c = customerProduction.Id,
      Status__c = 'Associated',
      Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator; Primary Freight Coordinator; Primary Contract Coordinator; Individual Reservations back-end Coordinator; IR Coordinator; Account Manager'
    );
    insert prodAssociation;
    System.runAs(user) {
      Map<String, Object> productionServices = new Map<String, Object>{
        'productionId' => customerProduction.Id,
        'services' => 'Housing;Ground Travel;Air;Freight'
      };
      /*System.assertEquals(
        true,
        VoyajerController.submitTraceResendContract(
          customerProduction.Id,
          stay.Id
        )
      );*/
    }
  }

  @isTest
  static void testSubmitResendContractNegative() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Housing__c stay = [
      SELECT Id
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
      LIMIT 1
    ];
    Opportunity customerProduction = new Opportunity(
      Name = 'test customer production',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      StageName = 'Active',
      AccountId = user.Contact.AccountId,
      CurrencyIsoCode = 'USD',
      CloseDate = Date.today().addDays(30)
    );
    insert customerProduction;
    Production_Associations__c prodAssociation = new Production_Associations__c(
      RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
        .get('Production_Coordinators')
        .getRecordTypeId(),
      User__c = UserInfo.getUserId(),
      Production_Opp__c = customerProduction.Id,
      Status__c = 'Associated',
      Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator; Primary Freight Coordinator; Primary Contract Coordinator; Individual Reservations back-end Coordinator; IR Coordinator; Account Manager'
    );
    insert prodAssociation;
    System.runAs(user) {
      Map<String, Object> productionServices = new Map<String, Object>{
        'productionId' => customerProduction.Id,
        'services' => 'Housing;Ground Travel;Air;Freight'
      };
      System.assertEquals(false, VoyajerController.submitTraceResendContract(null, null));
    }
  }

  @isTest
  static void testItinerarySubmitHousing() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = new Opportunity(
      Name = 'test customer production',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      StageName = 'Active',
      AccountId = user.Contact.AccountId,
      CurrencyIsoCode = 'USD',
      CloseDate = Date.today().addDays(30)
    );
    insert customerProduction;
    System.runAs(user) {
      Map<String, Object> productionServices = new Map<String, Object>{
        'productionId' => customerProduction.Id,
        'services' => 'Housing;Ground Travel;Air;Freight'
      };
      System.assertEquals(
        'Housing;Ground Travel;Air;Freight',
        VoyajerController.saveProductionServices(JSON.serialize(productionServices))
      );
      City__c city = new City__c(Name = 'City to test', City__c = 'City', Country__c = 'United States');
      insert city;
      Map<String, Object> saveLodgingItinerary = new Map<String, Object>{
        'officePreference' => user.Housing_Preference__c,
        'productionId' => customerProduction.Id,
        'recordType' => 'housing',
        'record' => new Map<String, Object>{
          'itineraryId' => '',
          'startDate' => Date.today().addDays(15),
          'endDate' => Date.today().addDays(16),
          'cityId' => city.Id,
          'lodgingId' => '',
          'budgetTarget' => Decimal.valueOf('50'),
          'hotelStars' => '3',
          'hotelType' => 'Limited',
          'distanceFromEvent' => 'Walking (0.5 miles)',
          'preferredBrands' => 'Marriot',
          'additionalNotes' => 'My other notes',
          'roomTypeRecords' => new List<Map<String, Object>>{
            new Map<String, Object>{ 'Unit_Type__c' => '1-Bedroom', 'Units__c' => 2 }
          },
          'concessionRecords' => new List<Map<String, Object>>{
            new Map<String, Object>{
              'Concessions_Requested__c' => 'All single rooms must have king beds.',
              'Notes__c' => 'Yes please'
            }
          }
        }
      };
      System.assertEquals(
        true,
        VoyajerController.upsertItineraryRecord(JSON.serialize(saveLodgingItinerary)).containsKey('record')
      );
      System.assertEquals(true, VoyajerController.subimtProductionItineraries(customerProduction.Id));
    }
  }

  @isTest
  static void testItinerarySubmitGround() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = new Opportunity(
      Name = 'test customer production',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      StageName = 'Active',
      AccountId = user.Contact.AccountId,
      CurrencyIsoCode = 'USD',
      CloseDate = Date.today().addDays(30)
    );
    insert customerProduction;
    System.runAs(user) {
      Map<String, Object> productionServices = new Map<String, Object>{
        'productionId' => customerProduction.Id,
        'services' => 'Housing;Ground Travel;Air;Freight'
      };
      System.assertEquals(
        'Housing;Ground Travel;Air;Freight',
        VoyajerController.saveProductionServices(JSON.serialize(productionServices))
      );
      Map<String, Object> saveGroundItinerary = new Map<String, Object>{
        'officePreference' => user.Housing_Preference__c,
        'productionId' => customerProduction.Id,
        'recordType' => 'ground',
        'record' => new Map<String, Object>{
          'itineraryId' => '',
          'tripDetailsId' => '',
          'groupType' => 'Crew',
          'qtyOfBuses' => Decimal.valueOf('1'),
          'startDate' => Date.today().addDays(15),
          'endDate' => Date.today().addDays(15),
          'additionalNotes' => 'My other notes',
          'busType' => 'Standard',
          'passengers' => '1',
          'gearLuggage' => 'no',
          'amenities' => 'WiFi',
          'notes' => 'snacks',
          'legs' => new List<Map<String, Object>>{
            new Map<String, Object>{
              'subTripDetailsId' => '',
              'subTripType' => 'City to City',
              'legId' => '',
              'datePickUp' => Date.today().addDays(15),
              'timePickUp' => '09:00:00.000',
              'dateDropOff' => Date.today().addDays(30),
              'timeDropOff' => '10:00:00.000',
              'locationPickUp' => 'Hotel',
              'locationDetailsPickUp' => 'Hotel 1',
              'locationDropOff' => 'Airport',
              'locationDetailsDropOff' => 'Airport 1'
            }
          }
        }
      };
      System.assertEquals(
        true,
        VoyajerController.upsertItineraryRecord(JSON.serialize(saveGroundItinerary)).containsKey('record')
      );
      System.assertEquals(true, VoyajerController.subimtProductionItineraries(customerProduction.Id));
    }
  }

  @isTest
  static void testItinerarySubmit2() {
    User user = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'jtestrr'
      LIMIT 1
    ];
    Opportunity customerProduction = [
      SELECT Id, RecordType.DeveloperName, Name, Account.Name, StageName, Service_Sought__c
      FROM Opportunity
      LIMIT 1
    ];
    System.runAs(user) {
      Map<String, Object> productionServices = new Map<String, Object>{
        'productionId' => customerProduction.Id,
        'services' => 'Housing;Ground Travel;Air;Freight'
      };
      System.assertEquals(
        'Housing;Ground Travel;Air;Freight',
        VoyajerController.saveProductionServices(JSON.serialize(productionServices))
      );
      List<Airport__c> airports = new List<Airport__c>{
        new Airport__c(Name = 'Airport 1'),
        new Airport__c(Name = 'Airport 2')
      };
      insert airports;
      City__c city = new City__c(Name = 'City to test', City__c = 'City', Country__c = 'United States');
      insert city;
      String venueAccountRT = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
        .get('Venue')
        .getRecordTypeId();
      Account venue = new Account(RecordTypeId = venueAccountRT, Name = 'Venue', City__c = city.Id);
      insert venue;
      Map<String, Object> saveAirItinerary = new Map<String, Object>{
        'officePreference' => user.Housing_Preference__c,
        'productionId' => customerProduction.Id,
        'recordType' => 'air',
        'record' => new Map<String, Object>{
          'itineraryId' => '',
          'airDetailsId' => '',
          'tripType' => 'Round Trip',
          'classService' => 'Economy',
          'pax' => Decimal.valueOf('1'),
          'preferredAirline' => 'United Airlines', //Updated on 02/09/2021
          'startDate' => Date.today().addDays(15),
          'endDate' => Date.today().addDays(15),
          'additionalNotes' => 'My other notes',
          'segments' => new List<Map<String, Object>>{
            new Map<String, Object>{
              'segmentId' => '',
              'departureDate' => Date.today().addDays(14),
              'timePickUp' => '04:00:00.000',
              'timeDropOff' => '07:00:00.000',
              'departureCityId' => airports.get(0).Id,
              'arrivalCityId' => airports.get(1).Id
            }
          }
        }
      };
      Map<String, Object> saveFreightItinerary = new Map<String, Object>{
        'officePreference' => user.Housing_Preference__c,
        'productionId' => customerProduction.Id,
        'recordType' => 'freight',
        'record' => new Map<String, Object>{
          'itineraryId' => '',
          'tripDetailsId' => '',
          'groupType' => 'Trucking',
          'notes' => 'stuff',
          'startDate' => Date.today().addDays(15),
          'endDate' => Date.today().addDays(15),
          'additionalNotes' => 'My other notes',
          'manifestId' => 'manifest',
          'legs' => new List<Map<String, Object>>{
            new Map<String, Object>{
              'subTripDetailsId' => '',
              'legId' => '',
              'datePickUp' => Date.today().addDays(15),
              'timePickUp' => '09:00:00.000',
              'dateDropOff' => Date.today().addDays(30),
              'timeDropOff' => '10:00:00.000',
              'locationDetailsPickUp' => 'Location 1',
              'locationDetailsDropOff' => 'Location 2'
            }
          }
        }
      };
      System.assertEquals(
        true,
        VoyajerController.upsertItineraryRecord(JSON.serialize(saveAirItinerary)).containsKey('record')
      );
      /*System.assertEquals(
        true,
        VoyajerController.upsertItineraryRecord(
            JSON.serialize(saveFreightItinerary)
          )
          .containsKey('record')
      );
      */
      System.assertEquals(true, VoyajerController.subimtProductionItineraries(customerProduction.Id));
    }
  }

  @isTest
  static void testHousingBidOptions() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Housing__c stay = [
      SELECT Id
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
      LIMIT 1
    ];
    Housing__c room = [
      SELECT
        Id,
        RecordTypeId,
        Units__c,
        Unit_Type__c,
        Special_Notes__c,
        Date_In__c,
        Date_Out__c,
        Rate__c,
        Nights_CC__c,
        Sales_Housing__c,
        Room_Type__c,
        Projected_Units__c,
        Projected_Room_nights__c,
        Production_CC__c,
        Status_CC__c
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId()
        AND Sales_Housing__c = :stay.Id
      LIMIT 1
    ];
    Concessions__c concession = [
      SELECT
        Id,
        Concession_Type__c,
        Concessions_Requested__c,
        Concession_Provided__c,
        Notes__c,
        Production__c,
        Housing__c
      FROM Concessions__c
      WHERE Housing__c = :stay.Id
      ORDER BY CreatedDate DESC
      LIMIT 1
    ];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      Housing__c = stay.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent',
      isHousingCloseOutAvailable__c = true,
      isHousingCloseOutEditable__c = true,
      Include_in_options__c = true
    );
    insert bid;
    room.Id = null;
    room.Sales_Housing__c = null;
    room.Bid__c = bid.Id;
    room.Room_Type__c = 'Bid';
    insert room;
    concession.Id = null;
    concession.Housing__c = null;
    concession.Bid__c = bid.Id;
    insert concession;
    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Rate_Commission_RRU')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);
    Test.startTest();
    update new Housing__c(Id = stay.Id, Status_CC__c = 'Pending Client Choice');
    System.runAs(customer) {
      System.assertEquals(
        true,
        VoyajerController.verifyOptionAccess('optionsHousing', stay.Id, customer.ContactId).containsKey('productionId')
      );
      ///System.assertEquals(
      //true,
      //.getOptionsHousing(stay.Id).containsKey('bidOptions')
      // );
      System.assertEquals(true, VoyajerController.getOptionsHousingDetail(bid.Id).containsKey('optionDetailRecord'));
      
      VoyajerController.getCloseOutHousingVAT(System.JSON.serialize(new Map<String, Object>{'serviceId' => stay.Id, 'accountId' => vendor.Contact.AccountId}));
    }
    Test.stopTest();
  }

  @isTest
  static void testGroundBidOptions() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Ground__c groundTrip = [
      SELECT Id, RecordTypeId, Production_Ground__c
      FROM Ground__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('GT_Trip_Details')
          .getRecordTypeId()
      LIMIT 1
    ];
    //Concessions__c concession = [SELECT Id, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, Notes__c, Production__c, Housing__c FROM Concessions__c WHERE Housing__c =: stay.Id ORDER BY CreatedDate DESC LIMIT 1];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      GT__c = groundTrip.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent',
      Options__c = 1
    );
    insert bid;
    Ground__c bidSubTrip = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Sub_Trip_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      Bid_Sub_Trip__c = bid.Id
    );
    insert bidSubTrip;
    Ground__c bidTravel = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Travel_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      GT_Sub_Trip_Details__c = bidSubTrip.Id
    );
    insert bidTravel;

    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Ground_Rate_Travel_Commission')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);

    Test.startTest();
    update new Ground__c(Id = groundTrip.Id, Status_Ground__c = 'Pending Client Choice');
    System.runAs(customer) {
      System.assertEquals(
        true,
        VoyajerController.verifyOptionAccess('optionsGT', groundTrip.Id, customer.ContactId).containsKey('productionId')
      );
      System.assertEquals(true, VoyajerController.getOptionsGT(groundTrip.Id).containsKey('bidOptions'));
      System.assertEquals(true, VoyajerController.getOptionsGTPreview(groundTrip.Id).containsKey('bidOptions'));
      System.assertEquals(true, VoyajerController.getOptionsGTDetail(bid.Id).containsKey('optionDetailRecord'));
      VoyajerController.updateVATData(System.JSON.serialize(new Map<String, Object>{'revenue' => new Map<String, Object>{'id' => vendorRevenue.Id},
      				 'vatnumber' => 'Test', 'accountId' => vendor.Contact.AccountId, 'address' => 'Test'}));
      VoyajerController.updateVATData(System.JSON.serialize(new Map<String, Object>{'revenue' => new Map<String, Object>{'id' => vendorRevenue.Id},
      				 'vatnumber' => 'Test', 'accountId' => vendor.Contact.AccountId}));
      
    }
    Test.stopTest();
  }

  @isTest
  static void testAirBidOptions() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Air__c air = [
      SELECT Id, RecordTypeId, Production__c
      FROM Air__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
          .get('Air_Trip_Details')
          .getRecordTypeId()
      LIMIT 1
    ];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      Air__c = air.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent',
      Options__c = 1
    );
    insert bid;
    Air__c segment = new Air__c(
      RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Itinerary_Details')
        .getRecordTypeId(),
      Production__c = customerProduction.Id,
      Bid_Itinerary__c = bid.Id
    );
    insert segment;
    Air__c travel = new Air__c(
      RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Segments')
        .getRecordTypeId(),
      Production__c = customerProduction.Id,
      Air_Itinerary_Details__c = segment.Id
    );
    insert travel;

    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Rate_Commission')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);

    Test.startTest();
    update new Air__c(Id = air.Id, Status__c = 'Pending Client Choice');
    System.runAs(customer) {
      System.assertEquals(
        true,
        VoyajerController.verifyOptionAccess('optionsAir', air.Id, customer.ContactId).containsKey('productionId')
      );
      System.assertEquals(true, VoyajerController.getOptionsAir(air.Id).containsKey('bidOptions'));
      System.assertEquals(true, VoyajerController.getOptionsAirPreview(air.Id).containsKey('bidOptions'));
      System.assertEquals(true, VoyajerController.getOptionsAirDetail(bid.Id).containsKey('optionDetailRecord'));
    }
    Test.stopTest();
  }

  @isTest
  static void testVendorHousingBidPages() {
    Test.startTest();
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Housing__c stay = [
      SELECT Id
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
      LIMIT 1
    ];
    Housing__c room = [
      SELECT
        Id,
        RecordTypeId,
        Units__c,
        Unit_Type__c,
        Special_Notes__c,
        Date_In__c,
        Date_Out__c,
        Rate__c,
        Nights_CC__c,
        Sales_Housing__c,
        Room_Type__c,
        Projected_Units__c,
        Projected_Room_nights__c,
        Production_CC__c
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId()
        AND Sales_Housing__c = :stay.Id
      LIMIT 1
    ];
    Concessions__c concession = [
      SELECT
        Id,
        Concession_Type__c,
        Concessions_Requested__c,
        Concession_Provided__c,
        Notes__c,
        Production__c,
        Housing__c
      FROM Concessions__c
      WHERE Housing__c = :stay.Id
      ORDER BY CreatedDate DESC
      LIMIT 1
    ];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      Housing__c = stay.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent',
      isHousingCloseOutEditable__c = true
    );
    insert bid;
    room.Id = null;
    room.Sales_Housing__c = null;
    room.Bid__c = bid.Id;
    room.Room_Type__c = 'Bid';
    insert room;
    concession.Id = null;
    concession.Housing__c = null;
    concession.Bid__c = bid.Id;
    insert concession;
    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Rate_Commission_RRU')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);

    System.runAs(vendor) {
      //Fix By Clay Dev 12 March, 2021 - Test class fixes
      //System.assertEquals(0, VoyajerController.getVendorBids(vendor.ContactId).size());
      System.assertEquals(1, VoyajerController.getVendorBids(vendor.ContactId).size());
      System.assertEquals(true, VoyajerController.getVendorProductionBids(bid.Id).containsKey('itineraries'));
      System.assertEquals(
        true,
        VoyajerController.getVendorHousingBid(stay.Id, vendor.Contact.AccountId, false).containsKey('info')
      );
    }
    Test.stopTest();
  }

  @isTest
  static void testVendorGroundBidPages() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vgtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Ground__c groundTrip = [
      SELECT Id, RecordTypeId, Production_Ground__c
      FROM Ground__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('GT_Trip_Details')
          .getRecordTypeId()
      LIMIT 1
    ];
    //Concessions__c concession = [SELECT Id, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, Notes__c, Production__c, Housing__c FROM Concessions__c WHERE Housing__c =: stay.Id ORDER BY CreatedDate DESC LIMIT 1];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      GT__c = groundTrip.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent'
    );
    insert bid;
    Ground__c bidSubTrip = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Sub_Trip_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      Bid_Sub_Trip__c = bid.Id
    );
    insert bidSubTrip;
    Ground__c bidTravel = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Travel_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      GT_Sub_Trip_Details__c = bidSubTrip.Id
    );
    insert bidTravel;
    /*
        concession.Id = null;
        concession.Housing__c = null;
        concession.Bid__c = bid.Id;
        insert concession;
        */
    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Ground_Rate_Travel_Commission')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);

    System.runAs(vendor) {
      //System.assertEquals(0, VoyajerController.getVendorBids(vendor.ContactId).size());
      System.assertEquals(true, VoyajerController.getVendorProductionBids(bid.Id).containsKey('itineraries'));
    }
  }

  @isTest
  static void testVendorHousingBidActions() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Housing__c stay = [
      SELECT Id
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
      LIMIT 1
    ];
    Housing__c room = [
      SELECT
        Id,
        RecordTypeId,
        Units__c,
        Unit_Type__c,
        Special_Notes__c,
        Date_In__c,
        Date_Out__c,
        Rate__c,
        Nights_CC__c,
        Sales_Housing__c,
        Room_Type__c,
        Projected_Units__c,
        Projected_Room_nights__c,
        Production_CC__c
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId()
        AND Sales_Housing__c = :stay.Id
      LIMIT 1
    ];
    Concessions__c concession = [
      SELECT
        Id,
        Concession_Type__c,
        Concessions_Requested__c,
        Concession_Provided__c,
        Notes__c,
        Production__c,
        Housing__c
      FROM Concessions__c
      WHERE Housing__c = :stay.Id
      ORDER BY CreatedDate DESC
      LIMIT 1
    ];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      Housing__c = stay.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent',
      isHousingCloseOutEditable__c = true
    );
    insert bid;
    room.Id = null;
    room.Sales_Housing__c = null;
    room.Bid__c = bid.Id;
    room.Room_Type__c = 'Bid';
    insert room;
    concession.Id = null;
    concession.Housing__c = null;
    concession.Bid__c = bid.Id;
    insert concession;
    Test.startTest();
    System.runAs(vendor) {
      Map<String, Object> vendorHousingBid = VoyajerController.getVendorHousingBid(
        stay.Id,
        vendor.Contact.AccountId,
        false
      );
      System.assertEquals(true, vendorHousingBid.containsKey('info'));
      Map<String, Object> journal = new Map<String, Object>{
        'name' => 'Vendor Test',
        'title' => 'CEO',
        'email' => 'ceo.vendor@rrtest.com'
      };
      ((Map<String, Object>) vendorHousingBid.get('info')).put('notes', 'my notes');
      vendorHousingBid.put('journal', journal);
      vendorHousingBid.put('userProfile', 'HousingVendor');
      System.assertEquals('done', VoyajerController.updateVendorHousingBid(JSON.serialize(vendorHousingBid)));
    }
    Test.stopTest();
  }

  @isTest
  static void testVendorGroundBidActions() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vgtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Ground__c groundTrip = [
      SELECT Id, RecordTypeId, Production_Ground__c
      FROM Ground__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('GT_Trip_Details')
          .getRecordTypeId()
      LIMIT 1
    ];
    //Concessions__c concession = [SELECT Id, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, Notes__c, Production__c, Housing__c FROM Concessions__c WHERE Housing__c =: stay.Id ORDER BY CreatedDate DESC LIMIT 1];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      GT__c = groundTrip.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent'
    );
    insert bid;
    Ground__c bidSubTrip = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Sub_Trip_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      Bid_Sub_Trip__c = bid.Id
    );
    insert bidSubTrip;
    Ground__c bidTravel = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Travel_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      GT_Sub_Trip_Details__c = bidSubTrip.Id
    );
    insert bidTravel;
    /*
        concession.Id = null;
        concession.Housing__c = null;
        concession.Bid__c = bid.Id;
        insert concession;
        */
    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Ground_Rate_Travel_Commission')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);
    Test.startTest();
    System.runAs(vendor) {
      Map<String, Object> vendorGroundBid = VoyajerController.getVendorGroundBid(
        groundTrip.Id,
        vendor.Contact.AccountId,
        false
      );
      System.assertEquals(true, vendorGroundBid.containsKey('info'));
      Map<String, Object> journal = new Map<String, Object>{
        'name' => 'Vendor Test',
        'title' => 'CEO',
        'email' => 'ceo.vendor@rrtest.com'
      };
      ((Map<String, Object>) vendorGroundBid.get('info')).put('notes', 'my notes');
      vendorGroundBid.put('journal', journal);
      System.assertEquals('done', VoyajerController.updateVendorGroundBid(JSON.serialize(vendorGroundBid)));
      Map<String, Object> unableBid = new Map<String, Object>{ 'bidId' => bid.Id, 'journal' => journal };
      System.assertEquals('done', VoyajerController.unabledVendorBid(JSON.serialize(unableBid)));
    }
    Test.stopTest();
  }

  @isTest
  static void testVendorHousingBidReservation() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Housing__c stay = [
      SELECT Id
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
      LIMIT 1
    ];
    Housing__c room = [
      SELECT
        Id,
        RecordTypeId,
        Units__c,
        Unit_Type__c,
        Special_Notes__c,
        Date_In__c,
        Date_Out__c,
        Rate__c,
        Nights_CC__c,
        Sales_Housing__c,
        Room_Type__c,
        Projected_Units__c,
        Projected_Room_nights__c,
        Production_CC__c
      FROM Housing__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId()
        AND Sales_Housing__c = :stay.Id
      LIMIT 1
    ];
    Concessions__c concession = [
      SELECT
        Id,
        Concession_Type__c,
        Concessions_Requested__c,
        Concession_Provided__c,
        Notes__c,
        Production__c,
        Housing__c
      FROM Concessions__c
      WHERE Housing__c = :stay.Id
      ORDER BY CreatedDate DESC
      LIMIT 1
    ];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      Housing__c = stay.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent',
      isHousingCloseOutAvailable__c = true,
      isHousingCloseOutEditable__c = true
    );
    insert bid;
    room.Id = null;
    room.Sales_Housing__c = null;
    room.Bid__c = bid.Id;
    room.Room_Type__c = 'Bid';
    insert room;
    concession.Id = null;
    concession.Housing__c = null;
    concession.Bid__c = bid.Id;
    insert concession;
    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Rate_Commission_RRU')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);

    System.runAs(vendor) {
      System.assertEquals(
        true,
        VoyajerController.getReservationHousingDetail(bid.Id).containsKey('reservationDetailRecord')
      );
      System.assertEquals(
        true,
        VoyajerController.verifyVendorAccess('optionsHousing', bid.Id, vendor.Contact.AccountId)
          .containsKey('productionId')
      );
      Map<String, Object> closeOut = new Map<String, Object>{
        'serviceId' => stay.Id,
        'accountId' => vendor.Contact.AccountId
      };
      System.assertEquals(
        true,
        VoyajerController.getCloseOutHousing(JSON.serialize(closeOut)).containsKey('productionId')
      );
    }
  }

  @isTest
  static void testVendorGroundBidReservation() {
    User customer = [SELECT Id, ContactId, Contact.AccountId FROM User WHERE alias = 'jtestrr' LIMIT 1];
    User vendor = [
      SELECT Id, ContactId, Contact.AccountId, Housing_Preference__c
      FROM User
      WHERE alias = 'vhtestrr'
      LIMIT 1
    ];

    Opportunity customerProduction = [SELECT Id FROM Opportunity LIMIT 1];
    Ground__c groundTrip = [
      SELECT Id, RecordTypeId, Production_Ground__c
      FROM Ground__c
      WHERE
        RecordTypeId = :Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
          .get('GT_Trip_Details')
          .getRecordTypeId()
      LIMIT 1
    ];
    //Concessions__c concession = [SELECT Id, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, Notes__c, Production__c, Housing__c FROM Concessions__c WHERE Housing__c =: stay.Id ORDER BY CreatedDate DESC LIMIT 1];

    Bid__c bid = new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId(),
      Production__c = customerProduction.Id,
      GT__c = groundTrip.Id,
      Vendor__c = vendor.Contact.AccountId,
      Status__c = 'Sent'
    );
    insert bid;
    Ground__c bidSubTrip = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Sub_Trip_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      Bid_Sub_Trip__c = bid.Id
    );
    insert bidSubTrip;
    Ground__c bidTravel = new Ground__c(
      RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
        .get('GT_Travel_Details')
        .getRecordTypeId(),
      Production_Ground__c = customerProduction.Id,
      GT_Sub_Trip_Details__c = bidSubTrip.Id
    );
    insert bidTravel;
    /*
        concession.Id = null;
        concession.Housing__c = null;
        concession.Bid__c = bid.Id;
        insert concession;
        */
    Revenue__c vendorRevenue = new Revenue__c(
      RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Ground_Rate_Travel_Commission')
        .getRecordTypeId(),
      CurrencyIsoCode = 'USD',
      Bid__c = bid.Id
    );
    insert vendorRevenue;
    update new Bid__c(Id = bid.Id, Commission_Revenue__c = vendorRevenue.Id);

    System.runAs(vendor) {
      System.assertEquals(
        true,
        VoyajerController.getReservationGTDetail(bid.Id).containsKey('reservationDetailRecord')
      );
      System.assertEquals(
        true,
        VoyajerController.verifyVendorAccess('optionsGT', bid.Id, vendor.Contact.AccountId).containsKey('productionId')
      );
    }
  }

  @isTest
  static void testPart2Documents() {
    //city
    City__c c = new City__c(Name = 'City Test Name');
    insert c;

    //acc contact
    Id recordTypeAcc = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Vendor')
      .getRecordTypeId();
    Account acc_con = new Account(
      Name = 'Acc Test Name',
      recordTypeId = recordTypeAcc,
      ShippingStreet = 'test street',
      City__c = c.Id,
      Star_Rating__c = '5',
      Visa_Accepted__c = 'Yes'
    );
    insert acc_con;

    //contact
    Contact con = new Contact(
      LastName = 'LNContact',
      FirstName = 'FNContact',
      Email = 'contacttest123@test.com',
      AccountId = acc_con.Id
    );
    insert con;

    //user
    Profile profileId = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Vendor' LIMIT 1]; //'Road Rebel Vendor' //'Customer Community Plus(Custom)'
    User u = new User(
      LastName = 'LNTest',
      FirstName = 'FNTest',
      Alias = 'atest',
      Email = 'qwertytest@test.com',
      Username = 'qwertytest@test.com',
      ProfileId = profileId.id,
      TimeZoneSidKey = 'GMT',
      LanguageLocaleKey = 'en_US',
      EmailEncodingKey = 'UTF-8',
      LocaleSidKey = 'en_US',
      ContactId = con.Id
    );
    insert u;

    //opp
    Opportunity o = new Opportunity(
      Name = 'Opp Test Name',
      Type = 'Test',
      AccountId = acc_con.Id,
      StageName = 'Qualification',
      CloseDate = System.today()
    );
    insert o;

    //Production_Associations__c
    Id recordTypeId2 = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
      .get('Production_Coordinators')
      .getRecordTypeId();
    Production_Associations__c pa = new Production_Associations__c(
      User__c = u.Id,
      Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator;Primary Freight Coordinator;IR Coordinator;Account Manager',
      Production_Opp__c = o.Id,
      RecordTypeId = recordTypeId2
    );
    insert pa;

    //### HOUSING
    //housing 1
    Id recordTypeHH = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Housing')
      .getRecordTypeId();
    Housing__c h = new Housing__c(
      RecordTypeId = recordTypeHH,
      Production_CC__c = o.Id,
      Housing_Preference__c = 'RRU',
      City__c = c.Id,
      Deadline_Date__c = System.today(),
      Date_In__c = System.today(),
      Date_Out__c = System.today()
    );
    insert h;

    //bid housing 1
    Id recordTypeBid = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Bid')
      .getRecordTypeId();
    Bid__c b = new Bid__c(
      Vendor__c = acc_con.Id,
      Production__c = o.Id,
      RecordTypeId = recordTypeBid,
      Contract_Due_Date__c = null,
      //Contract_Due_Date__c = System.today(),
      Status__c = 'Contracted',
      Housing__c = h.Id,
      Room_Rate_Release_date__c = System.today(),
      isHousingCloseOutEditable__c = true
    );
    insert b;

    Test.startTest();
    //saveDocument
    VoyajerController.saveDocument('File Name Test', 'ZmlsZSB0ZXN0', 'File ReName Test', 'Contract', b.id);
    VoyajerController.saveDocument('File Name Test', 'ZmlsZSB0ZXN0', 'File ReName Test', 'Contract', h.id);

    //getDocuments
    //bid
    String cdId = [
      SELECT Id, ContentDocumentId, ContentDocument.CreatedDate, LinkedEntityId, ContentDocument.title
      FROM ContentDocumentLink
      WHERE LinkedEntityId = :b.Id
      LIMIT 1
    ]
    .ContentDocumentId;
    Share__c sha = new Share__c(WhatID__c = cdId, RelativeID__c = b.Id, isForVendors__c = true);

    try {
      insert sha;
    } catch (Exception e) {
      system.debug('duplication error/other error');
    }

    /*//housing
        cdId = [SELECT Id, ContentDocumentId, ContentDocument.CreatedDate, LinkedEntityId, ContentDocument.title FROM ContentDocumentLink WHERE LinkedEntityId =:h.Id LIMIT 1].ContentDocumentId;
        Share__c sha2 = new Share__c(WhatID__c = cdId, RelativeID__c = h.Id, isForVendors__c = true);
        insert sha2;*/

    Map<String, Object> auxStringObjectMap = new Map<String, Object>();
    System.runAs(u) {
      auxStringObjectMap = VoyajerController.getDocuments(b.Id);
      auxStringObjectMap = VoyajerController.getDocuments(h.Id);
    }
    Test.stopTest();
  }

  @isTest
  static void testPart2Housing() {
    //city
    City__c c = new City__c(Name = 'City Test Name');
    insert c;

    //acc contact
    Id recordTypeAcc = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Vendor')
      .getRecordTypeId();
    Account acc_con = new Account(
      Name = 'Acc Test Name',
      recordTypeId = recordTypeAcc,
      ShippingStreet = 'test street',
      City__c = c.Id,
      Star_Rating__c = '5',
      Visa_Accepted__c = 'Yes'
    );
    insert acc_con;

    //contact
    Contact con = new Contact(
      LastName = 'LNContact',
      FirstName = 'FNContact',
      Email = 'contacttest123@test.com',
      AccountId = acc_con.Id
    );
    insert con;

    //user
    Profile profileId = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Vendor' LIMIT 1]; //'Road Rebel Vendor' //'Customer Community Plus(Custom)'
    User u = new User(
      LastName = 'LNTest',
      FirstName = 'FNTest',
      Alias = 'atest',
      Email = 'qwertytest@test.com',
      Username = 'qwertytest@test.com',
      ProfileId = profileId.id,
      TimeZoneSidKey = 'GMT',
      LanguageLocaleKey = 'en_US',
      EmailEncodingKey = 'UTF-8',
      LocaleSidKey = 'en_US',
      ContactId = con.Id
    );
    insert u;

    //opp
    Opportunity o = new Opportunity(
      Name = 'Opp Test Name',
      Type = 'Test',
      AccountId = acc_con.Id,
      StageName = 'Qualification',
      CloseDate = System.today()
    );
    insert o;

    //Production_Associations__c
    Id recordTypeId2 = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
      .get('Production_Coordinators')
      .getRecordTypeId();
    Production_Associations__c pa = new Production_Associations__c(
      User__c = u.Id,
      Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator;Primary Freight Coordinator;IR Coordinator;Account Manager',
      Production_Opp__c = o.Id,
      RecordTypeId = recordTypeId2
    );
    insert pa;

    //### HOUSING
    //housing 1
    Id recordTypeHH = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Housing')
      .getRecordTypeId();
    Housing__c h = new Housing__c(
      RecordTypeId = recordTypeHH,
      Production_CC__c = o.Id,
      Housing_Preference__c = 'RRU',
      City__c = c.Id,
      Deadline_Date__c = System.today(),
      Date_In__c = System.today(),
      Date_Out__c = System.today()
    );
    insert h;

    //bid housing 1
    Id recordTypeBid = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Bid')
      .getRecordTypeId();
    Bid__c b = new Bid__c(
      Vendor__c = acc_con.Id,
      Production__c = o.Id,
      RecordTypeId = recordTypeBid,
      Contract_Due_Date__c = null,
      //Contract_Due_Date__c = System.today(),
      Status__c = 'Contracted',
      Housing__c = h.Id,
      Room_Rate_Release_date__c = System.today(),
      isHousingCloseOutEditable__c = true
    );
    insert b;

    //revenue bid housing 1
    Id recordTypeHRCRRE = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Rate_Commission_RRE')
      .getRecordTypeId();
    Revenue__c revenuebidh1 = new Revenue__c(
      RecordTypeId = recordTypeHRCRRE,
      Bid__c = b.Id,
      Total_Price__c = 10,
      Gratuity__c = 10,
      Base_Cost__c = 10,
      Rate__c = 10
    );
    insert revenuebidh1;

    //housing 2
    Id recordTypeRTO = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();
    Housing__c hRTO = new Housing__c(
      RecordTypeId = recordTypeRTO,
      Production_CC__c = o.Id,
      Housing_Preference__c = 'RRU',
      City__c = c.Id,
      Deadline_Date__c = System.today(),
      Date_In__c = System.today(),
      Date_Out__c = System.today(),
      Bid__c = b.Id
    );
    insert hRTO;

    //housing 3
    Id recordTypeIR = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Individual_Reservation')
      .getRecordTypeId();
    Housing__c hIR = new Housing__c(
      RecordTypeId = recordTypeIR,
      Production_CC__c = o.Id,
      Housing_Preference__c = 'RRU',
      City__c = c.Id,
      Deadline_Date__c = System.today(),
      Date_In__c = System.today(),
      Date_Out__c = System.today(),
      Bid__c = b.Id
    );
    insert hIR;

    //bid housing 3
    Bid__c bidhIR = new Bid__c(
      Vendor__c = acc_con.Id,
      Production__c = o.Id,
      RecordTypeId = recordTypeBid,
      Contract_Due_Date__c = null,
      //Contract_Due_Date__c = System.today(),
      Status__c = 'Contracted',
      Housing__c = hIR.Id,
      Room_Rate_Release_date__c = System.today(),
      isHousingCloseOutEditable__c = true
    );
    insert bidhIR;

    Test.startTest();
    Map<String, Object> auxStringObjectMap = new Map<String, Object>();
    System.runAs(u) {
      /*//getVendorBids
            List<VoyajerController.VendorBid> bids = new List<VoyajerController.VendorBid>();
            bids = VoyajerController.getVendorBids(con.Id);
            
            //getVendorProductionBids
            auxStringObjectMap = VoyajerController.getVendorProductionBids(b.Id);*/
      auxStringObjectMap = VoyajerController.getVendorProductionBids(bidhIR.Id);

      //getReservationHousingDetail
      auxStringObjectMap = VoyajerController.getReservationHousingDetail(b.Id);
    }
    Test.stopTest();
  }

  @isTest
  static void testPart2GT() {
    //city
    City__c c = new City__c(Name = 'City Test Name');
    insert c;

    //acc contact
    Id recordTypeAcc = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Vendor')
      .getRecordTypeId();
    Account acc_con = new Account(
      Name = 'Acc Test Name',
      recordTypeId = recordTypeAcc,
      ShippingStreet = 'test street',
      City__c = c.Id,
      Star_Rating__c = '5',
      Visa_Accepted__c = 'Yes'
    );
    insert acc_con;

    //contact
    Contact con = new Contact(
      LastName = 'LNContact',
      FirstName = 'FNContact',
      Email = 'contacttest123@test.com',
      AccountId = acc_con.Id
    );
    insert con;

    //user
    Profile profileId = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Vendor' LIMIT 1]; //'Road Rebel Vendor' //'Customer Community Plus(Custom)'
    User u = new User(
      LastName = 'LNTest',
      FirstName = 'FNTest',
      Alias = 'atest',
      Email = 'qwertytest@test.com',
      Username = 'qwertytest@test.com',
      ProfileId = profileId.id,
      TimeZoneSidKey = 'GMT',
      LanguageLocaleKey = 'en_US',
      EmailEncodingKey = 'UTF-8',
      LocaleSidKey = 'en_US',
      ContactId = con.Id
    );
    insert u;

    //opp
    Opportunity o = new Opportunity(
      Name = 'Opp Test Name',
      Type = 'Test',
      AccountId = acc_con.Id,
      StageName = 'Qualification',
      CloseDate = System.today()
    );
    insert o;

    //Production_Associations__c
    Id recordTypeId2 = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
      .get('Production_Coordinators')
      .getRecordTypeId();
    Production_Associations__c pa = new Production_Associations__c(
      User__c = u.Id,
      Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator;Primary Freight Coordinator;IR Coordinator;Account Manager',
      Production_Opp__c = o.Id,
      RecordTypeId = recordTypeId2
    );
    insert pa;

    //### GT
    //gt 1
    Id recordTypeGTD = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
      .get('GT_Trip_Details')
      .getRecordTypeId();
    Ground__c gt1 = new Ground__c(
      RecordTypeId = recordTypeGTD,
      Production_Ground__c = o.Id,
      Status_Ground__c = 'Contracted',
      Start_City__c = c.Id,
      Arriving_city__c = c.Id,
      Start_Date__c = System.today(),
      End_Date__c = System.today()
    );
    insert gt1;

    //bid gt 1
    Id recordTypeBidGT = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId();
    Bid__c bidgt1 = new Bid__c(
      Vendor__c = acc_con.Id,
      Production__c = o.Id,
      RecordTypeId = recordTypeBidGT,
      Contract_Due_Date__c = null,
      //Contract_Due_Date__c = System.today(),
      Status__c = 'Contracted',
      GT__c = gt1.Id,
      Room_Rate_Release_date__c = System.today()
    );
    insert bidgt1;

    //gt2
    Id recordTypeGTSTD = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
      .get('GT_Sub_Trip_Details')
      .getRecordTypeId();
    Ground__c gt2 = new Ground__c(
      RecordTypeId = recordTypeGTSTD,
      Production_Ground__c = o.Id,
      Status_Ground__c = 'Contracted',
      Start_City__c = c.Id,
      Arriving_city__c = c.Id,
      Start_Date__c = System.today(),
      End_Date__c = System.today(),
      Bid_Sub_Trip__c = bidgt1.Id
    );
    insert gt2;

    //gt3
    Id recordTypeVT = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
      .get('Vehicle_Type')
      .getRecordTypeId();
    Ground__c gt3 = new Ground__c(
      RecordTypeId = recordTypeVT,
      Production_Ground__c = o.Id,
      GT_Sub_Trip_Details__c = gt2.Id,
      Bid__c = bidgt1.Id
    );
    insert gt3;

    //gt4
    Id recordTypeGTTD = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
      .get('GT_Travel_Details')
      .getRecordTypeId();
    Ground__c gt4 = new Ground__c(
      RecordTypeId = recordTypeGTTD,
      Production_Ground__c = o.Id,
      Start_City__c = c.Id,
      Arriving_city__c = c.Id,
      Start_Date__c = System.today(),
      End_Date__c = System.today(),
      Bid_Sub_Trip__c = bidgt1.Id,
      GT_Sub_Trip_Details__c = gt2.Id,
      Vehicle_Lookup__c = gt3.Id
    );
    insert gt4;

    //revenue bid gt 1
    Revenue__c revenuwbidgt1 = new Revenue__c(
      Bid__c = bidgt1.Id,
      Total_Price__c = 10,
      Gratuity__c = 10,
      Base_Cost__c = 10,
      Rate__c = 10
    );
    insert revenuwbidgt1;
    //END DATA

    Test.startTest();
    Map<String, Object> auxStringObjectMap = new Map<String, Object>();
    System.runAs(u) {
      //getReservationGTDetail
      auxStringObjectMap = VoyajerController.getReservationGTDetail(bidgt1.Id);

      //getContactUsData
      auxStringObjectMap = VoyajerController.getContactUsData(o.Id);
    }
    Test.stopTest();
  }
}
```


# Last Modified


# Usage

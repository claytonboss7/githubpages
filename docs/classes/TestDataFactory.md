---
layout: default
title: TestDataFactory
parent: classes
---

```@isTest
public with sharing class TestDataFactory {

    public static void createHousingDataHotelHousing() {

      Test.startTest();
      ApexUtil.OpportunityTrigger_Is_Enabled = false;
      ApexUtil.HousingTrigger_Is_Enabled = false;
      HousingTriggerHandler.TriggerDisabled = true;
      String Hotel_VendorRT = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Vendor')
      .getRecordTypeId();
      Id customerProfile = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Customer'].Id;
      Id vendorProfile = [SELECT Id FROM Profile WHERE Name = 'Road Rebel Vendor'].Id;
      Id guestUserProfile = [SELECT Id FROM Profile WHERE Name LIKE '%Guest%'].Id;
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
          RecordTypeId = Hotel_VendorRT,
          Status__c = 'Active',
          Market__c = 'Other',
          CurrencyIsoCode = 'USD',
          ShippingStreet = 'Ship Street',
          ShippingCity = 'San Diego',
          ShippingState = 'California',
          ShippingPostalCode = '90210'
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
          ProfileId = guestUserProfile,
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
          ProfileId = guestUserProfile,
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
          //Alias__c = 'Other'
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
          //Alias__c = 'Other'
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

      Bid__c bid = new Bid__c(
        RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId(),
        Production__c = opportunity.Id,
        Housing__c = housingStay.Id,
        Vendor__c = [SELECT Id FROM Account WHERE RecordTypeId = :Hotel_VendorRT].Id,
        Status__c = 'Sent',
        isHousingCloseOutEditable__c = true    );
      insert bid;
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
          Production_CC__c = opportunity.Id,
          Comps__c = 10,
          Commission_Due__c = 100,
          Bid__c = bid.Id,
          Rate__c = 100,
          Total_Room_Nights__c = 1
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
          Production_CC__c = opportunity.Id,
          Comps__c = 10,
          Commission_Due__c = 100
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
          Production__c = opportunity.Id,
          Bid__c = bid.Id
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

      Revenue__c theCommiss = new Revenue__c(
        RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
          .get('Housing_Rate_Commission_RRU')
          .getRecordTypeId(),
        CurrencyIsoCode = 'USD',
        Bid__c = bid.Id,
        Commission_Percent__c = 10,
        Commission_Type__c = 'Percentage',
        Total__c = 100,
        Invoice_Amount__c = 100
      );
      insert theCommiss;
      update new Bid__c(Id = bid.Id, Commission_Revenue__c = theCommiss.Id);
      /* create some of the shared config objects */
      insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
      insert new Dashboard_Session__c(
        Production_ID__c = [SELECT Id FROM Opportunity LIMIT 1]
        .Id,
        SetupOwnerId = UserInfo.getUserId()
      );
      Test.stopTest();
    }

}```

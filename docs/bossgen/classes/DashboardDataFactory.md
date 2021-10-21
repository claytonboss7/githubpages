---
layout: default
title: DashboardDataFactory
parent: classes
---
# Metadata Type
classes


# Filename 
DashboardDataFactory


# Raw XML
```
@isTest
public class DashboardDataFactory{
    private static Account productionAccount;
    private static Contact productionContact;
    private static Opportunity production;
    static{
        productionAccount = new Account(
            Name = 'ProductionAccountTest01'
        );
        insert productionAccount;
        productionContact = new Contact(
            LastName = 'ProductionContactTest01',
            AccountId = productionAccount.Id,
            Email = 'ProductionContactTest01@test.com'
        );
        insert productionContact;
        production = new Opportunity(
            RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), 
            Name = 'Cats', 
            AccountId = productionAccount.id, 
            StageName = 'Active', 
            CloseDate = Date.Today()
        );
        insert production;
    }
    public static void createCongaQuery(){
        List<String> nameList = new List<String>{'Housing - BidById',
          'Housing - HousingsByBidId',
          'Housing - ContactById',
          'Housing - ContactsByAccountId',
          'Housing - ProductionAssociationsByOppId',
          'Housing - UserById',
          'Housing - AssociatedCitiesByAccountId',
          'Housing - CorporateHousingVendorsByAccountId',
          'Housing - ConcessionsByBidId',
          'Housing - RevenueByBidId',
          'Housing - HousingDoubleRooms2Beds - Rate',
          'Housing - VendorAirportAssociationsByVendorId'};
              List<APXTConga4__Conga_Merge_Query__c> congaQueries = new List<APXTConga4__Conga_Merge_Query__c>();
              for(String name : nameList) {
                  congaQueries.add(new APXTConga4__Conga_Merge_Query__c(APXTConga4__Name__c = name));
              }
                  insert congaQueries;
    }
    public static void createHousingData(Integer numberOfBids, Boolean isAll){
        List<City__c> housingCities = new List<City__c>{
            new City__c(Name = 'San Diego, California', City__c = 'San Diego', Country__c = 'United States', State__c = 'California')
            //new City__c(Name = 'Toronto, Ontario', City__c = 'Toronto', Country__c = 'Canada', State__c = 'Ontario'),
            //new City__c(Name = 'Barcelona, Catalonia', City__c = 'Barcelona', Country__c = 'Spain', State__c = 'Catalonia')
        };
        insert housingCities;
        Integer j;
        List<Account> housingVendorAccounts = new List<Account>();
        for(Integer i = j = 0; i < (numberOfBids + 1); i++){
            housingVendorAccounts.add(new Account(
                RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Hotel_Vendor').getRecordTypeId(), 
                Name = 'HousingVendorTest' + String.valueOf(i + 1),
                City__c = housingCities[j].Id,
                ShippingStreet = 'Street' + String.valueOf(i + 1),
                ShippingCountry = housingCities[j].Country__c,
                ShippingState = housingCities[j] != null ? housingCities[j].State__c : 'California',
                Walk_to_Restaurant__c = 'Yes'
            ));
            j = j + 1 < housingCities.size() ? j + 1 : 0;
        }
        insert housingVendorAccounts;
        List<Contact> housingVendorContacts = new List<Contact>();
        for(Integer i = 0; i < numberOfBids; i++){
            housingVendorContacts.add(new Contact(
                LastName = 'HousingVendorContactTest' + String.valueOf(i + 1),
                AccountId = housingVendorAccounts.size() > i ? housingVendorAccounts[i].id : null,
                Email = 'HousingVendorContactTest' + String.valueOf(i + 1) + '@test.com',
                Order__c = 1
            ));
        }
        insert housingVendorContacts;
        List<Account> housingVendorCorporateAccounts = new List<Account>();
        for(Integer i = j = 0; i < (numberOfBids + 1); i++){
            housingVendorCorporateAccounts.add(new Account(
                RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Corporate_Housing_Vendor').getRecordTypeId(), 
                Name = 'HousingVendorTest' + String.valueOf(i + 1),
                City__c = housingCities[j].Id,
                ShippingStreet = 'Street' + String.valueOf(i + 1),
                ShippingCountry = housingCities[j].Country__c,
                ShippingState = housingCities[j].State__c,
                Walk_to_Restaurant__c = 'Yes'
            ));
            j = j + 1 < housingCities.size() ? j + 1 : 0;
        }
        if(isAll) insert housingVendorCorporateAccounts;
        insert new List<Production_Associations__c>{
            new Production_Associations__c(
                RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId(), 
                Production_Opp__c = production.id,
                User__c = UserInfo.getUserId(),
                Team_Roles__c = 'Primary Housing Coordinator;Primary Contract Coordinator'
            ),
            new Production_Associations__c(
                RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId(), 
                Production_Opp__c = production.id,
                Contact__c = productionContact.Id,
                Company__c = productionAccount.id,
                Role__c = 'Primary Housing;CC: Housing;Contract Signer'
            ),
            new Production_Associations__c(
                RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId(), 
                Production_Opp__c = production.id,
                Contact__c = !housingVendorContacts.isEmpty() ? housingVendorContacts[0].Id : null,
                Company__c = !housingVendorContacts.isEmpty() ? housingVendorContacts[0].AccountId : null,
                Role__c = 'Other'
            )
        };
        List<Housing__c> productionRoomTypes = new List<Housing__c>();
        for(Integer i = 1; i <= 3; i++){
            productionRoomTypes.add(new Housing__c(
                RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Room_Types_Ops').getRecordTypeId(),
                Production_CC__c = production.id, 
                Unit_Type__c = i == 2 ? '2-Bedroom / 1-Bath' : String.valueOf(i) + '-Bedroom',
                Special_Notes__c = 'Test ' + String.valueOf(i)
            ));
        }
        insert productionRoomTypes;
        List<Concessions__c> productionConcessions = new List<Concessions__c>();
        for(Integer i = 1; i <= 3; i++){
            productionConcessions.add(new Concessions__c(
                Production__c = production.id, 
                Concessions_Requested__c = i == 0 ? 'Complimentary High Speed internet.' : i == 1 ? 'Complimentary Parking.' : 'All single rooms must have king beds.',
                Concession_Type__c = 'Housing',
                Notes__c = 'Test ' + String.valueOf(i)
            ));
        }
        insert productionConcessions;
        Housing__c housingSales = new Housing__c(
            RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Sales_Housing').getRecordTypeId(),
            Production_CC__c = production.id,
            Contracting_Requirements__c = null,
            Billing_Options__c = null,
            Internal_Notes__c = null
        );
        insert housingSales;
        Housing__c housingStay = new Housing__c(
            RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Hotel_Housing').getRecordTypeId(),
            Production_CC__c = production.id,
            Date_In__c = Date.Today(),
            Date_Out__c = Date.Today().addMonths(1),
            City__c = housingCities[0].id,
            Group__c = 'Cast',
            Deadline_Date__c = Date.Today().addMonths(1),
            Status_CC__c = 'Itinerary Received'
        );
        Housing__c corporateHousingStay = new Housing__c(
            RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Corporate_Housing').getRecordTypeId(),
            Production_CC__c = production.id,
            Date_In__c = Date.Today(),
            Date_Out__c = Date.Today().addMonths(1),
            City__c = housingCities[0].id,
            Group__c = 'Cast',
            Deadline_Date__c = Date.Today().addMonths(1),
            Status_CC__c = 'Itinerary Received'
        );
        insert new List<Housing__c>{housingStay, corporateHousingStay};
        Itinerary__c housingItinerary = new Itinerary__c(
            RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Housing_Itinerary').getRecordTypeId(),
            Production__c = production.id,
           	Housing__c = housingStay.Id,
            Start_Date__c = housingStay.Date_In__c,
            End_Date__c = housingStay.Date_Out__c,
            City__c = housingStay.City__c,
            Status__c = housingStay.Status_CC__c
        );
        insert housingItinerary;
        Housing__c housingTournament = new Housing__c(
            RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Tournament').getRecordTypeId(),
            Production_CC__c = production.id,
            Date_In__c = Date.Today(),
            Date_Out__c = Date.Today().addMonths(1),
            City__c = housingCities[0].id,
            Group__c = 'Cast',
            Deadline_Date__c = Date.Today().addMonths(1),
            Status_CC__c = 'Itinerary Received'
        );
        if(isAll) insert housingTournament;
        List<Journal__c> housingJournals = new List<Journal__c>();
        for(Integer i = 1; i <= 3; i++){
            housingJournals.add(new Journal__c(
                RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Journal').getRecordTypeId(),
                Production__c = production.id, 
                Housing__c = housingStay.Id,
                Journal_Entry__c = 'Test ' + String.valueOf(i)
            ));
        }
        insert housingJournals;
        List<Journal__c> housingChildJournals = new List<Journal__c>();
        for(Integer i = 1; i <= 3; i++){
            housingChildJournals.add(new Journal__c(
                RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Journal').getRecordTypeId(),
                Production__c = production.id, 
                Housing__c = housingStay.Id,
                Parent_Journal__c = housingJournals[0].Id,
                Journal_Entry__c = 'Test ' + String.valueOf(i)
            ));
        }
        if(isAll) insert housingChildJournals;
        List<Housing__c> housingStayRoomTypes = new List<Housing__c>();
        for(Housing__c productionRoomType:productionRoomTypes){
            housingStayRoomTypes.add(new Housing__c(
                RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Room_Types_Ops').getRecordTypeId(),
                Production_CC__c = production.id, 
                Date_In__c = housingStay.Date_In__c,
                Date_Out__c = housingStay.Date_Out__c,
                Sales_Housing__c = housingStay.Id,
                Unit_Type__c = productionRoomType.Unit_Type__c,
                Special_Notes__c = productionRoomType.Special_Notes__c
            ));
        }
        insert housingStayRoomTypes;
        List<Concessions__c> housingStayConcessions = new List<Concessions__c>();
        for(Concessions__c productionConcession:productionConcessions){
            housingStayConcessions.add(new Concessions__c(
                Production__c = production.id, 
                Housing__c = housingStay.Id, 
                Concessions_Requested__c = productionConcession.Concessions_Requested__c,
                Concession_Type__c = 'Housing',
                Notes__c = productionConcession.Concessions_Requested__c
            ));
        }
        insert housingStayConcessions;
        List<Bid__c> housingBids = new List<Bid__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            housingBids.add(new Bid__c(
                RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId(),
                Production__c = production.id,
                Housing__c = housingStay.id,
                Vendor__c = housingVendorAccounts.size() > i ? housingVendorAccounts[i].id : null,
                Vendor_Contact__c = housingVendorContacts.size() > i ? housingVendorContacts[i].id : null,
                City__c = housingCities[0].id,
                CurrencyIsoCode = 'USD',
                Status__c = 'Unsent',
                Options__c = i + 1
            ));
        }
        insert housingBids;
        List<Housing__c> housingBidRoomTypes = new List<Housing__c>();
        List<Concessions__c> housingBidConcessions = new List<Concessions__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            for(Housing__c productionRoomType:housingStayRoomTypes){
                housingBidRoomTypes.add(new Housing__c(
                    RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Room_Types_Ops').getRecordTypeId(),
                    Production_CC__c = production.id, 
                    Bid__c = housingBids.size() > i ? housingBids[i].id : null,
                    Room_Type__c = 'Bid',
                    Date_In__c = housingStay.Date_In__c,
                    Date_Out__c = housingStay.Date_Out__c,
                    Unit_Type__c = productionRoomType.Unit_Type__c,
                    Special_Notes__c = productionRoomType.Special_Notes__c
                ));
            }
            for(Concessions__c housingStayConcession:housingStayConcessions){
                housingBidConcessions.add(new Concessions__c(
                    Production__c = production.id, 
                    Bid__c = housingBids.size() > i ? housingBids[i].id : null, 
                    Concessions_Requested__c = housingStayConcession.Concessions_Requested__c,
                    Concession_Type__c = 'Housing',
                    Notes__c = housingStayConcession.Concessions_Requested__c
                ));
            }
        }
        insert housingBidRoomTypes;
        insert housingBidConcessions;
    }
    public static void createGTData(Integer numberOfBids){
        List<Account> gtVendorAccounts = new List<Account>();
        for(Integer i = 0; i < numberOfBids; i++){
            gtVendorAccounts.add(new Account(
                RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Ground_Travel_Vendor').getRecordTypeId(), 
                Name = 'GtVendorTest' + String.valueOf(i + 1)
            ));
        }
        insert gtVendorAccounts;
        List<Contact> gtVendorContacts = new List<Contact>();
        for(Integer i = 0; i < numberOfBids; i++){
            gtVendorContacts.add(new Contact(
                LastName = 'GtVendorContactTest' + String.valueOf(i + 1),
                AccountId = gtVendorAccounts.size() > i ? gtVendorAccounts[i].id : null,
                Email = 'GtVendorContactTest' + String.valueOf(i + 1) + '@test.com',
                Order__c = 1
            ));
        }
        insert gtVendorContacts;
        insert new Production_Associations__c(
            RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId(), 
            Production_Opp__c = production.id,
            User__c = UserInfo.getUserId(),
            Team_Roles__c = 'Primary GT Coordinator;Primary Contract Coordinator'
        );
        insert new Production_Associations__c(
            RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId(), 
            Production_Opp__c = production.id,
            Contact__c = !gtVendorContacts.isEmpty() ? gtVendorContacts[0].id : null,
            Role__c = 'Primary GT;CC: GT;Contract Signer'
        );
        Ground__c gtSales = new Ground__c(
            RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Sales_GT_Details').getRecordTypeId(),
            Production_Ground__c = production.id,
            Contracting_Terms__c = null,
            Billing_Options__c = null,
            Internal_Notes__c = null
        );
        insert gtSales;
        City__c city = new City__c(
            Name = 'San Diego, California',
            City__c = 'San Diego',
            Country__c = 'United States',
            State__c = 'California'
        );
        insert city;
        Ground__c gtTrip = new Ground__c(
            RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId(),
            Production_Ground__c = production.id,
            Start_Date__c = Date.Today(),
            End_Date__c = Date.Today().addMonths(1),
            Start_City__c = city.id,
            Group_Type__c = 'Cast',
            Deadline_Date__c = Date.Today().addMonths(1),
            Status__c = 'Contracted'
        );
        insert gtTrip;
        Itinerary__c gtItinerary = new Itinerary__c(
            RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('GT_Itinerary').getRecordTypeId(),
            Production__c = production.id,
           	GT__c = gtTrip.Id,
            Start_Date__c = gtTrip.Start_Date__c,
            End_Date__c = gtTrip.End_Date__c,
            City__c = gtTrip.Start_City__c,
            Status__c = gtTrip.Status__c
        );
        insert gtItinerary;
        Ground__c gtTripSubtrip = new Ground__c(
            RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId(),
            Production_Ground__c = production.id, 
            GT_Trip_Details__c = gtTrip.Id,
            Trip_Order__c = 1,
            Description__c = null
        );
        insert gtTripSubtrip;
        List<Ground__c> gtTripTravels = new List<Ground__c>();
        for(Integer i = 0; i <= 3; i++){
            gtTripTravels.add(new Ground__c(
                RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId(),
                Production_Ground__c = production.id, 
                GT_Sub_Trip_Details__c = gtTripSubtrip.id,
                Line__c = i,
                Vehicle_Ref__c = String.valueOf(i),
                Start_Date__c = Date.Today().addDays(i + 1),
                Start_Date_Time__c = Time.newInstance(i, 0, 0, 0),
                Start_Date_Full__c = Datetime.newInstance(Date.Today().addDays(i + 1), Time.newInstance(i, 0, 0, 0)),
                End_Date__c = Date.Today().addDays(i + 2),
                End_Date_Time__c = Time.newInstance(i, 0, 0, 0),
                End_Date_Full__c = Datetime.newInstance(Date.Today().addDays(i + 2), Time.newInstance(i, 0, 0, 0)),
                Travel_Type__c = 'Depart',
                Group_Type__c = 'Cast',
                Location_Type__c = 'Airport',
                Location_Pick_up__c = 'Airport',
                Location_Drop_off__c = 'Airport',
                Location_Details__c = 'Test ' + String.valueOf(i),
                Airline_Info_Special_Notes__c = 'Coach will meet group in front of Hotel'
            ));
        }
        insert gtTripTravels;
        List<Ground__c> gtTripVehicles = new List<Ground__c>();
        for(Integer i = 0; i <= 3; i++){
            gtTripVehicles.add(new Ground__c(
                RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId(),
                Production_Ground__c = production.id, 
                GT_Sub_Trip_Details__c = gtTripSubtrip.id,
                Line__c = i,
                Vehicle_Ref__c = String.valueOf(i),
                Vehicle_Type__c = 'Coach',
                Capacity__c = (i + 1) * 10,
                Make__c = 'Volvo',
                Model__c = '417',
                Year__c = '2019',
                Amenities__c = 'WiFi;DVD;Table'
            ));
        }
        insert gtTripVehicles;
        List<Bid__c> gtBids = new List<Bid__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            gtBids.add(new Bid__c(
                RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId(),
                Production__c = production.id,
                GT__c = gtTrip.id,
                Vendor__c = gtVendorAccounts.size() > i ? gtVendorAccounts[i].id : null,
                Vendor_Contact__c = gtVendorContacts.size() > i ? gtVendorContacts[i].id : null,
                City__c = city.id,
                CurrencyIsoCode = 'USD',
                Status__c = 'Unsent',
                Options__c = i + 1
            ));
        }
        insert gtBids;
        List<Ground__c> gtBidSubtrips = new List<Ground__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            gtBidSubtrips.add(new Ground__c(
                RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId(),
                Production_Ground__c = production.id, 
                Bid_Sub_Trip__c = gtBids.size() > i ? gtBids[i].id : null,
                Trip_Order__c = 1,
                Description__c = null
            ));
        }
        insert gtBidSubtrips;
        List<Ground__c> gtBidTravels = new List<Ground__c>();
        List<Ground__c> gtBidVehicles = new List<Ground__c>();
        List<Revenue__c> gtBidRevenues = new List<Revenue__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            for(Integer j = 0; j <= 3; j++){
                gtBidTravels.add(new Ground__c(
                    RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId(),
                    Production_Ground__c = production.id, 
                    GT_Sub_Trip_Details__c = gtBidSubtrips.size() > i ? gtBidSubtrips[i].id : null,
                    Line__c = j,
                    Vehicle_Ref__c = String.valueOf(j),
                    Start_Date__c = Date.Today().addDays(j + 1),
                    Start_Date_Time__c = Time.newInstance(j, 0, 0, 0),
                    Start_Date_Full__c = Datetime.newInstance(Date.Today().addDays(j + 1), Time.newInstance(j, 0, 0, 0)),
                    End_Date__c = Date.Today().addDays(j + 2),
                    End_Date_Time__c = Time.newInstance(j, 0, 0, 0),
                    End_Date_Full__c = Datetime.newInstance(Date.Today().addDays(j + 2), Time.newInstance(j, 0, 0, 0)),
                    Travel_Type__c = 'Depart',
                    Group_Type__c = 'Cast',
                    Location_Type__c = 'Airport',
                    Location_Pick_up__c = 'Airport',
                    Location_Drop_off__c = 'Airport',
                    Location_Details__c = 'Test ' + String.valueOf(j),
                    Airline_Info_Special_Notes__c = 'Coach will meet group in front of Hotel'
                ));
                gtBidVehicles.add(new Ground__c(
                    RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId(),
                    Production_Ground__c = production.id, 
                    Bid__c = gtBids.size() > i ? gtBids[i].id : null,
                    Line__c = j,
                    Vehicle_Ref__c = String.valueOf(j),
                    Vehicle_Type__c = 'Coach',
                    Capacity__c = (j + 1) * 10,
                    Make__c = 'Volvo',
                    Model__c = String.valueOf(415 + j),
                    Year__c = String.valueOf(2020 + j),
                    Amenities__c = 'WiFi;DVD;Table'
                ));
            }
            gtBidRevenues.add(new Revenue__c(
                RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName().get('Ground_Rate_Travel_Commission').getRecordTypeId(),
                Production__c = production.id,
                Bid__c = gtBids.size() > i ? gtBids[i].id : null,
                Base_Cost__c = 20 * (i + 1),
                Commission__c = 5 * (i + 1),
                Rate__c = 1 * (i + 1),
                Gratuity__c = 2 * i + 1,
                Total_Price__c = 30 * (i + 1),
                CurrencyIsoCode = 'USD'
            ));
        }
        insert gtBidTravels;
        insert gtBidVehicles;
        insert gtBidRevenues;
    }
    public static void createFreightData(Integer numberOfBids){
        List<Account> freightVendorAccounts = new List<Account>();
        for(Integer i = 0; i < numberOfBids; i++){
            freightVendorAccounts.add(new Account(
                RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Freight_Vendor').getRecordTypeId(), 
                Name = 'FreightVendorTest' + String.valueOf(i + 1)
            ));
        }
        insert freightVendorAccounts;
        List<Contact> freightVendorContacts = new List<Contact>();
        for(Integer i = 0; i < numberOfBids; i++){
            freightVendorContacts.add(new Contact(
                LastName = 'FreightVendorContactTest' + String.valueOf(i + 1),
                AccountId = freightVendorAccounts.size() > i ? freightVendorAccounts[i].id : null,
                Email = 'FreightVendorContactTest' + String.valueOf(i + 1) + '@test.com',
                Order__c = 1
            ));
        }
        insert freightVendorContacts;
        insert new Production_Associations__c(
            RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId(), 
            Production_Opp__c = production.id,
            User__c = UserInfo.getUserId(),
            Team_Roles__c = 'Primary Freight Coordinator;Primary Contract Coordinator'
        );
        insert new Production_Associations__c(
            RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId(), 
            Production_Opp__c = production.id,
            Contact__c = !freightVendorContacts.isEmpty() ? freightVendorContacts[0].id : null,
            Role__c = 'Primary Freight;CC: Freight;Contract Signer'
        );
        Freight__c freightSales = new Freight__c(
            RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Sales_Freight_Details').getRecordTypeId(),
            Production__c = production.id,
            Contracting_Terms__c = null,
            Billing_Options__c = null,
            Internal_Notes__c = null
        );
        insert freightSales;
        City__c city = new City__c(
            Name = 'San Diego, California',
            City__c = 'San Diego',
            Country__c = 'United States',
            State__c = 'California'
        );
        insert city;
        Freight__c freightTrip = new Freight__c(
            RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId(),
            Production__c = production.id,
            Start_Date__c = Date.Today(),
            End_Date__c = Date.Today().addMonths(1),
            Start_City__c = city.id,
            Group_Type__c = 'Cast',
            Deadline_Date__c = Date.Today().addMonths(1),
            Status__c = 'Contracted'
        );
        insert freightTrip;
        Itinerary__c freightItinerary = new Itinerary__c(
            RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Freight_Itinerary').getRecordTypeId(),
            Production__c = production.id,
           	Freight__c = freightTrip.Id,
            Start_Date__c = freightTrip.Start_Date__c,
            End_Date__c = freightTrip.End_Date__c,
            City__c = freightTrip.Start_City__c,
            Status__c = freightTrip.Status__c
        );
        insert freightItinerary;
        Freight__c freightTripSubtrip = new Freight__c(
            RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Sub_Trip_Details').getRecordTypeId(),
            Production__c = production.id, 
            Freight_Trip_Details__c = freightTrip.Id,
            Trip_Order__c = 1,
            Description__c = null
        );
        insert freightTripSubtrip;
        List<Freight__c> freightTripEquipments = new List<Freight__c>();
        for(Integer i = 0; i <= 3; i++){
            freightTripEquipments.add(new Freight__c(
                RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Equipment_Details').getRecordTypeId(),
                Production__c = production.id, 
                Freight_Sub_Trip_Details__c = freightTripSubtrip.id,
                Line__c = i,
                Vehicle_Ref__c = String.valueOf(i),
                Start_Date__c = Date.Today().addDays(i + 1),
                Start_Date_Time__c = Time.newInstance(i, 0, 0, 0),
                Start_Date_Full__c = Datetime.newInstance(Date.Today().addDays(i + 1), Time.newInstance(i, 0, 0, 0)),
                End_Date__c = Date.Today().addDays(i + 2),
                End_Date_Time__c = Time.newInstance(i, 0, 0, 0),
                End_Date_Full__c = Datetime.newInstance(Date.Today().addDays(i + 2), Time.newInstance(i, 0, 0, 0)),
                Travel_Type__c = 'Depart',
                Group_Type__c = 'Cast',
                Location_Type__c = 'Airport',
                Location_Pick_up__c = 'Airport',
                Location_Drop_off__c = 'Airport',
                Location_Details__c = 'Test ' + String.valueOf(i),
                Airline_Info_Special_Notes__c = 'Coach will meet group in front of Hotel'
            ));
        }
        insert freightTripEquipments;
        List<Freight__c> freightTripVehicles = new List<Freight__c>();
        for(Integer i = 0; i <= 3; i++){
            freightTripVehicles.add(new Freight__c(
                RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId(),
                Production__c = production.id, 
                Freight_Sub_Trip_Details__c = freightTripSubtrip.id,
                Line__c = i,
                Vehicle_Ref__c = String.valueOf(i),
                Vehicle_Type__c = 'Coach',
                Capacity__c = String.valueOf((i + 1) * 10),
                Make__c = 'Volvo',
                Model__c = '417',
                Year__c = '2019',
                Amenities__c = 'WiFi;DVD;Table'
            ));
        }
        insert freightTripVehicles;
        List<Bid__c> freightBids = new List<Bid__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            freightBids.add(new Bid__c(
                RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId(),
                Production__c = production.id,
                Freight__c = freightTrip.id,
                Vendor__c = freightVendorAccounts.size() > i ? freightVendorAccounts[i].id : null,
                Vendor_Contact__c = freightVendorContacts.size() > i ? freightVendorContacts[i].id : null,
                City__c = city.id,
                CurrencyIsoCode = 'USD',
                Status__c = 'Unsent',
                Options__c = i + 1
            ));
        }
        insert freightBids;
        List<Freight__c> freightBidSubtrips = new List<Freight__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            freightBidSubtrips.add(new Freight__c(
                RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Sub_Trip_Details').getRecordTypeId(),
                Production__c = production.id, 
                Bid_Sub_Trip__c = freightBids.size() > i ? freightBids[i].id : null,
                Trip_Order__c = 1,
                Description__c = null
            ));
        }
        insert freightBidSubtrips;
        List<Freight__c> freightBidEquipments = new List<Freight__c>();
        List<Freight__c> freightBidVehicles = new List<Freight__c>();
        List<Revenue__c> freightBidRevenues = new List<Revenue__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            for(Integer j = 0; j <= 3; j++){
                freightBidEquipments.add(new Freight__c(
                    RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Equipment_Details').getRecordTypeId(),
                    Production__c = production.id, 
                    Freight_Sub_Trip_Details__c = freightBidSubtrips.size() > i ? freightBidSubtrips[i].id : null,
                    Line__c = j,
                    Vehicle_Ref__c = String.valueOf(j),
                    Start_Date__c = Date.Today().addDays(j + 1),
                    Start_Date_Time__c = Time.newInstance(j, 0, 0, 0),
                    Start_Date_Full__c = Datetime.newInstance(Date.Today().addDays(j + 1), Time.newInstance(j, 0, 0, 0)),
                    End_Date__c = Date.Today().addDays(j + 2),
                    End_Date_Time__c = Time.newInstance(j, 0, 0, 0),
                    End_Date_Full__c = Datetime.newInstance(Date.Today().addDays(j + 2), Time.newInstance(j, 0, 0, 0)),
                    Travel_Type__c = 'Depart',
                    Group_Type__c = 'Cast',
                    Location_Type__c = 'Airport',
                    Location_Pick_up__c = 'Airport',
                    Location_Drop_off__c = 'Airport',
                    Location_Details__c = 'Test ' + String.valueOf(j),
                    Airline_Info_Special_Notes__c = 'Coach will meet group in front of Hotel'
                ));
                freightBidVehicles.add(new Freight__c(
                    RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId(),
                    Production__c = production.id, 
                    Bid__c = freightBids.size() > i ? freightBids[i].id : null,
                    Line__c = j,
                    Vehicle_Ref__c = String.valueOf(j),
                    Vehicle_Type__c = 'Coach',
                    Capacity__c = String.valueOf((j + 1) * 10),
                    Make__c = 'Volvo',
                    Model__c = '417',
                    Year__c = String.valueOf(2020 + j),
                    Amenities__c = 'WiFi;DVD;Table'
                ));
            }
            freightBidRevenues.add(new Revenue__c(
                RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName().get('Freight_Rate_Commission').getRecordTypeId(),
                Production__c = production.id,
                Bid__c = freightBids.size() > i ? freightBids[i].id : null,
                Base_Cost__c = 20 * (i + 1),
                Commission__c = 5 * (i + 1),
                Rate__c = 1 * (i + 1),
                Gratuity__c = 2 * i + 1,
                Total_Price__c = 30 * (i + 1),
                CurrencyIsoCode = 'USD'
            ));
        }
        insert freightBidEquipments;
        insert freightBidVehicles;
        insert freightBidRevenues;
    }
    public static void createAirData(Integer numberOfBids){
        List<Account> airVendorAccounts = new List<Account>();
        for(Integer i = 0; i < numberOfBids; i++){
            airVendorAccounts.add(new Account(
                RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId(), 
                Name = 'AirVendorTest' + String.valueOf(i + 1)
            ));
        }
        insert airVendorAccounts;
        List<Contact> airVendorContacts = new List<Contact>();
        for(Integer i = 0; i < numberOfBids; i++){
            airVendorContacts.add(new Contact(
                LastName = 'AirVendorContactTest' + String.valueOf(i + 1),
                AccountId = airVendorAccounts.size() > i ? airVendorAccounts[i].id : null,
                Email = 'AirVendorContactTest' + String.valueOf(i + 1) + '@test.com',
                Order__c = 1
            ));
        }
        insert airVendorContacts;
        insert new Production_Associations__c(
            RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId(), 
            Production_Opp__c = production.id,
            User__c = UserInfo.getUserId(),
            Team_Roles__c = 'Primary Air Coordinator;Primary Contract Coordinator'
        );
        insert new Production_Associations__c(
            RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Contacts').getRecordTypeId(), 
            Production_Opp__c = production.id,
            Contact__c = !airVendorContacts.isEmpty() ? airVendorContacts[0].id : null,
            Role__c = 'Primary Air;CC: Air;Contract Signer'
        );
        Air__c airSales = new Air__c(
            RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Sales_Air_Details').getRecordTypeId(),
            Production__c = production.id,
            Air_Internal_Notes__c = null
        );
        insert airSales;
        Air__c airTrip = new Air__c(
            RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId(),
            Production__c = production.id,
            Trip_Type__c = 'Multi-City',
            Group_Type__c = 'Cast',
            Departure_City__c = null,
            Departure_Date__c = Date.Today().addDays(1),
            Arrival_City__c = null,
            Status__c = 'Contracted'
        );
        insert airTrip;
        Itinerary__c airItinerary = new Itinerary__c(
            RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Air_Itinerary').getRecordTypeId(),
            Production__c = production.id,
           	Air__c = airTrip.Id,
            Start_Date__c = airTrip.Departure_Date__c,
            Status__c = airTrip.Status__c
        );
        insert airItinerary;
        City__c city = new City__c(
            Name = 'San Diego, California',
            City__c = 'San Diego',
            Country__c = 'United States',
            State__c = 'California'
        );
        insert city;
        List<Airport__c> airports = new List<Airport__c>();
        for(Integer i = 0; i <= 4; i++){
            airports.add(new Airport__c(
                Name = 'Airport' + String.valueOf(i),
                Airport_Code__c = 'A' + String.valueOf(i),
                City__c = city.id
            ));
        }
        insert airports;
        List<Air__c> airTripSegments = new List<Air__c>();
        for(Integer i = 0; i <= 3; i++){
            airTripSegments.add(new Air__c(
                RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId(),
                Production__c = production.id,
                Air_Trip_Details__c = airTrip.Id,
                Departure_Date__c = Date.Today().addDays(i + 1),
                Dep_Time__c = Time.newInstance(i, 0, 0, 0),
                Departure_City__c = airports[i].id,
                Arrival_Date__c = Date.Today().addDays(i + 2),
                Arr_Time__c = Time.newInstance(i, 0, 0, 0),
                Arrival_City__c = airports[i + 1].id
            ));
        }
        insert airTripSegments;
        List<Bid__c> airBids = new List<Bid__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            airBids.add(new Bid__c(
                RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId(),
                Production__c = production.id,
                Air__c = airTrip.id,
                Vendor__c = airVendorAccounts.size() > i ? airVendorAccounts[i].id : null,
                Vendor_Contact__c = airVendorContacts.size() > i ? airVendorContacts[i].id : null,
                CurrencyIsoCode = 'USD',
                Status__c = 'Unsent',
                Options__c = i + 1
            ));
        }
        insert airBids;
        List<Air__c> airBidItineraries = new List<Air__c>();
        List<Air__c> airBidDeviations = new List<Air__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            airBidItineraries.add(new Air__c(
                RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Itinerary_Details').getRecordTypeId(),
                Production__c = production.id, 
                Bid_Itinerary__c = airBids.size() > i ? airBids[i].id : null,
                Trip_Type__c = airTrip.Trip_Type__c,
                Group_Type__c = airTrip.Group_Type__c,
                Description__c = null,
                PAX__c = airTrip.PAX__c
            ));
            airBidDeviations.add(new Air__c(
                RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Deviation_Details').getRecordTypeId(),
                Production__c = production.id, 
                Bid_Deviation__c = airBids.size() > i ? airBids[i].id : null,
                Trip_Type__c = airTrip.Trip_Type__c,
                Group_Type__c = airTrip.Group_Type__c,
                Description__c = null,
                Deviation_Order_Conga__c = 1
            ));
        }
        insert airBidItineraries;
        insert airBidDeviations;
        List<Air__c> airBidSegments = new List<Air__c>();
        List<Revenue__c> rateDetails = new List<Revenue__c>();
        for(Integer i = 0; i < numberOfBids; i++){
            for(Integer j = 0; j <= 3; j++){
                airBidSegments.add(new Air__c(
                    RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId(),
                    Production__c = production.id,
                    Air_Itinerary_Details__c = airBidItineraries.size() > i ? airBidItineraries[i].id : null,
                    Order__c = j,
                    Departure_Date__c = Date.Today().addDays(j + 1),
                    Dep_Time__c = Time.newInstance(j, 0, 0, 0),
                    Departure_City__c = airports[j].id,
                    Arrival_Date__c = Date.Today().addDays(j + 2),
                    Arr_Time__c = Time.newInstance(j, 0, 0, 0),
                    Arrival_City__c = airports[j + 1].id,
                    Flight_No__c = String.valueOf(j),
                    Flight_Duration_hrs__c = j,
                    Flight_Duration_Mins__c = j,
                    Class__c = 'Economy'
                ));
                airBidSegments.add(new Air__c(
                    RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId(),
                    Production__c = production.id,
                    Air_Deviation_Details__c = airBidDeviations.size() > i ? airBidDeviations[i].id : null,
                    Order__c = j,
                    Departure_Date__c = Date.Today().addDays(j + 4),
                    Dep_Time__c = Time.newInstance(j, 0, 0, 0),
                    Departure_City__c = airports[j].id,
                    Arrival_Date__c = Date.Today().addDays(j + 5),
                    Arr_Time__c = Time.newInstance(j, 0, 0, 0),
                    Arrival_City__c = airports[j + 1].id,
                    Flight_No__c = String.valueOf(j),
                    Flight_Duration_hrs__c = j,
                    Flight_Duration_Mins__c = j,
                    Class__c = 'Economy',
                    Number_of_Seats__c = j + 1
                ));
                rateDetails.add(new Revenue__c(
                    RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName().get('Air_Rate_Commission').getRecordTypeId(),
                    Production__c = production.id,
                    Bid__c = airBids.size() > i ? airBids[i].id : null,
                    Deviation__c = math.mod(j + 1, 2) == 0 ? (airBidDeviations.size() > i ? airBidDeviations[i].id : null) : null,
                    Rate_currency__c = 20 * (j + 1),
                    Service_Fees__c = 10 * (j + 1),
                    Additional_Fees__c = 5 * (j + 1),
                    Total_Taxes__c = 2*j + 1,
                    Total_Price__c = 30 * (j + 1),
                    of_seats__c = j + 1,
                    Record_Locator__c = String.valueOf(j + 1)
                ));
            }
        }
        insert airBidSegments;
        insert rateDetails;
    }
}
```


# Last Modified


# Usage

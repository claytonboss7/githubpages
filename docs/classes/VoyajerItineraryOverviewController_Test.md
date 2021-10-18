---
layout: default
title: VoyajerItineraryOverviewController_Test
parent: classes
---

```@isTest
public class VoyajerItineraryOverviewController_Test {
    static{
        //DATA
        //acc
        Account a = new Account(Name = 'Acc Test Name');
        insert a;
        
        //opp
        Opportunity o = new Opportunity(Name = 'Opp Test Name',
                                          Type = 'Test',
                                          AccountId = a.Id,
                                          StageName ='Qualification',
                                          CloseDate = System.today());
        insert o;
        
        //city
        City__c c = new City__c(Name = 'City Test Name');
        insert c;
        
        //### HOUSING
        //housing 1
        Id recordTypeHH = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Hotel_Housing').getRecordTypeId();
        Housing__c h = new Housing__c(RecordTypeId = recordTypeHH,
                                     Production_CC__c = o.Id,
                                     Housing_Preference__c = 'RRU',
                                     City__c = c.Id,
                                     Deadline_Date__c = System.today(),
                                     Date_In__c = System.today(),
                                     Date_Out__c = System.today());
        insert h;
        
        //bid housing 1
        Id recordTypeBid = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId();
        Bid__c b = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBid,
                             Contract_Due_Date__c = null,
                             //Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             Housing__c = h.Id);
        insert b;
        
        //housing 2
        Housing__c h2 = new Housing__c(RecordTypeId = recordTypeHH,
                                     Production_CC__c = o.Id,
                                     Housing_Preference__c = 'RRU',
                                     City__c = c.Id,
                                     Deadline_Date__c = System.today(),
                                     Date_In__c = System.today(),
                                     Date_Out__c = System.today());
        insert h2;
        
        //bid housing 2
        Bid__c b2 = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBid,
                             //Contract_Due_Date__c = null,
                             Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             Housing__c = h2.Id);
        insert b2;
        
        Id recordTypeRTo = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Room_Types_Ops').getRecordTypeId();
        Housing__c roomType = new Housing__c(RecordTypeId = recordTypeRTo,
                                     Production_CC__c = o.Id,
                                     Housing_Preference__c = 'RRU',
                                     City__c = c.Id,
                                     Bid__c = b2.Id,
                                     Deadline_Date__c = System.today(),
                                     Date_In__c = System.today(),
                                     Date_Out__c = System.today().addDays(2));
        insert roomType;
        //###GT
        //gt 1
        Id recordTypeGTD = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId();
        Ground__c gt1 = new Ground__c(RecordTypeId = recordTypeGTD,
                                     Production_Ground__c = o.Id,
                                     Status_Ground__c = 'Contracted',
                                     Start_City__c = c.Id,
                                     Arriving_city__c = c.Id,
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today().addDays(2));
        insert gt1;
        
        //bid gt 1
        Id recordTypeBidGT = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId();
        Bid__c bidgt1 = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBidGT,
                             Contract_Due_Date__c = null,
                             //Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             GT__c = gt1.Id,
                             Room_Rate_Release_date__c = System.today());
        insert bidgt1;
        
        //gt2
        Id recordTypeGTSTD = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId();
        Ground__c gt2 = new Ground__c(RecordTypeId = recordTypeGTSTD,
                                     Production_Ground__c = o.Id,
                                     Status_Ground__c = 'Contracted',
                                     Start_City__c = c.Id,
                                     Arriving_city__c = c.Id,
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today(),
                                     //Bid_Sub_Trip__c = bidgt1.Id,
                                     GT_Trip_Details__c = gt1.Id);
        insert gt2;
        
        //gt3
        Id recordTypeVT = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId();
        Ground__c gt3 = new Ground__c(RecordTypeId = recordTypeVT,
                                     Production_Ground__c = o.Id,
                                     GT_Sub_Trip_Details__c = gt2.Id,
                                     Bid__c = bidgt1.Id);
        insert gt3;
        
        //gt4
        Id recordTypeGTTD = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId();
        Ground__c gt4 = new Ground__c(RecordTypeId = recordTypeGTTD,
                                     Production_Ground__c = o.Id,
                                     Start_City__c = c.Id,
                                     Arriving_city__c = c.Id,
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today().addDays(2),
                                     Bid_Sub_Trip__c = bidgt1.Id,
                                     GT_Sub_Trip_Details__c = gt2.Id,
                                     Vehicle_Lookup__c = gt3.Id);
        insert gt4;
        
        //revenue bid gt 1
        Revenue__c revenuwbidgt1 = new Revenue__c(Bid__c = bidgt1.Id,
                                                  Total_Price__c = 10,
                                                  Gratuity__c = 10,
                                                  Base_Cost__c = 10,
                                                  Rate__c = 10);
        insert revenuwbidgt1;
        
        //###FREIGHT
        //f 1
        Id recordTypeF = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId();
        Freight__c f1 = new Freight__c(RecordTypeId = recordTypeF,
                                     Production__c = o.Id,
                                     Start_City__c = c.Id,
                                     End_city__c = c.Id,
                                     Deadline_Date__c = System.today(),
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today().addDays(2),
                                     Description__c = 'Test desc',
                                   	 Service_Type__c = 'Ocean');
        insert f1;
        
        //bid f 1
        Id recordTypeBidF = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId();
        Bid__c bidf1 = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBidF,
                             Contract_Due_Date__c = null,
                             //Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             Freight__c = f1.Id);
        insert bidf1;
 		Freight__c freightSubtrip = new Freight__c(Freight_Trip_Details__c = f1.Id, Production__c = o.Id, 
        	RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Sub_Trip_Details').getRecordTypeId());
        insert freightSubtrip;
        //f 2
        Freight__c f2 = new Freight__c(RecordTypeId = recordTypeF,
                                     Production__c = o.Id,
                                     Start_City__c = c.Id,
                                     End_city__c = c.Id,
                                     Deadline_Date__c = System.today(),
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today().addDays(2),
                                     Description__c = 'Test desc',
                                   	 Service_Type__c = 'Ocean');
        insert f2;
        
        //bid f 2
        Bid__c bidf2 = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBidF,
                             //Contract_Due_Date__c = null,
                             Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             Freight__c = f2.Id);
        insert bidf2;
        //END DATA

        Air__c airTrip = new Air__c(
            RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId(),
            Production__c = o.id,
            Trip_Type__c = 'Multi-City',
            Group_Type__c = 'Cast',
            Departure_City__c = null,
            Departure_Date__c = Date.Today().addDays(1),
            Arrival_City__c = null,
            Status__c = 'Contracted'
        );
        Air__c airTrip2 = new Air__c(
            RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId(),
            Production__c = o.id,
            Trip_Type__c = 'Multi-City',
            Group_Type__c = 'Cast',
            Departure_City__c = null,
            Departure_Date__c = Date.Today().addDays(1),
            Arrival_City__c = null,
            Return_Date__c = Date.Today().addDays(2),
            Status__c = 'Contracted'
        );
        insert new List<Air__c>{airTrip, airTrip2};

        Itinerary__c airItinerary = new Itinerary__c(
            RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Air_Itinerary').getRecordTypeId(),
            Production__c = o.id,
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
                Production__c = o.id,
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
        airBids.add(new Bid__c(
            RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Air_Bid').getRecordTypeId(),
            Production__c = o.id,
            Air__c = airTrip.id,
            CurrencyIsoCode = 'USD',
            Status__c = 'Unsent',
            Options__c = 1
        ));
        insert airBids;
    }
    static testMethod void test01(){
        Opportunity o = [Select Id from Opportunity where Name = 'Opp Test Name'];        
        Test.startTest();
        // fix by Clay - 24 Dec, 2020
        String result = VoyajerItineraryOverviewController.searchItineraries(o.id, String.valueOf(System.today()), String.valueOf(System.today()), null);
        VoyajerItineraryOverviewController.getObjectsFromItinerary(result, 'Test');
        Map<Date, List<VoyajerItineraryOverviewController.Itinerary>> searchItinerariesMap = 
            (Map<Date, List<VoyajerItineraryOverviewController.Itinerary>>) 
            System.JSON.deserialize(VoyajerItineraryOverviewController.searchItineraries(o.id, null, null, null), 
        	Map<Date, List<VoyajerItineraryOverviewController.Itinerary>>.class);
		result = VoyajerItineraryOverviewController.searchItineraries(o.id, String.valueOf(System.today()), String.valueOf(System.today()), 'Test');
        VoyajerItineraryOverviewController.getFilteredItineraryRecordByCity(searchItinerariesMap, 'Test');
        
        //String result = VoyajerItineraryOverviewController.searchItineraries(o.id, String.valueOf(System.today()), String.valueOf(System.today()));
        Test.stopTest();
    }
}```

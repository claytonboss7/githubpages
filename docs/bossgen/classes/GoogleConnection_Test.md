---
layout: default
title: GoogleConnection_Test
parent: classes
---
# Metadata Type
classes


# Filename 
GoogleConnection_Test


# Raw XML
```
@isTest
public class GoogleConnection_Test {
    private static City__c cityRecord;
    private static Account vendorRecord;
    private static Account venueRecord;
    private static Vendor_Venue__c vendorVenueRecord;
    private static Airport__c airportRecord;
    static void generateData(){
        cityRecord = new City__c(Name = 'Test City',City__c = 'Pasadena',State__c='California',Country__c='United States');
        insert cityRecord;
        vendorRecord = new Account(Name = 'Test Parent', ShippingStreet = 'Test Parent', City__c = cityRecord.Id, RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Hotel_Vendor').getRecordTypeId());
        insert vendorRecord;
        venueRecord = new Account(Name = 'Test Venue', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Venue').getRecordTypeId());
        insert venueRecord;
        vendorVenueRecord = new Vendor_Venue__c(Vendor__c = vendorRecord.Id, Venue__c = venueRecord.Id);
        insert vendorVenueRecord;
        airportRecord = new Airport__c(Name = 'Test Airport', City__c = cityRecord.Id);
        insert airportRecord;
    }
    public static testMethod void pingTest(){
        generateData();
        Test.startTest();
        Set<Id> ids = new Set<Id>();
        ids.add(cityRecord.Id);
        GoogleConnection.ping(ids);
        Test.stopTest();  
    }
    public static testMethod void testverifyDistanceAirport(){
        generateData();
        Vendor_Airport_Association__c vas = new Vendor_Airport_Association__c(Airport__c = airportRecord.Id, Vendor__c = vendorRecord.Id);
        insert vas;
        Test.startTest();
        Set<Id> ids = new Set<Id>();
        ids.add(vas.Id);
        GoogleConnection.verifyDistanceAirport(ids);
        Test.stopTest();
        system.assertEquals(70138,[SELECT Id, Distance__c FROM Vendor_Airport_Association__c WHERE Id =: vas.Id].Distance__c);
    }
}
```


# Last Modified


# Usage

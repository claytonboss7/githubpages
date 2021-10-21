---
layout: default
title: VendorAirportTrigger_Test
parent: classes
---
# Metadata Type
classes


# Filename 
VendorAirportTrigger_Test


# Raw XML
```
@isTest
public class VendorAirportTrigger_Test {
    private static City__c cityRecord;
    private static Account vendorRecord;
    private static Airport__c airportRecord;
    static void generateData(){
        cityRecord = new City__c(Name = 'Test City',City__c = 'Pasadena',State__c='California',Country__c='United States');
        insert cityRecord;
        vendorRecord = new Account(Name = 'Test Parent', ShippingStreet = 'Test Parent', City__c = cityRecord.Id, RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Hotel_Vendor').getRecordTypeId());
        insert vendorRecord;
        airportRecord = new Airport__c(Name = 'Test Venue');
        insert airportRecord;
    }
    public static testMethod void insertTest(){
        generateData();
        Test.startTest();
        Vendor_Airport_Association__c vendorAirportRecord = new Vendor_Airport_Association__c(Vendor__c = vendorRecord.Id, Airport__c = airportRecord.Id);
        insert vendorAirportRecord;
        Test.stopTest();        
    }
    public static testMethod void updateTest(){
        generateData();
        Vendor_Airport_Association__c vendorAirportRecord = new Vendor_Airport_Association__c(Vendor__c = vendorRecord.Id, Airport__c = airportRecord.Id);
        insert vendorAirportRecord;
        Test.startTest();
        update vendorAirportRecord;
        Test.stopTest();        
    }
}
```


# Last Modified


# Usage

---
layout: default
title: VoyajerCustomLookup
parent: classes
---

```public class VoyajerCustomLookup {
    @AuraEnabled
    public static List<sObject> fetchLookupValues(String searchKeyWord, String sObjectName, String fieldName) {
        String searchKey = searchKeyWord + '%';
        List<sObject> result = new List<sObject>();
        String sQuery = '';
        switch on sObjectName {
            when 'Account' {
                String venueAccountRT = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Venue').getRecordTypeId();
                if(fieldName.equals('Venue_City__c')) sQuery = 'SELECT Id, Name, ShippingStreet, ShippingCity, ShippingState, ShippingPostalCode, City__c, City__r.Name, City__r.City__c, City__r.State__c, City__r.Country__c FROM Account WHERE RecordTypeId =: venueAccountRT AND City__c <> NULL AND (City__r.Name LIKE: searchKey OR City__r.City__c LIKE: searchKey OR City__r.State__c LIKE: searchKey OR City__r.Country__c LIKE: searchKey) ORDER BY CreatedDate DESC LIMIT 5';
                if(fieldName.equals('Venue__c')) sQuery = 'SELECT Id, Name, ShippingStreet, ShippingCity, ShippingState, ShippingPostalCode, City__c FROM Account WHERE City__c <> NULL AND RecordTypeId =: venueAccountRT AND Name LIKE: searchKey ORDER BY CreatedDate DESC LIMIT 5';
            }
            when 'City__c' {
                sQuery = 'SELECT Id, Name, City__c, State__c, Country__c FROM City__c WHERE City__c <> NULL AND Country__c <> NULL AND (Name LIKE: searchKey OR City__c LIKE: searchKey OR State__c LIKE: searchKey OR Country__c LIKE: searchKey) ORDER BY CreatedDate DESC LIMIT 5';
            }
            when 'Airport__c' {
                sQuery = 'SELECT Id, Name, Airport_Code__c FROM Airport__c WHERE Name <> NULL AND (Name LIKE: searchKey OR Airport_Code__c LIKE: searchKey) ORDER BY CreatedDate DESC LIMIT 5';
            }
        }
        if(String.isNotBlank(sQuery)) {
            List<sObject> listOfRecords = Database.query(sQuery);
            for(sObject obj : listOfRecords) result.add(obj);
        }
        return result;
    }
    
    @AuraEnabled
    public static sObject loadLookupValues(String recordId, String sObjectName, String fieldName) {
        sObject record;
        switch on sObjectName {
            when 'Account' {
                if(fieldName.equals('Venue_City__c')) {
                    record = new City__c();
                    List<City__c> searchCity = [SELECT Id, Name, City__c, State__c, Country__c FROM City__c WHERE Id = :recordId];
                    if(!searchCity.isEmpty()) record = searchCity.get(0);
                }
                if(fieldName.equals('Venue__c')) {
                    record = new Account();
                    List<Account> searchAccount = [SELECT Id, Name, ShippingStreet, ShippingCity, ShippingState, ShippingPostalCode, City__c, City__r.Name, City__r.City__c, City__r.State__c, City__r.Country__c FROM Account WHERE Id = :recordId];
                    if(!searchAccount.isEmpty()) record = searchAccount.get(0);
                }
            }
            when 'City__c' {
                record = new City__c();
                List<City__c> searchCity = [SELECT Id, Name, City__c, State__c, Country__c FROM City__c WHERE Id = :recordId];
                if(!searchCity.isEmpty()) record = searchCity.get(0);
            }
            when 'Airport__c' {
                record = new Airport__c();
                List<Airport__c> searchAirport = [SELECT Id, Name, Airport_Code__c FROM Airport__c WHERE Id = :recordId];
                if(!searchAirport.isEmpty()) record = searchAirport.get(0);
            }
            when else {
                record = null;
            }
        }
        return record;
    }
}```

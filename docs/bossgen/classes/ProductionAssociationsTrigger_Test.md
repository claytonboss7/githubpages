---
layout: default
title: ProductionAssociationsTrigger_Test
parent: classes
---
# Metadata Type
classes


# Filename 
ProductionAssociationsTrigger_Test


# Raw XML
```
@isTest
public class ProductionAssociationsTrigger_Test {
    private static Account accountRecord;
    private static Opportunity productionRecord;
    private static Production_Associations__c productionAssociationRecord;
    static void generateData(){
        accountRecord = new Account(Name = 'Test', RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Airline_Vendor').getRecordTypeId());
        insert accountRecord;
        productionRecord = new Opportunity(Name = 'Test',CloseDate = system.today(), StageName = 'Closed Won', RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName().get('Live_Performance').getRecordTypeId(), AccountId = accountRecord.Id);
        insert productionRecord;
        productionAssociationRecord = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary Freight Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        insert productionAssociationRecord;
    }
    public static testMethod void insertTest(){
        generateData();
        Test.startTest();
        Production_Associations__c productionAssociation = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary GT Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        insert productionAssociation;
        Test.stopTest();
        system.assert([SELECT Id FROM Production_Associations__c].size() == 2);
    }
    public static testMethod void insertErrorTest(){
        generateData();
        Test.startTest();
        Production_Associations__c productionAssociation = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary Freight Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        try{
            insert productionAssociation;
        }catch(DMLException e){
            system.assert(e.getMessage().contains('It cannot have two primary coordinators.'));
        }        
        Test.stopTest();
    }
    public static testMethod void updateTest(){
        generateData();
        Test.startTest();
        Production_Associations__c productionAssociation = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary GT Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        insert productionAssociation;
        productionAssociation.Team_Roles__c = 'Primary GT Coordinator';
        update productionAssociation;
        Test.stopTest();
        system.assert([SELECT Id FROM Production_Associations__c].size() == 2);
    }
    public static testMethod void updateErrorTest(){
        generateData();
        Test.startTest();
        Production_Associations__c productionAssociation = new Production_Associations__c(User__c = UserInfo.getUserId(), Team_Roles__c = 'Primary GT Coordinator', Production_Opp__c = productionRecord.Id,RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName().get('Production_Coordinators').getRecordTypeId());
        insert productionAssociation;
        productionAssociation.Team_Roles__c = 'Primary Freight Coordinator';
        try{
            update productionAssociation;
        }catch(DMLException e){
            system.assert(e.getMessage().contains('It cannot have two primary coordinators.'));
        }  
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

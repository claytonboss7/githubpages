---
layout: default
title: ConcessionsTriggerHandler_Test
parent: classes
---
# Metadata Type
classes


# Filename 
ConcessionsTriggerHandler_Test


# Raw XML
```
@isTest
public class ConcessionsTriggerHandler_Test {
  @TestSetup
  static void generateData() {
    Account accountRecord = new Account(
      Name = 'Test',
      RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName()
        .get('Airline_Vendor')
        .getRecordTypeId()
    );
    insert accountRecord;

    Opportunity productionRecord = new Opportunity(
      Name = 'Test',
      CloseDate = system.today(),
      StageName = 'Closed Won',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      AccountId = accountRecord.Id
    );
    insert productionRecord;

    Housing__c housingRecord = new Housing__c(
      Production_CC__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Hotel_Housing')
        .getRecordTypeId(),
      Status_CC__c = 'Itinerary Received'
    );
    insert housingRecord;

    Bid__c bidRecordHousing = new Bid__c(
      Housing__c = housingRecord.Id,
      Production__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId()
    );
    insert bidRecordHousing;
  }

  @isTest
  public static void insertTest() {
    Test.startTest();
    Concessions__c concession = new Concessions__c(
      Bid__c = [SELECT Id FROM Bid__c LIMIT 1]
      .Id,
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Concession_Type__c = 'Corporate Housing',
      Concessions_Requested__c = 'Tax Terms & conditions:'
    );
    insert concession;
    Test.stopTest();

    Concessions__c[] theConcessions = [SELECT Id FROM Concessions__c];
    system.assertEquals(theConcessions.size(), 1);
  }

  @isTest
  public static void testUpdateConcessionCreationForSecondStay() {
    Test.startTest();
    Concessions__c concession = new Concessions__c(
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Concession_Type__c = 'Housing',
      Concessions_Requested__c = 'Tax Terms & conditions:'
    );
    insert concession;
    Test.stopTest();
    concession.Concession_Type__c = 'Housing';
    update concession;
  }
  public static testMethod void testDeleteConcessionRemoveFromStay() {
    Test.startTest();
    Concessions__c concession = new Concessions__c(
      Production__c = [SELECT Id FROM Opportunity LIMIT 1]
      .Id,
      Concession_Type__c = 'Housing',
      Concessions_Requested__c = 'Tax Terms & conditions:'
    );
    insert concession;
    Test.stopTest();

    delete concession;
    undelete concession;
  }
}
```


# Last Modified


# Usage

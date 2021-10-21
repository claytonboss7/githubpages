---
layout: default
title: TraceHelperTest
parent: classes
---
# Metadata Type
classes


# Filename 
TraceHelperTest


# Raw XML
```
/**
 * @description       :
 * @author            : claytonboss@roadrebel.com
 * @group             :
 * @last modified on  : 10-14-2021
 * @last modified by  : sfdc cb
 * Modifications Log
 * Ver   Date         Author                      Modification
 * 1.0   04-30-2021   claytonboss@roadrebel.com   Initial Version
 * 1.1   09-30-2021   claytonboss@roadrebel.com   Initial Version
 **/
@isTest
public with sharing class TraceHelperTest {
  /**
   * @description TestSetup method for Trace Specific Scenarios
   * @author claytonboss@roadrebel.com | 05-01-2021
   **/
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
      Office_Location__c = 'RRU',
      StageName = 'Closed Won',
      RecordTypeId = Schema.SObjectType.Opportunity.getRecordTypeInfosByDeveloperName()
        .get('Live_Performance')
        .getRecordTypeId(),
      AccountId = accountRecord.Id
    );
    insert productionRecord;

    Production_Associations__c prodAssoc = new Production_Associations__c(
      Production_Opp__c = productionRecord.Id,
      User__c = UserInfo.getUserId(),
      Team_Roles__c = 'Primary Contract Coordinator;Primary Housing Coordinator',
      RecordTypeId = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
        .get('Production_Coordinators')
        .getRecordTypeId()
    );

    insert prodAssoc;

    Housing__c housingRecord = new Housing__c(
      Production_CC__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Hotel_Housing')
        .getRecordTypeId(),
      Status_CC__c = 'Itinerary Received'
    );

    insert housingRecord;

    Housing__c housingRecordCorporate = new Housing__c(
      Production_CC__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Corporate_Housing')
        .getRecordTypeId()
    );

    insert housingRecordCorporate;

    Housing__c housingRecordIR = new Housing__c(
      Production_CC__c = productionRecord.Id,
      Status_CC__c = 'Itinerary Received',
      Trace_Date__c =  system.today(),
      RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
        .get('Individual_Reservation')
        .getRecordTypeId()
    );

    insert housingRecordIR;

    Bid__c bidRecordHotelHousing = new Bid__c(
      Housing__c = housingRecord.Id,
      Production__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId()
    );

    insert bidRecordHotelHousing;

    Bid__c bidRecordCorporateHousing = new Bid__c(
      Housing__c = housingRecordCorporate.Id,
      Production__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId()
    );

    insert bidRecordCorporateHousing;

    Bid__c bidRecordHousingIR = new Bid__c(
      Housing__c = housingRecordIR.Id,
      Production__c = productionRecord.Id,
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Housing_Bid').getRecordTypeId()
    );

    insert bidRecordHousingIR;
  }

  @isTest
  static void testCreateBidTracesHotelHousing() {
    Task[] theTraces = TraceHelper.createTracesContractBid(
      /**
       * this
       */
      new List<Bid__c>{
        [
          SELECT
            Id,
            Production__c,
            Contracting_Back_End_Coordinator__c,
            Housing_Record_Type__c,
            Housing__c,
            Housing__r.Production_CC__c,
            Housing__r.Name,
            Housing__r.Status_CC__C,
            Status__c
          FROM Bid__c WHERE Housing__r.RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId()
          LIMIT 1
        ]
      }
    );
    system.assertNotEquals(theTraces.size(), 0);
  }
  @isTest
  static void testCreateBidTracesCorporateHousing() {
    Task[] theTraces = TraceHelper.createTracesContractBid(
      /**
       * this
       */
      new List<Bid__c>{
        [
          SELECT
            Id,
            Production__c,
            Contracting_Back_End_Coordinator__c,
            Housing_Record_Type__c,
            Housing__c,
            Housing__r.Production_CC__c,
            Housing__r.Name,
            Housing__r.Status_CC__C,
            Status__c
          FROM Bid__c WHERE Housing__r.RecordTypeId = :Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Corporate_Housing')
          .getRecordTypeId()
          LIMIT 1
        ]
      }
    );
    system.assertNotEquals(theTraces.size(), 0);
  }
  @isTest
  static void testTracesDuplicateCheck() {
    Bid__c theBid = [
      SELECT
        Id,
        Production__c,
        Contracting_Back_End_Coordinator__c,
        Housing_Record_Type__c,
        Housing__c,
        Housing__r.Production_CC__c,
        Housing__r.Name,
        Housing__r.Status_CC__C,
        Status__c
      FROM Bid__c
      LIMIT 1
    ];

    //the traces are created for the first time
    Task[] theTraces = TraceHelper.createTracesContractBid(new List<Bid__c>{ theBid });
    system.assertNotEquals(theTraces.size(), 0);

    // do we have more than 25 traces?
    Map<String, Boolean> isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), false);

    // attempt the trace creation again, should not create duplicates
    Task[] theTraces2 = TraceHelper.createTracesContractBid(new List<Bid__c>{ theBid });
    isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), false);

    //now we will force 10 more tasks in so it is "duped"
    Task[] theTasks = new List<Task>();
    for (integer i = 0; i < 10; i++) {
      theTasks.add(
        new Task(Contract_Task__c = true, WhatId = theBid.Id, RecordTypeId = TraceHelper.getTraceTaskRecordType())
      );
    }
    insert theTasks;
    system.debug(theTasks);

    //here we know we have 22 Traces and 10 new dummy ones we just created, so we should be at 32, over duplicate threshhold of 25
    Integer theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), true);
    system.assertEquals(32, theTasksCount);
  }

  /**
   * @description verifies that the Bid_Has_Duplicate_Traces__c field is true when a dupe situation happens
   * @author claytonboss@roadrebel.com | 05-01-2021
   **/
  @isTest
  static void testTracesDuplicateCheckVerifyBidUpdate() {
    Bid__c theBid = [
      SELECT
        Id,
        Production__c,
        Contracting_Back_End_Coordinator__c,
        Housing_Record_Type__c,
        Housing__c,
        Housing__r.Production_CC__c,
        Housing__r.Name,
        Housing__r.Status_CC__C,
        Status__c
      FROM Bid__c
      LIMIT 1
    ];

    //the traces are created for the first time
    Task[] theTraces = TraceHelper.createTracesContractBid(new List<Bid__c>{ theBid });
    system.assertNotEquals(theTraces.size(), 0);

    // do we have more than 25 traces?
    Map<String, Boolean> isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), false);

    // attempt the trace creation again, should not create duplicates
    Task[] theTraces2 = TraceHelper.createTracesContractBid(new List<Bid__c>{ theBid });
    isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), false);

    //now we will force 10 more tasks in so it is "duped"
    Test.startTest();
    Task[] theTasks = new List<Task>();
    for (integer i = 0; i < 10; i++) {
      theTasks.add(
        new Task(
          Order__c = (i == 9 ? 22 : null),
          Contract_Task__c = true,
          WhatId = theBid.Id,
          RecordTypeId = TraceHelper.getTraceTaskRecordType()
        )
      );
    }
    insert theTasks;
    system.debug(theTasks);

    //here we know we have 22 Traces and 10 new dummy ones we just created, so we should be at 32, over duplicate threshhold of 25
    Integer theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), true);
    system.assertEquals(32, theTasksCount);

    Test.stopTest();

    Bid__c[] theBids = [SELECT Id FROM Bid__c WHERE Bid_Has_Duplicate_Traces__c = TRUE LIMIT 1];
    system.assertEquals(theBids.size(), 1);
  }

  /**
   * @description verifies that the Bid_Has_Duplicate_Traces__c field is true when a dupe situation happens
   * @author claytonboss@roadrebel.com | 05-01-2021
   **/
  @isTest
  static void testTracesDuplicateCheckVerifyBidUpdateNegative() {
    Bid__c theBid = [
      SELECT
        Id,
        Production__c,
        Contracting_Back_End_Coordinator__c,
        Housing_Record_Type__c,
        Housing__c,
        Housing__r.Production_CC__c,
        Housing__r.Name,
        Housing__r.Status_CC__C,
        Status__c
      FROM Bid__c
      LIMIT 1
    ];

    //the traces are created for the first time
    Task[] theTraces = TraceHelper.createTracesContractBid(new List<Bid__c>{ theBid });
    system.assertNotEquals(theTraces.size(), 0);

    // do we have more than 25 traces?
    Map<String, Boolean> isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), false);

    Bid__c[] theBids = [SELECT Id FROM Bid__c WHERE Bid_Has_Duplicate_Traces__c = TRUE LIMIT 1];
    system.assertEquals(theBids.size(), 0);

    // attempt the trace creation again, should not create duplicates
    Task[] theTraces2 = TraceHelper.createTracesContractBid(new List<Bid__c>{ theBid });
    isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), false);

    //now we will force 10 more tasks in so it is "duped"
    Test.startTest();
    Task[] theTasks = new List<Task>();
    for (integer i = 0; i < 10; i++) {
      theTasks.add(
        new Task(
          Order__c = (i == 9 ? 22 : null),
          Contract_Task__c = true,
          WhatId = theBid.Id,
          RecordTypeId = TraceHelper.getTraceTaskRecordType()
        )
      );
    }
    insert theTasks;
    system.debug(theTasks);

    //here we know we have 22 Traces and 10 new dummy ones we just created, so we should be at 32, over duplicate threshhold of 25
    Integer theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    isDuped = TraceHelper.traceHasDuplicates(new List<Bid__c>{ [SELECT Id FROM Bid__c LIMIT 1] });
    system.assertEquals(isDuped.get(theBid.Id), true);
    system.assertEquals(32, theTasksCount);

    Test.stopTest();

    theBids = [SELECT Id FROM Bid__c WHERE Bid_Has_Duplicate_Traces__c = TRUE LIMIT 1];
    system.assertEquals(theBids.size(), 1);
  }

  @isTest
  static void testCreateBidTracesOverload() {
    Task[] theTraces = TraceHelper.createTracesContractBid(
      [
        SELECT
          Id,
          Production__c,
          Contracting_Back_End_Coordinator__c,
          Housing_Record_Type__c,
          Housing__c,
          Housing__r.Production_CC__c,
          Housing__r.Name,
          Housing__r.Status_CC__C,
          Status__c
        FROM Bid__c
        LIMIT 1
      ],
      new Housing__c(Status_CC__c = 'Itinerary Received')
    );
    system.assertNotEquals(theTraces.size(), 0);
  }

  @isTest
  static void testCreateTraceHousingHotelHousing() {
    Bid__c theBid = [SELECT Id FROM Bid__c WHERE Housing__r.RecordType.DeveloperName = 'Hotel_Housing' LIMIT 1];
    // check to see if tasks exist yet for the bid, should be no
    Integer theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(0, theTasksCount);
    theBid.Status__c = 'In Contracting';
    theBid.Rate_Agreement_Last_Send_Date__c = system.today();

    update theBid;

    theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(22, theTasksCount);

    theBid.Status__c = 'Pending Client Signature';

    update theBid;

    theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(22, theTasksCount);
  }

  @isTest
  static void testCreateTraceHousingCorporateHousing() {
    Bid__c theBid = [SELECT Id FROM Bid__c WHERE Housing__r.RecordType.DeveloperName = 'Corporate_Housing' LIMIT 1];
    // check to see if tasks exist yet for the bid, should be no
    Integer theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(0, theTasksCount);
    theBid.Status__c = 'In Contracting';
    theBid.Rate_Agreement_Last_Send_Date__c = system.today();

    update theBid;

    theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(15, theTasksCount);
  }

  @isTest
  static void testCreateTraceHousingIR() {
    Bid__c theBid = [
      SELECT Id, Housing__r.Production_CC__c, Housing__c
      FROM Bid__c
      WHERE Housing__r.RecordType.DeveloperName = 'Individual_Reservation'
      LIMIT 1
    ];
    system.debug('theBid :::::::::::::: ' + theBid);
    // check to see if tasks exist yet for the bid, should be no
    Integer theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(0, theTasksCount);
    theBid.Status__c = 'In Contracting';
    theBid.Rate_Agreement_Last_Send_Date__c = system.today();
    update theBid;

    theTasksCount = [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id];
    system.assertEquals(7, theTasksCount);
  }

  @isTest
  static void getTypeByServiceTest() {
    String theGround = TraceHelper.getTypeByService(new Ground__c());
    String theFreight = TraceHelper.getTypeByService(new Freight__c());
    String theAir = TraceHelper.getTypeByService(new Air__c());
  }

  @isTest
  static void testEnumStringFormat() {
    String myEnumName = 'BLAH_BLAH';
    myEnumName = TraceHelper.enumToString(myEnumName);
    system.assertEquals(myEnumName, 'Blah Blah');
  }

  @isTest
  static void testEnumStringFormatList() {
    String[] myEnumNames = new List<String>{ 'BLAH_BLAH', 'BLAH2_BLAH2' };
    myEnumNames = TraceHelper.enumToString(myEnumNames);
    system.debug(myEnumNames);
    system.assertEquals(myEnumNames[0], 'Blah Blah');
  }

  @isTest
  static void testGetPrimaryHousingCoordinator() {
    // this should get the Primary Housing Coordinator from the PA Record

    Housing__c hou = [
      SELECT Id, Status_CC__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    String thePrimaryHousingCoordinator = TraceHelper.getCoordinatorServicePrimary(hou);

    system.assertEquals(thePrimaryHousingCoordinator, UserInfo.getUserId());
  }

  @isTest
  static void testGetStayBackendCoordinator() {
    // this should get the Primary Housing Coordinator from the PA Record

    Housing__c hou = [
      SELECT Id, Back_end_Coordinator__c, Production_CC__c, Status_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    hou.Back_End_Coordinator__c = UserInfo.getUserId();
    update hou;

    String thePrimaryHousingCoordinator = TraceHelper.getCoordinatorServiceBackend(hou);

    system.assertEquals(thePrimaryHousingCoordinator, UserInfo.getUserId());
  }

  @isTest
  static void testGetUltimateHousingCoordinator() {
    // this should get the "Ultimate" Primary Housing Coordinator from the PA Record and the housing record
    // by using the primary housing coordinator if a backend doesn't exist, otherwise use backend
    // backend is not set here so we would expect it to bring back userinfo.getuserid

    Housing__c hou = [
      SELECT Id, Back_end_Coordinator__c, Production_CC__c, Status_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    String theUltimateHousingCoordinator = TraceHelper.getCoordinatorService(hou);

    system.assertEquals(theUltimateHousingCoordinator, UserInfo.getUserId());
  }

  @isTest
  static void testGetUltimateHousingCoordinatorBackEndExists() {
    // this should get the "Ultimate" Primary Housing Coordinator from the PA Record and the housing record
    // by using the primary housing coordinator if a backend doesn't exist, otherwise use backend
    // backend is not set here so we would expect it to bring back userinfo.getuserid

    Housing__c hou = [
      SELECT Id, Back_end_Coordinator__c, Production_CC__c, Status_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    String sarahId = [SELECT Id FROM User WHERE Email LIKE '%sarah@roadrebel.com%' LIMIT 1]?.Id;
    system.debug('&&&&&&&&sarahId :: ' + sarahId);
    Test.startTest();
    hou.Back_End_Coordinator__c = sarahId;
    hou.Status_CC__c = 'Rework';
    update hou;
    Test.stopTest();

    system.debug('hou ::: ' + hou);

    String theUltimateHousingCoordinator = TraceHelper.getCoordinatorService(hou);

    system.assertEquals(theUltimateHousingCoordinator, sarahId);
  }

  @isTest
  static void testGetUltimateHousingContractCoordinator() {
    // this should get the "Ultimate" Primary Housing Coordinator from the PA Record and the housing record
    // by using the primary housing coordinator if a backend doesn't exist, otherwise use backend
    // backend is not set here so we would expect it to bring back userinfo.getuserid

    Housing__c hou = [
      SELECT Id, Back_end_Coordinator__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    String theUltimateHousingCoordinator = TraceHelper.getCoordinatorContracts(
      [
        SELECT
          Id,
          Production__c,
          Contracting_Back_End_Coordinator__c,
          Housing__c,
          Housing__r.Name,
          Housing__r.Production__c
        FROM Bid__c
        LIMIT 1
      ]
    );

    system.assertEquals(theUltimateHousingCoordinator, UserInfo.getUserId());
  }

  @isTest
  static void testGetCoordinatorContractsBackendExists() {
    // this should get the "Ultimate" Primary Housing Coordinator from the PA Record and the housing record
    // by using the primary housing coordinator if a backend doesn't exist, otherwise use backend
    // backend is not set here so we would expect it to bring back userinfo.getuserid

    Housing__c hou = [
      SELECT Id, Back_end_Coordinator__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    Bid__c theBid = [
      SELECT
        Id,
        Housing__c,
        Housing__r.Name,
        Housing__r.Status_CC__c,
        Housing__r.Production_CC__c,
        Contracting_Back_End_Coordinator__c,
        Production__c
      FROM Bid__c
      WHERE Housing__c = :hou.Id
    ];

    String theUltimateHousingCoordinator = TraceHelper.getCoordinatorContracts(theBid);

    system.assertEquals(theUltimateHousingCoordinator, UserInfo.getUserId());
  }

  @isTest
  static void testCoordinatorBackendReAssign() {
    // this should get the "Ultimate" Primary Housing Coordinator from the PA Record and the housing record
    // by using the primary housing coordinator if a backend doesn't exist, otherwise use backend
    // backend is not set here so we would expect it to bring back userinfo.getuserid

    Housing__c hou = [
      SELECT Id, Back_end_Coordinator__c, Production_CC__c
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
    ];

    Bid__c theBid = [
      SELECT
        Id,
        Housing__c,
        Housing__r.Name,
        Housing__r.Status_CC__c,
        Housing__r.Production_CC__c,
        Contracting_Back_End_Coordinator__c,
        Production__c
      FROM Bid__c
      WHERE Housing__c = :hou.Id
    ];

    theBid.Contracting_Back_End_Coordinator__c = UserInfo.getUserId();
    update theBid;

    theBid.Contracting_Back_End_Coordinator__c = [SELECT Id FROM User WHERE isActive = TRUE LIMIT 1].Id;
    update theBid;

    theBid.Contracting_Back_End_Coordinator__c = null;
    update theBid;
  }

  @isTest
  static void testLoadHousingTraces() {
    Set<string> theTraces = TraceHelper.getTracesHotelHousing();
    system.assertNotEquals(theTraces.size(), 0);
  }

  @isTest
  static void testLoadBidTraces() {
    Set<String> theTraces = TraceHelper.getTracesContractsBidAll();
    system.assertNotEquals(theTraces.size(), 0);
  }

  @isTest
  static void testLoadCoordinatorPicklistTraceDashboard() {
    List<SelectOption> theCoordinators = TraceHelper.getCoordinatorOptionsValues();
    system.assertNotEquals(theCoordinators.size(), 0);

    Map<Id, User> theUsers = TraceHelper.coordinatorListUsers;
    system.assertNotEquals(theCoordinators.size(), 0);
  }

  @isTest
  static void testHousingTraceStatusChange() {
    String recordTypeHotelHousing = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Hotel_Housing')
      .getRecordTypeId();
    Housing__c theHousing = [
      SELECT Id, Status_CC__c, Trace_Date__c, DeadLine_Date__c, Production_CC__c, Back_End_Coordinator__c
      FROM Housing__c
      WHERE RecordTypeId = :recordTypeHotelHousing
      LIMIT 1
    ];
    //theHousing.Back_End_Coordinator__c = [SELECT Id FROM User WHERE Name LIKE '%sarah@roadrebel.com%'];
    // TraceHelper.createServiceStatusTrace(theHousing, 'Housing__c');
    Task[] theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c, RecordType.Name
      FROM Task
      WHERE WhatId = :theHousing.Id
    ];

    system.debug(JSON.serializePretty(theTasks));

    theHousing.Status_CC__c = 'Bid Request Stage';
    Test.startTest();
    update theHousing;
    Test.stopTest();

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE WhatId = :theHousing.Id
    ];
    system.debug(JSON.serializePretty(theTasks));

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE Subject = 'Bid Request Stage' AND Status = 'Open' AND WhatId = :theHousing.Id
    ];

    system.assertEquals(theTasks.size(), 1);

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE Subject = 'Itinerary Received' AND Status = 'Open' AND WhatId = :theHousing.Id
    ];

    system.assertEquals(theTasks.size(), 0);

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE Subject = 'Itinerary Received' AND Status = 'Completed' AND WhatId = :theHousing.Id
    ];

    system.assertEquals(theTasks.size(), 1);

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE Subject = 'Bid Request Stage' AND Status = 'Completed' AND WhatId = :theHousing.Id
    ];

    system.assertEquals(theTasks.size(), 0);
    // we need to make sure that when we assign the backend our most recent trace (singular) stay open,
    // the others should complete and reasssign the task owner

    //TraceHelper.traceReassignWhenBackendSelected(theServices, theStatus, theCoordinator)
  }


  @isTest
  static void testHousingTraceStatusChangeIndividualReservation() {
    String recordTypeIR = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Individual_Reservation')
      .getRecordTypeId();


      String janaId = [SELECT Id FROM User WHERE Name = 'Jana Leighty' ORDER BY CreatedDate ASC LIMIT 1].Id;

    Housing__c theHousing = [
      SELECT Id, Status_CC__c, Trace_Date__c, DeadLine_Date__c, Production_CC__c, Back_End_Coordinator__c
      FROM Housing__c
      WHERE RecordTypeId = :recordTypeIR
      LIMIT 1
    ];

    Housing__c[] existingHousings = [SELECT Id FROM Housing__c WHERE RecordTypeID = :recordTypeIR];
    system.assertNotEquals(existingHousings.size(),0);
    //theHousing.Back_End_Coordinator__c = [SELECT Id FROM User WHERE Name LIKE '%sarah@roadrebel.com%'];
    // TraceHelper.createServiceStatusTrace(theHousing, 'Housing__c');
    Integer theCounBidRequestStage = [SELECT Count() FROM Task WHERE WhatId = :theHousing.Id AND Subject = 'Bid Request Stage'];
    system.assertEquals(theCounBidRequestStage,0);

    Task[] theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c, RecordType.Name
      FROM Task
      WHERE WhatId = :theHousing.Id
    ];

    system.debug(JSON.serializePretty(theTasks));

    theHousing.Trace_Date__c = system.today();
    theHousing.Status_CC__c = 'Bid Request Stage';
    Test.startTest();
    update theHousing;
    Test.stopTest();

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c,ActivityDate
      FROM Task
      WHERE Subject = 'Bid Request Stage' AND Status = 'Open' AND WhatId = :theHousing.Id AND OwnerId = :UserInfo.getUserId()
    ];

    system.assertEquals(theTasks.size(), 1);

    system.assertNotEquals(theTasks[0].ActivityDate, null);
    // we need to make sure that when we assign the backend our most recent trace (singular) stay open,
    // the others should complete and reasssign the task owner

    //TraceHelper.traceReassignWhenBackendSelected(theServices, theStatus, theCoordinator)

    theHousing.Back_end_Coordinator__c = janaId;
    update theHousing;

    Task[] theTasksUpdated = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c,ActivityDate
      FROM Task
      WHERE Subject = 'Bid Request Stage' AND Status = 'Open' AND WhatId = :theHousing.Id AND OwnerId = :janaId
    ];
    //system.assertEquals(theTasksUpdated.size(), 1);


  }


  @isTest
  static void testHousingBackendCoordinatorAddition() {
    // this should be i
    string sarahId = [SELECT Id FROM User WHERE Email LIKE '%sarah@roadrebel.com%' LIMIT 1].Id;

    Housing__c theHousing = [
      SELECT Id, Status_CC__c, Trace_Date__c, DeadLine_Date__c, Production_CC__c, Back_End_Coordinator__c
      FROM Housing__c
      LIMIT 1
    ];

    Task[] theTasks = [
      SELECT Id, OwnerId, What.Name, What.Type, Owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE WhatId = :theHousing.Id
    ];

    system.assertEquals(theTasks.size(), 1);

    /* Milestone 1 
        - We should have 1 tasks for our Housing that was created with TraceDate specified (itinerary receieved)
        - t
        */

    theHousing.Status_CC__c = 'Bid Request Stage';
    update theHousing;

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE Subject = 'Bid Request Stage' AND Status = 'Open' AND WhatId = :theHousing.Id
    ];

    system.assertEquals(theTasks.size(), 1);

    theHousing.Back_End_Coordinator__c = sarahId;
    update theHousing;

    theTasks = [
      SELECT Id, OwnerId, what.name, what.type, owner.Name, Status, Priority, Subject, Task_Type__c
      FROM Task
      WHERE Subject = 'Bid Request Stage' AND Status = 'Completed' AND WhatId = :theHousing.Id AND OwnerId = :sarahId
    ];

    system.assertEquals(theTasks.size(), 0);
  }
  @isTest
  static void testGetUltimateServiceContractingCoordinator() {
    // this should be i
   TraceHelper.getUltimateServiceContractingCoordinator([SELECT Id,Back_End_Coordinator__c,Production_CC__c FROM Housing__c], [SELECT Production__c,Housing__r.Back_End_Coordinator__c,Housing__c,Contracting_Back_End_Coordinator__c,Id,Name FROM Bid__c]);
  }

  @isTest
  static void testGetCoordinatorOptionsValuesListAll() {
    // this should be i
   String[] theUsers = TraceHelper.GetCoordinatorOptionsValuesListAll();
   system.assertNotEquals(theUsers.size(),0);
  }
  
}
```


# Last Modified


# Usage

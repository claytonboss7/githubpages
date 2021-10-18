---
layout: default
title: CongaSignTransactionTriggerHandler_Test
parent: classes
---

```/**
 * @description       : trace automation related to Conga Sign and the SENT or COMPLETE status it writes when sending a conga doc for signature
 * @author            : clay b
 * @group             :
 * @last modified on  : 05-04-2021
 * @last modified by  : clay b
 * Modifications Log
 * Ver   Date         Author   Modification
 * 1.0   05-04-2021   clay b   Initial Version
 **/

@isTest
public class CongaSignTransactionTriggerHandler_Test {
  /**
   * @description test setup method that uses the RR Data Factory for a standard housing setup with Hotel Housing
   * @author clay b | 05-04-2021
   **/
  @TestSetup
  static void makeData() {
    RoadRebelDataFactory.createHousingSetup();
  }

  /**
   * @description asserts the *Final Status* of the *Bid* is *Pending Client Signature* same with *Status_CC* on *Housing*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsContractToClient() {
    Task[] theTasks = [SELECT Id FROM Task];
    //delete theTasks;
    Test.startTest();

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Contract To Client',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    Bid__c theBid = [SELECT Id FROM Bid__c];
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = theBid.Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;
	
    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;

    Bid__c[] theBids = [
      SELECT Id, Rate_Agreement_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    update new Bid__c(Id = theBid.Id, Housing_Contract_Last_Send_Date__c = system.today() + 3);

    system.debug('theCount' + [SELECT COUNT() FROM Task WHERE WhatId = :theBid.Id]);

    system.assertEquals(theBids[0].Final_Status__c, 'Pending Client Signature');
    system.assertEquals(theBids[0].Housing__r.Status_CC__c, 'Pending Client Signature');

    Test.stopTest();
  }

  /**
   * @description asserts the functionality of the "SENT" status for stamping the *Rate Agreement Last Send Date*
   * * also worth noting that the trigger for traces is Rate Agreement Last Send Date or Housing Contract Last Send Date
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsRateAgreement() {
    // tests the Rate Agreement Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Rate Agreement',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
      Bid__c[] theBids = [
      SELECT Id, Rate_Agreement_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertNotEquals(theBids[0].Rate_Agreement_Last_Send_Date__c, null);

    Test.stopTest();

    Task[] theTasks = [SELECT Id FROM Task];
    system.debug('thetasks ::: ' + thetasks.size());

    //TODO ASSERT
  }

  /**
   * @description asserts the functionality of the "SENT" status for stamping the *Housing Contract Last Send Date*
   * * also worth noting that the trigger for traces is Rate Agreement Last Send Date or Housing Contract Last Send Date
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsHousingContract() {
    Test.startTest();

    Bid__c[] theBids = [
      SELECT Id, Housing_Contract_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertEquals(theBids[0].Housing_Contract_Last_Send_Date__c, null);

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Housing Contract',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
	theBids = [
      SELECT Id, Housing_Contract_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertNotEquals(theBids[0].Housing_Contract_Last_Send_Date__c, null);

    Test.stopTest();
  }

  /**
   * @description - asserts the datestamp for *Trip Details Update Last Send Date*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsTripDetailsUpdate() {
    // tests the Rate Agreement Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    Bid__c[] theBids = [
      SELECT Id, Trip_Details_Update_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertEquals(theBids[0].Trip_Details_Update_Last_Send_Date__c, null);

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Trip Details Update',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
	theBids = [
      SELECT Id, Trip_Details_Update_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertNotEquals(theBids[0].Trip_Details_Update_Last_Send_Date__c, null);

    Test.stopTest();
  }

  /**
   * @description asserts the functionality of the "SENT" status for stamping the *Transportation Contract Last Send Date*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsTransportationContract() {
    // tests the Rate Agreement Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    Bid__c[] theBids = [
      SELECT Id, Transportation_Contract_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertEquals(theBids[0].Transportation_Contract_Last_Send_Date__c, null);

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Transportation Contract',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
	theBids = [
      SELECT Id, Transportation_Contract_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertNotEquals(theBids[0].Transportation_Contract_Last_Send_Date__c, null);

    Test.stopTest();
  }

  /**
   * @description asserts the functionality of the "SENT" status for stamping the *Counter Needed Last Send Date*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsCounterNeeded() {
    Test.startTest();

    Bid__c[] theBids = [
      SELECT Id, Counter_Needed_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertEquals(theBids[0].Counter_Needed_Last_Send_Date__c, null);

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'ContractClientSigned - Counter Needed',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
	theBids = [
      SELECT Id, Counter_Needed_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertNotEquals(theBids[0].Counter_Needed_Last_Send_Date__c, null);

    Test.stopTest();
  }

  /**
   * @description asserts the functionality of the "SENT" status for stamping the *Final Contract Last Send Date*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsFinalContract() {
    Test.startTest();

    Bid__c[] theBids = [
      SELECT Id, Final_Contract_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertEquals(theBids[0].Final_Contract_Last_Send_Date__c, null);

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Final Contract',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
	theBids = [
      SELECT Id, Final_Contract_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertNotEquals(theBids[0].Final_Contract_Last_Send_Date__c, null);

    Test.stopTest();
  }

  /**
   * @description asserts the functionality of the "SENT" status for stamping the *Pick Up Report Last Send Date*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateSentDocumentsPickUpReport() {
    // tests the Rate Agreement Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    Bid__c[] theBids = [
      SELECT Id, Pick_Up_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];

    system.assertEquals(theBids[0].Pick_Up_Last_Send_Date__c, null);

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'PickUp Report',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    insert trans;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
	theBids = [SELECT Id, Pick_Up_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c FROM Bid__c LIMIT 1];

    system.assertNotEquals(theBids[0].Pick_Up_Last_Send_Date__c, null);

    Test.stopTest();
  }

  /**
   * @description asserts the functionality of the "COMPLETE" status for Completing the trace for *Pending Client Signature*
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateCompleteDocumentsContractToClient() {
    // tests the Contract to Client Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Contract To Client',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;
	
    Bid__c[] theBids = [
      SELECT Id, Rate_Agreement_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];
    update new Bid__c(Id = theBids[0].Id, Housing_Contract_Last_Send_Date__c = system.today() + 3);

    insert trans;
	
    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;
	
    List<Task> taskList = new List<Task>();
    for (Task taskRec : [SELECT Id, Subject, Status, ActivityDate FROM Task where Subject = 'Pending Client Signature' 
                         AND WhatId =: theBids[0].Id]) {
        taskRec.ActivityDate = system.today();
        taskList.add(taskRec);
    }
    update taskList;
        
    trans.APXT_CongaSign__Status__c = 'COMPLETE';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    Test.stopTest();

    for (Task t : [SELECT Id, ActivityDate, Status, Subject FROM Task WHERE Contract_Task__c = TRUE]) {
      if (t.Subject == 'Pending Client Signature') {
        system.assertEquals(t.ActivityDate, null);
        system.assertEquals(t.Status, 'Completed');
      }
    }
  }

  /**
   * @description asserts the functionality of the "COMPLETE" status at Rate Agreement and following trace automations:
   * Awaiting Pickup Report - 1 biz day after a week from today, Open trace
   * Pending Contract - Completes this trace, date blank
   * Need to Send to Client - 1 biz day after today, open trace
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateCompleteDocumentsRateAgreement() {
    // tests the Rate Agreement Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Rate Agreement',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    Bid__c[] theBids = [
      SELECT Id, Rate_Agreement_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];
    update new Bid__c(Id = theBids[0].Id, Housing_Contract_Last_Send_Date__c = system.today() + 3);

    insert trans;

    trans.APXT_CongaSign__Status__c = 'SENT';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;
	
    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
    for (Task t : [SELECT Id, Subject, Status, ActivityDate FROM Task])
      system.debug('t ::::::: ' + t);

    trans.APXT_CongaSign__Status__c = 'COMPLETE';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;

    Test.stopTest();
    for (Task t : [SELECT Id, Subject, Status, ActivityDate FROM Task])
      system.debug('t ::::::: ' + t);

    Task[] theTasks = [
      SELECT Id, Subject, Status, ActivityDate
      FROM Task
      WHERE Subject = 'Need to Send to Client'
      LIMIT 1
    ];
    //system.assertEquals(theTasks[0].ActivityDate, ApexUtil.AddBusinessDays(Date.Today(), 1));
    system.assertNotEquals(null, theTasks[0].ActivityDate);
    system.assertEquals(theTasks[0].Status, 'Open');

    /*

    theTasks = [SELECT Id, Subject, Status, ActivityDate FROM Task WHERE Subject = 'Pending Client Signature' LIMIT 1];
    system.assertEquals(theTasks[0].ActivityDate, null);
    system.assertEquals(theTasks[0].Status, 'Completed');

    /*
    theTasks = [SELECT Id, Subject, Status, ActivityDate FROM Task WHERE Subject = 'Pending Rate Agreement' LIMIT 1];
    system.assertEquals(theTasks[0].ActivityDate, null);
    system.assertEquals(theTasks[0].Status, 'Completed');
    */
    theTasks = [SELECT Id, Subject, Status, ActivityDate FROM Task WHERE Subject = 'Pending Contract' LIMIT 1];
    system.assertEquals(theTasks[0].ActivityDate, null);
    system.assertEquals(theTasks[0].Status, 'Completed');
	
    /**
    theTasks = [SELECT Id, Subject, Status, ActivityDate FROM Task WHERE Subject = 'Awaiting Pick-Up' LIMIT 1];
    system.assertEquals(theTasks[0].ActivityDate, (ApexUtil.AddBusinessDays(Date.Today() + 7, 1)));
    system.assertEquals(theTasks[0].Status, 'Open');
	**/
    //
  }

  /**
   * @description asserts the functionality of the "COMPLETE" status at Housing Contract for the following trace automations:
   * Pending Contract - Completes this trace, date blank
   * Need to Send to Client - 1 biz day after today, open trace
   * @author clay b | 05-04-2021
   **/
  @isTest
  static void testAfterUpdateCompleteDocumentsHousingContract() {
    // tests the Rate Agreement Document being sent and the bid status update, housing update, and datestamp it causes
    Test.startTest();

    CongaSignTransactionTriggerHandler handler = new CongaSignTransactionTriggerHandler();
    APXT_CongaSign__Transaction__c trans = new APXT_CongaSign__Transaction__c();

    ContentVersion contentVersionInsert = new ContentVersion(
      Title = 'Housing Contract',
      PathOnClient = 'Test.jpg',
      VersionData = Blob.valueOf('Test Content Data'),
      IsMajorVersion = true
    );
    insert contentVersionInsert;

    Bid__c[] theBids = [
      SELECT Id, Rate_Agreement_Last_Send_Date__c, Housing__r.Status_CC__c, Final_Status__c
      FROM Bid__c
      LIMIT 1
    ];
    update new Bid__c(Id = theBids[0].Id, Housing_Contract_Last_Send_Date__c = system.today() + 3);

    insert trans;

    APXT_CongaSign__Document__c congaDoc = new APXT_CongaSign__Document__c();
	congaDoc.APXT_CongaSign__Transaction__c = trans.Id;
	congaDoc.APXT_CongaSign__ContentDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__ContentVersionId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
	congaDoc.APXT_CongaSign__Type__c = 'Original';
	insert congaDoc;
	
    for (Task t : [SELECT Id, Subject, Status, ActivityDate FROM Task])
      system.debug('t ::::::: ' + t);

    trans.APXT_CongaSign__Status__c = 'COMPLETE';
    trans.Parent_a0D__c = [SELECT Id FROM Bid__c].Id;
    trans.APXT_CongaSign__OriginalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;
    trans.APXT_CongaSign__FinalDocumentId__c = [SELECT Id FROM ContentDocument LIMIT 1].Id;

    update trans;
    
	
    Test.stopTest();
    for (Task t : [SELECT Id, Subject, Status, ActivityDate FROM Task])
      system.debug('t ::::::: ' + t);

    Task[] theTasks = [
      SELECT Id, Subject, Status, ActivityDate
      FROM Task
      WHERE Subject = 'Need to Send to Client'
      LIMIT 1
    ];
    system.assertEquals(theTasks[0].ActivityDate, ApexUtil.AddBusinessDays(Date.Today(), 1));
    system.assertEquals(theTasks[0].Status, 'Open');

    theTasks = [SELECT Id, Subject, Status, ActivityDate FROM Task WHERE Subject = 'Pending Contract' LIMIT 1];
    system.assertEquals(theTasks[0].ActivityDate, null);
    system.assertEquals(theTasks[0].Status, 'Completed');
  }
}```

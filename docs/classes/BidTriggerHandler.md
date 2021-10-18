---
layout: default
title: BidTriggerHandler
parent: classes
---

```public without sharing class BidTriggerHandler implements ITriggerHandler {
  public static Boolean TriggerDisabled = false;
  public static Boolean createdTraces = false;

  public Boolean IsDisabled() {
    return ApexUtil.BidTrigger_Is_Enabled == true ? false : true;
  }

  public void BeforeInsert(List<SObject> newItems) {
    Bid__c[] theBids = (Bid__c[]) newItems;
    assignUUIDs(theBids);
  }

  public void BeforeUpdate(Map<Id, SObject> newItems, Map<Id, SObject> oldItems) {
    Map<Id, Bid__c> bidsMap = (Map<Id, Bid__c>) newItems;
    Map<Id, Bid__c> oldBidsMap = (Map<Id, Bid__c>) oldItems;
    populateCongaFields(oldBidsMap, bidsMap);
  }

  public void BeforeDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterInsert(Map<Id, SObject> newItems) {
    Map<Id, Bid__c> bidsMap = (Map<Id, Bid__c>) newItems;
    doVendorBidCounts(null, bidsMap);
  }

  public void AfterUpdate(Map<Id, SObject> newItems, Map<Id, SObject> oldItems) {
    Map<Id, Bid__c> bidsMap = (Map<Id, Bid__c>) newItems;
    Map<Id, Bid__c> oldBidsMap = (Map<Id, Bid__c>) oldItems;
    Set<String> theTraceFields = new Set<String>{
      'Rate_Agreement_Last_Send_Date__c',
      'Housing_Contract_Last_Send_Date__c'
    };
    doVendorBidCounts(oldBidsMap, bidsMap);
    ///if (createdTraces == false)
      generateBidTraces(oldBidsMap, bidsMap);
    createdTraces = true;
    updateCongaBidTraces(oldBidsMap, bidsMap);
    createJournalEntries(oldBidsMap, bidsMap);
    verifySabreRate(oldBidsMap, bidsMap);
    verifyNoBidReason(oldBidsMap, bidsMap);
    TraceHelper.updateTracesBackendReassignedContracts(oldBidsMap, bidsMap);
  }

  public void AfterDelete(Map<Id, SObject> oldItems) {
    Map<Id, Bid__c> oldBidsMap = (Map<Id, Bid__c>) oldItems;
    doVendorBidCounts(null, oldBidsMap);
  }

  public void AfterUndelete(Map<Id, SObject> oldItems) {
  }

  public static void doVendorBidCounts(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    Map<String, Integer> bidCountVendorMap = new Map<String, Integer>();
    Map<String, Integer> bidCountVendorContractedMap = new Map<String, Integer>();
    Set<Id> housingIds = new Set<Id>();
    Set<Id> vendorIds = new Set<Id>();
    if (Trigger.isInsert) {
      for (Bid__c b : bidsMap.values()) {
        if (b.Housing__c != null)
          housingIds.add(b.Housing__c);
        if (b.Vendor__c != null)
          vendorIds.add(b.Vendor__c);
      }
    } else if (Trigger.isUpdate) {
      for (Bid__c b : bidsMap.values()) {
        if (b.Housing__c != null)
          housingIds.add(b.Housing__c);
        if (oldBidsMap.get(b.Id).Housing__c != null)
          housingIds.add(oldBidsMap.get(b.Id).Housing__c);
        if (b.Vendor__c != null)
          vendorIds.add(b.Vendor__c);
        if (oldBidsMap.get(b.Id).Vendor__c != null)
          vendorIds.add(oldBidsMap.get(b.Id).Vendor__c);
      }
    } else if (Trigger.isDelete) {
      for (Bid__c b : bidsMap.values()) {
        if (b.Housing__c != null)
          housingIds.add(b.Housing__c);
        if (b.Vendor__c != null)
          vendorIds.add(b.Vendor__c);
      }
    }
    if (housingIds.size() > 0) {
      Map<String, Integer> bidCountMap = new Map<String, Integer>();
      for (Bid__c b : [SELECT Id, Housing__c FROM Bid__c WHERE Housing__c IN :housingIds]) {
        if (bidCountMap.get(b.Housing__c) != null) {
          bidCountMap.put(b.Housing__c, bidCountMap.get(b.Housing__c) + 1);
        } else {
          bidCountMap.put(b.Housing__c, 1);
        }
      }

      List<Housing__c> housingList = new List<Housing__c>();
      Housing__c h;
      for (String s : bidCountMap.keySet()) {
        h = new Housing__c(Id = s, No_of_bids__c = bidCountMap.get(s));
        housingList.add(h);
      }

      if (housingList.size() > 0)
        update housingList;
    }
    if (vendorIds.size() > 0) {
      for (Bid__c b : [SELECT Id, Vendor__c, Status__c FROM Bid__c WHERE Vendor__c IN :vendorIds]) {
        bidCountVendorMap.put(
          b.Vendor__c,
          bidCountVendorMap.get(b.Vendor__c) != null ? bidCountVendorMap.get(b.Vendor__c) + 1 : 1
        );
        if (b.Status__c == 'Contracted')
          bidCountVendorContractedMap.put(
            b.Vendor__c,
            bidCountVendorContractedMap.get(b.Vendor__c) != null ? bidCountVendorContractedMap.get(b.Vendor__c) + 1 : 1
          );
      }
    }

    List<Account> accountList = new List<Account>();
    Account acc;
    for (String s : bidCountVendorMap.keySet()) {
      acc = new Account(Id = s, bids__c = (bidCountVendorMap.get(s) != null ? bidCountVendorMap.get(s) : 0));
      accountList.add(acc);
    }

    List<Account> accountContractList = new List<Account>();
    for (String s : bidCountVendorContractedMap.keySet()) {
      acc = new Account(
        Id = s,
        of_contracted_bids__c = (bidCountVendorContractedMap.get(s) != null ? bidCountVendorContractedMap.get(s) : 0)
      );
      accountContractList.add(acc);
    }

    if (accountList.size() > 0)
      update accountList;
    if (accountContractList.size() > 0)
      update accountContractList;
  }

  public static void populateCongaFields(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    for (Bid__c bid : bidsMap.values()) {
      if (bid.Options__c == 0)
        bid.Options__c = null;
      if (bid.Options__c != null)
        bid.Include_in_options__c = true;
      if (bid.Housing__c != null)
        bid.Cover__c = bid.Include_in_option_cover_sheet__c;
      if (
        bid.Conga_Update_Fields__c != null &&
        bid.Conga_Update_Fields__c != oldBidsMap.get(bid.Id).Conga_Update_Fields__c
      ) {
        Map<String, Object> congaUpdateFieldsMap = (Map<String, Object>) JSON.deserializeUntyped(
          bid.Conga_Update_Fields__c.replace('\'', '"')
        );
        if (congaUpdateFieldsMap.containsKey('Status__c'))
          bid.Status__c = (String) congaUpdateFieldsMap.get('Status__c');
        if (congaUpdateFieldsMap.containsKey('Vendor_Contact__c'))
          bid.Vendor_Contact__c = (String) congaUpdateFieldsMap.get('Vendor_Contact__c');
        bid.Conga_Update_Fields__c = null;
      }
      if (
        bid.Rate_Agreement_Last_Send_Date__c != null &&
        bid.Rate_Agreement_Last_Send_Date__c != oldBidsMap.get(bid.Id).Rate_Agreement_Last_Send_Date__c
      )
        bid.Rate_Agreement_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Housing_Contract_Last_Send_Date__c != null &&
        bid.Housing_Contract_Last_Send_Date__c != oldBidsMap.get(bid.Id).Housing_Contract_Last_Send_Date__c
      )
        bid.Housing_Contract_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Trip_Details_Update_Last_Send_Date__c != null &&
        bid.Trip_Details_Update_Last_Send_Date__c != oldBidsMap.get(bid.Id).Trip_Details_Update_Last_Send_Date__c
      )
        bid.Trip_Details_Update_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Transportation_Contract_Last_Send_Date__c != null &&
        bid.Transportation_Contract_Last_Send_Date__c !=
        oldBidsMap.get(bid.Id).Transportation_Contract_Last_Send_Date__c
      )
        bid.Transportation_Contract_Last_Send_By__c = UserInfo.getName();
      if (
        bid.GCIP_Last_Send_Date__c != null &&
        bid.GCIP_Last_Send_Date__c != oldBidsMap.get(bid.Id).GCIP_Last_Send_Date__c
      )
        bid.GCIP_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Contract_Date_Change_Last_Send_Date__c != null &&
        bid.Contract_Date_Change_Last_Send_Date__c != oldBidsMap.get(bid.Id).Contract_Date_Change_Last_Send_Date__c
      )
        bid.Contract_Date_Change_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Contract_to_Client_Last_Send_Date__c != null &&
        bid.Contract_to_Client_Last_Send_Date__c != oldBidsMap.get(bid.Id).Contract_to_Client_Last_Send_Date__c
      )
        bid.Contract_to_Client_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Room_Changes_Last_Send_Date__c != null &&
        bid.Room_Changes_Last_Send_Date__c != oldBidsMap.get(bid.Id).Room_Changes_Last_Send_Date__c
      )
        bid.Room_Changes_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Counter_Needed_Last_Send_Date__c != null &&
        bid.Counter_Needed_Last_Send_Date__c != oldBidsMap.get(bid.Id).Counter_Needed_Last_Send_Date__c
      )
        bid.Counter_Needed_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Final_Contract_Last_Send_Date__c != null &&
        bid.Final_Contract_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Contract_Last_Send_Date__c
      ) {
        if (
          Schema.SObjectType.Bid__c.getRecordTypeInfosByName().get('Housing_Bid') != null &&
          bid.recordtypeId.equals(
            Schema.SObjectType.Bid__c.getRecordTypeInfosByName().get('Housing_Bid').getRecordTypeId()
          )
        ) {
          //bid.Final_Status__c = 'Contracted';
          system.debug('wrote final status on bid');
        } else if (
          Schema.SObjectType.Bid__c.getRecordTypeInfosByName().get('GT_Bid') != null &&
          bid.recordtypeId.equals(Schema.SObjectType.Bid__c.getRecordTypeInfosByName().get('GT_Bid').getRecordTypeId())
        )
          system.debug('wrote final status on bid');
        //bid.Final_Status__c = 'Contracted';
        bid.Final_Contract_Last_Send_By__c = UserInfo.getName();
      }
      if (
        bid.Email_Confirmation_Last_Send_Date__c != null &&
        bid.Email_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Email_Confirmation_Last_Send_Date__c
      )
        bid.Email_Confirmation_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Credit_Card_Last_Send_Date__c != null &&
        bid.Credit_Card_Last_Send_Date__c != oldBidsMap.get(bid.Id).Credit_Card_Last_Send_Date__c
      )
        bid.Credit_Card_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Cancellation_Last_Send_Date__c != null &&
        bid.Cancellation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Cancellation_Last_Send_Date__c
      )
        bid.Cancellation_Last_Send_By__c = UserInfo.getName();
      if (
        bid.No_Pick_Up_Last_Send_Date__c != null &&
        bid.No_Pick_Up_Last_Send_Date__c != oldBidsMap.get(bid.Id).No_Pick_Up_Last_Send_Date__c
      )
        bid.No_Pick_Up_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Pick_Up_Last_Send_Date__c != null &&
        bid.Pick_Up_Last_Send_Date__c != oldBidsMap.get(bid.Id).Pick_Up_Last_Send_Date__c
      ) {
        bid.Pick_Up_Last_Send_By__c = UserInfo.getName();
        bid.isHousingCloseOutAvailable__c = bid.isHousingCloseOutEditable__c = true;
      }
      if (
        bid.Rooming_List_Last_Send_Date__c != null &&
        bid.Rooming_List_Last_Send_Date__c != oldBidsMap.get(bid.Id).Rooming_List_Last_Send_Date__c
      )
        bid.Rooming_List_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Deposit_Due_Last_Send_Date__c != null &&
        bid.Deposit_Due_Last_Send_Date__c != oldBidsMap.get(bid.Id).Deposit_Due_Last_Send_Date__c
      )
        bid.Deposit_Due_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Utilization_Last_Send_Date__c != null &&
        bid.Utilization_Last_Send_Date__c != oldBidsMap.get(bid.Id).Utilization_Last_Send_Date__c
      )
        bid.Utilization_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Names_Final_Payment_Last_Send_Date__c != null &&
        bid.Names_Final_Payment_Last_Send_Date__c != oldBidsMap.get(bid.Id).Names_Final_Payment_Last_Send_Date__c
      )
        bid.Names_Final_Payment_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Final_Choice_Last_Send_Date__c != null &&
        bid.Final_Choice_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Choice_Last_Send_Date__c
      )
        bid.Final_Choice_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Ticketed_Confirmation_Last_Send_Date__c != null &&
        bid.Ticketed_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Ticketed_Confirmation_Last_Send_Date__c
      )
        bid.Ticketed_Confirmation_Last_Send_By__c = UserInfo.getName();
      if (
        bid.Final_Air_Confirmation_Last_Send_Date__c != null &&
        bid.Final_Air_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Air_Confirmation_Last_Send_Date__c
      )
        bid.Final_Air_Confirmation_Last_Send_By__c = UserInfo.getName();
    }
  }

  public static void generateBidTraces(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    Set<String> theTraceFields = new Set<String>{
      'Rate_Agreement_Last_Send_Date__c',
      'Housing_Contract_Last_Send_Date__c'
    };
    Bid__c[] changedRecords = getChangedRecords(theTraceFields, oldBidsMap, bidsMap);
    Map<Id, Bid__c> bidMap = new Map<Id, Bid__c>();
    for (Bid__c b : changedRecords) {
      if (b.Air__c != null)
        bidMap.put(b.Id, b);
    }
    if (changedRecords.size() > 0) {
      system.debug('inside bid changed records');
      Map<Id, Id> tournamentProductions = new Map<Id, Id>();
      List<Task> tournamentTraces = new List<Task>();
      String traceCoordinator = '';
      List<Task> contractTraces = new List<Task>();
      Map<String, Task> contractAirTracesMap = new Map<String, Task>();
      Set<String> contractTracesList = new Set<String>();

      for (Bid__c bid : changedRecords) {
        traceCoordinator = TraceHelper.getCoordinatorContracts(bid);

        contractTraces = TraceHelper.createTracesContractBid(changedRecords);
      }
      createdTraces = true;

      try {
        if (!contractTraces.isEmpty())
          system.debug('upsert traces');
        upsert contractTraces;
      } catch (DmlException e) {
        System.debug('BidTriggerHandler.generateBidTraces() - DmlException: ' + e.getMessage());
      }
    }
  }

  public static void updateCongaBidTraces(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    Map<String, Set<Id>> sentBidsMap = new Map<String, Set<Id>>{
      'rateAgreementSentBidIds' => new Set<Id>(),
      'housingAgreementSentBidIds' => new Set<Id>(),
      'contractToClientSentBidIds' => new Set<Id>(),
      'counterNeededSentBidIds' => new Set<Id>(),
      'finalContractSentBidIds' => new Set<Id>(),
      'emailConfirmationSentBidIds' => new Set<Id>(),
      'tripDetailsUpdateSentBidIds' => new Set<Id>(),
      'transportationContractSentBidIds' => new Set<Id>(),
      'namesFinalPaymentSentBidIds' => new Set<Id>(),
      'depositDueSentBidIds' => new Set<Id>(),
      'utilizationSentBidIds' => new Set<Id>(),
      'ticketedConfirmationSentBidIds' => new Set<Id>()
    };
    system.debug('inside update traces');
    List<String> traceSubjects = new List<String>{
      ///Housing
      'Rooming List Due Date',
      'Rooming List Reminder',
      'Pending Contract',
      'Pending Rate Agreement',
      'Create GCIP',
      'Contract Due Date', // will this be OK?  Hoping removing from this list means not to evaluate it
      'Check-in Call',
      'Pending Client Signature',
      'Need to Send to Client',
      ///GT
      'Confirmation Email',
      'Pending Hotel Counter',
      'Pending Counter',
      'Pending Trip Update',
      ///Air
      'Names & Final Payment Reminder',
      'Deposit Reminder',
      'Utilization Reminder',
      'Ticketed Confirmation'
    };
    Set<Id> sentBidIds = new Set<Id>();
    List<Task> pendingClientTasks = new List<Task>();
    Map<String, Task> contractTasksMap = new Map<String, Task>();
    Map<Id, Bid__c> bidsToUpdate = new Map<Id, Bid__c>();
    List<Housing__c> housingsToUpdate = new List<Housing__c>();
    Map<Id, Task> tracesToUpdate = new Map<Id, Task>();
    for (Bid__c bid : bidsMap.values()) {
      if (
        bid.Rate_Agreement_Last_Send_Date__c != null &&
        bid.Rate_Agreement_Last_Send_Date__c != oldBidsMap.get(bid.Id).Rate_Agreement_Last_Send_Date__c
      )
        sentBidsMap.get('rateAgreementSentBidIds').add(bid.id);
      if (
        bid.Housing_Contract_Last_Send_Date__c != null &&
        bid.Housing_Contract_Last_Send_Date__c != oldBidsMap.get(bid.Id).Housing_Contract_Last_Send_Date__c
      )
        sentBidsMap.get('housingAgreementSentBidIds').add(bid.id);
      if (
        bid.Contract_to_Client_Last_Send_Date__c != null &&
        bid.Contract_to_Client_Last_Send_Date__c != oldBidsMap.get(bid.Id).Contract_to_Client_Last_Send_Date__c
      ) {
        sentBidsMap.get('contractToClientSentBidIds').add(bid.id);
        system.debug('contract to client');
        bidsToUpdate.put(bid.id, (new Bid__c(Id = bid.Id, Status__c = 'Pending Client Signature')));
        housingsToUpdate.add(new Housing__c(Id = bid.Housing__c, Status_CC__c = 'Pending Client Signature'));
      }
      if (
        bid.Counter_Needed_Last_Send_Date__c != null &&
        bid.Counter_Needed_Last_Send_Date__c != oldBidsMap.get(bid.Id).Counter_Needed_Last_Send_Date__c
      )
        sentBidsMap.get('counterNeededSentBidIds').add(bid.id);
      if (
        bid.Final_Contract_Last_Send_Date__c != null &&
        bid.Final_Contract_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Contract_Last_Send_Date__c
      )
        sentBidsMap.get('finalContractSentBidIds').add(bid.id);
      if (
        bid.Email_Confirmation_Last_Send_Date__c != null &&
        bid.Email_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Email_Confirmation_Last_Send_Date__c
      )
        sentBidsMap.get('emailConfirmationSentBidIds').add(bid.id);
      if (
        bid.Trip_Details_Update_Last_Send_Date__c != null &&
        bid.Trip_Details_Update_Last_Send_Date__c != oldBidsMap.get(bid.Id).Trip_Details_Update_Last_Send_Date__c
      )
        sentBidsMap.get('tripDetailsUpdateSentBidIds').add(bid.id);
      if (
        bid.Transportation_Contract_Last_Send_Date__c != null &&
        bid.Transportation_Contract_Last_Send_Date__c !=
        oldBidsMap.get(bid.Id).Transportation_Contract_Last_Send_Date__c
      )
        sentBidsMap.get('transportationContractSentBidIds').add(bid.id);
      if (
        bid.Names_Final_Payment_Last_Send_Date__c != null &&
        bid.Names_Final_Payment_Last_Send_Date__c != oldBidsMap.get(bid.Id).Names_Final_Payment_Last_Send_Date__c
      )
        sentBidsMap.get('namesFinalPaymentSentBidIds').add(bid.id);
      if (
        bid.Deposit_Due_Last_Send_Date__c != null &&
        bid.Deposit_Due_Last_Send_Date__c != oldBidsMap.get(bid.Id).Deposit_Due_Last_Send_Date__c
      )
        sentBidsMap.get('depositDueSentBidIds').add(bid.id);
      if (
        bid.Utilization_Last_Send_Date__c != null &&
        bid.Utilization_Last_Send_Date__c != oldBidsMap.get(bid.Id).Utilization_Last_Send_Date__c
      )
        sentBidsMap.get('utilizationSentBidIds').add(bid.id);
      if (
        bid.Ticketed_Confirmation_Last_Send_Date__c != null &&
        bid.Ticketed_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Ticketed_Confirmation_Last_Send_Date__c
      )
        sentBidsMap.get('ticketedConfirmationSentBidIds').add(bid.id);
    }
    for (String key : sentBidsMap.keySet())
      sentBidIds.addAll(sentBidsMap.get(key));
    for (Task trace : [
      SELECT id, Task_Type__c, Status, Subject, WhatId, ActivityDate, What.Type
      FROM Task
      WHERE WhatId IN :sentBidIds AND Contract_Task__c = TRUE AND Subject IN :traceSubjects
    ]) {
      if (trace.Task_Type__c == 'Housing Status Trace') {
        system.debug('trace :: ' + trace);
        system.debug('sendBidIds :: ' + sentBidIds);
        system.debug('sentBidsMap keyset:: ' + sentBidsMap.keyset());
        system.debug('sentBidsMap :: ' + sentBidsMap);
        system.debug('trace.whatId :: ' + trace.WhatId);
        system.debug(sentBidsMap.get('contractToClientSentBidIds').contains(trace.WhatId));
        if (sentBidsMap.get('rateAgreementSentBidIds').contains(trace.WhatId)) {
          if (oldBidsMap.get(trace.WhatId).Rate_Agreement_Last_Send_Date__c == null) {
            system.debug('inside rate agreement block');
            if (trace.Subject == 'Pending Contract') {
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
            } else if (trace.Subject == 'Pending Rate Agreement') {
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
            } else if (trace.Subject == 'Rooming List Due Date') {
              if (
                (String.isEmpty(bidsMap.get(trace.WhatId).Production_Office_Location__c) ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRU' ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRA') &&
                bidsMap.get(trace.WhatId).Housing_Record_Type__c != 'Corporate Housing' &&
                bidsMap.get(trace.WhatId).Rooming_list_due_by__c != null
              ) {
                trace.ActivityDate = bidsMap.get(trace.WhatId).Rooming_list_due_by__c;
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              }
            } else if (trace.Subject == 'Rooming List Reminder') {
              if (
                (String.isEmpty(bidsMap.get(trace.WhatId).Production_Office_Location__c) ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRU' ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRA') &&
                bidsMap.get(trace.WhatId).Housing_Record_Type__c != 'Corporate Housing' &&
                bidsMap.get(trace.WhatId).Rooming_list_due_by__c != null
              ) {
                trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Rooming_list_due_by__c, -5);
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              } else if (
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRE' &&
                bidsMap.get(trace.WhatId).Housing_Record_Type__c != 'Corporate Housing' &&
                bidsMap.get(trace.WhatId).Rooming_list_due_by__c != null
              ) {
                trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Rooming_list_due_by__c, -10);
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              }
            } else if (trace.Subject == 'Check-in call') {
            	if (bidsMap.get(trace.WhatId).Parent_Start_Date__c != null) {
              		trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Parent_Start_Date__c, -1);
              		trace.Status = 'Open';
              		tracesToUpdate.put(trace.Id, trace);
            	}
          	}
          } 
        }
        if (
          sentBidsMap.get('housingAgreementSentBidIds').contains(trace.WhatId) &&
          !sentBidsMap.get('contractToClientSentBidIds').contains(trace.WhatId)
        ) {
          system.debug('inside housing agreement block ::');
          //179011529
            if (trace.Subject == 'Pending Contract') {
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
              bidsToUpdate.put(trace.whatId, (new Bid__c(Id = trace.WhatId, Final_Status__c = 'In Contracting')));
          } 
         if (oldBidsMap.get(trace.WhatId).Housing_Contract_Last_Send_Date__c == null) {
            system.debug('inside housing agreement block');
            if (trace.Subject == 'Pending Rate Agreement') {
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
            } else if (trace.Subject == 'Rooming List Due Date') {
              if (
                (String.isEmpty(bidsMap.get(trace.WhatId).Production_Office_Location__c) ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRU' ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRA') &&
                bidsMap.get(trace.WhatId).Housing_Record_Type__c != 'Corporate Housing' &&
                bidsMap.get(trace.WhatId).Rooming_list_due_by__c != null
              ) {
                trace.ActivityDate = bidsMap.get(trace.WhatId).Rooming_list_due_by__c;
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              }
            } else if (trace.Subject == 'Rooming List Reminder') {
              if (
                (String.isEmpty(bidsMap.get(trace.WhatId).Production_Office_Location__c) ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRU' ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRA') &&
                bidsMap.get(trace.WhatId).Housing_Record_Type__c != 'Corporate Housing' &&
                bidsMap.get(trace.WhatId).Rooming_list_due_by__c != null
              ) {
                trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Rooming_list_due_by__c, -5);
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              } else if (
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRE' &&
                bidsMap.get(trace.WhatId).Housing_Record_Type__c != 'Corporate Housing' &&
                bidsMap.get(trace.WhatId).Rooming_list_due_by__c != null
              ) {
                trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Rooming_list_due_by__c, -10);
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              }
            } else if (trace.Subject == 'Contract Due Date') {
              if (bidsMap.get(trace.WhatId).Contract_Due_Date__c != null) {
                trace.ActivityDate = bidsMap.get(trace.WhatId).Contract_Due_Date__c;
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              }
            } else if (trace.Subject == 'Create GCIP') {
              if (
                (String.isEmpty(bidsMap.get(trace.WhatId).Production_Office_Location__c) ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRU' ||
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRA') &&
                bidsMap.get(trace.WhatId).Parent_Start_Date__c != null
              ) {
                trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Parent_Start_Date__c, -14);
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              } else if (
                bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRE' &&
                bidsMap.get(trace.WhatId).Parent_Start_Date__c != null
              ) {
                trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Parent_Start_Date__c, -7);
                trace.Status = 'Open';
                tracesToUpdate.put(trace.Id, trace);
              }
            } else if (trace.Subject == 'Check-in call') {
            if (bidsMap.get(trace.WhatId).Parent_Start_Date__c != null) {
              trace.ActivityDate = ApexUtil.AddBusinessDays(bidsMap.get(trace.WhatId).Parent_Start_Date__c, -1);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
            }
          }
          } 
        } else if (sentBidsMap.get('contractToClientSentBidIds').contains(trace.WhatId)) {
          // update bid and housing
          system.debug('inside contract to client agreement block');
          system.debug('sweetspot');
          new Bid__c(Id = trace.WhatId, Final_Status__c = 'Pending Client Signature');

          if (trace.subject.equalsIgnoreCase('Need to Send to Client')) {
              //178134542
              if(trace.ActivityDate != null) {
                system.debug('in need to send to client');
                system.debug(trace);
                trace.Status = 'Completed';
                trace.ActivityDate = null;
                tracesToUpdate.put(trace.Id, trace);
          	}
          } else if (trace.subject == 'Pending Client Signature') {
            system.debug('inside pending sig block');
            system.debug(trace);

            if (
              String.isEmpty(bidsMap.get(trace.WhatId).Production_Office_Location__c) ||
              bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRU' ||
              bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRA'
            ) {
              system.debug('rru or rra or empty production office location');
              //pendingClientTasks.add(trace);
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 7);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
            } else if (bidsMap.get(trace.WhatId).Production_Office_Location__c == 'RRE') {
              system.debug('RRE block');
              trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 7);
              trace.Status = 'Open';
              tracesToUpdate.put(trace.Id, trace);
            }
          } else if (trace.subject == 'Contract Due Date')
            contractTasksMap.put(trace.WhatId, trace);
        }
        if (sentBidsMap.get('counterNeededSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Hotel Counter') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
          }
        }
        if (sentBidsMap.get('finalContractSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Contract Due Date') {
            if (trace.ActivityDate != null) {
              trace.ActivityDate = null;
              trace.Status = 'Completed';
              tracesToUpdate.put(trace.Id, trace);
            }
          }
        }
      } else if (trace.Task_Type__c == 'Ground Status Trace') {
        if (sentBidsMap.get('rateAgreementSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Contract') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
            bidsToUpdate.put(trace.whatId, (new Bid__c(Id = trace.WhatId, Final_Status__c = 'In Contracting')));
          }
        } else if (sentBidsMap.get('transportationContractSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Contract') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
            bidsToUpdate.put(trace.whatId, (new Bid__c(Id = trace.WhatId, Final_Status__c = 'In Contracting')));
          }
        } else if (sentBidsMap.get('contractToClientSentBidIds').contains(trace.WhatId)) {
          if (trace.subject.equalsIgnoreCase('Need to Send to Client')) {
            system.debug('hello in NEED2SEND2CLIENT');
            trace.Status = 'Completed';
            trace.ActivityDate = null;
            tracesToUpdate.put(trace.Id, trace);
          }
          if (trace.subject == 'Pending Client Signature') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 7);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('counterNeededSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Counter') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
            bidsToUpdate.put(trace.whatId, (new Bid__c(Id = trace.WhatId, Final_Status__c = 'Pending Counter')));
          }
        } else if (sentBidsMap.get('tripDetailsUpdateSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Trip Update') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('emailConfirmationSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Confirmation Email' && trace.ActivityDate != null) {
            trace.ActivityDate = null;
            trace.Status = 'Completed';
            tracesToUpdate.put(trace.Id, trace);
          }
        }
      } else if (trace.Task_Type__c == 'Freight Status Trace') {
        if (sentBidsMap.get('rateAgreementSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Rate Agreement') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
            bidsToUpdate.put(trace.whatId, (new Bid__c(Id = trace.WhatId, Final_Status__c = 'In Contracting')));
          }
        } else if (sentBidsMap.get('contractToClientSentBidIds').contains(trace.WhatId)) {
          if (trace.subject.equalsIgnoreCase('Need to Send to Client')) {
            trace.Status = 'Completed';
            trace.ActivityDate = null;
            tracesToUpdate.put(trace.Id, trace);
          }
          if (trace.subject == 'Pending Client Signature') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 7);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('counterNeededSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Counter') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
            bidsToUpdate.put(trace.whatId, (new Bid__c(Id = trace.WhatId, Final_Status__c = 'Pending Counter')));
          }
        } else if (sentBidsMap.get('tripDetailsUpdateSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Pending Trip Update') {
            trace.ActivityDate = ApexUtil.AddBusinessDays(Date.Today(), 2);
            trace.Status = 'Open';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('emailConfirmationSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Confirmation Email' && trace.ActivityDate != null) {
            trace.ActivityDate = null;
            trace.Status = 'Completed';
            tracesToUpdate.put(trace.Id, trace);
          }
        }
      } else if (trace.Task_Type__c == 'Air Status Trace') {
        if (sentBidsMap.get('namesFinalPaymentSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Names & Final Payment Reminder' && trace.ActivityDate != null) {
            trace.ActivityDate = null;
            trace.Status = 'Completed';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('depositDueSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Deposit Reminder' && trace.ActivityDate != null) {
            trace.ActivityDate = null;
            trace.Status = 'Completed';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('utilizationSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Utilization Reminder' && trace.ActivityDate != null) {
            trace.ActivityDate = null;
            trace.Status = 'Completed';
            tracesToUpdate.put(trace.Id, trace);
          }
        } else if (sentBidsMap.get('ticketedConfirmationSentBidIds').contains(trace.WhatId)) {
          if (trace.Subject == 'Ticketed Confirmation' && trace.ActivityDate != null) {
            trace.ActivityDate = null;
            trace.Status = 'Completed';
            tracesToUpdate.put(trace.Id, trace);
          }
        }
      }
    }
    for (Task trace : pendingClientTasks)
      if (contractTasksMap.containsKey(trace.WhatId) && contractTasksMap.get(trace.WhatId).ActivityDate != null) {
        trace.ActivityDate = ApexUtil.AddBusinessDays(contractTasksMap.get(trace.WhatId).ActivityDate, -2);
        trace.Status = 'Open';
        tracesToUpdate.put(trace.Id, trace);
      }
    system.debug('set the pending client sig trace');
    system.debug(tracesToUpdate);

    try {
      if (!tracesToUpdate.isEmpty())
        update tracesToUpdate.values();
      ApexUtil.BidTrigger_Is_Enabled = false;
      if (!bidsToUpdate.isEmpty())
        update bidsToUpdate.values();
      if (!housingsToUpdate.isEmpty())
        update housingsToUpdate;
      ApexUtil.BidTrigger_Is_Enabled = true;
    } catch (DmlException e) {
      System.debug('BidTriggerHandler.updateCongaBidTraces() - DmlException: ' + e.getMessage());
    }
  }

  public static void createJournalEntries(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    List<JournalCreation.JournalEntry> journalEntries = new List<JournalCreation.JournalEntry>();
    String journal_bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
        .get('Bid_Journal') != null
      ? Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Bid_Journal').getRecordTypeId()
      : null;
    for (Bid__c bid : bidsMap.values()) {
      ///Bid Status Journal Entries
      if (bid.Status__c != oldBidsMap.get(bid.Id).Status__c && bid.Status__c == 'Contracted') {
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'This bid is contracted.')
        );
      }
      if (bid.Final_Status__c != oldBidsMap.get(bid.Id).Final_Status__c)
        journalEntries.add(
          new JournalCreation.JournalEntry(
            'bid',
            bid.Id,
            journal_bidJournalRT,
            'Final status is changed to ' +
            bid.Final_Status__c +
            '.'
          )
        );
      if (bid.Final_Status__c != oldBidsMap.get(bid.Id).Final_Status__c && bid.Final_Status__c == 'Contracted')
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Received contract due date.')
        );

      ///Conga Journal Entries
      if (
        bid.Rate_Agreement_Last_Send_Date__c != null &&
        bid.Rate_Agreement_Last_Send_Date__c != oldBidsMap.get(bid.Id).Rate_Agreement_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Rate Agreement was completed.')
        );
      if (
        bid.Housing_Contract_Last_Send_Date__c != null &&
        bid.Housing_Contract_Last_Send_Date__c != oldBidsMap.get(bid.Id).Housing_Contract_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Housing Contract was completed.')
        );
      if (
        bid.Contract_to_Client_Last_Send_Date__c != null &&
        bid.Contract_to_Client_Last_Send_Date__c != oldBidsMap.get(bid.Id).Contract_to_Client_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Contract to Client was completed.')
        );
      if (
        bid.Email_Confirmation_Last_Send_Date__c != null &&
        bid.Email_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Email_Confirmation_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Email Confirmation was completed.')
        );
      if (
        bid.Trip_Details_Update_Last_Send_Date__c != null &&
        bid.Trip_Details_Update_Last_Send_Date__c != oldBidsMap.get(bid.Id).Trip_Details_Update_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Trip Details Update was completed.')
        );
      if (
        bid.Transportation_Contract_Last_Send_Date__c != null &&
        bid.Transportation_Contract_Last_Send_Date__c !=
        oldBidsMap.get(bid.Id).Transportation_Contract_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry(
            'bid',
            bid.Id,
            journal_bidJournalRT,
            'Transportation Contract was completed.'
          )
        );

      if (
        bid.Names_Final_Payment_Last_Send_Date__c != null &&
        bid.Names_Final_Payment_Last_Send_Date__c != oldBidsMap.get(bid.Id).Names_Final_Payment_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Names & Final Payment was completed.')
        );
      if (
        bid.Deposit_Due_Last_Send_Date__c != null &&
        bid.Deposit_Due_Last_Send_Date__c != oldBidsMap.get(bid.Id).Deposit_Due_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Deposit Due was completed.')
        );
      if (
        bid.Utilization_Last_Send_Date__c != null &&
        bid.Utilization_Last_Send_Date__c != oldBidsMap.get(bid.Id).Utilization_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Utilization was completed.')
        );

      if (
        bid.Counter_Needed_Last_Send_Date__c != null &&
        bid.Counter_Needed_Last_Send_Date__c != oldBidsMap.get(bid.Id).Counter_Needed_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Counter Needed was completed.')
        );
      if (
        bid.Final_Contract_Last_Send_Date__c != null &&
        bid.Final_Contract_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Contract_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Final Contract was completed.')
        );
      if (
        bid.Credit_Card_Last_Send_Date__c != null &&
        bid.Credit_Card_Last_Send_Date__c != oldBidsMap.get(bid.Id).Credit_Card_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Credit Card Change was completed.')
        );
      /**if (
        bid.Cancellation_Last_Send_Date__c != null &&
        bid.Cancellation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Cancellation_Last_Send_Date__c
      )
        journalEntries.add(new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Cancellation was completed.'));
	  **/
      /** 178452352
      if (
        bid.Pick_Up_Last_Send_Date__c != null &&
        bid.Pick_Up_Last_Send_Date__c != oldBidsMap.get(bid.Id).Pick_Up_Last_Send_Date__c
      )
        journalEntries.add(new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Pick Up Report was completed.'));
	  **/
      if (
        bid.Final_Choice_Last_Send_Date__c != null &&
        bid.Final_Choice_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Choice_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Final Choice was completed.')
        );
      if (
        bid.Ticketed_Confirmation_Last_Send_Date__c != null &&
        bid.Ticketed_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Ticketed_Confirmation_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Ticketed Confirmation was completed.')
        );
      if (
        bid.Final_Air_Confirmation_Last_Send_Date__c != null &&
        bid.Final_Air_Confirmation_Last_Send_Date__c != oldBidsMap.get(bid.Id).Final_Air_Confirmation_Last_Send_Date__c
      )
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, journal_bidJournalRT, 'Final Air Confirmation was completed.')
        );

      ///Journal Entries Automation
      if (bid.New_Journal_RecordType__c != null && bid.New_Journal_Entry__c != null)
        journalEntries.add(
          new JournalCreation.JournalEntry('bid', bid.Id, bid.New_Journal_RecordType__c, bid.New_Journal_Entry__c)
        );
    }
    if (!journalEntries.isEmpty()) {
      Map<Id, Bid__c> bidsToUpdate = new Map<Id, Bid__c>();
      for (Bid__c bid : bidsMap.values())
        if (bid.New_Journal_RecordType__c != null && bid.New_Journal_Entry__c != null)
          bidsToUpdate.put(
            bid.Id,
            (new Bid__c(
              Id = bid.Id,
              Final_Status__c = 'In Contracting',
              New_Journal_RecordType__c = null,
              New_Journal_Entry__c = null
            ))
          );
      try {
        JournalCreation.insertJournal(journalEntries);
        ApexUtil.BidTrigger_Is_Enabled = false;
        if (!bidsToUpdate.isEmpty())
          update bidsToUpdate.values();

        ApexUtil.BidTrigger_Is_Enabled = true;
      } catch (DmlException e) {
        System.debug('BidTriggerHandler.createJournalEntries() - DmlException: ' + e.getMessage());
      }
    }
  }

  public static void verifySabreRate(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    Set<String> accountIds = new Set<String>();
    for (Bid__c bid : bidsMap.values())
      accountIds.add(bid.Vendor__c);

    Map<String, Account> accountMap = new Map<String, Account>();
    for (Account acc : [SELECT Id, Sabre_Hotel_Code__c FROM Account WHERE Id IN :accountIds])
      accountMap.put(acc.Id, acc);

    Set<Id> bidIds = new Set<Id>();
    Set<Id> bidWithoutCodeIds = new Set<Id>();
    for (Bid__c bid : bidsMap.values()) {
      if (
        bid.Status__c == 'Sent' &&
        oldBidsMap.get(bid.Id).Status__c != bid.Status__c &&
        bid.Housing__c != null &&
        bid.Vendor__c != null &&
        accountMap.get(bid.Vendor__c).Sabre_Hotel_Code__c != null
      )
        bidIds.add(bid.Id);
      if (
        bid.Status__c == 'Sent' &&
        oldBidsMap.get(bid.Id).Status__c != bid.Status__c &&
        bid.Housing__c != null &&
        bid.Vendor__c != null &&
        accountMap.get(bid.Vendor__c).Sabre_Hotel_Code__c == null
      )
        bidWithoutCodeIds.add(bid.Id);
    }

    if (!bidIds.isEmpty() && !Test.isRunningTest())
      SabreWs.getHotelRatingInfoRQ(bidIds);
    if (!bidWithoutCodeIds.isEmpty() && !Test.isRunningTest())
      SabreWs.getHotelRatingInfoRQByAccount(bidWithoutCodeIds);
  }

  public static void verifyNoBidReason(Map<Id, Bid__c> oldBidsMap, Map<Id, Bid__c> bidsMap) {
    List<Bid__c> bidList = new List<Bid__c>();
    for (Bid__c bid : bidsMap.values()) {
      if (
        bid.GT__c != null &&
        bid.Status__c == 'Sold Out / Not Bidding' &&
        bid.No_Bid_reason__c == null &&
        oldBidsMap.get(bid.Id).No_Bid_reason__c != null &&
        bid.No_Bid_reason__c != oldBidsMap.get(bid.Id).No_Bid_reason__c
      ) {
        bidList.add(new Bid__c(Id = bid.Id, Status__c = 'Sent'));
      }
    }
    if (!bidList.isEmpty()) {
      ApexUtil.BidTrigger_Is_Enabled = false;
      update bidList;
      ApexUtil.BidTrigger_Is_Enabled = true;
    }
  }

  public static List<SObject> getChangedRecords(
    Set<String> fieldNames,
    Map<Id, SObject> oldItems,
    Map<Id, SObject> newItems
  ) {
    List<SObject> changedRecords = new List<SObject>();
    for (SObject newRecord : newItems.values()) {
      Id recordId = (Id) newRecord.get('Id');
      if (oldItems == null || !oldItems.containsKey(recordId)) {
        continue;
      }

      SObject oldRecord = oldItems.get(recordId);
      for (String fieldName : fieldNames) {
        if (oldRecord.get(fieldName) != newRecord.get(fieldName)) {
          changedRecords.add(newRecord);
          break;
        }
      }
    }
    return changedRecords;
  }

  public static void assignUUIDs(Bid__c[] newBids) {
    for (Bid__c bid : newBids) {
      bid.UUID_for_Landing_Page__c = ApexUtil.mkUuid();
    }
  }
}```

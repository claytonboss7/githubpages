---
layout: default
title: TaskTriggerHandler
parent: classes
---

```public without sharing class TaskTriggerHandler implements ITriggerHandler {
  public static Boolean TriggerDisabled = false;
  public static Boolean hasProcessed = false;
  @testVisible
  public static String bidPrefix = Schema.SObjectType.Bid__c.getKeyPrefix();
  @testVisible
  public static String housingPrefix = Schema.SObjectType.Housing__c.getKeyPrefix();

  public Boolean IsDisabled() {
    return TriggerDisabled;
  }

  public void BeforeInsert(List<SObject> newItems) {
  }

  public void BeforeUpdate(Map<Id, SObject> newItems, Map<Id, SObject> oldItems) {
    Map<Id, Task> newTasks = (Map<Id, Task>) newItems;
    Map<Id, Task> oldTasks = (Map<Id, Task>) oldItems;
    getBidContractingCoordinator(oldTasks, newTasks);
  }

  public void BeforeDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterInsert(Map<Id, SObject> newItems) {
    Map<Id, Task> newTasks = (Map<Id, Task>) newItems;
    handleDupeTraceCheck(null, newTasks);
  }

  public void AfterUpdate(Map<Id, SObject> newItems, Map<Id, SObject> oldItems) {
    Map<Id, Task> newTasks = (Map<Id, Task>) newItems;
    Map<Id, Task> oldTasks = (Map<Id, Task>) oldItems;
    //getBidContractingCoordinator(oldTasks, newTasks);
    bidUpdatesV2(oldTasks, newTasks);
    handleDupeTraceCheck(oldTasks, newTasks);
  }

  public void AfterDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterUndelete(Map<Id, SObject> oldItems) {
  }

  public void getBidContractingCoordinator(Map<Id, Task> oldTasks, Map<Id, Task> newTasks) {
    Task[] changedTasks = getChangedRecords(
      new Set<String>{ 'ActivityDate', 'Calc_Coordinator__c' },
      oldTasks,
      newTasks
    );
    system.debug('changedTasks ::: ' + changedTasks);
    if (changedTasks.size() > 0) {
      system.debug(':-: inside getBidContractingCoordinator');
      Set<Id> bidIds = new Set<Id>();
      Set<Id> housingIds = new Set<Id>();
      Map<Id, Housing__c> housingMap = new Map<Id, Housing__c>();
      Map<Id, Housing__c> bidIdToHousing = new Map<Id, Housing__c>();
      Task[] updateTasks = new List<Task>();
      Map<Id, User> theUsers;
      Map<Id, Bid__c> theBids;
      Map<Id, Housing__c> theHousingsUpdate = new Map<Id, Housing__c>();
      Housing__c theHousing;
      Integer countActive = 0;

      Boolean bidType = false;
      Boolean housingType = false;

      for (Task t : changedTasks) {
        if (t != null && bidPrefix != null && housingPrefix != null && t.whatId != null && bidType != null) {
          bidType = String.valueOf(t.WhatId)?.contains(bidPrefix) ? true : false;
          housingType = String.valueOf(t.WhatId)?.contains(housingPrefix) ? true : false;
        }

        if (bidType) {
          bidIds.add(t.WhatId);
        } else if (housingType) {
          housingIds.add(t.WhatId);
        }
      }

      system.debug('bidType :-: ' + bidType);
      system.debug('housingType :-: ' + housingType);
      system.debug('bidIds :-: ' + bidIds);
      system.debug('housingIds :-: ' + housingIds);

      theBids = new Map<Id, Bid__c>(
        [
          SELECT
            Id,
            Contracting_Back_End_Coordinator__c,
            Contracting_Back_End_Coordinator__r.Name,
            Housing__r.Production_CC__c,
            Housing__c,
            Housing__r.Id,
            Housing__r.Back_end_Coordinator__c,
            Housing__r.Status_CC__c,
            Production__c,
            (SELECT Id, ActivityDate, WhatId, What.Type, Status, Subject FROM Tasks)
          FROM Bid__c
          WHERE (Id IN :bidIds OR Housing__c IN :housingIds) AND Housing__c != NULL
        ]
      );

      system.debug('theBids :-: ' + theBids);

      for (Bid__c b : theBids.values()) {
        countActive = 0;
        theHousing = new Housing__c(
          Id = b.Housing__r.Id,
          Production_CC__c = b.Housing__r.Production_CC__c,
          Back_End_Coordinator__c = b.Housing__r.Back_end_Coordinator__c,
          Status_CC__c = b.Housing__r.Status_CC__c
        );
        bidIdToHousing.put(b.Id, theHousing);

        Task[] theTasks = b.Tasks;
        countActive = 0;
        for (Task t : theTasks) {
          if (t.ActivityDate != null && t.Status == 'Open') {
            countActive = countActive + 1;
          }
        }

        system.debug('in bid loop and counted traces');

        theHousing.Count_Active_Bid_Traces__c = countActive > 0 ? countActive : 0;
        theHousingsUpdate.put(theHousing.Id, theHousing);
      }

      if (housingIds.size() > 0) {
        system.debug('had housing ids');

        housingMap = new Map<Id, Housing__c>(
          [SELECT Id, Status_CC__c, Production_CC__c, Back_End_Coordinator__c FROM Housing__c WHERE Id IN :housingIds]
        );
      }

      if (housingIds.size() > 0 || bidIds.size() > 0) {
        system.debug('had housing or bid ids and queried users');
        theUsers = new Map<Id, User>(
          [
            SELECT Id, Name
            FROM User
            WHERE isActive = TRUE AND Profile.Name != 'Road Rebel Vendor' AND Profile.Name != 'Road Rebel Customer'
          ]
        );

        for (Task t : newTasks.values()) {
          Housing__c theHousingRecord = housingType
            ? housingMap?.get(t.WhatId)
            : bidType ? bidIdToHousing?.get(t.WhatId) : null;

          Bid__c theBid = bidType ? theBids.get(t.WhatId) : null;

          system.debug('**** t.WhatId:: ' + t.WhatId);
          system.debug('**** t.What.Type :: ' + t.What.Type);
          system.debug('**** theHousingRecord :: ' + theHousingRecord);
          system.debug('**** housingMap :: ' + housingMap);
          system.debug('**** bidIdToHousing :: ' + bidIdToHousing);
          system.debug('bidPrefix : : : ' + bidPrefix);
          system.debug('housingPrefix : : : ' + housingPrefix);
          system.debug('bidids : : : ' + bidids);
          system.debug('housingids : : : ' + housingids);

          String contractingCoordinatorFinal = bidType ? TraceHelper.getCoordinatorContracts(theBid) : null;

          String theType = TraceHelper.getTypeByBid(theBid);
          String primaryContractCoordinator = bidType
            ? theUsers.get(TraceHelper.getCoordinatorContractPrimary(theBid?.Housing__r.Production_CC__c, theType))
                ?.Name
            : null;
          String contractingBackendCoordinator = bidType
            ? theUsers.get(TraceHelper.getCoordinatorContractsBackend(theBid))?.Name
            : null;
          String primaryServiceCoordinatorFinal = housingType
            ? theUsers.get(TraceHelper.getCoordinatorService(theHousingRecord))?.Name
            : null;
          String primaryServiceCoordinator = housingType
            ? theUsers.get(TraceHelper.getCoordinatorServicePrimary(theHousingRecord))?.Name
            : null;
          String serviceBackendCoordinator = housingType
            ? theUsers.get(TraceHelper.getCoordinatorServiceBackend(theHousingRecord))?.Name
            : null;

          /*
          Task theUpdateTask = new Task(
            Contracting_Coordinator_Final__c = contractingCoordinatorFinal,
            Primary_Contract_Coordinator__c = primaryContractCoordinator,
            Contracting_Back_End_Coordinator__c = contractingBackendCoordinator,
            Primary_Service_Coordinator_Final__c = primaryServiceCoordinatorFinal,
            Primary_Service_Coordinator__c = primaryServiceCoordinator,
            Service_Backend_Coordinator__c = serviceBackendCoordinator,
            Id = t.Id
          );
          */

          t.Contracting_Coordinator_Final__c = contractingCoordinatorFinal;
          t.Primary_Contract_Coordinator__c = primaryContractCoordinator;
          t.Contracting_Back_End_Coordinator__c = contractingBackendCoordinator;
          t.Primary_Service_Coordinator_Final__c = primaryServiceCoordinatorFinal;
          t.Primary_Service_Coordinator__c = primaryServiceCoordinator;
          t.Service_Backend_Coordinator__c = serviceBackendCoordinator;

          if (bidType)
            t.OwnerId = contractingCoordinatorFinal;

          system.debug('contractingCoordinatorFinal: ' + contractingCoordinatorFinal);
          system.debug('primaryContractCoordinator' + primaryContractCoordinator);
          system.debug('contractingBackendCoordinator : ' + contractingBackendCoordinator);
          system.debug('primaryServiceCoordinatorFinal  ' + primaryServiceCoordinatorFinal);
          system.debug('primaryServiceCoordinator :' + primaryServiceCoordinator);
          system.debug('serviceBackendCoordinator : ' + serviceBackendCoordinator);

          // updateTasks.add(theUpdateTask);
        }
      }

      if (theHousingsUpdate.size() > 0) {
        update theHousingsUpdate.values();
        hasProcessed = true;
      }

      ApexUtil.HousingTrigger_Is_Enabled = false;

      if (updateTasks.size() > 0) {
        update updateTasks;
        hasProcessed = true;
      }
    }
  }

  public static void handleDupeTraceCheck(Map<Id, Task> oldTasks, Map<Id, Task> newTasks) {
    Task[] changedTasks = getChangedRecords(new Set<String>{ 'Order__c' }, oldTasks, newTasks);

    for (Task t : changedTasks) {
      if (t.Order__c == 22) {
        TraceHelper.updateDupesOnBid(new Set<String>{ t.WhatId });
      }
    }
  }

  private static Set<String> taskSubjectsSet = new Set<String>{
    'Pending Update',
    'Pending Date Change',
    'Pending No Rooms Picked Up',
    'Pending Cancellation',
    'Awaiting Addendum',
    'Pending Issue'
  };

  public static void bidUpdatesV2(Map<Id, Task> oldTasksMap, Map<Id, Task> tasksMap) {
    Map<Id, Task> housingBidTasksMap = new Map<Id, Task>();
    List<Bid__c> housingBidsToUpdate = new List<Bid__c>();
    String bidPrefix = Schema.SObjectType.Bid__c.getKeyPrefix();
    for (Task task : tasksMap.values()) {
      if (
        String.isNotEmpty(task.WhatId) &&
        ((String) task.WhatId).startsWith(bidPrefix) &&
        taskSubjectsSet.contains(task.Subject) &&
        task.Contract_Task__c == true &&
        oldTasksMap.get(task.Id).ActivityDate == null &&
        task.ActivityDate != null
      ) {
        housingBidTasksMap.put(task.WhatId, task);
      }
    }
    if (!housingBidTasksMap.isEmpty()) {
      List<Bid__c> bidsToUpdate = [
        SELECT id, Final_Status__c, Final_Status_Previous__c
        FROM Bid__c
        WHERE id IN :housingBidTasksMap.keySet() AND RecordType.DeveloperName = 'Housing_Bid'
      ];
      for (Bid__c bid : bidsToUpdate) {
        bid.Final_Status__c = 'Pending Update';
        housingBidsToUpdate.add(bid);
      }
      try {
        //update housingBidsToUpdate;
      } catch (DmlException e) {
        System.debug('TaskTriggerHandler.bidUpdatesV2() - DmlException: ' + e.getMessage());
      }
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
        for (String fieldName : fieldNames) {
          if (newRecord.get(fieldName) != null) {
            changedRecords.add(newRecord);
          }
        }
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
}```

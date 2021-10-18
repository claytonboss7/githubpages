---
layout: default
title: HousingTriggerHandler
parent: classes
---

```/**
 * @description       :
 * @author            : sfdc cb
 * @group             :
 * @last modified on  : 09-07-2021
 * @last modified by  : sfdc cb
 **/
public class HousingTriggerHandler implements ITriggerHandler {
  public static Boolean TriggerDisabled = false;

  public static String productionId = '';
  public static Boolean hasProcessed = false;
  //Fix By Clay Dev 15 May, 2021 #177390799
  public static Boolean skipStatusChangeJE = false;
  public static Set<Id> theTournamentIds = new Set<Id>();
  public static Map<Id, Housing__c> theHousingMap = new Map<Id, Housing__c>();
  public static Map<String, String> productionToPrimaryHousingCoordinator = new Map<String, String>();
  public static List<RecordType> recordTypeList = [
    SELECT Id, Name
    FROM RecordType
    WHERE Name IN ('Room Types & Ops', 'Hotel Housing')
  ];

  public Boolean IsDisabled() {
    return !ApexUtil.HousingTrigger_Is_Enabled;
  }

  public void BeforeInsert(List<SObject> newItems) {
    Housing__c[] newHousings = (Housing__c[]) newItems;
    for (Housing__c housing : newHousings) {
      if (
        housing.RecordTypeId != null &&
        housing.RecordTypeId ==
        Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId()
      ) {
        if (housing.isRoomTypeHotelHousingStay__c == true) {
          housing.Rate_Period__c = housing.Rate_Period__c != null
            ? housing.Rate_Period__c
            : 'Per Night';
        }
      }

      if (String.isNotEmpty(housing.Status_CC__c))
        housing.Status_Change_Date__c = Date.Today();
    }
  }

  public void BeforeUpdate(
    Map<Id, SObject> newItems,
    Map<Id, SObject> oldItems
  ) {
    Map<Id, Housing__c> theNewItems = (Map<Id, Housing__c>) newItems;
    Map<Id, Housing__c> theOldItems = (Map<Id, Housing__c>) oldItems;
    for (Housing__c housing : theNewItems.values()) {
      if (
        String.isNotEmpty(housing.Status_CC__c) &&
        housing.Status_CC__c != theOldItems.get(housing.id).Status_CC__c
      )
        housing.Status_Change_Date__c = Date.Today();
      else if (
        String.isEmpty(housing.Status_CC__c) &&
        housing.Status_CC__c != theOldItems.get(housing.id).Status_CC__c
      )
        housing.Status_Change_Date__c = null;
    }
  }

  public void BeforeDelete(Map<Id, SObject> oldItems) {
    //HousingTriggerHandler.copyRoomTypeToOtherStay(null, Trigger.old);
  }

  public void AfterInsert(Map<Id, SObject> newItems) {
    Map<Id, Housing__c> theNewItems = (Map<Id, Housing__c>) newItems;
    createTraces(null, theNewItems);
    //Fix By clay Dev 17 Feb, 2021 #176828479
    copyRoomTypeToOtherStay(null, theNewItems.values());
    populateStartAndEndDate(theNewItems.values());
  }

  public void AfterUpdate(
    Map<Id, SObject> newItems,
    Map<Id, SObject> oldItems
  ) {
    Map<Id, Housing__c> theNewItems = (Map<Id, Housing__c>) newItems;
    Map<Id, Housing__c> theOldItems = (Map<Id, Housing__c>) oldItems;

    populateStartAndEndDate(theNewItems.values());
    afterInsertUpdateActions(theOldItems, theNewItems);

    String journal_tripJournalRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Journal__c' AND Name = 'Trip Journal'
    ]
    .Id;
    List<JournalCreation.JournalEntry> journalEntries = new List<JournalCreation.JournalEntry>();
    for (Housing__c h : theNewItems.values()) {
      if (
        (h.New_Journal_RecordType__c != null &&
        h.New_Journal_Entry__c != null)
      )
        journalEntries.add(
          new JournalCreation.JournalEntry(
            'housing',
            h.Id,
            h.New_Journal_RecordType__c,
            h.New_Journal_Entry__c
          )
        );
      if (
        !skipStatusChangeJE &&
        (h.Status_CC__c != theOldItems.get(h.Id).Status_CC__c)
      )
        journalEntries.add(
          new JournalCreation.JournalEntry(
            'housing',
            h.Id,
            journal_tripJournalRT,
            'Housing status is changed to ' +
            h.Status_CC__c +
            '.'
          )
        );

      if (
        h.Back_End_Coordinator__c == null &&
        theOldItems?.get(h?.Id)?.Back_End_Coordinator__c != null
      ) {
        system.debug('******************* inside backend set to null');
        TraceHelper.updateTracesBackendRemovedHousing(
          newItems.values(),
          h.Status_CC__c,
          TraceHelper.getCoordinatorServicePrimary(h)
        );
      } else if (
        h.Back_End_Coordinator__c != null &&
        theOldItems?.get(h?.Id)?.Back_End_Coordinator__c == null
      ) {
        system.debug('******************* inside backend populated');
        TraceHelper.updateTracesBackendReassignedHousing(
          newItems.values(),
          h.Status_CC__c,
          TraceHelper.getCoordinatorServicePrimary(h)
        );
      } else if (
        h.Back_End_Coordinator__c !=
        theOldItems?.get(h?.Id)?.Back_End_Coordinator__c
      ) {
        system.debug('******************* inside backend populated');
        TraceHelper.updateTracesBackendReassignedHousing(
          newItems.values(),
          h.Status_CC__c,
          TraceHelper.getCoordinatorServicePrimary(h)
        );
      }
    }

    if (journalEntries.size() > 0) {
      JournalCreation.insertJournal(journalEntries);
      Housing__c hAux;
      List<Housing__c> hAuxList = new List<Housing__c>();
      for (Housing__c h : theNewItems.values()) {
        if (
          h.New_Journal_RecordType__c != null &&
          h.New_Journal_Entry__c != null
        ) {
          hAux = new Housing__c(
            Id = h.Id,
            New_Journal_RecordType__c = null,
            New_Journal_Entry__c = null
          );
          hAuxList.add(hAux);
        }
      }
      ApexUtil.HousingTrigger_Is_Enabled = false;
      if (hAuxList.size() > 0)
        update hAuxList;
      ApexUtil.HousingTrigger_Is_Enabled = true;
    }

    system.debug('i should be creatingtraces in trigger');

    //Fix By clay Dev 11 Feb, 2021 #176828479
    copyDetailsOnStays(theOldItems, theNewItems.values());
    //Fix By clay Dev 17 Feb, 2021 #176828479
    copyRoomTypeToOtherStay(theOldItems, theNewItems.values());

    //        if (hasProcessed == false)
    createTraces(theOldItems, theNewItems);
  }

  public void AfterDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterUndelete(Map<Id, SObject> oldItems) {
  }

  @testVisible
  public static List<Task> traceTaskList {
    get {
      if (
        productionId != null &&
        productionId != '' &&
        theHousingMap.size() > 0
      ) {
        if (traceTaskList == null) {
          traceTaskList = [
            SELECT
              Id,
              WhatId,
              Subject,
              ActivityDate,
              Status,
              OwnerId,
              Owner.Name
            FROM Task
            WHERE
              WhatId IN :theHousingMap.keySet()
              AND IsForStayOrTrip__c = TRUE
              AND RecordType.Name = 'Trace Task'
            ORDER BY createddate
          ];
        }
      }
      Map<String, Task> finalTaskList = new Map<String, Task>();
      for (Task tsk : traceTaskList) {
        finalTaskList.put(tsk.subject, tsk);
      }
      system.debug(
        '****************** returning traceTaskList' + traceTaskList
      );
      system.debug('****************** final finalTaskList' + finalTaskList);

      return finalTaskList.values();
    }
    private set;
  }

  public static List<Task> taskList {
    get {
      if (productionId != null && productionId != '') {
        if (taskList == null) {
          taskList = [
            SELECT Id, WhatId, Subject
            FROM Task
            WHERE
              WhatId IN :theTournamentIds
              AND Task_Type__c = 'Tournament Status Trace'
          ];
        } else {
          return taskList;
        }
      }
      traceTaskList = taskList;
      return taskList;
    }
    private set;
  }

  public static List<Production_Associations__c> prodAsses {
    get {
      if (productionId != null && productionId != '') {
        if (prodAsses == null) {
          prodAsses = [
            SELECT Production_Opp__c, User__c, Team_Roles__c
            FROM Production_Associations__c
            WHERE
              Production_Opp__c = :productionId
              AND Team_Roles__c INCLUDES (
                'Primary Housing Coordinator',
                'Primary Contract Coordinator'
              )
          ];
        } else {
          return prodAsses;
        }
      }
      return prodAsses;
    }
    public set {
    }
  }

  public static void afterInsertUpdateActions(
    Map<Id, Housing__c> oldHousingMap,
    Map<Id, Housing__c> housingMap
  ) {
    Set<Id> productions = new Set<Id>();
    Set<Id> tournaments = new Set<Id>();
    Map<Id, Id> coordinators = new Map<Id, Id>();

    for (Housing__c housing : housingMap.values()) {
      productions.add(housing.Production_CC__c);
      productionId = housing.Production_CC__c;
      if (String.isNotBlank(housing.Tournament__c))
        tournaments.add(housing.Tournament__c);
    }
    /*List<Production_Associations__c> prodAss = [
      SELECT Production_Opp__c, User__c
      FROM Production_Associations__c
      WHERE Production_Opp__c = :productions
      AND Team_Roles__c INCLUDES ('Primary Contract Coordinator')];*/

    List<Production_Associations__c> theProdAsses = new List<Production_Associations__c>(
      prodAsses
    );
    system.debug('theProdAsses ::: ' + theProdAsses);
    system.debug('theProdAsses ::: ' + prodAsses);

    for (Production_Associations__c pa : theProdAsses) {
      coordinators.put(pa.Production_Opp__c, pa.User__c);
    }

    theTournamentIds = tournaments;

    List<Task> theTaskList = new List<Task>(taskList);
    Set<String> tournamentTracesList = new Set<String>();
    for (Task t : theTaskList) {
      tournamentTracesList.add(task.WhatId + '-' + task.Subject);
    }

    List<Task> tournamentTraces = new List<Task>();
    for (Housing__c housing : housingMap.values()) {
      if (
        coordinators.containsKey(housing.Production_CC__c) &&
        String.isNotBlank(housing.Tournament__c) ||
        (String.isNotBlank(housing.Tournament__c) && Test.isRunningTest())
      ) {
        if (
          !tournamentTracesList.contains(
            housing.Tournament__c + '-Logo & Background Image'
          )
        ) {
          tournamentTraces.add(
            new Task(
              OwnerId = coordinators.get(housing.Production_CC__c) != null
                ? coordinators.get(housing.Production_CC__c)
                : UserInfo.getUserId(),
              WhatId = housing.Tournament__c,
              Status = 'Open',
              Priority = 'No Follow up',
              Task_Type__c = 'Tournament Status Trace',
              Order__c = 1,
              Contract_Task__c = true,
              Subject = 'Logo & Background Image'
            )
          );
          tournamentTracesList.add(
            housing.Tournament__c + '-Logo & Background Image'
          );
        }
        if (
          !tournamentTracesList.contains(
            housing.Tournament__c + '-Weblink to Client'
          )
        ) {
          tournamentTraces.add(
            new Task(
              OwnerId = coordinators.get(housing.Production_CC__c) != null
                ? coordinators.get(housing.Production_CC__c)
                : UserInfo.getUserId(),
              WhatId = housing.Tournament__c,
              Status = 'Open',
              Priority = 'No Follow up',
              Task_Type__c = 'Tournament Status Trace',
              Order__c = 2,
              Contract_Task__c = true,
              Subject = 'Weblink to Client'
            )
          );
          tournamentTracesList.add(
            housing.Tournament__c + '-Weblink to Client'
          );
        }
        if (
          !tournamentTracesList.contains(housing.Tournament__c + '-Add Teams')
        ) {
          tournamentTraces.add(
            new Task(
              OwnerId = coordinators.get(housing.Production_CC__c) != null
                ? coordinators.get(housing.Production_CC__c)
                : UserInfo.getUserId(),
              WhatId = housing.Tournament__c,
              Status = 'Open',
              Priority = 'No Follow up',
              Task_Type__c = 'Tournament Status Trace',
              Order__c = 3,
              Contract_Task__c = true,
              Subject = 'Add Teams'
            )
          );
          tournamentTracesList.add(housing.Tournament__c + '-Add Teams');
        }
      }
    }
    if (!tournamentTraces.isEmpty())
      insert tournamentTraces;
    verifyRevenueForRoomTypes(oldHousingMap, housingMap);
  }

  public static void verifyRevenueForRoomTypes(
    Map<Id, Housing__c> oldHousingMap,
    Map<Id, Housing__c> housingMap
  ) {
    Map<Id, Housing__c> roomTypeMap = new Map<Id, Housing__c>();
    Set<String> bidIds = new Set<String>();
    for (Housing__c housing : housingMap.values()) {
      if (
        housing.RecordTypeId ==
        Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId() &&
        housing.Bid__c != null
      ) {
        roomTypeMap.put(housing.Id, housing);
        bidIds.add(housing.Bid__c);
      }
    }
    if (!roomTypeMap.isEmpty()) {
      Map<Id, Revenue__c> revenueMap = new Map<Id, Revenue__c>();
      for (Revenue__c revenue : [
        SELECT
          Id,
          Bid__c,
          RecordTypeId,
          Room_Type__c,
          Room_Type_Name__c,
          Room_Nights__c,
          Rate_currency__c
        FROM Revenue__c
        WHERE Room_Type__c IN :roomTypeMap.keySet()
      ])
        revenueMap.put(revenue.Room_Type__c, revenue);

      Map<Id, Bid__c> bidMap = new Map<Id, Bid__c>();
      for (Bid__c bid : [
        SELECT
          Id,
          Housing__c,
          Housing__r.Name,
          Housing__r.Date_In__c,
          Housing__r.Date_Out__c,
          Vendor__c,
          Vendor__r.ShippingCountry
        FROM Bid__c
        WHERE Id IN :bidIds
      ])
        bidMap.put(bid.Id, bid);

      Map<Id, Revenue__c> revenueBidMap = new Map<Id, Revenue__c>();
      for (Revenue__c revenueBid : [
        SELECT
          Id,
          Bid__c,
          Commission_Type__c,
          Commission__c,
          Commission_Percent__c,
          Commission_Due__c,
          Notes__c,
          Does_this_match_amount_on_pick_up_report__c,
          Do_you_need_invoice_sent__c,
          Is_this_a_monthly_Pick_Up__c,
          VAT__c,
          VAT_Rate__c,
          Breakfast__c,
          Breakfast_Rate__c,
          CurrencyIsoCode
        FROM Revenue__c
        WHERE
          RecordType.Name IN (
            'Housing Rate & Commission RRE',
            'Housing Rate & Commission RRU'
          )
          AND Bid__c IN :bidIds
          AND Room_Type__c = NULL
      ]) {
        revenueBidMap.put(revenueBid.Bid__c, revenueBid);
      }

      List<Revenue__c> revenueList = new List<Revenue__c>();
      Revenue__c revenueRecord;
      for (Housing__c roomType : roomTypeMap.values()) {
        if (
          revenueBidMap.get(roomType.Bid__c) != null &&
          revenueBidMap.get(roomType.Bid__c).Is_this_a_monthly_Pick_Up__c !=
          'Yes'
        ) {
          revenueRecord = revenueMap.get(roomType.Id) != null
            ? revenueMap.get(roomType.Id)
            : new Revenue__c();
          revenueRecord.Bid__c = roomType.Bid__c;
          revenueRecord.Room_Type__c = roomType.Id;
          revenueRecord.Comps__c = roomType.Comps__c;
          revenueRecord.Room_Type_Name__c = roomType.Unit_Type__c;
          revenueRecord.Room_Nights__c = roomType.Total_Room_Nights__c;
          revenueRecord.Rate_currency__c = roomType.Rate__c;
          revenueRecord.Confirmations__c = roomType.Confirmations__c;
          revenueRecord.Commission_Type__c = revenueBidMap.get(
              roomType.Bid__c
            ) != null
            ? revenueBidMap.get(roomType.Bid__c).Commission_Type__c
            : 'Amount';
          revenueRecord.Commission__c = revenueBidMap.get(roomType.Bid__c) !=
            null
            ? revenueBidMap.get(roomType.Bid__c).Commission__c
            : null;
          revenueRecord.Commission_Percent__c = revenueBidMap.get(
              roomType.Bid__c
            ) != null
            ? revenueBidMap.get(roomType.Bid__c).Commission_Percent__c
            : null;
          revenueRecord.Commission_Per_Room__c = roomType.Commission_Per_Room__c;
          revenueRecord.Date_In__c = bidMap.get(roomType.Bid__c) != null
            ? bidMap.get(roomType.Bid__c).Housing__r.Date_In__c
            : null;
          revenueRecord.Date_Out__c = bidMap.get(roomType.Bid__c) != null
            ? bidMap.get(roomType.Bid__c).Housing__r.Date_Out__c
            : null;
          revenueRecord.Stay_ID__c = bidMap.get(roomType.Bid__c) != null
            ? bidMap.get(roomType.Bid__c).Housing__r.Name
            : null;
          if (
            bidMap.get(roomType.Bid__c) != null &&
            bidMap.get(roomType.Bid__c).Vendor__r.ShippingCountry != null &&
            isEuropean(bidMap.get(roomType.Bid__c).Vendor__r.ShippingCountry)
          ) {
            revenueRecord.RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
              .get('Housing_Rate_Commission_RRE')
              .getRecordTypeId();
            revenueRecord.CurrencyIsoCode = 'EUR';
          } else {
            revenueRecord.RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
              .get('Housing_Rate_Commission_RRU')
              .getRecordTypeId();
            revenueRecord.CurrencyIsoCode = 'USD';
          }
          revenueList.add(revenueRecord);
        }
      }
      if (!revenueList.isEmpty())
        upsert revenueList;
    }
  }

  public static Boolean isEuropean(String country) {
    Set<String> countries = new Set<String>();
    countries.add('Albania');
    countries.add('Germany');
    countries.add('Andorra');
    countries.add('Armenia');
    countries.add('Austria');
    countries.add('Azerbaijan');
    countries.add('Belgium');
    countries.add('Belarus');
    countries.add('Bosnia and Herzegovina');
    countries.add('Bulgaria');
    countries.add('Cyprus');
    countries.add('Holy See (Vatican City State)');
    countries.add('Croatia');
    countries.add('Denmark');
    countries.add('Slovakia');
    countries.add('Slovenia');
    countries.add('Spain');
    countries.add('Estonia');
    countries.add('Finland');
    countries.add('France');
    countries.add('Georgia');
    countries.add('Greece');
    countries.add('Hungary');
    countries.add('Ireland');
    countries.add('Iceland');
    countries.add('Italy');
    countries.add('Kazakhstan');
    countries.add('Latvia');
    countries.add('Liechtenstein');
    countries.add('Lithuania');
    countries.add('Luxembourg');
    countries.add('Macedonia');
    countries.add('Malta');
    countries.add('Moldova');
    countries.add('Monaco');
    countries.add('Montenegro');
    countries.add('Norway');
    countries.add('Netherlands');
    countries.add('Poland');
    countries.add('Portugal');
    countries.add('United Kingdom');
    countries.add('Czech Republic');
    countries.add('Romania');
    countries.add('Russia');
    countries.add('San Marino');
    countries.add('Serbia');
    countries.add('Sweden');
    countries.add('Switzerland');
    countries.add('Turkey');
    countries.add('Ukraine');
    if (countries.contains(country))
      return true;

    return false;
  }

  public static void createTraces(
    Map<Id, Housing__c> oldHousingMap,
    Map<Id, Housing__c> housingMap
  ) {
    system.debug('housingmap ::: ' + housingMap);
    theHousingMap = housingMap;
    Set<Id> productions = new Set<Id>();
    Map<Id, Id> coordinators = new Map<Id, Id>();
    List<Task> traces = new List<Task>();
    Id recordTypeTT = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName()
      .get('Trace_Task')
      .getRecordTypeId();

    for (Housing__c housing : housingMap.values()) {
      system.debug('housing::: ' + housing);
      system.debug('trace date::: ' + housing.Trace_Date__c);
      system.debug('housing statis::: ' + housing.Status_CC__c);
      system.debug('housing::: ' + housing);
      system.debug('coordinators::: ' + coordinators);
      system.debug('oldHousingMap::: ' + oldHousingMap);

      if (
        (housing.RecordTypeId ==
        Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Hotel_Housing')
          .getRecordTypeId() ||
        housing.RecordTypeId ==
        Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Corporate_Housing')
          .getRecordTypeId() ||
        housing.RecordTypeId ==
        Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Individual_Reservation')
          .getRecordTypeId()) &&
        String.isNotEmpty(housing.Status_CC__c) &&
        (oldHousingMap == null &&
        housing.Trace_Date__c != null) ||
        (oldHousingMap == null &&
        housing.DeadLine_Date__c != null) ||
        (oldHousingMap == null &&
        housing.Status_CC__c != null) ||
        housing.Trace_Date__c !=
        oldHousingMap?.get(housing?.Id)?.Trace_Date__c ||
        housing.Trace_Date_Priority__c !=
        oldHousingMap?.get(housing?.Id)?.Trace_Date_Priority__c ||
        housing.Status_CC__c != oldHousingMap?.get(housing?.Id)?.Status_CC__c
      ) {
        system.debug('made it in housing trigger logic for traces');
        // this should hopefully stop dupe contract traces
        Set<String> theStatuses = TraceHelper.getTracesHousingAll();
        for (String s : theStatuses) {
          system.debug(s);
        }
        String theHousingStatus = String.valueOf(housing.Status_CC__c);
        system.debug('theHousingStatus :: ' + theHousingStatus);
        system.debug(
          'send to client? : ' + theStatuses.contains(theHousingStatus)
        );

        system.debug('thestatuses :: ' + JSON.serializePretty(theStatuses));
        if (
          theStatuses.contains(housing.Status_CC__c) &&
          housing.Status_CC__c != oldHousingMap?.get(housing?.Id)?.Status_CC__c
        ) {
          system.debug('made it in status not null');
          TraceHelper.updateTracesStatusUpdateHousing(
            housingMap.keySet(),
            housing.Status_CC__c,
            TraceHelper.getCoordinatorService(housing)
          );
        }

        TraceHelper.createTraceServiceStatus(housing, 'Housing__c');
      }
    }
  }
  //Fix By clay Dev 11 Feb, 2021 #176828479
  public static Set<String> fieldsNameToCopy = new Set<String>{
    'Deadline_Trace_Date__c',
    'Contracting_Requirements__c',
    'Hotel_Class__c',
    'Star_Preference__c',
    'Distance_to_Venue__c',
    'Brand_Preference__c'
  };

  public static void copyDetailsOnStays(
    Map<Id, Housing__c> oldHousingsMap,
    List<Housing__c> newList
  ) {
    if (recordTypeList.size() > 1) {
      String hotelHousingRecordTypeId = recordTypeList[0].Name ==
        'Hotel Housing'
        ? recordTypeList[0].Id
        : recordTypeList[1].Id;
      String salesHousingRecordTypeId = recordTypeList[0].Name ==
        'Sales Housing'
        ? recordTypeList[0].Id
        : recordTypeList[1].Id;

      Set<String> productionIdSet = new Set<String>();
      for (Housing__c housing : newList) {
        if (
          housing.RecordTypeId == salesHousingRecordTypeId &&
          housing.Production_CC__c != null
        ) {
          for (String field : fieldsNameToCopy) {
            if (
              housing.get(field) != oldHousingsMap.get(housing.Id).get(field) ||
              Test.isRunningTest()
            ) {
              productionIdSet.add(housing.Production_CC__c);
              break;
            }
          }
        }
      }
      if (productionIdSet.size() > 0) {
        List<Housing__c> stays = [
          SELECT Id, Production_CC__c, Status_CC__c
          FROM Housing__c
          WHERE
            RecordTypeId = :hotelHousingRecordTypeId
            AND Production_CC__c IN :productionIdSet
            AND Status_CC__c IN ('Itinerary Received', 'Tentative Dates')
        ];

        if (stays.size() > 0) {
          Map<String, List<Housing__c>> productionIdToHousingListMap = new Map<String, List<Housing__c>>();
          for (Housing__c stay : stays) {
            if (
              !productionIdToHousingListMap.containsKey(stay.Production_CC__c)
            ) {
              productionIdToHousingListMap.put(
                stay.Production_CC__c,
                new List<Housing__c>()
              );
            }
            productionIdToHousingListMap.get(stay.Production_CC__c).add(stay);
          }

          List<Housing__c> housingListToUpdate = new List<Housing__c>();
          Map<Id, Housing__c> housingMapToUpdate = new Map<Id, Housing__c>();
          for (Housing__c housing : newList) {
            if (
              productionIdToHousingListMap.containsKey(housing.Production_CC__c)
            ) {
              for (
                Housing__c stay : productionIdToHousingListMap.get(
                  housing.Production_CC__c
                )
              ) {
                for (String field : fieldsNameToCopy) {
                  if (
                    housing.get(field) !=
                    oldHousingsMap.get(housing.Id).get(field)
                  ) {
                    if (field.equalsIgnoreCase('Deadline_Trace_Date__c')) {
                      stay.put('Deadline_Date__c', housing.get(field));
                    } else {
                      stay.put(field, housing.get(field));
                    }
                  }
                }
                housingMapToUpdate.put(stay.Id, stay);
              }
            }
          }
          if (housingMapToUpdate.size() > 0) {
            update housingMapToUpdate.values();
          }
        }
      }
    }
  }

  public static void copyRoomTypeToOtherStay(
    Map<Id, Housing__c> oldHousingsMap,
    List<Housing__c> newList
  ) {
    if (recordTypeList.size() > 1) {
      String hotelHousingRecordTypeId, roomTypeRecordTypeId;
      for (RecordType rt : recordTypeList) {
        if (rt.Name == 'Hotel Housing') {
          hotelHousingRecordTypeId = rt.Id;
        } else if (rt.Name == 'Room Types & Ops') {
          roomTypeRecordTypeId = rt.Id;
        }
      }

      Set<String> productionIdSet = new Set<String>();
      for (Housing__c roomType : newList) {
        //Fix By Clay Dev 4 March, 2021 #177163455
        //if(roomType.RecordTypeId == roomTypeRecordTypeId && roomType.Production_CC__c != null && String.isBlank(roomType.Sales_Housing__c)) {
        if (
          roomType.RecordTypeId == roomTypeRecordTypeId &&
          roomType.Production_CC__c != null &&
          String.isBlank(roomType.Sales_Housing__c) &&
          String.isBlank(roomType.Bid__c)
        ) {
          productionIdSet.add(roomType.Production_CC__c);
        }
      }

      if (
        productionIdSet.size() > 0 &&
        String.isNotBlank(hotelHousingRecordTypeId)
      ) {
        //Fix By Clay Dev 4 March, 2021 #177163455 Added  AND Bid__c = null in query
        List<Housing__c> stays = [
          SELECT
            Id,
            Production_CC__c,
            Date_In__c,
            Date_Out__c,
            (
              SELECT Id, Unit_Type__c
              FROM Housing__r
              WHERE
                RecordTypeId = :roomTypeRecordTypeId
                AND Sales_Housing__c != NULL
                AND Bid__c = NULL
            )
          FROM Housing__c
          WHERE
            RecordTypeId = :hotelHousingRecordTypeId
            AND Production_CC__c IN :productionIdSet
            AND Status_CC__c IN ('Itinerary Received', 'Tentative Dates')
        ];

        if (stays.size() > 0) {
          Map<String, List<Housing__c>> productionIdToHousingListMap = new Map<String, List<Housing__c>>();
          Map<String, Map<String, String>> stayIdToRoomTypeToIdMap = new Map<String, Map<String, String>>();
          for (Housing__c stay : stays) {
            if (
              !productionIdToHousingListMap.containsKey(stay.Production_CC__c)
            ) {
              productionIdToHousingListMap.put(
                stay.Production_CC__c,
                new List<Housing__c>()
              );
            }
            productionIdToHousingListMap.get(stay.Production_CC__c).add(stay);

            Map<String, String> roomTypeToIdMap = new Map<String, String>();
            for (Housing__c housing : stay.Housing__r) {
              housing.Unit_Type__c = housing.Unit_Type__c != null
                ? housing.Unit_Type__c
                : '';
              roomTypeToIdMap.put(housing.Unit_Type__c.trim(), housing.Id);
            }
            stayIdToRoomTypeToIdMap.put(stay.Id, roomTypeToIdMap);
          }

          List<Housing__c> housingListToInsert = new List<Housing__c>();
          List<Housing__c> housingListToUpdate = new List<Housing__c>();
          List<Housing__c> housingListToDelete = new List<Housing__c>();

          for (Housing__c roomType : newList) {
            if (
              productionIdToHousingListMap.containsKey(
                roomType.Production_CC__c
              )
            ) {
              for (
                Housing__c stay : productionIdToHousingListMap.get(
                  roomType.Production_CC__c
                )
              ) {
                if (Trigger.isInsert) {
                  Housing__c newRTRec = roomType.clone();
                  newRTRec.Id = null;
                  newRTRec.Date_In__c = stay.Date_In__c;
                  newRTRec.Date_Out__c = stay.Date_Out__c;
                  newRTRec.Sales_Housing__c = stay.Id;
                  housingListToInsert.add(newRTRec);
                } else if (Trigger.isUpdate) {
                  String oldUnitType = oldHousingsMap.get(roomType.Id)
                    .Unit_Type__c;
                  if (oldUnitType == null) {
                    oldUnitType = '';
                  }
                  if (
                    stayIdToRoomTypeToIdMap.containsKey(stay.Id) &&
                    stayIdToRoomTypeToIdMap.get(stay.Id)
                      .containsKey(oldUnitType.trim())
                  ) {
                    Housing__c newRTRec = roomType.clone();
                    newRTRec.Id = stayIdToRoomTypeToIdMap.get(stay.Id)
                      .get(oldUnitType.trim());
                    newRTRec.Sales_Housing__c = stay.Id;
                    housingListToUpdate.add(newRTRec);
                  }
                } else if (Trigger.isDelete) {
                  String newUnitType = roomType.Unit_Type__c;
                  if (newUnitType == null) {
                    newUnitType = '';
                  }
                  if (
                    stayIdToRoomTypeToIdMap.containsKey(stay.Id) &&
                    stayIdToRoomTypeToIdMap.get(stay.Id)
                      .containsKey(newUnitType.trim())
                  ) {
                    Housing__c rtToDelete = new Housing__c();
                    rtToDelete.Id = stayIdToRoomTypeToIdMap.get(stay.Id)
                      .get(newUnitType.trim());
                    housingListToDelete.add(rtToDelete);
                  }
                }
              }
            }
          }
          ApexUtil.HousingTrigger_Is_Enabled = false;
          if (housingListToInsert.size() > 0) {
            insert housingListToInsert;
          }
          if (housingListToUpdate.size() > 0) {
            update housingListToUpdate;
          }
          if (housingListToDelete.size() > 0) {
            delete housingListToDelete;
          }
          ApexUtil.HousingTrigger_Is_Enabled = true;
        }
      }
    }
  }

  //Fix By clay Dev 17 Feb, 2021 #176993593
  public static void populateStartAndEndDate(List<Housing__c> newList) {
    List<RecordType> recordTypeList = [
      SELECT Id, Name
      FROM RecordType
      WHERE Name IN ('Room Types & Ops', 'Hotel Housing')
    ];
    if (recordTypeList.size() > 1) {
      String hotelHousingRecordTypeId, roomTypeRecordTypeId;
      for (RecordType rt : recordTypeList) {
        if (rt.Name == 'Hotel Housing') {
          hotelHousingRecordTypeId = rt.Id;
        } else if (rt.Name == 'Room Types & Ops') {
          roomTypeRecordTypeId = rt.Id;
        }
      }
      Set<String> hotelHousingIdSet = new Set<String>();
      Set<String> bidIdSet = new Set<String>();
      for (Housing__c roomType : newList) {
        if (
          roomType.RecordTypeId == roomTypeRecordTypeId &&
          roomType.Production_CC__c != null
        ) {
          if (String.isNotBlank(roomType.Sales_Housing__c)) {
            hotelHousingIdSet.add(roomType.Sales_Housing__c);
          } else if (String.isNotBlank(roomType.Bid__c)) {
            bidIdSet.add(roomType.Bid__c);
          }
        }
      }
      if (bidIdSet.size() > 0 || hotelHousingIdSet.size() > 0) {
        String query =
          'Select Id, Sales_Housing__c, Sales_Housing__r.Date_In__c,  Sales_Housing__r.Date_Out__c, ' +
          'Bid__r.Housing__c, Bid__r.Housing__r.Date_In__c, Bid__r.Housing__r.Date_Out__c, Date_In__c, ' +
          'Date_Out__c from Housing__c where RecordTypeId =: roomTypeRecordTypeId ';
        if (hotelHousingIdSet.size() > 0 && bidIdSet.size() == 0) {
          query += ' AND Sales_Housing__c IN :hotelHousingIdSet';
        } else if (bidIdSet.size() > 0 && hotelHousingIdSet.size() == 0) {
          query += ' AND Bid__c IN :bidIdSet';
        } else if (bidIdSet.size() > 0 && hotelHousingIdSet.size() > 0) {
          query += ' AND (Sales_Housing__c IN :hotelHousingIdSet OR Bid__c IN :bidIdSet)';
        } else {
          return;
        }

        List<Housing__c> roomTypeList = Database.query(query);
        Map<String, Housing__c> salesHousingIdToRecMap = new Map<String, Housing__c>();
        for (Housing__c rtRec : roomTypeList) {
          Housing__c salesHousingRec;
          if (rtRec.Bid__c != null && rtRec.Bid__r.Housing__c != null) {
            salesHousingRec = rtRec.Bid__r.Housing__r;
          } else if (rtRec.Sales_Housing__c != null) {
            salesHousingRec = rtRec.Sales_Housing__r;
          }
          if (salesHousingRec != null) {
            if (!salesHousingIdToRecMap.containsKey(salesHousingRec.Id)) {
              salesHousingRec.Date_In__c = salesHousingRec.Date_Out__c = null;
              salesHousingIdToRecMap.put(salesHousingRec.Id, salesHousingRec);
            }
            salesHousingRec = salesHousingIdToRecMap.get(salesHousingRec.Id);
            if (
              salesHousingRec.Date_In__c == null ||
              (rtRec.Date_In__c != null &&
              rtRec.Date_In__c < salesHousingRec.Date_In__c)
            ) {
              salesHousingRec.Date_In__c = rtRec.Date_In__c;
            }
            if (
              salesHousingRec.Date_Out__c == null ||
              (rtRec.Date_Out__c != null &&
              rtRec.Date_Out__c > salesHousingRec.Date_Out__c)
            ) {
              salesHousingRec.Date_Out__c = rtRec.Date_Out__c;
            }
            salesHousingIdToRecMap.put(salesHousingRec.Id, salesHousingRec);
          }
        }
        if (salesHousingIdToRecMap.size() > 0) {
          List<Itinerary__c> itineraryUpdateList = new List<Itinerary__c>();
          for (Itinerary__c itRec : [
            SELECT Id, Housing__c, Start_Date__c, End_Date__c
            FROM Itinerary__c
            WHERE Housing__c IN :salesHousingIdToRecMap.keySet()
          ]) {
            if (
              itRec.Start_Date__c !=
              salesHousingIdToRecMap.get(itRec.Housing__c).Date_In__c ||
              itRec.End_Date__c !=
              salesHousingIdToRecMap.get(itRec.Housing__c).Date_Out__c
            ) {
              itRec.Start_Date__c = salesHousingIdToRecMap.get(itRec.Housing__c)
                .Date_In__c;
              itRec.End_Date__c = salesHousingIdToRecMap.get(itRec.Housing__c)
                .Date_Out__c;
              itineraryUpdateList.add(itRec);
            }
          }
          ApexUtil.HousingTrigger_Is_Enabled = false;
          update salesHousingIdToRecMap.values();
          ApexUtil.HousingTrigger_Is_Enabled = true;

          if (itineraryUpdateList.size() > 0) {
            update itineraryUpdateList;
          }
        }
      }
    }
  }
}```

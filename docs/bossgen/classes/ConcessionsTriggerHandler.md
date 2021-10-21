---
layout: default
title: ConcessionsTriggerHandler
parent: classes
---
# Metadata Type
classes


# Filename 
ConcessionsTriggerHandler


# Raw XML
```
public with sharing class ConcessionsTriggerHandler implements ITriggerHandler {
  public static Boolean TriggerDisabled = false;

  public Boolean IsDisabled() {
    return !ApexUtil.ConcessionsTrigger_Is_Enabled;
  }

  public void BeforeInsert(List<SObject> newItems) {
  }

  public void BeforeUpdate(Map<Id, SObject> newItems, Map<Id, SObject> oldItems) {
  }

  public void BeforeDelete(Map<Id, SObject> oldItems) {
    Map<Id, Concessions__c> oldConcessionMap = (Map<Id, Concessions__c>) oldItems;

    copyConsessionToOtherStay(null, oldItems.values());
  }

  public void AfterInsert(Map<Id, SObject> newItems) {
    Map<Id, Concessions__c> newConcessionMap = (Map<Id, Concessions__c>) newItems;
    copyConsessionToOtherStay(null, newConcessionMap.values());
  }

  public void AfterUpdate(Map<Id, SObject> newItems, Map<Id, SObject> oldItems) {
    Map<Id, Concessions__c> oldConcessionMap = (Map<Id, Concessions__c>) oldItems;
    Map<Id, Concessions__c> newConcessionMap = (Map<Id, Concessions__c>) newItems;
    copyConsessionToOtherStay(oldConcessionMap, newConcessionMap.values());
  }

  public void AfterDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterUndelete(Map<Id, SObject> oldItems) {
  }

  /*

  public static void populateCongaFields(Map<Id, Concessions__c> oldConcessionsMap, List<Concessions__c> concessions) {
    Map<Id, Bid__c> bidsMap = new Map<Id, Bid__c>();
    Map<String, List<String>> ConcessionsRequestedMap = new Map<String, List<String>>();
    for (Concessions__c concession : concessions)
      if (
        (oldConcessionsMap == null &&
        String.isNotEmpty(concession.Bid__c) &&
        concession.Concession_Type__c == 'Corporate Housing' &&
        String.isNotEmpty(concession.Concessions_Requested__c)) ||
        (oldConcessionsMap != null &&
        (concession.Bid__c != oldConcessionsMap.get(concession.Id).Bid__c ||
        concession.Concessions_Requested__c != oldConcessionsMap.get(concession.Id).Concessions_Requested__c ||
        (concession.Concession_Type__c != oldConcessionsMap.get(concession.Id).Concession_Type__c &&
        (concession.Concession_Type__c == 'Corporate Housing' ||
        oldConcessionsMap.get(concession.Id).Concession_Type__c == 'Corporate Housing'))))
      )
        bidsMap.put(
          concession.Bid__c,
          new Bid__c(
            id = concession.Bid__c,
            Corporate_Concessions_Total_Conga__c = 0,
            Corporate_Concessions_Conga__c = ''
          )
        );
    if (!bidsMap.values().isEmpty()) {
      ConcessionsRequestedMap = MetadataHelper.getFieldDependencies(
        'Concessions__c',
        'Concessions_Requested__c',
        'Concession_Provided__c'
      );
      String concessionsProvided;
      for (Concessions__c concessionItem : [
        SELECT id, Bid__c, Concessions_Requested__c
        FROM Concessions__c
        WHERE
          Bid__c IN :bidsMap.keySet()
          AND Concession_Type__c = 'Corporate Housing'
          AND Concessions_Requested__c != NULL
        ORDER BY createdDate DESC
      ]) {
        bidsMap.get(concessionItem.Bid__c).Corporate_Concessions_Total_Conga__c++;
        concessionsProvided = '';
        if (ConcessionsRequestedMap.get(concessionItem.Concessions_Requested__c) != null)
          for (String concessionProvidedItem : ConcessionsRequestedMap.get(concessionItem.Concessions_Requested__c))
            concessionsProvided +=
              '<tr><td width="5" height="20"></td><td width="12" height="20"><table width="12" height="8" cellspacing="0" cellpadding="0" border="1"><tr><td></td></tr></table></td><td width="5" height="20"></td><td width="353" height="20" align="left">' +
              concessionProvidedItem +
              '</td></tr>';
        bidsMap.get(concessionItem.Bid__c).Corporate_Concessions_Conga__c +=
          (math.mod((Integer) bidsMap.get(concessionItem.Bid__c).Corporate_Concessions_Total_Conga__c, 2) != 0
            ? '<tr>'
            : '') +
          '<td width="50%" align="left" valign="top"><table width="100%" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="5" height="20"></th><th width="12" height="20"></th><th width="5" height="20"></th><th width="353" height="20" align="left">' +
          concessionItem.Concessions_Requested__c +
          '</tr></thead><tbody>' +
          concessionsProvided +
          '</tbody></table></td>' +
          (math.mod((Integer) bidsMap.get(concessionItem.Bid__c).Corporate_Concessions_Total_Conga__c, 2) == 0
            ? '</tr>'
            : '');
      }
      for (Bid__c bid : bidsMap.values())
        bid.Corporate_Concessions_Conga__c =
          '<table width="740" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle">' +
          bid.Corporate_Concessions_Conga__c +
          (math.mod((Integer) bid.Corporate_Concessions_Total_Conga__c, 2) != 0
            ? '<td width="50%" align="left" valign="top"></td></tr></table>'
            : '</table>');
      try {
        update bidsMap.values();
      } catch (DmlException e) {
        System.debug('ConcessionsTriggerHandler - DmlException: ' + e.getMessage());
      }
    }
  }

  */

  //Fix By clay Dev 11 Feb, 2021 #176828479
  public static void copyConsessionToOtherStay(
    Map<Id, Concessions__c> oldConcessionsMap,
    List<Concessions__c> concessions
  ) {
    Set<String> productionIdSet = new Set<String>();
    for (Concessions__c concession : concessions) {
      if (
        concession.Concession_Type__c == 'Housing' &&
        concession.Production__c != null &&
        concession.Housing__c == null &&
        concession.Bid__c == null &&
        concession.Air__c == null &&
        concession.Freight__c == null
      ) {
        productionIdSet.add(concession.Production__c);
      }
    }
    if (productionIdSet.size() > 0) {
      List<RecordType> salesHousingRecordType = [SELECT Id FROM RecordType WHERE Name = 'Hotel Housing'];
      List<Housing__c> stays = new List<Housing__c>();

      if (salesHousingRecordType.size() > 0) {
        stays = [
          SELECT Id, Production_CC__c, (SELECT Id, Concessions_Requested__c FROM Concessions__r)
          FROM Housing__c
          WHERE
            RecordTypeId = :salesHousingRecordType[0].Id
            AND Production_CC__c IN :productionIdSet
            AND Status_CC__c IN ('Itinerary Received', 'Tentative Dates')
        ];

        if (stays.size() > 0) {
          Map<String, List<Housing__c>> productionIdToHousingListMap = new Map<String, List<Housing__c>>();
          Map<String, Map<String, String>> stayIdToConsessionRequestedToIdMap = new Map<String, Map<String, String>>();
          for (Housing__c stay : stays) {
            if (!productionIdToHousingListMap.containsKey(stay.Production_CC__c)) {
              productionIdToHousingListMap.put(stay.Production_CC__c, new List<Housing__c>());
            }
            productionIdToHousingListMap.get(stay.Production_CC__c).add(stay);

            Map<String, String> concessionRequestedToIdMap = new Map<String, String>();
            for (Concessions__c concession : stay.Concessions__r) {
              concession.Concessions_Requested__c = concession.Concessions_Requested__c == null
                ? ''
                : concession.Concessions_Requested__c;
              concessionRequestedToIdMap.put(concession.Concessions_Requested__c.trim(), concession.Id);
            }
            stayIdToConsessionRequestedToIdMap.put(stay.Id, concessionRequestedToIdMap);
          }

          List<Concessions__c> concessionListToInsert = new List<Concessions__c>();
          List<Concessions__c> concessionListToUpdate = new List<Concessions__c>();
          List<Concessions__c> concessionListToDelete = new List<Concessions__c>();

          for (Concessions__c concession : concessions) {
            if (productionIdToHousingListMap.containsKey(concession.Production__c)) {
              for (Housing__c stay : productionIdToHousingListMap.get(concession.Production__c)) {
                if (Trigger.isInsert) {
                  Concessions__c cxAux = concession.clone();
                  cxAux.Id = null;
                  cxAux.Housing__c = stay.Id;
                  concessionListToInsert.add(cxAux);
                } else if (Trigger.isUpdate) {
                  String oldConcessionRequested = oldConcessionsMap.get(concession.Id).Concessions_Requested__c;
                  oldConcessionRequested = oldConcessionRequested == null ? '' : oldConcessionRequested;
                  if (
                    stayIdToConsessionRequestedToIdMap.containsKey(stay.Id) &&
                    stayIdToConsessionRequestedToIdMap.get(stay.Id).containsKey(oldConcessionRequested.trim())
                  ) {
                    Concessions__c cxAux = concession.clone();
                    cxAux.Id = stayIdToConsessionRequestedToIdMap.get(stay.Id).get(oldConcessionRequested.trim());
                    cxAux.Housing__c = stay.Id;
                    concessionListToUpdate.add(cxAux);
                  }
                } else if (Trigger.isDelete) {
                  String newConcessionRequested = concession.Concessions_Requested__c;
                  newConcessionRequested = newConcessionRequested == null ? '' : newConcessionRequested;
                  if (
                    stayIdToConsessionRequestedToIdMap.containsKey(stay.Id) &&
                    stayIdToConsessionRequestedToIdMap.get(stay.Id).containsKey(newConcessionRequested.trim())
                  ) {
                    Concessions__c cxAux = new Concessions__c();
                    cxAux.Id = stayIdToConsessionRequestedToIdMap.get(stay.Id).get(newConcessionRequested.trim());
                    concessionListToDelete.add(cxAux);
                  }
                }
              }
            }
          }
          if (concessionListToInsert.size() > 0) {
            insert concessionListToInsert;
          }
          if (concessionListToUpdate.size() > 0) {
            update concessionListToUpdate;
          }
          if (concessionListToDelete.size() > 0) {
            delete concessionListToDelete;
          }
        }
      }
    }
  }
}
```


# Last Modified


# Usage

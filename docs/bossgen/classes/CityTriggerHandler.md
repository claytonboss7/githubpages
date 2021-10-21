---
layout: default
title: CityTriggerHandler
parent: classes
---
# Metadata Type
classes


# Filename 
CityTriggerHandler


# Raw XML
```
/**
 * @description       : city trigger handler
 * @author            : sfdc cb
 * @group             : triggerhandlers
 * @last modified on  : 09-07-2021
 * @last modified by  : sfdc cb
 **/
public class CityTriggerHandler implements ITriggerHandler {
  public static Boolean TriggerDisabled = false;

  public Boolean IsDisabled() {
    return !ApexUtil.CityTrigger_Is_Enabled;
  }

  public void BeforeInsert(List<SObject> newItems) {
  }

  public void BeforeUpdate(
    Map<Id, SObject> newItems,
    Map<Id, SObject> oldItems
  ) {
  }

  public void BeforeDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterInsert(Map<Id, SObject> newItems) {
    Map<Id, City__c> cityMap = (Map<Id, City__c>) newItems;
    doGoogleAndSabreIntegration(null, cityMap);
  }

  public void AfterUpdate(
    Map<Id, SObject> newItems,
    Map<Id, SObject> oldItems
  ) {
    Map<Id, City__c> cityMap = (Map<Id, City__c>) newItems;
    Map<Id, City__c> oldCityMap = (Map<Id, City__c>) oldItems;
    doGoogleAndSabreIntegration(oldCityMap, cityMap);
  }

  public void AfterDelete(Map<Id, SObject> oldItems) {
  }

  public void AfterUndelete(Map<Id, SObject> oldItems) {
  }

  /**
   * @description calls the Google distance integration and the sabre integration on the change of a City State or Country
   * @param  oldItems passed in from insert/update .. is null on insert
   * @param  newItems passed in from insert/update .. if value exists in insert trigger on new items it is a candididate
   */
  public void doGoogleAndSabreIntegration(
    Map<Id, City__c> oldItems,
    Map<Id, City__c> newItems
  ) {
    Set<Id> cityIds = new Set<Id>();
    Set<Id> cityForSabreIds = new Set<Id>();

    if (oldItems != null) {
      for (City__c c : newItems.values()) {
        if (
          c.City__c != oldItems.get(c.Id).City__c ||
          c.State__c != oldItems.get(c.Id).State__c ||
          c.Country__c != oldItems.get(c.Id).Country__c
        ) {
          cityIds.add(c.Id);
        }
        if (c.City__c != oldItems.get(c.Id).City__c)
          cityForSabreIds.add(c.Id);
      }
    } else {
      for (City__c c : newItems.values()) {
        if (c.City__c != null || c.State__c != null || c.Country__c != null) {
          cityIds.add(c.Id);
        }
        if (c.City__c != null)
          cityForSabreIds.add(c.Id);
      }
    }

    if (cityIds.size() > 0 && !Test.isRunningTest())
      GoogleConnection.ping(cityIds);
    if (cityForSabreIds.size() > 0 && !Test.isRunningTest())
      Database.executeBatch(new SabreCityBatch(cityForSabreIds), 10);
  }
}
```


# Last Modified


# Usage

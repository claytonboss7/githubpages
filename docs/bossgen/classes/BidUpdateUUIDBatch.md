---
layout: default
title: BidUpdateUUIDBatch
parent: classes
---
# Metadata Type
classes


# Filename 
BidUpdateUUIDBatch


# Raw XML
```
/**
 * @description       : batch class to process bids and add the UUID for the landing page for older bids
 * @author            : sfdc cb
 * @group             : landing page
 * @last modified on  : 10-04-2021
 * @last modified by  : sfdc cb
**/

global class BidUpdateUUIDBatch implements Database.Batchable<sObject>, Database.AllowsCallouts {
    public String theQuery { get; set; }
  
    public BidUpdateUUIDBatch(String query) {
      theQuery = query;
    }

    global Database.QueryLocator start(Database.BatchableContext jobId) {
      return Database.getQueryLocator(theQuery);
    }
  
    global void execute(Database.BatchableContext jobId, List<sObject> recordList) {

        Bid__c[] bidsToUpdate = (Bid__c[]) recordList;

        for (Bid__c bid : bidsToUpdate) {
            bid.UUID_for_Landing_Page__c = ApexUtil.mkUuid();
        }

        try {
            ApexUtil.BidTrigger_Is_Enabled = false;
            update bidsToUpdate;
        } catch (Exception e){
            system.debug ('error updating the bids');
        }
      
    }
  
    global void finish(Database.BatchableContext jobIdParam) {
    }
  }
```


# Last Modified


# Usage

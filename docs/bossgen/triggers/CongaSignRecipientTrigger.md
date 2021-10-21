---
layout: default
title: CongaSignRecipientTrigger
parent: triggers
---
# Metadata Type
triggers


# Filename 
CongaSignRecipientTrigger


# Raw XML
```
trigger CongaSignRecipientTrigger on APXT_CongaSign__Recipient__c (after insert, after update){
    if(ApexUtil.CongaSignRecipientTrigger_Is_Enabled){
        if(trigger.isInsert){
        }
        else if(trigger.isUpdate){
            CongaSignRecipientTriggerHandler.updateCongaSignRecipients(trigger.oldMap, trigger.newMap);
            CongaSignRecipientTriggerHandler.createJournalEntries(trigger.oldMap, trigger.newMap);
        }
    }        
}
```


# Last Modified


# Usage

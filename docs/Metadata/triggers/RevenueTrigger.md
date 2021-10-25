---
layout: default
title: RevenueTrigger
parent: triggers
grand_parent: Metadata
---
# Metadata Type
triggers


# Filename 
RevenueTrigger


# Raw XML
```
trigger RevenueTrigger on Revenue__c (before insert, before update, after insert, after update, before delete) {
    if(ApexUtil.RevenueTrigger_Is_Enabled){
        if(trigger.isBefore){
            if(trigger.isInsert){
                RevenueTriggerHandler.populateFields(null, trigger.new);
            }
            else if(trigger.isUpdate){
                RevenueTriggerHandler.populateFields(trigger.oldMap, trigger.new);
            }
            else if(trigger.isDelete){
                for(Revenue__c revenue : trigger.old){
                    if(revenue.Sync_to_QB__c == true || revenue.Invoiced__c == true) revenue.addError('You can not delete a record that is already invoiced in accounting');
                }
            }
        }
        else{
            if(trigger.isInsert){
                RevenueTriggerHandler.afterActions(null, trigger.new);
            }
            else if(trigger.isUpdate){
                RevenueTriggerHandler.afterActions(trigger.oldMap, trigger.new);
            }
        }
    }
}
```


# Last Modified


# Usage

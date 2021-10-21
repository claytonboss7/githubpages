---
layout: default
title: GroundTrigger
parent: triggers
---
# Metadata Type
triggers


# Filename 
GroundTrigger


# Raw XML
```
trigger GroundTrigger on Ground__c (before insert, before update, after insert, after update, after delete){
    if(trigger.isBefore){
        if(trigger.isInsert){
            GroundTriggerHandler.populateFields(null, trigger.new);
        }
        else if(trigger.isUpdate){
            GroundTriggerHandler.populateFields(trigger.oldMap, trigger.new);
        }
    }
    else{
        if(trigger.isInsert){
            GroundTriggerHandler.populateCongaFields(null, trigger.new);
            GroundTriggerHandler.createTraces(null, trigger.newMap);
        }
        else if(trigger.isUpdate){
            GroundTriggerHandler.populateCongaFields(trigger.oldMap, trigger.new);
            GroundTriggerHandler.createJournals(trigger.oldMap,trigger.new);
            GroundTriggerHandler.createTraces(trigger.oldMap, trigger.newMap);
        }
        else if(trigger.isDelete){
            GroundTriggerHandler.populateCongaFields(null, trigger.old);
        }
    }
}
```


# Last Modified


# Usage

---
layout: default
title: JournalTrigger
parent: triggers
---

```trigger JournalTrigger on Journal__c (after insert, after update) {
    Set<Id> journalIds = new Set<Id>();
    if(trigger.isInsert){
        for(Journal__c j : trigger.new){
            if(j.Journal_Entry__c != null) journalIds.add(j.Id);
        }
    }else{
        for(Journal__c j : trigger.new){
            if(j.Journal_Entry__c != trigger.oldMap.get(j.Id).Journal_Entry__c) journalIds.add(j.Id);
        }
    }
    
    if(!journalIds.isEmpty()) update [SELECT Id FROM Related_Contact__c WHERE Journal__c IN: journalIds];
}```

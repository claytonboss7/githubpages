---
layout: default
title: JournalCreation
parent: classes
---

```global class JournalCreation {
    
    global static void insertJournal(List<JournalEntry> entries){
        Journal__c newJournal;
        List<Journal__c> newJournalList = new List<Journal__c>();
        for(JournalEntry je : entries){
            newJournal = new Journal__c(
                RecordTypeId = je.record_type,
                Housing__c = (je.obj == 'housing' ? je.obj_id : null),
                G__c = (je.obj == 'ground' ? je.obj_id : null),
                Bid__c = (je.obj == 'bid' ? je.obj_id : null),
                Journal_Entry__c = je.entry
            );
            newJournalList.add(newJournal);
        }
        insert newJournalList;
    }
    
    global class JournalEntry{
        public String obj;
        public String obj_id;
        public String record_type;
        public String entry;
        
        global JournalEntry(String vobj, String vobj_id, String vrecord_type, String ventry){
            obj = vobj;
            obj_id = vobj_id;
            record_type = vrecord_type;
            entry = ventry;
        }
    }
}```

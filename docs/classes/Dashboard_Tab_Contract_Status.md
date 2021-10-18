---
layout: default
title: Dashboard_Tab_Contract_Status
parent: classes
---

```global class Dashboard_Tab_Contract_Status {
    public String bidContractId {get;set;}
    public String statusTaskId {get;set;}
    public String statusFlag {get;set;}
    public Date statusTraceDate {get;set;}
    public String relativeParentSObjectName {get;set;}
    public String opportunityId {get;set;}
    public Ground__c bidOutDate {get;set;}
    public List<SelectOption> finalstatusPL {get;set;}
    public Bid__c bidContract {
        set;
        get {
            if(bidContract == null) bidContract = new Bid__c();
            return bidContract;
        }
    }
    public Integer tracesCount {
        set;
        get {
            if(tracesCount == null) tracesCount = 0;
            return tracesCount;
        }
    }
    public Map<Id,String> traceSubjects {get;set;}
    public List<Dashboard_Tab_Contract_Status.TaskWrapper> contractTraceList1 {get;set;}
    public List<Dashboard_Tab_Contract_Status.TaskWrapper> contractTraceList2 {get;set;}

    public void loadTraces() {
        traceSubjects = new Map<Id,String>();
        bidOutDate = new Ground__c();
        switch on relativeParentSObjectName {
            when 'Ground' {
                List<Bid__c> searchBid = [SELECT GT__r.End_Date__c FROM Bid__c WHERE Id = :bidContractId AND GT__c <> NULL LIMIT 1];
                if(!searchBid.isEmpty()) bidOutDate = new Ground__c(End_Date__c = searchbid.get(0).GT__r.End_Date__c);
            }
            when 'Freight' {
                List<Bid__c> searchBid = [SELECT Freight__r.End_Date__c FROM Bid__c WHERE Id = :bidContractId AND Freight__c <> NULL LIMIT 1];
                if(!searchBid.isEmpty()) bidOutDate = new Ground__c(End_Date__c = searchbid.get(0).Freight__r.End_Date__c);
            }
            when 'Air' {
                List<Bid__c> searchBid = [SELECT Air__r.Return_Date__c FROM Bid__c WHERE Id = :bidContractId AND Air__c <> NULL LIMIT 1];
                if(!searchBid.isEmpty()) bidOutDate = new Ground__c(End_Date__c = searchbid.get(0).Air__r.Return_Date__c);
            }
        }
        tracesCount = 0;
        contractTraceList1 = new List<Dashboard_Tab_Contract_Status.TaskWrapper>();
        contractTraceList2 = new List<Dashboard_Tab_Contract_Status.TaskWrapper>();
        //Fix By Clay Dev 9 Feb, 2021 #176645471 
        //List<Task> contractTraces = [SELECT Id, OwnerId, Subject, Status, ActivityDate, Priority, Order__c FROM Task WHERE WhatId = :bidContractId AND Contract_Task__c = true ORDER BY Order__c ASC];
        List<Task> contractTraces = [SELECT Id, OwnerId, Subject, Status, ActivityDate, Priority, Order__c FROM Task WHERE WhatId = :bidContractId ORDER BY Order__c ASC];
        if(!contractTraces.isEmpty()){
            //Fix By Clay Dev 9 Feb, 2021 #176645471 
            //for(tracesCount = 0; tracesCount < (contractTraces.size()/2)-1; tracesCount++) contractTraceList1.add(new Dashboard_Tab_Contract_Status.TaskWrapper(contractTraces.get(tracesCount),contractTraces.get(tracesCount).Id, contractTraces.get(tracesCount).Priority, contractTraces.get(tracesCount).Subject, contractTraces.get(tracesCount).ActivityDate, ((contractTraces.get(tracesCount).Status.equals('Completed'))? true : false), false));
            //for(tracesCount = tracesCount; tracesCount < contractTraces.size(); tracesCount++) contractTraceList2.add(new Dashboard_Tab_Contract_Status.TaskWrapper(contractTraces.get(tracesCount),contractTraces.get(tracesCount).Id, contractTraces.get(tracesCount).Priority, contractTraces.get(tracesCount).Subject, contractTraces.get(tracesCount).ActivityDate, ((contractTraces.get(tracesCount).Status.equals('Completed'))? true : false), false));
        	
            Integer halfListSize = Math.Mod(contractTraces.size(), 2) > 0 ? contractTraces.size()/2 + 1 : contractTraces.size()/2;
            for(tracesCount = 0; tracesCount < halfListSize; tracesCount++) contractTraceList1.add(new Dashboard_Tab_Contract_Status.TaskWrapper(contractTraces.get(tracesCount),contractTraces.get(tracesCount).Id, contractTraces.get(tracesCount).Priority, contractTraces.get(tracesCount).Subject, contractTraces.get(tracesCount).ActivityDate, ((contractTraces.get(tracesCount).Status.equals('Completed'))? true : false), false));
            for(tracesCount = halfListSize; tracesCount < contractTraces.size(); tracesCount++) contractTraceList2.add(new Dashboard_Tab_Contract_Status.TaskWrapper(contractTraces.get(tracesCount),contractTraces.get(tracesCount).Id, contractTraces.get(tracesCount).Priority, contractTraces.get(tracesCount).Subject, contractTraces.get(tracesCount).ActivityDate, ((contractTraces.get(tracesCount).Status.equals('Completed'))? true : false), false));
        }
        for(Task trace : contractTraces) traceSubjects.put(trace.Id,trace.Subject);
        finalstatusPL = new List<SelectOption>();
        finalstatusPL.addAll(GTDashboardController.PickThePicklist('Bid__c','Final_Status__c'));
        bidContract = String.isNotEmpty(bidContractId) ? [SELECT Id, Final_Status__c FROM Bid__c WHERE Id =: bidContractId] : new Bid__c();
    }
    
    public void changeDoneStatus() {
        update new Task(Id = statusTaskId, Status = 'Completed', ActivityDate = null);
        String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Bid_Journal').getRecordTypeId();
        JournalCreation.insertJournal(new List<JournalCreation.JournalEntry>{new JournalCreation.JournalEntry('bid',bidContractId,bidJournalRT,traceSubjects.get(statusTaskId)+' trace is complete.')});
        loadTraces();
    }
    
    public void changeFollowStatus() {
        String newFollowStatus = statusFlag;
        switch on statusFlag {
            when 'No Follow up' { newFollowStatus = 'Normal Follow up'; }
            when 'Normal Follow up' { newFollowStatus = 'Urgent Follow Up'; }
            when 'Urgent Follow Up' { newFollowStatus = 'No Follow up'; }
        }
        update new Task(Id = statusTaskId, Priority = newFollowStatus);
        loadTraces();
    }
    
    @RemoteAction
    global static String validateDates(String d, String outDate, String traceParentSObject){
        Date todayDate = system.today();
        if(d != null && d != ''){
            if(parseDate(d) == null) return 'Please use a valid date';
            else{
                if(traceParentSObject != 'Air'){
                    if(parseDate(d) < todayDate) return 'Dates before today are not allowed';
                    if(parseDate(d) > parseDate(outDate)) return 'Dates after the '+traceParentSObject + (traceParentSObject == 'Housing' ? ' date out' : ' end date') +' are not allowed';
                }
            }
        }
        return '';
    }
    
    public static Date parseDate(String inDate){
        Date dateRes = null;
        //	1 - Try locale specific mm/dd/yyyy or dd/mm/yyyy	
        try {
            String candDate	= inDate.substring(0,Math.min(10,inDate.length()));// grab date portion only m[m]/d[d]/yyyy , ignore time
            dateRes	= Date.parse(candDate);
        }
        catch (Exception e){}        
        if(dateRes == null){
            //	2 - Try yyyy-mm-dd			
            try{
                String candDate	= inDate.substring(0,10);// grab date portion only, ignore time, if any
                dateRes	= Date.valueOf(candDate);
            }
            catch (Exception e){} 
        }
        return dateRes;
    }
    
    public void updateStatusTraceDate() {
        update new Task(Id = statusTaskId, ActivityDate = statusTraceDate, Status = 'Open');
        switch on relativeParentSObjectName {
            when 'Air' {
                List<Bid__c> searchBid = [SELECT Air_Charter__c FROM Bid__c WHERE Id =:bidContractId LIMIT 1];
                if(!searchBid.isEmpty() && !searchBid[0].Air_Charter__c && traceSubjects.containsKey(statusTaskId)){
                    if(traceSubjects.get(statusTaskId) == 'Contract Due Date') update new Bid__c(id = searchBid[0].id, Client_Contract_Date__c = statusTraceDate != null && String.valueOf(statusTraceDate) != '' ? statusTraceDate : null);
                    else if(traceSubjects.get(statusTaskId) == 'Deposit Due') update new Bid__c(id = searchBid[0].id, Client_Deposit_Due_Date__c = statusTraceDate != null && String.valueOf(statusTraceDate) != '' ? statusTraceDate : null);
                    else if(traceSubjects.get(statusTaskId) == 'Utilization Date') update new Bid__c(id = searchBid[0].id, Client_Utilization_Date__c = statusTraceDate != null && String.valueOf(statusTraceDate) != '' ? statusTraceDate : null);
                    else if(traceSubjects.get(statusTaskId) == 'Names & Final Payment Due') update new Bid__c(id = searchBid[0].id, Client_Names_Final_Payment__c = statusTraceDate != null && String.valueOf(statusTraceDate) != '' ? statusTraceDate : null);
                }
            }
        }
        String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Bid_Journal').getRecordTypeId();
        if(statusTraceDate != null && String.valueOf(statusTraceDate) != '') JournalCreation.insertJournal(new List<JournalCreation.JournalEntry>{new JournalCreation.JournalEntry('bid',bidContractId,bidJournalRT,traceSubjects.get(statusTaskId)+' trace date changed to '+(Datetime.newInstance(statusTraceDate, Time.newInstance(0,0,0,0))).format('dd-MMM-YYYY')+'.')});
        loadTraces();
    }
    
    public class TaskWrapper {
        public Task obj {get;set;}
        public String taskId {get;set;}
        public String priority {get;set;}
        public String subject {get;set;}
        public Date taskDate {get;set;}        
        public Boolean isDone {get;set;}
        public Boolean isDateAfterOutAllowed {get;set;}
        
        public TaskWrapper(Task obj, String taskId, String priority, String subject, Date taskDate, Boolean isDone, Boolean isDateAfterOutAllowed) {
            this.obj = obj;
            this.taskId = taskId;
            this.priority = priority;
            this.subject = subject;
            this.taskDate = taskDate;
            this.isDone = isDone;
            this.isDateAfterOutAllowed = isDateAfterOutAllowed;
        }
    }
}```

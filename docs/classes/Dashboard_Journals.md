---
layout: default
title: Dashboard_Journals
parent: classes
---

```public class Dashboard_Journals {
    public String relativeRecordId {get;set;}
    public String relativeSObjectName {get;set;}
    public String opportunityId {get;set;}
    public String journalModalAction {get;set;}
    public String journalId {get;set;}
    public String journalParentId {get;set;}
    public Boolean useIssueFilter {get;set;}
    public Boolean useSalesFilter {get;set;}
    public String keyWord {get;set;}
    public Journal__c journal {get;set;}
    public Journal__c journalParent {get;set;}
    public String journalJSON {get;set;}
    public Set<String> journalCompanies {get;set;}
    public Set<String> journalContacts {get;set;}
    public Set<String> journalCompanyContacts {get;set;}
    public List<Journal__c> journalMasterList {get;set;}
    public Map<Id,List<Journal__c>> journalChildMap {get;set;}
    public String productionType {get;set;}
    
    public void loadJournals() {
        System.debug('Loading journals...');
        if(useIssueFilter == null) useIssueFilter = false;
        if(useSalesFilter == null) useSalesFilter = false;
        journalModalAction = 'Create';
        journal = new Journal__c();
        journalParent = new Journal__c();
        journalCompanies = new Set<String>();
        journalContacts = new Set<String>();
        journalCompanyContacts = new Set<String>();
        journalMasterList = new List<Journal__c>();
        journalChildMap = new Map<Id,List<Journal__c>>();
        List<Journal__c> journalListMasterAux;
        List<Journal__c> journalListChildAux;
        Set<String> journalIds = new Set<String>();
        Boolean addJournal1;
        Boolean addJournal2;
        Boolean addJournal3;
        switch on relativeSObjectName {
            when 'Production'{
                journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c
                                        FROM Journal__c WHERE Production__c = :relativeRecordId AND RecordType.DeveloperName = 'Journal' AND Parent_Journal__c = null 
                                        AND Bid__c = null AND Housing__c = null AND G__c = null AND Air__c = null AND Freight__c = null
                                        ORDER BY CreatedDate DESC];
            }
            when 'Bid' { 
                Bid__c objAux = [SELECT Id, RecordType.DeveloperName, GT__c, Air__c, Freight__c FROM Bid__c WHERE Id =: relativeRecordId];
                if(objAux.RecordType.DeveloperName == 'GT_Bid'){
                    journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c 
                                            WHERE ((Bid__c = :relativeRecordId AND RecordType.Name = 'Bid Journal') OR (G__c =: objAux.GT__c AND RecordType.Name <> 'Bid Journal')) AND Parent_Journal__c = null ORDER BY CreatedDate DESC];
                }else if(objAux.RecordType.DeveloperName == 'Freight_Bid'){
                    journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c 
                                            WHERE ((Bid__c = :relativeRecordId AND RecordType.Name = 'Bid Journal') OR (Freight__c =: objAux.Freight__c AND RecordType.Name <> 'Bid Journal')) AND Parent_Journal__c = null ORDER BY CreatedDate DESC];
                }else if(objAux.RecordType.DeveloperName == 'Air_Bid'){
                    journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c 
                                            WHERE ((Bid__c = :relativeRecordId AND RecordType.Name = 'Bid Journal') OR (Air__c =: objAux.Air__c AND RecordType.Name <> 'Bid Journal')) AND Parent_Journal__c = null ORDER BY CreatedDate DESC];
                }else{
                    journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c WHERE Bid__c = :relativeRecordId AND RecordType.Name = 'Bid Journal' AND Parent_Journal__c = null ORDER BY CreatedDate DESC];
                }
            }
            when 'Housing' { journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c WHERE Housing__c = :relativeRecordId AND RecordType.Name <> 'Bid Journal' AND Parent_Journal__c = null ORDER BY CreatedDate DESC]; }
            when 'Ground','GCQ' { journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c WHERE G__c = :relativeRecordId AND RecordType.Name <> 'Bid Journal' AND Parent_Journal__c = null ORDER BY CreatedDate DESC]; }
            when 'FCQ' { journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c WHERE Freight__c = :relativeRecordId AND RecordType.DeveloperName = 'FCQ_Journal' AND Parent_Journal__c = null ORDER BY CreatedDate DESC]; }
        	when 'ACQ' { journalListMasterAux = [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c WHERE Air__c = :relativeRecordId AND RecordType.DeveloperName = 'GCQ_Journal' AND Parent_Journal__c = null ORDER BY CreatedDate DESC]; }
        }
        for(Journal__c j : journalListMasterAux) {
            addJournal1 = true;
            addJournal2 = true;
            addJournal3 = true;
            if(!useSalesFilter && useIssueFilter && !j.Issue__c) addJournal1 = false;
            if(!useIssueFilter && useSalesFilter && !j.Sales__c) addJournal2 = false;
            if(String.isNotBlank(keyWord) && String.isNotBlank(j.Journal_Entry__c) && !j.Journal_Entry__c.toLowerCase().contains(keyWord.toLowerCase())) addJournal3 = false;

            if(addJournal1 && addJournal2 && addJournal3){
                journalMasterList.add(j);
                journalIds.add(j.Id);
            }
        }
        for(Journal__c j : [SELECT Id, Name, Production__c, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, Bid__c, Housing__c, G__c, Air__c, Freight__c, Parent_Journal__c FROM Journal__c WHERE Parent_Journal__c IN: journalIds ORDER BY CreatedDate DESC]) {
            if(journalChildMap.containsKey(j.Parent_Journal__c)) { journalListChildAux = journalChildMap.get(j.Parent_Journal__c); journalListChildAux.add(j); journalChildMap.put(j.Parent_Journal__c,journalListChildAux.clone()); }
            else { journalListChildAux = new List<Journal__c>();  journalListChildAux.add(j); journalChildMap.put(j.Parent_Journal__c,journalListChildAux.clone()); }
        }
        for(Journal__c j : journalMasterList) if(!journalChildMap.containsKey(j.Id)) journalChildMap.put(j.Id,new List<Journal__c>());
    }
    
    public void openJournal() {
        journalModalAction = 'Create';
        journal = new Journal__c();
        journalParent = new Journal__c();
        journalCompanies = new Set<String>();
        journalContacts = new Set<String>();
        journalCompanyContacts = new Set<String>();
        if(String.isNotBlank(journalId)) {
            List<Journal__c> searchJournal = [SELECT 	Id, Name, RecordTypeId, RecordType.Name, Issue__c, Client_Retention_CR__c, Sales__c, Alert_all_coordinators__c, Mark_Journal_trace_complete__c, 
                                              			Production_checkbox__c, Vendor_Checkbox__c, Trace_Date__c, Trace_Date_Formula__c, Journal_Entry__c, Vendor__c, Air__c, Bid__c, Freight__c, G__c,
                                              			Housing__c, Parent_Journal__c, Production__c, Trace_Coordinator__c, Task_ID__c, CreatedBy.Name
                                              FROM Journal__c 
                                              WHERE Id = :journalId 
                                              LIMIT 1];
            if(!searchJournal.isEmpty()) {
                journal = searchJournal.get(0);
                //for(Related_Companies__c rc : [SELECT Id, Company__c FROM Related_Companies__c WHERE Journal__c =: journal.Id AND Company__c <> null]) journalCompanies.add(rc.Company__c);
                for(Related_Contact__c rc : [SELECT Id, Contact__c FROM Related_Contact__c WHERE Journal__c =: journal.Id AND Contact__c <> null AND Type__c includes ('Production Contacts')]) journalContacts.add(rc.Contact__c);
                for(Related_Contact__c rc : [SELECT Id, Contact__c FROM Related_Contact__c WHERE Journal__c =: journal.Id AND Contact__c <> null AND Type__c includes ('Company Contacts')]) journalCompanyContacts.add(rc.Contact__c);
            } else {
                journalId = '';
                loadJournals();
            }
            journalModalAction = 'Edit';
        }
        System.debug('journalId -> '+journalId);
    }
    
    public void openJournalReply() {
        journal = new Journal__c();
        journalCompanies = new Set<String>();
        journalContacts = new Set<String>();
        journalCompanyContacts = new Set<String>();
        if(String.isNotBlank(journalParentId)) {
            System.debug(journalParentId);
            List<Journal__c> searchParentJournal = [SELECT Id, Name, Journal_Entry__c, CreatedDate, CreatedBy.Name FROM Journal__c  WHERE Id = :journalParentId LIMIT 1];
            if(!searchParentJournal.isEmpty()) {
                System.debug('setting parent');
                journalParent = searchParentJournal.get(0);
                if(String.isNotBlank(journalId)) {
                    List<Journal__c> searchJournalReply = [SELECT Id, Name, Journal_Entry__c FROM Journal__c  WHERE Id = :journalId AND Parent_Journal__c = :journalParent.Id LIMIT 1];
                    if(!searchJournalReply.isEmpty()) journal = searchJournalReply.get(0);
                } else {
                    journalId = '';
                }
            } else {
                journalId = '';
            }
            journalModalAction = 'Edit';
        }
        System.debug('journalId -> '+journalId);
    }
    
    public void upsertJournal() {
        System.debug(journalJSON);
        Map<String,Object> root = (Map<String,Object>) JSON.deserializeUntyped(journalJSON);
        String journalJSONId = '';
        Id taskTraceRecordTypeId = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName().get('Trace_Task').getRecordTypeId();
        if(root.containsKey('id')) journalJSONId = (String) root.get('id');
        String coordinatorType;
        if(journal.Id == null || journalId.equals(journalJSONId)) {
            if(root.containsKey('parentId')) {
                if(root.containsKey('journalEntry')) journal.Journal_Entry__c = (String) root.get('journalEntry');
                journal.Parent_Journal__c = journalParentId;
                upsert journal;
            } else {
                if(root.containsKey('issue')) journal.Issue__c = (Boolean) root.get('issue');
                if(root.containsKey('sales')) journal.Sales__c = (Boolean) root.get('sales');
                if(root.containsKey('categoryProduction')) journal.Production_checkbox__c = (Boolean) root.get('categoryProduction');
                if(root.containsKey('categoryHousingVendor')) journal.Vendor_Checkbox__c = (Boolean) root.get('categoryHousingVendor');
                if(root.containsKey('journalEntry')) journal.Journal_Entry__c = (String) root.get('journalEntry');
                if(root.containsKey('journalCoordinator')) journal.Trace_Coordinator__c = ((String) root.get('journalCoordinator')) == ''? null : ((String) root.get('journalCoordinator'));
                    if(root.containsKey('traceDate')) {
                        String traceDate = (String) root.get('traceDate');
                        if(String.isNotEmpty(traceDate)) journal.Trace_Date__c = Date.valueOf(traceDate.split('/')[2]+'-'+traceDate.split('/')[0]+'-'+traceDate.split('/')[1]);
                        else journal.Trace_Date__c = null;
                    }
                if(root.containsKey('markComplete')) journal.Mark_Journal_trace_complete__c = (Boolean) root.get('markComplete');
                if(journal.Mark_Journal_trace_complete__c == true) journal.Trace_Date__c = null;
                system.debug(relativeSObjectName);
                switch on relativeSObjectName {
                    when 'Production'{
                        journal.Production__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Journal').getRecordTypeId();
                        if(productionType == 'Housing') coordinatorType = 'Primary Housing Coordinator';
                        if(productionType == 'Ground') coordinatorType = 'Primary GT Coordinator';
                        if(productionType == 'Freight') coordinatorType = 'Primary Freight Coordinator';
                        if(productionType == 'Air') coordinatorType = 'Primary Air Coordinator';
                    }
                    when 'Bid' {
                        journal.Bid__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Bid_Journal').getRecordTypeId();
                        Bid__c objAux = [SELECT Id, RecordType.DeveloperName FROM Bid__c WHERE Id =: relativeRecordId];
                        if(objAux.RecordType.DeveloperName == 'Air_Bid') coordinatorType = 'Primary Air Coordinator';
                        if(objAux.RecordType.DeveloperName == 'Freight_Bid') coordinatorType = 'Primary Freight Coordinator';
                        if(objAux.RecordType.DeveloperName == 'GT_Bid') coordinatorType = 'Primary GT Coordinator';
                        if(objAux.RecordType.DeveloperName == 'Housing_Bid') coordinatorType = 'Primary Housing Coordinator';
                    }
                    when 'Housing' {
                        journal.Housing__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Vendor_Journal').getRecordTypeId();
                        coordinatorType = 'Primary Housing Coordinator';
                    }
                    when 'Ground' {
                        journal.G__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId();
                        coordinatorType = 'Primary GT Coordinator';
                    }
                    when 'Air' {
                        journal.Air__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId();
                        coordinatorType = 'Primary Air Coordinator';
                    }
                    when 'GCQ' {
                        journal.G__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('GCQ_Journal').getRecordTypeId();
                        coordinatorType = 'Primary GT Coordinator';
                    }
                    when 'ACQ' {
                        journal.Air__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('GCQ_Journal').getRecordTypeId();
                        coordinatorType = 'Primary Air Coordinator';
                    }
                    when 'FCQ' {
                        journal.Freight__c = relativeRecordId;
                        journal.RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('FCQ_Journal').getRecordTypeId();
                        coordinatorType = 'Primary Freight Coordinator';
                    }
                }
                upsert journal;
                System.debug('Journal upserted!');
                if(journal.Trace_Coordinator__c != null) {
                    Task trace = new Task(
                        Id = journal.Task_ID__c != null ? journal.Task_ID__c : null,
                        Subject = journal.Journal_Entry__c.length() > 40? journal.Journal_Entry__c.subString(0,40) : journal.Journal_Entry__c,
                        RecordTypeId = taskTraceRecordTypeId,
                        ActivityDate = journal.Trace_Date__c,
                        OwnerId = journal.Trace_Coordinator__c,
                        WhatId = journal.Id, 
                        Description = journal.Journal_Entry__c, 
                        Status = journal.Mark_Journal_trace_complete__c? 'Completed' : 'Open'
                    );
                    upsert trace;
                    if(journal.Task_ID__c == null) update new Journal__c(Id = journal.Id, Task_ID__c = trace.Id);
                }
                if(root.containsKey('alertAll')) {
                    Boolean alert = (Boolean) root.get('alertAll');
                    if(alert && coordinatorType != '' && coordinatorType != null) {
                        Set<String> userEmails = new Set<String>();
                        for(Production_Associations__c pa : [SELECT Id, User__c, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId AND User__c <> null]) userEmails.add(pa.User__r.Email);
                        if(userEmails.size() > 0){
                            List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes (:coordinatorType)];
                            List<String> userEmailsList = new List<String>(userEmails);
                            Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage(); 
                            if(prodAssocAux.size() > 0) mail.setOrgWideEmailAddressId(verifyWideAddress(prodAssocAux[0].User__r.Email));
                            mail.setToAddresses(userEmailsList); 
                            mail.setSubject('Urgent: Journal Entry for ' + opportunity.Name); 
                            String bodyAux = journal.Journal_Entry__c + '<br/><br/>';
                            bodyAux += '<a href="'+ ApexPages.currentPage().getHeaders().get('Host') + '/' + journal.Id + '" target="_blank">Click here for the Journal entry</a><br/>';
                            switch on relativeSObjectName {
                                when 'Housing' { /*bodyAux += '<a href="'+ ApexPages.currentPage().getHeaders().get('Host') + '/' + housingStayViewId + '" target="_blank">Click here for the Housing Stay Detail link</a><br/><br/>';*/ }
                                when 'Ground' { /*'<a href="'+ ApexPages.currentPage().getHeaders().get('Host') + '/' + housingStayViewId + '" target="_blank">Click here for the Trip Detail link</a><br/><br/>';*/ }
                            }
                            bodyAux += 'Thanks, <br/>' + UserInfo.getUserName();
                            mail.setHtmlBody(bodyAux); 
                            Messaging.sendEmail(new Messaging.SingleEmailMessage[] { mail });
                        }
                    }
                }
                
                /*List<Related_Companies__c> newJournalCompanies = new List<Related_Companies__c>();
                Set<String> relatedCompaniesAux = new Set<String>();
                if(root.containsKey('journalCompanies')) {
                    List<Object> journalJSONCompanies = (List<Object>) root.get('journalCompanies');
                    for(Object journalJSONCompanyId : journalJSONCompanies) if(((String) journalJSONCompanyId).length() == 18) newJournalCompanies.add(new Related_Companies__c(Journal__c = journal.Id, Company__c = (String) journalJSONCompanyId));
                    delete [SELECT Id FROM Related_Companies__c WHERE Journal__c = :journal.Id AND Company__c <> null];
                }
                if(!newJournalCompanies.isEmpty()) insert newJournalCompanies;*/
                Map<String,Related_Contact__c> newJournalContacts = new Map<String,Related_Contact__c>();
                delete [SELECT Id FROM Related_Contact__c WHERE Journal__c = :journal.Id AND Contact__c <> null];
                if(root.containsKey('journalContacts')) {
                    List<Object> journalJSONContacts = (List<Object>) root.get('journalContacts');
                    for(Object journalJSONContactId : journalJSONContacts) if(((String) journalJSONContactId).length() == 18) newJournalContacts.put((String) journalJSONContactId,new Related_Contact__c(Journal__c = journal.Id, Contact__c = (String) journalJSONContactId, Type__c = 'Production Contacts;'));
                }
                if(root.containsKey('journalCompanyContacts')) {
                    List<Object> journalJSONCompanyContacts = (List<Object>) root.get('journalCompanyContacts');
                    for(Object journalJSONContactId : journalJSONCompanyContacts) if(((String) journalJSONContactId).length() == 18) {
                        if(newJournalContacts.containsKey((String) journalJSONContactId)) newJournalContacts.get((String) journalJSONContactId).Type__c += 'Company Contacts;';
                        else newJournalContacts.put((String) journalJSONContactId,new Related_Contact__c(Journal__c = journal.Id, Contact__c = (String) journalJSONContactId, Type__c = 'Company Contacts;'));
                    }
                }
                if(!newJournalContacts.isEmpty()) insert newJournalContacts.values();
            }
        }
        loadJournals();
    }
    
    public static String verifyWideAddress(String email){
        String oweaId;
        List<OrgWideEmailAddress> oweaList;
        if(Test.isRunningTest()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; else oweaList = [select Id from OrgWideEmailAddress where Address =: email];
        if(oweaList.isEmpty()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; //Email default
        if(!oweaList.isEmpty()) oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
        return oweaId;
    }
    
    /*public class AssociationWrapper {
        public String associationId {get;set;}
        public String relativeId {get;set;}
        public String name {get;set;}
        public String roles {get;set;}
        public String belongsTo {get;set;}
        
        public AssociationWrapper() {
            this.associationId = '';
            this.relativeId = '';
            this.name = '';
            this.roles = '';
            this.belongsTo = '';
        }
        
        public AssociationWrapper(String associationId, String relativeId, String name, String roles, String belongsTo) {
            this.associationId = associationId;
            this.relativeId = relativeId;
            this.name = name;
            this.roles = roles;
            this.belongsTo = belongsTo;
        }
    }*/
}```

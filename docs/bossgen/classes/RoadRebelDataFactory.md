---
layout: default
title: RoadRebelDataFactory
parent: classes
---
# Metadata Type
classes


# Filename 
RoadRebelDataFactory


# Raw XML
```
@isTest
public with sharing class RoadRebelDataFactory {
    public RoadRebelDataFactory() {
    }

    public static void createHousingSetup() {
        Id recordTypeHH = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
            .get('Hotel_Housing')
            .getRecordTypeId();
        // trace record type for tasks which they all should have
        Id recordTypeTT = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName()
            .get('Trace_Task')
            .getRecordTypeId();

        Id recordTypeId2 = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
            .get('Production_Coordinators')
            .getRecordTypeId();

        Id recordTypeBid = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
            .get('Housing_Bid')
            .getRecordTypeId();

        Id recordTypeG = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
            .get('GT_Trip_Details')
            .getRecordTypeId();

        Account a = new Account(Name = 'Acc Test Name');
        insert a;

        Opportunity o = new Opportunity(
            Name = 'Opp Test Name',
            Type = 'Test',
            AccountId = a.Id,
            StageName = 'Qualification',
            CloseDate = System.today()
        );
        insert o;

        Production_Associations__c pa = new Production_Associations__c(
            User__c = UserInfo.getUserId(),
            Team_Roles__c = 'Primary Contract Coordinator; Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator;Primary Freight Coordinator',
            Production_Opp__c = o.Id,
            RecordTypeId = recordTypeId2 // production coordinators
        );
        insert pa;

        City__c c = new City__c(Name = 'City Test Name');
        insert c;

        Housing__c h = new Housing__c(
            RecordTypeId = recordTypeHH,
            Production_CC__c = o.Id,
            Housing_Preference__c = 'RRU',
            City__c = c.Id,
            Deadline_Date__c = System.today(),
            Date_In__c = System.today(),
            Date_Out__c = System.today(),
            Trace_Date__c = system.today()
        );
        insert h;

        Task[] theTasks = new List<Task>();

        for (Integer x = 0; x < 10; x++) {
            //task bid housing 2
            theTasks.add(
                new Task(
                    Subject = 'Itinerary Received',
                    Contract_Task__c = false,
                    recordTypeId = recordTypeTT,
                    WhatId = h.Id,
                    ActivityDate = System.today(),
                    Priority = 'Normal Follow Up',
                    Task_Type__c = 'Housing Status Trace',
                    Status = 'Open',
                    IsForStayOrTrip__c = true
                )
            );
        }

        for (Integer x = 0; x < 10; x++) {
            //task bid housing 2
            theTasks.add(
                new Task(
                    Subject = 'Bid Request Stage',
                    Contract_Task__c = false,
                    recordTypeId = recordTypeTT,
                    WhatId = h.Id,
                    ActivityDate = System.today(),
                    Priority = 'Normal Follow Up',
                    Task_Type__c = 'Housing Status Trace',
                    Status = 'Open',
                    IsForStayOrTrip__c = true
                )
            );
        }

        insert theTasks;

        Task theTask = new Task(
            Subject = 'Pending Client Choice',
            Contract_Task__c = false,
            recordTypeId = recordTypeTT,
            WhatId = h.Id,
            ActivityDate = System.today(),
            Priority = 'Normal Follow Up',
            Task_Type__c = 'Housing Status Trace',
            Status = 'Open',
            IsForStayOrTrip__c = true
        );
        insert theTask;
        Test.setCreatedDate(theTask.Id, system.today() + 3);

        Bid__c b = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBid,
            Contract_Due_Date__c = null,
            Status__c = 'In Contracting',
            Housing__c = h.Id
        );
        insert b;

        Task[] theTasksBid = new List<Task>();

        for (Integer x = 0; x < 10; x++) {
            //task bid housing 2
            theTasksBid.add(
                new Task(
                    Subject = 'Pending Contract',
                    Contract_Task__c = true,
                    recordTypeId = recordTypeTT,
                    WhatId = b.Id,
                    ActivityDate = System.today(),
                    Priority = 'Normal Follow Up',
                    Task_Type__c = 'Housing Status Trace',
                    Status = 'Open',
                    IsForStayOrTrip__c = false
                )
            );
        }

        theTasksBid.add(
            new Task(
                Subject = 'Pending Client Signature',
                Contract_Task__c = true,
                recordTypeId = recordTypeTT,
                WhatId = b.Id,
                ActivityDate = System.today(),
                Priority = 'Normal Follow Up',
                Task_Type__c = 'Housing Status Trace',
                Status = 'Open',
                IsForStayOrTrip__c = false
            )
        );

        theTasksBid.add(
            new Task(
                Subject = 'Pending Client Signature',
                Contract_Task__c = true,
                recordTypeId = recordTypeTT,
                WhatId = b.Id,
                ActivityDate = System.today(),
                Priority = 'Normal Follow Up',
                Task_Type__c = 'Housing Status Trace',
                Status = 'Completed',
                IsForStayOrTrip__c = false
            )
        );

        insert theTasksBid;
    }
}
```


# Last Modified


# Usage

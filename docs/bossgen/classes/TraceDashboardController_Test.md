---
layout: default
title: TraceDashboardController_Test
parent: classes
---
# Metadata Type
classes


# Filename 
TraceDashboardController_Test


# Raw XML
```
@isTest
public class TraceDashboardController_Test {
    @TestSetup
    static void makeData() {
        Id recordTypeTT = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName()
            .get('Trace_Task')
            .getRecordTypeId();
        Task t = new Task(Subject = 'Rework', Contract_Task__c = true, recordTypeId = recordTypeTT);
        insert t;

        //user
        Profile profileId = [SELECT Id FROM Profile WHERE Name = 'Standard User' LIMIT 1];
        User u = new User(
            LastName = 'LNTestAR',
            FirstName = 'FNTestAR',
            Alias = 'atestAR',
            Email = 'qwertytestAR@testar.com',
            Username = 'uqwertytestAR@testar.com',
            ProfileId = profileId.id,
            TimeZoneSidKey = 'GMT',
            LanguageLocaleKey = 'en_US',
            EmailEncodingKey = 'UTF-8',
            LocaleSidKey = 'en_US'
        );
        insert u;

        //acc
        Account a = new Account(Name = 'Acc Test Name');
        insert a;

        //opp
        Opportunity o = new Opportunity(
            Name = 'Opp Test Name',
            Type = 'Test',
            AccountId = a.Id,
            StageName = 'Qualification',
            CloseDate = System.today()
        );
        insert o;

        //Production_Associations__c
        //set<String> teamRolesPL = new set<String>{'Primary Housing Coordinator','Test'};
        Id recordTypeId2 = Schema.SObjectType.Production_Associations__c.getRecordTypeInfosByDeveloperName()
            .get('Production_Coordinators')
            .getRecordTypeId();
        Production_Associations__c pa = new Production_Associations__c(
            User__c = u.Id,
            Team_Roles__c = 'Primary Housing Coordinator;Primary GT Coordinator;Primary Air Coordinator;Primary Freight Coordinator',
            Production_Opp__c = o.Id,
            RecordTypeId = recordTypeId2
        );
        insert pa;
        system.debug('insert pa;' + pa);

        //city
        City__c c = new City__c(Name = 'City Test Name');
        insert c;

        //### HOUSING
        //housing 1
        Id recordTypeHH = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
            .get('Hotel_Housing')
            .getRecordTypeId();
        Housing__c h = new Housing__c(
            RecordTypeId = recordTypeHH,
            Production_CC__c = o.Id,
            Housing_Preference__c = 'RRU',
            City__c = c.Id,
            Deadline_Date__c = System.today(),
            Date_In__c = System.today(),
            Date_Out__c = System.today()
        );
        insert h;

        //bid housing 1
        Id recordTypeBid = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
            .get('Housing_Bid')
            .getRecordTypeId();
        Bid__c b = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBid,
            Contract_Due_Date__c = null,
            //Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            Housing__c = h.Id
        );
        insert b;

        //task bid housing 1
        Task t2 = new Task(
            WhatId = h.Id,
            Task_Type__c = 'Housing Status Trace',
            recordTypeId = recordTypeTT,
            ActivityDate = System.today(),
            Subject = 'Rework',
            Contract_Task__c = false,
            Priority = 'Urgent Follow Up'
        );
        insert t2;

        //housing 2
        Housing__c h2 = new Housing__c(
            RecordTypeId = recordTypeHH,
            Production_CC__c = o.Id,
            Housing_Preference__c = 'RRU',
            City__c = c.Id,
            Deadline_Date__c = System.today(),
            Date_In__c = System.today(),
            Date_Out__c = System.today()
        );
        insert h2;

        //bid housing 2
        Bid__c b2 = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBid,
            //Contract_Due_Date__c = null,
            Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            Housing__c = h2.Id
        );
        insert b2;

        //task bid housing 2
        Task t3 = new Task(
            Subject = 'Rework',
            Contract_Task__c = true,
            recordTypeId = recordTypeTT,
            WhatId = b2.Id,
            ActivityDate = System.today(),
            Priority = 'Urgent Follow Up'
        );
        insert t3;

        //###GT
        //gt 1
        Id recordTypeG = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
            .get('GT_Trip_Details')
            .getRecordTypeId();
        Ground__c gt1 = new Ground__c(
            RecordTypeId = recordTypeG,
            Production_Ground__c = o.Id,
            Start_City__c = c.Id,
            Arriving_city__c = c.Id,
            Deadline_Date__c = System.today(),
            Start_Date__c = System.today(),
            End_Date__c = System.today(),
            Description__c = 'Test desc',
            Service_Type_Ground__c = 'Rentals;Coach'
        );
        insert gt1;

        //bid gt 1
        Id recordTypeBidGT = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
            .get('GT_Bid')
            .getRecordTypeId();
        Bid__c bidgt1 = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBidGT,
            Contract_Due_Date__c = null,
            //Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            GT__c = gt1.Id
        );
        insert bidgt1;

        //task bid gt 1
        Task tgt1 = new Task(
            WhatId = gt1.Id,
            Task_Type__c = 'Ground Status Trace',
            recordTypeId = recordTypeTT,
            ActivityDate = System.today(),
            Subject = 'Rework',
            Contract_Task__c = false,
            Priority = 'Urgent Follow Up'
        );
        insert tgt1;

        //gt 2
        Ground__c gt2 = new Ground__c(
            RecordTypeId = recordTypeG,
            Production_Ground__c = o.Id,
            Start_City__c = c.Id,
            Arriving_city__c = c.Id,
            Deadline_Date__c = System.today(),
            Start_Date__c = System.today(),
            End_Date__c = System.today(),
            Description__c = 'Test desc',
            Service_Type_Ground__c = 'Rentals;Coach'
        );
        insert gt2;

        //bid gt 2
        Bid__c bidgt2 = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBidGT,
            //Contract_Due_Date__c = null,
            Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            GT__c = gt2.Id
        );
        insert bidgt2;

        //task bid gt 2
        Task tgt2 = new Task(
            Subject = 'Rework',
            Contract_Task__c = true,
            recordTypeId = recordTypeTT,
            WhatId = bidgt2.Id,
            ActivityDate = System.today(),
            Priority = 'Urgent Follow Up'
        );
        insert tgt2;

        //###FREIGHT
        //f 1
        Id recordTypeF = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName()
            .get('Freight_Trip_Details')
            .getRecordTypeId();
        Freight__c f1 = new Freight__c(
            RecordTypeId = recordTypeF,
            Production__c = o.Id,
            Start_City__c = c.Id,
            End_city__c = c.Id,
            Deadline_Date__c = System.today(),
            Start_Date__c = System.today(),
            End_Date__c = System.today(),
            Description__c = 'Test desc',
            Service_Type__c = 'Ocean'
        );
        insert f1;

        //bid f 1
        Id recordTypeBidF = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
            .get('Freight_Bid')
            .getRecordTypeId();
        Bid__c bidf1 = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBidF,
            Contract_Due_Date__c = null,
            //Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            Freight__c = f1.Id
        );
        insert bidf1;

        //task bid f 1
        Task tf1 = new Task(
            WhatId = f1.Id,
            Task_Type__c = 'Freight Status Trace',
            recordTypeId = recordTypeTT,
            ActivityDate = System.today(),
            Subject = 'Rework',
            Contract_Task__c = false,
            Priority = 'Urgent Follow Up'
        );
        insert tf1;

        //f 2
        Freight__c f2 = new Freight__c(
            RecordTypeId = recordTypeF,
            Production__c = o.Id,
            Start_City__c = c.Id,
            End_city__c = c.Id,
            Deadline_Date__c = System.today(),
            Start_Date__c = System.today(),
            End_Date__c = System.today(),
            Description__c = 'Test desc',
            Service_Type__c = 'Ocean'
        );
        insert f2;

        //bid f 2
        Bid__c bidf2 = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBidF,
            //Contract_Due_Date__c = null,
            Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            Freight__c = f2.Id
        );
        insert bidf2;

        //task bid f 2
        Task tf2 = new Task(
            Subject = 'Rework',
            Contract_Task__c = true,
            recordTypeId = recordTypeTT,
            WhatId = bidf2.Id,
            ActivityDate = System.today(),
            Priority = 'Urgent Follow Up'
        );
        insert tf2;

        /* air traces */
        Id recordTypeAir = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Trip_Details')
            .getRecordTypeId();
        Air__c airRecord = new Air__c(
            RecordTypeId = recordTypeAir,
            Production__c = o.Id,
            //Start_City__c = c.Id,
            //End_city__c = c.Id,
            Deadline_Date__c = System.today(),
            Start_Date__c = System.today(),
            End_Date__c = System.today(),
            Description__c = 'Test desc'
        );
        //Service_Type__c = 'Ocean');
        insert airRecord;

        //bid f 1
        Id recordTypeBidAir = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Bid')
            .getRecordTypeId();
        Bid__c bida1 = new Bid__c(
            Vendor__c = a.Id,
            Production__c = o.Id,
            RecordTypeId = recordTypeBidAir,
            Contract_Due_Date__c = null,
            //Contract_Due_Date__c = System.today(),
            Status__c = 'Contracted',
            Air__c = airRecord.Id
        );
        insert bida1;

        //task bid f 1
        Task tfa = new Task(
            WhatId = airRecord.Id,
            Task_Type__c = 'Air Status Trace',
            recordTypeId = recordTypeTT,
            ActivityDate = System.today(),
            Subject = 'Rework',
            Contract_Task__c = false,
            Priority = 'Urgent Follow Up'
        );
        insert tfa;
    }

    static testMethod void test01() {
        TraceDashboardController tdc = new TraceDashboardController();
        tdc.searchAllCoordinators = true;
        tdc.searchAllStatus = true;
        tdc.searchTraceType = 'Trace Date';
        //tdc.searchSortBy = '';
        Test.startTest();
        tdc.searchTrace();
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

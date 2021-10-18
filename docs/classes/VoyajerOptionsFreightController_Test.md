---
layout: default
title: VoyajerOptionsFreightController_Test
parent: classes
---

```@isTest
public class VoyajerOptionsFreightController_Test {
    static testMethod void test01(){
        //DATA
        //acc
        Account a = new Account(Name = 'Acc Test Name');
        insert a;
        
        //opp
        Opportunity o = new Opportunity(Name = 'Opp Test Name',
                                          Type = 'Test',
                                          AccountId = a.Id,
                                          StageName ='Qualification',
                                          CloseDate = System.today());
        insert o;
        
        //city
        City__c c = new City__c(Name = 'City Test Name');
        insert c;
        
        //###FREIGHT
        //f 1
        Id recordTypeF = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId();
        Freight__c f1 = new Freight__c(RecordTypeId = recordTypeF,
                                     Production__c = o.Id,
                                     Start_City__c = c.Id,
                                     End_city__c = c.Id,
                                     Deadline_Date__c = System.today(),
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today(),
                                     Description__c = 'Test desc',
                                   	 Service_Type__c = 'Ocean');
        insert f1;
        
        //bid f 1
        Id recordTypeBidF = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('Freight_Bid').getRecordTypeId();
        Bid__c bidf1 = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBidF,
                             Contract_Due_Date__c = null,
                             //Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             Freight__c = f1.Id,
                             Options__c = 1);
        insert bidf1;
 
        //f 2
        Id recordTypeFST = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Sub_Trip_Details').getRecordTypeId();
        Freight__c f2 = new Freight__c(RecordTypeId = recordTypeFST,
                                       Bid_Sub_Trip__c = bidf1.Id,
                                     Production__c = o.Id,
                                     Start_City__c = c.Id,
                                     End_city__c = c.Id,
                                     Deadline_Date__c = System.today(),
                                     Start_Date__c = System.today(),
                                     End_Date__c = System.today(),
                                     Description__c = 'Test desc',
                                   	 Service_Type__c = 'Ocean');
        insert f2;
        
        //bid f 2
        Bid__c bidf2 = new Bid__c(Vendor__c = a.Id,
                             Production__c = o.Id,
                             RecordTypeId = recordTypeBidF,
                             //Contract_Due_Date__c = null,
                             Contract_Due_Date__c = System.today(),
                             Status__c = 'Contracted',
                             Freight__c = f2.Id);
        insert bidf2;
        //END DATA
        
        Test.startTest();
        String result = VoyajerOptionsFreightController.searchBidOptions(f1.Id);
        Test.stopTest();
    }
}```

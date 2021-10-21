---
layout: default
title: DashboardBidContractWrapper_Test
parent: classes
---
# Metadata Type
classes


# Filename 
DashboardBidContractWrapper_Test


# Raw XML
```
@isTest
public class DashboardBidContractWrapper_Test{
    @isTest static void Test_DashboardBidContractWrapper(){
        Test.startTest();
        DashboardBidContractWrapper wrapperA = new DashboardBidContractWrapper(null,null,null,null,null);
        Freight__c f1 = new Freight__c(Start_Date__c = System.today(),
                                     End_Date__c = System.today(),
                                     Description__c = 'Test desc',
                                   	 Service_Type__c = 'Ocean');
        Ground__c g1 = null;
        Air__c a1 = null;
        DashboardBidContractWrapper wrapperB = new DashboardBidContractWrapper(f1,null,null,null,null,null);
        DashboardBidContractWrapper wrapperC = new DashboardBidContractWrapper(g1,null,null,null,null,null);
        DashboardBidContractWrapper wrapperD = new DashboardBidContractWrapper(a1,null,null,null,null,null);
        wrapperD.setHousingFields(null,null,null,null,null,null);
        wrapperD.setGroundFields(null,null,null,null,null,null);
        wrapperD.setFreightFields(null,null,null,null,null,null);
        wrapperD.setAirFields(null,null,null,null,null,null,null);
        
        DashboardBidContractWrapper.orderFieldBidContract = 'startDate';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'dep_arr';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'endDate';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'rt_dep_arr';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'vendor';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'groupName';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'status';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'venue';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'city';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'serviceType';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'trip_type';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'pax';
        wrapperB.compareTo(wrapperC);
        DashboardBidContractWrapper.orderFieldBidContract = 'none';
        wrapperB.compareTo(wrapperC);
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

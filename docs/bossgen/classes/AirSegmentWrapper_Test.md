---
layout: default
title: AirSegmentWrapper_Test
parent: classes
---
# Metadata Type
classes


# Filename 
AirSegmentWrapper_Test


# Raw XML
```
@isTest
public class AirSegmentWrapper_Test {
    public static testMethod void testAirSegmentWrapper(){
        Test.startTest();
        List<AirSegmentWrapper> aswList=  new List<AirSegmentWrapper>();
        aswList.add(new AirSegmentWrapper(new Air__c(),system.today()));
        aswList.add(new AirSegmentWrapper(new Air__c(),system.today()));
        AirSegmentWrapper.orderField = 'date';
        AirSegmentWrapper.orderOrientation = 'ASC';
        aswList.sort();
        Test.stopTest();
    }
    public static testMethod void testAirSegmentWrapperOther(){
        Test.startTest();
        List<AirSegmentWrapper> aswList=  new List<AirSegmentWrapper>();
        aswList.add(new AirSegmentWrapper(new Air__c(),'','test departure','','test arrival'));
        aswList.add(new AirSegmentWrapper(new Air__c(),'','test departure','','test arrival'));
        AirSegmentWrapper.orderField = 'date';
        AirSegmentWrapper.orderOrientation = 'ASC';
        aswList.sort();
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

---
layout: default
title: DashboardSearchBoxWrapper_Test
parent: classes
---

```@isTest
public class DashboardSearchBoxWrapper_Test{
    @isTest static void Test_DashboardSearchBoxWrapper(){
        Test.startTest();
        DashboardSearchBoxWrapper dashboard = new DashboardSearchBoxWrapper();
        system.assert(!dashboard.isPriorTrip);
        Test.stopTest();
    }
}```

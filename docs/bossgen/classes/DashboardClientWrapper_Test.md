---
layout: default
title: DashboardClientWrapper_Test
parent: classes
---
# Metadata Type
classes


# Filename 
DashboardClientWrapper_Test


# Raw XML
```
@isTest
public class DashboardClientWrapper_Test{
    @isTest static void Test_DashboardClientWrapper(){
        Test.startTest();
        DashboardClientWrapper wrapper = new DashboardClientWrapper();
        system.assert(wrapper.firstName == '');
        DashboardClientWrapper wrapperOther = new DashboardClientWrapper(null,null,null,null,null,null,null,null,null,null,null,null,null,null,'test');
        system.assert(wrapperOther.note == 'test');
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

---
layout: default
title: wrapperLocation_Test
parent: classes
---
# Metadata Type
classes


# Filename 
wrapperLocation_Test


# Raw XML
```
@isTest
public class wrapperLocation_Test{
    @isTest static void Test_DashboardSearchBoxWrapper(){
        Test.startTest();
        wrapperLocation wrapper = new wrapperLocation('value1','value2','value3','value4','value5','value6');
        system.assertEquals('value6',wrapper.data6);
        Test.stopTest();
    }
}
```


# Last Modified


# Usage

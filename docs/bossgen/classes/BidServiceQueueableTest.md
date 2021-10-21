---
layout: default
title: BidServiceQueueableTest
parent: classes
---
# Metadata Type
classes


# Filename 
BidServiceQueueableTest


# Raw XML
```
@isTest
public class BidServiceQueueableTest {
    static testmethod void test1() {
        // startTest/stopTest block to force async processes 
        //   to run in the test.
        Test.startTest();        
        System.enqueueJob(new BidServiceQueueable(new List<Object>()));
        Test.stopTest();

    }
}
```


# Last Modified


# Usage

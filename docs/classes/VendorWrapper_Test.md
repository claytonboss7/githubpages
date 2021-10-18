---
layout: default
title: VendorWrapper_Test
parent: classes
---

```@isTest
public class VendorWrapper_Test{
    @isTest static void Test_VendorWrapper(){
        Test.startTest();
        List<VendorWrapper> listWrapper = new List<VendorWrapper>();
        listWrapper.add(new VendorWrapper(new Account(),null,null,null,null,null,null,null,null));
        listWrapper.add(new VendorWrapper(new Account(),null,null,null,null,null,null,null,null));
        VendorWrapper.orderFieldVendor = 'info';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'flag';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'distance';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'vendor';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'service_types';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'city';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'status';
        listWrapper.sort();
        VendorWrapper.orderFieldVendor = 'created_date';
        listWrapper.sort();
        Test.stopTest();
    }
}```

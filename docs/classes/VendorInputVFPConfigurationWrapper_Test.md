---
layout: default
title: VendorInputVFPConfigurationWrapper_Test
parent: classes
---

```@isTest
public class VendorInputVFPConfigurationWrapper_Test{
    @isTest static void Test_VendorInputVFPConfigurationWrapper(){
        Test.startTest();
        VendorInputVFPConfigurationWrapper wrapper = new VendorInputVFPConfigurationWrapper();
        system.assert(wrapper.idsOfFleetsToDelete != null);
        Test.stopTest();
    }
}```

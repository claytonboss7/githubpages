---
layout: default
title: VendorVenueTrigger
parent: triggers
---
# Metadata Type
triggers


# Filename 
VendorVenueTrigger


# Raw XML
```
trigger VendorVenueTrigger on Vendor_Venue__c (after insert, after update) {
    if(ApexUtil.VendorVenueTrigger_Is_Enabled){
        Set<Id> vvIds = new Set<Id>();
        if(trigger.isInsert){
            for(Vendor_Venue__c vv : trigger.new){
                if(vv.Vendor__c != null && vv.Venue__c != null) vvIds.add(vv.Id);
            }
        }else{
            for(Vendor_Venue__c vv : trigger.new){
                if(vv.Vendor__c != trigger.oldMap.get(vv.Id).Vendor__c || vv.Venue__c != trigger.oldMap.get(vv.Id).Venue__c) vvIds.add(vv.Id);
            }
        }
        
        if(vvIds.size() > 0) GoogleConnection.verifyDistance(vvIds);
    }
}
```


# Last Modified


# Usage

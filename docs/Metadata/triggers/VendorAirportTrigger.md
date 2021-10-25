---
layout: default
title: VendorAirportTrigger
parent: triggers
grand_parent: Metadata
---
# Metadata Type
triggers


# Filename 
VendorAirportTrigger


# Raw XML
```
trigger VendorAirportTrigger on Vendor_Airport_Association__c (after insert, after update) {
    if(ApexUtil.VendorAirportTrigger_Is_Enabled){
        Set<Id> vaIds = new Set<Id>();
        if(trigger.isInsert){
            for(Vendor_Airport_Association__c va : trigger.new){
                if(va.Vendor__c != null && va.Airport__c != null) vaIds.add(va.Id);
            }
        }else{
            for(Vendor_Airport_Association__c va : trigger.new){
                if(va.Vendor__c != trigger.oldMap.get(va.Id).Vendor__c || va.Airport__c != trigger.oldMap.get(va.Id).Airport__c)  
                    vaIds.add(va.Id);
            }
        }
        
        if(vaIds.size() > 0) GoogleConnection.verifyDistanceAirport(vaIds);
    }
}
```


# Last Modified


# Usage

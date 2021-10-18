---
layout: default
title: VendorVenueAssociatorInvoke
parent: classes
---

```public class VendorVenueAssociatorInvoke {
    @InvocableMethod(
      label='Reassociate Venue'
      description='Recalc the Venue on the Vendor Venue records based on Vendor City'
      category='VendorVenue'
    )
    public static void recalcVenue(List<ID> ids) {
      // List<Contact> accounts = [SELECT Name FROM Contact WHERE Id IN :ids];
        
      VendorVenueAssociatorBatch vbatch = new VendorVenueAssociatorBatch('SELECT Venue__r.Name,Venue__c,Vendor__r.Name,Vendor__r.City__r.Name,Vendor__r.ShippingCity,Id FROM Vendor_Venue__c WHERE Recalc_Venue__c = true');
  
      database.executebatch(vbatch, 1);
    }
  }```

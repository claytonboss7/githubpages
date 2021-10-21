---
layout: default
title: PDF_InvocableGeneratorLP
parent: classes
---
# Metadata Type
classes


# Filename 
PDF_InvocableGeneratorLP


# Raw XML
```
/**
 * @description       : process builder to try and fire off PDF generation
 * @author            : clay b
 * @group             : 
 * @last modified on  : 06-23-2021
 * @last modified by  : clay b
 * Modifications Log 
 * Ver   Date         Author   Modification
 * 1.0   06-23-2021   clay b   Initial Version
**/
public without sharing class PDF_InvocableGeneratorLP {
  /*
    @InvocableMethod(
      label='Create PDF'
      description='Triggers PDF Creation from the Landing Page'
      category='PDF'
    )
    public static void saveAttachment(List<Id> ids) {

        try{
         
            for (String bid : ids){
                Blob bidAttachment;
                PageReference pageRef = new PageReference('https://rrdev-voyajer.cs196.force.com/PDF_BidSubmissionLP');
                pageRef.getParameters().put('bidid', bid);
                pageRef.getParameters().put('gen', '1');
                if (!Test.isRunningTest())
                  bidAttachment = pageRef.getContentAsPDF();
                else
                  bidAttachment = Blob.valueof(
                    'bidAttachment Test'
                  );
          
             BidTriggerHandler.TriggerDisabled = true;
             VoyajerBidSubmissionController.saveBidMemorializationAttachment(bid,bidAttachment);
            }

        } catch (Exception e){

            system.debug ('PDF_InvocableGeneratorLP error ... ' + e.getMessage() + ' - ' + e.getStackTraceString());

        }
    }
    */
  }
```


# Last Modified


# Usage

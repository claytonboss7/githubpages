---
layout: default
title: TestPDFGeneration
parent: classes
---

```public class TestPDFGeneration {
	
    //'https://roadrebel--rrdev--c.visualforce.com/apex/APXTConga4__Conga_Composer?id=a0e7g000007KxEpAAK&
    //QueryId=[Bid]a0D7g000002QPfjEAG?pv0=a0e7g000007KxEpAAK,[Housings]a0D7g000002QPgPEAW?
    //pv0=a0e7g000007KxEpAAK,[Contact]a0D7g000002QPfeEAG?pv0=0037g00000tsfbWAAQ,
    //[Concessions]a0D7g000002QPgJEAW?pv0=a0e7g000007KxEpAAK,[VendorContacts]a0D7g000002QPgMEAW?pv0=0017g00001HvORYAA3,
    //[VendorAirports]a0D7g000002QPgSEAW?pv0=0017g00001HvORYAA3,[Revenue]a0D7g000002QPgGEAW?pv0=a0e7g000007KxEpAAK&
    //TemplateId=a0L7g0000042MskEAE&csbusinessUnit=Sarah_Road_Rebe&CSRecipient1=0037g00000tsfbWAAQ&csvisible=1&
    //CSRoutingType=SERIAL&OFN=Rate+Agreement-H-0599521&DS7=1141&DefaultPDF=1&contentShareType=V&contentVisibility=
    //AllUsers&csexpiration=2021-10-12T16:06:32.241Z
    
    //https://roadrebel--rrdev--apxtconga4.visualforce.com/apex/Conga_Composer?
    //contentShareType=V&
    //QueryId=%5BBid%5Da0D7g000002QPfjEAG%3Fpv0%3Da0e7g000007KxEpAAK%2C%5BHousings%5Da0D7g000002QPgPEAW%3Fpv0%3Da0e7g000007KxEpAAK%2C%5BContact%5Da0D7g000002QPfeEAG%3Fpv0%3D0037g00000tsfbWAAQ%2C%5BConcessions%5Da0D7g000002QPgJEAW%3Fpv0%3Da0e7g000007KxEpAAK%2C%5BVendorContacts%5Da0D7g000002QPgMEAW%3Fpv0%3D0017g00001HvORYAA3%2C%5BVendorAirports%5Da0D7g000002QPgSEAW%3Fpv0%3D0017g00001HvORYAA3%2C%5BRevenue%5Da0D7g000002QPgGEAW%3Fpv0%3Da0e7g000007KxEpAAK&DS7=1141&CSRecipient1=0037g00000tsfbWAAQ&contentVisibility=AllUsers&csvisible=1&CSRoutingType=SERIAL&DefaultPDF=1&OFN=Rate+Agreement-H-0599521&id=a0e7g000007KxEpAAK&csexpiration=2021-10-12T16%3A07%3A36.244Z&csbusinessUnit=Sarah_Road_Rebe&TemplateId=a0L7g0000042MskEAE
    public static void testPDF() {
      Blob bidAttachment;
      PageReference pageRef = Page.APXTConga4__Conga_Composer ;
      pageRef.getParameters().put('id', 'a0e7g000007KxEpAAK');
      pageRef.getParameters().put('TemplateId', 'a0L7g0000042MskEAE');
      pageRef.getParameters().put('contentVisibility', 'AllUsers');
      pageRef.getParameters().put('DefaultPDF', '1');
      pageRef.getParameters().put('OFN', 'Rate Agreement H-0599521');
      pageRef.getParameters().put('QueryId', '[Bid]a0D7g000002QPfjEAG?pv0=a0e7g000007KxEpAAK,[Housings]a0D7g000002QPgPEAW?'+
    'pv0=a0e7g000007KxEpAAK,[Contact]a0D7g000002QPfeEAG?pv0=0037g00000tsfbWAAQ,'+
    '[Concessions]a0D7g000002QPgJEAW?pv0=a0e7g000007KxEpAAK,[VendorContacts]a0D7g000002QPgMEAW?pv0=0017g00001HvORYAA3,'+
    '[VendorAirports]a0D7g000002QPgSEAW?pv0=0017g00001HvORYAA3,[Revenue]a0D7g000002QPgGEAW?pv0=a0e7g000007KxEpAAK');
     bidAttachment = pageRef.getContentAsPDF();
      system.assert(false, bidAttachment);
      String fileName = 'Rate Agreement H-0599521';
      String bidId = 'a0D7g000002QPfjEAG';  
      ContentVersion bidContentVersion = new ContentVersion();
      bidContentVersion.PathOnClient = fileName +'.pdf';
      bidContentVersion.Title = fileName;
      bidContentVersion.VersionData = bidAttachment;
      upsert bidContentVersion;
       
      ContentVersion contentVersion_2 = [SELECT Id, Title, ContentDocumentId 
                            FROM ContentVersion WHERE Id = :bidContentVersion.Id LIMIT 1];
        ContentDocumentLink contentlink = new ContentDocumentLink();
        contentlink.LinkedEntityId = bidId;
        contentlink.contentdocumentid = contentVersion_2.contentdocumentid;
        contentlink.ShareType = 'V';
        contentlink.Visibility = 'AllUsers';
        insert contentlink;  
    }
}```

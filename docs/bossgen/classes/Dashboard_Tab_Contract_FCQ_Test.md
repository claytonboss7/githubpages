---
layout: default
title: Dashboard_Tab_Contract_FCQ_Test
parent: classes
---
# Metadata Type
classes


# Filename 
Dashboard_Tab_Contract_FCQ_Test


# Raw XML
```
@isTest
public class Dashboard_Tab_Contract_FCQ_Test{
    private static Dashboard_Tab_Contract_FCQ freightFcqController;
    private static DashboardConfigurationWrapper vfpConfiguration;
    static{
        DashboardDataFactory.createFreightData(1);
        vfpConfiguration = new DashboardConfigurationWrapper();
        vfpConfiguration.productionId = [Select id from Opportunity where Name = 'Cats'].id;
        vfpConfiguration.parentId = [Select id from Freight__c where Recordtype.DeveloperName = 'Freight_Trip_Details' limit 1].id;
        vfpConfiguration.bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        vfpConfiguration.clientMap = new Map<Id,DashboardClientWrapper>();
		freightFcqController = new Dashboard_Tab_Contract_FCQ();
		freightFcqController.vfpConfiguration = vfpConfiguration;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
	}
	//
    @isTest static void Test_OpenFCQ(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
        freightFcqController.fcqFreightJSON = '{"confirmAddressRoute":true,"confirmAllPermits":true,"exclusiveShipment":"LTL","driverName1":"DriverTest","driverMobile1":"(805) 453-2053","otherDrivers":[{"driverName":"driverName 2","driverMobile":"(805) 453-2054"},{"driverName":"driverName 3","driverMobile":"(805) 453-2055"}]}';
		freightFcqController.saveFCQ();
        System.assert(String.isNotEmpty(freightFcqController.fcqFreight.Id) && String.isNotBlank(freightFcqController.fcqFreight.Driver_Name_1__c) && String.isNotBlank(freightFcqController.fcqFreight.Driver_Mobile_1__c));
		freightFcqController.fcqId = null;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
		freightFcqController.getDetailByNumberNext();
		freightFcqController.getDetailByNumberBefore();
		Test.stopTest();
    }
    @isTest static void Test_DeactivateFCQ(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
        freightFcqController.fcqFreightJSON = '{"confirmAddressRoute":true,"confirmAllPermits":true,"exclusiveShipment":"LTL","driverName1":"DriverTest","driverMobile1":"(805) 453-2053","otherDrivers":[{"driverName":"driverName 2","driverMobile":"(805) 453-2054"},{"driverName":"driverName 3","driverMobile":"(805) 453-2055"}]}';
		freightFcqController.saveFCQ();
        System.assert(String.isNotEmpty(freightFcqController.fcqFreight.Id) && String.isNotBlank(freightFcqController.fcqFreight.Driver_Name_1__c) && String.isNotBlank(freightFcqController.fcqFreight.Driver_Mobile_1__c));
		freightFcqController.deactivateFCQ();
        System.assert(String.isBlank(freightFcqController.fcqId));
		Test.stopTest();
    } 
    @isTest static void Test_OpenEmailConfirmation(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
		freightFcqController.fcqEmailType = 'Email Confirmation';
		freightFcqController.chkContactSelected = 'production_contacts';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.draft != null && String.isNotEmpty(freightFcqController.draft.id) && String.isNotEmpty(freightFcqController.fcqBid.Form_Email_Confirmation__c) && freightFcqController.draft.Production_Assoc_Type__c == 'production_contacts');
        System.assert(freightFcqController.dataContactPL.size() > 1);
        freightFcqController.recordContactSelected = freightFcqController.dataContactPL[1].getValue();
		freightFcqController.changeContactDataSelected();
		freightFcqController.saveEmailConfirmation();
		freightFcqController.fcqEmailType = 'Email Confirmation';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.draft != null && String.isNotEmpty(freightFcqController.draft.id) && String.isNotEmpty(freightFcqController.fcqBid.Form_Email_Confirmation__c) && freightFcqController.draft.Production_Assoc_Type__c == 'production_contacts');
		freightFcqController.chkContactSelected = 'gt_coordinators';
		freightFcqController.searchContactData();
        System.assert(freightFcqController.dataContactPL.size() > 1);
        freightFcqController.recordContactSelected = freightFcqController.dataContactPL[1].getValue();
		freightFcqController.changeContactDataSelected();
		freightFcqController.saveEmailConfirmation();
		freightFcqController.fcqEmailType = 'Email Confirmation';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.draft != null && String.isNotEmpty(freightFcqController.draft.id) && String.isNotEmpty(freightFcqController.fcqBid.Form_Email_Confirmation__c) && freightFcqController.draft.Production_Assoc_Type__c == 'gt_coordinators');
		Test.stopTest();
    }
    @isTest static void Test_DeactivateEmailConfirmation(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
		freightFcqController.fcqEmailType = 'Email Confirmation';
		freightFcqController.chkContactSelected = 'production_contacts';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.draft != null && String.isNotEmpty(freightFcqController.draft.id) && String.isNotEmpty(freightFcqController.fcqBid.Form_Email_Confirmation__c) && freightFcqController.draft.Production_Assoc_Type__c == 'production_contacts');
        System.assert(freightFcqController.dataContactPL.size() > 1);
		freightFcqController.deactivateEmailConfirmation();
        System.assert(freightFcqController.draft != null && String.isEmpty(freightFcqController.draft.id) && String.isEmpty(freightFcqController.fcqBid.Form_Email_Confirmation__c));
		Test.stopTest();
    }
    @isTest static void Test_OpenSendToFT(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
		freightFcqController.fcqEmailType = 'Send to FT';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.dataContact_sendToFTPL.size() > 1);
        freightFcqController.recordContactSelected = freightFcqController.dataContact_sendToFTPL[1].getValue();
		freightFcqController.changeContactDataSelectedFT();
		Test.stopTest();
    }
    @isTest static void Test_AttachFcq(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
		freightFcqController.fcqEmailType = 'Send to FT';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.dataContact_sendToFTPL.size() > 1);
        freightFcqController.recordContactSelected = freightFcqController.dataContact_sendToFTPL[1].getValue();
		freightFcqController.changeContactDataSelected();
		freightFcqController.openAttachFcq();
		freightFcqController.searchFreight.Start_Date__c = Date.Today();
		freightFcqController.searchFreight.End_Date__c = Date.Today().addDays(2);
		freightFcqController.searchAttachFcq();
        System.assert(!freightFcqController.isFcqEmpty && freightFcqController.isFcqSearched);
		Test.stopTest();
    }
    @isTest static void Test_AttachDoc(){
		String subtripsSelected = '';
		Test.startTest();
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
        System.assert(String.isNotBlank(freightFcqController.fcqId));
		freightFcqController.fcqEmailType = 'Send to FT';
		freightFcqController.openEmailConfirmation();
        System.assert(freightFcqController.dataContact_sendToFTPL.size() > 1);
		freightFcqController.attachdocument_objectid = freightFcqController.fcqBid.id;
		freightFcqController.loadDocuments = true;
		freightFcqController.loadJournals = false;
		freightFcqController.openAttachDocs();
        System.assert(freightFcqController.attachDocumentList.isEmpty());
		freightFcqController.documentRelationId = freightFcqController.fcqBid.id;
		freightFcqController.filename = 'Attach Test 1';
		freightFcqController.body = 'data:text/plain;base64,VGVzdA==';
		freightFcqController.doAttachmentLast();
        System.assert(String.isNotEmpty(freightFcqController.newattachment_id) && String.isNotBlank(freightFcqController.newattachment_name));
		freightFcqController.documentRelationId = null;
		freightFcqController.filename = 'Attach Test 2';
		freightFcqController.body = 'data:text/plain;base64,VGVzdA==';
		freightFcqController.newattachment_id = null;
		freightFcqController.newattachment_name = null;
		freightFcqController.doAttachmentLast();
        System.assert(String.isEmpty(freightFcqController.newattachment_id) && String.isBlank(freightFcqController.newattachment_name));
		Test.stopTest();
    }
}
```


# Last Modified


# Usage

---
layout: default
title: Dashboard_Tab_Contract_Air_GCQ_Test
parent: classes
---

```@isTest
public class Dashboard_Tab_Contract_Air_GCQ_Test{
    private static Dashboard_Tab_Contract_Air_GCQ airGcqController;
    private static DashboardConfigurationWrapper vfpConfiguration;
    static{
        DashboardDataFactory.createAirData(1);
        vfpConfiguration = new DashboardConfigurationWrapper();
        vfpConfiguration.productionId = [Select id from Opportunity where Name = 'Cats'].id;
        vfpConfiguration.bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        vfpConfiguration.clientMap = new Map<Id,DashboardClientWrapper>();
		airGcqController = new Dashboard_Tab_Contract_Air_GCQ();
		airGcqController.vfpConfiguration = vfpConfiguration;
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }
    @isTest static void Test_OpenGCQ(){
		String segmentsSelected = '';
		String actualGcqId = '';
		Test.startTest();
		airGcqController.airCounter = 0;
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
		airGcqController.saveGCQ();
		airGcqController.gcqId = null;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
        actualGcqId = airGcqController.gcqId;
		airGcqController.getDetailByNumberNext();
		airGcqController.getDetailByNumberBefore();
		Test.stopTest();
    }
    @isTest static void Test_DeactivateGCQ(){
		String segmentsSelected = '';
		Test.startTest();
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
		airGcqController.deactivateGCQ();
        System.assert(String.isBlank(airGcqController.gcqId));
		Test.stopTest();
    }
    @isTest static void Test_OpenPreviewGCQ(){
		String segmentsSelected = '';
		Test.startTest();
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
        airGcqController.selectedGcqId = airGcqController.gcqId;
		airGcqController.openPreviewGCQ();
        System.assert(String.isNotBlank([Select GCQ_Main_Travel_Information_Conga__c From Air__c Where Id =:airGcqController.gcqId].GCQ_Main_Travel_Information_Conga__c));
        airGcqController.gcqId = null;
		airGcqController.openPreviewGCQ();
		Test.stopTest();
    }
    @isTest static void Test_OpenFinalAirConfirmation(){
		String segmentsSelected = '';
		Test.startTest();
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
		airGcqController.openFinalAirConfirmation();
		List<SelectOption> productionAssociationContacts = airGcqController.getBidAgreementProductionAssociationContacts();
        System.assert(airGcqController.draft != null && String.isNotEmpty(airGcqController.draft.id) && String.isNotEmpty(airGcqController.gcqBid.Form_Final_Air_Confirmation__c));
        airGcqController.draft.Production_Assoc_Contact_Id__c = !productionAssociationContacts.isEmpty() ? productionAssociationContacts[0].getValue() : null;
		airGcqController.changeBidAgreementProductionAssociationContact();
        System.assert(airGcqController.draft != null && String.isNotBlank(airGcqController.draft.Salutation__c));
		airGcqController.selectedGcqId = airGcqController.gcqId;
		airGcqController.saveFinalAirConfirmation();
		Test.stopTest();
    }
    @isTest static void Test_DeactivateFinalAirConfirmation(){
		String segmentsSelected = '';
		Test.startTest();
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
		airGcqController.openFinalAirConfirmation();
        System.assert(airGcqController.draft != null && String.isNotEmpty(airGcqController.draft.id) && String.isNotEmpty(airGcqController.gcqBid.Form_Final_Air_Confirmation__c));
		airGcqController.deactivateFinalAirConfirmation();
        System.assert(String.isEmpty(airGcqController.gcqBid.Form_Final_Air_Confirmation__c));
		airGcqController.deactivateFinalAirConfirmation();
		Test.stopTest();
    }
    @isTest static void Test_AttachGcq(){
		String segmentsSelected = '';
		Test.startTest();
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
		airGcqController.openFinalAirConfirmation();
        System.assert(airGcqController.draft != null && String.isNotEmpty(airGcqController.draft.id) && String.isNotEmpty(airGcqController.gcqBid.Form_Final_Air_Confirmation__c));
		airGcqController.openAttachGcq();
		airGcqController.attachGcq_departureDate = String.valueOf(Date.Today().addDays(-1));
		airGcqController.attachGcq_arrivalDate = String.valueOf(Date.Today().addDays(1));
		airGcqController.searchAttachGcq();
        System.assert(!airGcqController.isGcqEmpty && airGcqController.isGcqSearched);
		Test.stopTest();
		//
    }
    @isTest static void Test_AttachDoc(){
		String segmentsSelected = '';
		Test.startTest();
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:vfpConfiguration.bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
        System.assert(String.isNotBlank(airGcqController.gcqId));
		airGcqController.openFinalAirConfirmation();
        System.assert(airGcqController.draft != null && String.isNotEmpty(airGcqController.draft.id) && String.isNotEmpty(airGcqController.gcqBid.Form_Final_Air_Confirmation__c));
		airGcqController.attachdocument_objectid = airGcqController.gcqBid.id;
		airGcqController.loadDocuments = true;
		airGcqController.loadJournals = false;
		airGcqController.openAttachDocs();
        System.assert(airGcqController.attachDocumentList.isEmpty());
		airGcqController.documentRelationId = airGcqController.gcqBid.id;
		airGcqController.filename = 'Attach Test 1';
		airGcqController.body = 'data:text/plain;base64,VGVzdA==';
		airGcqController.doAttachmentLast();
        System.assert(String.isNotEmpty(airGcqController.newattachment_id) && String.isNotBlank(airGcqController.newattachment_name));
		airGcqController.documentRelationId = null;
		airGcqController.filename = 'Attach Test 2';
		airGcqController.body = 'data:text/plain;base64,VGVzdA==';
		airGcqController.newattachment_id = null;
		airGcqController.newattachment_name = null;
		airGcqController.doAttachmentLast();
        System.assert(String.isEmpty(airGcqController.newattachment_id) && String.isBlank(airGcqController.newattachment_name));
		Test.stopTest();
    }
}```

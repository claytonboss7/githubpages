---
layout: default
title: Dashboard_Tab_Contract_Forms_Test
parent: classes
---

```@isTest
public class Dashboard_Tab_Contract_Forms_Test{
	private static Dashboard_Tab_Contract_Forms formController;
	//
    static{
        DashboardDataFactory.createGTData(1);
		formController = new Dashboard_Tab_Contract_Forms();
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }
    @isTest static void Test_GT_OpenForm_RateAgreement(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Rate Agreement';
		formController.formValue = 'Form_Rate_Agreement__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getContactsBidsByVendor();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Rate_Agreement__c) && String.isNotEmpty(formController.draft.Id));
		String contactsJson = Dashboard_Tab_Contract_Forms.searchContactEmail('GtVendorContactTest');
        System.assert(String.isNotBlank(contactsJson));
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.isCongaSignSent = true;
		formController.saveBidAgreement();
		formController.draft.Id = null;
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Rate Agreement';
		formController.formValue = 'Form_Rate_Agreement__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Rate_Agreement__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Rate_Agreement__c from Bid__c where id =:formController.formBid.Id].Form_Rate_Agreement__c));
		formController.deactivateBidAgreement();
		Test.stopTest();
    }
    @isTest static void Test_GT_OpenForm_TransportationContract(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Transportation Contract';
		formController.formValue = 'Form_Transportation_Contract__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getContactsBidsByVendor();
		formController.getBidAgreementProductionAssociationContacts();
		formController.getBidAgreementCreditCards();
        System.assert(String.isNotBlank(formController.formBid.Form_Transportation_Contract__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Transportation_Contract__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_TripDetailsUpdate(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Trip Details Update';
		formController.formValue = 'Form_Trip_Details_Update__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Trip_Details_Update__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Trip_Details_Update__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_ContractToClient(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Contract To Client';
		formController.formValue = 'Form_Contract_to_Client__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Contract_to_Client__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Contract_to_Client__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_CounterNeeded(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Counter Needed';
		formController.formValue = 'Form_Counter_Needed__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Counter_Needed__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Counter_Needed__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_FinalContract(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Final Contract';
		formController.formValue = 'Form_Final_Contract__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Contract__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Contract__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_CreditCardChange(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Credit Card Change';
		formController.formValue = 'Form_Credit_Card_Change__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Credit_Card_Change__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Credit_Card_Change__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_EmailConfirmation(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
        DashboardConfigurationWrapper vfpConfiguration = new DashboardConfigurationWrapper();
        vfpConfiguration.productionId = [Select id from Opportunity where Name = 'Cats'].id;
        vfpConfiguration.parentId = [Select id from Ground__c where Recordtype.DeveloperName = 'GT_Trip_Details' limit 1].id;
        vfpConfiguration.bidId = bidId;
        vfpConfiguration.clientMap = new Map<Id,DashboardClientWrapper>();
		Dashboard_Tab_Contract_GCQ gtGcqController = new Dashboard_Tab_Contract_GCQ();
		gtGcqController.vfpConfiguration = vfpConfiguration;
		String subtripsSelected = '';
		gtGcqController.loadBidSubTrips();
		for(Ground__c gtBidSubtrip:[Select id from Ground__c where Bid_Sub_Trip__c =:bidId and RecordType.DeveloperName = 'GT_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + gtBidSubtrip.id : gtBidSubtrip.id;
		gtGcqController.tripsSelected = subtripsSelected;
		gtGcqController.openGCQ();
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Email Confirmation';
		formController.formValue = 'Form_Email_Confirmation__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Email_Confirmation__c) && String.isNotEmpty(formController.draft.Id) && formController.draft.Production_Assoc_Type__c == 'production_contacts');
        System.assert(!formController.dataContactPL.isEmpty());
        formController.draft.Production_Assoc_Contact_Id__c = formController.dataContactPL[0].getValue();
		formController.changeContactDataSelected();
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Email Confirmation';
		formController.formValue = 'Form_Email_Confirmation__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Email_Confirmation__c) && String.isNotEmpty(formController.draft.Id) && formController.draft.Production_Assoc_Type__c == 'production_contacts');
        System.assert(!formController.dataContactPL.isEmpty());
        formController.draft.Production_Assoc_Type__c = 'coordinators';
		formController.searchContactData();
        formController.draft.Production_Assoc_Contact_Id__c = formController.dataContactPL[0].getValue();
		formController.changeContactDataSelected();
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Email Confirmation';
		formController.formValue = 'Form_Email_Confirmation__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Email_Confirmation__c) && String.isNotEmpty(formController.draft.Id) && formController.draft.Production_Assoc_Type__c == 'coordinators');
		formController.openAttachGcq();
		formController.attachGcq_departureDate = String.valueOf(Date.Today().addDays(-1));
		formController.attachGcq_arrivalDate = String.valueOf(Date.Today().addDays(1));
		formController.searchAttachGcq();
        System.assert(!formController.isGcqEmpty && formController.isGcqSearched);
		Test.stopTest();
	}
    @isTest static void Test_GT_OpenForm_Cancellation(){
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId;
		ContentVersion contentVersionTest1 = new ContentVersion(Title = 'DocumentTest1', PathOnClient = '/DocumentTest1.txt', VersionData = Blob.valueOf('DocumentTest1'));
		insert contentVersionTest1;
		Id contentDocumentId = [Select Id, ContentDocumentId From ContentVersion Where Id =:contentVersionTest1.Id].ContentDocumentId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Cancellation';
		formController.formValue = 'Form_Cancellation_Letter__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Cancellation_Letter__c) && String.isNotEmpty(formController.draft.Id));
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = contentDocumentId;
		formController.sendEmail();
		formController.formBid.Id = null;
		formController.sendEmail();
		formController.formBid.Id = bidId;
		formController.form_attachs = 'Test';
		formController.sendEmail();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Cancellation';
		formController.formValue = 'Form_Cancellation_Letter__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Cancellation_Letter__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_RateAgreement(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Rate Agreement';
		formController.formValue = 'Form_Rate_Agreement__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getContactsBidsByVendor();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Rate_Agreement__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Rate_Agreement__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Rate_Agreement__c from Bid__c where id =:formController.formBid.Id].Form_Rate_Agreement__c));
		Test.stopTest();
    }
    @isTest static void Test_Freight_OpenForm_TransportationContract(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Transportation Contract';
		formController.formValue = 'Form_Transportation_Contract__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getContactsBidsByVendor();
		formController.getBidAgreementProductionAssociationContacts();
		formController.getBidAgreementCreditCards();
        System.assert(String.isNotBlank(formController.formBid.Form_Transportation_Contract__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Transportation_Contract__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_TripDetailsUpdate(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Trip Details Update';
		formController.formValue = 'Form_Trip_Details_Update__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Trip_Details_Update__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Trip_Details_Update__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_ContractToClient(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Contract To Client';
		formController.formValue = 'Form_Contract_to_Client__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Contract_to_Client__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Contract_to_Client__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_CounterNeeded(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Counter Needed';
		formController.formValue = 'Form_Counter_Needed__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Counter_Needed__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Counter_Needed__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_FinalContract(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Final Contract';
		formController.formValue = 'Form_Final_Contract__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Contract__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Contract__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_CreditCardChange(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Credit Card Change';
		formController.formValue = 'Form_Credit_Card_Change__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Credit_Card_Change__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Credit_Card_Change__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_EmailConfirmation(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
        DashboardConfigurationWrapper vfpConfiguration = new DashboardConfigurationWrapper();
        vfpConfiguration.productionId = [Select id from Opportunity where Name = 'Cats'].id;
        vfpConfiguration.parentId = [Select id from Freight__c where Recordtype.DeveloperName = 'Freight_Trip_Details' limit 1].id;
        vfpConfiguration.bidId = bidId;
        vfpConfiguration.clientMap = new Map<Id,DashboardClientWrapper>();
		Dashboard_Tab_Contract_FCQ freightFcqController = new Dashboard_Tab_Contract_FCQ();
		freightFcqController.vfpConfiguration = vfpConfiguration;
		String subtripsSelected = '';
		freightFcqController.loadBidSubTrips();
		for(Freight__c freightBidSubtrip:[Select id from Freight__c where Bid_Sub_Trip__c =:bidId and RecordType.DeveloperName = 'Freight_Sub_Trip_Details']) subtripsSelected += String.isNotBlank(subtripsSelected) ? ',' + freightBidSubtrip.id : freightBidSubtrip.id;
		freightFcqController.tripsSelected = subtripsSelected;
		freightFcqController.openFCQ();
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Email Confirmation';
		formController.formValue = 'Form_Email_Confirmation__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Email_Confirmation__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Email_Confirmation__c) && String.isNotEmpty(formController.draft.Id));
		formController.openAttachGcq();
		formController.attachGcq_departureDate = String.valueOf(Date.Today().addDays(-1));
		formController.attachGcq_arrivalDate = String.valueOf(Date.Today().addDays(1));
		formController.searchAttachGcq();
        System.assert(!formController.isGcqEmpty && formController.isGcqSearched);
		Test.stopTest();
	}
    @isTest static void Test_Freight_OpenForm_Cancellation(){
        DashboardDataFactory.createFreightData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Freight_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Freight';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Cancellation';
		formController.formValue = 'Form_Cancellation_Letter__c';
		formController.draftCode = null;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Cancellation_Letter__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Cancellation_Letter__c) && String.isNotEmpty(formController.draft.Id));
		Test.stopTest();
	}
    @isTest static void Test_Air_OpenForm_DepositDue(){
        DashboardDataFactory.createAirData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Deposit Due';
		formController.formValue = 'Form_Deposit_Due__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Deposit_Due__c) && String.isNotEmpty(formController.draft.Id));
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = null;
		formController.sendEmail();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Deposit Due';
		formController.formValue = 'Form_Deposit_Due__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Deposit_Due__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Deposit_Due__c from Bid__c where id =:formController.formBid.Id].Form_Deposit_Due__c));
		Test.stopTest();
    }
    @isTest static void Test_Air_OpenForm_Utilization(){
        DashboardDataFactory.createAirData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Utilization';
		formController.formValue = 'Form_Utilization__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Utilization__c) && String.isNotEmpty(formController.draft.Id));
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = null;
		formController.sendEmail();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Utilization';
		formController.formValue = 'Form_Utilization__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Utilization__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Utilization__c from Bid__c where id =:formController.formBid.Id].Form_Utilization__c));
		Test.stopTest();
    }
    @isTest static void Test_Air_OpenForm_NamesFinalPayment(){
        DashboardDataFactory.createAirData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Names & Final Payment';
		formController.formValue = 'Form_Names_Final_Payment__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Names_Final_Payment__c) && String.isNotEmpty(formController.draft.Id));
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = null;
		formController.sendEmail();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Names & Final Payment';
		formController.formValue = 'Form_Names_Final_Payment__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Names_Final_Payment__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Names_Final_Payment__c from Bid__c where id =:formController.formBid.Id].Form_Names_Final_Payment__c));
		Test.stopTest();
    }
    @isTest static void Test_Air_OpenForm_FinalChoice(){
        DashboardDataFactory.createAirData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Final Choice';
		formController.formValue = 'Form_Final_Choice__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Choice__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Choice__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Final_Choice__c from Bid__c where id =:formController.formBid.Id].Form_Final_Choice__c));
		Test.stopTest();
    }
    @isTest static void Test_Air_OpenForm_TicketedConfirmation(){
        DashboardDataFactory.createAirData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Ticketed Confirmation';
		formController.formValue = 'Form_Ticketed_Confirmation__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Ticketed_Confirmation__c) && String.isNotEmpty(formController.draft.Id));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Ticketed_Confirmation__c) && String.isNotEmpty(formController.draft.Id));
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Ticketed_Confirmation__c from Bid__c where id =:formController.formBid.Id].Form_Ticketed_Confirmation__c));
		Test.stopTest();
    }
    @isTest static void Test_Air_OpenForm_FinalAirConfirmation(){
        DashboardDataFactory.createAirData(1);
        Id bidId = [Select id from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].id;
        update new Bid__c(Id = bidId, Status__c = 'Contracted');
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId;
        DashboardConfigurationWrapper vfpConfiguration = new DashboardConfigurationWrapper();
        vfpConfiguration.productionId = [Select id from Opportunity where Name = 'Cats'].id;
        vfpConfiguration.bidId = bidId;
        vfpConfiguration.clientMap = new Map<Id,DashboardClientWrapper>();
		Dashboard_Tab_Contract_Air_GCQ airGcqController = new Dashboard_Tab_Contract_Air_GCQ();
		airGcqController.vfpConfiguration = vfpConfiguration;
		String segmentsSelected = '';
		airGcqController.loadBidSegments();
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Itinerary_Details__r.Bid_Itinerary__c =:bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		for(Air__c airBidSegment:[Select id, Air_Itinerary_Details__c, Air_Deviation_Details__c from Air__c where Air_Deviation_Details__r.Bid_Deviation__c =:bidId and RecordType.DeveloperName = 'Air_Segments' limit 2]) segmentsSelected += String.isNotBlank(segmentsSelected) ? ',' + airBidSegment.id : airBidSegment.id;
		airGcqController.segmentsSelected = segmentsSelected;
		airGcqController.openGCQ();
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Final Air Confirmation';
		formController.formValue = 'Form_Final_Air_Confirmation__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Air_Confirmation__c) && String.isNotEmpty(formController.draft.Id));
		formController.openAttachGcq();
		formController.attachGcq_departureDate = String.valueOf(Date.Today().addDays(-1));
		formController.attachGcq_arrivalDate = String.valueOf(Date.Today().addDays(1));
		formController.searchAttachGcq();
        System.assert(!formController.isGcqEmpty && formController.isGcqSearched);
		formController.selectedGcqId = airGcqController.gcqId;
		formController.attachdocument_objectid = bidId;
		formController.openAttachDocs();
        System.assert(formController.attachDocumentList.isEmpty());
		formController.documentRelationId = bidId;
		formController.filename = 'Attach Test 1';
		formController.body = 'data:text/plain;base64,VGVzdA==';
		formController.doAttachmentLast();
        System.assert(String.isNotEmpty(formController.newattachment_id) && String.isNotBlank(formController.newattachment_name));
		formController.documentRelationId = null;
		formController.filename = 'Attach Test 2';
		formController.body = 'data:text/plain;base64,VGVzdA==';
		formController.newattachment_id = null;
		formController.newattachment_name = null;
		formController.doAttachmentLast();
        System.assert(String.isEmpty(formController.newattachment_id) && String.isBlank(formController.newattachment_name));
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Final Air Confirmation';
		formController.formValue = 'Form_Final_Air_Confirmation__c';
		formController.draftCode = formController.draft.Name;
		formController.openForm();
        System.assert(String.isNotBlank(formController.formBid.Form_Final_Air_Confirmation__c) && String.isNotEmpty(formController.draft.Id));
		formController.selectedGcqId = 'Test';
		formController.saveBidAgreement();
		formController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Final_Air_Confirmation__c from Bid__c where id =:formController.formBid.Id].Form_Final_Air_Confirmation__c));
		Test.stopTest();
	}
	//Changes as per 175349270
	@isTest static void Test_GT_OpenForm_GCIP(){
		Bid__c bidId = [Select id,Production__c,Form_GT_GCIP__c,Vendor__c,Housing__c,
		Contracting_Back_End_Coordinator__c from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].get(0);
        update new Bid__c(Id = bidId.id, Status__c = 'Contracted',Form_GT_GCIP__c = '',Vendor__c = null,Contracting_Back_End_Coordinator__c=null);
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId.id;
		Test.startTest();
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Ground Transportation Procedures';
		formController.formValue = 'Form_Create_GCIP__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getContactsBidsByVendor();
		formController.getBidAgreementProductionAssociationContacts();
        //System.assert(String.isNotBlank(formController.formBid.Form_Create_GCIP__c));
		String contactsJson = Dashboard_Tab_Contract_Forms.searchContactEmail('GtVendorContactTest');
        //System.assert(String.isNotBlank(contactsJson));
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.isCongaSignSent = true;
		formController.saveBidAgreement();
		formController.draft.Id = null;
		formController.saveBidAgreement();
		formController.isBidAgreementRendered = false;
		formController.formLabel = 'Ground Transportation Procedures';
		formController.formValue = 'Form_Create_GCIP__c';
		//formController.draftCode = formController.draft.Name;
		formController.draftCode = null;
		formController.openForm();
		formController.bindAttentionDetails();				//Changes as per 175349270
		formController.newFormGCIPTask();					//Changes as per 175349270
		String sendEmail = Dashboard_Tab_Contract_Forms.sendEmail('rhoffman@cloudcreations.com','','','Email Test 1','','',bidId.Production__c,bidId.Housing__c);				//Changes as per 175349270
		formController.sendEmailFormWithAttachs();			//Changes as per 175349270
		//System.assert(String.isNotBlank(formController.formBid.Form_Create_GCIP__c));
		formController.deactivateBidAgreement();
        //System.assert(String.isEmpty([Select Id, Form_Create_GCIP__c from Bid__c where id =:formController.formBid.Id].Form_Create_GCIP__c));
		formController.deactivateBidAgreement();
		Test.stopTest();
	}
	//Changes as per 175349270
	@isTest static void Test_GT_OpenForm_NegativeCases1(){
		Bid__c bidId = [Select id,Production__c,GT__c,Vendor__c from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].get(0);
        update new Bid__c(Id = bidId.id, Status__c = 'Contracted', GT__c = null, Vendor__c = null);
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId.id;

		Test.startTest();
		//Creating Ground__c
		Id Sales_GT_Details = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
		.get('Sales_GT_Details')
		.getRecordTypeId();
		Ground__c obj = new Ground__c();
		obj.Production_Ground__c = bidId.Production__c;
		obj.RecordTypeId = Sales_GT_Details;
		obj.Bid__c = bidId.id;
		insert obj;

		//Rate Agreement
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Rate Agreement';
		formController.formValue = 'Form_Rate_Agreement__c';
		formController.openForm();

		//Rate Agreement
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Trip Details Update';
		formController.formValue = 'Form_Trip_Details_Update__c';
		formController.openForm();

		//Transportation Contract
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Transportation Contract';
		formController.formValue = 'Form_Transportation_Contract__c';
		formController.openForm();

		Test.stopTest();
	}
	//Changes as per 175349270
	@isTest static void Test_GT_OpenForm_NegativeCases2(){
		Bid__c bidId = [Select id,Production__c,GT__c,Vendor__c from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].get(0);
        update new Bid__c(Id = bidId.id, Status__c = 'Contracted', GT__c = null, Vendor__c = null);
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId.id;

		Test.startTest();
		//Creating Ground__c
		Id Sales_GT_Details = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
		.get('Sales_GT_Details')
		.getRecordTypeId();
		Ground__c obj = new Ground__c();
		obj.Production_Ground__c = bidId.Production__c;
		obj.RecordTypeId = Sales_GT_Details;
		obj.Bid__c = bidId.id;
		insert obj;

		//Credit Card Change
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Credit Card Change';
		formController.formValue = 'Form_Credit_Card_Change__c';
		formController.openForm();

		//Email Confirmation
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Email Confirmation';
		formController.formValue = 'Form_Email_Confirmation__c';
		formController.openForm();
	

		Test.stopTest();
	}
	//Changes as per 175349270
	@isTest static void Test_GT_OpenForm_NegativeCases3(){
		Bid__c bidId = [Select id,Production__c,GT__c,Vendor__c from Bid__c where Recordtype.DeveloperName = 'GT_Bid' limit 1].get(0);
        update new Bid__c(Id = bidId.id, Status__c = 'Contracted', GT__c = null, Vendor__c = null);
		formController.bidParentSObject = 'Ground';
		formController.bidContractId = bidId.id;

		Test.startTest();
		//Creating Ground__c
		Id Sales_GT_Details = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName()
		.get('Sales_GT_Details')
		.getRecordTypeId();
		Ground__c obj = new Ground__c();
		obj.Production_Ground__c = bidId.Production__c;
		obj.RecordTypeId = Sales_GT_Details;
		obj.Bid__c = bidId.id;
		insert obj;

		//Ground Transportation Procedures
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Ground Transportation Procedures';
		formController.formValue = 'Form_Create_GCIP__c';
		formController.openForm();

		//Cancellation
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Cancellation';
		formController.formValue = 'Form_Cancellation_Letter__c';
		formController.openForm();

		//Counter Needed
		formController.loadForms();
		System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Counter Needed';
		formController.formValue = 'Form_Counter_Needed__c';
		formController.openForm();

		Test.stopTest();
	}
	@isTest static void Test_Air_OpenForm_NegativeCases1(){
        DashboardDataFactory.createAirData(1);
        Bid__c bidId = [Select id,Air__c,Client_Deposit_Due_Date__c,Client_Utilization_Date__c  from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].get(0);
        update new Bid__c(Id = bidId.id, Status__c = 'Contracted',Air__c = null,Client_Deposit_Due_Date__c = Date.today(),Client_Utilization_Date__c = Date.today());
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId.id;
		Test.startTest();

		//Deposit Due
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Deposit Due';
		formController.formValue = 'Form_Deposit_Due__c';
		formController.draftCode = null;
		formController.openForm();
		formController.getBidAgreementProductionAssociationContacts();
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = null;
		formController.sendEmail();

		//Utilization
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Utilization';
		formController.formValue = 'Form_Utilization__c';
		formController.draftCode = null;
		formController.openForm();
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = null;
		formController.sendEmail();


		Test.stopTest();
	}
	@isTest static void Test_Air_OpenForm_NegativeCases2(){
        DashboardDataFactory.createAirData(1);
        Bid__c bidId = [Select id,Air__c,Client_Names_Final_Payment__c from Bid__c where Recordtype.DeveloperName = 'Air_Bid' limit 1].get(0);
        update new Bid__c(Id = bidId.id, Status__c = 'Contracted',Air__c = null,Client_Names_Final_Payment__c = Date.today());
		formController.bidParentSObject = 'Air';
		formController.bidContractId = bidId.id;
		Test.startTest();

		//Names & Final Payment
		formController.loadForms();
        System.assert(String.isNotBlank(formController.formBid.Id));
		formController.formLabel = 'Names & Final Payment';
		formController.formValue = 'Form_Names_Final_Payment__c';
		formController.draftCode = null;
		formController.openForm();
		formController.form_to = 'Test@test.com';
		formController.form_cc = '';
		formController.form_bcc = '';
		formController.form_subject = 'Email Test 1';
		formController.form_body = 'EmailBody Test 1';
		formController.form_attachs = null;
		formController.sendEmail();

		Test.stopTest();
	}
}```

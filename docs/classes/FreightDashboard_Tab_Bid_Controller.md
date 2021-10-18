---
layout: default
title: FreightDashboard_Tab_Bid_Controller
parent: classes
---

```global class FreightDashboard_Tab_Bid_Controller {
    public DashboardConfigurationWrapper vfpConfiguration {get;set;}
    public Opportunity opportunity {get;set;}
    public String opportunityId {get;set;}
    public Integer tripBidNumber {get;set;}
    public Integer totalRecsBids {get;set;}
    public Map<Integer,BidWrapper> bidDataMap {get;set;}
    public Bid__c bidData {get;set;}
    public FreightDashboard freightDashboard {get;set{bidDataMap = value.bidDataMap;freightDashboard = value;}}
    public String itineraryId {get;set;}
    public List<SelectOption> contactsBidsByVendor {get;set;}
    public String contactPrimarySelected {get;set;}
    public List<Freight__c> bidSubTrips {get;set;}
    public Map<Id, List<Freight__c>> bidSubTripEquipmentsMap {get;set;}
    public Boolean isPageLoaded {get;set;}
    public Boolean loadDocuments {get;set;}
    public String modal {get;set;}
    public String equipmentrequestedJson {get;set;}
    private Map<String, APXTConga4__Conga_Merge_Query__c> congaQueriesMap;
    public String congaQueriesJson {get;set;}
    //PreviewOptions
    public String previewBidOptions_congaQueriesJson {get;set;}
    public String previewBidOptions_congaTemplateId {get;set;}
    //BidAgrement
    public Draft__c draft {get;set;}
    public List<Freight__c> bidAgreementSubTrips {get;set;}
    public List<Freight__c> bidAgreementVehicles {get;set;}
    public List<Concessions__c> bidAgreementConcessions {get;set;}
    public String journal_bidjournalRT {get;set;}
    public Revenue__c bidAgreementRevenue {get;set;}
    public Contact bidPrimaryContact {get;set;}
    public Contact bidAgreementPrimaryContact {get;set;}
    public Contact bidAgreementAttentionContact {get;set;}
    public Boolean isBidAgreementRendered {get;set;}
    public Boolean isResendBidRendered {get;set;}
    public Boolean isReleaseBidRendered {get;set;}
    public String bidAgreement_type {get;set;}
    public String bidAgreement_to {get;set;}
    public String bidAgreement_cc {get;set;}
    public String bidAgreement_bcc {get;set;}
    public String bidAgreement_message {get;set;}
    public String bidAgreement_terms {get;set;}
    public String bidAgreement_lastModifiedBy {get;set;}
    public String bidAgreement_congaEmailTemplateId {get;set;}
    public String bidAgreement_congaTemplateId {get;set;}
    public String bidAgreement_congaSignTemplateId {get;set;}
    public String bidAgreement_emailFromUserId {get;set;}
    public String bidAgreement_congaEmailFromId {get;set;}
    public String coordinatorGT {get;set;}
    public Boolean isCongaSignSent {get;set;}
    public String emailResult {get;set;}
    //ResendBid
    public Map<String,List<ContactWrapper>> contactsByVendorBidMap {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendorParentBidMap {get;set;}
    public Map<String,List<SelectOption>> contactSelectOptionBidMap {get;set;}
    public String vendorcontact_actual_id {get;set;}
    public String resendBidAgreement_contactPrimary {get;set;}
    public String resendBidAgreement_congaEmailSubject {get;set;}
    public String resendBidAgreement_congaEmailTemplateId {get;set;}
    public String resendBidAgreement_congaQueriesJson {get;set;}
    public String resendBidAgreement_congaTemplateId {get;set;}
    public String resendBidAgreement_emailFromUserId {get;set;}
    public String resendBidAgreement_congaEmailFromId {get;set;}
    //ReleaseBid
    public String releaseVendorcontact_actual_id {get;set;}
    public String releaseVendoraccount_actual_id {get;set;}
    public Map<String,List<SelectOption>> contactSelectOption_releaseMap {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendor_releaseMap {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendorParent_releaseMap {get;set;}
    public String releaseEmailBid_body {get;set;}
    public String emailbid_to {get;set;}
    public String emailbid_cc {get;set;}
    public String emailbid_bcc {get;set;}
    public String emailbid_subject {get;set;}
    public String emailbid_id {get;set;}
    public String emailbid_primarycontactname {get;set;}
    public String emailAttachs {get;set;}
    public String emailMessage {get;set;}
    //AddContacts
    public String messageCreateContact {get;set;}
    public Contact vendorContact {get;set;}
    public String vendorContact_id {get;set;}
    public List<SelectOption> contact_DesignationTitle {get;set;}
    //Attachs
    public String filename {get;set;}
    transient public String body {get;set;}
    public List<ContentDocument> attachDocumentList {get;set;}
    public String attachdocument_objectid {get;set;}
    public String newattachment_id {get;set;}
    public String newattachment_name {get;set;}
    public List<ContentDocument> documentBidList {get;set;}
    public Integer documentListFirst {get;set;}
    public Integer documentListPage {get;set;}
    public Integer documentListLastPage {get;set;}
    public List<Integer> documentListPages {get;set;}
    public String documentId {get;set;}
    public String documentTitle {get;set;}
    public String documentRelationId {get;set;}
    //Bid History
    public List<SelectOption> production_markettypes {get;set;}
    public Freight__c freightFilter {get;set;}
    public static String orderBidHistory {get;set;}
    public static String orderBidHistoryOrientation {get;set;}
    public Boolean orderCheckBidHistory {get;set;}
    public Boolean orderChangeBidHistory {get;set;}
    public List<BidVendorWrapper> bidRelatedVendorList {get;set;}
    public String bidhistorysearch_market {get;set;}
    public Date bidhistorysearch_from {get;set;}
    public Date bidhistorysearch_to {get;set;}
    public Boolean bidhistorysearch_onlyirstays {get;set;}
    public Map<String,Revenue__c> rateBidMap {get;set;}
    //Rate Details
    public Revenue__c bidRevenue {get;set;}
    //Additional Fees
    public String concessionJson {get;set;}
    public List<Concessions__c> concessionsRequestedBid {get;set;}
    public String concessionRequestedActual {get;set;}
    public String concessionNoteActual {get;set;}
    public String concessionActual {get;set;}
    public String concessionIncludedActual {get;set;}
    public String concessionRateActual {get;set;}
    public String concessionOrderActual {get;set;}
    //Trip Details
    public Map<String,Boolean> hasFreightMap {get;set;}
    public String freight_FreightSubStripDetailsRT {get;set;}
    public String subtripIdActual {get;set;}
    public String equipmentActualId {get;set;}
    public String equipmentActualOrder {get;set;}
    public String newequipment_subtripid {get;set;}
    public String newequipment_line {get;set;}
    public String newequipment_vehicle {get;set;}
    public Date newequipment_startdate {get;set;}
    public String newequipment_starttime {get;set;}
    public Date newequipment_enddate {get;set;}
    public String newequipment_endtime {get;set;}
    public String newequipment_traveltype {get;set;}
    public String newequipment_grouptype {get;set;}
    public String newequipment_locationpickuptype {get;set;}
    public String newequipment_locationpickupdetails {get;set;}
    public String newequipment_locationdropofftype {get;set;}
    public String newequipment_locationdropoffdetails {get;set;}
    public String newequipment_notes {get;set;}
    public String newtravel_tripcontents {get;set;}
    public Boolean newequipment_updatemaster {get;set;}
    public String freight_FreightEquipmentDetailsRT {get;set;}
    public Freight__c newEquipment {get;set;}
    public Freight__c newVehicleBid {get;set;}
    public List<SelectOption> freight_amenitiesPL {get;set;}
    public List<Freight__c> vehiclesByBidList {get;set;}
    public String vehicleIdActual {get;set;}
    public String vehicle_vehicleref {get;set;}
    public String vehicle_vehicletype {get;set;}
    public String vehicle_capacity {get;set;}
    public String vehicle_make {get;set;}
    public String vehicle_model {get;set;}
    public String vehicle_year {get;set;}
    public String vehicle_amenities {get;set;}
    public String vehicle_truck {get;set;}
    public String vehicle_equipmentrequested {get;set;}
    public String freight_vehicletypeRT {get;set;} 
    public String url {get;set;}
    //Locked
    public String bidid_locked {get;set;}
    public Boolean bidstatus_locked {get;set;}
    //BidJournals
    public Boolean isBidJournalsRendered {get;set;}
    public List<SelectOption> freight_triptypePL {get;set;}
    public Boolean tripHaveContracted {get;set;}
    
    public String contractingBidId {get;set;}
    public String contractingParentId {get;set;}
    public String airlineInfoJson {get;set;}
    public String equipmentJson {get;set;}
    public Map<String,String> symbolMap {get;set;}
    public String grouptypeJson {get;set;}
    
    public String communityURLvalue {get;set;}//victor
    
    public FreightDashboard_Tab_Bid_Controller() {
        bidData = new Bid__c();
        System.debug('FreightDashboard_Tab_Bid_Controller.tripBidNumber: ' + tripBidNumber);
        journal_bidjournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByName().get('Bid Journal') != null ? Schema.SObjectType.Journal__c.getRecordTypeInfosByName().get('Bid Journal').getRecordTypeId() : null;
        Init();
    }
    public void Init(){
        vendorContact = new Contact();
        freight_FreightSubStripDetailsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Freight__c' and DeveloperName = 'Freight_Sub_Trip_Details'].Id;
        freight_FreightEquipmentDetailsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Freight__c' and DeveloperName = 'Equipment_Details'].Id;
        freight_vehicletypeRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Freight__c' and DeveloperName = 'Vehicle_Type'].Id;
        url = ApexPages.currentPage().getHeaders().get('Host');
        
        production_markettypes = new List<SelectOption>();
        production_markettypes.add(new SelectOption('','--Select--'));
        production_markettypes.addAll(FreightDashboardController.PickThePicklist('Opportunity','Market_Type__c'));
        freightFilter = new Freight__c();
        List<wrapperSearchPL> consValueList = new List<wrapperSearchPL>();
        Map<Object,List<String>> dependValuesByControlValue = FreightDashboardController.getDependentPicklistValues(Concessions__c.Concessions_Requested__c);
        for(Object k1 : dependValuesByControlValue.keySet()){
            if((String) k1 == 'Freight'){
                for(String k2: dependValuesByControlValue.get(k1)){
                    consValueList.add(new wrapperSearchPL(k2,k2));
                }
            }
        }
        concessionJson = JSON.serialize(consValueList);
        concessionsRequestedBid = new List<Concessions__c>();
        bidSubTrips = new List<Freight__c>();
        newEquipment = new Freight__c();
        newVehicleBid = new Freight__c();
        freight_amenitiesPL = new List<SelectOption>();
        Schema.DescribeFieldResult fieldResult = Freight__c.Amenities__c.getDescribe();
        List<Schema.PicklistEntry> ple = fieldResult.getPicklistValues();
        for( Schema.PicklistEntry pickListVal : ple){
            freight_amenitiesPL.add(new SelectOption(pickListVal.getValue(),pickListVal.getLabel()));
        }
        rateBidMap = new Map<String,Revenue__c>();
        draft = new Draft__c();
        isPageLoaded = isBidAgreementRendered = isResendBidRendered = isBidJournalsRendered = isReleaseBidRendered = isCongaSignSent = false;
        freight_triptypePL = new List<SelectOption>();
        
        consValueList = new List<wrapperSearchPL>();
        for(SelectOption so : FreightDashboardController.PickThePicklist('Freight__c','Equipment_requested__c')){
            consValueList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        equipmentrequestedJson = JSON.serialize(consValueList);
        
        consValueList = new List<wrapperSearchPL>();
        for(SelectOption so : FreightDashboardController.PickThePicklist('Freight__c','Equipment_requested__c')){
            consValueList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        equipmentrequestedJson = JSON.serialize(consValueList);
        
        consValueList = new List<wrapperSearchPL>();
        for(SelectOption so : FreightDashboardController.PickThePicklist('Freight__c','Group_Type__c')){
            consValueList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        grouptypeJson = JSON.serialize(consValueList);    
        
        consValueList = new List<wrapperSearchPL>();
        consValueList.add(new wrapperSearchPL('Air Freight','Air Freight'));
        consValueList.add(new wrapperSearchPL('Sea Freight','Sea Freight'));
        consValueList.add(new wrapperSearchPL('Truck','Truck'));
        consValueList.add(new wrapperSearchPL('Temperature Controlled Truck','Temperature Controlled Truck'));
        consValueList.add(new wrapperSearchPL('28 Foot Van Hill Trailers','28 Foot Van Hill Trailers'));
        consValueList.add(new wrapperSearchPL('Drop Deck Van Trailers','Drop Deck Van Trailers'));
        consValueList.add(new wrapperSearchPL('53-Foot Van Trailers','53-Foot Van Trailers'));
        consValueList.add(new wrapperSearchPL('Expandable Trailers','Expandable Trailers'));
        consValueList.add(new wrapperSearchPL('Gooseneck Equipped Tractors','Gooseneck Equipped Tractors'));
        consValueList.add(new wrapperSearchPL('53-Foot Drop Deck Curtain-side Trailers','53-Foot Drop Deck Curtain-side Trailers'));
        consValueList.add(new wrapperSearchPL('Vending Trailers','Vending Trailers'));
        consValueList.add(new wrapperSearchPL('Climate Controlled Trailers','Climate Controlled Trailers'));
        consValueList.add(new wrapperSearchPL('Auto Transport Trailers','Auto Transport Trailers'));
        consValueList.add(new wrapperSearchPL('Drop Deck Flatbed Trailers','Drop Deck Flatbed Trailers'));
        consValueList.add(new wrapperSearchPL('Gooseneck Trailers','Gooseneck Trailers'));
        consValueList.add(new wrapperSearchPL('Rollback trucks','Rollback trucks'));
        consValueList.add(new wrapperSearchPL('Belly Box Trailers','Belly Box Trailers'));
        consValueList.add(new wrapperSearchPL('Hospitality Trailers','Hospitality Trailers'));
        consValueList.add(new wrapperSearchPL('Lift gate Van Trailers','Lift gate Van Trailers'));
        consValueList.add(new wrapperSearchPL('Tag Trailers','Tag Trailers'));
        consValueList.add(new wrapperSearchPL('Motorsports Trailers','Motorsports Trailers'));
        consValueList.add(new wrapperSearchPL('Long Wheelbase Trailers','Long Wheelbase Trailers'));   
        equipmentJson = JSON.serialize(consValueList);
        
        Community_Settings__c comSetCS = Community_Settings__c.getInstance();
		communityURLvalue = comSetCS.Community_URL__c;
    }
    public void viewContractingDetailByBid(){
        if(vfpConfiguration != null){
            vfpConfiguration.bidId = contractingBidId;
            vfpConfiguration.parentId = contractingParentId;
            vfpConfiguration.productionId = opportunityId;
            vfpConfiguration.parentSObject = 'Freight';
        }
    }
    public void uncontractBid(){
        if(bidDataMap.get(tripBidNumber).b.Status_Previous__c != null && bidDataMap.get(tripBidNumber).b.Status_Previous__c != ''){
            update new Bid__c(Id= bidDataMap.get(tripBidNumber).b.Id,Status__c = bidDataMap.get(tripBidNumber).b.Status_Previous__c,Status_Previous__c=null,Contracted_date_time__c=null);
            update new Freight__c(Id = vfpConfiguration.parentId, Status__c = 'Bid Request Stage');
            /*
            switch on vfpConfiguration.parentSObject {
                when 'Housing' { update new Housing__c(Id = vfpConfiguration.parentId, Status_CC__c = 'Bid Request Stage'); }
                when 'Ground' { update new Ground__c(Id = vfpConfiguration.parentId, Status_Ground__c = 'Bid Request Stage'); }
                when 'Freight'{ update new Freight__c(Id = vfpConfiguration.parentId, Status__c = 'Bid Request Stage'); }
                when 'Air'{ update new Air__c(Id = vfpConfiguration.parentId, Status__c = 'Bid Request Stage'); }
            }
            */
            bidDataMap.get(tripBidNumber).b.Status__c = bidDataMap.get(tripBidNumber).b.Status_Previous__c;
            bidData.Status__c = bidDataMap.get(tripBidNumber).b.Status_Previous__c;
            if(bidDataMap.get(tripBidNumber).b.Freight__c != null){
                //update new Freight__c(Id=bidDataMap.get(tripBidNumber).b.Freight__c,Status__c=bidDataMap.get(tripBidNumber).b.Freight__r.Status_Previous__c);
                update new Freight__c(Id=bidDataMap.get(tripBidNumber).b.Freight__c,Status__c='Bid Request Stage');
                List<Itinerary__c> itineraryAuxList =  [SELECT Id FROM Itinerary__c WHERE Freight__c =: bidDataMap.get(tripBidNumber).b.Freight__c AND RecordType.DeveloperName = 'Freight_Itinerary'];
                //if(itineraryAuxList.size() > 0) update new Itinerary__c(Id = itineraryAuxList[0].Id,Status__c = bidDataMap.get(tripBidNumber).b.Freight__r.Status_Previous__c);
                if(itineraryAuxList.size() > 0) update new Itinerary__c(Id = itineraryAuxList[0].Id,Status__c = 'Bid Request Stage');
            }
            
            /*List<Freight__c> subTripList = [SELECT Id FROM Freight__c WHERE Bid_Sub_Trip__c =: bidDataMap.get(tripBidNumber).b.Id AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'];
            delete [SELECT Id FROM Freight__c WHERE Freight_Sub_Trip_Details__c IN: subTripList AND RecordType.DeveloperName = 'Equipment_Details']; //equipments bid
            delete [SELECT Id FROM Concessions__c WHERE Bid__c =: bidDataMap.get(tripBidNumber).b.Id]; //additional fees
            delete [SELECT Id FROM Freight__c WHERE Bid__c =: bidDataMap.get(tripBidNumber).b.Id AND RecordType.DeveloperName = 'Vehicle_Type']; //vehicles bid
            
            //DELETE TRACES
            delete [SELECT Id FROM Task WHERE WhatId =: bidDataMap.get(tripBidNumber).b.Id AND Order__c <> NULL];
            //DELETE GCQ
            //List<Freight__c> subTripList = [SELECT Id, Name FROM Freight__c WHERE Bid_Sub_Trip__c =: bidDataMap.get(tripBidNumber).b.Id AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'];
            //if(!subTripList.isEmpty()) delete [SELECT Id FROM Sub_Trip_GCQ__c WHERE GT_Sub_Trip_Details__c IN: subTripList];
            
            delete subTripList;*/
        }
        
        getBidInformation();
    }
    public void contractBid(){
        Dashboard__c cs = Dashboard__c.getOrgDefaults();
        String contractidnumber = getNumberFormat(Integer.valueOf(cs.Contract_ID__c));
        update new Bid__c(Id=bidDataMap.get(tripBidNumber).b.Id,Contract_ID__c=contractidnumber,Status_Previous__c=bidDataMap.get(tripBidNumber).b.Status__c,Status__c = 'Contracted',Final_Status__c = 'In Contracting',Contracted_date_time__c=system.now());
        bidDataMap.get(tripBidNumber).b.Status_Previous__c = bidDataMap.get(tripBidNumber).b.Status__c;
        bidData.Status_Previous__c = bidDataMap.get(tripBidNumber).b.Status__c;
        bidData.Contract_ID__c = contractidnumber;
        bidData.Status__c = 'Contracted';
        bidDataMap.get(tripBidNumber).b.Contract_ID__c = contractidnumber;
        cs.Contract_ID__c = cs.Contract_ID__c + 1;
        update cs;
        system.debug(bidData.Status__c);
        system.debug(bidData.Status__c);
        if(tripHaveContracted){
            if(bidDataMap.get(tripBidNumber).b.Freight__c != null){
                Freight__c f = [SELECT Id, Start_Date__c, End_Date__c, Start_City__c, End_City__c, Description__c, Freight_Preferences__c, Status__c, Trace_Date__c, Deadline_Date__c,
                                Group_Type__c, Service_Type__c FROM Freight__c WHERE Id =: bidDataMap.get(tripBidNumber).b.Freight__c];
                Itinerary__c it = [SELECT Id, Production__c, Status__c, Start_Date__c, End_Date__c, Freight__c, City__c FROM Itinerary__c WHERE Freight__c =: bidDataMap.get(tripBidNumber).b.Freight__c];
                Freight__c newFreight = f.clone();
                newFreight.Vendor__c = bidDataMap.get(tripBidNumber).b.Vendor__c;
                newFreight.Status_Previous__c = bidDataMap.get(tripBidNumber).b.Freight__r.Status__c;
                newFreight.Status__c = 'Contracted';
                newFreight.Production__c = bidDataMap.get(tripBidNumber).b.Production__c;
                newFreight.Vendor_lookup__c = bidData.Vendor__c;
                newFreight.RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId();
                system.debug(newFreight);
                insert newFreight;
                
                cloneInformationToFreight(bidDataMap.get(tripBidNumber).b,newFreight,freight_vehicletypeRT,freight_FreightSubStripDetailsRT,freight_FreightEquipmentDetailsRT);
                
                bidDataMap.get(tripBidNumber).b.Freight__c = newFreight.Id;
                bidData.Freight__c = newFreight.Id;
                update bidData;
                
                Itinerary__c newItinerary = it.clone();
                newItinerary.Status__c = 'Contracted';
                newItinerary.Production__c = bidDataMap.get(tripBidNumber).b.Production__c;
                newItinerary.Freight__c = newFreight.Id;
                system.debug(newItinerary);
                insert newItinerary;
                
                //cloneInformationToBid(bidDataMap.get(tripBidNumber).b,freight_vehicletypeRT,freight_FreightSubStripDetailsRT,freight_FreightEquipmentDetailsRT);
                
                tripBidNumber = null;
                bidDataMap = new Map<Integer,BidWrapper>();
            }
        }else{
            if(bidDataMap.get(tripBidNumber).b.Freight__c != null){
                update new Freight__c(Id=bidDataMap.get(tripBidNumber).b.Freight__c,Vendor__c=bidDataMap.get(tripBidNumber).b.Vendor__c,Status_Previous__c=bidDataMap.get(tripBidNumber).b.Freight__r.Status__c,Status__c='Contracted');
                List<Itinerary__c> itineraryAuxList =  [SELECT Id FROM Itinerary__c WHERE Freight__c =: bidDataMap.get(tripBidNumber).b.Freight__c AND RecordType.DeveloperName = 'Fregiht_Itinerary'];
                if(itineraryAuxList.size() > 0) update new Itinerary__c(Id = itineraryAuxList[0].Id,Status__c = 'Contracted');
                //cloneInformationToBid(bidDataMap.get(tripBidNumber).b,freight_vehicletypeRT,freight_FreightSubStripDetailsRT,freight_FreightEquipmentDetailsRT);
            }
        }
        getBidInformation();
    }
    public static void cloneInformationToFreight(Bid__c dataBid, Freight__c fData, String freight_vehicletypeRT, String freight_FreightSubStripDetailsRT, String freight_FreightEquipmentDetailsRT){
        Freight__c gAux;
        List<Freight__c> gAuxList;
        Concessions__c cAux;
        List<Concessions__c> cAuxList;
        
        Map<String,List<Freight__c>> vehiclesDataMap = new Map<String,List<Freight__c>>();
        for(Freight__c vData : [SELECT Id, Production__c, Equipment__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, Freight_Trip_Details__c
                               FROM Freight__c WHERE RecordType.Name = 'Vehicle Type' AND Production__c =: dataBid.Production__c AND Freight_Trip_Details__c =: dataBid.Freight__c
                               AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_details__c = NULL]){
                                   gAuxList = vehiclesDataMap.get(vData.Freight_Trip_Details__c) != null ? vehiclesDataMap.get(vData.Freight_Trip_Details__c) : new List<Freight__c>();
                                   gAuxList.add(vData);
                                   vehiclesDataMap.put(vData.Freight_Trip_Details__c,gAuxList.clone());
                               }
        
        Map<String,List<Concessions__c>> concessionsDataMap = new Map<String,List<Concessions__c>>();
        for(Concessions__c cData : [SELECT Id, Agreed__c, Freight__c, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, CurrencyIsoCode, Notes__c, Order__c
                                    FROM Concessions__c WHERE Freight__c =: dataBid.Freight__c AND Production__c =: dataBid.Production__c
                                    AND Bid__c = NULL AND Housing__c = NULL AND GT__c = NULL]){
                                        cAuxList = concessionsDataMap.get(cData.Freight__c) != null ? concessionsDataMap.get(cData.Freight__c) : new List<Concessions__c>();
                                        cAuxList.add(cData);
                                        concessionsDataMap.put(cData.Freight__c,cAuxList.clone());
                                    }
        
        Map<String,List<Freight__c>> subtripDataMap = new Map<String,List<Freight__c>>();
        Set<String> subtripDataIds = new Set<String>();
        for(Freight__c subtripData : [SELECT Id, Service_Type__c, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, Freight_Trip_Details__c
                                     FROM Freight__c 
                                     WHERE RecordType.DeveloperName = 'Freight_Sub_Trip_Details' AND Freight_Trip_Details__c =: dataBid.Freight__c ORDER BY Trip_Order__c ASC]){
                                         subtripDataIds.add(subtripData.Id);
                                         gAuxList = subtripDataMap.get(subtripData.Freight_Trip_Details__c) != null ? subtripDataMap.get(subtripData.Freight_Trip_Details__c) : new List<Freight__c>();
                                         gAuxList.add(subtripData);
                                         subtripDataMap.put(subtripData.Freight_Trip_Details__c,gAuxList.clone());
                                     }
        
        Map<String,List<Freight__c>> travelsBySubTripMapAux = new Map<String,List<Freight__c>>();
        if(subtripDataIds.size() > 0){
            for(Freight__c g : [SELECT Id, Line__c, Equipment__c, Vehicle_Ref__c, Freight_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c,
                               Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c
                               FROM Freight__c WHERE RecordType.DeveloperName = 'Equipment_Details' AND Freight_Sub_Trip_Details__c =: subtripDataIds ORDER BY Line__c ASC]){
                                   gAuxList = travelsBySubTripMapAux.get(g.Freight_Sub_Trip_Details__c) != null ? travelsBySubTripMapAux.get(g.Freight_Sub_Trip_Details__c) : new List<Freight__c>();
                                   gAuxList.add(g);
                                   travelsBySubTripMapAux.put(g.Freight_Sub_Trip_Details__c,gAuxList.clone());
                                   
                               }
        }
        
        gAuxList = new List<Freight__c>();
        cAuxList = new List<Concessions__c>();
        Map<Integer,Freight__c> subtripInsertMap = new Map<Integer,Freight__c>();
        Map<Integer,List<Freight__c>> travelInsertMap = new Map<Integer,List<Freight__c>>();
        Integer cx = 1;
        List<Freight__c> travelListAux = new List<Freight__c>();

        if(vehiclesDataMap.get(dataBid.Freight__c) != null){
            for(Freight__c g : vehiclesDataMap.get(dataBid.Freight__c)){
                gAux = g.clone();
                gAux.Id = null;
                gAux.RecordTypeId = freight_vehicletypeRT;
                gAux.Production__c = dataBid.Production__c;
                gAux.Freight_Trip_Details__c = fData.Id;
                gAuxList.add(gAux);
            }
        }
        if(concessionsDataMap.get(dataBid.Freight__c) != null){
            for(Concessions__c c : concessionsDataMap.get(dataBid.Freight__c)){
                cAux = c.clone();
                cAux.Id = null;
                cAux.Production__c = dataBid.Production__c;
                cAux.Freight__c = fData.Id;
                cAuxList.add(cAux);
            }
        }
        
        if(subtripDataMap.get(dataBid.Freight__c) != null){
            for(Freight__c gs : subtripDataMap.get(dataBid.Freight__c)){
                gAux = gs.clone();
                gAux.Id = null;
                gAux.Freight_Trip_Details__c = null;
                gAux.RecordTypeId = freight_FreightSubStripDetailsRT;
                gAux.Production__c = dataBid.Production__c;
                gAux.Freight_Trip_Details__c = fData.Id;
                subtripInsertMap.put(cx,gAux);
                if(travelsBySubTripMapAux.get(gs.Id) != null){
                    for(Freight__c gs2 : travelsBySubTripMapAux.get(gs.Id)){
                        gAux = gs2.clone();
                        gAux.Id = null;
                        gAux.Freight_Trip_Details__c = null;
                        gAux.RecordTypeId = freight_FreightEquipmentDetailsRT;
                        gAux.Production__c = dataBid.Production__c;
                        
                        travelListAux = travelInsertMap.get(cx) != null ? travelInsertMap.get(cx) : new List<Freight__c>();
                        travelListAux.add(gAux);
                        travelInsertMap.put(cx,travelListAux.clone());
                    }
                }
                cx++;
            }
        }
        
        if(gAuxList.size() > 0) insert gAuxList;
        if(cAuxList.size() > 0) insert cAuxList;
        
        if(subtripInsertMap.size() > 0){
            insert subtripInsertMap.values();
            List<Freight__c> travelNewList = new List<Freight__c>();
            for(Integer ix : subtripInsertMap.keySet()){
                if(travelInsertMap.get(ix) != null){
                    for(Freight__c gms : travelInsertMap.get(ix)){
                        gms.Freight_Sub_Trip_Details__c = subtripInsertMap.get(ix).Id;
                        travelNewList.add(gms);
                    }
                }
            }
            if(travelNewList.size() > 0) insert travelNewList;
        }
    }
    public static String getNumberFormat(Integer num){
        String contractnumber = '';
        Integer count = 10 - String.valueOf(num).length();
        for(Integer i = 1; i <= count; i++){
            contractnumber = contractnumber + '0';
        }
        contractnumber = contractnumber + String.valueOf(num);
        return contractnumber;
    }
    public void editBidDataLocked(){
        if(bidid_locked != null && bidid_locked != ''){
            Bid__c b = new Bid__c(Id = bidid_locked,Locked__c = bidstatus_locked);
            update b;
        }
    }
    public void sendResendBid(){
        if(bidData != null && contactPrimarySelected != null){
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id =: contactPrimarySelected]) contactMap.put(c.Id,c);
            
            //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Freight Coordinator')];
            User userActual = FreightDashboardController.verifyEmailUser(UserInfo.getUserId(),opportunityid,bidData.Freight__c);
            
            Journal__c journalAux;
            Bid__c bAux;
            List<Journal__c> journalAuxList = new List<Journal__c>();
            Map<String,Bid__c> bidUpdateMap = new Map<String,Bid__c>();
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
        	Messaging.SingleEmailMessage mail;
            String[] toAddresses;
            Set<String> ccAddresses;
            String body = '';
            List<EmailTemplate> templateLink = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate WHERE DeveloperName ='Freight_Bid_Request_Link_All'];
            String subject = '';
            
            Freight__c fAux = new Freight__c(Id=bidData.Freight__c);
            
            //New Journals
            journalAux = new Journal__c(
                RecordTypeId = journal_bidjournalRT,
                Bid__c = bidData.Id,
                Journal_Entry__c = 'Freight Bid Request Link has been sent to ' + contactMap.get(contactPrimarySelected).Name + ' at ' + contactMap.get(contactPrimarySelected).Email
            );
            journalAuxList.add(journalAux);
            
            //Bid update
            bAux = new Bid__c(Id=bidData.Id,/*Status__c='Bid Request Stage',*/Vendor_Contact__c=contactPrimarySelected);
            bidUpdateMap.put(bAux.Id,bAux);
            
            //EMAIL
            ccAddresses = new Set<String>();
            if(bidData.Vendor__c != null){
                for(ContactWrapper cw : contactsByVendorBidMap.get(bidData.Vendor__c)){
                    if(!cw.disabled && cw.selected){
                        ccAddresses.add(cw.c.Email);
                    }
                }
            }
            if(bidData.Vendor__r.ParentId != null){
                for(ContactWrapper cw : contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId)){
                    if(!cw.disabled && cw.selected){
                        ccAddresses.add(cw.c.Email);
                    }
                }
            }
            
            mail = new Messaging.SingleEmailMessage();
            if(userActual != null && userActual.Email != null) mail.setOrgWideEmailAddressId(verifyWideAddress(userActual.Email));
            toAddresses = new String[] {contactMap.get(contactPrimarySelected).Email};
                mail.setToAddresses(toAddresses);
            if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
                        
            subject = (templateLink.size() > 0 ? templateLink[0].Subject.replace('{ProductionName}',bidData.Production__r.Name)
                       .replace('{StartDate}',(bidData.Freight__r.Start_Date__c != null ? Datetime.newInstance(bidData.Freight__r.Start_Date__c.year(),bidData.Freight__r.Start_Date__c.month(),bidData.Freight__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                       .replace('{EndDate}',(bidData.Freight__r.End_Date__c != null ? Datetime.newInstance(bidData.Freight__r.End_Date__c.year(),bidData.Freight__r.End_Date__c.month(),bidData.Freight__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                       .replace('{BidNumber}',bidData.Name)
                       : '');
            body = 'Dear ' + contactMap.get(contactPrimarySelected).Name + ',<br/><br/>' +  
                (templateLink.size() > 0 ? templateLink[0].HtmlValue.replace('{FreightCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
                 //.replace('{ContactName}',contactMap.get(contactPrimarySelected).Name) 
                 .replace('{VendorURL}','<a href="http://' + url + '/' + bidData.Vendor__c + '" target="_blank">' + bidData.Vendor__r.Name + '</a>')
                 //.replace('{BidURL}','<a href="' + (communityURLvalue != null ? communityURLvalue : '') + '/s/?service=freight&record=' + bidData.Id + '" target="_blank">' + (communityURLvalue != null ? communityURLvalue : '') + '/s/?service=freight&record=' + bidData.Id + '</a>')
                 .replace('{BidURL}','<a href="http://' + url + '/' + bidData.Id + '" target="_blank">http://' + url + '/' + bidData.Id + '</a>')
                 : '');
            fAux.Email_Body_Bid_Request_Link__c = null;
            mail.setSubject(subject);
            mail.setHtmlBody(body);
            myEmails.add(mail);


            insert journalAuxList;
            
            update bidUpdateMap.values();
            
            //fAux.Bid_Request__c = system.today();
           	update fAux;
            
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
        }
    }
    public void saveEditVehicleBid(){
        if(vehicleIdActual != null && vehicleIdActual != ''){
            newVehicleBid = new Freight__c(
                Id = vehicleIdActual,
                Equipment__c = vehicle_vehicleref,
                Vehicle_Type__c = vehicle_vehicletype,
                Capacity__c = vehicle_capacity,
                Make__c = vehicle_make,
                Model__c = vehicle_model,
                Year__c = vehicle_year,
                //Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null)
                Freight_Truck_Sq_Ft__c = vehicle_truck,
                Equipment_requested__c = vehicle_equipmentrequested
            );
            update newVehicleBid;
            getVehiclesByBid();
        }
    }
    public void addVehicleBid(){
		if(bidData != null && bidData.id != null){
            newVehicleBid.Id = null;
            newVehicleBid.RecordTypeId = freight_vehicletypeRT;
            newVehicleBid.Production__c = opportunityId;
            //newVehicleBid.Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null);
            //if(bidData.Status__c == 'Contracted') newVehicleBid.Bid__c = bidData.Id ; else newVehicleBid.Freight_Trip_Details__c = bidData.Freight__c;
            newVehicleBid.Bid__c = bidData.Id;
            newVehicleBid.Equipment__c = vehicle_vehicleref;
            newVehicleBid.Equipment_requested__c = vehicle_equipmentrequested;
            system.debug(newVehicleBid);
            insert newVehicleBid;
            getVehiclesByBid();
        }        
    }
    public void newVehicleBid(){
        newVehicleBid = new Freight__c();
    }
    public void deleteVehicleBid(){
        if(vehicleIdActual != null && vehicleIdActual != ''){
            delete [SELECT Id FROM Freight__c WHERE Id=:vehicleIdActual];
            getVehiclesByBid();
        }
    }
    public void getVehiclesByBid(){
        vehiclesByBidList = new List<Freight__c>();
        if(bidData != null && bidData.Id != null){
            //if(bidData.Status__c == 'Contracted'){
                vehiclesByBidList = [SELECT Id, Production__c, RecordTypeId, RecordType.Name, Equipment__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, Freight_Truck_Sq_Ft__c, Equipment_requested__c
                                     FROM Freight__c WHERE RecordType.Name = 'Vehicle Type' AND Production__c =: opportunityId 
                                     AND Bid__c =: bidData.Id AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_Details__c = NULL];
            /*}else{
                vehiclesByBidList = [SELECT Id, Production__c, RecordTypeId, RecordType.Name, Equipment__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c 
                                     FROM Freight__c WHERE RecordType.Name = 'Vehicle Type' AND Production__c =: opportunityId AND Freight_Trip_Details__c =: bidData.Freight__c
                                     AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_Details__c = NULL];
            }*/
        }
    }
    public void saveEquipmentBid(){
        Freight__c equipment = new Freight__c(
            Id = equipmentActualId != null && equipmentActualId != '' ? equipmentActualId : null,
            RecordTypeId = freight_FreightEquipmentDetailsRT,
            Line__c = newequipment_line != null && newequipment_line != '' ? Decimal.valueOf(newequipment_line) : null,
            Equipment__c = newequipment_vehicle,
            Start_Date__c = newequipment_startdate != null ? newequipment_startdate : null,
            Start_Date_Time__c = newequipment_starttime != null && newequipment_starttime != '' ? Time.newInstance(Integer.valueOf(newequipment_starttime.split(':')[0]),newequipment_starttime.split(':').size() > 0 ? Integer.valueOf(newequipment_starttime.split(':')[1]) : 0,0,0) : null,
            End_Date__c = newequipment_enddate != null ? newequipment_enddate : null,
            End_Date_Time__c = newequipment_endtime != null && newequipment_endtime != '' ? Time.newInstance(Integer.valueOf(newequipment_endtime.split(':')[0]),newequipment_endtime.split(':').size() > 0 ? Integer.valueOf(newequipment_endtime.split(':')[1]) : 0,0,0) : null,
            Travel_Type__c = newequipment_traveltype,
            Group_Type__c = newequipment_grouptype,
            Location_Type__c = newequipment_locationpickuptype,
            Location_Details__c = newequipment_locationpickupdetails,
            Location_Drop_Off_Type__c = newequipment_locationdropofftype,
            Location_Details_Drop_Off__c = newequipment_locationdropoffdetails,
            Airline_Info_Special_Notes__c = newequipment_notes,
            Freight_Trip_Contents__c = newtravel_tripcontents /*,
            Equipment_requested__c = newtravel_equipmentrequested*/
        );
        if(newequipment_subtripid != null && newequipment_subtripid != '') equipment.Freight_Sub_Trip_Details__c = newequipment_subtripid;
        if(equipmentActualId == null || equipmentActualId == '') equipment.Production__c = opportunityId;
        
        upsert equipment;

        if(newequipment_updatemaster){
            Freight__c freightAux = new Freight__c(Id = bidData.Freight__c);
            if(newequipment_startdate != null) freightAux.Start_Date__c = bidData.Freight__r.Start_Date__c != null ? (bidData.Freight__r.Start_Date__c <= newequipment_startdate ? bidData.Freight__r.Start_Date__c : newequipment_startdate) : newequipment_startdate;
            if(newequipment_enddate != null) freightAux.End_Date__c = bidData.Freight__r.End_Date__c != null ? (bidData.Freight__r.End_Date__c >= newequipment_enddate ? bidData.Freight__r.End_Date__c : newequipment_enddate) : newequipment_enddate;
            update freightAux;
        }
        getSubStripByBid();
    }
    public void deleteEquipmentBid(){
        if(String.isNotBlank(equipmentActualId)){
            delete [SELECT Id FROM Freight__c WHERE Id =: equipmentActualId];
            getSubStripByBid();
        }
    }
    public void saveSubTripBid(){
        if(subtripIdActual != null && subtripIdActual != ''){
            Freight__c freightAux;
            for(Freight__c freight : bidSubTrips){
                if(freight.Id == subtripIdActual){
                    freightAux = freight;
                    freightAux.Service_Type__c = bidData.Freight__r.Service_Type__c;
                    update freight;
                    break;
                }
            }
            Boolean enter = false;
            Integer i = 1;
            List<Freight__c> freightExistList = new List<Freight__c>();
			for(Freight__c freight : [SELECT Id, Trip_Order__c FROM Freight__c WHERE RecordType.Name = 'Freight Sub Trip Details' AND Bid_Sub_Trip__c =:bidData.Id ORDER BY Trip_Order__c ASC]){
                if(freight.Id != freightAux.Id){
                    if(i == freightAux.Trip_Order__c){
                        if(freight.Trip_Order__c >= freightAux.Trip_Order__c && (i - 1 != 0))
                            freight.Trip_Order__c = i - 1;
                        else
                            freight.Trip_Order__c = i + 1;
                        
                        freightExistList.add(freight);
                    }else{
                        freight.Trip_Order__c = i;
                        freightExistList.add(freight);
                    }
                }
                i++;
            }
            
            if(freightExistList.size() > 0) update freightExistList;
            getSubStripByBid();
        }
    }
    public void deleteSubTripBid(){
        system.debug(subtripIdActual);
        if(subtripIdActual != null && subtripIdActual != '' && bidData != null && bidData.Id != null){
            //delete [SELECT Id FROM Sub_Trip_GCQ__c WHERE GT_Sub_Trip_Details__c =: subtripIdActual];
            delete [SELECT Id FROM Freight__c WHERE RecordType.DeveloperName = 'Equipment_Details' AND Freight_Sub_Trip_Details__c =: subtripIdActual];
            delete [SELECT Id FROM Freight__c WHERE Id =: subtripIdActual];
            
            Integer cont = 1;
            List<Freight__c> freightExistList = new List<Freight__c>();
            for(Freight__c freight : [SELECT Id, Trip_Order__c FROM Freight__c WHERE RecordType.DeveloperName = 'Freight_Sub_Trip_Details' AND Bid__c =: bidData.Id ORDER BY Trip_Order__c ASC]){
                freight.Trip_Order__c = cont;
                freightExistList.add(freight);
                cont++;
            }
            
            if(freightExistList.size() > 0) update freightExistList;
            getSubStripByBid();
        }
    }
    public void newSubTripBid(){
        if(bidData != null && bidData.Id != null){
            List<Freight__c> freightExistList;
            //if(bidData.Status__c == 'Contracted') 
                freightExistList = [SELECT Id, Trip_Order__c FROM Freight__c WHERE RecordType.Name = 'Freight Sub Trip Details' AND Bid_Sub_Trip__c =: bidData.Id ORDER BY Trip_Order__c DESC LIMIT 1];
            /*else
                freightExistList = [SELECT Id, Trip_Order__c FROM Freight__c WHERE RecordType.Name = 'Freight Sub Trip Details' AND Freight_Trip_Details__c =: bidData.Freight__c ORDER BY Trip_Order__c DESC LIMIT 1];*/
            
            Freight__c new_subtrip = new Freight__c(
                Production__c = opportunityId,
                RecordTypeId = freight_FreightSubStripDetailsRT,
                Trip_Order__c = (freightExistList.size() > 0 ? (freightExistList[0].Trip_Order__c != null ? freightExistList[0].Trip_Order__c + 1 : 1) : 1),
                Description__c = 'Airport transfer'
            );
            //if(bidData.Status__c == 'Contracted') new_subtrip.Bid_Sub_Trip__c = bidData.Id ; else new_subtrip.Freight_Trip_Details__c = bidData.Freight__c;
            new_subtrip.Bid_Sub_Trip__c = bidData.Id;
            insert new_subtrip;
            
            getSubStripByBid();
        }
    }
    public void getSubStripByBid(){
        hasFreightMap = new Map<String,Boolean>();
        bidSubTrips = new List<Freight__c>();
        bidSubTripEquipmentsMap = new Map<Id, List<Freight__c>>();
        //if(bidData.Status__c == 'Contracted'){
        for(Freight__c subTrip:[Select id, Trip_Type__c, Trip_Order__c, Sub_Trip_Type__c, Description__c, Sub_Trip_Notes__c, Freight_Trip_Contents__c, 
                                (Select id, Line__c, Equipment__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c,
                                 Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c, Freight_Trip_Contents__c, Start_Date_Time_Text__c, End_Date_Time_Text__c, Location_Drop_Off_Type__c, Location_Details_Drop_Off__c,
                                 Equipment_requested__c from FreightEquipments__r order by Line__c) 
                                from Freight__c where Bid_Sub_Trip__c =:bidDataMap.get(tripBidNumber).b.Id and RecordType.DeveloperName = 'Freight_Sub_Trip_Details' order by Trip_Order__c, Line__c]){
                                    if(subTrip.FreightEquipments__r != null){
                                        for(Freight__c travel : subTrip.FreightEquipments__r){
                                            travel.Start_Date_Time_Text__c = travel.Start_Date__c != null && travel.Start_Date_Time__c != null ? Datetime.newInstance(travel.Start_Date__c, travel.Start_Date_Time__c).format('h:mm a') : '';
                                            travel.End_Date_Time_Text__c = travel.End_Date__c != null && travel.End_Date_Time__c != null ? Datetime.newInstance(travel.End_Date__c, travel.End_Date_Time__c).format('h:mm a') : '';
                                        }
                                    }
                                    bidSubTrips.add(subTrip);
                                    bidSubTripEquipmentsMap.put(subTrip.id, subTrip.FreightEquipments__r);
                                }
        /*}else{
            for(Freight__c subTrip:[Select id, Trip_Type__c, Trip_Order__c, Sub_Trip_Type__c, Description__c, Sub_Trip_Notes__c, (Select id, Line__c, Equipment__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c from FreightEquipments__r order by Line__c) 
                                   from Freight__c where Freight_Trip_Details__c =:bidDataMap.get(tripBidNumber).b.Freight__c and RecordType.DeveloperName = 'Freight_Sub_Trip_Details' order by Trip_Order__c, Line__c]){
                                       bidSubTrips.add(subTrip);
                                       //hasFreightMap.put(subtrip.Id,subtrip.GT_Freight__c != null ? true : false);
                                       bidSubTripEquipmentsMap.put(subTrip.id, subTrip.FreightEquipments__r);
                                   }
        }*/
    }
    public void saveEditConcessionBid(){
        if(concessionActual != null && concessionActual != ''){
            Concessions__c concessionBid = new Concessions__c(
                Id=concessionActual,
                Concession_Type__c = 'Freight',
                Concessions_Requested__c=concessionRequestedActual,
                Notes__c=concessionNoteActual,
                Included_Excluded__c = concessionIncludedActual,
            	Rate__c = (concessionRateActual != null && concessionRateActual != '' && concessionRateActual.trim() != '' ? concessionRateActual : null),
                Order__c = (concessionOrderActual != null && concessionOrderActual != '' ? Decimal.valueOf(concessionOrderActual) : null)
            );
            update concessionBid;
            Integer i = 1;
            Integer j;
            List<Concessions__c> concessionAuxList = new List<Concessions__c>();
            Map<Integer,Integer> mapAux = new Map<Integer,Integer>();
            for(Concessions__c c : [SELECT Id, Concessions_Requested__c, Concession_Type__c, Notes__c, Included_Excluded__c, Rate__c, Order__c FROM Concessions__c WHERE Production__c =: opportunityId AND Bid__c =:bidData.Id and Concession_Type__c = 'Freight' ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC]){
                if(c.Order__c != null){
                    if(c.Id != concessionBid.Id){
                        if(concessionOrderActual != null && concessionOrderActual != '' && i == Integer.valueOf(concessionOrderActual)){
                            j = i - 1;
                            if(j != 0 && mapAux.get(j) == null){
                                c.Order__c = j ;
                                mapAux.put(j,j);
                            }else{
                                c.Order__c = i + 1;
                                mapAux.put(i,i);
                            }
                            concessionAuxList.add(c);
                        }else{
                            c.Order__c = i;
                            concessionAuxList.add(c);
                        }
                    }
                    i++;
                }
            }
            if(!concessionAuxList.isEmpty()) update concessionAuxList;
            getConcessionsByBid();      
        }
    }
    public void deleteConcessionBid(){
        delete [SELECT Id FROM Concessions__c WHERE Id=:concessionActual];
        getConcessionsByBid();
    }
    public void addConcessionBid(){
        if(bidData != null && bidData.Id != null){
            Concessions__c newConcessionBid = new Concessions__c();
            newConcessionBid.Concession_Type__c = 'Freight';
            newConcessionBid.Production__c = opportunityId;
            newConcessionBid.Concessions_Requested__c = concessionRequestedActual;
            newConcessionBid.Notes__c = concessionNoteActual;
            newConcessionBid.Included_Excluded__c = concessionIncludedActual;
            newConcessionBid.Rate__c = (concessionRateActual != null && concessionRateActual != '' && concessionRateActual.trim() != '' ? concessionRateActual : null);
            newConcessionBid.Bid__c = bidData.Id;
            newConcessionBid.Order__c = (concessionOrderActual != null && concessionOrderActual != '' ? Decimal.valueOf(concessionOrderActual) : null);
            insert newConcessionBid;
            
            if(concessionOrderActual != null && concessionOrderActual != ''){
                Integer i = 1;
                Integer j;
                List<Concessions__c> concessionAuxList = new List<Concessions__c>();
                Map<Integer,Integer> mapAux = new Map<Integer,Integer>();
                for(Concessions__c c : [SELECT Id, Concessions_Requested__c, Concession_Type__c, Notes__c, Included_Excluded__c, Rate__c, Order__c FROM Concessions__c WHERE Production__c =: opportunityId AND Bid__c =:bidData.Id and Concession_Type__c = 'Freight' ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC]){
                    if(c.Order__c != null){
                        if(c.Id != newConcessionBid.Id){
                            if(concessionOrderActual != null && concessionOrderActual != '' && i == Integer.valueOf(concessionOrderActual)){
                                j = i - 1;
                                if(j != 0 && mapAux.get(j) == null){
                                    c.Order__c = j ;
                                    mapAux.put(j,j);
                                }else{
                                    c.Order__c = i + 1;
                                    mapAux.put(i,i);
                                }
                                concessionAuxList.add(c);
                            }else{
                                c.Order__c = i;
                                concessionAuxList.add(c);
                            }
                        }
                        i++;
                    }
                }
                if(!concessionAuxList.isEmpty()) update concessionAuxList;
            }
            getConcessionsByBid();
        }
    }
    public void getConcessionsByBid(){
    	concessionsRequestedBid = new List<Concessions__c>();
        if(bidData != null && bidData.Id != null){
                concessionsRequestedBid = [SELECT Id, Concessions_Requested__c, Concession_Type__c, Notes__c, Included_Excluded__c, Rate__c, Order__c
                                           FROM Concessions__c 
                                           WHERE Production__c =: opportunityId AND Bid__c =:bidData.Id and Concession_Type__c = 'Freight' ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC];
        }
    }
    public void searchBidHistory(){
        String vendor = bidData.Vendor__c;
        bidRelatedVendorList = new List<BidVendorWrapper>();
        String query = 'SELECT Id, Name, Production__c, Production__r.Name, Freight__c, Freight__r.Start_Date__c, Freight__r.End_Date__c, Freight__r.Description__c,' +
            ' Status__c, No_Bid_reason__c, Venue__c, Venue__r.Name, Vendor__r.ParentId, Vendor__r.Parent.Name, CreatedDate' +
            ' FROM Bid__c WHERE Vendor__c =: vendor';
        
        //if(bidhistorysearch_onlyirstays != null) query += ' AND Freight__r.RecordType.Name = \'Individual Reservation\'';
        if(bidhistorysearch_market != null && bidhistorysearch_market.trim() != '') query += ' AND Production__r.Market_Type__c = \'' + bidhistorysearch_market +'\'';
        if(bidhistorysearch_from != null && String.valueOf(bidhistorysearch_from).trim() != '') query += ' AND Freight__r.Start_Date__c >=: bidhistorysearch_from';
        if(bidhistorysearch_to != null && String.valueOf(bidhistorysearch_to).trim() != '') query += ' AND Freight__r.End_Date__c <=: bidhistorysearch_to';
        
        if(orderBidHistoryOrientation == null) orderBidHistoryOrientation = 'ASC';
        system.debug(orderBidHistoryOrientation);
        if(orderCheckBidHistory){
            if(orderChangeBidHistory){
                orderBidHistoryOrientation = 'ASC';
            }else{
                if(orderBidHistoryOrientation == 'ASC') orderBidHistoryOrientation = 'DESC'; else orderBidHistoryOrientation = 'ASC';
            }
        }
        for(Bid__c b : Database.query(query)){
            bidRelatedVendorList.add(new BidVendorWrapper(b,b.Name,b.Production__r.Name,b.Freight__r.Start_Date__c,b.Freight__r.End_Date__c,b.Freight__r.Description__c,null,b.Status__c,b.No_Bid_reason__c,b.Venue__r.Name,b.Vendor__r.Parent.Name,b.CreatedDate.date()));
        }
        bidRelatedVendorList.sort();
    }
    public void openBidHistory(){
        bidRelatedVendorList = new List<BidVendorWrapper>();
        Set<String> bidIdsAux = new Set<String>();
        for(Bid__c b : [SELECT Id, Name, Production__c, Production__r.Name, Freight__c, Freight__r.Start_Date__c, Freight__r.End_Date__c, Freight__r.Description__c,
                        Status__c, No_Bid_reason__c, Venue__c, Venue__r.Name, Vendor__r.ParentId, Vendor__r.Parent.Name, CreatedDate
                        FROM Bid__c WHERE Vendor__c =: bidData.Vendor__c AND RecordType.DeveloperName = 'Freight_Bid' ORDER BY CreatedDate DESC]){
                            bidIdsAux.add(b.Id);
                            bidRelatedVendorList.add(new BidVendorWrapper(b,b.Name,b.Production__r.Name,b.Freight__r.Start_Date__c,b.Freight__r.End_Date__c,b.Freight__r.Description__c,null,b.Status__c,b.No_Bid_reason__c,b.Venue__r.Name,b.Vendor__r.Parent.Name,b.CreatedDate.date()));
                        }
        rateBidMap = new Map<String,Revenue__c>();
        for(Revenue__c r : [Select id, Base_Cost__c, Commission__c, Rate__c, Gratuity__c, Total_Price__c, CurrencyIsoCode, Bid__c from Revenue__c where Bid__c IN: bidIdsAux and RecordType.DeveloperName = 'Freight_Rate_Commission' order by createdDate ASC]) rateBidMap.put(r.Bid__c,r);
        for(String bididaux : bidIdsAux){
            if(rateBidMap.get(bididaux) == null) rateBidMap.put(bididaux, new Revenue__c());
        }
        for(BidVendorWrapper bw : bidRelatedVendorList){
            bw.rate = 0;
        }
    }
    public void getBidInformation(){
        tripHaveContracted = false;
        system.debug(tripBidNumber);
        system.debug(bidDataMap);
        if(tripBidNumber != null && bidDataMap.get(tripBidNumber) != null){
            bidData = [Select Id, RecordTypeId, RecordType.Name, Name, Production__c, Production__r.Name, Production__r.Production_ID__c, Production__r.Account.Name, Production__r.Account.Physical_Address__c, Production__r.Office_Location__c, Freight__c, Freight__r.Name, Freight__r.Start_Date__c, Freight__r.End_Date__c, Freight__r.Status__c, Freight__r.Freight_Preferences__c, Vendor__c, Vendor__r.Vendor_ID__c, Vendor__r.Phone, 
                       Vendor__r.ParentId, Vendor__r.Name, Vendor__r.City__r.Name, Vendor__r.ShippingCountry, Vendor_Address__c, Vendor_Contact__c, Vendor_Contact__r.Name, Vendor_Contact_Email__c, Vendor_Contact_Phone__c, Locked__c, Status__c, Status_Previous__c, Internal_notes__c, DX_to_Venue__c, Venue__c, Venue__r.Name, 
                       Include_in_options__c, Options__c, Include_in_option_cover_sheet__c, No_Bid_reason__c, Trips_Details_Update_Contact_Id__c, Trip_Details_Update_Terms__c, Trip_Details_Update_Payment_Policy__c, Trip_Details_Update_Cancel_Policy__c, Trip_Details_Update_Last_Send_By__c, Trip_Details_Update_Last_Send_Date__c, Rate_Agreement_Contact_Id__c, Rate_Agreement_Production_Contact_Id__c, 
                       Rate_Agreement_Terms__c, Rate_Agreement_Payment_Policy__c, Rate_Agreement_Cancellation_Policy__c, Rate_Agreement_Last_Send_By__c, Rate_Agreement_Last_Send_Date__c, Transportation_Contract_Contact_Id__c, Transportation_Contract_Terms__c, Transportation_Contract_Payment_Policy__c, Transportation_Contract_Cancel_Policy__c, Transportation_Contract_Last_Send_By__c, 
                       Transportation_Contract_Last_Send_Date__c, Billing_Options__c, Show_Include_Rate__c, Freight__r.Service_Type__c, Form_Rate_Agreement__c, Form_Transportation_Contract__c, Form_Trip_Details_Update__c 
                       From Bid__c Where Id =:bidDataMap.get(tripBidNumber).b.Id];
            getContactsByVendorBid();
            getSubStripByBid();
            getVehiclesByBid();
            getConcessionsByBid();
            getBidRevenue();
            
            if(vfpConfiguration != null){
                vfpConfiguration.bidId = bidData.Id;
                vfpConfiguration.parentId = bidData.Freight__c;
                vfpConfiguration.productionId = opportunityId;
                vfpConfiguration.parentSObject = 'Freight';
            }
            
            for(Integer bk : bidDataMap.keySet()){
                if(bidDataMap.get(bk).b.Id != bidData.Id && bidDataMap.get(bk).b.Status__c == 'Contracted') tripHaveContracted = true;
            }
            
            freight_triptypePL = new List<SelectOption>();
            freight_triptypePL.add(new SelectOption('',''));
            Map<Object,List<String>> dependValuesByControlValue = FreightDashboardController.getDependentPicklistValues(Freight__c.Trip_Type__c);
            for(Object k1 : dependValuesByControlValue.keySet()){
                if((String) k1 == bidData.Freight__r.Service_Type__c){
                    for(String k2: dependValuesByControlValue.get(k1)){
                        freight_triptypePL.add(new SelectOption(k2,k2));
                    }
                }
            }
            
            /**
            *  @Conga: Update for Conga.
            */
            User emailFromUser = FreightDashboardController.verifyEmailUser(UserInfo.getUserId(),opportunityid,bidData.Freight__c);
            resendBidAgreement_emailFromUserId = emailFromUser.Id;
            resendBidAgreement_congaEmailFromId = verifyWideAddress(emailFromUser.Email);
            congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
            for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('Freight - BidsWithOptionsByBidId', 'Freight - SubTripsByBidId', 'Freight - BidById', 'Freight - ContactById', 'Freight - ProductionAssociationsByOppId', 'Freight - UserById')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
            previewBidOptions_congaQueriesJson = resendBidAgreement_congaQueriesJson = JSON.serialize(congaQueriesMap);
            Map<String, APXTConga4__Conga_Template__c> congaTemplatesMap = new Map<String, APXTConga4__Conga_Template__c>();
            for(APXTConga4__Conga_Template__c congaTemplate:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c in ('Freight - Bid', 'Freight - Options')]) congaTemplatesMap.put(congaTemplate.APXTConga4__Name__c, congaTemplate);
            previewBidOptions_congaTemplateId = congaTemplatesMap.get('Freight - Options') != null ? congaTemplatesMap.get('Freight - Options').id : null;
            resendBidAgreement_congaTemplateId = congaTemplatesMap.get('Freight - Bid') != null ? congaTemplatesMap.get('Freight - Bid').id : null;
            /**
            *  @/Conga
            */
            isBidAgreementRendered = isResendBidRendered = isBidJournalsRendered = isReleaseBidRendered = false;
            
            coordinatorGT = null;
            for(Production_Associations__c pa : [SELECT Id, Production_Opp__c, User__c, Team_Roles__c, User__r.Name, Role__c FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId]){
                if(pa.User__c != null && pa.Team_Roles__c != null){
                    if(pa.Team_Roles__c.contains('Primary Freight Coordinator')) coordinatorGT = pa.User__c; 
                }
            }
        }
    }
    public void getContactsByVendorBid(){
        if(bidData != null){
            Map<String,Contact> contactMap = new Map<String,Contact>();
            bidPrimaryContact = String.isNotEmpty(bidData.Vendor_Contact__c) ? [Select Id, FirstName, Name, Phone, Email From Contact Where Id =:bidData.Vendor_Contact__c LIMIT 1] : new Contact();
            for(Contact contact : [Select Id, Name, Email from Contact where AccountId =:bidData.Vendor__c]) contactMap.put(contact.Id,contact);
            if(bidData.Vendor__r.ParentId != null) for(Contact contact : [Select Id, Name, Email from Contact where AccountId =:bidData.Vendor__r.ParentId]) contactMap.put(contact.Id,contact);
            contactsBidsByVendor = new List<SelectOption>();
            contactsBidsByVendor.add(new SelectOption('',''));
            for(Contact contact : contactMap.values()) contactsBidsByVendor.add(new SelectOption(contact.Id,contact.Name));
        }
    }
    public void changeContactPrimaryBid(){
        bidPrimaryContact = String.isNotEmpty(bidData.Vendor_Contact__c) ? [Select Id, FirstName, Name, Phone, Email from Contact where Id =:bidData.Vendor_Contact__c limit 1] : new Contact();
    }
    public void changeContactPrimary(){
        bidPrimaryContact = String.isNotEmpty(draft.Primary_Contact_Id__c) ? [Select Id, FirstName, Name, Phone, Email from Contact where Id =:draft.Primary_Contact_Id__c limit 1] : new Contact();
    }
    public void save(){
        if(bidData != null && bidData.Id != null){
            System.debug('bidData: ' + bidData);
            upsert bidRevenue;
            bidData.Commission_Revenue__c = bidRevenue.Id;
            update bidData;
        }
    }
    public void soldOutBidStatus(){
        if(bidData != null && bidData.Id != null){
            bidData.Status__c = 'Sold Out / Not Bidding';
            update bidData;
            getBidInformation();
        }
    }
    public static String verifyWideAddress(String email){
       String oweaId;
       List<OrgWideEmailAddress> oweaList;
       if(Test.isRunningTest()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; else oweaList = [select Id from OrgWideEmailAddress where Address =: email];
       if(oweaList.isEmpty()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; //Email default
       oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
       return oweaId;
   }
    @RemoteAction
    global static List<String> getFreightAmenities(String freightid){
        List<String> dataList = new List<String>();
        Freight__c freight = [SELECT Id, Production__c, RecordTypeId, RecordType.Name, Equipment__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c FROM Freight__c WHERE Id =:freightid];
        if(freight.Amenities__c != null) for(String s : freight.Amenities__c.split(';')) dataList.add(s);
        return dataList;
    }
    @RemoteAction
    global static String searchVehicleTrip(String query, String bidid){
        query = '%' + query + '%';
        List<wrapperData> vehicleList = new List<wrapperData>();
        String description;
        Bid__c b = [SELECT Id, Status__c, Freight__c FROM Bid__c WHERE Id =: bidid];
        List<Freight__c> searchList;
        if(b.Status__c == 'Contracted')
            searchList = [SELECT Id, Equipment__c FROM Freight__c 
                           WHERE Equipment__c LIKE: query AND Bid__c =: bidid AND RecordType.Name = 'Vehicle Type' AND Freight_Trip_Details__c = NULL 
                           AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_Details__c = NULL];
        else
            searchList = [SELECT Id, Equipment__c FROM Freight__c 
                           WHERE Equipment__c LIKE: query AND Bid__c = NULL AND RecordType.Name = 'Vehicle Type' AND Freight_Trip_Details__c =: b.Freight__c 
                           AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_Details__c = NULL];
            
        for(Freight__c g : searchList) vehicleList.add(new wrapperData(g.Equipment__c,g.Equipment__c,''));
        return JSON.serialize(vehicleList);
    }
    ///BidAgreement Methods
    public void openBidAgreement(){
        Bid__c bid = [Select id, Vendor__c, Vendor_Contact__c, Vendor__r.Payment_policy__c, Vendor__r.Cancellation_Policy__c, Form_Rate_Agreement__c, Form_Trip_Details_Update__c, Form_Transportation_Contract__c, Rate_Agreement_Last_Send_Date__c, Rate_Agreement_Last_Send_By__c, Trip_Details_Update_Last_Send_Date__c, Trip_Details_Update_Last_Send_By__c, Transportation_Contract_Last_Send_Date__c, Transportation_Contract_Last_Send_By__c from Bid__c where id =:bidData.Id];
        List<Revenue__c> bidRevenues = [Select id, VAT_Rate__c, Gratuity__c, Total_Price__c from Revenue__c where Bid__c =:bidDataMap.get(tripBidNumber).b.Id and RecordType.DeveloperName = 'Freight_Rate_Commission' order by createdDate desc limit 1];
        bidAgreementRevenue = !bidRevenues.isEmpty() ? bidRevenues[0] : new Revenue__c();
        if((bidAgreement_type == 'Rate Agreement' && String.isNotBlank(bid.Form_Rate_Agreement__c)) || (bidAgreement_type == 'Trip Details Update' && String.isNotBlank(bid.Form_Trip_Details_Update__c)) || (bidAgreement_type == 'Transportation Contract' && String.isNotBlank(bid.Form_Transportation_Contract__c))) draft = [SELECT Id, Name, Salutation__c, Attention__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate, Payment_Policy__c, Cancellation_Policy__c FROM Draft__c WHERE Name =:(bidAgreement_type == 'Rate Agreement' ? bid.Form_Rate_Agreement__c : bidAgreement_type == 'Trip Details Update' ? bid.Form_Trip_Details_Update__c : bidAgreement_type == 'Transportation Contract' ? bid.Form_Transportation_Contract__c : '')];            
        else{
            draft = new Draft__c();
            draft.Salutation__c = 'Hi ,';
            draft.Attention__c = draft.Primary_Contact_Id__c = bid.Vendor_Contact__c;
            draft.Date__c = Date.today();
            draft.Subject__c = (String.isNotBlank(bidAgreement_type) ? bidAgreement_type + ' - ' : '') + bidData.Production__r.Name + ' - ' + (bidData.Freight__r.Start_Date__c != null ? Datetime.newInstance(bidData.Freight__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' - ' + (bidData.Freight__r.End_Date__c != null ? Datetime.newInstance(bidData.Freight__r.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' (' + bidData.Freight__r.Name + ')';
            draft.Body__c = (bidAgreement_type == 'Rate Agreement' ? 'Congratulations! You have been selected for the upcoming trip for ' + bidData.Production__r.Name + '.<br/><br/>Attached is the rate agreement for the group. Please sign and return at your earliest opportunity. <br/><br/>Looking forward to working with you for this production’s trip!. <br/><br/><br/>Thanks' : bidAgreement_type == 'Trip Details Update' ? 'Attached you will find updated Trip Details for ' + bidData.Production__r.Name + '.<br/><br/>Please reply to this email to confirm you have updated these changes or sign and scan the form back to me at your earliest opportunity. If you have any questions, please contact us immediately.<br/><br/><br/>Thanks' : bidAgreement_type == 'Transportation Contract' ? 'Congratulations! You have been selected for the upcoming trip for ' + bidData.Production__r.Name + '.<br/><br/>You will receive a separate email soon from Conga Sign which is the contract for the group. Please sign and submit today so we can forward to the client. If you absolutely need to use your company contract, then please include all items in the attached contract into your own contract. ‘Road Rebel’ and their employees should not appear on your agreement.<br/><br/>Please sign and submit only one contract to me as soon as possible. Looking forward to working with you for this production’s trip!<br/><br/><br/>Thanks,' : '');
            draft.Terms__c = bidAgreement_type == 'Rate Agreement' ? bidData.Rate_Agreement_Terms__c : bidAgreement_type == 'Trip Details Update' ? bidData.Trip_Details_Update_Terms__c : bidAgreement_type == 'Transportation Contract' ? '<ul><li>Driver(s) must assist with luggage.</li><li>Driver(s) will be on time, drive safely and only use cell phones in emergencies.</li><li>Driver(s) name and cell will be provided prior to travel.</li><li>Driver(s) are responsible for having directions to destination.</li><li>Bus company will not sub-contract coaches.</li><li>Any mechanical failure, or driver/dispatch negligence can cause major issues for their itinerary. This includes being lost or stopping unnecessarily. Bus company will make all efforts to fix any mechanical issues immediately. All drivers should be aware that any requests from Tour Management should be adhered to. Weather or roadway conditions, infringement on D.O.T regulations or the intervention of any governmental body are of exception. Road Rebel should be contacted immediately should any of the events listed occur.</li></ul>' : '';
            draft.Payment_Policy__c = String.isNotEmpty(bid.Vendor__c) ? bid.Vendor__r.Payment_policy__c : null;
            draft.Cancellation_Policy__c = String.isNotEmpty(bid.Vendor__c) ? bid.Vendor__r.Cancellation_Policy__c : null;
            insert draft;
            draft = [SELECT Id, Salutation__c, Name, Attention__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate, Payment_Policy__c, Cancellation_Policy__c FROM Draft__c WHERE Id = :draft.Id];
            if(bidAgreement_type == 'Rate Agreement') bid.Form_Rate_Agreement__c = bidData.Form_Rate_Agreement__c = draft.Name; 
            else if(bidAgreement_type == 'Trip Details Update') bid.Form_Trip_Details_Update__c = bidData.Form_Trip_Details_Update__c = draft.Name;
            else if(bidAgreement_type == 'Transportation Contract') bid.Form_Transportation_Contract__c = bidData.Form_Transportation_Contract__c = draft.Name; 
            update bid;
        }
        bidAgreementSubTrips = [Select id, Trip_Order__c, Trip_Type__c, Sub_Trip_Type__c, Description__c, Sub_Trip_Notes__c, (Select id, Line__c, Equipment__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Pick_up__c, Location_Type__c, Location_Details__c, Location_Drop_off__c, Location_Drop_Off_Type__c, Location_Details_Drop_Off__c, Airline_Info_Special_Notes__c from FreightEquipments__r order by Line__c) 
                                from Freight__c where Bid_Sub_Trip__c =:bidData.Id and RecordType.DeveloperName = 'Freight_Sub_Trip_Details' order by Trip_Order__c, Line__c];
        bidAgreementVehicles = [Select Id, Production__c, RecordTypeId, RecordType.Name, Equipment__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Freight_Truck_Sq_Ft__c, Amenities__c, Other_Amenities__c, Equipment_requested__c 
                                from Freight__c WHERE RecordType.Name = 'Vehicle Type' AND Production__c =: opportunityId AND Bid__c =: bidData.Id AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_Details__c = NULL];
        bidAgreementConcessions = [Select id, Concessions_Requested__c, Concession_Provided__c, Concession_Type__c, Notes__c, Included_Excluded__c, Rate__c from Concessions__c where Bid__c =:bidData.Id and Concession_Type__c = 'Freight'];
        if(bidAgreement_type != 'Trip Details Update') changeBidAgreementContactPrimary();
        else changeBidAgreementAttentionContact();
        bidAgreement_message = draft.Body__c;
        bidAgreement_terms = draft.Terms__c;
        bidData.Rate_Agreement_Last_Send_By__c = bid.Rate_Agreement_Last_Send_By__c;
        bidData.Rate_Agreement_Last_Send_Date__c = bid.Rate_Agreement_Last_Send_Date__c;
        bidData.Trip_Details_Update_Last_Send_By__c = bid.Trip_Details_Update_Last_Send_By__c;
        bidData.Trip_Details_Update_Last_Send_Date__c = bid.Trip_Details_Update_Last_Send_Date__c;
        bidData.Transportation_Contract_Last_Send_By__c = bid.Transportation_Contract_Last_Send_By__c;
        bidData.Transportation_Contract_Last_Send_Date__c = bid.Transportation_Contract_Last_Send_Date__c;
        /**
        *  @Conga
        */
        User emailFromUser = FreightDashboardController.verifyEmailUser(UserInfo.getUserId(), opportunityid, bidData.Freight__c);
        bidAgreement_congaEmailFromId = verifyWideAddress(emailFromUser.Email);
        congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
        for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('Freight - BidById', 'Freight - SubTripsByBidId', 'Freight - ContactById', 'Freight - ClientContactById', 'Freight - ProductionAssociationsByOppId', 'Freight - UserById')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
        congaQueriesJson = JSON.serialize(congaQueriesMap);
        Map<String, APXTConga4__Conga_Template__c> congaTemplatesMap = new Map<String, APXTConga4__Conga_Template__c>();
        for(APXTConga4__Conga_Template__c congaTemplate:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c in (:('Freight - ' + bidAgreement_type), :('Freight - ' + bidAgreement_type + ' Sign'))]) congaTemplatesMap.put(congaTemplate.APXTConga4__Name__c, congaTemplate);
        bidAgreement_congaTemplateId = congaTemplatesMap.get('Freight - ' + bidAgreement_type) != null ? congaTemplatesMap.get('Freight - ' + bidAgreement_type).id : null;
        bidAgreement_congaSignTemplateId = congaTemplatesMap.get('Freight - ' + bidAgreement_type + ' Sign') != null ? congaTemplatesMap.get('Freight - ' + bidAgreement_type + ' Sign').id : null;
        List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c =:('Freight - ' + bidAgreement_type)];
        bidAgreement_congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        /**
        *  @/Conga
        */
        isBidAgreementRendered = true;
    }
    public void changeBidAgreementContactPrimary(){
        List<Contact> bidAgreementContacts = [Select Id, FirstName, Name, Phone, Email from Contact where Id =:draft.Primary_Contact_Id__c limit 1];
        bidAgreementPrimaryContact = !bidAgreementContacts.isEmpty() ? bidAgreementContacts[0] : new Contact();
        draft.Salutation__c = 'Hi ' + (!bidAgreementContacts.isEmpty() ? bidAgreementContacts[0].FirstName : '') + ',';
    }
    public void changeBidAgreementAttentionContact(){
        List<Contact> bidAgreementContacts = [Select Id, FirstName, Name, Title, Phone, Email from Contact where Id =:draft.Attention__c limit 1];
        bidAgreementAttentionContact = !bidAgreementContacts.isEmpty() ? bidAgreementContacts[0] : new Contact();
        draft.Salutation__c = 'Hi ' + (!bidAgreementContacts.isEmpty() ? bidAgreementContacts[0].FirstName : '') + ',';
    }
    public List<SelectOption> getBidAgreementProductionAssociationContacts(){
        List<SelectOption> options = new List<SelectOption>();
        for(Production_Associations__c productAssoc:[Select Id, Contact__c, Contact__r.Name From Production_Associations__c Where Production_Opp__c =:opportunityId AND Contact__c != NULL AND RecordType.Name = 'Production Contacts' and Role__c includes ('Primary Freight', 'CC: Freight', 'Contract Signer')]) options.add(new SelectOption(productAssoc.Contact__c, productAssoc.Contact__r.Name));
        return options;
    }
    public void saveBidAgreement(){
        if(bidData != null && bidData.Id != null){
            try{
                if(bidAgreement_type == 'Rate Agreement'){
                    draft.Body__c = bidAgreement_message;
                    bidData.Rate_Agreement_Terms__c = draft.Terms__c = bidAgreement_terms;
                    bidData.Rate_Agreement_Payment_Policy__c = draft.Payment_Policy__c;
                    bidData.Rate_Agreement_Cancellation_Policy__c = draft.Cancellation_Policy__c;
                }
                else if(bidAgreement_type == 'Trip Details Update'){
                    draft.Body__c = bidAgreement_message;
                    bidData.Trip_Details_Update_Terms__c = draft.Terms__c = bidAgreement_terms;    
                    bidData.Trip_Details_Update_Payment_Policy__c = draft.Payment_Policy__c;
                    bidData.Trip_Details_Update_Cancel_Policy__c = draft.Cancellation_Policy__c;
                }
                else if(bidAgreement_type == 'Transportation Contract'){
                    draft.Body__c = bidAgreement_message;
                    bidData.Transportation_Contract_Terms__c = draft.Terms__c= bidAgreement_terms;  
                    bidData.Transportation_Contract_Payment_Policy__c = draft.Payment_Policy__c;
                    bidData.Transportation_Contract_Cancel_Policy__c = draft.Cancellation_Policy__c;
                } 
                update draft;
                draft = [SELECT Id, Name, Salutation__c, Attention__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate, Payment_Policy__c, Cancellation_Policy__c FROM Draft__c WHERE Id = :draft.Id];
                update bidData;
                /**
                *  @Conga: Update for Conga.
                */
                User emailFromUser = FreightDashboardController.verifyEmailUser(UserInfo.getUserId(), opportunityid, bidData.Freight__c);
                String emailBody = (String.isNotBlank(draft.Salutation__c) ? draft.Salutation__c + '<br/><br/>' : '') + (String.isNotBlank(draft.Body__c) ? draft.Body__c.removeStartIgnoreCase('<p>').removeEndIgnoreCase('</p>') : '') + (String.isNotBlank(emailFromUser.Name) ? '<br/>' + emailFromUser.Name : '') + '<br/>Freight Coordinator';
                if(isCongaSignSent){
                    emailResult = sendEmail(bidAgreement_to, bidAgreement_cc, bidAgreement_bcc, draft.Subject__c, emailBody, null, opportunityId, bidData.Freight__c); 
                    isCongaSignSent = false;
                }
                else if(String.isNotBlank(bidAgreement_congaEmailTemplateId)) update new APXTConga4__Conga_Email_Template__c(id = bidAgreement_congaEmailTemplateId, APXTConga4__HTMLBody__c = emailBody);
            }catch(Exception e){
                system.debug(e.getMessage());
            }
        }
    }
    public void deactivateBidAgreement(){
        if(bidData != null && bidData.Id != null){
            try{
                delete draft;
                bidData.put(bidAgreement_type == 'Rate Agreement' ? 'Form_Rate_Agreement__c' : bidAgreement_type == 'Trip Details Update' ? 'Form_Trip_Details_Update__c' : bidAgreement_type == 'Transportation Contract' ? 'Form_Transportation_Contract__c' : '', null);
                bidData.put(bidAgreement_type == 'Rate Agreement' ? 'Rate_Agreement_Last_Send_Date__c' : bidAgreement_type == 'Trip Details Update' ? 'Trip_Details_Update_Last_Send_Date__c' : bidAgreement_type == 'Transportation Contract' ? 'Transportation_Contract_Last_Send_Date__c' : '', null);
                bidData.put(bidAgreement_type == 'Rate Agreement' ? 'Rate_Agreement_Last_Send_By__c' : bidAgreement_type == 'Trip Details Update' ? 'Trip_Details_Update_Last_Send_By__c' : bidAgreement_type == 'Transportation Contract' ? 'Transportation_Contract_Last_Send_By__c' : '', null);
                update bidData;
            }
            catch(Exception e){
                system.debug(e.getMessage());
            }
        }
    }
    @RemoteAction
    public static String searchContactEmail(String query){
        query = '%' + query + '%';
        List<wrapperData> Contacts = new List<wrapperData>();
        for(Contact contact : [Select Id, Name, Email FROM Contact Where (Name like:query or Email like:query) and email != null limit 20]) Contacts.add(new wrapperData(contact.Id, contact.Name + ', ' + contact.Email, contact.Email));
        return JSON.serialize(Contacts);
    }
    //End BidAgreement Methods
    ///ResendBidAgreement Methods
    public void openResendBid(){
        vendorContact = new Contact();
        contactSelectOptionBidMap = new Map<String,List<SelectOption>>();
        contactsByVendorBidMap = new Map<String,List<ContactWrapper>>();
        contactsByVendorParentBidMap = new Map<String,List<ContactWrapper>>();
        List<ContactWrapper> contactAuxList;
        List<SelectOption> contactAuxSelectOptions;
        if(bidData.Vendor__r.ParentId != null){
            for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId =: bidData.Vendor__r.ParentId AND Email <> NULL ORDER BY Order__c ASC]){
                contactAuxList = contactsByVendorParentBidMap.get(c.AccountId) != null ? contactsByVendorParentBidMap.get(c.AccountId) : new List<ContactWrapper>();
                contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),false));
                contactsByVendorParentBidMap.put(c.AccountId,contactAuxList.clone());
            }
        }
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId =: bidData.Vendor__c AND Email <> NULL AND Order__c <> NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendorBidMap.get(c.AccountId) != null ? contactsByVendorBidMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(bidData.Vendor_Contact__c == c.Id ? true : (c.Order__c == 1 ? true : false)),(bidData.Vendor_Contact__c == c.Id ? true : (bidData.Vendor_Contact__c == null && c.Order__c == 1 ? true : false))));
            contactsByVendorBidMap.put(c.AccountId,contactAuxList.clone());
        }
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId =: bidData.Vendor__c AND Email <> NULL AND Order__c = NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendorBidMap.get(c.AccountId) != null ? contactsByVendorBidMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),(c.Order__c == 1 ? true : false)));
            contactsByVendorBidMap.put(c.AccountId,contactAuxList.clone());
        }
        if(contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId) != null){
            for(ContactWrapper cw : contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId)){
                contactAuxSelectOptions = contactSelectOptionBidMap.get(bidData.Vendor__c) != null ? contactSelectOptionBidMap.get(bidData.Vendor__c) : new List<SelectOption>();
                contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                contactSelectOptionBidMap.put(bidData.Vendor__c,contactAuxSelectOptions.clone());
            }
        }
        if(contactsByVendorBidMap.get(bidData.Vendor__c) != null){
            for(ContactWrapper cw : contactsByVendorBidMap.get(bidData.Vendor__c)){
                contactAuxSelectOptions = contactSelectOptionBidMap.get(bidData.Vendor__c) != null ? contactSelectOptionBidMap.get(bidData.Vendor__c) : new List<SelectOption>();
                contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                contactSelectOptionBidMap.put(bidData.Vendor__c,contactAuxSelectOptions.clone());
            }
        }
        if(contactsByVendorBidMap.get(bidData.Vendor__c) == null) contactsByVendorBidMap.put(bidData.Vendor__c,new List<ContactWrapper>());
        if(contactSelectOptionBidMap.get(bidData.Vendor__c) == null) contactSelectOptionBidMap.put(bidData.Vendor__c,new List<SelectOption>());
        if(contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId) == null) contactsByVendorParentBidMap.put(bidData.Vendor__r.ParentId,new List<ContactWrapper>());
        contact_DesignationTitle = new List<SelectOption>();
        contact_DesignationTitle.add(new SelectOption('',''));
        for(Schema.PicklistEntry pickListVal : Contact.Designation_title__c.getDescribe().getPicklistValues()) contact_DesignationTitle.add(new SelectOption(pickListVal.getValue(),pickListVal.getLabel()));
        List<Itinerary__c> itineraries = [SELECT Id FROM Itinerary__c WHERE Freight__c =:bidData.Freight__c AND RecordType.DeveloperName = 'Freight_Itinerary'];
        itineraryId = !itineraries.isEmpty() ? itineraries[0].Id : null;
        /**
        *  @Conga: Update for Conga.
        */
        List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id, APXTConga4__Subject__c From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c = 'Freight - Resend Bid'];
        resendBidAgreement_congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        if(!congaEmailTemplates.isEmpty() && String.isNotBlank(congaEmailTemplates[0].APXTConga4__Subject__c)) resendBidAgreement_congaEmailSubject = congaEmailTemplates[0].APXTConga4__Subject__c.replace('{OpportunityName}', bidData.Production__r.Name).replace('{StartDate}', bidData.Freight__r.Start_Date__c != null ? Datetime.newInstance(bidData.Freight__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{EndDate}', bidData.Freight__r.End_Date__c != null ? Datetime.newInstance(bidData.Freight__r.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{BidName}', bidData.Name);
        else resendBidAgreement_congaEmailSubject = 'FREIGHT BID REQUEST - ' + bidData.Production__r.Name + ' - ' + (bidData.Freight__r.Start_Date__c != null ? Datetime.newInstance(bidData.Freight__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' - ' + (bidData.Freight__r.End_Date__c != null ? Datetime.newInstance(bidData.Freight__r.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' (' + bidData.Name + ')';
        /**
        *  @/Conga
        */
        isResendBidRendered = true;
    }
    public void changeContactVendorResendBid(){
        if(vendorcontact_actual_id != null && vendorcontact_actual_id != '') bidData.Vendor_Contact__c = vendorcontact_actual_id;
        for(ContactWrapper cw : contactsByVendorBidMap.get(bidData.Vendor__c)){
            if(vendorcontact_actual_id == cw.c.Id){ cw.selected = true; cw.disabled = true;
            }else{
                if(cw.selected && cw.disabled){  cw.selected = false; cw.disabled = false;
                }
            }
        }
        if(bidData.Vendor__r.ParentId != null){
            for(ContactWrapper cw : contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId)){
                if(vendorcontact_actual_id == cw.c.Id){ cw.selected = true; cw.disabled = true;
                }else{
                    if(cw.selected && cw.disabled){ cw.selected = false; cw.disabled = false;
                    }
                }
            }
        }
    }
    //End ResendBidAgreement Methods
    ///ReleaseBid Methods
    public void openReleaseByBid(){
        if(bidData != null && bidData.Vendor__c != null){
            contactSelectOption_releaseMap = new Map<String,List<SelectOption>>();
            contactsByVendor_releaseMap = new Map<String,List<ContactWrapper>>();
            contactsByVendorParent_releaseMap = new Map<String,List<ContactWrapper>>();
            List<ContactWrapper> contactAuxList;
            List<SelectOption> contactAuxSelectOptions;
            
            if(bidData.Vendor__r.ParentId != null){
                for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId =: bidData.Vendor__r.ParentId AND Email <> NULL ORDER BY Order__c ASC]){
                    contactAuxList = contactsByVendorParent_releaseMap.get(c.AccountId) != null ? contactsByVendorParent_releaseMap.get(c.AccountId) : new List<ContactWrapper>();
                    contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),false));
                    contactsByVendorParent_releaseMap.put(c.AccountId,contactAuxList.clone());
                }
            }
            
            for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId =: bidData.Vendor__c AND Email <> NULL AND Order__c <> NULL ORDER BY Order__c ASC]){
                contactAuxList = contactsByVendor_releaseMap.get(c.AccountId) != null ? contactsByVendor_releaseMap.get(c.AccountId) : new List<ContactWrapper>();
                contactAuxList.add(new ContactWrapper(c,(bidData.Vendor_Contact__c == c.Id ? true : (c.Order__c == 1 ? true : false)),(bidData.Vendor_Contact__c == c.Id ? true : (bidData.Vendor_Contact__c == null && c.Order__c == 1 ? true : false))));
                contactsByVendor_releaseMap.put(c.AccountId,contactAuxList.clone());
            }
            
            for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId =: bidData.Vendor__c AND Email <> NULL AND Order__c = NULL ORDER BY Order__c ASC]){
                contactAuxList = contactsByVendor_releaseMap.get(c.AccountId) != null ? contactsByVendor_releaseMap.get(c.AccountId) : new List<ContactWrapper>();
                contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),(c.Order__c == 1 ? true : false)));
                contactsByVendor_releaseMap.put(c.AccountId,contactAuxList.clone());
            }
            
            if(contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId) != null){
                for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId)){
                    contactAuxSelectOptions = contactSelectOption_releaseMap.get(bidData.Vendor__c) != null ? contactSelectOption_releaseMap.get(bidData.Vendor__c) : new List<SelectOption>();
                    contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                    contactSelectOption_releaseMap.put(bidData.Vendor__c,contactAuxSelectOptions.clone());
                }
            }
            if(contactsByVendor_releaseMap.get(bidData.Vendor__c) != null){
                for(ContactWrapper cw : contactsByVendor_releaseMap.get(bidData.Vendor__c)){
                    contactAuxSelectOptions = contactSelectOption_releaseMap.get(bidData.Vendor__c) != null ? contactSelectOption_releaseMap.get(bidData.Vendor__c) : new List<SelectOption>();
                    contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                    contactSelectOption_releaseMap.put(bidData.Vendor__c,contactAuxSelectOptions.clone());
                }
            }
            if(contactsByVendor_releaseMap.get(bidData.Vendor__c) == null) contactsByVendor_releaseMap.put(bidData.Vendor__c,new List<ContactWrapper>());
            if(contactSelectOption_releaseMap.get(bidData.Vendor__c) == null) contactSelectOption_releaseMap.put(bidData.Vendor__c,new List<SelectOption>());
            if(contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId) == null) contactsByVendorParent_releaseMap.put(bidData.Vendor__r.ParentId,new List<ContactWrapper>());
            
            isReleaseBidRendered = true;
        }
    }
    public void sendReleaseByBid(){
        if(bidData != null && releaseVendorcontact_actual_id != null){
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id =:releaseVendorcontact_actual_id]) contactMap.put(c.Id,c);
            List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =:opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Freight Coordinator')];
            Journal__c journalAux;
            Bid__c bAux;
            List<Journal__c> journalAuxList = new List<Journal__c>();
            Map<String,Bid__c> bidUpdateMap = new Map<String,Bid__c>();
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail;
            String[] toAddresses;
            Set<String> ccAddresses;
            String body = '';
            List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='Freight_Release_Bid'];
            //New Journals
            journalAux = new Journal__c(
                RecordTypeId = journal_bidjournalRT,
                Bid__c = bidData.Id,
                Journal_Entry__c = 'Release Bid has been sent to ' + contactMap.get(releaseVendorcontact_actual_id).Name + ' at ' + contactMap.get(releaseVendorcontact_actual_id).Email
            );
            journalAuxList.add(journalAux);
            
            //Bid update
            if(bidData != null && bidData.Status__c != 'Contracted'){
                bAux = new Bid__c(Id=bidData.Id,Status__c='Sold Out / Not Bidding');
                bidUpdateMap.put(bAux.Id,bAux);
            }
            
            //EMAIL
            ccAddresses = new Set<String>();
            if(bidData.Vendor__c != null){
                for(ContactWrapper cw : contactsByVendor_releaseMap.get(bidData.Vendor__c)){
                    if(!cw.disabled && cw.selected) ccAddresses.add(cw.c.Email);
                }
            }
            if(bidData.Vendor__r.ParentId != null){
                for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId)){
                    if(!cw.disabled && cw.selected) ccAddresses.add(cw.c.Email);
                }
            }
            
            mail = new Messaging.SingleEmailMessage();
            if(prodAssocAux.size() > 0) mail.setOrgWideEmailAddressId(verifyWideAddress(prodAssocAux[0].User__r.Email));
            toAddresses = new String[] {contactMap.get(releaseVendorcontact_actual_id).Email};
                mail.setToAddresses(toAddresses);
            if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
            String dateIn = (bidData.Freight__r.Start_Date__c != null ? Datetime.newInstance(bidData.Freight__r.Start_Date__c.year(),bidData.Freight__r.Start_Date__c.month(),bidData.Freight__r.Start_Date__c.day()).format('dd MMMMM yyyy') : '');
            String dateOut = (bidData.Freight__r.End_Date__c != null ? Datetime.newInstance(bidData.Freight__r.End_Date__c.year(),bidData.Freight__r.End_Date__c.month(),bidData.Freight__r.End_Date__c.day()).format('dd MMMMM yyyy')  : '');
            mail.setSubject(template.size() > 0 ? template[0].Subject.replace('{ProductionName}',bidData.Production__r.Name).replace('{StartDate}',dateIn).replace('{EndDate}',dateOut) : '');
            if(template.size() > 0) body = (template[0].HTMLValue != null ? template[0].HTMLValue.replace('{FreightCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
                                            .replace('{VendorName}',bidData.Vendor__r.Name)
                                            .replace('{ProductionName}',bidData.Production__r.Name)
                                            .replace('{StartDate}',dateIn)
                                            .replace('{EndDate}',dateOut) : '');
            mail.setHtmlBody(body);
            myEmails.add(mail);
            insert journalAuxList;
            update bidUpdateMap.values();
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
        }
    }
    public void changeContactVendorReleaseByBid(){
        if(releaseVendorcontact_actual_id != null && releaseVendorcontact_actual_id != '') bidData.Vendor_Contact__c = releaseVendorcontact_actual_id;
        for(ContactWrapper cw : contactsByVendor_releaseMap.get(bidData.Vendor__c)){
            if(releaseVendorcontact_actual_id == cw.c.Id){
                cw.selected = true;
                cw.disabled = true;
            }else{
                if(cw.selected && cw.disabled){ cw.selected = false; cw.disabled = false;
                }
            }
        }
        if(bidData.Vendor__r.ParentId != null){
            for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId)){
                if(releaseVendorcontact_actual_id == cw.c.Id){ cw.selected = true; cw.disabled = true;
                }else{
                    if(cw.selected && cw.disabled){ cw.selected = false; cw.disabled = false;
                    }
                }
            }
        }
    }
    public void sendPreviewPdf(){
        emailMessage = '';
        try{
            emailMessage = sendEmail(emailbid_to,emailbid_cc,emailbid_bcc,emailbid_subject,releaseEmailBid_body,emailAttachs,opportunityId,bidData.Freight__c);
            if(emailMessage == ''){
                Journal__c journalAux;
                journalAux = new Journal__c(
                    RecordTypeId=journal_bidjournalRT,
                    Bid__c=emailbid_id,
                    Journal_Entry__c='Release Bid has been sent to ' + emailbid_primarycontactname + ' at ' + emailbid_to
                );
                List<Bid__c> bidAux = [SELECT Id, Status__c FROM Bid__c WHERE Id=:emailbid_id];
                if(bidAux.size() > 0 && bidAux[0].Status__c != 'Contracted'){
                    Bid__c b = new Bid__c(Id=emailbid_id,Status__c='Sold Out / Not Bidding');
                    update b;
                }
                if(journalAux != null) insert journalAux;
            }
        }catch(DMLException e){
            system.debug(e.getMessage());
            emailMessage = e.getMessage();
        }
    }
    @RemoteAction
    global static List<String> getDataPreviewResendBid(String opportunityid, String tripid, String bidid, String primarycontact,String url){
        List<String> result = new List<String>();
        //To
        String primary_name = '';
        List<Contact> contactList = [SELECT Id, Name, Email FROM Contact WHERE Id =: primarycontact];
        if(contactList.size() > 0){
            primary_name = contactList[0].Name;
            if(contactList[0].Email != null) 
                result.add(contactList[0].Email); 
            else 
                result.add('');
        }else{
            result.add('');
        }
        
        List<Opportunity> productionAux = [SELECT Id, Name FROM Opportunity WHERE Id =: opportunityid];
        List<Bid__c> bidAux = new List<Bid__c>();
        if(bidid != null && bidid != '') bidAux = [SELECT Id, Name, Vendor__c, Vendor__r.Name FROM Bid__c WHERE Id =: bidid];
        List<Freight__c> freightAux = [SELECT Id, Name, RecordType.Name, Start_Date__c, End_Date__c FROM Freight__c WHERE Id =: tripid];
        String dateIn = (freightAux[0].Start_Date__c != null ? Datetime.newInstance(freightAux[0].Start_Date__c.year(),freightAux[0].Start_Date__c.month(),freightAux[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateOut = (freightAux[0].End_Date__c != null ? Datetime.newInstance(freightAux[0].End_Date__c.year(),freightAux[0].End_Date__c.month(),freightAux[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        String subject;
        
        //Body
        String body = '';
        //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Freight Coordinator')];
        User userActual = FreightDashboardController.verifyEmailUser(UserInfo.getUserId(),opportunityid,tripid);
        
        List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='Freight_Bid_Request_Link_All'];
        subject = template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name)
            .replace('{StartDate}',dateIn)
            .replace('{EndDate}',dateOut)
            .replace('{BidNumber}',bidAux.size() > 0 ? bidAux[0].Name : '') : '';
        result.add(subject);
        if(template.size() > 0) body = 'Dear ' + primary_name + ',<br/><br/>' + 
            template[0].HTMLValue.replace('{FreightCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
            .replace('{VendorURL}','<a href=' + url + '/' + bidAux[0].Vendor__c + ' target=_blank>' + bidAux[0].Vendor__r.Name + '</a>')
            .replace('{BidURL}','<a href=' + url + '/' + bidAux[0].Id + ' target=_blank>' + url + '/' + bidAux[0].Id + '</a>')
            .replace('{ProductionName}',productionAux[0].Name);
        result.add(body);
        
        result.add(productionAux[0].Name);

        return result;
    }
    @RemoteAction
    global static List<String> getDataPreviewReleaseBid(String opportunityid, String tripid, String bidid, String primarycontact){
        List<String> result = new List<String>();
        //To
        String primary_name = '';
        List<Contact> contactList = [SELECT Id, Name, Email FROM Contact WHERE Id =: primarycontact];
        if(contactList.size() > 0){
            primary_name = contactList[0].Name;
            if(contactList[0].Email != null) 
                result.add(contactList[0].Email); 
            else 
                result.add('');
        }else{
            result.add('');
        }
        Bid__c bidAux = new Bid__c();
        if(bidid != null && bidid != '') bidAux = [SELECT Id, Name, Vendor__c, Vendor__r.Name FROM Bid__c WHERE Id =: bidid];
        List<Freight__c> freightAux = [SELECT Id, Name, RecordType.Name, Start_Date__c, End_Date__c FROM Freight__c WHERE Id =: tripid];
        List<Opportunity> productionAux = [SELECT Id, Name FROM Opportunity WHERE Id =: opportunityid];
        List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Freight Coordinator')];
        List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName = 'Freight_Release_Bid'];
        String dateIn = (freightAux[0].Start_Date__c != null ? Datetime.newInstance(freightAux[0].Start_Date__c.year(),freightAux[0].Start_Date__c.month(),freightAux[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateOut = (freightAux[0].End_Date__c != null ? Datetime.newInstance(freightAux[0].End_Date__c.year(),freightAux[0].End_Date__c.month(),freightAux[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        result.add(template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name).replace('{StartDate}',dateIn).replace('{EndDate}',dateOut) : '');
        result.add(template[0].HTMLValue != null ? template[0].HTMLValue.replace('{FreightCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
                                        .replace('{VendorName}',bidAux.Vendor__r.Name)
                                        .replace('{ProductionName}',productionAux[0].Name)
                                        .replace('{StartDate}',dateIn)
                                        .replace('{EndDate}',dateOut) : '');
        return result;
    }
    public static String sendEmail(String toList, String ccList, String bccList, String subject, String body, String attachs, String oppid, String tripid){
        try{
            //TO
            Set<String> toAddress = new Set<String>();
            for(String k : toList.split(',')) if(k.trim() != '') toAddress.add(k.trim());
            //CC
            Set<String> ccAddress = new Set<String>();
            for(String k : ccList.split(',')) if(k.trim() != '') ccAddress.add(k.trim());
            //BCC
            Set<String> bccAddress = new Set<String>();
            for(String k : bccList.split(',')) if(k.trim() != '') bccAddress.add(k.trim());

            User userActual = FreightDashboardController.verifyEmailUser(UserInfo.getUserId(),oppid,tripid);
            
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
            if(userActual != null && userActual.Email != null) mail.setOrgWideEmailAddressId(verifyWideAddress(userActual.Email));
            mail.setToAddresses(new List<String>(toAddress));
            if(ccAddress.size() > 0) mail.setCcAddresses(new List<String>(ccAddress));
            if(bccAddress.size() > 0) mail.setBccAddresses(new List<String>(bccAddress));
            mail.setSubject(subject);
            mail.setHtmlBody(body);
            
            if(attachs != null){
                Set<String> attachIds = new Set<String>();
                for(String att : attachs.split(',')){
                    if(att.trim() != '') attachIds.add(att.trim());
                }
                system.debug(attachIds);
                //Attachment
                List<ContentVersion> contentVersions = [SELECT Id, ContentDocumentId, Title, PathOnClient, VersionData FROM ContentVersion WHERE ContentDocumentId IN: attachIds];
                List<Messaging.Emailfileattachment> fileAttachments = new List<Messaging.Emailfileattachment>();
                if(contentVersions.size() > 0){
                    Messaging.Emailfileattachment efa;
                    for(ContentVersion cv : contentVersions){
                        efa = new Messaging.Emailfileattachment();
                        efa.setFileName(cv.PathOnClient.subString(2,cv.PathOnClient.length()));
                        efa.setBody(cv.VersionData);
                        fileAttachments.add(efa);
                    }
                }
                if(fileAttachments.size() > 0) mail.setFileAttachments(fileAttachments);
            }
            myEmails.add(mail);
            Messaging.SendEmailResult[] mailResult = Messaging.sendEmail(myEmails);
            if(!mailResult[0].isSuccess()) return mailResult[0].getErrors()[0].getMessage();
        }
        catch(System.EmailException e){
            System.debug('###FreightDashboard_Tab_Bid_Controller.sendEmail() - Email Exception: ' + e.getMessage());
            return 'An internal error has occurred. Please contact your administrator.';
        }
        return '';
    }
    //End ReleaseBid Methods
    ///DeactivateBid Methods
    public void deactivateBid(){
        if(bidData != null && bidData.Id != null){
            bidData.Status__c = 'Deactivated Bid';
            bidData.Locked__c = true;
            bidData.Deactivate__c = true;
            update bidData;
        }
    }
    //End DeactivateBid Methods
    //AddContacts Methods
    @RemoteAction
    global static Contact getDataContact(String contactId){
        return [SELECT Id, AccountId, FirstName, LastName, Phone, Work_Phone_Extension__c, Email, MobilePhone, Alternate_Email__c, Fax, Designation_title__c, Description, MailingStreet, MailingPostalCode, OtherStreet, City__c, City__r.Name FROM Contact WHERE Id =:contactId];
    }
    public void saveAddContactVendor(){
        messageCreateContact = '';
        try{
            system.debug(vendorContact);
            vendorContact.Id = (vendorContact_id != null && vendorContact_id.trim() != '' ? vendorContact_id : null);
            upsert vendorContact;
        }
        catch(DMLException e){
            messageCreateContact = validateError(e.getMessage());
        }
        if(isResendBidRendered) openResendBid();
        else if(isReleaseBidRendered) openReleaseByBid();
    }
    public static String validateError(String error){
        String message = '';
        if(error.contains('DUPLICATES_DETECTED')) message = 'You\'re creating a duplicate record. We recommend you use an existing record.';
        else message = error;
        return message;
    }
    //End AddContacts Methods
    //Rate Details Methods
    public void calculateTotalPrice(){
        if(bidRevenue != null) bidRevenue.Total_Price__c = (bidRevenue.Base_Cost__c != null ? bidRevenue.Base_Cost__c : 0) + (bidRevenue.Commission__c != null ? bidRevenue.Commission__c : 0);
    }
    public void calculateRevenue(){
        if(bidRevenue != null){
            if(bidRevenue.Commission__c != null){
                bidRevenue.Rate__c = (100 * bidRevenue.Commission__c)/(bidRevenue.Base_Cost__c != null ? bidRevenue.Base_Cost__c : 0);
            }else if(bidRevenue.Rate__c != null){
                bidRevenue.Commission__c = (bidRevenue.Rate__c * (bidRevenue.Base_Cost__c != null ? bidRevenue.Base_Cost__c : 0))/100;
            }
            calculateTotalPrice();
        }
    }
    public void calculateRevenueByCommission(){
        if(bidRevenue != null && bidRevenue.Commission__c != null){
            bidRevenue.Rate__c = (100*bidRevenue.Commission__c)/(bidRevenue.Base_Cost__c != null ? bidRevenue.Base_Cost__c : 0);
            calculateTotalPrice();
        }
    }
    public void calculateRevenueByRate(){
        if(bidRevenue != null && bidRevenue.Rate__c != null){
            bidRevenue.Commission__c = ((bidRevenue.Base_Cost__c != null ? bidRevenue.Base_Cost__c : 0) * bidRevenue.Rate__c)/100;
            calculateTotalPrice();
        }
    }
    public void getBidRevenue(){
        List<Revenue__c> bidRevenues = [Select id, Base_Cost__c, Commission__c, Rate__c, VAT_Rate__c, Gratuity__c, Total_Price__c, CurrencyIsoCode from Revenue__c where Bid__c =:bidDataMap.get(tripBidNumber).b.Id and RecordType.DeveloperName = 'Freight_Rate_Commission' order by createdDate desc limit 1];
        bidRevenue = !bidRevenues.isEmpty() ? bidRevenues[0] : new Revenue__c(RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByName().get('Freight Rate & Commission') != null ? Schema.SObjectType.Revenue__c.getRecordTypeInfosByName().get('Freight Rate & Commission').getRecordTypeId() : null, Bid__c = bidDataMap.get(tripBidNumber).b.Id, CurrencyIsoCode = 'USD');
    	symbolMap = new Map<String,String>();
        symbolMap.put(bidRevenue.CurrencyIsoCode,'');
        getSymbol();
    }
    public List<SelectOption> getCurrencyValues(){
      List<SelectOption> options = new List<SelectOption>();
       for(Schema.PicklistEntry pickListVal : Revenue__c.CurrencyIsoCode.getDescribe().getPicklistValues()) options.add(new SelectOption(pickListVal.getValue(), pickListVal.getValue() + ' - ' + pickListVal.getLabel()));
       return options;
    }
    public void getSymbol(){
        for(SelectOption so : FreightDashboardController.PickThePicklist('Revenue__c','CurrencyIsoCode')) symbolMap.put(so.getValue(),'');

        symbolMap.put('AED','د.إ');
        symbolMap.put('AFN','Af');
        symbolMap.put('ALL','L');
        symbolMap.put('AMD','Դ');
        symbolMap.put('AOA','Kz');
        symbolMap.put('ARS','$');
        symbolMap.put('AUD','$');
        symbolMap.put('AWG','ƒ');
        symbolMap.put('AZN','ман');
        symbolMap.put('BAM','КМ');
        symbolMap.put('BBD','$');
        symbolMap.put('BDT','৳');
        symbolMap.put('BGN','лв');
        symbolMap.put('BHD','ب.د');
        symbolMap.put('BIF','₣');
        symbolMap.put('BMD','$');
        symbolMap.put('BND','$');
        symbolMap.put('BOB','Bs.');
        symbolMap.put('BRL','R$');
        symbolMap.put('BSD','$');
        symbolMap.put('BTN','');
        symbolMap.put('BWP','P');
        symbolMap.put('BYN','Br');
        symbolMap.put('BZD','$');
        symbolMap.put('CAD','$');
        symbolMap.put('CDF','₣');
        symbolMap.put('CHF','₣');
        symbolMap.put('CLP','$');
        symbolMap.put('CNY','¥');
        symbolMap.put('COP','$');
        symbolMap.put('CRC','₡');
        symbolMap.put('CUP','$');
        symbolMap.put('CVE','$');
        symbolMap.put('CZK','Kč');
        symbolMap.put('DJF','₣');
        symbolMap.put('DKK','kr');
        symbolMap.put('DOP','$');
        symbolMap.put('DZD','د.ج');
        symbolMap.put('EGP','£');
        symbolMap.put('ERN','Nfk');
        symbolMap.put('ETB','');
        symbolMap.put('EUR','€');
        symbolMap.put('FJD','$');
        symbolMap.put('FKP','£');
        symbolMap.put('GBP','£');
        symbolMap.put('GEL','ლ');
        symbolMap.put('GHS','₵');
        symbolMap.put('GIP','£');
        symbolMap.put('GMD','D');
        symbolMap.put('GNF','₣');
        symbolMap.put('GTQ','Q');
        symbolMap.put('GYD','$');
        symbolMap.put('HKD','$');
        symbolMap.put('HNL','L');
        symbolMap.put('HRK','Kn');
        symbolMap.put('HTG','G');
        symbolMap.put('HUF','Ft');
        symbolMap.put('IDR','Rp');
        symbolMap.put('ILS','₪');
        symbolMap.put('INR','₹');
        symbolMap.put('IQD','ع.د');
        symbolMap.put('IRR','﷼');
        symbolMap.put('ISK','Kr');
        symbolMap.put('JMD','$');
        symbolMap.put('JOD','د.ا');
        symbolMap.put('JPY','¥');
        symbolMap.put('KES','Sh');
        symbolMap.put('KGS','');
        symbolMap.put('KHR','៛');
        symbolMap.put('KPW','₩');
        symbolMap.put('KRW','₩');
        symbolMap.put('KWD','د.ك');
        symbolMap.put('KYD','$');
        symbolMap.put('KZT','〒');
        symbolMap.put('LAK','₭');
        symbolMap.put('LBP','ل.ل');
        symbolMap.put('LKR','Rs');
        symbolMap.put('LRD','$');
        symbolMap.put('LSL','L');
        symbolMap.put('LYD','ل.د');
        symbolMap.put('MAD','د.م.');
        symbolMap.put('MDL','L');
        symbolMap.put('MGA','');
        symbolMap.put('MKD','ден');
        symbolMap.put('MMK','K');
        symbolMap.put('MNT','₮');
        symbolMap.put('MOP','P');
        symbolMap.put('MRU','UM');
        symbolMap.put('MUR','₨');
        symbolMap.put('MVR','ރ.');
        symbolMap.put('MWK','MK');
        symbolMap.put('MXN','$');
        symbolMap.put('MYR','RM');
        symbolMap.put('MZN','MTn');
        symbolMap.put('NAD','$');
        symbolMap.put('NGN','₦');
        symbolMap.put('NIO','C$');
        symbolMap.put('NOK','kr');
        symbolMap.put('NPR','₨');
        symbolMap.put('NZD','$');
        symbolMap.put('OMR','ر.ع.');
        symbolMap.put('PAB','B/.');
        symbolMap.put('PEN','S/.');
        symbolMap.put('PGK','K');
        symbolMap.put('PHP','₱');
        symbolMap.put('PKR','₨');
        symbolMap.put('PLN','zł');
        symbolMap.put('PYG','₲');
        symbolMap.put('QAR','ر.ق');
        symbolMap.put('RON','L');
        symbolMap.put('RSD','din');
        symbolMap.put('RUB','р.');
        symbolMap.put('RWF','₣');
        symbolMap.put('SAR','ر.س');
        symbolMap.put('SBD','$');
        symbolMap.put('SCR','₨');
        symbolMap.put('SDG','£');
        symbolMap.put('SEK','kr');
        symbolMap.put('SGD','$');
        symbolMap.put('SHP','£');
        symbolMap.put('SLL','Le');
        symbolMap.put('SOS','Sh');
        symbolMap.put('SRD','$');
        symbolMap.put('STN','Db');
        symbolMap.put('SYP','ل.س');
        symbolMap.put('SZL','L');
        symbolMap.put('THB','฿');
        symbolMap.put('TJS','ЅМ');
        symbolMap.put('TMT','m');
        symbolMap.put('TND','د.ت');
        symbolMap.put('TOP','T$');
        symbolMap.put('TRY','₤');
        symbolMap.put('TTD','$');
        symbolMap.put('TWD','$');
        symbolMap.put('TZS','Sh');
        symbolMap.put('UAH','₴');
        symbolMap.put('UGX','Sh');
        symbolMap.put('USD','$');
        symbolMap.put('UYU','$');
        symbolMap.put('UZS','');
        symbolMap.put('VEF','Bs F');
        symbolMap.put('VND','₫');
        symbolMap.put('VUV','Vt');
        symbolMap.put('WST','T');
        symbolMap.put('XAF','₣');
        symbolMap.put('XCD','$');
        symbolMap.put('XPF','₣');
        symbolMap.put('YER','﷼');
        symbolMap.put('ZAR','R');
        symbolMap.put('ZMW','ZK');
        symbolMap.put('ZWL','$');
    }
    //End Rate Details
    //Attachs
    public void openAttachDocs(){
        attachDocumentList = new List<ContentDocument>();
        if(attachdocument_objectid != null && attachdocument_objectid != ''){
            Set<String> contentDocumentIds = new Set<String>();
            for(ContentDocumentLink cdl : [Select Id, LinkedEntityId, ContentDocumentId FROM ContentDocumentLink WHERE LinkedEntityId =: attachdocument_objectid]) contentDocumentIds.add(cdl.ContentDocumentId);
            attachDocumentList = [Select Id, Title, FileExtension, CreatedDate FROM ContentDocument WHERE Id IN: contentDocumentIds];
        }
    }
    public void doAttachmentLast(){
        if(filename != null && body != null){
            try{
                ContentVersion conVer = new ContentVersion();
                conVer.PathOnClient = '/'+filename;
                conVer.Title = filename.split('\.')[0];
                //conVer.VersionData = EncodingUtil.base64Decode(body.subString(0,100).split(',')[1] + body.substring(100,body.length()));
                conVer.VersionData = (!Test.isRunningTest() ? EncodingUtil.base64Decode(body.subString(0,100).split(',')[1] + body.substring(100,body.length())) : Blob.valueOf('Test'));
                insert conVer;
                
                ContentVersion contentver = [SELECT ContentDocumentId, ContentDocument.FileExtension FROM ContentVersion WHERE Id =:conVer.Id];
                
                //Create ContentDocumentLink
                ContentDocumentLink cDe = new ContentDocumentLink();
                cDe.ContentDocumentId = contentver.ContentDocumentId;
                cDe.LinkedEntityId = documentRelationId;
                cDe.ShareType = 'V';
                cDe.Visibility = 'AllUsers';
                insert cDe;
                
                newattachment_id = contentver.ContentDocumentId;
                newattachment_name = filename;
            }catch(Exception e){
				system.debug(e.getMessage());
            }
        }
        filename = null;
        body = null;
        getDocumentsByBid();
    }
    public void getDocumentsByBid(){
        documentBidList = new List<ContentDocument>();
        documentListPages = new List<Integer>();
        documentListFirst = 0;
        documentListPage = 1;
        documentListLastPage = 0;
        if(bidData != null && bidData.Id != null){
            Set<String> contentDocumentIds = new Set<String>();
            for(ContentDocumentLink cdl : [SELECT Id, LinkedEntityId, ContentDocumentId FROM ContentDocumentLink WHERE LinkedEntityId =: bidData.Id]) contentDocumentIds.add(cdl.ContentDocumentId);
            documentBidList = [SELECT Id, Title, FileExtension, CreatedDate FROM ContentDocument WHERE Id IN: contentDocumentIds ORDER BY CreatedDate DESC];
            if(!documentBidList.isEmpty()) {
                Integer i = 0;
                do { i++; documentListPages.add(i); } while ((i*10)<documentBidList.size());
                documentListLastPage = i;
            }
        }
    }
    //End Attachs
    //Wrappers
    global class wrapperData{
        public String data;
        public String value;
        public String extra1;
        public wrapperData(String data, String value, String extra1){
            this.data = data;
            this.value = value;
            this.extra1 = extra1;
        }
    }
    global class ContactWrapper{
        public Contact c {get;set;}
        public Boolean selected {get;set;}
        public Boolean disabled {get;set;}
        public ContactWrapper(Contact cc, Boolean cselected, Boolean cdisabled){
            c = cc;
            selected = cselected;
            disabled = cdisabled;
        }
    }
    global class wrapperSearchPL{
        public String dataid;
        public String dataname;
        public wrapperSearchPL(String cdataid, String cdataname){
            dataid = cdataid;
            dataname = cdataname;
        }
    }
    global class BidVendorWrapper implements Comparable{
        public Bid__c b {get;set;}
        public String name {get;set;}
        public String production {get;set;}
        public Date datein {get;set;}
        public Date dateout {get;set;}
        public String description {get;set;}
        public Decimal rate {get;set;}
        public String status {get;set;}
        public String nobidreason {get;set;}
        public String venue {get;set;}
        public String vendorparent {get;set;}
        public Date createddate {get;set;}
        
        global BidVendorWrapper(Bid__c vb,String vname, String vproduction, Date vdatein, Date vdateout, String vdescription, Decimal vrate, String vstatus, String vnobidreason, String vvenue, String vvendorparent, Date vcreateddate){
            b = vb;
            name = vname;
            production = vproduction;
            datein = vdatein;
            dateout = vdateout;
            vdescription = vdescription;
            rate = vrate;
            status = vstatus;
            nobidreason = vnobidreason;
            venue = vvenue;
            vendorparent = vvendorparent;
            createddate = vcreateddate;
        }
        
        public Integer compareTo(Object obj) {
            BidVendorWrapper data = (BidVendorWrapper)obj;
            if (orderBidHistory == 'created_date') return sortByCreatedDate(data);
            if (orderBidHistory == 'name') return sortByName(data);
            if (orderBidHistory == 'production') return sortByProduction(data);
            if (orderBidHistory == 'date_in') return sortByDateIn(data);
            if (orderBidHistory == 'date_out') return sortByDateOut(data);
            if (orderBidHistory == 'description') return sortByDescription(data);
            if (orderBidHistory == 'rate') return sortByRate(data);
            if (orderBidHistory == 'status') return sortByStatus(data);
            if (orderBidHistory == 'no_bid_reason') return sortByNoBidReason(data);
            if (orderBidHistory == 'venue') return sortByVenue(data);
            if (orderBidHistory == 'provider') return sortByProvider(data);
            return 0;
        }
        
        private Integer sortByCreatedDate(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.createddate > data.createddate) return 1;
            }else{
                if (this.createddate < data.createddate) return 1;
            }
            if (this.createddate == data.createddate) return 0;
            return -1;
        }
        private Integer sortByName(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.name > data.name) return 1;
            }else{
                if (this.name < data.name) return 1;
            }
            if (this.name == data.name) return 0;
            return -1;
        }
        private Integer sortByProduction(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.production > data.production) return 1;
            }else{
                if (this.production < data.production) return 1;
            }
            if (this.production == data.production) return 0;
            return -1;
        }
        private Integer sortByDateIn(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.datein > data.datein) return 1;
            }else{
                if (this.datein < data.datein) return 1;
            }
            if (this.datein == data.datein) return 0;
            return -1;
        }
        private Integer sortByDateOut(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.dateout > data.dateout) return 1;
            }else{
                if (this.dateout < data.dateout) return 1;
            }
            if (this.dateout == data.dateout) return 0;
            return -1;
        }
        private Integer sortByDescription(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.description > data.description) return 1;
            }else{
                if (this.description < data.description) return 1;
            }
            if (this.description == data.description) return 0;
            return -1;
        }
        private Integer sortByRate(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.rate > data.rate) return 1;
            }else{
                if (this.rate < data.rate) return 1;
            }
            if (this.rate == data.rate) return 0;
            return -1;
        }
        private Integer sortByStatus(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.status > data.status) return 1;
            }else{
                if (this.status < data.status) return 1;
            }
            if (this.status == data.status) return 0;
            return -1;
        }
        private Integer sortByNoBidReason(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.nobidreason > data.nobidreason) return 1;
            }else{
                if (this.nobidreason < data.nobidreason) return 1;
            }
            if (this.nobidreason == data.nobidreason) return 0;
            return -1;
        }
        private Integer sortByVenue(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.venue > data.venue) return 1;
            }else{
                if (this.venue < data.venue) return 1;
            }
            if (this.venue == data.venue) return 0;
            return -1;
        }
        private Integer sortByProvider(BidVendorWrapper data) {
            if(orderBidHistoryOrientation == 'ASC'){
                if (this.vendorparent > data.vendorparent) return 1;
            }else{
                if (this.vendorparent < data.vendorparent) return 1;
            }
            if (this.vendorparent == data.vendorparent) return 0;
            return -1;
        }
    }
    //End Wrappers
    /**
    *  @Conga: Conga Methods.
    */
    public void congaResendBid(){
        if(String.isNotBlank(resendBidAgreement_contactPrimary)){
            List<String> congaParameters = new List<String>();
            String contactPrimaryName = '';
            Contact primaryContact = new Contact();
            String ccEmails = '';
            for(ContactWrapper contactWrapperItem:(bidData.Vendor__c != null ? contactsByVendorBidMap.get(bidData.Vendor__c) : new List<ContactWrapper>())){
                if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
                if(String.isNotEmpty(contactWrapperItem.c.id) && contactWrapperItem.c.id.equals(resendBidAgreement_contactPrimary)) primaryContact = contactWrapperItem.c;
            }
            for(ContactWrapper contactWrapperItem:(bidData.Vendor__r.ParentId != null ? contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId) : new List<ContactWrapper>())){
                if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
                if(String.isNotEmpty(contactWrapperItem.c.id) && contactWrapperItem.c.id.equals(resendBidAgreement_contactPrimary)) primaryContact = contactWrapperItem.c;
            }
            congaParameters.add('&id=' + bidData.id + (congaQueriesMap.containsKey('Freight - BidById') ? '&QueryId=[Bid]' + congaQueriesMap.get('Freight - BidById').Id + '?pv0=' + bidData.id + (congaQueriesMap.containsKey('Freight - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap.get('Freight - SubTripsByBidId').Id + '?pv0=' + bidData.id : '') + (congaQueriesMap.containsKey('Freight - ContactById') ? ',[Contact]' + congaQueriesMap.get('Freight - ContactById').Id + '?pv0=' + resendBidAgreement_contactPrimary : '') + (congaQueriesMap.containsKey('Freight - UserById') ? ',[EmailFromUser]' + congaQueriesMap.get('Freight - UserById').Id + '?pv0=' + (String.isNotBlank(resendBidAgreement_emailFromUserId) ? resendBidAgreement_emailFromUserId : '') : '') : '') + '&CongaEmailTemplateId='+ resendBidAgreement_congaEmailTemplateId + '&EmailSubject=' + resendBidAgreement_congaEmailSubject.replace(' ', '+') + (String.isNotBlank(resendBidAgreement_congaEmailFromId) ? '&EmailFromID=' + resendBidAgreement_congaEmailFromId : '') + '&EmailToId=' + resendBidAgreement_contactPrimary + '&EmailCC=' + ccEmails + '&TemplateId=' + resendBidAgreement_congaTemplateId + '&OFN=Freight+Bid-' + bidData.Name);
            try{
                congaSendEmail(congaParameters);
                if(bidData.Status__c != 'Contracted'){
                    bidData.Status__c = 'Sent';
                    update new Bid__c(Id = bidData.Id, Status__c = 'Sent');               
                }
                if(bidData.Freight__r.Status__c != 'Contracted' || bidData.Freight__r.Status__c != 'In Contracting'){
                    update new Freight__c(id = bidData.Freight__c, Status__c = 'Bid Request Stage');
                    List<Itinerary__c> itineraries = [SELECT Id FROM Itinerary__c WHERE Freight__c =:bidData.Freight__c AND RecordType.DeveloperName = 'Freight_Itinerary'];
                    if(!itineraries.isEmpty()) update new Itinerary__c(Id = itineraries[0].Id, Status__c = 'Bid Request Stage');
                }
                insert new Journal__c(RecordTypeId = journal_bidjournalRT, Bid__c = bidData.Id, Journal_Entry__c = 'Resend Bid email was sent to ' + (String.isNotBlank(primaryContact.Name) ? primaryContact.Name : '') + ' ' + (String.isNotBlank(primaryContact.Email) ? primaryContact.Email : '') + (String.isNotBlank(ccEmails) ? ', cc: ' + ccEmails : ''));
            }
            catch(Exception e){
                System.debug('###FreightDashboard_Tab_Bid_Controller.congaResendBid() - Exception: ' + e.getMessage());
            }
        }
    }
    @future(callout=true)
    public static void congaSendEmail(List<String> congaParameters){
        HttpRequest request = new HttpRequest();
        request.setMethod('GET');
        request.setTimeout(120000);
        Http http = new Http();
        HTTPResponse response;
        for(String parameters:congaParameters){
            request.setEndpoint('https://composer.congamerge.com/composer8/index.html?sessionId=' + UserInfo.getOrganizationId() + '' +UserInfo.getSessionId().SubString(15) + '&serverUrl=' + EncodingUtil.urlEncode(System.Url.getSalesforceBaseUrl().toExternalForm() + '/services/Soap/u/29.0/' + UserInfo.getOrganizationId(), 'UTF-8') + parameters + '&DefaultPDF=1&DS7=2&APIMode=12');
            try{
                response = http.send(request);  
                System.debug('###FreightDashboard_Tab_Bid_Controller.congaEmail(parameters = ' + parameters + ') => Response Status Code: ' + response.getStatusCode() + ', Response Body: ' + (String.isNotEmpty(response.getBody()) ? response.getBody().left(255) : ''));
            }
            catch(Exception e){
                System.debug('###FreightDashboard_Tab_Bid_Controller.congaEmail() - Callout Exception: ' + e.getMessage());
            }
        }
    }
    /**
    *  @/Conga
    */
}```

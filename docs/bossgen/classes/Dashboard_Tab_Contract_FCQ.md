---
layout: default
title: Dashboard_Tab_Contract_FCQ
parent: classes
---
# Metadata Type
classes


# Filename 
Dashboard_Tab_Contract_FCQ


# Raw XML
```
public class Dashboard_Tab_Contract_FCQ {
    public DashboardConfigurationWrapper vfpConfiguration {get;set;}
    public String fcqId {get;set;}
    public String fcqFreightName {get;set;}
    public String fcqFreightService {get;set;}
    public String tripsSelected {get;set;}
    public String clientIdReceived {get;set;}
    public String fcqClientId {get;set;}
    public String clientsJSON {get;set;}
    public String fcqVendorContactId {get;set;}
    public String subTripfcqListJSON {get;set;}
    public String subTripfcqMapJSON {get;set;}
    public Bid__c fcqBid {get;set;}
    public String journal_bidjournalRT {get;set;}
    public Map<Id,Contact> vendorContacts {get;set;}
    public String vendorContactsJSON {get;set;}
    public List<SelectOption> vendorContactOptions {get;set;}
    public Freight__c fcqFreight {get;set;}
    public String fcqFreightJSON {get;set;}
    public List<Freight__c> subTripList {get;set;}
    public List<Freight__c> subTripfcqList {get;set;}
    public List<Contact> drivers {get;set;}
    public Map<Id,List<Freight__c>> travelsBySubTripMap {get;set;}
    public Map<Id,List<Dashboard_Tab_Contract_FCQ.SubTripfcqWrapper>> subTripfcqMap {get;set;}
    public Boolean loadDocuments {get;set;}
    public Boolean loadJournals {get;set;}
    public String congaQueriesJson {get;set;}
    public String congaEmailFromId {get;set;}
    public String congaEmailTemplateId {get;set;}
    public String congaTemplateId {get;set;}
    public String fcqEmailType {get;set;}
    public Sub_Trip_FCQ__c fcqDetail {get;set;}
    public Integer fcqActualNumber {get;set;}
    public Integer subTripfcqMapSize {get;set;}
    public Map<Integer,String> fcqDetailMap {get;set;}
    public String subtripSelected {get;set;}
    public List<Freight__c> vehiclesByBidList {get;set;}
    public List<SelectOption> dataContactPL {get;set;}
    public String chkContactSelected {get;set;}
    public cContactWrapper dataContactSelected {get;set;}
    public String recordContactSelected {get;set;}
    public Draft__c draft {get;set;}
    public String primaryCoordinatorName {get;set;}
    public String bodyemail {get;set;}
    public Boolean isNew {get;set;}
    public String filename {get;set;}
    transient public String body {get;set;}
    public String newattachment_id {get;set;}
    public String newattachment_name {get;set;}
    public String documentRelationId {get;set;}
    public String attachdocument_objectid {get;set;}
    public List<ContentDocument> attachDocumentList {get;set;}
    //Send to FT
    public List<SelectOption> dataContact_sendToFTPL {get;set;}
    public cContactWrapper dataContactSendToFTSelected {get;set;}
    //Attach FCQ
    public Boolean isAttachFCQRendered {get;set;}
    public Map<Freight__c, List<Freight__c>> fcqSubtripsMap {get;set;}
    public Map<Id, Freight__c> bidSubtripsMap {get;set;}
    public Boolean isFcqEmpty {get;set;}
    public Boolean isFcqSearched {get;set;}
    public Freight__c searchFreight {get;set;}
    
    public Dashboard_Tab_Contract_FCQ(){
        fcqActualNumber = 0;
        subTripfcqMapSize = 0;
        fcqDetailMap = new Map<Integer,String>();
        vehiclesByBidList = new List<Freight__c>();
        drivers = new List<Contact>();
        dataContactPL = new List<SelectOption>();
        dataContact_sendToFTPL = new List<SelectOption>();
        isAttachFCQRendered = false;
    }
    public void loadBidSubTrips() {
        fcqDetail = new Sub_Trip_FCQ__c();
        fcqFreightName = '';
        fcqFreightService = '';
        drivers = new List<Contact>();
        List<Freight__c> searchFreight = [SELECT Name, Service_Type__c FROM Freight__c WHERE Id = :vfpConfiguration.parentId LIMIT 1];
        if(!searchFreight.isEmpty()) {
            fcqFreightName = searchFreight.get(0).Name;
            fcqFreightService = searchFreight.get(0).Service_Type__c;
        }
        fcqFreight = new Freight__c();
        fcqId = '';
        tripsSelected = '';
        vendorContactsJSON = '';
        subTripfcqList = new List<Freight__c>();
        travelsBySubTripMap = new Map<Id,List<Freight__c>>();
        subTripList = [SELECT Id, Name, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, Freight_Trip_Details__c, Start_Date__c
                       FROM Freight__c WHERE Bid_Sub_Trip__c = :vfpConfiguration.bidId AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details' ORDER BY Trip_Order__c ASC];
        if(!subTripList.isEmpty()){
            for(Freight__c subtrip : subTripList) travelsBySubTripMap.put(subtrip.Id,new List<Freight__c>());
            for(Freight__c g : [SELECT Id, Line__c, Equipment__c, Vehicle_Ref__c, Freight_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c FROM Freight__c WHERE RecordType.DeveloperName = 'Equipment_Details' AND Freight_Sub_Trip_Details__c =: subTripList ORDER BY Line__c ASC]) if(travelsBySubTripMap.containsKey(g.Freight_Sub_Trip_Details__c)) travelsBySubTripMap.get(g.Freight_Sub_Trip_Details__c).add(g);
        }
        subTripfcqMap = new Map<Id,List<Dashboard_Tab_Contract_FCQ.SubTripfcqWrapper>>();
        loadBidSubTripsfcqMap();
        fcqBid = new Bid__c();
        List<Bid__c> searchBid = [SELECT Id, Name, Vendor__c, Vendor__r.Name, Vendor__r.ParentId, Vendor_Contact__c, Provider__c, Freight__c, Freight__r.Name, Freight__r.Start_Date__c, Freight__r.Service_Type__c, Form_Email_Confirmation__c, Production__c, Production__r.Production_ID__c, Email_Confirmation_Last_Send_By__c, Email_Confirmation_Last_Send_Date__c, Contracting_Back_End_Coordinator__c, Contracting_Back_End_Coordinator__r.Name, Contracting_Back_End_Coordinator__r.Email, Contracting_Back_End_Coordinator__r.Phone FROM Bid__c WHERE Id = :vfpConfiguration.bidId LIMIT 1];
        if(!searchBid.isEmpty()) {
            fcqBid = searchBid.get(0);
            vehiclesByBidList = [SELECT Id, Production__c, RecordTypeId, RecordType.Name, Equipment__c, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c 
                                     FROM Freight__c WHERE RecordType.DeveloperName = 'Vehicle_Type' AND Production__c =: fcqBid.Production__c
                                     AND Bid__c =: fcqBid.Id AND Bid_Sub_Trip__c = NULL AND Freight_Sub_Trip_Details__c = NULL AND Sales_Freight_details__c = NULL];
            
            vendorContacts = new Map<Id,Contact>();
            Map<String,Contact> contactMap = new Map<String,Contact>();
            if(fcqBid.Vendor__c != null){
                for(Contact c : [SELECT Id, Name, Email, Phone, MobilePhone  FROM Contact WHERE AccountId =: fcqBid.Vendor__c]) contactMap.put(c.Id,c);
                if(fcqBid.Vendor__r.ParentId != null) for(Contact c : [SELECT Id, Name, Email, Phone, MobilePhone FROM Contact WHERE AccountId =: fcqBid.Vendor__r.ParentId]) contactMap.put(c.Id,c);
            } 
            else if(fcqBid.Provider__c != null){
                for(Contact c : [SELECT Id, Name, Email, Phone, MobilePhone FROM Contact WHERE AccountId =: fcqBid.Provider__c]) contactMap.put(c.Id,c);
                if(fcqBid.Provider__r.ParentId != null) for(Contact c : [SELECT Id, Name, Email, Phone, MobilePhone FROM Contact WHERE AccountId =: fcqBid.Provider__r.ParentId]) contactMap.put(c.Id,c);
            }
            vendorContactOptions = new List<SelectOption>();
            vendorContactOptions.add(new SelectOption('','---None---'));
            for(Contact c : contactMap.values()){
                vendorContacts.put(c.Id,c);
                vendorContactOptions.add(new SelectOption(c.Id,c.Name));
            }
            vendorContactsJSON = JSON.serialize(vendorContacts);
            clientsJSON = JSON.serialize(vfpConfiguration.clientMap);
        }
    }
    public void loadBidSubTripsfcqMap() {
        Set<Id> subTripIds = new Set<Id>();
        for(Freight__c subTrip : subTripList) {
            subTripIds.add(subTrip.Id);
            subTripfcqMap.put(subTrip.Id,new List<Dashboard_Tab_Contract_FCQ.SubTripfcqWrapper>());
        }
        
        Map<String,String> mapTemp = new Map<String,String>();
        if(!subTripIds.isEmpty()) {
            List<Sub_Trip_FCQ__c> searchSubTripfcqrelatives = [SELECT FCQ_Details__c, FCQ_Details__r.Name, Freight_Sub_Trip_Details__c FROM Sub_Trip_FCQ__c WHERE Freight_Sub_Trip_Details__c IN :subTripIds ORDER BY CreatedDate ASC];
            for(Sub_Trip_FCQ__c st : searchSubTripfcqrelatives){
                subTripfcqMap.get(st.Freight_Sub_Trip_Details__c).add(new Dashboard_Tab_Contract_FCQ.SubTripfcqWrapper(st.FCQ_Details__c, st.FCQ_Details__r.Name));
                mapTemp.put(st.FCQ_Details__c,st.FCQ_Details__c);
            }
        }
        
        Integer j = 1;
        fcqDetailMap = new Map<Integer,String>();
        for(String s : mapTemp.keySet()){
            fcqDetailMap.put(j,s);
            j++;
        }
        
        for(Id subTripId : subTripfcqMap.keySet()){
            for(Integer i=0; i<subTripfcqMap.get(subTripId).size(); i++){
                if(subTripfcqMap.get(subTripId).size()>1 && i<subTripfcqMap.get(subTripId).size()-1) subTripfcqMap.get(subTripId).get(i).name += ', ';
            }
        }
        
        fcqActualNumber = 0;
        subTripfcqMapSize = 0;
        isAttachFCQRendered = false;
    }
    public void OpenFCQ() {
        fcqClientId = '';
        fcqFreight = new Freight__c();
        subTripfcqList = new List<Freight__c>();
        drivers = new List<Contact>();
        if(String.isBlank(fcqId)) {
            fcqClientId = clientIdReceived;
            if(fcqBid != null && fcqBid.Id != null && !tripsSelected.equals('')) {
                fcqFreight.Production__c = vfpConfiguration.productionId;
                fcqFreight.Client_Contact__c = fcqClientId;
                fcqFreight.Vendor_lookup__c = fcqBid.Vendor__c;
                fcqFreight.Vendor_Contact__c = fcqBid.Vendor_Contact__c;
                fcqVendorContactId = fcqFreight.Vendor_Contact__c;
                fcqFreight.RecordTypeId = Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('FCQ_Details').getRecordTypeId();
                Set<String> fcqTripIds = new Set<String>();
                for(String tripIdSelected : tripsSelected.split(',')) fcqTripIds.add(tripIdSelected);
                List<Sub_Trip_FCQ__c> fcqSubTrips = new List<Sub_Trip_FCQ__c>();
                for(Freight__c subTrip : subTripList) if(fcqTripIds.contains(subTrip.Id)) fcqSubTrips.add(new Sub_Trip_FCQ__c(Freight_Sub_Trip_Details__c = subTrip.Id));
                if(!fcqSubTrips.isEmpty()) {
                    insert fcqFreight;
                    fcqId = fcqFreight.Id;
                    for(Sub_Trip_FCQ__c subTripfcq : fcqSubTrips) subTripfcq.FCQ_Details__c = fcqId;
                    insert fcqSubTrips;
                    loadBidSubTripsfcqMap();
                    Set<Id> subTripfcqIds = new Set<Id>();
                    List<Sub_Trip_FCQ__c> searchfcqTrips = [SELECT Freight_Sub_Trip_Details__c FROM Sub_Trip_FCQ__c WHERE FCQ_Details__c = :fcqId];
                    for(Sub_Trip_FCQ__c subTripfcq : searchfcqTrips) subTripfcqIds.add(subTripfcq.Freight_Sub_Trip_Details__c);
                    for(Freight__c subTrip : subTripList) if(subTripfcqIds.contains(subTrip.Id)) subTripfcqList.add(subTrip);
                }
            }
        } else {
            List<Freight__c> searchfcq = [SELECT 	Id, Name, Production__c, Client_Contact__c, Vendor_lookup__c, Vendor_lookup__r.Name, Vendor_Contact__c, CreatedDate, CreatedBy.Name, Driver_Name_1__c, Driver_Mobile_1__c,
                                          			Confirm_Address_Route__c, Confirm_all_permits_ATA_Carnets_Import__c, Is_it_an_exclusive_shipment_or_LTL__c, Trailer_information__c, Any_specific_info_need_for_entering_the__c,
                                          			Vehicle_registration__c, Confirm_size__c, Equipment_FCQ__c, Flight_info__c, Carnet_info__c, Vessel_number__c
                                         FROM Freight__c WHERE Id = :fcqId LIMIT 1];
        	if(!searchfcq.isEmpty()) fcqFreight = searchfcq.get(0);
            fcqId = fcqFreight.Id;
            fcqVendorContactId = fcqFreight.Vendor_Contact__c;
            fcqClientId = fcqFreight.Client_Contact__c;
            Set<Id> subTripfcqIds = new Set<Id>();
            List<Sub_Trip_FCQ__c> searchfcqTrips = [SELECT Freight_Sub_Trip_Details__c FROM Sub_Trip_FCQ__c WHERE FCQ_Details__c = :fcqId];
            for(Sub_Trip_FCQ__c subTripfcq : searchfcqTrips) subTripfcqIds.add(subTripfcq.Freight_Sub_Trip_Details__c);
            for(Freight__c subTrip : subTripList) if(subTripfcqIds.contains(subTrip.Id)) subTripfcqList.add(subTrip);
            for(Contact driver : [SELECT Id, FirstName, Name, MobilePhone FROM Contact WHERE FCQ_Driver__c = :fcqFreight.Id ORDER BY CreatedDate]) drivers.add(driver);
        }
        subTripfcqListJSON = JSON.serialize(subTripfcqList);
        subTripfcqMapJSON = JSON.serialize(travelsBySubTripMap);
        getfcqDetailActual();
        /**
        *  @Conga: Update for Conga.
        */
        List<APXTConga4__Conga_Template__c> congaTemplates = [Select Id From APXTConga4__Conga_Template__c Where APXTConga4__Name__c = 'Freight - Email Confirmation'];
        congaTemplateId = !congaTemplates.isEmpty() ? congaTemplates[0].id : null;
        Map<String, APXTConga4__Conga_Merge_Query__c> congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
        for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('Freight - BidById', 'Freight - SubTripsByFCQId', 'Freight - FCQById')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
        congaQueriesJson = JSON.serialize(congaQueriesMap);
        /**
        *  @/Conga
        */
    }
    public void getfcqDetailActual(){
        List<Sub_Trip_FCQ__c> fcqDetailList = [SELECT Id, Name, FCQ_Details__r.Name FROM Sub_Trip_FCQ__c WHERE FCQ_Details__c = :fcqId];
        if(fcqDetailList.size() > 0) fcqDetail = fcqDetailList[0];
        fcqActualNumber = 0;
        subTripfcqMapSize = fcqDetailMap.size();
        for(Integer i : fcqDetailMap.keySet()){
            if(fcqId == fcqDetailMap.get(i)){
                fcqActualNumber = i;
            }
        }
    }
    public void getDetailByNumberBefore(){
        fcqActualNumber = fcqActualNumber - 1;
        subTripfcqMapSize = fcqDetailMap.size();
        for(Integer i : fcqDetailMap.keySet()){
            if(fcqActualNumber == i){
                fcqId = fcqDetailMap.get(i);
                OpenFCQ();
            }
        }
    }
    public void getDetailByNumberNext(){
        fcqActualNumber = fcqActualNumber + 1;
        subTripfcqMapSize = fcqDetailMap.size();
        for(Integer i : fcqDetailMap.keySet()){
            if(fcqActualNumber == i){
                fcqId = fcqDetailMap.get(i);
                OpenFCQ();
            }
        }
    }
    public void SaveFCQ() {
        Map<String,Object> root = (Map<String,Object>) JSON.deserializeUntyped(fcqFreightJSON);
        Freight__c fcqUpdated = new Freight__c();
        fcqUpdated.Id = fcqFreight.Id;
        if(root.containsKey('clientContact')) fcqUpdated.Client_Contact__c = String.isNotBlank((String) root.get('clientContact'))? (String) root.get('clientContact') : null;
        if(root.containsKey('vendorContact')) fcqUpdated.Vendor_Contact__c = String.isNotBlank((String) root.get('vendorContact'))? (String) root.get('vendorContact') : null;
        if(root.containsKey('confirmAddressRoute')) fcqUpdated.Confirm_Address_Route__c = (Boolean) root.get('confirmAddressRoute');
        if(root.containsKey('confirmAllPermits')) fcqUpdated.Confirm_all_permits_ATA_Carnets_Import__c = (Boolean) root.get('confirmAllPermits');
        if(root.containsKey('driverName1')) {
            if(String.isNotBlank((String) root.get('driverName1'))) {
                fcqUpdated.Driver_Name_1__c = (String) root.get('driverName1');
                if(root.containsKey('driverMobile1')) fcqUpdated.Driver_Mobile_1__c = (String) root.get('driverMobile1');
            } else {
                fcqUpdated.Driver_Name_1__c = '';
                fcqUpdated.Driver_Mobile_1__c = '';
            }
        }
        List<Contact> driversUpsert = new List<Contact>();
        List<Contact> driversRemoved = new List<Contact>();
        Map<Id,Contact> driversNow = new Map<Id,Contact>();
        for(Contact driver : drivers) driversNow.put(driver.Id,driver);
        if(root.containsKey('otherDrivers')) {
            Id fcqContactRTId = Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('FCQ_Driver').getRecordTypeId();
            List<Object> otherDriversJSON = (List<Object>) root.get('otherDrivers');
            for(Object otherDriverJSON : otherDriversJSON) {
                Map<String,Object> otherDriver = (Map<String,Object>) otherDriverJSON;
                Contact driverNew = new Contact();
                if(otherDriver.containsKey('driverId') && String.isNotBlank((String) otherDriver.get('driverId'))) driverNew.Id = (String) otherDriver.get('driverId');
                if(otherDriver.containsKey('driverMobile')) driverNew.MobilePhone = (String) otherDriver.get('driverMobile');
                if(otherDriver.containsKey('driverName') && String.isNotBlank((String) otherDriver.get('driverName'))) {
                    List<String> names = ((String) otherDriver.get('driverName')).split(' ');
                    if(names.size()>1) {
                        driverNew.LastName = names.get(names.size()-1);
                        names.remove(names.size()-1);
                        driverNew.FirstName = String.join(names, ' ');
                    }
                    else driverNew.LastName = (String) otherDriver.get('driverName');
                    driverNew.RecordTypeId = fcqContactRTId;
                    driverNew.FCQ_Driver__c = fcqFreight.Id;
                }
                if(driverNew.RecordTypeId == fcqContactRTId) driversUpsert.add(driverNew);
            }
        }
        if(!driversUpsert.isEmpty() && String.isBlank(fcqUpdated.Driver_Name_1__c)) {
            fcqUpdated.Driver_Name_1__c = String.isNotBlank(driversUpsert.get(0).FirstName)? driversUpsert.get(0).FirstName+' '+driversUpsert.get(0).LastName : driversUpsert.get(0).LastName;
            fcqUpdated.Driver_Mobile_1__c = driversUpsert.get(0).MobilePhone;
            driversUpsert.remove(0);
        }
        for(Contact driver : driversUpsert) if(String.isNotBlank(driver.Id) && driversNow.containsKey(driver.Id)) driversNow.remove(driver.Id);
        for(Contact driver : driversNow.values()) driversRemoved.add(driver);
        if(!driversUpsert.isEmpty()) upsert driversUpsert;
        if(!driversRemoved.isEmpty()) delete driversRemoved;
        if(root.containsKey('exclusiveShipment')) fcqUpdated.Is_it_an_exclusive_shipment_or_LTL__c = (String) root.get('exclusiveShipment');
        if(root.containsKey('trailerInformation')) fcqUpdated.Trailer_information__c = (String) root.get('trailerInformation');
        if(root.containsKey('anySpecificInfo')) fcqUpdated.Any_specific_info_need_for_entering_the__c = (String) root.get('anySpecificInfo');
        if(root.containsKey('vehicleRegistration')) fcqUpdated.Vehicle_registration__c = (String) root.get('vehicleRegistration');
        if(root.containsKey('confirmSize')) fcqUpdated.Confirm_size__c = (Boolean) root.get('confirmSize');
        if(root.containsKey('equipmentFCQ')) fcqUpdated.Equipment_FCQ__c = (Boolean) root.get('equipmentFCQ');
        if(root.containsKey('flightInfo')) fcqUpdated.Flight_info__c = (String) root.get('flightInfo');
        if(root.containsKey('carnetInfo')) fcqUpdated.Carnet_info__c = (String) root.get('carnetInfo');
        if(root.containsKey('vesselNumber')) fcqUpdated.Vessel_number__c = (String) root.get('vesselNumber');
        update fcqUpdated;
        OpenFCQ();
    }
    public void deactivateFCQ() {
        if(fcqFreight.Id != null && String.isNotBlank(fcqId)) {
            List<Sub_Trip_FCQ__c> fcqSubTrips = [SELECT Id FROM Sub_Trip_FCQ__c WHERE FCQ_Details__c = :fcqFreight.Id];
            if(!fcqSubTrips.isEmpty()) delete fcqSubTrips;
            List<Journal__c> journals = new List<Journal__c>();
            for(Journal__c j : [SELECT Id, Journal_Entry__c FROM Journal__c WHERE Freight__c =: fcqFreight.Id AND RecordType.DeveloperName = 'FCQ_Journal']){
                j.Journal_Entry__c = '(FCQ Deactivated) ' + (j.Journal_Entry__c != null ? j.Journal_Entry__c : '');
                journals.add(j);
            }
            update journals;
            delete fcqFreight;
        }
        fcqId = '';
        loadBidSubTripsfcqMap();
    }
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
                conVer.VersionData = (body.length() > 100 ? EncodingUtil.base64Decode(body.subString(0,100).split(',')[1] + body.substring(100,body.length())) : EncodingUtil.base64Decode(body.split(',')[1]));
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
            }
            catch(Exception e){
				system.debug(e.getMessage());
            }
        }
        filename = null;
        body = null;
    }
    public static String verifyWideAddress(String email){
        String oweaId;
        List<OrgWideEmailAddress> oweaList;
        if(Test.isRunningTest()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; else oweaList = [select Id from OrgWideEmailAddress where Address =: email];
        if(oweaList.isEmpty()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; //Email default
        oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
        return oweaId;
    }
    public User verifyEmailUser(String userId){
        Map<String,User> associationsMap = new Map<String,User>();
        List<Production_Associations__c> productAssociactions = [SELECT Id, User__c, User__r.Name, User__r.Email, User__r.Phone FROM Production_Associations__c WHERE RecordType.DeveloperName = 'Production_Coordinators' AND Production_Opp__c =:fcqBid.Production__c AND Team_Roles__c includes ('Primary Contract Coordinator') AND User__c <> NULL];
        return !productAssociactions.isEmpty() && (productAssociactions[0].User__c == userId || String.isEmpty(fcqBid.Contracting_Back_End_Coordinator__c)) ? productAssociactions[0].User__r : String.isNotEmpty(fcqBid.Contracting_Back_End_Coordinator__c) ? fcqBid.Contracting_Back_End_Coordinator__r : new User();
    }    
    ///EmailConfirmationSendtoFT Methods
    public void openEmailConfirmation(){
        draft = new Draft__c();
        User emailFromUser = verifyEmailUser(UserInfo.getUserId());
        primaryCoordinatorName = emailFromUser.Name;
        congaEmailFromId = verifyWideAddress(emailFromUser.Email);
        if(fcqEmailType == 'Email Confirmation'){
            isNew = false;
            dataContactSelected = new cContactWrapper();
            if(String.isNotBlank(fcqBid.Form_Email_Confirmation__c)){
                draft = [SELECT Id, Name, Attention__c, Salutation__c, Production_Assoc_Type__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate FROM Draft__c WHERE Name = :fcqBid.Form_Email_Confirmation__c];
                recordContactSelected = draft.Production_Assoc_Contact_Id__c;
                chkContactSelected = draft.Production_Assoc_Type__c;
                if(recordContactSelected != null && recordContactSelected != ''){
                    if(draft.Production_Assoc_Type__c == 'production_contacts'){
                        List<Contact> cAux = [SELECT Id, Name, Email FROM Contact WHERE Id =: recordContactSelected];
                        if(cAux.size() > 0) dataContactSelected = new cContactWrapper(cAux[0].Id,cAux[0].Name,cAux[0].Email,'contact');
                    }else if(draft.Production_Assoc_Type__c == 'ft_coordinators'){
                        List<User> uAux = [SELECT Id, Name, Email FROM User WHERE Id =: recordContactSelected];
                        if(uAux.size() > 0) dataContactSelected = new cContactWrapper(uAux[0].Id,uAux[0].Name,uAux[0].Email,'user');
                    }
                }
            }else{
                isNew = true;
                draft.Subject__c =  (fcqBid.Freight__r.Start_Date__c != null ? Datetime.newInstance(fcqBid.Freight__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' Travel Confirmations for ' + vfpConfiguration.productionName ;
                draft.Body__c = 'Please review the attached confirmations for your upcoming travel.' +
                    '<br/><br/>All details have been confirmed with the vendors and your contact information has been provided to them. Please don\'t hesitate to contact their dispatch if there are any questions or last minute changes that they can update directly.' +
                    '<br/><br/>Bus driver assignment is based on information given at the time of confirmation call and is subject to change. For up-to-date driver information, we recommend that you call dispatch at the number listed the day prior/morning of trip.' +
                    '<br/><br/><br/>Thanks,';
                
                if(String.isNotBlank(draft.Subject__c)) {
                    insert draft;
                    draft = [SELECT Id, Name, Attention__c, Salutation__c, Production_Assoc_Type__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate FROM Draft__c WHERE Id = :draft.Id];
                    update new Bid__c(Id = fcqBid.Id, Form_Email_Confirmation__c = draft.Name);
                    fcqBid.Form_Email_Confirmation__c =  draft.Name;
                }
            }
            searchContactData();
            journal_bidjournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByName().get('Bid Journal') != null ? Schema.SObjectType.Journal__c.getRecordTypeInfosByName().get('Bid Journal').getRecordTypeId() : null;
            Bid__c bid = [Select id, Email_Confirmation_Last_Send_By__c, Email_Confirmation_Last_Send_Date__c from Bid__c where id =:fcqBid.Id];
            fcqBid.Email_Confirmation_Last_Send_By__c = bid.Email_Confirmation_Last_Send_By__c;
            fcqBid.Email_Confirmation_Last_Send_Date__c = bid.Email_Confirmation_Last_Send_Date__c;
        }
        else if(fcqEmailType == 'Send to FT'){
            dataContact_sendToFTPL = new List<SelectOption>();
            dataContact_sendToFTPL.add(new SelectOption('','-- Select --'));
            dataContactSendToFTSelected = new cContactWrapper();
            if(fcqBid != null && fcqBid.Production__c != null){
                Map<Id,Profile> profileIds = new Map<id,profile>([SELECT Id,UserLicenseId FROM Profile where UserLicenseId  in (SELECT Id FROM UserLicense where name ='Salesforce')]);
                for(User k1 : [SELECT Id, Name FROM User WHERE isActive = true AND ProfileId IN: profileIds.Keyset() ORDER BY Name ASC]){
                    dataContact_sendToFTPL.add(new SelectOption(k1.Id,k1.Name));
                }
                List<Production_Associations__c> coordinators = [SELECT Id, User__c, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: fcqBid.Production__c AND Team_Roles__c includes ('Primary Contract Coordinator') LIMIT 1];
                if(!coordinators.isEmpty()) dataContactSendToFTSelected = new cContactWrapper(coordinators[0].User__c,coordinators[0].User__r.Name,coordinators[0].User__r.Email,'user');
            }
            draft.Subject__c = 'FCQ completed for ' + vfpConfiguration.productionName + ' ' + (fcqBid.Freight__r.Start_Date__c != null ? Datetime.newInstance(fcqBid.Freight__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') +' Is this field the same as description from the trip details tab?';
            draft.Body__c = 'Please proof and reply at your earliest opportunity.';
        }
        /**
        *  @Conga: Update for Conga.
        */
        List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id, APXTConga4__Subject__c From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c = 'Freight - Email Confirmation'];
        congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        /**
        *  @/Conga
        */
    }
    public void changeContactDataSelected(){
        if(recordContactSelected != null && recordContactSelected != ''){
            if(chkContactSelected == null || chkContactSelected == 'production_contacts'){
                List<Contact> c = [SELECT Id, Name, FirstName, Email FROM Contact WHERE Id =: recordContactSelected];
                if(c.size() > 0){
                    dataContactSelected = new cContactWrapper(c[0].Id,c[0].Name,c[0].Email,'contact');
                    draft.Salutation__c = 'Hi ' + (String.isNotBlank(c[0].FirstName) ? c[0].FirstName : c[0].Name) + ',';
                } 
            }else{
                List<User> u = [SELECT Id, Name, FirstName, Email FROM User WHERE Id =: recordContactSelected];
                if(u.size() > 0){
                    dataContactSelected = new cContactWrapper(u[0].Id,u[0].Name,u[0].Email,'user');
                    draft.Salutation__c = 'Hi ' + (String.isNotBlank(u[0].FirstName) ? u[0].FirstName : u[0].Name) + ',';
                } 
            }
        }
    }
    public void searchContactData(){
        dataContactPL = new List<SelectOption>();
        dataContactPL.add(new SelectOption('','-- Select --'));
        String dataContactShow;
        if(chkContactSelected == null || chkContactSelected == 'production_contacts'){
            for(Production_Associations__c pa : [SELECT Id, Contact__c, Contact__r.Name, Contact__r.FirstName, Contact__r.LastName, Contact__r.Title, Contact__r.Email, Contact__r.Order__c FROM Production_Associations__c WHERE Production_Opp__c =: vfpConfiguration.productionId AND Contact__c <> null AND Contact__r.Email <> null AND Role__c includes ('Primary Freight','CC: Freight','Contract Signer') ORDER BY Contact__r.Order__c ASC]){
                dataContactShow = (pa.Contact__r.Order__c != null ? pa.Contact__r.Order__c + ' - ' : '') + pa.Contact__r.Name + ' - ' + pa.Contact__r.Email;
                dataContactPL.add(new SelectOption(pa.Contact__c,dataContactShow));
                if(isNew){
                    draft.Production_Assoc_Type__c = 'production_contacts';
                    if(pa.Contact__r.Order__c == 1 && (recordContactSelected == null || recordContactSelected == '')){
                        dataContactSelected = new cContactWrapper(pa.Contact__c,pa.Contact__r.Name,pa.Contact__r.Email,'contact');
                        draft.Salutation__c = 'Hi ' + (String.isNotBlank(pa.Contact__r.FirstName) ? pa.Contact__r.FirstName : pa.Contact__r.Name) + ',';
                    }else{
                        if(recordContactSelected == pa.Contact__c){
                            dataContactSelected = new cContactWrapper(pa.Contact__c,pa.Contact__r.Name,pa.Contact__r.Email,'contact');
                            draft.Salutation__c = 'Hi ' + (String.isNotBlank(pa.Contact__r.FirstName) ? pa.Contact__r.FirstName : pa.Contact__r.Name) + ',';
                        }
                    }
                }
                else{
                    if(recordContactSelected == pa.Contact__c) dataContactSelected = new cContactWrapper(pa.Contact__c,pa.Contact__r.Name,pa.Contact__r.Email,'contact');
                }
            }
        }else{
            for(Production_Associations__c pa : [SELECT Id, User__c, User__r.Name, User__r.FirstName, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: vfpConfiguration.productionId AND RecordType.DeveloperName = 'Production_Coordinators' AND Team_Roles__c includes ('Primary Freight Coordinator','Freight back-end Coordinator') AND User__c <> NULL ORDER BY User__r.Name ASC]){
                dataContactPL.add(new SelectOption(pa.User__c,pa.User__r.Name));
                if(isNew && recordContactSelected == pa.User__c){
                    draft.Production_Assoc_Type__c = 'ft_coordinators';
                    dataContactSelected = new cContactWrapper(pa.User__c,pa.User__r.Name,pa.User__r.Email,'user');
                    draft.Salutation__c = 'Hi ' + (String.isNotBlank(pa.User__r.FirstName) ? pa.User__r.FirstName : pa.User__r.Name) + ',';
                }
                else if(recordContactSelected == pa.User__c) dataContactSelected = new cContactWrapper(pa.User__c,pa.User__r.Name,pa.User__r.Email,'user');
            }
        }
    }
    public void changeContactDataSelectedFT(){
        if(recordContactSelected != null && recordContactSelected != ''){
            List<User> c = [SELECT Id, Name, Email FROM User WHERE Id =: recordContactSelected];
            if(c.size() > 0) dataContactSendToFTSelected = new cContactWrapper(c[0].Id,c[0].Name,c[0].Email,'user');
        }
    }
    public void saveEmailConfirmation(){
        if(fcqEmailType == 'Email Confirmation'){
            if(String.isNotEmpty(draft.Id)){
                draft.Body__c = bodyemail;
                draft.Production_Assoc_Type__c = chkContactSelected;
                draft.Production_Assoc_Contact_Id__c = recordContactSelected;
                update draft;
                draft = [SELECT Id, Name, Attention__c, Salutation__c, Production_Assoc_Type__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate FROM Draft__c WHERE Id =:draft.Id];
            }
        }
        /**
        *  @Conga: Update for Conga.
        */
        if(String.isNotBlank(congaEmailTemplateId)) update new APXTConga4__Conga_Email_Template__c(id = congaEmailTemplateId, APXTConga4__HTMLBody__c = (String.isNotBlank(draft.Salutation__c) ? draft.Salutation__c + '<br/><br/>' : '') + (String.isNotBlank(bodyemail) ? bodyemail.removeStartIgnoreCase('<p>').removeEndIgnoreCase('</p>') : '') + (String.isNotBlank(primaryCoordinatorName) ? '<br/>' + primaryCoordinatorName : '') + '<br/>Freight Coordinator');
    }
    public void deactivateEmailConfirmation(){
        if(fcqBid != null && fcqBid.Id != null){
            delete [SELECT Id FROM Draft__c WHERE Name =: fcqBid.Form_Email_Confirmation__c];
            update new Bid__c(Id = fcqBid.Id, Form_Email_Confirmation__c = null);
            fcqBid.Form_Email_Confirmation__c = null;
            draft = new Draft__c();
        }
    }
    //End EmailConfirmationSendtoFT Methods
    ///Attach FCQ Methods
    public void openAttachFcq(){
        fcqSubtripsMap = new Map<Freight__c, List<Freight__c>>();
        bidSubtripsMap = new Map<Id, Freight__c>();
        searchFreight = new Freight__c();
        isAttachFCQRendered = isFcqEmpty = true;
        isFcqSearched = false;  
    }
    public void searchAttachFcq(){
        if(searchFreight.Start_Date__c != null && searchFreight.End_Date__c != null){
            fcqSubtripsMap.clear();
            bidSubtripsMap.clear();
            for(Sub_Trip_FCQ__c subtripFcq:[Select FCQ_Details__r.Name, Freight_Sub_Trip_Details__r.id, Freight_Sub_Trip_Details__r.Description__c, Freight_Sub_Trip_Details__r.Bid_Sub_Trip__c, Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__c, Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Name, Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Description__c from Sub_Trip_FCQ__c where ((Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Start_Date__c >=:((Date) searchFreight.get('Start_Date__c')) and Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.Start_Date__c <=:((Date) searchFreight.get('End_Date__c'))) or (Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.End_Date__c >=:((Date) searchFreight.get('Start_Date__c')) and Freight_Sub_Trip_Details__r.Bid_Sub_Trip__r.Freight__r.End_Date__c <=:((Date) searchFreight.get('End_Date__c')))) and Freight_Sub_Trip_Details__r.Production__c =:fcqBid.Production__c order by FCQ_Details__r.Name, Freight_Sub_Trip_Details__r.Trip_Order__c]){
                if(fcqSubtripsMap.get(subtripFcq.FCQ_Details__r) == null) fcqSubtripsMap.put(subtripFcq.FCQ_Details__r, new List<Freight__c>{subtripFcq.Freight_Sub_Trip_Details__r});
                else fcqSubtripsMap.get(subtripFcq.FCQ_Details__r).add(subtripFcq.Freight_Sub_Trip_Details__r);
                bidSubtripsMap.put(subtripFcq.Freight_Sub_Trip_Details__r.id, subtripFcq.Freight_Sub_Trip_Details__r);
            } 
            for(Freight__c bidSubtrip:[Select id, (Select id, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c from FreightEquipments__r order by Line__c limit 1) from Freight__c where id in:bidSubtripsMap.keySet() order by Trip_Order__c]) bidSubtripsMap.put(bidSubtrip.id, bidSubtrip);
            isFcqEmpty = bidSubtripsMap.values().isEmpty();
            isFcqSearched = true;
        }
    }
    //End Attach FCQ Methods
    public class cContactWrapper{
        public String recordId {get;set;}
        public String name {get;set;}
        public String email {get;set;}
        public String typez {get;set;}
        public cContactWrapper(){
            this.recordId = '';
            this.name = '';
            this.email = '';
            this.typez = '';
        }
        public cContactWrapper(String vrecordId, String vname, String vemail, String vtypez){
            this.recordId = vrecordId;
            this.name = vname;
            this.email = vemail;
            this.typez = vtypez;
        }
    }
    public class SubTripfcqWrapper {
        public Id recordId {get;set;}
        public String name {get;set;}
        public SubTripfcqWrapper(Id recordId, String name) {
            this.recordId = recordId;
            this.name = name;
        }
    }
}
```


# Last Modified


# Usage

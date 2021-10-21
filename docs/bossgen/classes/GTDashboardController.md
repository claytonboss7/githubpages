---
layout: default
title: GTDashboardController
parent: classes
---
# Metadata Type
classes


# Filename 
GTDashboardController


# Raw XML
```
global class GTDashboardController {
    public String communityNoteCoordinator {get; set;}
    public DashboardConfigurationWrapper vfpConfiguration {get;set;}
    public Opportunity opportunity {get;set;}
    public String opportunityId {get;set;}
    public String tabDefault {get;set;}
    public String tabGroundDefault {get;set;}
    public String ground_vehicletypeRT {get;set;} 
    public String ground_salesGTDetailsRT {get;set;}
    public String ground_GTTripDetailsRT {get;set;}
    public String ground_GTSubStripDetailsRT {get;set;}
    public String ground_GTTravelDetailsRT {get;set;}
    public String itinerary_GTItineraryRT {get;set;}
    public String journal_tripJournalRT {get;set;}
    public String task_traceTaskRT {get;set;}
    public String bid_GTBidRT {get;set;}
    public String journal_bidjournalRT {get;set;}
    public List<SelectOption> ground_amenitiesPL {get;set;}
    public List<SelectOption> productionCompanyPL {get;set;}
    public List<SelectOption> productionContactPL {get;set;}
    public List<SelectOption> companyContactPL {get;set;}
    public List<SelectOption> teamMembers {get;set;}
    public String coordinatorGT {get;set;}
    public String coordinatorGTName {get;set;}
    public String backendcoordinatorGT {get;set;}
    public String messageCreateContact {get;set;}
    public String url {get;set;}
    public String dateToday {get;set;}
    public String grountypeJson {get;set;}
    public String concessionJson {get;set;}
    public String form_to {get;set;}
    public String form_cc {get;set;}
    public String form_bcc {get;set;}
    public String form_subject {get;set;}
    public String form_body {get;set;}
    public String form_date {get;set;}
    public String searchOption {get;set;}
    public String searchValue {get;set;}
    
    //Sales Tab
    public List<Ground__c> vehiclesByProductionList {get;set;}
    public Ground__c new_vehicle {get;set;}
    public String vehicleIdActual {get;set;}
    public String vehicle_vehicleref {get;set;}
    public String vehicle_vehicletype {get;set;}
    public Integer vehicle_capacity {get;set;}
    public String vehicle_make {get;set;}
    public String vehicle_model {get;set;}
    public String vehicle_year {get;set;}
    public String vehicle_amenities {get;set;}
    public String vehicle_otheramenities {get;set;}
    public String vehicle_luggage {get;set;}
    public List<Concessions__c> itemsByProductionList {get;set;}
    public Concessions__c new_item {get;set;}
    public String itemIdActual {get;set;}
    public String item_requested {get;set;}
    public String item_provided {get;set;}
    public Ground__c ground {get;set;}
    public static List<String> billingoptionsPL {get;set;}
    public String paymentInformation {get;set;}
    
    //GT Itinerary Tab
    public Itinerary__c itineraryFilter {get;set;}
    public Date itinerary_startdate {get;set;}
    public Date itinerary_enddate {get;set;}
    public String itinerary_city {get;set;}
    public String itinerary_vendor {get;set;}
    public String itinerary_status {get;set;}
    public Boolean itinerary_showprior {get;set;}
    public Boolean itinerary_showcontracted {get;set;}
    public Boolean itinerary_showcancelled {get;set;}
    public List<Itinerary__c> itineraryList {get;set;}
    //public List<Itinerary__c> tournamentList {get;set;}
    public Ground__c newtrip {get;set;}
    public Itinerary__c newitinerary {get;set;}
    public String newtrip_startcity {get;set;}
    public String newtrip_startcityid {get;set;}
    public String newtrip_grouptype {get;set;}
    public Boolean newtrip_clear {get;set;}
    public Journal__c newJournal {get;set;}
    public String createjournal_id {get;set;}
    public String createjournal_productioncompanyids {get;set;}
    public String createjournal_productioncontactids {get;set;}
    public String createjournal_companycontactids {get;set;}
    public String createjournal_coordinator {get;set;}
    public Boolean createjournal_alert {get;set;}
    public String createjournal_type {get;set;}
    public String createjournal_tracedate {get;set;}
    public Map<String,List<Ground__c>> vehiclesByTripMap {get;set;}
    public Map<String,List<Ground__c>> vehiclesByBidMap {get;set;}
    public String itineraryIdActual {get;set;}
    public String orderFieldTrip {get;set;}
    public String orderOrientationTrip {get;set;}
    public Boolean orderCheckTrip{get;set;}
    public Boolean orderChangeTrip {get;set;}
    public List<SelectOption> statusItineraryPL {get;set;} 
    public static List<String> groupTypePL {get;set;}
    public Map<String,List<Ground__c>> tripsItineraryMap {get;set;}
    public Map<String,List<Ground__c>> tripsItineraryBidMap {get;set;}
    public Map<String,Integer> tripsItineraryCountMap {get;set;}
    public Map<String,List<Ground__c>> travelsItineraryMap {get;set;}
    public Map<String,Integer> travelsItineraryCountMap {get;set;}
    public Map<String,Revenue__c> ratesByBidMap {get;set;}
    public Map<String,Bid__c> bidContractByGTMap {get;set;}
    public Boolean renderBid {get;set;}
    public String itinerarySummary_congaQueriesJson {get;set;}
    public String itinerarySummary_congaTemplateId {get;set;}
    
    //GT Trip Tab
    public Ground__c groundFilter {get;set;}
    public List<Ground__c> tripList {get;set;}
    public Date trip_startdate {get;set;}
    public Date trip_enddate {get;set;}
    public String trip_city {get;set;}
    public String trip_vendor {get;set;}
    public String trip_status {get;set;}
    public Boolean trip_showprior {get;set;}
    public Boolean trip_showcontracted {get;set;}
    public Boolean trip_showcancelled {get;set;}
    public String tripViewId {get;set;}
    public Ground__c tripView {get;set;}
    public String itineraryId {get;set;}
    public List<ContentDocument> documentTripList {get;set;}
    public String filename {get;set;}
    public transient String bodytrip {get;set;}
    public String documentRelationId {get;set;}
    public String documentIdActual {get;set;}
    public String emailMessage {get;set;}
    public String emailBody {get;set;}
    public String emailAttachs {get;set;}
    public String emailTo {get;set;}
    public String emailCC {get;set;}
    public String emailBCC {get;set;}
    public String emailSubject {get;set;}
    public String documentId {get;set;}
    public String documentTitle {get;set;}
    public String vendorsJson {get;set;}
    public List<Journal__c> journalByTripList {get;set;}
    public Map<String,List<Journal__c>> journalByTripMap {get;set;}
    public String tripJournalSearch {get;set;}
    public Boolean checkIssue {get;set;}
    public Boolean checkSales {get;set;}
    public String journalIdActual {get;set;}
    public String journalChildIdActual {get;set;}
    public Journal__c journalView {get;set;}
    public Journal__c journalChildView {get;set;}
    public String newJournalChildEntry {get;set;}
    public List<SelectOption> clientsByProduction {get;set;}
    public Contact clientByProduction {get;set;}
    public List<BidWrapper> bAuxWrapper {get;set;}
    public List<BidWrapper> bidsByTripShowList {get;set;}
    public Integer totalRecsBids {get;set;}
    public Integer OffsetSizeBids {get;set;}
    public Integer LimitSizeBids {get;set;}
    public String orderFieldBid {get;set;}
    public String orderOrientationBid {get;set;}
    public Boolean orderCheckBid{get;set;}
    public Boolean orderChangeBid {get;set;}
    public Boolean prevShowBid {get;set;}
    public Boolean nextShowBid {get;set;}
    public String bid_id {get;set;}
    public String bid_notes {get;set;}
    public Integer bid_option {get;set;}
    public Boolean refreshBidData {get;set;}
    public Integer tripBidNumber {get;set;}
    public String detailId {get;set;}
    public String searchVendor_CityGoogle {get;set;}
    public String searchvendor_type {get;set;}
    public String searchvendor_data1 {get;set;}
    public String searchvendor_value1 {get;set;}
    public String searchvendor_data2 {get;set;}
    public String searchvendor_value2 {get;set;}
    public String searchvendor_status {get;set;}
    public Set<String> vendorNotSelectedIds {get;set;}
    public List<Account> searchVendorList {get;set;}
    public String searchvendor_button {get;set;}
    public String searchvendor_vendor {get;set;}
    public String searchvendor_venue {get;set;}
    public String searchvendor_airportcode {get;set;}
    public String searchvendor_country {get;set;}
    public String searchvendor_address {get;set;}
    public String searchvendor_city {get;set;}
    public String searchvendor_state {get;set;}
    public String searchvendor_zip {get;set;}
    public String searchvendor_servicetype {get;set;}
    public String searchvendor_amenities {get;set;}
    public List<SelectOption> servicetypesPL {get;set;}
    public Account vendorFilter {get;set;}
    public String selectedVendors {get;set;}
    public String selectedTrips {get;set;}
    public Boolean bidSendBidFirstTime {get;set;}
    public Map<String,Bid__c> sendBidRequestMap {get;set;}
    public Integer sendBidRequestMapSize {get;set;}
    public Map<String,Boolean> sendBidRequestMapSelected {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendor_bidRequestMap {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendorParent_bidRequestMap {get;set;}
    public Map<String,List<SelectOption>> contactSelectOption_bidRequestMap {get;set;}
    public List<String> bidByTripIds {get;set;}
    public String vendoraccount_actual_id {get;set;}
    public String vendorcontact_actual_id {get;set;}
    public Contact vendorContact {get;set;}
    public String vendorContact_id {get;set;}
    public List<SelectOption> contact_DesignationTitlePL {get;set;}
    public String emailbid_body {get;set;}
    public String type_email {get;set;}
    public String dataids {get;set;}
    public List<SelectOption> contactsByProduction {get;set;} 
    public List<ContactWrapper> contactWrapperByProduction {get;set;} 
    public String sendOptions_primaryContactId {get;set;}
    public String sendOptions_congaEmailTemplateId {get;set;}
    public String sendOptions_congaEmailSubject {get;set;}
    public String sendOptions_congaTemplateId {get;set;}
    public String sendOptions_emailFromUserId {get;set;}
    public String sendOptions_congaEmailFromId {get;set;}
    public String sendOptions_congaQueriesJson {get;set;}
    public String sendBidRequest_accountIds {get;set;}
    public String sendBidRequest_congaEmailTemplateId {get;set;}
    public String sendBidRequest_congaEmailSubject {get;set;}
    public String sendBidRequest_congaTemplateId1 {get;set;}
    public String sendBidRequest_congaTemplateId2 {get;set;}
    public String sendBidRequest_emailFromUserId {get;set;}
    public String sendBidRequest_congaEmailFromId {get;set;}
    public Map<String,Bid__c> sendBidRequestMapRelease {get;set;}
    public Integer sendBidRequestMapReleaseSize {get;set;}
    public Map<String,Boolean> sendBidRequestMapReleaseSelected {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendor_releaseMap {get;set;}
    public Map<String,List<ContactWrapper>> contactsByVendorParent_releaseMap {get;set;}
    public Map<String,List<SelectOption>> contactSelectOption_releaseMap {get;set;}
    public Concessions__c newConcessionTrip {get;set;}
    public List<Concessions__c> concessionsRequestedTrip {get;set;}
    public String concessionActual {get;set;}
    public String concessionRequestedActual {get;set;}
    public String concessionNoteActual {get;set;}
    public Boolean concessionCreateInBid {get;set;}
    public List<SelectOption> concessions_concessionTypePL {get;set;}
    public Ground__c newVehicleTrip {get;set;}
    public List<Ground__c> vehiclesByTripList {get;set;}
    public List<Ground__c> subTripList {get;set;}
    public String subtripIdActual {get;set;}
    public String subtripFreight {get;set;}
    public Map<String,List<Ground__c>> travelsBySubTripMap {get;set;}
    public Map<String,Boolean> hasFreightMap {get;set;}
    public Ground__c newTravel {get;set;}
    public String travelActualId {get;set;}
    public String travelActualOrder {get;set;}
    public String newtravel_subtripid {get;set;}
    public String newtravel_line {get;set;}
    public String newtravel_vehicle {get;set;}
    public String newtravel_vehicleid {get;set;}
    public Date newtravel_startdate {get;set;}
    public String newtravel_starttime {get;set;}
    public Date newtravel_enddate {get;set;}
    public String newtravel_endtime {get;set;}
    public String newtravel_traveltype {get;set;}
    public String newtravel_grouptype {get;set;}
    public String newtravel_locationpickuptype {get;set;}
    public String newtravel_locationpickupdetails {get;set;}
    public String newtravel_locationdropofftype {get;set;}
    public String newtravel_locationdropoffdetails {get;set;}
    public String newtravel_notes {get;set;}
    public Boolean newtravel_updatemaster {get;set;}
    public String searchlocation_type {get;set;}
    public String searchlocation_value1 {get;set;}
    public String searchlocation_value2 {get;set;}
    public String searchlocation_value3 {get;set;}
    public List<wrapperLocation> searchLocationList {get;set;}
    public List<wrapperLocation> searchLocationRelatedList {get;set;}
    public Boolean searchlocation_open {get;set;}
    public Date tripview_tracedate {get;set;}
    public Map<Integer,BidWrapper> bidDataMap {get;set;}
    public GTDashboard gtDashboard {get;set;}
    public Integer bidsCreated {get;set;}
    public String contactPrimarySelected {get;set;}
    public String contractingBidId {get;set;}
    public String contractingParentId {get;set;}
    public String prod_assoc_CoordinatorsRT {get;set;}
    public String prod_assoc_ContactsRT {get;set;}
    public String tripview_status {get;set;}
    public String dataBidIdsearch {get;set;}
    public String releaseEmailBid_body {get;set;}
    public String emailbid_to {get;set;}
    public String emailbid_cc {get;set;}
    public String emailbid_bcc {get;set;}
    public String emailbid_subject {get;set;}
    public String emailbid_id {get;set;}
    public String emailbid_primarycontactname {get;set;}
    public Integer tripview_option {get;set;}
    public String airlineInfoJson {get;set;}
    public String grouptypeJson {get;set;}
    public List<SelectOption> vendorType2PL {get;set;}
    public List<SelectOption> officeLocationPL {get;set;}
    public List<SelectOption> commissionTypePL {get;set;}
    public String messageCreateAccount {get;set;}
    public String newVendor_id {get;set;}
    public String newVendor_name {get;set;}
    public String newVendor_vendorType {get;set;}
    public String newVendor_address1 {get;set;}
    public String newVendor_city {get;set;}
    public String newVendor_zip {get;set;}
    public String newVendor_officeLocation {get;set;}
    public String newVendor_commissionType {get;set;}
    public Boolean isProdJournalsRendered {get;set;}
    public String makeJson {get;set;}
    public String modelJson {get;set;}
    public Map<String,String> symbolMap {get;set;}
    private Map<String, APXTConga4__Conga_Merge_Query__c> congaQueriesMap;
    public String congaQueriesJson {get;set;}
    public String communityURLvalue {get;set;}//CS - victor
    public Boolean isBidRequestRendered {get;set;}
    public Boolean isBidResendRendered {get;set;}
    
    //Pagination Vendor
    public Integer limitVendor {get;set;}
    public Integer offsetVendor {get;set;}
    public String searchTypeVendor {get;set;}
    public Integer totalPagesVendor {get;set;}
    public Boolean orderCheckVendor {get;set;}
    public Boolean orderChangeVendor {get;set;}
    public String orderOrientationVendor {get;set;}
    public String orderFieldVendor {get;set;}
    public Id firstIdVendor {get;set;}
    public Id lastIdVendor {get;set;}
    public Object firstValueOfSortedFieldVendor {get;set;}
    public Object lastValueOfSortedFieldVendor {get;set;}
    
    //Pagination Itinerary
    public Integer limitItinerary {get;set;}
    public Integer offsetItinerary {get;set;}
    public String searchTypeItinerary {get;set;}
    public Integer totalPagesItinerary {get;set;}
    public Boolean orderCheckItinerary {get;set;}
    public Boolean orderChangeItinerary {get;set;}
    public String orderOrientationItinerary {get;set;}
    public String orderFieldItinerary {get;set;}
    public Id firstIdItinerary {get;set;}
    public Id lastIdItinerary {get;set;}
    public Object firstValueOfSortedFieldItinerary {get;set;}
    public Object lastValueOfSortedFieldItinerary {get;set;}
    
    //Pagination
    public Integer limitTrip {get;set;}
    public Integer offsetTrip {get;set;}
    public String searchTypeTrip {get;set;}
    public Integer totalPagesTrip {get;set;}
    public Id firstId {get;set;}
    public Id lastId {get;set;}
    public Object firstValueOfSortedField {get;set;}
    public Object lastValueOfSortedField {get;set;}
    
    public GTDashboardController(ApexPages.StandardController standardController) {
        vfpConfiguration = new DashboardConfigurationWrapper();
        Opportunity opp = (Opportunity) standardController.getRecord();
        Init();
        if(opp != null && opp.Id != null){
            opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Office_Location__c FROM Opportunity WHERE Id=:opp.Id];
            opportunityId = opportunity.Id;
            //getDataProduction();
        }
    }
    
    public GTDashboardController() {
        Init();
    }
    
    public void Init() {
        limitVendor = 20;
        limitTrip = 20;
        limitItinerary = 20;
        isBidRequestRendered = false;
        isBidResendRendered = false;
        isProdJournalsRendered = false;
        renderBid = false;
        tabDefault = 'sales';
        tabGroundDefault = 'trip_bids';
        Schema.DescribeFieldResult fieldResult;
        List<Schema.PicklistEntry> ple;
        dateToday = String.valueOf(Datetime.now().format('MM/dd/yyyy'));
        
        List<wrapperSearchPL> groupList = new List<wrapperSearchPL>();
        for(SelectOption so : PickThePicklist('Ground__c','Group_Type__c')){
            groupList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        grountypeJson = JSON.serialize(groupList);
        
        List<wrapperSearchPL> airlineInfoList = new List<wrapperSearchPL>();
        for(SelectOption so : PickThePicklist('Ground__c','Airline_Info_Special_Notes__c')){
            airlineInfoList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        airlineInfoJson = JSON.serialize(airlineInfoList);
        
        List<wrapperSearchPL> grouptypeList = new List<wrapperSearchPL>();
        for(SelectOption so : PickThePicklist('Ground__c','Group_Type__c')){
            grouptypeList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        grouptypeJson = JSON.serialize(grouptypeList);

        List<wrapperSearchPL> modelList = new List<wrapperSearchPL>();
        for(SelectOption so : PickThePicklist('Ground__c','Model__c')){
            modelList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        modelJson = JSON.serialize(modelList);
        
        List<wrapperSearchPL> makeList = new List<wrapperSearchPL>();
        for(SelectOption so : PickThePicklist('Ground__c','Make__c')){
            makeList.add(new wrapperSearchPL(so.getValue(),so.getValue()));
        }
        makeJson = JSON.serialize(makeList);

        task_traceTaskRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Task' and Name = 'Trace Task'].Id;
        ground_vehicletypeRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Ground__c' and Name = 'Vehicle Type'].Id;
        ground_salesGTDetailsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Ground__c' and DeveloperName = 'Sales_GT_Details'].Id;
        ground_GTTripDetailsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Ground__c' and Name = 'GT Trip Details'].Id;
        itinerary_GTItineraryRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Itinerary__c' and Name = 'GT Itinerary'].Id;
        journal_tripJournalRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Journal__c' and Name = 'Trip Journal'].Id;
        bid_GTBidRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Bid__c' and Name = 'GT Bid'].Id;
        journal_bidjournalRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Journal__c' and Name = 'Bid Journal'].Id;
        ground_GTSubStripDetailsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Ground__c' and Name = 'GT Sub Trip Details'].Id;
    	ground_GTTravelDetailsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Ground__c' and Name = 'GT Travel Details'].Id;
        prod_assoc_CoordinatorsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Production_Associations__c' and DeveloperName = 'Production_Coordinators'].Id;
        prod_assoc_ContactsRT = [SELECT Id FROM RecordType WHERE sObjectType = 'Production_Associations__c' and DeveloperName = 'Production_Contacts'].Id;
        
        productionCompanyPL = new List<SelectOption>();
        productionContactPL = new List<SelectOption>();
        companyContactPL = new List<SelectOption>();
        teamMembers = new List<SelectOption>();
        url = ApexPages.currentPage().getHeaders().get('Host');
        dataBidIdsearch = null;
        
        //Sales
        ground_amenitiesPL = new List<SelectOption>();
        fieldResult = Ground__c.Amenities__c.getDescribe();
        ple = fieldResult.getPicklistValues();
        for( Schema.PicklistEntry pickListVal : ple){
            ground_amenitiesPL.add(new SelectOption(pickListVal.getValue(),pickListVal.getLabel()));
        }
        
        vehiclesByProductionList = new List<Ground__c>();
        new_vehicle = new Ground__c();
        itemsByProductionList = new List<Concessions__c>();
        new_item = new Concessions__c(Concession_Type__c='GT');
        ground = new Ground__c();
        
        billingoptionsPL = new List<String>();
        for(SelectOption so : PickThePicklist('Ground__c','Billing_Options__c')){
            billingoptionsPL.add(so.getValue());
        }
        //paymentInformation = '';

        //Itinerary
        orderFieldItinerary = 'Start_Date__c';
        orderOrientationItinerary = 'ASC';
        orderCheckItinerary = false;
        orderChangeItinerary = false;
        itineraryFilter = new Itinerary__c();
        itinerary_showcontracted = false;
        itinerary_showcancelled = false;
        itinerary_showprior = false;
        newtrip_clear = false;
        newJournal = new Journal__c();
        vehiclesByTripMap = new Map<String,List<Ground__c>>();
        vehiclesByBidMap = new Map<String,List<Ground__c>>();
        statusItineraryPL = new List<SelectOption>();
        statusItineraryPL.add(new SelectOption('','-- Select --'));
        statusItineraryPL.add(new SelectOption('Itinerary Received','Itinerary Received'));
        statusItineraryPL.add(new SelectOption('Bid Request Stage','Bid Request Stage'));
        statusItineraryPL.add(new SelectOption('Presenter/Promoter Provided','Presenter/Promoter Provided'));
        statusItineraryPL.add(new SelectOption('Pending Client Choice','Pending Client Choice'));
        statusItineraryPL.add(new SelectOption('Budgeting','Budgeting'));
        statusItineraryPL.add(new SelectOption('Cancelled','Cancelled'));
        statusItineraryPL.add(new SelectOption('Contracted on Own','Contracted on Own'));
        statusItineraryPL.add(new SelectOption('Layoff','Layoff'));
        statusItineraryPL.add(new SelectOption('Pending Trip Information','Pending Trip Information'));
        statusItineraryPL.add(new SelectOption('Pending Airport Confirmation','Pending Airport Confirmation'));
        statusItineraryPL.add(new SelectOption('Send to Client','Send to Client'));
        
        tripsItineraryMap = new Map<String,List<Ground__c>>();
        tripsItineraryBidMap = new Map<String,List<Ground__c>>();
        travelsItineraryMap = new Map<String,List<Ground__c>>();
        tripsItineraryCountMap = new Map<String,Integer>();
        travelsItineraryCountMap = new Map<String,Integer>();
        bidContractByGTMap = new Map<String,Bid__c>();
        
        //Trip
        groundFilter = new Ground__c();
        tripList = new List<Ground__c>();
        trip_showcontracted = false;
        trip_showcancelled = false;
        trip_showprior = false;
        //TripWrapper.orderFieldTrip = 'start_date';
        //TripWrapper.orderOrientationTrip = 'ASC';
        orderFieldTrip = 'Start_Date__c';
        orderOrientationTrip = 'ASC';
        orderCheckTrip = false;
        orderChangeTrip = false;
        documentTripList = new List<ContentDocument>();
        documentIdActual = null;
        vendorsJson = '[]';
        journalByTripList = new List<Journal__c>();
        journalByTripMap = new Map<String,List<Journal__c>>();
        checkIssue = false;
        checkSales = false;
        journalView = new Journal__c();
        journalChildView = new Journal__c();
        clientsByProduction = new List<SelectOption>();
        clientByProduction = new Contact();
        totalRecsBids = 0;
        BidWrapper.orderFieldBid = 'initial';
        BidWrapper.orderOrientationBid = 'ASC';
        orderFieldBid = 'initial';
        orderOrientationBid = 'ASC';
        orderCheckBid = false;
        orderChangeBid = false;
        OffsetSizeBids = 0;
    	LimitSizeBids = 5;
        prevShowBid = false;
        nextShowBid = false;
        tripBidNumber = null;
        refreshBidData = true;
        detailId = null;
        searchVendor_CityGoogle = null;
        vendorNotSelectedIds = new Set<String>();
        //VendorWrapper.orderFieldVendor = 'Name';
        //VendorWrapper.orderOrientationVendor = 'ASC';
        orderFieldVendor = 'Name';
        orderOrientationVendor = 'ASC';
        orderCheckVendor = false;
        orderChangeVendor = false;
        servicetypesPL = new List<SelectOption>();
        servicetypesPL.addAll(PickThePicklist('Account','Service_Types__c'));
        vendorFilter = new Account();
        bidSendBidFirstTime = true;
        contact_DesignationTitlePL = new List<SelectOption>();
        contact_DesignationTitlePL.add(new SelectOption('',''));
        contact_DesignationTitlePL.addAll(PickThePicklist('Contact','Designation_title__c'));
        vendorContact = new Contact();
        emailBid_body = null;
        newConcessionTrip = new Concessions__c();
        concessionsRequestedTrip = new List<Concessions__c>();
        List<wrapperSearchPL> consValueList = new List<wrapperSearchPL>();
        Map<Object,List<String>> dependValuesByControlValue = getDependentPicklistValues(Concessions__c.Concessions_Requested__c);
        concessions_concessionTypePL = new List<SelectOption>();
        for(Object k1 : dependValuesByControlValue.keySet()){
            if((String) k1 == 'GT'){
                for(String k2: dependValuesByControlValue.get(k1)){
                    concessions_concessionTypePL.add(new SelectOption(k2,k2));
                    consValueList.add(new wrapperSearchPL(k2,k2));
                }
            }
        }
        concessionJson = JSON.serialize(consValueList);
 
        newVehicleTrip = new Ground__c();
        vehiclesByTripList = new List<Ground__c>();
        subTripList = new List<Ground__c>();
        travelsBySubTripMap = new Map<String,List<Ground__c>>();
        hasFreightMap = new Map<String,Boolean>();
        newTravel = new Ground__c();
        searchLocationList = new List<wrapperLocation>();
        searchLocationRelatedList = new List<wrapperLocation>();
        searchlocation_open = false;
        bidsCreated = 0;
        
        vendorType2PL = new List<SelectOption>();
        vendorType2PL.addAll(PickThePicklist('Account','GT_Vendor_Type__c'));
        officeLocationPL = new List<SelectOption>();
        officeLocationPL.addAll(PickThePicklist('Account','Office_Location__c'));
        commissionTypePL = new List<SelectOption>();
        commissionTypePL.addAll(PickThePicklist('Account','Commission_Type__c'));

        //Contracting
        gtDashboard = new GTDashboard();
        
        //CS - victor
        Community_Settings__c comSetCS = Community_Settings__c.getInstance();
        communityURLvalue = comSetCS.Community_URL__c;
    }
    
    public void createNewVendor(){
        messageCreateAccount = '';
        try{
            Account a = new Account(
                RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Ground_Travel_Vendor').getRecordTypeId(),
                Name = newVendor_name,
                GT_Vendor_Type__c = newVendor_vendorType,
                ShippingStreet = newVendor_address1,
                City__c = newVendor_city,
                ShippingPostalCode = newVendor_zip,
                Office_Location__c = newVendor_officeLocation,
                Commission_Type__c = newVendor_commissionType
            );
            insert a;
            newVendor_id = a.Id;
            searchvendor_value1 = newVendor_name;
            searchvendor_button = 'main';
            searchvendor_data1 = 'vendor';
            searchvendor_value2 = '';
            searchvendor_status = 'All';
            searchVendor();
        }catch(DMLException e){
            messageCreateAccount = validateError(e.getMessage());
        }
    }
    
    public void sendBidRequestLink(){
        if(dataids != null && dataids.trim() != ''){
            Set<String> vendorContactIds = new Set<String>();
            for(String d : dataids.split(',')){
                vendorContactIds.add(sendBidRequestMap.get(d).Vendor_Contact__c);
            }
            
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id IN: vendorContactIds]) contactMap.put(c.Id,c);
            
            //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email, User__r.Phone FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            User userActual = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripViewId);
            String owaeId = userActual != null && userActual.Email != null ? verifyWideAddress(userActual.Email) : null;
            
            Journal__c journalAux;
            Bid__c bAux;
            List<Journal__c> journalAuxList = new List<Journal__c>();
            Map<String,Bid__c> bidUpdateMap = new Map<String,Bid__c>();
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail;
            String[] toAddresses;
            Set<String> ccAddresses;
            String body = ''; 
            List<EmailTemplate> templateLink = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate WHERE DeveloperName ='GT_Bid_Request_Link_All'];
            String subject = '';
            
            Ground__c gAux = new Ground__c(Id=tripViewId);
            
            for(String d : dataids.split(',')){
                //New Journals
                journalAux = new Journal__c(
                    RecordTypeId = journal_bidjournalRT,
                    Bid__c = sendBidRequestMap.get(d).Id,
                    Journal_Entry__c = 'Ground Travel Bid Request Link has been sent to ' + contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Name + ' at ' + contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email
                );
                journalAuxList.add(journalAux);
                
                //Bid update
                if(sendBidRequestMap.get(d) != null && sendBidRequestMap.get(d).Status__c != 'Contracted'){
                    bAux = new Bid__c(Id=sendBidRequestMap.get(d).Id,Status__c='Sent');
                    bidUpdateMap.put(bAux.Id,bAux);
                }
                
                //EMAIL
                ccAddresses = new Set<String>();
                for(ContactWrapper cw : contactsByVendor_bidRequestMap.get(d)){
                    if(!cw.disabled && cw.selected){
                        ccAddresses.add(cw.c.Email);
                    } 
                }
                
                if(sendBidRequestMap.get(d).Vendor__r.ParentId != null){
                    for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(sendBidRequestMap.get(d).Vendor__r.ParentId)){
                        if(!cw.disabled && cw.selected){
                            ccAddresses.add(cw.c.Email);
                        } 
                    }
                }
                
                mail = new Messaging.SingleEmailMessage();
                if(owaeId != null && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(owaeId);
                toAddresses = new String[] {contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email};
                    mail.setToAddresses(toAddresses);
                if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));                
                subject = (templateLink.size() > 0 ? templateLink[0].Subject.replace('{ProductionName}',sendBidRequestMap.get(d).Production__r.Name)
                           .replace('{StartDate}',(sendBidRequestMap.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.Start_Date__c.year(),sendBidRequestMap.get(d).GT__r.Start_Date__c.month(),sendBidRequestMap.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                           .replace('{EndDate}',(sendBidRequestMap.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.End_Date__c.year(),sendBidRequestMap.get(d).GT__r.End_Date__c.month(),sendBidRequestMap.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                           .replace('{BidNumber}',sendBidRequestMap.get(d).Name)
                           : '');
                
                body = (templateLink.size() > 0 ? templateLink[0].HtmlValue.replace('{GroundTravelCoordinator}',userActual != null && userActual.Name != '' ? userActual.Name : '')
                        .replace('{ContactName}',sendBidRequestMap.get(d).Vendor_Contact__c != null && contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c) != null ? contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Name : '')
                        .replace('{VendorURL}',sendBidRequestMap.get(d).Vendor__c != null ? sendBidRequestMap.get(d).Vendor__r.Name : '')
                        //.replace('{VendorURL}','<a href="https://ccdev-roadrebel.cs42.force.com/" target="_blank">' + sendBidRequestMap.get(d).Vendor__r.Name + '</a>')
                        //.replace('{VendorURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Vendor__c + '" target="_blank">' + sendBidRequestMap.get(d).Vendor__r.Name + '</a>')
                        .replace('{BidURL}','<a href="'+ (communityURLvalue != null ? communityURLvalue + '/s/?service=ground&record=' + sendBidRequestMap.get(d).Id : '') +'" target="_blank">'+ (communityURLvalue != null ? communityURLvalue + '/s/?service=ground&record=' + sendBidRequestMap.get(d).Id : '') + '</a>')
                        //.replace('{BidURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Id + '" target="_blank">http://' + url + '/' + sendBidRequestMap.get(d).Id + '</a>')
                        .replace('{CoordinatorPhone}',userActual != null && userActual.Phone != null ? userActual.Phone : '')
                        : '');
                
                gAux.Email_Body_Bid_Request_Link__c = null;
                mail.setSubject(subject);
                mail.setHtmlBody(body);
                myEmails.add(mail);
            }    
            
            insert journalAuxList;
            
            update bidUpdateMap.values();
            
            if(tripViewId != null && (tripView.Status_Ground__c != 'Contracted' || tripView.Status_Ground__c != 'In Contracting')){
                gAux.Status_Ground__c = 'Bid Request Stage';
                tripView.Status_Ground__c = 'Bid Request Stage';
                List<Itinerary__c> itineraryAuxList =  [SELECT Id FROM Itinerary__c WHERE GT__c =: tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
                if(itineraryAuxList.size() > 0) update new Itinerary__c(Id=itineraryAuxList[0].Id,Status__c='Bid Request Stage');
                searchTrip();
            }
            tripView.Bid_Request__c = system.today();
            gAux.Bid_Request__c = system.today();
            update gAux;
            
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
            isBidRequestRendered = false;
            //viewTripDetail();
        }
    }
    
    public void saveStatusTrip(){
        if(tripViewId != null && tripViewId != ''){
            Ground__c gAux = new Ground__c(Id = tripViewId,Status_Ground__c = tripview_status);
            update gAux;
            tripView.Status_Ground__c = tripview_status;
            searchTrip();
        }
    }
    
    public void saveBackEndCoordinator(){
        if(tripView != null && tripView.Id != null){
            tripView.Back_end_Coordinator__c = backendcoordinatorGT != null && backendcoordinatorGT != '' ? backendcoordinatorGT : null;
            update tripView;
        }
    }
    
    public void viewContractingDetailByItinerary(){
        if(vfpConfiguration != null){
            vfpConfiguration.bidId = contractingBidId;
            vfpConfiguration.parentId = contractingParentId;
            vfpConfiguration.productionId = opportunityId;
            vfpConfiguration.parentSObject = 'Ground';
        }
    }
    
    public void changeClientTrip(){
        if(contactPrimarySelected != null && contactPrimarySelected != ''){
            clientByProduction = [SELECT Id, FirstName, Name, Phone, Email, Title, MobilePhone FROM Contact WHERE Id =: contactPrimarySelected LIMIT 1];
            List<Production_Associations__c> paList = [SELECT Id, Contact__c, Role__c, Production_Opp__c FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId AND Contact__c <> NULL AND RecordType.DeveloperName = 'Production_Contacts'];
            system.debug(paList);
            if(paList.size() > 0){
                String roles;
                for(Production_Associations__c pAssoc : paList){
                    if(contactPrimarySelected != null && contactPrimarySelected != '' && pAssoc.Contact__c == contactPrimarySelected && pAssoc.Role__c != null){
                        if(pAssoc.Role__c != null && !pAssoc.Role__c.contains('Primary GT')){
                            pAssoc.Role__c = pAssoc.Role__c + ';Primary GT;';
                        }else{
                            if(pAssoc.Role__c == null) pAssoc.Role__c = 'Primary GT;';
                        }
                    }else{
                        roles = '';
                        if(pAssoc.Role__c != null){
                            for(String tr : pAssoc.Role__c.split(';')){
                                if(tr != 'Primary GT') roles = roles + tr + ';';
                            }
                        }
                        pAssoc.Role__c = roles;
                    }
                }
                system.debug(paList);
                update paList;
            }else{
                insert new Production_Associations__c(RecordTypeId = prod_assoc_ContactsRT, Production_Opp__c = opportunityId,Role__c = 'Primary GT;', Contact__c = contactPrimarySelected);
            }
        }
    }
    
    public void saveOtherInformation(){
        /*//Trace
        if(tripView.Id != null && tripview_tracedate != null && coordinatorGT != null && tripView.Status_Ground__c != null){
            system.debug('# valid for trace...');
            Date actualTraceDate = [SELECT Trace_Date__c FROM Ground__c WHERE Id =:tripView.Id].Trace_Date__c;
            if(actualTraceDate != tripview_tracedate){
                system.debug('# creating trace...');
                Id recordTypeTT = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName().get('Trace_Task').getRecordTypeId();
                insert new Task(
                    recordTypeId = recordTypeTT,
                    WhatId=tripView.Id,
                    ActivityDate=tripview_tracedate,
                    Deadline_Date__c=tripView.Deadline_Date__c != null ? tripView.Deadline_Date__c : null,
                    OwnerId=coordinatorGT,
                    Subject=tripView.Status_Ground__c,
                    Task_Type__c='Ground Status Trace'
                );
            }
        }*/
        
        if(tripViewId != null && tripViewId != ''){
            update new Ground__c(Id=tripViewId,Trace_Date__c=tripview_tracedate);
        }
    }
    
    public void searchLocation(){
        String strQuery;
        String nameAux;
        searchLocationList = new List<wrapperLocation>();
        searchLocationRelatedList = new List<wrapperLocation>();
        if(searchlocation_open){
            Map<String,Bid__c> bidAuxMap = new Map<String,Bid__c>();
            Date StartDate = tripView.Start_Date__c;
            Date EndDate = tripView.End_Date__c;
            if(searchlocation_type == 'hotel'){
                strQuery = 'SELECT Id, Vendor__c, Vendor__r.Name, Vendor__r.ShippingStreet, Vendor__r.City__c, Vendor__r.City__r.Name, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode FROM Bid__c' +
                    ' WHERE Vendor__c <> NULL AND Status__c = \'Contracted\' AND RecordType.Name IN (\'Housing Bid\') AND Production__c =: opportunityId' + 
                    ' AND ((Housing__r.Date_In__c <=: StartDate AND Housing__r.Date_Out__c >=: StartDate) OR (Housing__r.Date_In__c <=: EndDate AND Housing__r.Date_Out__c >=: EndDate))';
                for(Bid__c b : Database.query(strQuery)) bidAuxMap.put(b.Vendor__c,b);            
                for(Bid__c b : bidAuxMap.values()){
                    searchLocationRelatedList.add(
                        new wrapperLocation(
                            b.Vendor__r.Name,
                            b.Vendor__r.ShippingStreet,
                            b.Vendor__r.City__r.Name,
                            b.Vendor__r.ShippingState,
                            b.Vendor__r.ShippingPostalCode,
                            ''
                        )
                    );
                }
            }else if(searchlocation_type == 'venue'){
                strQuery = 'SELECT Id, Venue__c, Venue__r.Vendor_ID__c, Venue__r.Name, Venue__r.ShippingStreet, Venue__r.City__c, Venue__r.City__r.Name, Venue__r.ShippingState, Venue__r.ShippingPostalCode FROM Bid__c' +
                    ' WHERE Venue__c <> NULL AND Status__c = \'Contracted\' AND RecordType.Name IN (\'Housing Bid\') AND Production__c =: opportunityId' + 
                    ' AND ((Housing__r.Date_In__c <=: StartDate AND Housing__r.Date_Out__c >=: StartDate) OR (Housing__r.Date_In__c <=: EndDate AND Housing__r.Date_Out__c >=: EndDate))';
                for(Bid__c b : Database.query(strQuery)) bidAuxMap.put(b.Venue__c,b);            
                for(Bid__c b : bidAuxMap.values()){
                    searchLocationRelatedList.add(
                        new wrapperLocation(
                            b.Venue__r.Vendor_ID__c,
                            b.Venue__r.Name,
                            b.Venue__r.ShippingStreet,
                            b.Venue__r.City__r.Name,
                            b.Venue__r.ShippingState,
                            b.Venue__r.ShippingPostalCode
                        )
                    );
                }
            }
        }
        
        if(!searchlocation_open){
            if(searchlocation_type == 'airport'){
                searchlocation_value1 = '%' + searchlocation_value1 + '%';
                strQuery = 'SELECT Id, Airport_Code__c, Name, City__c, City__r.Name FROM Airport__c WHERE Name LIKE: searchlocation_value1 OR Airport_Code__c LIKE: searchlocation_value1 OR City__r.Name LIKE: searchlocation_value1';
                strQuery += ' LIMIT 100';
                for(Airport__c a : Database.query(strQuery)){
                    nameAux = (a.Airport_Code__c != null ? a.Airport_Code__c + ' - ' : '') + a.Name + (a.City__c != null ? ' - ' + a.City__r.Name : '');
                    searchLocationList.add(
                        new wrapperLocation(
                            nameAux,
                            '',
                            '',
                            '',
                            '',
                            ''
                        )
                    );
                }
            }else if(searchlocation_type == 'hotel'){
                strQuery = 'SELECT Id, Vendor__c, Vendor__r.Name, Vendor__r.ShippingStreet, Vendor__r.City__c, Vendor__r.City__r.Name, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode FROM Bid__c' +
                    ' WHERE Vendor__c <> NULL AND Status__c = \'Contracted\' AND RecordType.Name IN (\'Housing Bid\') AND Production__c =: opportunityId';
                system.debug(strQuery);
                for(Bid__c b : Database.query(strQuery)){
                    searchLocationRelatedList.add(
                        new wrapperLocation(
                            b.Vendor__r.Name,
                            b.Vendor__r.ShippingStreet,
                            b.Vendor__r.City__r.Name,
                            b.Vendor__r.ShippingState,
                            b.Vendor__r.ShippingPostalCode,
                            ''
                        )
                    );
                }
                
                strQuery = 'SELECT Id, Name, ShippingStreet, City__r.Name FROM Account' +
                    ' WHERE RecordType.Name IN (\'Hotel Vendor\',\'Corporate Housing Vendor\')';
                if(searchlocation_value1 != null && searchlocation_value1 != ''){
                    searchlocation_value1 = '%' + searchlocation_value1 + '%';
                    strQuery += ' AND City__r.Name LIKE: searchlocation_value1';
                }
                if(searchlocation_value2 != null && searchlocation_value2 != ''){
                    searchlocation_value2 = '%' + searchlocation_value2 + '%';
                    strQuery += ' AND Name LIKE: searchlocation_value2';
                }
                if(searchlocation_value3 != null && searchlocation_value3 != ''){
                    searchlocation_value3 = '%' + searchlocation_value3 + '%';
                    strQuery += ' AND ShippingStreet LIKE: searchlocation_value3';
                }
                strQuery += ' ORDER BY Name ASC LIMIT 100';
                for(Account a : Database.query(strQuery)){
                    searchLocationList.add(
                        new wrapperLocation(
                            a.Name,
                            a.ShippingStreet,
                            a.City__r.Name,
                            '',
                            '',
                            ''
                        )
                    );
                }
            }else if(searchlocation_type == 'venue'){
                strQuery = 'SELECT Id, Vendor_ID__c, Name, ShippingStreet, City__r.Name FROM Account' +
                    ' WHERE RecordType.Name IN (\'Venue\')';
                if(searchlocation_value1 != null && searchlocation_value1 != ''){
                    searchlocation_value1 = '%' + searchlocation_value1 + '%';
                    strQuery += ' AND Name LIKE: searchlocation_value1';
                }
                if(searchlocation_value2 != null && searchlocation_value2 != ''){
                    searchlocation_value2 = '%' + searchlocation_value2 + '%';
                    strQuery += ' AND City__r.Name LIKE: searchlocation_value2';
                }
                strQuery += ' ORDER BY Name ASC LIMIT 100';
                for(Account a : Database.query(strQuery)){
                    searchLocationList.add(
                        new wrapperLocation(
                            a.Vendor_ID__c,
                            a.Name,
                            a.ShippingStreet,
                            a.City__r.Name,
                            '',
                            ''
                        )
                    );
                }
            }
        }
    }
    
    public void deleteTravel(){
        if(travelActualId != null && travelActualId != ''){
            delete [SELECT Id FROM Ground__c WHERE Id =: travelActualId];
            refreshSubtripsDataBids(tripViewid);
            searchItinerary();
            getSubStripByTrip();
        }
    }
    
    public void saveTravel(){
        Ground__c travel = new Ground__c(
            Id = travelActualId != null && travelActualId != '' ? travelActualId : null,
            RecordTypeId = ground_GTTravelDetailsRT,
            Line__c = newtravel_line != null && newtravel_line != '' ? Decimal.valueOf(newtravel_line) : null,
            Vehicle_Ref__c = newtravel_vehicle,
            Vehicle_Lookup__c = newtravel_vehicleid != null && newtravel_vehicleid != '' ? newtravel_vehicleid : null,
            Start_Date__c = newtravel_startdate != null ? newtravel_startdate : null,
            Start_Date_Time__c = newtravel_starttime != null && newtravel_starttime != '' ? Time.newInstance(Integer.valueOf(newtravel_starttime.split(':')[0]),newtravel_starttime.split(':').size() > 0 ? Integer.valueOf(newtravel_starttime.split(':')[1]) : 0,0,0) : null,
            End_Date__c = newtravel_enddate != null ? newtravel_enddate : null,
            End_Date_Time__c = newtravel_endtime != null && newtravel_endtime != '' ? Time.newInstance(Integer.valueOf(newtravel_endtime.split(':')[0]),newtravel_endtime.split(':').size() > 0 ? Integer.valueOf(newtravel_endtime.split(':')[1]) : 0,0,0) : null,
            Travel_Type__c = newtravel_traveltype,
            Group_Type__c = newtravel_grouptype,
            Location_Type__c = newtravel_locationpickuptype,
            Location_Details__c = newtravel_locationpickupdetails,
            Location_Drop_Off_Type__c = newtravel_locationdropofftype,
            Location_Details_Drop_Off__c = newtravel_locationdropoffdetails,
            Airline_Info_Special_Notes__c = newtravel_notes
        );
        travel.Start_Date_Full__c = travel.Start_Date__c != null && travel.Start_Date_Time__c != null ? Datetime.newInstance(travel.Start_Date__c, travel.Start_Date_Time__c) : null;
        travel.End_Date_Full__c = travel.End_Date__c != null && travel.End_Date_Time__c != null ? Datetime.newInstance(travel.End_Date__c, travel.End_Date_Time__c) : null;
        if(newtravel_subtripid != null && newtravel_subtripid != '') travel.GT_Sub_Trip_Details__c = newtravel_subtripid;
        if(travelActualId == '') travel.Production_Ground__c = opportunityId;
        upsert travel;
        
        if(newtravel_updatemaster){
            Ground__c gAux = new Ground__c(Id = tripViewId);
            if(newtravel_startdate != null){
                tripView.Start_Date__c = tripView.Start_Date__c != null ? (tripView.Start_Date__c <= newtravel_startdate ? tripView.Start_Date__c : newtravel_startdate) : newtravel_startdate;
                gAux.Start_Date__c = tripView.Start_Date__c != null ? (tripView.Start_Date__c <= newtravel_startdate ? tripView.Start_Date__c : newtravel_startdate) : newtravel_startdate;
            }
            if(newtravel_enddate != null){
                tripView.End_Date__c = tripView.End_Date__c != null ? (tripView.End_Date__c >= newtravel_enddate ? tripView.End_Date__c : newtravel_enddate) : newtravel_enddate;
                gAux.End_Date__c = tripView.End_Date__c != null ? (tripView.End_Date__c >= newtravel_enddate ? tripView.End_Date__c : newtravel_enddate) : newtravel_enddate;
            }
            update gAux;
        }
        refreshSubtripsDataBids(tripViewid);
        searchItinerary();
        getSubStripByTrip();
    }
    
    public void saveSubTrip(){
        if(subtripIdActual != null && subtripIdActual != ''){
            Ground__c gAux;
            for(Ground__c gd : subTripList){
                if(gd.Id == subtripIdActual){
                    gAux = gd;
                    gAux.GT_Freight__c = subtripFreight != null && subtripFreight != '' ? subtripFreight : null;
                    update gd;
                    break;
                }
            }
            system.debug(gAux);
            Boolean enter = false;
            Integer i = 1;
            List<Ground__c> groundExistList = new List<Ground__c>();
			for(Ground__c gd : [SELECT Id, Trip_Order__c FROM Ground__c WHERE RecordType.Name = 'GT Sub Trip Details' AND GT_Trip_Details__c =: tripViewid ORDER BY Trip_Order__c ASC]){
                if(gd.Id != gAux.Id){
                    if(i == gAux.Trip_Order__c){
                        if(gd.Trip_Order__c >= gAux.Trip_Order__c && (i - 1 != 0))
                            gd.Trip_Order__c = i - 1;
                        else
                            gd.Trip_Order__c = i + 1;
                        
                        groundExistList.add(gd);
                    }else{
                        gd.Trip_Order__c = i;
                        groundExistList.add(gd);
                    }
                }
                i++;
            }
            
            if(groundExistList.size() > 0) update groundExistList;
            refreshSubtripsDataBids(tripViewid);
            searchItinerary();
            getSubStripByTrip();
        }
    }
    
    public void deleteSubTrip(){
        if(subtripIdActual != null && subtripIdActual != ''){
            delete [SELECT Id FROM Ground__c WHERE RecordType.Name = 'GT Travel Details' AND GT_Sub_Trip_Details__c =: subtripIdActual];
            delete [SELECT Id FROM Ground__c WHERE Id =: subtripIdActual];
            
            Integer cont = 1;
            List<Ground__c> groundExistList = new List<Ground__c>();
            for(Ground__c gd : [SELECT Id, Trip_Order__c FROM Ground__c WHERE RecordType.Name = 'GT Sub Trip Details' AND GT_Trip_Details__c =: tripViewid ORDER BY Trip_Order__c ASC]){
                gd.Trip_Order__c = cont;
                groundExistList.add(gd);
                cont++;
            }
            
            if(groundExistList.size() > 0) update groundExistList;
            refreshSubtripsDataBids(tripViewid);
            searchItinerary();
            getSubStripByTrip();
        }
    }
    
    public void newSubTrip(){
        if(tripViewId != null && tripViewid != ''){
            List<Ground__c> groundExistList = [SELECT Id, Trip_Order__c FROM Ground__c WHERE RecordType.Name = 'GT Sub Trip Details' AND GT_Trip_Details__c =: tripViewid ORDER BY Trip_Order__c DESC LIMIT 1];
            Ground__c new_subtrip = new Ground__c(
                Production_Ground__c = opportunityId,
                RecordTypeId = ground_GTSubStripDetailsRT,
                GT_Trip_Details__c = tripViewid,
                Trip_Order__c = (groundExistList.size() > 0 ? (groundExistList[0].Trip_Order__c != null ? groundExistList[0].Trip_Order__c + 1 : 1) : 1),
                Description__c = (tripview != null ? tripview.Description__c : null)
            );
            insert new_subtrip;
            refreshSubtripsDataBids(tripViewid);
            searchItinerary();
            getSubStripByTrip();
        }
    }
    
    public static void refreshSubtripsDataBids(String tripViewId){
        List<Bid__c> bidExist = [SELECT Id, GT__c, Production__c FROM Bid__c WHERE GT__c =: tripViewId AND Status__c = 'Unsent'];
        if(bidExist.size() > 0){
            List<Ground__c> subTripDelete = [SELECT Id FROM Ground__c WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND Bid_Sub_Trip__c IN: bidExist];
            system.debug(subTripDelete);
            delete [SELECT Id FROM Ground__c WHERE GT_Sub_Trip_Details__c IN: subTripDelete AND RecordType.DeveloperName = 'GT_Travel_Details'];
            delete subTripDelete;
            
            Ground__c gAux;
            List<Ground__c> gAuxList;
            Map<String,List<Ground__c>> subtripDataMap = new Map<String,List<Ground__c>>();
            Set<String> subtripDataIds = new Set<String>();
            for(Ground__c subtripData : [SELECT Id, Service_Type__c, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, GT_Trip_Details__c
                                         FROM Ground__c 
                                         WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND GT_Trip_Details__c =: tripViewId ORDER BY Trip_Order__c ASC]){
                                             subtripDataIds.add(subtripData.Id);
                                             gAuxList = subtripDataMap.get(subtripData.GT_Trip_Details__c) != null ? subtripDataMap.get(subtripData.GT_Trip_Details__c) : new List<Ground__c>();
                                             gAuxList.add(subtripData);
                                             subtripDataMap.put(subtripData.GT_Trip_Details__c,gAuxList.clone());
                                         }
                
            Map<String,List<Ground__c>> travelsBySubTripMapAux = new Map<String,List<Ground__c>>();
            if(subtripDataIds.size() > 0){
                for(Ground__c g : [SELECT Id, Line__c, Vehicle_Ref__c, Vehicle_Lookup__c, GT_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c,
                                   Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c, Start_Date_Time__c, End_Date_Time__c, Location_Drop_Off_Type__c, Location_Details_Drop_Off__c, Sub_Trip_Notes__c
                                   FROM Ground__c WHERE RecordType.DeveloperName = 'GT_Travel_Details' AND GT_Sub_Trip_Details__c =: subtripDataIds ORDER BY Line__c ASC]){
                                       gAuxList = travelsBySubTripMapAux.get(g.GT_Sub_Trip_Details__c) != null ? travelsBySubTripMapAux.get(g.GT_Sub_Trip_Details__c) : new List<Ground__c>();
                                       gAuxList.add(g);
                                       travelsBySubTripMapAux.put(g.GT_Sub_Trip_Details__c,gAuxList.clone());
                                       
                                   }
            }
            
            Map<Integer,Ground__c> subtripInsertMap = new Map<Integer,Ground__c>();
            Map<Integer,List<Ground__c>> travelInsertMap = new Map<Integer,List<Ground__c>>();
            Integer cx = 1;
            List<Ground__c> travelListAux;
            for(Bid__c b : bidExist){
                if(subtripDataMap.get(b.GT__c) != null){
                    for(Ground__c gs : subtripDataMap.get(b.GT__c)){
                        gAux = gs.clone();
                        gAux.Id = null;
                        gAux.GT_Trip_Details__c = null;
                        gAux.RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId();
                        gAux.Production_Ground__c = b.Production__c;
                        gAux.Bid_Sub_Trip__c = b.Id;
                        subtripInsertMap.put(cx,gAux);
                        if(travelsBySubTripMapAux.get(gs.Id) != null){
                            for(Ground__c gs2 : travelsBySubTripMapAux.get(gs.Id)){
                                gAux = gs2.clone();
                                gAux.Id = null;
                                gAux.GT_Trip_Details__c = null;
                                gAux.Vehicle_Lookup__c = gs2.Vehicle_Lookup__c;
                                gAux.RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId();
                                gAux.Production_Ground__c = b.Production__c;
                                gAux.Bid_Sub_Trip__c = b.Id;
                                
                                travelListAux = travelInsertMap.get(cx) != null ? travelInsertMap.get(cx) : new List<Ground__c>();
                                travelListAux.add(gAux);
                                travelInsertMap.put(cx,travelListAux.clone());
                            }
                        }
                        cx++;
                    }
                }
            }
            
            if(subtripInsertMap.size() > 0){
                insert subtripInsertMap.values();
                List<Ground__c> travelNewList = new List<Ground__c>();
                for(Integer ix : subtripInsertMap.keySet()){
                    if(travelInsertMap.get(ix) != null){
                        for(Ground__c gms : travelInsertMap.get(ix)){
                            gms.GT_Sub_Trip_Details__c = subtripInsertMap.get(ix).Id;
                            travelNewList.add(gms);
                        }
                    }
                }
                if(travelNewList.size() > 0) insert travelNewList;
            }
        }
    }
    
    public void getSubStripByTrip(){
        subTripList = new List<Ground__c>();
        travelsBySubTripMap = new Map<String,List<Ground__c>>();
        hasFreightMap = new Map<String,Boolean>();
        if(tripViewId != null && tripViewid != ''){
            for(Ground__c subtrip : [SELECT Id, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, GT_Trip_Details__c, GT_Freight__c, GT_Freight__r.Name
                                     FROM Ground__c 
                                     WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND GT_Trip_Details__c =: tripViewid ORDER BY Trip_Order__c ASC]){
                                         subTripList.add(subtrip);
                                         hasFreightMap.put(subtrip.Id,subtrip.GT_Freight__c != null ? true : false);
                                     }
            
            if(subTripList.size() > 0){
                List<Ground__c> travelAux;
                for(Ground__c g : [SELECT Id, Line__c, Vehicle_Ref__c, Vehicle_Lookup__c, GT_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details_Drop_Off__c,
                                   Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c, Start_Date_Time__c, End_Date_Time__c, Start_Date_Time_Text__c, End_Date_Time_Text__c, Location_Drop_Off_Type__c
                                   FROM Ground__c WHERE RecordType.Name = 'GT Travel Details' AND GT_Sub_Trip_Details__c =: subTripList ORDER BY Line__c ASC]){
                                       g.Start_Date_Time_Text__c = g.Start_Date__c != null && g.Start_Date_Time__c != null ? Datetime.newInstance(g.Start_Date__c, g.Start_Date_Time__c).format('h:mm a') : '';
                                       g.End_Date_Time_Text__c = g.End_Date__c != null && g.End_Date_Time__c != null ? Datetime.newInstance(g.End_Date__c, g.End_Date_Time__c).format('h:mm a') : '';
                                       travelAux = travelsBySubTripMap.get(g.GT_Sub_Trip_Details__c) != null ? travelsBySubTripMap.get(g.GT_Sub_Trip_Details__c) : new List<Ground__c>();
                                       travelAux.add(g);
                                       travelsBySubTripMap.put(g.GT_Sub_Trip_Details__c,travelAux.clone());
                                   }
                for(Ground__c subtrip : subTripList){
                    if(travelsBySubTripMap.get(subtrip.Id) == null) travelsBySubTripMap.put(subtrip.Id,new List<Ground__c>());
                }
            }
        }
    }
    
    public void saveEditVehicleTrip(){
        if(vehicleIdActual != null && vehicleIdActual != ''){
            new_vehicle = new Ground__c(
                Id = vehicleIdActual,
                Vehicle_Ref__c = vehicle_vehicleref,
                Vehicle_Type__c = vehicle_vehicletype,
                Capacity__c = vehicle_capacity,
                Make__c = vehicle_make,
                Model__c = vehicle_model,
                Year__c = vehicle_year,
                Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null),
                Other_Amenities__c = vehicle_otheramenities,
                Gear_Luggage_Space__c = vehicle_luggage
            );
            update new_vehicle;
            
            refreshVehicleDataBids(tripViewId);
        }
        searchItinerary();
        getVehiclesByTrip();
    }
    
    public void addVehicleTrip(){
        if(opportunityId != null && opportunityId != null && tripViewId != null && tripViewId != ''){
            newVehicleTrip.Id = null;
            newVehicleTrip.RecordTypeId = ground_vehicletypeRT;
            newVehicleTrip.Production_Ground__c = opportunityId;
            newVehicleTrip.GT_Trip_Details__c = tripViewId;
            newVehicleTrip.Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null);
            newVehicleTrip.Make__c = vehicle_make;
            newVehicleTrip.Model__c = vehicle_model;
            insert newVehicleTrip;
            
            refreshVehicleDataBids(tripViewId);
        }
        searchItinerary();
        getVehiclesByTrip();
    }
    
    public static void refreshVehicleDataBids(String tripViewId){
        List<Bid__c> bidExist = [SELECT Id, GT__c, Production__c FROM Bid__c WHERE GT__c =: tripViewId AND Status__c = 'Unsent'];
        if(bidExist.size() > 0){
            delete [SELECT Id FROM Ground__c WHERE RecordType.DeveloperName = 'Vehicle_Type' AND Bid__c IN: bidExist];
            
            List<Ground__c> vehiclesByTripList = [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, Gear_Luggage_Space__c, Description__c
                                       FROM Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: bidExist[0].Production__c 
                                       AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND GT_Trip_Details__c =: tripViewId AND Sales_GT_Details__c = NULL];
            Ground__c gAux;
            List<Ground__c> gListAux = new List<Ground__c>();
            for(Bid__c b : bidExist){
                for(Ground__c g : vehiclesByTripList){
                    gAux = g.clone();
                    gAux.Trip_Vehicle__c = g.Id;
                    gAux.Bid__c = b.Id;
                    gAux.GT_Trip_Details__c = null;
                    gAux.Production_Ground__c = b.Production__c;
                    gAux.RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId();
                    gListAux.add(gAux);
                }
            }
            
            if(gListAux.size() > 0) insert gListAux;
        }
    }
    
    public void getVehiclesByTrip(){
        vehiclesByTripList = new List<Ground__c>();
        if(tripViewId != null && tripViewId != ''){
           vehiclesByTripList = [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, Gear_Luggage_Space__c
                                       FROM Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: opportunityId 
                                       AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND GT_Trip_Details__c =: tripViewId AND Sales_GT_Details__c = NULL];
        }
    }
    
    public void saveEditConcessionTrip(){
        if(concessionActual != null && concessionActual != ''){
            //newConcessionTrip = new Concessions__c(Id=concessionActual,Concession_Type__c = 'GT',Concessions_Requested__c=concessionRequestedActual,Notes__c=concessionNoteActual);
            newConcessionTrip = new Concessions__c(Id=concessionActual,Concession_Type__c = 'GT',Concessions_Requested__c=concessionRequestedActual,Create_in_Bid__c=concessionCreateInBid);
            update newConcessionTrip;
            refreshConcessionDataBids(tripViewId);
        }
        getConcessionsByTrip();        
    }
    
    public void deleteConcession(){
        if(concessionActual != null && concessionActual != ''){
            delete [SELECT Id FROM Concessions__c WHERE Id=:concessionActual];
            refreshConcessionDataBids(tripViewId);
        }
        getConcessionsByTrip();
    }
    
    public void addConcessionTrip(){
        system.debug(tripViewId);
        if(tripViewId != null && tripViewId !=''){
            newConcessionTrip.Concession_Type__c = 'GT';
            newConcessionTrip.Production__c = opportunityId;
            newConcessionTrip.GT__c = tripViewId;
            newConcessionTrip.Create_in_Bid__c=concessionCreateInBid;
            newConcessionTrip.Concessions_Requested__c = concessionRequestedActual;
            insert newConcessionTrip;
            
            refreshConcessionDataBids(tripViewId);
        }
        getConcessionsByTrip();
    }
    
    public static void refreshConcessionDataBids(String tripViewId){
        List<Bid__c> bidExist = [SELECT Id, GT__c, Production__c FROM Bid__c WHERE GT__c =: tripViewId AND Status__c = 'Unsent'];
        if(bidExist.size() > 0){
            delete [SELECT Id FROM Concessions__c WHERE Bid__c IN: bidExist];
            
            List<Concessions__c> concessionByTripList = [SELECT Id, Concessions_Requested__c, Concession_Type__c, Notes__c, Create_in_Bid__c FROM Concessions__c WHERE Production__c =: bidExist[0].Production__c AND GT__c =: tripViewId AND Create_in_Bid__c = true ORDER BY CreatedDate DESC];
            Concessions__c cAux;
            List<Concessions__c> cListAux = new List<Concessions__c>();
            for(Bid__c b : bidExist){
                for(Concessions__c c : concessionByTripList){
                    cAux = c.clone();
                    cAux.Bid__c = b.Id;
                    cAux.Production__c = b.Production__c;
                    cListAux.add(cAux);
                }
            }
            
            if(cListAux.size() > 0) insert cListAux;
        }
    }
    
    public void getConcessionsByTrip(){
    	concessionsRequestedTrip = new List<Concessions__c>();
        if(opportunityId != null && opportunityId != ''){
            if(tripViewId != null && tripViewId != ''){
                concessionsRequestedTrip = [SELECT Id, Concessions_Requested__c, Concession_Type__c, Notes__c, Create_in_Bid__c FROM Concessions__c WHERE Production__c =: opportunityId AND GT__c =: tripViewId ORDER BY CreatedDate DESC];
            }
        }
    }
    
    public void newConcessionTrip(){
        newConcessionTrip = new Concessions__c(Concession_Type__c='GT');
    }
    
    public void sendEditReleaseBid(){
        if(dataids != null && dataids.trim() != ''){
            Set<String> vendorContactIds = new Set<String>();
            for(String d : dataids.split(',')){
                vendorContactIds.add(sendBidRequestMapRelease.get(d).Vendor_Contact__c);
            }
            
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id IN: vendorContactIds]) contactMap.put(c.Id,c);
            
            //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            User userActual = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripViewId);
            String owaeId = userActual != null && userActual.Email != null ? verifyWideAddress(userActual.Email) : null;
            
            Journal__c journalAux;
            Bid__c bAux;
            List<Journal__c> journalAuxList = new List<Journal__c>();
            Map<String,Bid__c> bidUpdateMap = new Map<String,Bid__c>();
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail;
            String[] toAddresses;
            Set<String> ccAddresses;
            String body = '';
            String dateIn;
            String dateOut;
            for(String d : dataids.split(',')){
                //New Journals
                journalAux = new Journal__c(
                    RecordTypeId = journal_bidjournalRT,
                    Bid__c = sendBidRequestMapRelease.get(d).Id,
                    Journal_Entry__c = 'Release Bid has been sent to ' + contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Name + ' at ' + contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Email
                );
                journalAuxList.add(journalAux);
                
                //Bid update
                if(sendBidRequestMapRelease.get(d) != null && sendBidRequestMapRelease.get(d).Status__c != 'Contracted'){
                    bAux = new Bid__c(Id=sendBidRequestMapRelease.get(d).Id,Status__c='Bid Released');
                    bidUpdateMap.put(bAux.Id,bAux);
                }
                
                //EMAIL
                ccAddresses = new Set<String>();
                for(ContactWrapper cw : contactsByVendor_releaseMap.get(d)){
                    if(!cw.disabled && cw.selected) ccAddresses.add(cw.c.Email);
                }
                if(sendBidRequestMapRelease.get(d).Vendor__r.ParentId != null){
                    for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(sendBidRequestMapRelease.get(d).Vendor__r.ParentId)){
                        if(!cw.disabled && cw.selected) ccAddresses.add(cw.c.Email);
                    }
                }
                
                dateIn = (sendBidRequestMapRelease.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMapRelease.get(d).GT__r.Start_Date__c.year(),sendBidRequestMapRelease.get(d).GT__r.Start_Date__c.month(),sendBidRequestMapRelease.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : '');
                dateOut = (sendBidRequestMapRelease.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMapRelease.get(d).GT__r.End_Date__c.year(),sendBidRequestMapRelease.get(d).GT__r.End_Date__c.month(),sendBidRequestMapRelease.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy')  : '');
                
                mail = new Messaging.SingleEmailMessage();
                if(owaeId != null && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(owaeId);
                toAddresses = new String[] {contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Email};
                    mail.setToAddresses(toAddresses);
                if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
                mail.setSubject(emailSubject.replace('{ProductionName}',sendBidRequestMapRelease.get(d).Production__r.Name)
                                .replace('{StartDate}',dateIn)
                                .replace('{EndDate}',dateOut)
                               );
                mail.setHtmlBody(emailBody.replace('{VendorName}',sendBidRequestMapRelease.get(d).Vendor__r.Name)
                                 .replace('{ProductionName}',sendBidRequestMapRelease.get(d).Production__r.Name)
                                 .replace('{StartDate}',dateIn)
                                 .replace('{EndDate}',dateOut)
                                 .replace('{GroundTravelCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
                                );
                myEmails.add(mail);
            }    
            
            Ground__c gAux = new Ground__c(Id = tripViewId,Email_Subject_Release_Bid__c=null,Email_Body_Release_Bid__c=null);
            update gAux;
            insert journalAuxList;
            update bidUpdateMap.values();
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
            openReleaseBid();
        }
    }
    
    public void saveAndCloseReleaseBid(){
        List<Ground__c> template = [SELECT Id, Email_Subject_Release_Bid__c, Email_Body_Release_Bid__c FROM Ground__c WHERE Id =: tripViewId];
        if(template.size() > 0){
            template[0].Email_Subject_Release_Bid__c = emailSubject.unescapeHtml4();
            template[0].Email_Body_Release_Bid__c = emailBody.unescapeHtml4();
            update template[0];
        }
    }
    
    public void sendReleaseBid(){
        if(dataids != null && dataids.trim() != ''){
            Set<String> vendorContactIds = new Set<String>();
            for(String d : dataids.split(',')){
                vendorContactIds.add(sendBidRequestMapRelease.get(d).Vendor_Contact__c);
            }
            
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id IN: vendorContactIds]) contactMap.put(c.Id,c);
            
            //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            User userActual = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripViewId);
            String owaeId = userActual != null && userActual.Email != null ? verifyWideAddress(userActual.Email) : null;
            
            Journal__c journalAux;
            Bid__c bAux;
            List<Journal__c> journalAuxList = new List<Journal__c>();
            Map<String,Bid__c> bidUpdateMap = new Map<String,Bid__c>();
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail;
            String[] toAddresses;
            Set<String> ccAddresses;
            String body = '';
            List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='GT_Release_Bid'];
            
            for(String d : dataids.split(',')){
                //New Journals
                journalAux = new Journal__c(
                    RecordTypeId = journal_bidjournalRT,
                    Bid__c = sendBidRequestMapRelease.get(d).Id,
                    Journal_Entry__c = 'Release Bid has been sent to ' + contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Name + ' at ' + contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Email
                );
                journalAuxList.add(journalAux);
                
                //Bid update
                if(sendBidRequestMapRelease.get(d) != null && sendBidRequestMapRelease.get(d).Status__c != 'Contracted'){
                    bAux = new Bid__c(Id=sendBidRequestMapRelease.get(d).Id,Status__c='Bid Released');
                    bidUpdateMap.put(bAux.Id,bAux);
                }
                
                //EMAIL
                ccAddresses = new Set<String>();
                for(ContactWrapper cw : contactsByVendor_releaseMap.get(d)){
                    if(!cw.disabled && cw.selected) ccAddresses.add(cw.c.Email);
                }
                if(sendBidRequestMapRelease.get(d).Vendor__r.ParentId != null){
                    for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(sendBidRequestMapRelease.get(d).Vendor__r.ParentId)){
                        if(!cw.disabled && cw.selected) ccAddresses.add(cw.c.Email);
                    }
                }
                
                mail = new Messaging.SingleEmailMessage();
                if(owaeId != null && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(owaeId);
                toAddresses = new String[] {contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Email};
                    mail.setToAddresses(toAddresses);
                if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
                String dateIn = (sendBidRequestMapRelease.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMapRelease.get(d).GT__r.Start_Date__c.year(),sendBidRequestMapRelease.get(d).GT__r.Start_Date__c.month(),sendBidRequestMapRelease.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : '');
                String dateOut = (sendBidRequestMapRelease.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMapRelease.get(d).GT__r.End_Date__c.year(),sendBidRequestMapRelease.get(d).GT__r.End_Date__c.month(),sendBidRequestMapRelease.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy')  : '');
                mail.setSubject('Release Bid - ' + 
                                sendBidRequestMapRelease.get(d).Production__r.Name + ' - ' + 
                                dateIn + '-' + dateOut
                               );
                mail.setSubject(template.size() > 0 ? template[0].Subject.replace('{ProductionName}',sendBidRequestMapRelease.get(d).Production__r.Name).replace('{StartDate}',dateIn).replace('{EndDate}',dateOut) : '');
                
                if(template.size() > 0) body = (template[0].HTMLValue != null ? template[0].HTMLValue.replace('{GroundTravelCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
                                                //.replace('{ContactName}',contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c).Name)
                                                .replace('{VendorName}',sendBidRequestMapRelease.get(d).Vendor__r.Name)
                                                .replace('{ProductionName}',sendBidRequestMapRelease.get(d).Production__r.Name)
                                                .replace('{StartDate}',dateIn)
                                                .replace('{EndDate}',dateOut) : '');
                mail.setHtmlBody(body);
                myEmails.add(mail);
            }    
            
            Ground__c hAux = new Ground__c(Id = tripViewId,Email_Subject_Release_Bid__c=null,Email_Body_Release_Bid__c=null);
            update hAux;
            insert journalAuxList;
            update bidUpdateMap.values();
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
            isBidResendRendered = false;
            getBidsByTrip();
        }
    }
    
    public void changeContactReleaseBid(){
        sendBidRequestMapRelease.get(vendoraccount_actual_id).Vendor_Contact__c = vendorcontact_actual_id;
        for(ContactWrapper cw : contactsByVendor_releaseMap.get(vendoraccount_actual_id)){
            if(vendorcontact_actual_id == cw.c.Id){
                cw.selected = true;
                cw.disabled = true;
            }else{
                if(cw.selected && cw.disabled){
                    cw.selected = false;
                    cw.disabled = false;
                }
            }
        }
        if(sendBidRequestMapRelease.get(vendoraccount_actual_id).Vendor__r.ParentId != null){
            for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(sendBidRequestMapRelease.get(vendoraccount_actual_id).Vendor__r.ParentId)){
                if(vendorcontact_actual_id == cw.c.Id){
                    cw.selected = true;
                    cw.disabled = true;
                }else{
                    if(cw.selected && cw.disabled){
                        cw.selected = false;
                        cw.disabled = false;
                    }
                }
            }
        }
    }
    
    public void openReleaseBid(){
        isBidResendRendered = true;
        sendBidRequestMapReleaseSize = 0;
        sendBidRequestMapRelease = new Map<String,Bid__c>();
        if(sendBidRequestMapReleaseSelected == null || sendBidRequestMapReleaseSelected.isEmpty()) sendBidRequestMapReleaseSelected = new Map<String,Boolean>();
        Set<String> parentIds = new Set<String>();
        for(Bid__c b : [SELECT Id, Name, Vendor__c, Vendor__r.Name, Vendor__r.ParentId, Vendor_Contact__c, Status__c, Production__c, Production__r.Name, GT__c, GT__r.Start_Date__c, GT__r.End_Date__c FROM Bid__c WHERE Id IN: bidByTripIds AND Vendor__c <> NULL AND Status__c = 'Sent' /*NOT IN ('Contracted','Cancelled','Contracted On Own','Bid Released')*/]){
            sendBidRequestMapRelease.put(b.Vendor__c,b);
            if(sendBidRequestMapReleaseSelected.get(b.Vendor__c) == null) sendBidRequestMapReleaseSelected.put(b.Vendor__c,false);
            if(b.Vendor__r.ParentId != null) parentIds.add(b.Vendor__r.ParentId);
        }
        
        contactSelectOption_releaseMap = new Map<String,List<SelectOption>>();
        contactsByVendor_releaseMap = new Map<String,List<ContactWrapper>>();
        contactsByVendorParent_releaseMap = new Map<String,List<ContactWrapper>>();
        List<ContactWrapper> contactAuxList;
        List<SelectOption> contactAuxSelectOptions;
        
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId IN: parentIds AND Email <> NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendorParent_releaseMap.get(c.AccountId) != null ? contactsByVendorParent_releaseMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),false));
            contactsByVendorParent_releaseMap.put(c.AccountId,contactAuxList.clone());
        }
        
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId IN: sendBidRequestMapRelease.keySet() AND Email <> NULL AND Order__c <> NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendor_releaseMap.get(c.AccountId) != null ? contactsByVendor_releaseMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),(c.Order__c == 1 ? true : false)));
            contactsByVendor_releaseMap.put(c.AccountId,contactAuxList.clone());
        }
        
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId IN: sendBidRequestMapRelease.keySet() AND Email <> NULL AND Order__c = NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendor_releaseMap.get(c.AccountId) != null ? contactsByVendor_releaseMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),(c.Order__c == 1 ? true : false)));
            contactsByVendor_releaseMap.put(c.AccountId,contactAuxList.clone());
        }
        
        String parentId;
        for(String key : sendBidRequestMapRelease.keySet()){
            parentId = sendBidRequestMapRelease.get(key).Vendor__r.ParentId;
            if(contactsByVendor_releaseMap.get(key) == null && (parentId != null && contactsByVendorParent_releaseMap.get(parentId) == null)){
                //sendBidRequestMapRelease.remove(key);
            }else{
                if(contactsByVendorParent_releaseMap.get(parentId) != null){
                    for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(parentId)){
                        contactAuxSelectOptions = contactSelectOption_releaseMap.get(key) != null ? contactSelectOption_releaseMap.get(key) : new List<SelectOption>();
                        contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                        contactSelectOption_releaseMap.put(key,contactAuxSelectOptions.clone());
                    }
                }
                if(contactsByVendor_releaseMap.get(key) != null){
                    for(ContactWrapper cw : contactsByVendor_releaseMap.get(key)){
                        contactAuxSelectOptions = contactSelectOption_releaseMap.get(key) != null ? contactSelectOption_releaseMap.get(key) : new List<SelectOption>();
                        contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                        contactSelectOption_releaseMap.put(key,contactAuxSelectOptions.clone());
                    }
                }
                if(contactsByVendor_releaseMap.get(key) == null) contactsByVendor_releaseMap.put(key,new List<ContactWrapper>());
                if(contactSelectOption_releaseMap.get(key) == null) contactSelectOption_releaseMap.put(key,new List<SelectOption>());
            }
        }
        for(String key : parentIds){
            if(contactsByVendorParent_releaseMap.get(key) == null) contactsByVendorParent_releaseMap.put(key,new List<ContactWrapper>());
            if(contactSelectOption_releaseMap.get(key) == null) contactSelectOption_releaseMap.put(key,new List<SelectOption>());
        }
        Boolean haveDefault;
        for(String key : sendBidRequestMapRelease.keySet()){
            if(contactsByVendor_releaseMap.get(key) == null) contactsByVendor_releaseMap.put(key,new List<ContactWrapper>());
            if(contactSelectOption_releaseMap.get(key) == null) contactSelectOption_releaseMap.put(key,new List<SelectOption>());
            
            if(sendBidRequestMapRelease.get(key).Vendor_Contact__c == null){
                haveDefault = false;
                parentId = sendBidRequestMapRelease.get(key).Vendor__r.ParentId;
                if(contactsByVendorParent_releaseMap.get(parentId) != null){
                    for(ContactWrapper cw : contactsByVendorParent_releaseMap.get(parentId)){
                        if(!haveDefault){
                            cw.selected = true;
                            haveDefault = true;
                        }
                    }
                }
                if(contactsByVendor_releaseMap.get(key) != null){
                    for(ContactWrapper cw : contactsByVendor_releaseMap.get(key)){
                        if(!haveDefault){
                            cw.selected = true;
                            haveDefault = true;
                        }
                    }
                }
            }
        }
        sendBidRequestMapReleaseSize = sendBidRequestMapRelease.size();
    }
    
    public void sendEditAllEmail(){
        if(dataids != null && dataids.trim() != ''){
            Set<String> vendorContactIds = new Set<String>();
            for(String d : dataids.split(',')){
                vendorContactIds.add(sendBidRequestMap.get(d).Vendor_Contact__c);
            }
            
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id IN: vendorContactIds]) contactMap.put(c.Id,c);
            
            //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email, User__r.Phone FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            User userActual = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripViewId);
            String owaeId = userActual != null && userActual.Email != null ? verifyWideAddress(userActual.Email) : null;
            
            Journal__c journalAux;
            Bid__c bAux;
            List<Journal__c> journalAuxList = new List<Journal__c>();
            Map<String,Bid__c> bidUpdateMap = new Map<String,Bid__c>();
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail;
            String[] toAddresses;
            Set<String> ccAddresses;
            String ccEmails = '';//@Conga
            List<String> congaParameters = new List<String>();//@Conga
            Integer i = 1;//@Conga
            String body = '';
            List<EmailTemplate> templatePDF = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate WHERE DeveloperName = 'GT_Bid_Request_All'];

            List<EmailTemplate> templateLink = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='GT_Bid_Request_Link_All'];
            String subject = '';
            
            Ground__c gAux = new Ground__c(Id=tripViewId);
            
            for(String d : dataids.split(',')){
                if(d.trim() != ''){
                    //New Journals
                    journalAux = new Journal__c(
                        RecordTypeId = journal_bidjournalRT,
                        Bid__c = sendBidRequestMap.get(d).Id,
                        Journal_Entry__c = 'GT Bid Request ' + type_email.toUpperCase() +' was sent to ' + contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Name + ' at ' + contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email
                    );
                    journalAuxList.add(journalAux);
                    
                    //Bid update
                    if(sendBidRequestMap.get(d) != null && sendBidRequestMap.get(d).Status__c != 'Contracted'){
                        bAux = new Bid__c(Id=sendBidRequestMap.get(d).Id,Status__c='Sent');
                        bidUpdateMap.put(bAux.Id,bAux);
                    }
                    
                    //EMAIL
                    ccAddresses = new Set<String>();
                    for(ContactWrapper cw : contactsByVendor_bidRequestMap.get(d)){
                        if(!cw.disabled && cw.selected){
                            ccAddresses.add(cw.c.Email);
                            ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + cw.c.Email : cw.c.Email;//@conga
                        } 
                    }
                    if(sendBidRequestMap.get(d).Vendor__r.ParentId != null){
                        for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(sendBidRequestMap.get(d).Vendor__r.ParentId)){
                            if(!cw.disabled && cw.selected){
                                ccAddresses.add(cw.c.Email);
                                ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + cw.c.Email : cw.c.Email;//@conga
                            } 
                        }
                    }
                    
                    mail = new Messaging.SingleEmailMessage();
                    if(owaeId != null && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(owaeId);
                    toAddresses = new String[] {contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email};
                        mail.setToAddresses(toAddresses);
                    if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
                    if(type_email == 'pdf'){
                        subject = (templatePDF.size() > 0 ? templatePDF[0].Subject.replace('{ProductionName}',sendBidRequestMap.get(d).Production__r.Name)
                                   .replace('{StartDate}',(sendBidRequestMap.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.Start_Date__c.year(),sendBidRequestMap.get(d).GT__r.Start_Date__c.month(),sendBidRequestMap.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{EndDate}',(sendBidRequestMap.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.End_Date__c.year(),sendBidRequestMap.get(d).GT__r.End_Date__c.month(),sendBidRequestMap.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{BidNumber}',sendBidRequestMap.get(d).Name)
                                   : '');
                        body = emailBody.replace('{GroundTravelCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
                            //.replace('{GroundTravelCoordinator}',(prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : ''))
                            .replace('{CoordinatorPhone}',userActual != null && userActual.Phone != null ? userActual.Phone : '');
                            //.replace('{CoordinatorPhone}',(prodAssocAux.size() > 0 && prodAssocAux[0].User__r.Phone != null ? prodAssocAux[0].User__r.Phone : ''))
                        gAux.Email_Body_Bid_Request__c = null;
                    }else{
                        subject = (templatePDF.size() > 0 ? templatePDF[0].Subject.replace('{ProductionName}',sendBidRequestMap.get(d).Production__r.Name)
                                   .replace('{StartDate}',(sendBidRequestMap.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.Start_Date__c.year(),sendBidRequestMap.get(d).GT__r.Start_Date__c.month(),sendBidRequestMap.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{EndDate}',(sendBidRequestMap.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.End_Date__c.year(),sendBidRequestMap.get(d).GT__r.End_Date__c.month(),sendBidRequestMap.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{BidNumber}',sendBidRequestMap.get(d).Name)
                                   : '');
                        body = emailBody.replace('{GroundTravelCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
                            //.replace('{GroundTravelCoordinator}',(prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : ''))
                            .replace('{VendorURL}',sendBidRequestMap.get(d).Vendor__r.Name)
                            //.replace('{VendorURL}','<a href="https://ccdev-roadrebel.cs42.force.com/" target="_blank">' + sendBidRequestMap.get(d).Vendor__r.Name + '</a>')
                            //.replace('{VendorURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Vendor__c + '" target="_blank">' + sendBidRequestMap.get(d).Vendor__r.Name + '</a>')
                            .replace('{BidURL}','<a href="'+ (communityURLvalue != null ? communityURLvalue + '/s/?service=ground&record=' + sendBidRequestMap.get(d).Id : '') +'" target="_blank">'+ (communityURLvalue != null ? communityURLvalue + '/s/?service=ground&record=' + sendBidRequestMap.get(d).Id : '') + '</a>')
                            //.replace('{BidURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Id + '" target="_blank">http://' + url + '/' + sendBidRequestMap.get(d).Id + '</a>')
                            .replace('{CoordinatorPhone}',userActual != null && userActual.Phone != null ? userActual.Phone : '');
                            //.replace('{CoordinatorPhone}',(prodAssocAux.size() > 0 && prodAssocAux[0].User__r.Phone != null ? prodAssocAux[0].User__r.Phone : ''));
                        gAux.Email_Body_Bid_Request_Link__c = null;
                    }
                    mail.setSubject(subject);
                    mail.setHtmlBody(body);
                    myEmails.add(mail);
                }
            }    
            
            insert journalAuxList;
            
            update bidUpdateMap.values();

            if(tripView != null && (tripView.Status_Ground__c != 'Contracted' || tripView.Status_Ground__c != 'In Contracting')){
                tripView.Status_Ground__c = 'Bid Request Stage';
                update new Ground__c(id = tripView.id, Status_Ground__c = 'Bid Request Stage', Email_Body_Bid_Request_Link__c = null, Bid_Request__c = system.today());
                List<Itinerary__c> itineraries =  [SELECT Id FROM Itinerary__c WHERE GT__c =:tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
                if(!itineraries.isEmpty()) update new Itinerary__c(Id = itineraries[0].Id, Status__c = 'Bid Request Stage');
                //searchTrip();
            }            
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
            openSendBidRequest();
        }
    }
    
    public void saveAndCloseBidRequest(){
        List<Ground__c> template = [SELECT Id, Email_Body_Bid_Request__c, Email_Body_Bid_Request_Link__c FROM Ground__c WHERE Id =: tripViewid];
        if(template.size() > 0){
            if(type_email == 'pdf') template[0].Email_Body_Bid_Request__c = emailBody;
            else template[0].Email_Body_Bid_Request_Link__c = emailBody;
            update template[0];
        }
    }
    
    public void openEditPDF(){
        List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
        if(type_email == 'pdf'){
            List<Ground__c> housingTemplate = [SELECT Id, Email_Body_Bid_Request__c FROM Ground__c WHERE Id =: tripViewid];
            if(housingTemplate.size() > 0 && housingTemplate[0].Email_Body_Bid_Request__c != null){
                emailBid_body = housingTemplate[0].Email_Body_Bid_Request__c.unescapeHtml4();
            }else{
                List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate WHERE DeveloperName = 'GT_Bid_Request_All'];
                if(template.size() > 0) emailBid_body = template[0].HTMLValue != null ? template[0].HTMLValue.unescapeHtml4() : '';
            }
        }else{
            List<Ground__c> housingTemplate = [SELECT Id, Email_Body_Bid_Request_Link__c FROM Ground__c WHERE Id =: tripViewid];
            if(housingTemplate.size() > 0 && housingTemplate[0].Email_Body_Bid_Request_Link__c != null){
                emailBid_body = housingTemplate[0].Email_Body_Bid_Request_Link__c.unescapeHtml4();
            }else{
                List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='GT_Bid_Request_Link_All'];
                if(template.size() > 0) emailBid_body = template[0].HTMLValue != null ? template[0].HTMLValue.unescapeHtml4() : '';
            }
        }
    }
    
    public void saveAddContactVendor(){
        messageCreateContact = '';
        try{
            vendorContact.Id = (vendorContact_id != null && vendorContact_id.trim() != '' ? vendorContact_id : null);
            system.debug(vendorContact);
            upsert vendorContact;
        }catch(DMLException e){
            messageCreateContact = validateError(e.getMessage());
        }
        
        Boolean exist = false;
        if(isBidRequestRendered){
            if(contactsByVendor_bidRequestMap.get(vendorContact.AccountId) != null){
                for(ContactWrapper cw : contactsByVendor_bidRequestMap.get(vendorContact.AccountId)){
                    if(vendorContact.Id == cw.c.Id) exist = true;
                }
            }
            if(!exist){
                Contact conAux = [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE Id =: vendorContact.Id];
                contactsByVendor_bidRequestMap.get(vendorContact.AccountId).add(new ContactWrapper(conAux,false,false));
                contactSelectOption_bidRequestMap.get(vendorContact.AccountId).add(new SelectOption(conAux.Id,conAux.Name));
            }
        }
        if(isBidResendRendered){
            if(contactsByVendor_releaseMap.get(vendorContact.AccountId) != null){
                for(ContactWrapper cw : contactsByVendor_releaseMap.get(vendorContact.AccountId)){
                    if(vendorContact.Id == cw.c.Id) exist = true;
                }
            }
            if(!exist){
                Contact conAux = [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE Id =: vendorContact.Id];
                contactsByVendor_releaseMap.get(vendorContact.AccountId).add(new ContactWrapper(conAux,false,false));
                contactSelectOption_releaseMap.get(vendorContact.AccountId).add(new SelectOption(conAux.Id,conAux.Name));
            }
        }
        //openSendBidRequest();
        //openReleaseBid();
    }
    
    public void changeContactVendorBid(){
        sendBidRequestMap.get(vendoraccount_actual_id).Vendor_Contact__c = vendorcontact_actual_id;
        for(ContactWrapper cw : contactsByVendor_bidRequestMap.get(vendoraccount_actual_id)){
            if(vendorcontact_actual_id == cw.c.Id){
                cw.selected = true;
                cw.disabled = true;
            }else{
                if(cw.selected && cw.disabled){
                    cw.selected = false;
                    cw.disabled = false;
                }
            }
        }
        if(sendBidRequestMap.get(vendoraccount_actual_id).Vendor__r.ParentId != null){
            for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(sendBidRequestMap.get(vendoraccount_actual_id).Vendor__r.ParentId)){
                if(vendorcontact_actual_id == cw.c.Id){
                    cw.selected = true;
                    cw.disabled = true;
                }else{
                    if(cw.selected && cw.disabled){
                        cw.selected = false;
                        cw.disabled = false;
                    }
                }
            }
        }
    }
       
    public void openSendBidRequest(){
        isBidRequestRendered = true;
        sendBidRequestMapSize = 0;
        sendBidRequestMap = new Map<String,Bid__c>();
        if(sendBidRequestMapSelected == null || sendBidRequestMapSelected.isEmpty()) sendBidRequestMapSelected = new Map<String,Boolean>();
        Set<String> parentIds = new Set<String>();
        for(Bid__c b : [SELECT Id, Name, Vendor__c, Vendor__r.Name, Vendor__r.ParentId, Vendor_Contact__c, Provider__c, Provider__r.Name, Provider__r.ParentId, Status__c, Production__c, Production__r.Name, GT__c, GT__r.Start_Date__c, GT__r.End_Date__c FROM Bid__c WHERE Id IN: bidByTripIds AND Status__c NOT IN ('Contracted','Cancelled','Contracted On Own','Bid Released','Sold Out / Not Bidding')]){
            if(b.Vendor__c != null){
                sendBidRequestMap.put(b.Vendor__c,b);
                if(sendBidRequestMapSelected.get(b.Vendor__c) == null) sendBidRequestMapSelected.put(b.Vendor__c,false);
            }
            if(b.Vendor__c == null && b.Provider__c != null){
                sendBidRequestMap.put(b.Provider__c,b);
                if(sendBidRequestMapSelected.get(b.Provider__c) == null) sendBidRequestMapSelected.put(b.Provider__c,false);
            }
            if(b.Vendor__r.ParentId != null) parentIds.add(b.Vendor__r.ParentId);
            if(b.Vendor__c == null && b.Provider__r.ParentId != null) parentIds.add(b.Provider__r.ParentId);
        }
        
        bidSendBidFirstTime = true;
        for(BidWrapper bw : bidsByTripShowList){
            if(bw.b != null && bw.b.Status__c != 'Unsent') bidSendBidFirstTime = false;
        }
        system.debug(sendBidRequestMap);
        
        contactSelectOption_bidRequestMap = new Map<String,List<SelectOption>>();
        contactsByVendor_bidRequestMap = new Map<String,List<ContactWrapper>>();
        contactsByVendorParent_bidRequestMap = new Map<String,List<ContactWrapper>>();
        List<ContactWrapper> contactAuxList;
        List<SelectOption> contactAuxSelectOptions;
                
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId IN: parentIds AND Email <> NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendorParent_bidRequestMap.get(c.AccountId) != null ? contactsByVendorParent_bidRequestMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),false));
            contactsByVendorParent_bidRequestMap.put(c.AccountId,contactAuxList.clone());
        }
        
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId IN: sendBidRequestMap.keySet() AND Email <> NULL AND Order__c <> NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendor_bidRequestMap.get(c.AccountId) != null ? contactsByVendor_bidRequestMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),(c.Order__c == 1 ? true : false)));
            contactsByVendor_bidRequestMap.put(c.AccountId,contactAuxList.clone());
            if(sendBidRequestMap.get(c.AccountId) != null && sendBidRequestMap.get(c.AccountId).Vendor_Contact__c == null && c.Order__c == 1) sendBidRequestMap.get(c.AccountId).Vendor_Contact__c = c.Id;
        }
        
        system.debug(contactsByVendor_bidRequestMap);
        
        for(Contact c : [SELECT Id, AccountId, Account.Name, Order__c, Account.ParentId, Name, Phone, Email, Fax, Designation_title__c FROM Contact WHERE AccountId IN: sendBidRequestMap.keySet() AND Email <> NULL AND Order__c = NULL ORDER BY Order__c ASC]){
            contactAuxList = contactsByVendor_bidRequestMap.get(c.AccountId) != null ? contactsByVendor_bidRequestMap.get(c.AccountId) : new List<ContactWrapper>();
            contactAuxList.add(new ContactWrapper(c,(c.Order__c == 1 ? true : false),(c.Order__c == 1 ? true : false)));
            contactsByVendor_bidRequestMap.put(c.AccountId,contactAuxList.clone());
        }
        
        String parentId;
        String parentIdProvider;
        for(String key : sendBidRequestMap.keySet()){
            parentId = sendBidRequestMap.get(key).Vendor__r.ParentId;
            parentIdProvider = sendBidRequestMap.get(key).Provider__r.ParentId;
            if(contactsByVendor_bidRequestMap.get(key) == null && contactsByVendorParent_bidRequestMap.get(parentId) == null){
                //sendBidRequestMap.remove(key);
            }else{
                if(contactsByVendorParent_bidRequestMap.get(parentId) != null){
                    for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(parentId)){
                        contactAuxSelectOptions = contactSelectOption_bidRequestMap.get(key) != null ? contactSelectOption_bidRequestMap.get(key) : new List<SelectOption>();
                        contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                        contactSelectOption_bidRequestMap.put(key,contactAuxSelectOptions.clone());
                    }
                }
                if(contactsByVendorParent_bidRequestMap.get(parentIdProvider) != null){
                    for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(parentIdProvider)){
                        contactAuxSelectOptions = contactSelectOption_bidRequestMap.get(key) != null ? contactSelectOption_bidRequestMap.get(key) : new List<SelectOption>();
                        contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                        contactSelectOption_bidRequestMap.put(key,contactAuxSelectOptions.clone());
                    }
                }
                if(contactsByVendor_bidRequestMap.get(key) != null){
                    for(ContactWrapper cw : contactsByVendor_bidRequestMap.get(key)){
                        contactAuxSelectOptions = contactSelectOption_bidRequestMap.get(key) != null ? contactSelectOption_bidRequestMap.get(key) : new List<SelectOption>();
                        contactAuxSelectOptions.add(new SelectOption(cw.c.Id,cw.c.Name));
                        contactSelectOption_bidRequestMap.put(key,contactAuxSelectOptions.clone());
                    }
                }
                if(contactsByVendor_bidRequestMap.get(key) == null) contactsByVendor_bidRequestMap.put(key,new List<ContactWrapper>());
                if(contactSelectOption_bidRequestMap.get(key) == null) contactSelectOption_bidRequestMap.put(key,new List<SelectOption>());
            }
        }
        for(String key : parentIds){
            if(contactsByVendorParent_bidRequestMap.get(key) == null) contactsByVendorParent_bidRequestMap.put(key,new List<ContactWrapper>());
            if(contactSelectOption_bidRequestMap.get(key) == null) contactSelectOption_bidRequestMap.put(key,new List<SelectOption>());
        }
        Boolean haveDefault;
        for(String key : sendBidRequestMap.keySet()){
            if(contactsByVendor_bidRequestMap.get(key) == null) contactsByVendor_bidRequestMap.put(key,new List<ContactWrapper>());
            if(contactSelectOption_bidRequestMap.get(key) == null) contactSelectOption_bidRequestMap.put(key,new List<SelectOption>());
            
            if(sendBidRequestMap.get(key).Vendor_Contact__c == null){
                haveDefault = false;
                parentId = sendBidRequestMap.get(key).Vendor__r.ParentId;
                parentIdProvider = sendBidRequestMap.get(key).Provider__r.ParentId;
                if(contactsByVendorParent_bidRequestMap.get(parentId) != null){
                    for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(parentId)){
                        if(!haveDefault){
                            cw.selected = true;
                            haveDefault = true;
                        }
                    }
                }
                if(contactsByVendorParent_bidRequestMap.get(parentIdProvider) != null){
                    for(ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(parentIdProvider)){
                        if(!haveDefault){
                            cw.selected = true;
                            haveDefault = true;
                        }
                    }
                }
                if(contactsByVendor_bidRequestMap.get(key) != null){
                    for(ContactWrapper cw : contactsByVendor_bidRequestMap.get(key)){
                        if(!haveDefault){
                            cw.selected = true;
                            haveDefault = true;
                        }
                    }
                }
            }
        }
        sendBidRequestMapSize = sendBidRequestMap.size();
        List<Itinerary__c> itineraries =  [SELECT Id FROM Itinerary__c WHERE GT__c =:tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
        itineraryId = !itineraries.isEmpty() ? itineraries[0].Id : null;

        //getDocumentsByProduction();
        /**
        *  @Conga: Update for Conga.
        */
        User emailFromUser = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripViewId);
        sendBidRequest_emailFromUserId = emailFromUser.Id;
        sendBidRequest_congaEmailFromId = verifyWideAddress(emailFromUser.Email);
        congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
        for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('GT - BidById', 'GT - ContactById', 'GT - SubTripsByBidId', 'GT - ContactsByAccountId', 'GT - ProductionAssociationsByOppId', 'GT - UserById', 'GT - AssociatedCitiesByAccountId')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
        congaQueriesJson = JSON.serialize(congaQueriesMap);
        Map<String, APXTConga4__Conga_Template__c> congaTemplatesMap = new Map<String, APXTConga4__Conga_Template__c>();
        for(APXTConga4__Conga_Template__c congaTemplate:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c in ('GT - Ground Travel Bid', 'GT - Ground Travel Profile')]) congaTemplatesMap.put(congaTemplate.APXTConga4__Name__c, congaTemplate);
        sendBidRequest_congaTemplateId1 = congaTemplatesMap.get('GT - Ground Travel Bid') != null ? congaTemplatesMap.get('GT - Ground Travel Bid').id : null;
        sendBidRequest_congaTemplateId2 = congaTemplatesMap.get('GT - Ground Travel Profile') != null ? congaTemplatesMap.get('GT - Ground Travel Profile').id : null;
        List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id, APXTConga4__Subject__c From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c = 'GT - Bid Request'];
        sendBidRequest_congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        if(!congaEmailTemplates.isEmpty() && String.isNotBlank(congaEmailTemplates[0].APXTConga4__Subject__c)) sendBidRequest_congaEmailSubject = congaEmailTemplates[0].APXTConga4__Subject__c.replace('{OpportunityName}', opportunity.Name).replace('{StartDate}', tripView.Start_Date__c != null ? Datetime.newInstance(tripView.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{EndDate}', tripView.End_Date__c != null ? Datetime.newInstance(tripView.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '');
        else sendBidRequest_congaEmailSubject = 'GROUND TRAVEL BID REQUEST - ' + opportunity.Name + ' - ' + (tripView.Start_Date__c != null ? Datetime.newInstance(tripView.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' - ' + (tripView.End_Date__c != null ? Datetime.newInstance(tripView.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' ({BidName})';
        /**
        *  @/Conga
        */
    }
    
    public void createBidRequest(){
        if(opportunityId != null && opportunityId != '' && selectedVendors != null && selectedVendors != ''  && selectedTrips != null && selectedTrips != ''){
            Set<String> accountIds = new Set<String>();
            for(String sv : selectedVendors.split(',')){
                if(sv.trim() != ''){
                    for(Account vw : searchVendorList){
                        if(vw.Id != null && sv.trim() == String.valueOf(vw.Id)){
                            accountIds.add(vw.Id);
                        }
                    }
                }
            }
            
            Map<String,String> accountContactMap = new Map<String,String>();
            for(Contact c : [SELECT Id, AccountId, Order__c FROM Contact WHERE AccountId IN: accountIds AND Order__c = 1]){
                accountContactMap.put(c.AccountId,c.Id);
            }
            
            Map<String,Account> accMap = new Map<String,Account>();
            for(Account acc : [SELECT Id, ParentId FROM Account WHERE Id IN: accountIds]){
                if(acc.ParentId != null){
                    accountIds.add(acc.ParentId);
                    accMap.put(acc.Id,acc);
                }
            }
            
            /*Map<String,List<Revenue__c>> revenueMap = new Map<String,List<Revenue__c>>();
            List<Revenue__c> revenueListAux;
            for(Revenue__c r : [SELECT Id, of_seats__c, Additional_Fees__c, Base_Cost__c, Bid__c, Breakfast__c, Breakfast_Rate__c, Charge_Type__c, City_Tax_Rate_percent__c, City_Tax_Type__c,
                                City_Tax__c, City_Tax_Rate__c, Client__c, Commission__c, Commission_Percent__c, Commission_Due__c, Commission_Type__c, CurrencyIsoCode, Fee_Dollar__c,
                                Fee_Percent__c, For_Dollar__c, For_Percent__c, Gratuity__c, Invoice_Amount__c, Invoice_Date__c, Invoice_Rate__c, Invoice_Units__c, Or__c, Paid__c, Production__c,
                                Rate_currency__c, Rate__c, Rate_per_person__c, Rate_Type__c, Rebate_currency__c, Rebate__c, Rebate_invoiced_Amount__c, Rebate_Note__c, Rebate_Per__c, Rebate_to_client_Due__c,
                                Rebate_to_RR_Due__c, Revenue_Type__c, Service_Fees__c, Surcharge__c, Surcharge_included__c, Tax__c, Tax_Included__c, Total_Price__c, Total_Taxes__c, VAT__c, VAT_Rate__c, Vendor__c
                                FROM Revenue__c WHERE Vendor__c IN: accountIds AND RecordType.Name = 'Revenue' AND Revenue_Type__c = 'Rebate']){
                                    revenueListAux = revenueMap.get(r.Vendor__c) != null ? revenueMap.get(r.Vendor__c) : new List<Revenue__c>();
                                    revenueListAux.add(r);
                                    revenueMap.put(r.Vendor__c,revenueListAux.clone());
                                }*/
            
            List<Bid__c> bidList = new List<Bid__c>();
            Bid__c b;
            Set<String> tripSelectedIds = new Set<String>();
            for(String tv : selectedTrips.split(',')){
                if(tv.trim() != '') tripSelectedIds.add(tv.trim());
            }
            
            Map<String,String> bidExistMap = new map<String,String>();
            for(Bid__c bExist : [SELECT Id, Vendor__c, GT__c FROM Bid__c WHERE GT__c IN: tripSelectedIds AND Vendor__c <> NULL]){
                bidExistMap.put(bExist.GT__c + '-' + bExist.Vendor__c,bExist.Id);
            }
            
            Map<String,Ground__c> gtExistMap = new Map<String,Ground__c>();
            for(Ground__c gExist : [SELECT Id, Start_City__c FROM Ground__c WHERE Id IN: tripSelectedIds]) gtExistMap.put(gExist.Id,gExist);
            
            Set<String> tripCreateIds = new Set<String>();
            for(String tv : selectedTrips.split(',')){
                if(tv.trim() != ''){
                    for(String sv : selectedVendors.split(',')){
                        if(sv.trim() != ''){
                            if(bidExistMap.get(tv.trim() + '-' + sv.trim()) == null){
                                tripCreateIds.add(tv.trim());
                                for(Account vw : searchVendorList){
                                    if(vw.Id != null && sv.trim() == String.valueOf(vw.Id)){
                                        b = new Bid__c(
                                            RecordTypeId = bid_GTBidRT,
                                            Production__c = opportunityId,
                                            GT__c = tv.trim(),
                                            Vendor__c = vw.Id,
                                            City__c = gtExistMap.get(tv.trim()) != null ? gtExistMap.get(tv.trim()).Start_City__c : null,
                                            CurrencyIsoCode = vw.CurrencyIsoCode,
                                            //Venue__c = (vvw.vv != null && vvMap.get(vvw.vv.Id) != null ? vvMap.get(vvw.vv.Id).Venue__c : null),
                                            Status__c = 'Unsent',
                                            Vendor_Contact__c = accountContactMap.get(vw.Id) != null ? accountContactMap.get(vw.Id) : null
                                            //DX_to_Venue__c = (vvw.vv != null && vvMap.get(vvw.vv.Id) != null ? vvMap.get(vvw.vv.Id).Distance_formula__c : null)
                                        );
                                        bidList.add(b);
                                    }
                                }
                            }
                        }
                    }
                }
            }
            
            //system.debug(bidList);
            bidsCreated = 0;
            if(bidList.size() > 0){
                insert bidList;
                bidsCreated = bidList.size();
      
                Ground__c gAux;
                List<Ground__c> gAuxList;
                Concessions__c cAux;
                List<Concessions__c> cAuxList;
                
                Map<String,List<Ground__c>> vehiclesDataMap = new Map<String,List<Ground__c>>();
                for(Ground__c vData : [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Trip_Vehicle__c, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, GT_Trip_Details__c, Gear_Luggage_Space__c
                                       FROM Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: opportunityId AND GT_Trip_Details__c IN: tripCreateIds
                                       AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL]){
                                           gAuxList = vehiclesDataMap.get(vData.GT_Trip_Details__c) != null ? vehiclesDataMap.get(vData.GT_Trip_Details__c) : new List<Ground__c>();
                                           gAuxList.add(vData);
                                           vehiclesDataMap.put(vData.GT_Trip_Details__c,gAuxList.clone());
                                       }
                
                Map<String,List<Concessions__c>> concessionsDataMap = new Map<String,List<Concessions__c>>();
                for(Concessions__c cData : [SELECT Id, GT__c, Agreed__c, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, CurrencyIsoCode, Notes__c, Order__c
                                                          FROM Concessions__c WHERE GT__c IN: tripCreateIds AND Production__c =: opportunityId AND Create_in_Bid__c = true
                                            AND Bid__c = NULL AND Housing__c = NULL AND Freight__c = NULL]){
                                                cAuxList = concessionsDataMap.get(cData.GT__c) != null ? concessionsDataMap.get(cData.GT__c) : new List<Concessions__c>();
                                                cAuxList.add(cData);
                                                concessionsDataMap.put(cData.GT__c,cAuxList.clone());
                                            }
                
                //TRIPS AND TRAVEL
                Map<String,List<Ground__c>> subtripDataMap = new Map<String,List<Ground__c>>();
                Set<String> subtripDataIds = new Set<String>();
                for(Ground__c subtripData : [SELECT Id, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, GT_Trip_Details__c, GT_Freight__c
                                         FROM Ground__c 
                                         WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND GT_Trip_Details__c IN: tripCreateIds ORDER BY Trip_Order__c ASC]){
                                             subtripDataIds.add(subtripData.Id);
                                             gAuxList = subtripDataMap.get(subtripData.GT_Trip_Details__c) != null ? subtripDataMap.get(subtripData.GT_Trip_Details__c) : new List<Ground__c>();
                                             gAuxList.add(subtripData);
                                             subtripDataMap.put(subtripData.GT_Trip_Details__c,gAuxList.clone());
                                         }
                
                Map<String,List<Ground__c>> travelsBySubTripMapAux = new Map<String,List<Ground__c>>();
                if(subtripDataIds.size() > 0){
                    for(Ground__c g : [SELECT Id, Line__c, Vehicle_Ref__c, Vehicle_Lookup__c, GT_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c,
                                       Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c, Location_Drop_Off_Type__c, Location_Details_Drop_Off__c, Start_Date_Time__c, End_Date_Time__c
                                       FROM Ground__c WHERE RecordType.DeveloperName = 'GT_Travel_Details' AND GT_Sub_Trip_Details__c IN: subtripDataIds ORDER BY Line__c ASC]){
                                           gAuxList = travelsBySubTripMapAux.get(g.GT_Sub_Trip_Details__c) != null ? travelsBySubTripMapAux.get(g.GT_Sub_Trip_Details__c) : new List<Ground__c>();
                                           gAuxList.add(g);
                                           travelsBySubTripMapAux.put(g.GT_Sub_Trip_Details__c,gAuxList.clone());
                                           
                                       }
                }

                gAuxList = new List<Ground__c>();
                cAuxList = new List<Concessions__c>();
                Map<Integer,Ground__c> subtripInsertMap = new Map<Integer,Ground__c>();
                Map<Integer,List<Ground__c>> travelInsertMap = new Map<Integer,List<Ground__c>>();
                Integer cx = 1;
                List<Ground__c> travelListAux = new List<Ground__c>();
                for(Bid__c bid : bidList){
                    if(vehiclesDataMap.get(bid.GT__c) != null){
                        for(Ground__c g : vehiclesDataMap.get(bid.GT__c)){
                            gAux = g.clone();
                            gAux.Trip_Vehicle__c = g.Id;
                            gAux.Id = null;
                            gAux.RecordTypeId = ground_vehicletypeRT;
                            gAux.Production_Ground__c = opportunityId;
                            gAux.GT_Trip_Details__c = null;
                            gAux.Bid__c = bid.Id;
                            gAuxList.add(gAux);
                        }
                    }
                    if(concessionsDataMap.get(bid.GT__c) != null){
                        for(Concessions__c c : concessionsDataMap.get(bid.GT__c)){
                            cAux = c.clone();
                            cAux.Id = null;
                            cAux.Production__c = opportunityId;
                            cAux.Bid__c = bid.Id;
                            cAux.GT__c = null;
                            cAuxList.add(cAux);
                        }
                    }
                    
                    if(subtripDataMap.get(bid.GT__c) != null){
                        for(Ground__c gs : subtripDataMap.get(bid.GT__c)){
                            gAux = gs.clone();
                            gAux.Id = null;
                            gAux.GT_Trip_Details__c = null;
                            gAux.RecordTypeId = ground_GTSubStripDetailsRT;
                            gAux.Production_Ground__c = opportunityId;
                            gAux.Bid_Sub_Trip__c = bid.Id;
                            subtripInsertMap.put(cx,gAux);
                            if(travelsBySubTripMapAux.get(gs.Id) != null){
                                for(Ground__c gs2 : travelsBySubTripMapAux.get(gs.Id)){
                                    gAux = gs2.clone();
                                    gAux.Id = null;
                                    gAux.GT_Trip_Details__c = null;
                                    gAux.RecordTypeId = ground_GTTravelDetailsRT;
                                    gAux.Production_Ground__c = opportunityId;
                                    gAux.Bid_Sub_Trip__c = bid.Id;
                                    gAux.Vehicle_Lookup__c = gs2.Vehicle_Lookup__c;
                                    
                                    travelListAux = travelInsertMap.get(cx) != null ? travelInsertMap.get(cx) : new List<Ground__c>();
                                    travelListAux.add(gAux);
                                    travelInsertMap.put(cx,travelListAux.clone());
                                }
                            }
                            cx++;
                        }
                    }
                }
                
                if(gAuxList.size() > 0) insert gAuxList;
                if(cAuxList.size() > 0) insert cAuxList;
                
                if(subtripInsertMap.size() > 0){
                    insert subtripInsertMap.values();
                    List<Ground__c> travelNewList = new List<Ground__c>();
                    for(Integer ix : subtripInsertMap.keySet()){
                        if(travelInsertMap.get(ix) != null){
                            for(Ground__c gms : travelInsertMap.get(ix)){
                                gms.GT_Sub_Trip_Details__c = subtripInsertMap.get(ix).Id;
                                travelNewList.add(gms);
                            }
                        }
                    }
                    if(travelNewList.size() > 0) insert travelNewList;
                }
            }
            
            getBidsByTrip();
        }
    }
    
    public void searchVendor(){
        vendorFilter = new Account();
        //VendorWrapper.orderFieldVendor = orderFieldVendor;
        detailId = null;
        String strQuery = '';
        searchVendorList = new List<Account>();

        strQuery = 'SELECT Id, Name, Flag_icon__c, Service_Types__c, City__c, City__r.Name, Status__c, CreatedDate, ShippingPostalCode, Preferred_formula__c, CurrencyIsoCode, ShippingState, ShippingStreet, ShippingCountry, ShippingCity ' + 
            ' FROM Account' +
            ' WHERE RecordType.Name IN (\'Ground Travel Vendor\')';
        //if(searchvendor_type != 'multiple') strQuery += ' AND Id NOT IN: vendorNotSelectedIds';
        strQuery += ' AND Id NOT IN: vendorNotSelectedIds';
        //Map<String,VendorWrapper> accAuxMap = new Map<String,VendorWrapper>();
        Boolean enterAirport;
        if(searchvendor_button == 'main'){
            if(searchvendor_status != null && searchvendor_status != '' && searchvendor_status != 'All') strQuery += ' AND Status__c =: searchvendor_status';
            if(searchvendor_data1 == 'vendor'){
                searchvendor_value1 = '%' + searchvendor_value1 + '%';
                strQuery += ' AND Name LIKE: searchvendor_value1';
            }else if(searchvendor_data1 == 'postal_code'){
                if(searchvendor_value1 != null && searchvendor_value1.trim() != ''){
                    searchvendor_value1 = '%' + searchvendor_value1 + '%';
                    strQuery += ' AND ShippingPostalCode LIKE: searchvendor_value1';
                }
            }else if(searchvendor_data1 == 'speed_key'){
                if(searchvendor_value1 != null && searchvendor_value1.trim() != ''){
                    strQuery += ' AND Id =: searchvendor_value1';
                }
            }            
            if(searchvendor_data1 == 'city'){
                if(searchvendor_value1 != null && searchvendor_value1 != ''){
                    searchVendor_CityGoogle = (searchvendor_value1 != null ? (searchvendor_value1 != '%%' ? searchvendor_value1.trim().replace(' ','+') + '+charter+bus+company' : '') : '');
                    searchvendor_value1 = '%' + searchvendor_value1 + '%';
                    //strQuery += ' AND City__r.Name LIKE: searchvendor_value1';
                    strQuery += ' AND Id IN (SELECT Vendor__c FROM Associated_Cities__c WHERE City__c <> NULL AND City__r.Name LIKE: searchvendor_value1)';
                }
            }
            if(searchvendor_value2 != null && searchvendor_value2 != ''){
                if(searchvendor_data2 == 'venue'){
                    searchvendor_value2 = '%' + searchvendor_value2 + '%';
                    strQuery += ' AND Id IN (SELECT Vendor__c FROM Vendor_Venue__c WHERE Venue__c <> NULL AND Venue__r.Name LIKE: searchvendor_value2)';
                }else if(searchvendor_data2 == 'airport_code'){
                    List<String> searchSplit = searchvendor_value2.split(' - ');
                    String str1;
                    String str2;
                    String str3;
                    strQuery += ' AND Id IN (SELECT Vendor__c FROM Vendor_Airport_Association__c WHERE Airport__c <> NULL';
                    if(searchSplit.size() > 0){
                        if(searchSplit.size() == 3){
                            str1 = searchSplit[0] != null ? '%' + searchSplit[0].trim() + '%' : '%%';
                            str2 = searchSplit[1] != null ? '%' + searchSplit[1].trim() + '%' : '%%';
                            str3 = searchSplit[2] != null ? '%' + searchSplit[2].trim() + '%' : '%%';
                            strQuery += ' AND (Airport__r.Airport_Code__c LIKE: str1 OR Airport__r.Name LIKE: str2 OR Airport__r.City__r.Name LIKE: str3)';
                        }else if(searchSplit.size() == 2){
                            str1 = searchSplit[0] != null ? '%' + searchSplit[0].trim() + '%' : '%%';
                            str2 = searchSplit[1] != null ? '%' + searchSplit[1].trim() + '%' : '%%';
                            strQuery += ' AND (Airport__r.Airport_Code__c LIKE: str1 OR Airport__r.Name LIKE: str1 OR Airport__r.City__r.Name LIKE: str1 OR Airport__r.Airport_Code__c LIKE: str2 OR Airport__r.Name LIKE: str2 OR Airport__r.City__r.Name LIKE: str2)';
                        }else{
                            searchvendor_value2 = '%' +  searchvendor_value2 + '%';
                             strQuery += ' AND (Airport__r.Name LIKE: searchvendor_value2 OR Airport__r.Airport_Code__c LIKE: searchvendor_value2)';
                        }
                    }else{
                        searchvendor_value2 = '%' +  searchvendor_value2 + '%';
                        strQuery += ' AND (Airport__r.Name LIKE: searchvendor_value2 OR Airport__r.Airport_Code__c LIKE: searchvendor_value2)';
                    }
                    strQuery += ')';
                }
            }
        }
        else{
            if(searchvendor_vendor != null && searchvendor_vendor != ''){
                searchvendor_vendor = '%' + searchvendor_vendor + '%';
                strQuery += ' AND Name LIKE: searchvendor_vendor';
            }
            if(searchvendor_address != null && searchvendor_address != ''){
                searchvendor_address = '%' + searchvendor_address + '%';
                strQuery += ' AND ShippingStreet LIKE: searchvendor_address';
            }
            if(searchvendor_country != null && searchvendor_country != '') strQuery += ' AND ShippingCountry =: searchvendor_country';
            system.debug(searchvendor_state);
            if(searchvendor_state != null && searchvendor_state != '') strQuery += ' AND ShippingState =: searchvendor_state';
            if(searchvendor_zip != null && searchvendor_zip != '') strQuery += ' AND ShippingPostalCode =: searchvendor_state';
            if(searchvendor_servicetype != null && searchvendor_servicetype.trim() != ''){
                List<String> serviceTypeList = new List<String>();
                for(String s : searchvendor_servicetype.split(',')){
                    if(s.trim() != '') serviceTypeList.add(s.trim());
                }
                strQuery += ' AND Service_Types__c IN: serviceTypeList';
            }
            if(searchvendor_amenities != null && searchVendor_Amenities != ''){
                for(String s : searchvendor_amenities.split(',')){
                    if(s.trim() == 'WiFi') strQuery += ' AND (WiFi_coach__c = \'Yes\' OR WiFi_CV__c = \'Yes\' OR WiFi_motorhome__c = \'Yes\' OR WiFi_star__c = \'Yes\')';
                    if(s.trim() == 'DVD') strQuery += ' AND (DVD__c = \'Yes\' OR DVD_CV__c = \'Yes\')';
                    if(s.trim() == 'Satellite TV') strQuery += ' AND Satellite_TV__c = \'Yes\'';
                    if(s.trim() == 'Outlets In Rows') strQuery += ' AND Outlets_in_Rows__c = \'Yes\'';
                    if(s.trim() == 'Table') strQuery += ' AND Table__c = \'Yes\'';
                    if(s.trim() == 'Trailer Hitch') strQuery += ' AND Trailer_Hitch__c = \'Yes\'';
                    if(s.trim() == 'Trailer') strQuery += ' AND Trailer__c = \'Yes\'';
                    if(s.trim() == 'Restroom') strQuery += ' AND Restroom__c = \'Yes\'';
                    if(s.trim() == 'Executive Coach') strQuery += ' AND Executive_Coach__c = \'Yes\'';
                    if(s.trim() == 'Sleepers') strQuery += ' AND Sleepers__c = \'Yes\'';
                    if(s.trim() == 'Leather Seats') strQuery += ' AND Leather_Seats__c = \'Yes\'';
                    if(s.trim() == 'Mini Bar') strQuery += ' AND Mini_Bar_CV__c = \'Yes\'';
                    if(s.trim() == 'Meet & Greet Services') strQuery += ' AND Meet_Greet_Service__c = \'Yes\'';
                    if(s.trim() == 'Airport Service') strQuery += ' AND Airport_Services__c = \'Yes\'';
                    if(s.trim() == 'Delivery') strQuery += ' AND Delivery__c = \'Yes\'';
                    if(s.trim() == 'Pick Up') strQuery += ' AND Pick_up__c = \'Yes\'';
                    if(s.trim() == 'Direct Bill') strQuery += ' AND Direct_Bill__c = \'Yes\'';
                    if(s.trim() == 'Master Bill Account w/ Credit Card') strQuery += ' AND Master_Bill_Account_w_Credit_Card__c = \'Yes\'';
                    if(s.trim() == 'Age requirement(Yrs)') strQuery += ' AND Age_Requirement_yrs__c = \'Yes\'';
                    if(s.trim() == 'Rental Insurance Options') strQuery += ' AND Rental_Insurance_Options__c = \'Yes\'';
                    if(s.trim() == 'Direct/Satellite TV') strQuery += ' AND Direct_Satellite_TV__c = \'Yes\'';
                    if(s.trim() == 'Fax') strQuery += ' AND Fax__c = \'Yes\'';
                    if(s.trim() == 'Make Up Area') strQuery += ' AND (Make_Up_Area__c = \'Yes\' OR Make_Up_Area_star__c = \'Yes\')';
                    if(s.trim() == 'Shampoo Sink') strQuery += ' AND Shampoo_sink__c = \'Yes\'';
                    if(s.trim() == 'Desk/Office Space') strQuery += ' AND Desk_Office_space__c = \'Yes\'';
                    if(s.trim() == 'Star Lounge') strQuery += ' AND Star_lounge__c = \'Yes\'';
                    if(s.trim() == 'Restrooms') strQuery += ' AND (Restrooms_motorhome__c = \'Yes\' OR Restrooms_star__c = \'Yes\')';
                    if(s.trim() == 'Ironing Board') strQuery += ' AND Ironing_board__c = \'Yes\'';
                    if(s.trim() == 'Stereo System') strQuery += ' AND Stereo_System__c = \'Yes\'';
                    if(s.trim() == 'Refrigerator') strQuery += ' AND (Refrigerator__c = \'Yes\' OR Refrigerator_star__c = \'Yes\' OR Refrigerator_motorhome__c = \'Yes\')';
                    if(s.trim() == 'Microwave') strQuery += ' AND (Microwave__c = \'Yes\' OR Microwave_motorhome__c = \'Yes\' OR Microwave_star__c = \'Yes\')';                  
                    if(s.trim() == 'Wet Bar') strQuery += ' AND (Wet_bar__c = \'Yes\' OR Wet_bar_star__c = \'Yes\')';
                    if(s.trim() == 'Wardrobe Rack') strQuery += ' AND (Wardrobe_Rack__c = \'Yes\' OR Wardrobe_Rack_star__c = \'Yes\')';
                    if(s.trim() == 'Other Resources/Amenities') strQuery += ' AND Other_Resources_Amenities__c = \'Yes\'';
                    if(s.trim() == 'Lounge Area') strQuery += ' AND Lounge_Area__c = \'Yes\'';
                    if(s.trim() == 'Bedroom') strQuery += ' AND Bedroom_star__c = \'Yes\'';
                    if(s.trim() == 'Direct TV/Satellite TV') strQuery += ' AND Direct_TV_Satellite_TV__c = \'Yes\'';
                    if(s.trim() == 'Shower') strQuery += ' AND Shower_star__c = \'Yes\'';
                    if(s.trim() == 'GPS') strQuery += ' AND GPS__c = \'Yes\'';
                    if(s.trim() == 'Child Seat') strQuery += ' AND Child_Seat__c = \'Yes\'';
                }
            }
            
            if((searchvendor_city != null && searchvendor_city != '') || (searchvendor_venue != null && searchvendor_venue != '') || (searchvendor_airportcode != null && searchvendor_airportcode != '')){
                if(searchvendor_city != null && searchvendor_city != ''){
                    searchVendor_CityGoogle = (searchvendor_city != null ? (searchvendor_city != '%%' ? searchvendor_city.trim().replace(' ','+') + '+charter+bus+company' : '') : '');
                    searchvendor_city = '%' + searchvendor_city + '%';
                    //strQuery += ' AND City__r.Name LIKE: searchvendor_city';
                    strQuery += ' AND Id IN (SELECT Vendor__c FROM Associated_Cities__c WHERE City__c <> NULL AND City__r.Name LIKE: searchvendor_city)';
                }
                if(searchvendor_venue != null && searchvendor_venue != ''){
                    strQuery += ' AND Id IN (SELECT Vendor__c FROM Vendor_Venue__c WHERE Venue__c <> NULL AND Venue__r.Name LIKE: searchvendor_venue)';
                }
                if(searchvendor_airportcode != null && searchvendor_airportcode != ''){
                    List<String> searchSplit = searchvendor_airportcode.split(' - ');
                    String str1;
                    String str2;
                    String str3;
                    strQuery += ' AND Id IN (SELECT Vendor__c FROM Vendor_Airport_Association__c WHERE Airport__c <> NULL';
                    if(searchSplit.size() > 0){
                        if(searchSplit.size() == 3){
                            str1 = searchSplit[0] != null ? '%' + searchSplit[0].trim() + '%' : '%%';
                            str2 = searchSplit[1] != null ? '%' + searchSplit[1].trim() + '%' : '%%';
                            str3 = searchSplit[2] != null ? '%' + searchSplit[2].trim() + '%' : '%%';
                            strQuery += ' AND (Airport__r.Airport_Code__c LIKE: str1 OR Airport__r.Name LIKE: str2 OR Airport__r.City__r.Name LIKE: str3)';
                        }else if(searchSplit.size() == 2){
                            str1 = searchSplit[0] != null ? '%' + searchSplit[0].trim() + '%' : '%%';
                            str2 = searchSplit[1] != null ? '%' + searchSplit[1].trim() + '%' : '%%';
                            strQuery += ' AND (Airport__r.Airport_Code__c LIKE: str1 OR Airport__r.Name LIKE: str1 OR Airport__r.City__r.Name LIKE: str1 OR Airport__r.Airport_Code__c LIKE: str2 OR Airport__r.Name LIKE: str2 OR Airport__r.City__r.Name LIKE: str21)';
                        }else{
                            searchvendor_airportcode = '%' + searchvendor_airportcode + '%';
                            strQuery += ' AND (Airport__r.Name LIKE: searchvendor_airportcode OR Airport__r.Airport_Code__c LIKE: searchvendor_airportcode)';
                        }
                    }else{
                        searchvendor_airportcode = '%' + searchvendor_airportcode + '%';
                        strQuery += ' AND (Airport__r.Name LIKE: searchvendor_airportcode OR Airport__r.Airport_Code__c LIKE: searchvendor_airportcode)';
                    }
                    strQuery += ')';
                }
            }
        }
        
        if(orderCheckVendor){
            if(orderChangeVendor){ orderOrientationVendor = 'ASC';
            }else{ if(orderOrientationVendor == 'ASC') orderOrientationVendor = 'DESC'; else orderOrientationVendor = 'ASC';}
        }
        orderCheckVendor = false;
        
        Integer totalRecordsVendor = Database.countQuery('Select count() from Account WHERE' + strQuery.substringAfter('WHERE'));
        totalPagesVendor = totalRecordsVendor != null && totalRecordsVendor == 0 ? 1 : Integer.valueOf((totalRecordsVendor/Decimal.valueOf(limitVendor)).round(System.RoundingMode.UP));
        if(String.isBlank(searchTypeVendor)){
            strQuery += ' ORDER BY ' + orderFieldVendor + ' ' + orderOrientationVendor + ' NULLS LAST' + ', Id LIMIT :limitVendor';
            searchVendorList = Database.query(strQuery);
            offsetVendor = null;
        }
        else{
            if(searchTypeVendor == 'next'){
                offsetVendor = (offsetVendor != null ? offsetVendor : 0) + limitVendor;
                strQuery += ' AND (' + orderFieldVendor + (orderOrientationVendor == 'ASC' ? ' >' : ' <') + ':lastValueOfSortedFieldVendor OR (' + orderFieldVendor  + ' =:lastValueOfSortedFieldVendor AND Id >:lastIdVendor)) ORDER BY ' + orderFieldVendor + ' ' + orderOrientationVendor + ' NULLS LAST' + ', Id LIMIT :limitVendor';
                searchVendorList = Database.query(strQuery);
            }
            else if(searchTypeVendor == 'previous'){
                offsetVendor = (offsetVendor != null ? offsetVendor : 0) - limitVendor;
                strQuery += ' AND (' + orderFieldVendor + (orderOrientationVendor == 'ASC' ? ' <' : ' >') + ':firstValueOfSortedFieldVendor OR (' + orderFieldVendor  + ' =:firstValueOfSortedFieldVendor AND Id <:firstIdVendor)) ORDER BY ' + orderFieldVendor + ' ' + (orderOrientationVendor == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT :limitVendor';
                searchVendorList = Database.query(strQuery);
                List<Account> gtVendors = new List<Account>();
                for(Integer i = searchVendorList.size() - 1; i >= 0; i--) gtVendors.add(searchVendorList[i]);
                searchVendorList = gtVendors;
            } 
            else if(searchTypeVendor == 'first'){
                offsetVendor = null;
                strQuery += ' ORDER BY ' + orderFieldVendor + ' ' + orderOrientationVendor + ' NULLS LAST' + ', Id LIMIT :limitVendor';
                searchVendorList = Database.query(strQuery);
            } 
            else if(searchTypeVendor == 'last'){
                offsetVendor = limitVendor * (Integer.valueOf((totalRecordsVendor / Decimal.valueOf(limitVendor)).round(System.RoundingMode.CEILING)) - 1);
                strQuery += ' ORDER BY ' + orderFieldVendor + ' ' + (orderOrientationVendor == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT ' + String.valueOf(totalRecordsVendor - offsetVendor);
                searchVendorList = Database.query(strQuery);
                List<Account> gtVendors = new List<Account>();
                for(Integer i = searchVendorList.size() - 1; i >= 0; i--) gtVendors.add(searchVendorList[i]);
                searchVendorList = gtVendors;
            } 
        }
        firstIdVendor = !searchVendorList.isEmpty() ? searchVendorList[0].Id : null;
        lastIdVendor = !searchVendorList.isEmpty() ? searchVendorList[searchVendorList.size() - 1].Id : null;
        //firstValueOfSortedFieldVendor = !searchVendorList.isEmpty() ? searchVendorList[0].get(orderFieldVendor) : null;
        //lastValueOfSortedFieldVendor = !searchVendorList.isEmpty() ? searchVendorList[searchVendorList.size() - 1].get(orderFieldVendor) : null;
        firstValueOfSortedFieldVendor = !searchVendorList.isEmpty() ? (orderFieldVendor == 'City__r.Name' ? searchVendorList[0].City__r.Name : searchVendorList[0].get(orderFieldVendor)) : null;
        lastValueOfSortedFieldVendor = !searchVendorList.isEmpty() ? (orderFieldVendor == 'City__r.Name' ? searchVendorList[searchVendorList.size() - 1].City__r.Name : searchVendorList[searchVendorList.size() - 1].get(orderFieldVendor)) : null;
        searchTypeVendor = null;
    }
    
    public void saveEditBid(){
        if(bid_id != null && bid_id.trim() != ''){           
            Bid__c bidTemp;
            Integer orderOld;
            Integer orderNow;
            for(BidWrapper bw : bidsByTripShowList){
                if(bw.b.Id == bid_id){
                    orderOld = Integer.valueOf(bw.b.Options__c);
                    bw.b.Options__c = (bid_option != null ? (bid_option != 0 ? bid_option : null) : null);
                    Bid__c b = new Bid__c(Id = bid_id,Internal_Notes__c = bid_notes,Options__c = (bid_option != null ? (bid_option != 0 ? bid_option : null) : null));
                    orderNow = Integer.valueOf(b.Options__c);
                    bw.option_original = b.Options__c != null ? b.Options__c : 999999;
                    bw.options = Integer.valueOf(b.Options__c);
                    if(b.Options__c != null){
                        b.Include_in_options__c = true;
                    }
                    update b;
                    break;
                }
            }
            List<Bid__c> bidUpdateList = new List<Bid__c>();
            
            BidWrapper.orderFieldBid = 'option_original';
            BidWrapper.orderOrientationBid = 'ASC';
            bidsByTripShowList.sort();

            Integer i = 1;
            //system.debug('orderNow: ' + orderNow);
            //system.debug('orderOld: ' + orderOld);

            List<Contact> contactList = new List<Contact>();
            for(BidWrapper bw : bidsByTripShowList){
                //system.debug('------');
                //system.debug('bw.b.Options__c: ' + bw.b.Options__c);
                if(bw.b.Options__c != null){
                    if(bw.b.Id != bid_id){
                        //system.debug('i: '+i);
                        //system.debug('bw.option_original: '+ bw.option_original);
                        if(i == orderNow){
                            if(orderOld != null && bw.option_original >= orderOld){
                                bw.b.Options__c = i - 1;
                                //system.debug('enter 1');
                            }else{
                                bw.b.Options__c = i + 1;
                                //system.debug('enter 2');
                            }
                            //system.debug('new: '+bw.b.Options__c);
                            bidUpdateList.add(bw.b);
                        }else{
                            system.debug('enter 3');
                            bw.b.Options__c = i;
                            //system.debug('new: '+bw.b.Options__c);
                            bidUpdateList.add(bw.b);
                        }
                    }
                    i++;
                }
            }
            
            /*for(Bid__c bsd : bidUpdateList){
                system.debug(bsd);
            }*/
            if(!bidUpdateList.isEmpty()) update bidUpdateList;
            refreshBidData = true;
            orderFieldBid = 'initial';
            BidWrapper.orderFieldBid = 'initial';
            BidWrapper.orderOrientationBid = 'ASC';
            getBidsByTrip();
        }
    }
    
    /** PAGINATION **/
    /*public void FirstPageBids()
    {
        bidsByTripShowList.clear();
        OffsetSizeBids = 0;
        if((OffsetSizeBids + LimitSizeBids) <= totalRecsBids){
            for(Integer i=0;i<LimitSizeBids;i++){
                bidsByTripShowList.add(bAuxWrapper.get(i));
            }  
            
        } else{
            for(Integer i=0;i<totalRecsBids;i++){
                bidsByTripShowList.add(bAuxWrapper.get(i));
            }      
            
        }
        getprevBids();
        getnxtBids();
    }
    
    public void previousBids()
    {
        bidsByTripShowList.clear();
		OffsetSizeBids = OffsetSizeBids - LimitSizeBids;      
       
        for(Integer i=OffsetSizeBids;i<(OffsetSizeBids+LimitSizeBids); i++){
            bidsByTripShowList.add(bAuxWrapper.get(i));
        }
        getprevBids();
        getnxtBids();
    }
    
    public void nextBids()
    {
        bidsByTripShowList.clear();
        OffsetSizeBids = OffsetSizeBids + LimitSizeBids;
        if((OffsetSizeBids + LimitSizeBids) <= totalRecsBids){
            for(Integer i=OffsetSizeBids;i<(OffsetSizeBids+LimitSizeBids);i++){
                bidsByTripShowList.add(bAuxWrapper.get(i));
            }
            
        } else{
            for(Integer i=OffsetSizeBids;i<totalRecsBids;i++){
                bidsByTripShowList.add(bAuxWrapper.get(i));
            }
        }
        system.debug(OffsetSizeBids);
        getprevBids();
        getnxtBids();
    }
    
    public void LastPageBids()
    {
        bidsByTripShowList.clear();
        if(math.mod(totalRecsBids , LimitSizeBids) == 0){
            OffsetSizeBids = LimitSizeBids * ((totalRecsBids/LimitSizeBids)-1);
        } else if (math.mod(totalRecsBids , limitSizeBids) != 0){
            OffsetSizeBids = LimitSizeBids * ((totalRecsBids/LimitSizeBids));
        }

        for(Integer i=OffsetSizeBids;i<totalRecsBids;i++){
            bidsByTripShowList.add(bAuxWrapper.get(i));
        }
        getprevBids();
        getnxtBids();
    }
    
    public void getprevBids()
    {
        if(OffsetSizeBids == 0) prevShowBid = true; else prevShowBid = false;
    }
    
    public void getnxtBids()
    {
        if((OffsetSizeBids + LimitSizeBids) >= totalRecsBids) nextShowBid = true; else nextShowBid = false;
    }*/
    /** END PAGINATION **/
    
    public void getBidsByTrip(){
        if(opportunityId != null && opportunityId != '' && tripViewId != null && tripViewId != ''){
            /*if(refreshBidData) tripBidNumber = null;
            else refreshBidData = true;*/
            tripview_option = 0;
            BidWrapper.orderFieldBid = orderFieldBid;
            totalRecsBids = 0;
            OffsetSizeBids = 0;
            bidsByTripShowList = new List<BidWrapper>();
            bidByTripIds = new List<String>();
            vendorNotSelectedIds = new Set<String>();
            String strQuery = 'SELECT Id, GT__c, Vendor__c, Vendor__r.Name, Vendor__r.Flag_icon__c, Status__c, Options__c, CreatedDate, Locked__c, Internal_notes__c, No_Bid_reason__c,' +
                ' Vendor__r.ShippingStreet, Vendor__r.ShippingState, Vendor__r.ShippingCity, Vendor__r.ShippingCountry, Vendor__r.ShippingPostalCode, Production__c,' +
                ' Vendor__r.BillingStreet, Vendor__r.BillingState, Vendor__r.BillingCity, Vendor__r.BillingCountry, Vendor__r.BillingPostalCode, GT__r.Status_Ground__c, GT__r.Status_Previous__c, Status_Previous__c' +
                ' FROM Bid__c WHERE GT__c =: tripViewId';
            bAuxWrapper = new List<BidWrapper>();
            vendorsJson = '[]';
            Map<String,String> vendorMap = new Map<String,String>();
            BidWrapper bwAux;
            for(Bid__c b : Database.query(strQuery)){
                if(b.Vendor__c != null) vendorNotSelectedIds.add(b.Vendor__c);
                if(b.Status__c != 'Deactivated Bid'){
                    bidByTripIds.add(b.Id);
                    if(b.Options__c != null && b.Options__c > tripview_option) tripview_option = Integer.valueOf(b.Options__c);
                    if(b.Vendor__c != null) vendorMap.put(b.Vendor__c,b.Vendor__r.Name);
                    bwAux = new BidWrapper(
                        b,
                        b.Vendor__r.Flag_icon__c,
                        b.Vendor__c != null ? b.Vendor__r.Name : '',
                        b.Status__c,
                        null,
                        b.Internal_notes__c != null ? b.Internal_notes__c : '',
                        (b.Options__c != null ? b.Options__c : 999999),
                        b.CreatedDate.date(),
                        b.Options__c != null ? b.Options__c : 999999
                    );
                    
                    bwAux.orderfix = (b.Status__c != 'Sold Out / Not Bidding' ? (b.Options__c != null ? String.valueOf(b.Options__c) : 'W' + b.Status__c) : 'Z' + (b.Options__c != null ? String.valueOf(b.Options__c) : ''));
                    //bAuxWrapper.add(bwAux);
                    bidsByTripShowList.add(bwAux);
                }
            }
            tripview_option++;
            
            symbolMap = new Map<String,String>();
            symbolMap.put(null,'');
            Map<String,Revenue__c> ratesMap = new Map<String,Revenue__c>();
            for(Revenue__c r : [Select id, Base_Cost__c, Commission__c, Rate__c, Gratuity__c, Total_Price__c, CurrencyIsoCode, Bid__c from Revenue__c where Bid__c IN: bidByTripIds and RecordType.DeveloperName = 'Ground_Rate_Travel_Commission' order by createdDate ASC]){
                ratesMap.put(r.Bid__c,r);
                symbolMap.put(r.CurrencyIsoCode,'');
            }
            
            List<wrapperVendor> wrapperVendorList = new List<wrapperVendor>();
            for(String vk : vendorMap.keySet()) wrapperVendorList.add(new wrapperVendor(vk,vendorMap.get(vk)));
            vendorsJson = JSON.serialize(wrapperVendorList);
            
            if(orderOrientationBid == null){
                orderOrientationBid = 'ASC';
                BidWrapper.orderOrientationBid = 'ASC';
            }
            else BidWrapper.orderOrientationBid = orderOrientationBid;
            if(orderCheckBid){
                if(orderChangeBid){
                    orderOrientationBid = 'ASC';
                    BidWrapper.orderOrientationBid = 'ASC';
                }else{
                    if(orderOrientationBid == 'ASC'){
                        orderOrientationBid = 'DESC';
                        BidWrapper.orderOrientationBid = 'DESC';
                    }else{
                        orderOrientationBid = 'ASC';
                        BidWrapper.orderOrientationBid = 'ASC';
                    }
                }
            }
            
            for(BidWrapper bw : bidsByTripShowList){
                bw.rate = ratesMap.get(bw.b.Id) != null && ratesMap.get(bw.b.Id).Total_Price__c != null ? ratesMap.get(bw.b.Id).Total_Price__c : null;
                bw.currency_code = ratesMap.get(bw.b.Id) != null && ratesMap.get(bw.b.Id).CurrencyIsoCode != null ? ratesMap.get(bw.b.Id).CurrencyIsoCode : 'USD';
                symbolMap.put(bw.currency_code,'');
            }
            getSymbol();

            totalRecsBids = bidsByTripShowList.size();
            bidsByTripShowList.sort();
            Integer p = 1;
            bidDataMap = new Map<Integer,BidWrapper>();
            for(BidWrapper bw : bidsByTripShowList){
                system.debug(bw);
                bw.numberz = p;
                bidDataMap.put(p,bw);
                if(dataBidIdsearch != null && dataBidIdsearch == bw.b.Id){
                    system.debug(p);
                    tripBidNumber = p;
                }
                p++;
            }
            dataBidIdsearch = null;

            gtDashboard.bidDataMap = bidDataMap;
            
            /*if((OffsetSizeBids + LimitSizeBids) <= totalRecsBids){
                for(Integer i = 0; i<LimitSizeBids; i++)
                    bidsByTripShowList.add(bAuxWrapper.get(i));
                
            }else{
                for(Integer i=0;i<totalRecsBids;i++)
                    bidsByTripShowList.add(bAuxWrapper.get(i));
            }*/
            
            if(refreshBidData){
                //getConcessionsByTrip();
                //getVehiclesByTrip();
                //getSubStripByTrip();
            }
            
            //getprevBids();
            //getnxtBids();
        }
    }
    
    public void createJournal(){
        if(journalIdActual != null && journalIdActual != '' && journalView.Id != null){
            upsert new Journal__c(Id=(journalChildIdActual != '' ? journalChildIdActual : null),RecordTypeId=journal_tripJournalRT,Parent_Journal__c=journalIdActual,Journal_Entry__c=newJournalChildEntry,Production__c=journalView.Production__c,G__c=journalView.G__c);
        }
        journalIdActual = null;
        journalChildIdActual = null;
        newJournalChildEntry = null;
        searchTripJournalsByGT();
    }
    
    public void viewReplyJournal(){
        journalView = new Journal__c();
        journalChildView = new Journal__c();
        if(journalIdActual != null && journalIdActual != '') journalView = [SELECT Id, Name, Journal_Entry__c, CreatedDate, CreatedBy.Name, Production__c, G__c FROM Journal__c WHERE Id =: journalIdActual];
        if(journalChildIdActual != null && journalChildIdActual != '') journalChildView = [SELECT Id, Name, Journal_Entry__c, CreatedDate, CreatedBy.Name, Production__c, G__c FROM Journal__c WHERE Id =: journalChildIdActual];
    }
    
    public void searchTripJournalsByGT(){
        if(tripViewId != null && tripViewId != ''){
            journalByTripList = new List<Journal__c>();
            journalByTripMap = new Map<String,List<Journal__c>>();
            List<Journal__c> journalListAux;
            String strQuery = 'SELECT Id, Name, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, G__c, Parent_Journal__c, Bid__c FROM Journal__c WHERE G__c =: tripViewId AND Parent_Journal__c = NULL';
            if(checkIssue && checkSales){
                strQuery += ' AND (Issue__c = true OR Sales__C = true)';
            }else{
                if(checkIssue != null && checkIssue) strQuery += ' AND Issue__c = true';
                if(checkSales != null && checkSales) strQuery += ' AND Sales__c = true';
            }
            strQuery += ' ORDER BY CreatedDate DESC';
            
            Set<String> journalParentIds = new Set<String>();
            Boolean wordSearch;
            for(Journal__c j : Database.query(strQuery)) 
            {
                wordSearch = true;
                if(tripJournalSearch != null && tripJournalSearch != '' && j.Journal_Entry__c != null && !j.Journal_Entry__c.containsIgnoreCase(tripJournalSearch)) wordSearch = false;
                if(wordSearch){
                    journalParentIds.add(j.Id);
                    journalByTripList.add(j);
                }
            }
            
            strQuery = 'SELECT Id, Name, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, G__c, Parent_Journal__c, Bid__c FROM Journal__c WHERE G__c =: tripViewId AND Parent_Journal__c IN: journalParentIds ORDER BY CreatedDate DESC';
            for(Journal__c j : Database.query(strQuery)) 
            {
                wordSearch = true;
                if(tripJournalSearch != null && tripJournalSearch != '' && j.Journal_Entry__c != null && !j.Journal_Entry__c.containsIgnoreCase(tripJournalSearch)) wordSearch = false;
                if(wordSearch){
                    journalListAux = journalByTripMap.get(j.Parent_Journal__c) != null ? journalByTripMap.get(j.Parent_Journal__c) : new List<Journal__c>();
                    journalListAux.add(j);
                    journalByTripMap.put(j.Parent_Journal__c,journalListAux.clone());
                }
            }
            
            for(Journal__c j : journalByTripList){
                if(journalByTripMap.get(j.Id) == null) journalByTripMap.put(j.Id,new List<Journal__c>());
            }
        }
    }
    
    public void viewTripJournals(){
        newtrip = new Ground__c();
        if(tripViewId != null && tripViewId != ''){
            journalByTripList = new List<Journal__c>();
            journalByTripMap = new Map<String,List<Journal__c>>();
            List<Journal__c> journalListAux;
            for(Journal__c j : [SELECT Id, Name, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, G__c, Parent_Journal__c, Bid__c FROM Journal__c WHERE G__c =: tripViewId ORDER BY CreatedDate DESC]){
                if(j.Parent_Journal__c == null){
                    journalByTripList.add(j);
                }else{
                    journalListAux = journalByTripMap.get(j.Parent_Journal__c) != null ? journalByTripMap.get(j.Parent_Journal__c) : new List<Journal__c>();
                    journalListAux.add(j);
                    journalByTripMap.put(j.Parent_Journal__c,journalListAux.clone());
                }
            }
            
            for(Journal__c j : journalByTripList){
                if(journalByTripMap.get(j.Id) == null) journalByTripMap.put(j.Id,new List<Journal__c>());
            }
        }
    }
    
    public void editDocumentTitle() {
        if(documentId != null && documentId != ''){
            update new ContentDocument(Id = documentId, Title = documentTitle);
            //for(ContentDocument document : documentBidList) if(document.Id == documentId) document.Title = documentTitle;
            for(ContentDocument document : documentTripList) if(document.Id == documentId) document.Title = documentTitle;
            documentId = '';
            documentTitle = '';
        }
    }
       
    public void deleteDocument(){
        if(documentIdActual != null && documentIdActual != ''){
            delete [SELECT Id FROM ContentDocument WHERE Id =: documentIdActual];
            getDocumentsByTrip();
        }
    }
    
    public void doAttachment(){
        system.debug(filename);
        system.debug(bodytrip);
        system.debug(documentRelationId);
        if(filename != null && bodytrip != null){
            try{
                ContentVersion conVer = new ContentVersion();
                conVer.PathOnClient = '/'+filename;
                conVer.Title = filename.split('\.')[0];
                conVer.VersionData = (!Test.isRunningTest() ? EncodingUtil.base64Decode(bodytrip.subString(0,100).split(',')[1] + bodytrip.substring(100,bodytrip.length())) : Blob.valueOf('Test'));
                insert conVer;
                
                Id conDoc = [SELECT ContentDocumentId FROM ContentVersion WHERE Id =:conVer.Id].ContentDocumentId;
                
                //Create ContentDocumentLink
                ContentDocumentLink cDe = new ContentDocumentLink();
                cDe.ContentDocumentId = conDoc;
                cDe.LinkedEntityId = documentRelationId;
                cDe.ShareType = 'V';
                cDe.Visibility = 'AllUsers';
                insert cDe;
            }catch(Exception e){
                system.debug(e.getMessage());
            }finally {
                bodytrip = null;
                filename = null;
            }
        }
        getDocumentsByTrip();
    }
    
    public void getDocumentsByTrip(){
        documentTripList = new List<ContentDocument>();
        if(tripViewId != null && tripViewId != ''){
            Set<String> entityIds = new Set<String>();
            for(Bid__c bid : [SELECT Id FROM Bid__c WHERE GT__c =: tripViewId]) entityIds.add(bid.Id);
            entityIds.add(tripViewId);
            Set<String> contentDocumentIds = new Set<String>();
            for(ContentDocumentLink cdl : [SELECT Id, LinkedEntityId, ContentDocumentId FROM ContentDocumentLink WHERE LinkedEntityId IN: entityIds]) contentDocumentIds.add(cdl.ContentDocumentId);
            documentTripList = [SELECT Id, Title, FileExtension, CreatedDate FROM ContentDocument WHERE Id IN: contentDocumentIds];
        }
    }
    
    public void viewTripDetail(){
        if(tripViewId != null && tripViewId != ''){
            tripView = [SELECT Id, Name, Description__c, Start_Date__c, End_Date__c, Group_Type__c, Amenities__c, Service_Type__c, Trace_Date__c, Status__c, Status_Ground__c, Deadline_Date__c,
                        Vendor_lookup__c, Vendor_lookup__r.City__r.Name, Vendor_lookup__r.City__c, Start_City__c, Start_City__r.Name, RecordTypeId, RecordType.Name, Back_end_Coordinator__c, Back_end_Coordinator__r.Name,
                        (SELECT Id, Client_Notes__c FROM Itinerary__r)
                        FROM Ground__c WHERE Id =: tripViewId];
            clientByProduction = new Contact();
            Map<String,String> contactAuxMap = new Map<String,String>();
            Map<String,String> userAuxMap = new Map<String,String>();
            if(tripView.Back_end_Coordinator__c != null) userAuxMap.put(tripView.Back_end_Coordinator__c,tripView.Back_end_Coordinator__r.Name);
            coordinatorGT = null;
            coordinatorGTName = null;
            tabGroundDefault = 'trip_bids';
            for(Production_Associations__c pa : [SELECT Id, Production_Opp__c, Ground__c, Contact__c, Contact__r.Name, Contact__r.Title, Contact__r.Order__c, Contact__r.Email, Contact__r.Phone, Contact__r.MobilePhone, User__c, Team_Roles__c, User__r.Name, Role__c FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId OR Ground__c =: tripViewId ORDER BY Contact__r.Name ASC]){
                if(pa.Production_Opp__c != null){
                    if(pa.Contact__c != null && pa.Role__c != null && (pa.Role__c.contains('Primary GT') || pa.Role__c.contains('CC: GT'))){
                        contactAuxMap.put(pa.Contact__c,pa.Contact__r.Name);
                        if(pa.Role__c.contains('Primary GT')) clientByProduction = new Contact(Id = pa.Contact__c, Email = pa.Contact__r.Email, Title = pa.Contact__r.Title,Phone = pa.Contact__r.Phone,MobilePhone = pa.Contact__r.MobilePhone);
                    }
                    if(pa.User__c != null){
                        userAuxMap.put(pa.User__c,pa.User__r.Name);
                        if(pa.Team_Roles__c != null){
                            if(pa.Team_Roles__c.contains('Primary GT Coordinator')){
                                coordinatorGT = pa.User__c;
                                coordinatorGTName = pa.User__r.Name;
                            }
                        }
                    }
                }
            }
            
            clientsByProduction = new List<SelectOption>();
            clientsByProduction.add(new SelectOption('',''));
            for(String k1 : contactAuxMap.keySet()){
                clientsByProduction.add(new SelectOption(k1,contactAuxMap.get(k1)));
            }
            
            teamMembers = new List<SelectOption>();
            teamMembers.add(new SelectOption('','-- Not Assigned --'));
            Map<Id,Profile> profileIds = new Map<id,profile>([SELECT Id,UserLicenseId FROM Profile where UserLicenseId  in (SELECT Id FROM UserLicense where name ='Salesforce')]);
            for(User k1 : [SELECT Id, Name FROM User WHERE isActive = true AND ProfileId IN: profileIds.Keyset() ORDER BY Name ASC]){
                teamMembers.add(new SelectOption(k1.Id,k1.Name));
            }
            
            getBidsByTrip();
            getConcessionsByTrip();
            getVehiclesByTrip();
            getSubStripByTrip();
            
            statusItineraryPL = new List<SelectOption>();
            statusItineraryPL.add(new SelectOption('','-- Select --'));
            statusItineraryPL.add(new SelectOption('Itinerary Received','Itinerary Received'));
            statusItineraryPL.add(new SelectOption('Bid Request Stage','Bid Request Stage'));
            statusItineraryPL.add(new SelectOption('Presenter/Promoter Provided','Presenter/Promoter Provided'));
            statusItineraryPL.add(new SelectOption('Pending Client Choice','Pending Client Choice'));
            statusItineraryPL.add(new SelectOption('Budgeting','Budgeting'));
            statusItineraryPL.add(new SelectOption('Cancelled','Cancelled'));
            statusItineraryPL.add(new SelectOption('Contracted on Own','Contracted on Own'));
            statusItineraryPL.add(new SelectOption('Layoff','Layoff'));
            statusItineraryPL.add(new SelectOption('Pending Trip Information','Pending Trip Information'));
            statusItineraryPL.add(new SelectOption('Pending Airport Confirmation','Pending Airport Confirmation'));
            statusItineraryPL.add(new SelectOption('Send to Client','Send to Client'));
            
            Boolean addValue = true;
            for(SelectOption so : statusItineraryPL){
                if(tripView.Status_Ground__c == so.getValue()) addValue = false;
            }
            if(addValue && tripView.Status_Ground__c != null) statusItineraryPL.add(new SelectOption(tripView.Status_Ground__c,tripView.Status_Ground__c));
            /**
            *  @Conga: Update for Conga.
            */
            congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
            for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('GT - BidsWithOptionsByGroundTravel', 'GT - SubTripsByTripId', 'GT - ContactById', 'GT - ProductionAssociationsByOppId', 'GT - UserById')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
            sendOptions_congaQueriesJson = JSON.serialize(congaQueriesMap);
            List<APXTConga4__Conga_Template__c> congaTemplates = [Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c = 'GT - Ground Travel Options'];
            sendOptions_congaTemplateId = !congaTemplates.isEmpty() ? congaTemplates[0].id : null;
            /**
            *  @/Conga
            */
        }
    }
    
    public void searchTrip(){
        clearListTabs();
        //TripWrapper.orderFieldTrip = orderFieldTrip;
        
        Set<String> tournamentIds = new Set<String>();
        String strQuery = 'SELECT Id, Production_Ground__c, Name, Vendor_lookup__c, Vendor_lookup__r.Name, Start_Date__c, End_Date__c, Description__c, Service_Type__c, Group_Type__c, Status_Ground__c, Deadline_Date__c, Service_Type_Text__c'+
            ' FROM Ground__c WHERE Production_Ground__c =: opportunityId AND RecordType.Name = \'GT Trip Details\'';

        Date tdy = system.today();
        if(!trip_showprior){
            strQuery += ' AND Start_Date__c >=: tdy';
        }else{
            //if(trip_startdate != null) strQuery += ' AND Start_Date__c >=: trip_startdate';
            //if(trip_enddate != null) strQuery += ' AND End_Date__c <=: trip_enddate';
            if(trip_startdate != null && trip_enddate != null){
                if(trip_startdate == trip_enddate){
                    strQuery += ' AND (Start_Date__c <=: trip_enddate AND End_Date__c >=: trip_enddate)';
                }else{
                    strQuery += ' AND ((Start_Date__c <=: trip_startdate AND End_Date__c >=: trip_startdate) OR (Start_Date__c <=: trip_enddate AND End_Date__c >=: trip_enddate))';
                }
            }else{
                if(trip_startdate != null) strQuery += ' AND (Start_Date__c >=: trip_startdate OR End_Date__c >=: trip_startdate)';
                if(trip_enddate != null) strQuery += ' AND (Start_Date__c >=: trip_enddate OR End_Date__c <=: trip_enddate)';
            }
        }
        if(trip_status != null && trip_status != '') strQuery += ' AND Status_Ground__c =: trip_status';
        if(trip_city != null && trip_city != ''){
            trip_city = '%' + trip_city + '%';
            strQuery += ' AND Start_City__r.Name LIKE: trip_city';
        }
        if(trip_vendor != null && trip_vendor != ''){
            trip_vendor = '%' + trip_vendor + '%';
            strQuery += ' AND Vendor_lookup__r.Name LIKE: trip_vendor';
        }
        if(trip_showcontracted || trip_showcancelled){
            strQuery += ' AND (';
            if(trip_showcontracted) strQuery += 'Status_Ground__c = \'Contracted On Own\'';
            if(trip_showcancelled){
                if(trip_showcancelled && trip_showcontracted) 
                    strQuery += ' OR Status_Ground__c = \'Cancelled\''; 
                else 
                    strQuery += 'Status_Ground__c = \'Cancelled\'';
            }
            strQuery += ')';
        }        
        //strQuery += ' ORDER BY Start_Date__c DESC LIMIT 100';
        
        if(orderCheckTrip){
            if(orderChangeTrip){ orderOrientationTrip = 'ASC';
            }else{ if(orderOrientationTrip == 'ASC') orderOrientationTrip = 'DESC'; else orderOrientationTrip = 'ASC';}
        }
        orderCheckTrip = false;
        
        Integer totalRecordsTrip = Database.countQuery('Select count() from Ground__c WHERE' + strQuery.substringAfter('WHERE'));
        totalPagesTrip = totalRecordsTrip != null && totalRecordsTrip == 0 ? 1 : Integer.valueOf((totalRecordsTrip/Decimal.valueOf(limitTrip)).round(System.RoundingMode.UP));
        if(String.isBlank(searchTypeTrip)){
            strQuery += ' ORDER BY ' + orderFieldTrip + ' ' + orderOrientationTrip + ' NULLS LAST' + ', Id LIMIT :limitTrip';
            tripList = Database.query(strQuery);
            offsetTrip = null;
        }
        else{
            if(searchTypeTrip == 'next'){
                offsetTrip = (offsetTrip != null ? offsetTrip : 0) + limitTrip;
                strQuery += ' AND (' + orderFieldTrip + (orderOrientationTrip == 'ASC' ? ' >' : ' <') + ':lastValueOfSortedField OR (' + orderFieldTrip  + ' =:lastValueOfSortedField AND Id >:lastId)) ORDER BY ' + orderFieldTrip + ' ' + orderOrientationTrip + ' NULLS LAST' + ', Id LIMIT :limitTrip';
                tripList = Database.query(strQuery);
            }
            else if(searchTypeTrip == 'previous'){
                offsetTrip = (offsetTrip != null ? offsetTrip : 0) - limitTrip;
                strQuery += ' AND (' + orderFieldTrip + (orderOrientationTrip == 'ASC' ? ' <' : ' >') + ':firstValueOfSortedField OR (' + orderFieldTrip  + ' =:firstValueOfSortedField AND Id <:firstId)) ORDER BY ' + orderFieldTrip + ' ' + (orderOrientationTrip == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT :limitTrip';
                tripList = Database.query(strQuery);
                List<Ground__c> airTrips = new List<Ground__c>();
                for(Integer i = tripList.size() - 1; i >= 0; i--) airTrips.add(tripList[i]);
                tripList = airTrips;
            } 
            else if(searchTypeTrip == 'first'){
                offsetTrip = null;
                strQuery += ' ORDER BY ' + orderFieldTrip + ' ' + orderOrientationTrip + ' NULLS LAST' + ', Id LIMIT :limitTrip';
                tripList = Database.query(strQuery);
            } 
            else if(searchTypeTrip == 'last'){
                offsetTrip = limitTrip * (Integer.valueOf((totalRecordsTrip / Decimal.valueOf(limitTrip)).round(System.RoundingMode.CEILING)) - 1);
                strQuery += ' ORDER BY ' + orderFieldTrip + ' ' + (orderOrientationTrip == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT ' + String.valueOf(totalRecordsTrip - offsetTrip);
                tripList = Database.query(strQuery);
                List<Ground__c> airTrips = new List<Ground__c>();
                for(Integer i = tripList.size() - 1; i >= 0; i--) airTrips.add(tripList[i]);
                tripList = airTrips;
            } 
        }
        firstId = !tripList.isEmpty() ? tripList[0].Id : null;
        lastId = !tripList.isEmpty() ? tripList[tripList.size() - 1].Id : null;
        firstValueOfSortedField = !tripList.isEmpty() ? (orderFieldTrip == 'Vendor_lookup__r.Name' ? tripList[0].Vendor_lookup__r.Name : tripList[0].get(orderFieldTrip)) : null;
        lastValueOfSortedField = !tripList.isEmpty() ? (orderFieldTrip == 'Vendor_lookup__r.Name' ? tripList[tripList.size() - 1].Vendor_lookup__r.Name : tripList[tripList.size() - 1].get(orderFieldTrip)) : null;
        searchTypeTrip = null;
        
        if(tripViewId != null && tripViewId != '') viewTripDetail();
    }
    
    public void deleteTrip(){
        if(itineraryIdActual != null && itineraryIdActual != ''){
            Ground__c gAux = [SELECT Id FROM Ground__c WHERE Id =: itineraryIdActual];
            delete [SELECT Id FROM Ground__c WHERE GT_Trip_Details__c =: gAux.Id AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL AND Bid__c = NULL];
            delete [SELECT Id FROM Concessions__c WHERE GT__c =: gAux.Id AND Bid__c = NULL];
            delete [SELECT Id FROM Itinerary__c WHERE GT__c =: gAux.Id];
            delete gAux;
            searchItinerary();
            orderFieldTrip = 'Start_Date__c';
            //TripWrapper.orderFieldTrip = 'start_date';
            searchTrip();
        }
    }
    
    public void editTrip(){
        newtrip = new Ground__c();
        newitinerary = new Itinerary__c();
        if(itineraryIdActual != null && itineraryIdActual != ''){
            newitinerary = [SELECT Id, GT__c FROM Itinerary__c WHERE Id =: itineraryIdActual];
            if(newitinerary.GT__c != null){
                newtrip = [SELECT Id, Start_City__r.Name, Start_Date__c, End_Date__c, Start_City__c, Description__c, GT_Preferences__c, Status__c, Status_Ground__c, Trace_Date__c, Deadline_Date__c, Group_Type__c, Service_Type__c FROM Ground__c WHERE Id =: newItinerary.GT__c];
                newtrip_startcity = newtrip.Start_City__r.Name;
            }
        }
    }
    
    public void saveCreateJournal(){
        newJournal.Id = (createjournal_id != null && createjournal_id != '' ? createjournal_id : null);
        if(createjournal_id == null || createjournal_id == ''){
            if(createjournal_type == 'trip' || createjournal_type == 'trip_stay'){
                newJournal.RecordTypeId = journal_tripJournalRT;
            }else{
                //newJournal.Bid__c = bidData.Id;
                //newJournal.RecordTypeId = journal_bidJournalRT; 
            }
        }
        if(newJournal.Production_checkbox__c) newJournal.Production__c = opportunityId;
        //newJournal.Housing__c = (createjournal_type == 'housing_stay' ? newHousingStay.Id : housingStayViewId); 
        if(createjournal_type == 'trip' && newtrip.Id != null) newJournal.G__c = newtrip.Id;
        if(createjournal_type == 'trip_stay' && tripViewId != null) newJournal.G__c = tripViewId;
        if(newJournal.Mark_Journal_trace_complete__c) newJournal.Trace_Date__c = null;
        //if(newJournal.Vendor_Checkbox__c) newJournal.Vendor__c = bidData.Vendor__c;
        system.debug(createjournal_tracedate);
        newJournal.Trace_Date__c = (createjournal_tracedate != null && createjournal_tracedate != '' ? Date.parse(createjournal_tracedate) : null);
        if(createjournal_coordinator != null && createjournal_coordinator != '') newJournal.Trace_Coordinator__c = createjournal_coordinator;
        upsert newJournal;
        
        //delete [SELECT Id, Company__c FROM Related_Companies__c WHERE Journal__c =: newJournal.Id AND Company__c <> null];
        delete [SELECT Id, Contact__c FROM Related_Contact__c WHERE Journal__c =: newJournal.Id AND Contact__c <> null];

        //Related Companies
        /*Related_Companies__c rcAux;
        List<Related_Companies__c> rcListAux = new List<Related_Companies__c>();
        if(createjournal_productioncompanyids != null && createjournal_productioncompanyids.trim() != ''){
            for(String s : createjournal_productioncompanyids.split(',')){
                if(s.trim() != ''){
                    rcAux = new Related_Companies__c(Company__c=s.trim(),Journal__c=newJournal.Id);
                    rcListAux.add(rcAux);
                }
            }
        }*/
        //Related Contacts
        Related_Contact__c rcoAux;
        Map<String,Related_Contact__c> rcoMapAux = new Map<String,Related_Contact__c>();
        if(createjournal_productioncontactids != null && createjournal_productioncontactids.trim() != ''){
            for(String s : createjournal_productioncontactids.split(',')){
                if(s.trim() != ''){
                    rcoAux = new Related_Contact__c(Contact__c=s.trim(),Journal__c=newJournal.Id,Type__c='Production Contacts;');
                    rcoMapAux.put(rcoAux.Contact__c,rcoAux);
                }
            }
        }
        if(createjournal_companycontactids != null && createjournal_companycontactids.trim() != ''){
            for(String s : createjournal_companycontactids.split(',')){
                if(s.trim() != ''){
                    rcoAux = new Related_Contact__c(Contact__c=s.trim(),Journal__c=newJournal.Id,Type__c=(rcoMapAux.get(s.trim()) != null ? rcoMapAux.get(s.trim()).Type__c + 'Company Contacts;' : 'Company Contacts;'));
                    rcoMapAux.put(rcoAux.Contact__c,rcoAux);
                }
            }
        }
        
        if(createjournal_alert){
            Set<String> userEmails = new Set<String>();
            for(Production_Associations__c pa : [SELECT Id, User__c, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId AND User__c <> null]) userEmails.add(pa.User__r.Email);
            if(userEmails.size() > 0){
                List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
                
                List<String> userEmailsList = new List<String>(userEmails);
                Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage(); 
                if(prodAssocAux.size() > 0 && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(verifyWideAddress(prodAssocAux[0].User__r.Email));
                mail.setToAddresses(userEmailsList); 
                mail.setSubject('Urgent: Journal Entry for ' + opportunity.Name); 
                String bodyAux = newJournal.Journal_Entry__c + '<br/><br/>' + 
                    '<a href="'+ ApexPages.currentPage().getHeaders().get('Host') + '/' + newJournal.Id + '" target="_blank">Click here for the Journal entry</a><br/>' +
                    //'<a href="'+ ApexPages.currentPage().getHeaders().get('Host') + '/' + housingStayViewId + '" target="_blank">Click here for the Trip Detail link</a><br/><br/>' +
                    'Thanks, <br/>'+
                    UserInfo.getUserName();
                mail.setHtmlBody(bodyAux); 
                Messaging.sendEmail(new Messaging.SingleEmailMessage[] { mail });
            }
        }

        if(createjournal_coordinator != null && createjournal_coordinator != '' && (createjournal_id == '' || createjournal_id == null)){
            Journal__c jAux = [SELECT Id, Task_ID__c FROM Journal__c WHERE Id =: newJournal.Id];
            Task t = new Task(
                Id = (jAux.Task_ID__c != null ? jAux.Task_ID__c : null),
                Subject = (newJournal.Journal_Entry__c.length() > 40 ? newJournal.Journal_Entry__c.subString(0,40) : newJournal.Journal_Entry__c),
                RecordTypeId = task_traceTaskRT,
                ActivityDate = newJournal.Trace_Date__c,
                OwnerId = createjournal_coordinator,
                WhatId = newJournal.Id, 
                Description = newJournal.Journal_Entry__c, 
                Status = 'Open'
            );
            if(newJournal.Mark_Journal_trace_complete__c) t.Status = 'Completed'; else t.Status = 'Open';
            upsert t;
            
            if(jAux.Task_ID__c == null){
                newJournal.Task_ID__c = t.Id;
                update newJournal;
            }
        }
        
        //if(rcListAux.size() > 0) insert rcListAux;
        if(rcoMapAux.size() > 0) insert rcoMapAux.values();
        //searchStayJournal();
        if(createjournal_type == 'trip_stay') searchTripJournalsByGT();
    }
    
    public void saveTrip(){
        system.debug(newtrip.Group_Type__c);
        Boolean createRecords = false;
        if(newtrip.Id == null){
            newtrip.Production_Ground__c = opportunityId;
            createRecords = true;
        }
        newtrip.RecordTypeId = ground_GTTripDetailsRT;
        newtrip.Group_Type__c = newtrip_grouptype;
        newtrip.Start_City__c = (newtrip_startcityid != null && newtrip_startcityid != '' ? newtrip_startcityid : null);
        upsert newtrip;
        
        if(newitinerary.Id == null) newitinerary.Production__c = opportunityId;
        newitinerary.RecordTypeId = itinerary_GTItineraryRT;
       	newitinerary.GT__c = newtrip.Id;
        newitinerary.Start_Date__c = newtrip.Start_Date__c;
        newitinerary.End_Date__c = newtrip.End_Date__c;
        newitinerary.Status__c = newtrip.Status_Ground__c;
        newitinerary.City__c = newtrip.Start_City__c;
        upsert newitinerary;
        
        if(createRecords){
            List<Ground__c> newVehiclesTrip = new List<Ground__c>();
            Ground__c gxAux;
            for(Ground__c vx : vehiclesByProductionList){
                gxAux = vx.clone();
                gxAux.Id = null;
                gxAux.Production_Ground__c = opportunityId;
                gxAux.GT_Trip_Details__c = newtrip.Id;
                gxAux.Start_Date__c = newtrip.Start_Date__c;
                gxAux.End_Date__c = newtrip.End_Date__c;
                gxAux.Start_City__c = newtrip.Start_City__c;
                gxAux.RecordTypeId = Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId();
                newVehiclesTrip.add(gxAux);
            }
            List<Concessions__c> newItemsTrip = new List<Concessions__c>();
            Concessions__c cxAux;
            for(Concessions__c cx : itemsByProductionList){
                cxAux = cx.clone();
                cxAux.Production__c = opportunityId;
                cxAux.GT__c = newtrip.Id;
                cxAux.Create_in_Bid__c = true;
                newItemsTrip.add(cxAux);
            }
            
            if(newVehiclesTrip.size() > 0) insert newVehiclesTrip;
            if(newItemsTrip.size() > 0) insert newItemsTrip;
        }
        
        if(newtrip_clear) newTrip();
        
        searchItinerary();
        //orderFieldTrip = 'Start_Date__c';
        //TripWrapper.orderFieldTrip = 'start_date';
        //searchTrip();
    }
    
    public void newTrip(){
        newtrip = new Ground__c(RecordTypeId = ground_GTTripDetailsRT, Status_Ground__c = 'Itinerary Received', GT_Preferences__c = 'RRU');
        newitinerary = new Itinerary__c(RecordTypeId = itinerary_GTItineraryRT);
        newtrip_startcity = null;
    }
    
    public void clearListTabs(){
        tripList = new List<Ground__c>();
        itineraryList = new List<Itinerary__c>(); 
    }
    
    public void searchItinerary(){
        system.debug(itinerary_showprior);
        system.debug(itinerary_startdate);
        system.debug(itinerary_enddate);
        system.debug(itinerary_city);
        system.debug(itinerary_vendor);
        system.debug(itinerary_status);
        system.debug(itinerary_showprior);
        system.debug(itinerary_showcontracted);
        system.debug(itinerary_showcancelled);
        clearListTabs();
        //itineraryMap = new Map<String,List<Itinerary__c>>();
		List<Itinerary__c> itiAuxList;
		itineraryList = new List<Itinerary__c>(); 
        //itineraryCountMap = new Map<String,Integer>();
        //tournamentList = new List<Itinerary__c>(); 
        Set<String> tournamentIds = new Set<String>();
        String strQuery = 'SELECT Id, Production__c, Status__c, Start_Date__c, End_Date__c, '+
            'Housing__c, GT__r.Bid__c, GT__r.Bid__r.Name, GT__r.Name, GT__r.RecordType.Name, '+
            'City__c, City__r.Name, GT__r.Vendor__c,  GT__r.Group_Type__c, GT__r.Status_Ground__c, GT__r.Status__c, GT__r.Deadline_Date__c, '+
            'Production__r.Parent_Production__c, GT__r.Description__c, GT__r.Vendor_lookup__c, GT__r.Vendor_lookup__r.Name, GT__r.Service_Type__c '+
            'FROM Itinerary__c WHERE Production__c =: opportunityId AND RecordType.Name = \'GT Itinerary\'';

        Date tdy = system.today();
        if(!itinerary_showprior){
            strQuery += ' AND Start_Date__c >=: tdy';
        }else{
            if(itinerary_startdate != null && itinerary_enddate != null){
                if(itinerary_startdate == itinerary_enddate){
                    strQuery += ' AND (Start_Date__c <=: itinerary_enddate AND End_Date__c >=: itinerary_enddate)';
                }else{
                    strQuery += ' AND ((Start_Date__c <=: itinerary_startdate AND End_Date__c >=: itinerary_startdate) OR (Start_Date__c <=: itinerary_enddate AND End_Date__c >=: itinerary_enddate))';
                }
            }else{
                if(itinerary_startdate != null) strQuery += ' AND (Start_Date__c >=: itinerary_startdate OR End_Date__c >=: itinerary_startdate)';
                if(itinerary_enddate != null) strQuery += ' AND (Start_Date__c >=: itinerary_enddate OR End_Date__c <=: itinerary_enddate)';
            }
        }
        if(itinerary_status != null && itinerary_status != '') strQuery += ' AND Status__c =: itinerary_status';
        if(itinerary_city != null && itinerary_city != '') strQuery += ' AND City__r.Name LIKE: itinerary_city';
        if(itinerary_vendor != null && itinerary_vendor != ''){
            itinerary_vendor = '%' + itinerary_vendor + '%';
            strQuery += ' AND GT__r.Vendor_lookup__r.Name LIKE: itinerary_vendor';
        }
        if(itinerary_showcontracted || itinerary_showcancelled){
            strQuery += ' AND (';
            if(itinerary_showcontracted) strQuery += 'Status__c = \'Contracted On Own\'';
            if(itinerary_showcancelled){
                if(itinerary_showcancelled && itinerary_showcontracted) 
                    strQuery += ' OR Status__c = \'Cancelled\''; 
                else 
                    strQuery += 'Status__c = \'Cancelled\'';
            }
            strQuery += ')';
        }

        //strQuery += ' ORDER BY Start_Date__c DESC LIMIT 100';
        if(orderCheckItinerary){
            if(orderChangeItinerary){ orderOrientationItinerary = 'ASC';
            }else{ if(orderOrientationItinerary == 'ASC') orderOrientationItinerary = 'DESC'; else orderOrientationItinerary = 'ASC';}
        }
        orderCheckItinerary = false;
        
        system.debug(strQuery.substringAfter('WHERE'));
        system.debug(searchTypeItinerary);
        system.debug(orderFieldItinerary);
        system.debug(orderOrientationItinerary);
        system.debug(offsetItinerary);
        system.debug(limitItinerary);
        Integer totalRecordsItinerary = Database.countQuery('Select count() from Itinerary__c WHERE' + strQuery.substringAfter('WHERE'));
        totalPagesItinerary = totalRecordsItinerary != null && totalRecordsItinerary == 0 ? 1 : Integer.valueOf((totalRecordsItinerary/Decimal.valueOf(limitItinerary)).round(System.RoundingMode.UP));
        if(String.isBlank(searchTypeItinerary)){
            strQuery += ' ORDER BY ' + orderFieldItinerary + ' ' + orderOrientationItinerary + ' NULLS LAST' + ', Id LIMIT :limitItinerary';
            itineraryList = Database.query(strQuery);
            offsetItinerary = null;
            system.debug('enter');
        }
        else{
            if(searchTypeItinerary == 'next'){
                offsetItinerary = (offsetItinerary != null ? offsetItinerary : 0) + limitItinerary;
                strQuery += ' AND (' + orderFieldItinerary + (orderOrientationItinerary == 'ASC' ? ' >' : ' <') + ':lastValueOfSortedFieldItinerary OR (' + orderFieldItinerary  + ' =:lastValueOfSortedFieldItinerary AND Id >:lastIdItinerary)) ORDER BY ' + orderFieldItinerary + ' ' + orderOrientationItinerary + ' NULLS LAST' + ', Id LIMIT :limitItinerary';
                itineraryList = Database.query(strQuery);
            }
            else if(searchTypeItinerary == 'previous'){
                offsetItinerary = (offsetItinerary != null ? offsetItinerary : 0) - limitItinerary;
                strQuery += ' AND (' + orderFieldItinerary + (orderOrientationItinerary == 'ASC' ? ' <' : ' >') + ':firstValueOfSortedFieldItinerary OR (' + orderFieldItinerary  + ' =:firstValueOfSortedFieldItinerary AND Id <:firstIdItinerary)) ORDER BY ' + orderFieldItinerary + ' ' + (orderOrientationItinerary == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT :limitItinerary';
                itineraryList = Database.query(strQuery);
                List<Itinerary__c> airTrips = new List<Itinerary__c>();
                for(Integer i = itineraryList.size() - 1; i >= 0; i--) airTrips.add(itineraryList[i]);
                itineraryList = airTrips;
            } 
            else if(searchTypeItinerary == 'first'){
                offsetItinerary = null;
                strQuery += ' ORDER BY ' + orderFieldItinerary + ' ' + orderOrientationItinerary + ' NULLS LAST' + ', Id LIMIT :limitItinerary';
                itineraryList = Database.query(strQuery);
            } 
            else if(searchTypeItinerary == 'last'){
                offsetItinerary = limitItinerary * (Integer.valueOf((totalRecordsItinerary / Decimal.valueOf(limitItinerary)).round(System.RoundingMode.CEILING)) - 1);
                strQuery += ' ORDER BY ' + orderFieldItinerary + ' ' + (orderOrientationItinerary == 'ASC' ? 'DESC' : 'ASC') + ' NULLS LAST' + ', Id LIMIT ' + String.valueOf(totalRecordsItinerary - offsetItinerary);
                itineraryList = Database.query(strQuery);
                List<Itinerary__c> airTrips = new List<Itinerary__c>();
                for(Integer i = itineraryList.size() - 1; i >= 0; i--) airTrips.add(itineraryList[i]);
                itineraryList = airTrips;
            } 
        }
        firstIdItinerary = !itineraryList.isEmpty() ? itineraryList[0].Id : null;
        lastIdItinerary = !itineraryList.isEmpty() ? itineraryList[itineraryList.size() - 1].Id : null;
        firstValueOfSortedFieldItinerary = !itineraryList.isEmpty() ? itineraryList[0].Start_Date__c : null;
        lastValueOfSortedFieldItinerary = !itineraryList.isEmpty() ? itineraryList[itineraryList.size()-1].Start_Date__c : null;
        searchTypeItinerary = null;
        /*Integer totalRecordsItinerary = Database.query(strQuery + ' LIMIT 50000').size();
        totalPagesItinerary = totalRecordsItinerary != null && totalRecordsItinerary == 0 ? 1 : Integer.valueOf((totalRecordsItinerary/Decimal.valueOf(limitItinerary)).round(System.RoundingMode.UP));
        if(searchTypeItinerary != null && searchTypeItinerary != ''){
            if(searchTypeItinerary == 'next') offsetItinerary = (offsetItinerary != null ? offsetItinerary : 0) + limitItinerary; 
            if(searchTypeItinerary == 'previous') offsetItinerary = (offsetItinerary != null ? offsetItinerary : 0) - limitItinerary;
            if(searchTypeItinerary == 'first') offsetItinerary = null;
            if(searchTypeItinerary == 'last') offsetItinerary = limitItinerary*(Integer.valueOf((totalRecordsItinerary/Decimal.valueOf(limitItinerary)).round(System.RoundingMode.CEILING)) - 1);
        }
        strQuery += ' ORDER BY ' + (orderFieldItinerary != null ? orderFieldItinerary : 'Start_Date__c') + ' ' + (orderOrientationItinerary != null ? orderOrientationItinerary : 'ASC') + ' NULLS LAST';
        if(offsetItinerary == null || offsetItinerary <= 0) strQuery += ' LIMIT :limitItinerary'; else strQuery += ' LIMIT :limitItinerary OFFSET :offsetItinerary';
        searchTypeItinerary = null;*/
        //system.debug(strQuery);
        
        system.debug(itineraryList);
        
        Set<String> tripIds = new Set<String>();
        for(Itinerary__c iti : itineraryList){
            if(iti.GT__c != null) tripIds.add(iti.GT__c);
        }
        
        bidContractByGTMap = new Map<String,Bid__c>();
        Set<String> bidIdsAux = new Set<String>();
        for(Bid__c b : [SELECT Id, Name, GT__c FROM Bid__c WHERE GT__c IN: tripIds and Status__c = 'Contracted' order by createdDate ASC]){
            bidContractByGTMap.put(b.GT__c,b);
            bidIdsAux.add(b.Id);
        }
            
        symbolMap = new Map<String,String>();
        symbolMap.put(null,'');
        ratesByBidMap = new Map<String,Revenue__c>();
        for(Revenue__c r : [Select id, Total_Price__c, Bid__c, Bid__r.Name, Bid__r.GT__c, CurrencyIsoCode from Revenue__c where Bid__r.GT__c IN: tripIds and Bid__r.Status__c = 'Contracted' and RecordType.DeveloperName = 'Ground_Rate_Travel_Commission' order by createdDate ASC]){
            ratesByBidMap.put(r.Bid__r.GT__c,r);
            symbolMap.put(r.CurrencyIsoCode,'');
        }
        getSymbol();
        
        system.debug(tripIds);
        //FOR ITINERARY TAB - TRIP
        vehiclesByTripMap = new Map<String,List<Ground__c>>();
        tripsItineraryMap = new Map<String,List<Ground__c>>();
        travelsItineraryMap = new Map<String,List<Ground__c>>();
        tripsItineraryCountMap = new Map<String,Integer>();
        travelsItineraryCountMap = new Map<String,Integer>();
        Set<String> subtripIds = new Set<String>();
        List<Ground__c> lstGroundAux;
        for(Ground__c hd : [SELECT Id, GT_Trip_Details__c, Vehicle_Ref__c, Make__c, Model__c, Amenities__c, RecordType.DeveloperName, Sub_Trip_Type__c, Description__c, Other_Amenities__c, Gear_Luggage_Space__c,
                            Vehicle_Type__c, Capacity__c, Year__c
                            FROM Ground__c WHERE GT_Trip_Details__c IN: tripIds AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL]){
            if(hd.RecordType.DeveloperName == 'Vehicle_Type'){
                lstGroundAux = vehiclesByTripMap.get(hd.GT_Trip_Details__c) != null ? vehiclesByTripMap.get(hd.GT_Trip_Details__c) : new List<Ground__c>();
                lstGroundAux.add(hd);
                vehiclesByTripMap.put(hd.GT_Trip_Details__c,lstGroundAux.clone());
            }
            if(hd.RecordType.DeveloperName == 'GT_Sub_Trip_Details'){
                lstGroundAux = tripsItineraryMap.get(hd.GT_Trip_Details__c) != null ? tripsItineraryMap.get(hd.GT_Trip_Details__c) : new List<Ground__c>();
                lstGroundAux.add(hd);
                tripsItineraryMap.put(hd.GT_Trip_Details__c,lstGroundAux.clone());
                subtripIds.add(hd.Id);
            }
        }
        
        vehiclesByBidMap = new Map<String,List<Ground__c>>();
        for(Ground__c hd : [SELECT Id, Bid__c, GT_Trip_Details__c, Vehicle_Ref__c, Make__c, Model__c, Amenities__c, Other_Amenities__c, RecordType.DeveloperName, Sub_Trip_Type__c, Description__c, Gear_Luggage_Space__c,
                            Vehicle_Type__c, Capacity__c, Year__c
                            FROM Ground__c WHERE Bid__c IN: bidIdsAux AND RecordType.DeveloperName = 'Vehicle_Type']){
            lstGroundAux = vehiclesByBidMap.get(hd.Bid__c) != null ? vehiclesByBidMap.get(hd.Bid__c) : new List<Ground__c>();
            lstGroundAux.add(hd);
            vehiclesByBidMap.put(hd.Bid__c,lstGroundAux.clone());
        }
        
        tripsItineraryBidMap = new Map<String,List<Ground__c>>();
        for(Ground__c hd : [SELECT Id, Bid_Sub_Trip__c, GT_Trip_Details__c, Vehicle_Ref__c, Make__c, Model__c, Amenities__c, RecordType.DeveloperName, Sub_Trip_Type__c, Description__c FROM Ground__c WHERE Bid_Sub_Trip__c IN: bidIdsAux AND RecordType.DeveloperName = 'GT_Sub_Trip_Details' ORDER BY Trip_Order__c, Line__c]){
            lstGroundAux = tripsItineraryBidMap.get(hd.Bid_Sub_Trip__c) != null ? tripsItineraryBidMap.get(hd.Bid_Sub_Trip__c) : new List<Ground__c>();
            lstGroundAux.add(hd);
            tripsItineraryBidMap.put(hd.Bid_Sub_Trip__c,lstGroundAux.clone());
            subtripIds.add(hd.Id);
        }
        
        for(Ground__c hd : [SELECT Id, GT_Sub_Trip_Details__c, Line__c, Vehicle_Ref__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, 
                            Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c, Sub_Trip_Notes__c, Vehicle_Lookup__c, 
                            Start_Date_Time__c, End_Date_Time__c, Location_Drop_Off_Type__c, Location_Details_Drop_Off__c, Start_Date_Time_Text__c, End_Date_Time_Text__c
                            FROM Ground__c WHERE RecordType.DeveloperName = 'GT_Travel_Details' AND GT_Sub_Trip_Details__c IN: subtripIds]){
                                hd.Start_Date_Time_Text__c = hd.Start_Date__c != null && hd.Start_Date_Time__c != null ? Datetime.newInstance(hd.Start_Date__c, hd.Start_Date_Time__c).format('h:mm a') : '';
                                hd.End_Date_Time_Text__c = hd.End_Date__c != null && hd.End_Date_Time__c != null ? Datetime.newInstance(hd.End_Date__c, hd.End_Date_Time__c).format('h:mm a') : '';
                                lstGroundAux = travelsItineraryMap.get(hd.GT_Sub_Trip_Details__c) != null ? travelsItineraryMap.get(hd.GT_Sub_Trip_Details__c) : new List<Ground__c>();
                                lstGroundAux.add(hd);
                                travelsItineraryMap.put(hd.GT_Sub_Trip_Details__c,lstGroundAux.clone());
        }
        for(String sd : tripIds){
            if(ratesByBidMap.get(sd) == null) ratesByBidMap.put(sd,new Revenue__c());
            if(bidContractByGTMap.get(sd) == null) bidContractByGTMap.put(sd,new Bid__c());
            if(vehiclesByTripMap.get(sd) == null) vehiclesByTripMap.put(sd,new List<Ground__c>());
            if(tripsItineraryMap.get(sd) == null){
                tripsItineraryMap.put(sd,new List<Ground__c>());
                tripsItineraryCountMap.put(sd,0);
            }else{
                tripsItineraryCountMap.put(sd,tripsItineraryMap.size());
            }
        }
        for(String sd : subtripIds){
            if(travelsItineraryMap.get(sd) == null){
                travelsItineraryMap.put(sd,new List<Ground__c>());
                travelsItineraryCountMap.put(sd,0);
            }else{
                travelsItineraryCountMap.put(sd,travelsItineraryMap.size());
            }
        }
        for(String sd : bidIdsAux){
            if(vehiclesByBidMap.get(sd) == null) vehiclesByBidMap.put(sd,new List<Ground__c>());
            if(tripsItineraryBidMap.get(sd) == null){
                tripsItineraryBidMap.put(sd,new List<Ground__c>());
                tripsItineraryCountMap.put(sd,0);
            }else{
                tripsItineraryCountMap.put(sd,tripsItineraryBidMap.size());
            }
        }
        /**
        *  @Conga: Update for Conga.
        */
        congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
        for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('GT - ItineraryByOppId')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
        itinerarySummary_congaQueriesJson = JSON.serialize(congaQueriesMap);
        List<APXTConga4__Conga_Template__c> congaTemplates = [Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c = 'GT - Ground Travel Itinerary'];
        itinerarySummary_congaTemplateId = !congaTemplates.isEmpty() ? congaTemplates[0].id : null;
        /**
        *  @/Conga
        */
    }
    
    public void saveSale(){
        update ground;
    }
    
    public void saveEditItem(){
        if(itemIdActual != null && itemIdActual != ''){
            new_item = new Concessions__c(
                Id = itemIdActual,
                Concession_Type__c='GT',
                Concessions_Requested__c = item_requested
                //Concession_Provided__c = item_provided
            );
            update new_item;
        }
        getRateDetailsProduction();
    }
    
    public void deleteItem(){
        if(itemIdActual != null && itemIdActual != '') delete [SELECT Id FROM Concessions__c WHERE Id=:itemIdActual];
        getRateDetailsProduction();
    }
    
    public void addItem(){
        if(opportunityId != null && opportunityId != null){
            new_item.Id = null;
            new_item.Concession_Type__c = 'GT';
            new_item.Production__c = opportunityId;
            new_item.Concessions_Requested__c = item_requested;
            insert new_item;
        }
        getRateDetailsProduction();
    }
    
    public void newItem(){
    	new_item = new Concessions__c(Concession_Type__c='GT');
    }
    
    public void saveEditVehicle(){
        if(vehicleIdActual != null && vehicleIdActual != ''){
            new_vehicle = new Ground__c(
                Id = vehicleIdActual,
                Vehicle_Ref__c = vehicle_vehicleref,
                Vehicle_Type__c = vehicle_vehicletype,
                Capacity__c = vehicle_capacity,
                Make__c = vehicle_make,
                Model__c = vehicle_model,
                Year__c = vehicle_year,
                Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null),
                Other_Amenities__c = vehicle_otheramenities
            );
            update new_vehicle;
        }
        getVehiclesProduction();
    }
    
    public void deleteVehicle(){
        if(vehicleIdActual != null && vehicleIdActual != '') delete [SELECT Id FROM Ground__c WHERE Id=:vehicleIdActual];
        searchItinerary();
        getVehiclesProduction();
    }
    
    public void deleteVehicleTrip(){
        if(vehicleIdActual != null && vehicleIdActual != ''){
            delete [SELECT Id FROM Ground__c WHERE Id=:vehicleIdActual];
            refreshVehicleDataBids(tripViewId);
        }
        searchItinerary();
        getVehiclesByTrip();
    }
    
    public void addVehicle(){
        system.debug(vehicle_amenities);
        if(opportunityId != null && opportunityId != null){
            new_vehicle.Id = null;
            new_vehicle.RecordTypeId = ground_vehicletypeRT;
            new_vehicle.Production_Ground__c = opportunityId;
            new_vehicle.Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null);
            new_vehicle.Make__c = vehicle_make;
            new_vehicle.Model__c = vehicle_model;
            insert new_vehicle;
        }
        getVehiclesProduction();
    }
    
    public void newVehicle(){
    	new_vehicle = new Ground__c();
    }
    
    public void newVehicleTrip(){
        newVehicleTrip = new Ground__c();
    }
    
    @RemoteAction
    global static List<String> getGroundAmenities(String groundid){
        List<String> dataList = new List<String>();
        Ground__c g = [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c FROM Ground__c WHERE Id =: groundid];
        if(g.Amenities__c != null){
            for(String s : g.Amenities__c.split(';')){
                dataList.add(s);
            }
        }
        return dataList;
    }
    
    public void getVehiclesProduction(){
        vehiclesByProductionList = new List<Ground__c>();
        if(opportunityId != null && opportunityId != ''){
           vehiclesByProductionList = [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c 
                                       FROM Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: opportunityId 
                                       AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND GT_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL];
        }
    }
    
    public void getRateDetailsProduction(){
        if(opportunityId != null && opportunityId != '') {
           itemsByProductionList = [SELECT Id, Concession_Type__c, Concession_Provided__c, Concessions_Requested__c 
                                    FROM Concessions__c 
                                    WHERE Concession_Type__c = 'GT' AND Production__c =: opportunityId AND Bid__c = NULL AND Housing__c = NULL AND Freight__c = NULL AND Air__c = NULL AND GT__c = NULL];
        	String defaultConcessionRequested = 'Vendor guarantees they are following CDC guidelines and Motorcoach (ABA or UMA) industry cleanliness protocols';
	        Boolean isDefaultConcessionExists = false;
	        for(Concessions__c concessionRec : itemsByProductionList) {
	            if(String.isNotBlank(concessionRec.Concessions_Requested__c) && 
	               			concessionRec.Concessions_Requested__c.equalsIgnoreCase(defaultConcessionRequested)) {
	                isDefaultConcessionExists = true;
	            }
	        }
	        if(!isDefaultConcessionExists) {
	            item_requested = defaultConcessionRequested;
	            addItem();
	            itemsByProductionList = [SELECT Id, Concession_Type__c, Concession_Provided__c, Concessions_Requested__c 
	                                    FROM Concessions__c 
	                                    WHERE Concession_Type__c = 'GT' AND Production__c =: opportunityId AND Bid__c = NULL AND Housing__c = NULL AND Freight__c = NULL AND Air__c = NULL AND GT__c = NULL];
	        }
        }
    }
    
    public void searchProduction() {
        List<Opportunity> searchOpportunity;
        opportunityId = null;
        opportunity = null;
        if(searchOption == 'searchByParent'){
            List<Ground__c> searchGround = [SELECT Id, Production_Ground__c FROM Ground__c WHERE Name =: searchValue AND RecordType.DeveloperName = 'GT_Trip_Details'];
            system.debug(searchGround);
            if(searchGround.size() > 0){
                opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Office_Location__c FROM Opportunity WHERE Id =: searchGround[0].Production_Ground__c];
                opportunityId = opportunity.Id;
                getDataProduction();
                tripViewId = searchGround[0].Id;
                if(tripViewId != null && tripViewId != '') viewTripDetail();
            }
        }else if(searchOption == 'searchByBid'){
            List<Bid__c> searchBid = [SELECT Id, Name, GT__c, GT__r.Name, Status__c, Production__c FROM Bid__c WHERE Name =: searchValue AND GT__c <> null AND RecordType.DeveloperName = 'GT_Bid'];
            dataBidIdsearch = null;
            if(searchBid.size() > 0){                
                opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Office_Location__c FROM Opportunity WHERE Id =: searchBid[0].Production__c];
                opportunityId = opportunity.Id;
                //getDataByBid = true;
                getDataProduction();
                tripViewId = searchBid[0].GT__c;
                dataBidIdsearch = searchBid[0].Id;
                if(tripViewId != null && tripViewId != '') viewTripDetail();
                if(searchBid[0].Status__c == 'Contracted'){
                    vfpConfiguration.bidId = searchBid[0].Id;
                    vfpConfiguration.bidName = searchBid[0].Name;
                    vfpConfiguration.parentId = searchBid[0].GT__c;
                }
            }
        }
    }
    
    public void getDataProduction() {
        if(opportunityId != null && opportunityId != ''){
            upsertSession(UserInfo.getUserId(),opportunityId); //SESSION CUSTOM SETTING
            tripViewId = null;
            tripView = null;
            tripBidNumber = null;
            
            vfpConfiguration = new DashboardConfigurationWrapper();
            system.debug(opportunityId);
            opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Production_ID__c, Office_Location__c FROM Opportunity WHERE Id=: opportunityId];
            List<Ground__c> groundList = [SELECT Id, Contracting_Terms__c, Billing_Options__c, Billing_options_Text__c, Internal_Notes__c, Payment_Information__c, Payment_Information__r.Credit_Card_Full_Name__c
                                          FROM Ground__c WHERE Production_Ground__c =: opportunityId AND RecordTypeId =: ground_salesGTDetailsRT ORDER BY CreatedDate ASC LIMIT 1];
            if(!groundList.isEmpty()) ground = groundList[0]; else createGround();
            if(ground != null) paymentInformation = ground.Payment_Information__r.Credit_Card_Full_Name__c;
            getAssociationsByProduction(); //GET Associations PL
            getVehiclesProduction(); //GET Vehicles
            getRateDetailsProduction(); //GET Rate Details (Concessions)
            searchItinerary(); // GET Itinerary/Ground
            searchTrip(); //GET Trip Tab
            vfpConfiguration.productionId = opportunityId;
            vfpConfiguration.productionName = opportunity.Alias_With_Production_Name__c;
            vfpConfiguration.parentSObject = 'Ground';
            Map<Id,DashboardClientWrapper> clientsMap = new Map<Id,DashboardClientWrapper>();
            for(Production_Associations__c pa : [SELECT Id, Production_Opp__c, Contact__c, Contact__r.FirstName, Contact__r.LastName, Contact__r.Title, Contact__r.Phone, Contact__r.MobilePhone, Contact__r.Work_Phone_Extension__c, Contact__r.Email, Contact__r.Alternate_Email__c, Contact__r.MailingStreet, Contact__r.MailingPostalCode, Contact__r.City__c, Contact__r.City__r.Name, Contact__r.Notes__c, Role__c FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId AND Contact__c <> null AND Role__c <> null ORDER BY Contact__r.Name ASC]){
                if(pa.Role__c.contains('Primary GT') || pa.Role__c.contains('CC: GT') || pa.Role__c.contains('Contract Singer')) clientsMap.put(pa.Contact__c, new DashboardClientWrapper(
                    pa.Contact__c, 
                    pa.Contact__r.FirstName, 
                    pa.Contact__r.LastName, 
                    pa.Contact__r.Title, 
                    pa.Contact__r.Phone, 
                    pa.Contact__r.MobilePhone, 
                    pa.Contact__r.Work_Phone_Extension__c, 
                    pa.Contact__r.Email, 
                    pa.Contact__r.Alternate_Email__c, 
                    pa.Contact__r.MailingStreet, 
                    '', 
                    pa.Contact__r.City__c, 
                    pa.Contact__r.City__r.Name, 
                    pa.Contact__r.MailingPostalCode, 
                    pa.Contact__r.Notes__c
                ));
                //if(pa.Role__c.contains('Primary Housing')) contactAssociationPrimary = pa.Contact__c;
            }
            vfpConfiguration.clientMap = clientsMap.clone();
            for(Id clientId : clientsMap.keySet()) {
                vfpConfiguration.clientMap.put(clientId,clientsMap.get(clientId));
                vfpConfiguration.clients.add(new SelectOption(clientId,clientsMap.get(clientId).firstName+' '+clientsMap.get(clientId).lastName));
            }
        	System.debug('vfpConfiguration.productionId -> '+vfpConfiguration.productionId);
        }
    }
    
    public void getAssociationsByProduction(){
        productionCompanyPL = new List<SelectOption>();
        productionContactPL = new List<SelectOption>();
        companyContactPL = new List<SelectOption>();
        teamMembers = new List<SelectOption>();
        coordinatorGT = null;
        coordinatorGTName = null;
        
        Set<String> companyIds = new Set<String>();
        teamMembers.add(new SelectOption('','---None---'));
        
        Map<String,String> compMap = new Map<String,String>();
        Map<String,String> prodContactMap = new Map<String,String>();
        
        for(Production_Associations__c pa : [SELECT Id, Company__c, Company__r.Name, Contact__c, Contact__r.Name, User__c, User__r.Name, Team_Roles__c, Production_Opp__c FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId ORDER BY User__r.Name ASC]){
            if(pa.Company__c != null){
                compMap.put(pa.Company__c,pa.Company__r.Name);
                companyIds.add(pa.Company__c);
            }
            if(pa.Contact__c != null) prodContactMap.put(pa.Contact__c,pa.Contact__r.Name);
            if(pa.User__c != null && pa.Team_Roles__c != null){
                teamMembers.add(new SelectOption(pa.User__c,pa.User__r.Name));
                if(pa.Team_Roles__c.contains('Primary GT Coordinator')){
                    coordinatorGT = pa.User__c;
                    coordinatorGTName = pa.User__r.Name;
                }
            }
        }
        
        for(String k1 : compMap.keySet()){
            productionCompanyPL.add(new SelectOption(k1,compMap.get(k1)));
        }
        for(String k1 : prodContactMap.keySet()){
            productionContactPL.add(new SelectOption(k1,prodContactMap.get(k1)));
        }
        
        Map<String,String> contactMap = new Map<String,String>();
        for(Contact c : [SELECT Id, Name FROM Contact WHERE AccountId IN: companyIds]) contactMap.put(c.Id,c.Name);
        for(AccountContactRelation acr : [SELECT Id, AccountId, ContactId, Contact.Name FROM AccountContactRelation WHERE AccountId IN: companyIds AND IsActive = true]) contactMap.put(acr.ContactId,acr.Contact.Name);
        
        for(String keyc : contactMap.keySet()){
            companyContactPL.add(new SelectOption(keyc,contactMap.get(keyc)));
        }
        vfpConfiguration.companies = productionCompanyPL.clone();
        vfpConfiguration.contacts = productionContactPL.clone();
        vfpConfiguration.companyContacts = companyContactPL.clone();
        vfpConfiguration.teamMembers = teamMembers.clone();
    }
    
    public void verifyGround(){
        String ContractBidId = apexpages.currentpage().getparameters().get('ContractBidId');
        String OpenBidId = apexpages.currentpage().getparameters().get('OpenBidId');
        String ServiceId = apexpages.currentpage().getparameters().get('ServiceId');
        system.debug(ContractBidId);
        if(ContractBidId != null && ContractBidId != ''){
            dataBidIdsearch = ContractBidId;
            List<Bid__c> searchBid = [SELECT Id, Name, GT__c, GT__r.Name, Status__c, Production__c FROM Bid__c WHERE Id =: dataBidIdsearch];
            if(searchBid.size() > 0){                
                opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Office_Location__c FROM Opportunity WHERE Id =: searchBid[0].Production__c];
                opportunityId = opportunity.Id;
                getDataProduction();
                tripViewId = searchBid[0].GT__c;
                dataBidIdsearch = searchBid[0].Id;
                if(tripViewId != null && tripViewId != '') viewTripDetail();
                if(searchBid[0].Status__c == 'Contracted'){
                    vfpConfiguration.bidId = searchBid[0].Id;
                    vfpConfiguration.bidName = searchBid[0].Name;
                    vfpConfiguration.parentId = searchBid[0].GT__c;
                    tabDefault = 'gt-contracting';
                }
            }
        }else if(ServiceId != null && ServiceId != ''){
            List<Ground__c> searchService = [SELECT Id, Name, Production_Ground__c FROM Ground__c WHERE Id =: ServiceId];
            if(searchService.size() > 0){
                opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, RecordType.DeveloperName, Production_ID__c, Office_Location__c FROM Opportunity WHERE Id =: searchService[0].Production_Ground__c];
                opportunityId = opportunity.Id;
                getDataProduction();
                tripViewId = searchService[0].Id;
                viewTripDetail();
                tabDefault = 'gt-trip';
            }
        }else if(OpenBidId != null && OpenBidId != ''){
            dataBidIdsearch = OpenBidId;
            List<Bid__c> searchBid = [SELECT Id, Name, GT__c, GT__r.Name, Status__c, Production__c FROM Bid__c WHERE Id =: dataBidIdsearch];
            if(searchBid.size() > 0){                
                opportunity = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Office_Location__c FROM Opportunity WHERE Id =: searchBid[0].Production__c];
                opportunityId = opportunity.Id;
                getDataProduction();
                tripViewId = searchBid[0].GT__c;
                dataBidIdsearch = searchBid[0].Id;
                if(tripViewId != null && tripViewId != '') viewTripDetail();
                if(searchBid[0].Status__c == 'Contracted'){
                    vfpConfiguration.bidId = searchBid[0].Id;
                    vfpConfiguration.bidName = searchBid[0].Name;
                    vfpConfiguration.parentId = searchBid[0].GT__c;
                }
                renderBid = true;
            }
        }else{
            if(opportunityId != null && opportunityId != '') getDataProduction();
            else{
                Dashboard_Session__c ds = Dashboard_Session__c.getValues(UserInfo.getUserId());
                if(ds != null && ds.Id != null && ds.Production_ID__c != null){
                    List<Opportunity> opportunities = [SELECT Id, Name, Alias_with_Production_Name__c, AccountId, Account.Name, Parent_Production__c, RecordTypeId, RecordType.Name, Office_Location__c FROM Opportunity WHERE Id =: ds.Production_ID__c];
                    if(!opportunities.isEmpty()){
                        opportunity = opportunities[0];
                        opportunityId = ds.Production_ID__c;
                        getDataProduction();
                    }
                }
            }
        }
    }
    
    public static void upsertSession(String userid, String opportunityid){
        Dashboard_Session__c ds = Dashboard_Session__c.getValues(userid);
        if(ds == null){
            Dashboard_Session__c dsnew = new Dashboard_Session__c();
            dsnew.Production_ID__c = opportunityid;
            dsnew.SetupOwnerId = UserInfo.getUserId();
            insert dsnew;
        }else{
            ds.Production_ID__c = opportunityid;
            upsert ds;
        }
    }
    
    public void createGround(){
        if(opportunityId != null && opportunityId != ''){
            String contractingTerms;
            if(opportunity.Office_Location__c == 'RRE'){
                //Added Contracting terms and one concession - Housing and GT  //Changes as per 175791240
				contractingTerms = '<ul>' + 
                    '<li>Driver(s) must assist with luggage.</li>' +
                    '<li>Driver(s) will be on time, drive safely and only use mobile phones in emergencies.</li>' +
                    '<li>Driver(s) name and mobile number(s) will be provided prior to travel.</li>' +
                    '<li>Driver(s) requested not to smoke in the coach. If the driver(s) is a smoker, he/she must smoke outside the coach without interference of the scheduled transfer.</li>' +
                    '<li>If driver(s) cannot speak English, a dispatch person speaking English must be available for communication with the client\'s representative and for translation to the driver(s) at all time. This number will be provided prior to travel.</li>' +
                    '<li>Driver(s) will keep a professional attitude towards the passengers on the bus and other vehicles on the road at all times.</li>' +
                    '<li>Driver(s) will be fully briefed on directions, schedules, pick-ups and drop-off spots; and he/she will follow instructions from the dispatcher as well as from the client.</li>' +
                    '<li>Bus company will not sub-contract coaches.</li>' +
                    '<li>Any mechanical failure, or driver/dispatch negligence can cause major issues for their itinerary. This includes being lost or stopping unnecessarily. Bus company will make all efforts to fix any mechanical issues immediately. All drivers should be aware that any requests from the client should be adhered to. Such circumstances as inclement weather conditions, impassable roadway conditions, infringement on date of travel regulations or the intervention of any governmental body are of exception. Client should be contacted immediately should any of the events listed occur.</li>' +
                    '<li>In case of breakdown or repair being needed the bus company shall use its best efforts to provide the client, at no additional charge, alternative ground transportation for any leased vehicle which may be temporarily disabled due to mechanical failure, if supplier deems it impractical to repair the vehicle within a reasonable time.</li>' +
                    '<li>Buses will be checked prior to departure that all contracted amenities are in working order.</li>' +
                    '<li>Buses will be clean upon arrival.</li>' +
                    '<li>Parking fees which may arise throughout the duration of service will be the responsibility of the client.</li>' +
                    '<li>This Agreement may be executed/signed in two or more separate copies/counterparts, together forming one agreement.</li>' +
                    '</ul>';
            }else{
                contractingTerms = '<ul>' +
                    '<li>Vendor must follow recommended CDC regulations and are expected to keep up on the latest guidelines.</li>' + 
                    '<li>One week prior to arrival, vendor will receive “Ground Transportation COVID-19 procedures” with standard cleanliness protocols. Vendor must agree to abide by all standards.</li>' + 
                    '<li>Hand sanitizer and sanitizing wipes and/or spray must be made readily available on board.</li>' + 
                    '<li>Driver must wear gloves when assisting with luggage. Group members will sanitize own luggage handles.</li>' + 
                    '<li>Driver must always wear a mask, when requested by Company Manager.</li>' + 
                    '<li>Driver must always socially distance from group.</li>' + 
                    '<li>Group members will travel with personal supply of sanitizer, wipes, masks, and gloves.</li>' + 
                    '<li>Driver(s) will be on time, drive safely and only use cell phones in emergencies.</li>' + 
                    '<li>Driver(s) name and cell will be provided prior to travel.</li>' + 
                    '<li>Driver(s) are responsible for having directions to destination.</li>' + 
                    '<li>Bus company will not sub-contract coaches.</li>' + 
                    '<li>Any mechanical failure, or driver/dispatch negligence can cause major issues for their itinerary. This includes being lost or stopping unnecessarily. Bus company will make all efforts to fix any mechanical issues immediately. All drivers should be aware that any requests from Tour Management should be adhered to. Weather or roadway conditions, infringement on D.O.T regulations or the intervention of any governmental body are of exception. Road Rebel should be contacted immediately should any of the events listed occur.</li>' + 
                    '<li>If the trip is cancelled due to Covid-19, group will not face any cancellation penalties.</li>' + 
                    '</ul>';
            }
            ground = new Ground__c(
                RecordTypeId = ground_salesGTDetailsRT,
                Production_Ground__c = opportunityId,
                Contracting_Terms__c = contractingTerms,
                Billing_Options__c = null,
                Internal_Notes__c = null
            );
            insert ground;
        }
    }
    
    public static Map<Object,List<String>> getDependentPicklistValues( Schema.sObjectField dependToken )
    {
        Schema.DescribeFieldResult depend = dependToken.getDescribe();
        Schema.sObjectField controlToken = depend.getController();
        if ( controlToken == null ) return null;
        Schema.DescribeFieldResult control = controlToken.getDescribe();
        List<Schema.PicklistEntry> controlEntries =
            (   control.getType() == Schema.DisplayType.Boolean
             ?   null
             :   control.getPicklistValues()
            );
        
        String base64map = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/';
        Map<Object,List<String>> dependentPicklistValues = new Map<Object,List<String>>();
        for ( Schema.PicklistEntry entry : depend.getPicklistValues() ) if ( entry.isActive() )
        {
            List<String> base64chars =
                String.valueOf
                (   ((Map<String,Object>) JSON.deserializeUntyped( JSON.serialize( entry ) )).get( 'validFor' )
                ).split( '' );
            for ( Integer index = 0; index < (controlEntries != null ? controlEntries.size() : 2); index++ )
            {
                Object controlValue =
                    (   controlEntries == null
                     ?   (Object) (index == 1)
                     :   (Object) (controlEntries[ index ].isActive() ? controlEntries[ index ].getLabel() : null)
                    );
                Integer bitIndex = index / 6, bitShift = 5 - Math.mod( index, 6 );
                if  (   controlValue == null
                     ||  (base64map.indexOf( base64chars[ bitIndex ] ) & (1 << bitShift)) == 0
                    ) continue;
                if ( !dependentPicklistValues.containsKey( controlValue ) )
                {
                    dependentPicklistValues.put( controlValue, new List<String>() );
                }
                dependentPicklistValues.get( controlValue ).add( entry.getLabel() );
            }
        }
        return dependentPicklistValues;
    }
    
    @RemoteAction
    global static List<String> getDataEmailBid(String opportunityid, String tripid, String bidid, String primarycontact, String typez, String url){
        List<String> result = new List<String>();
        system.debug(opportunityid);
        system.debug(tripid);
        system.debug(bidid);
        system.debug(primarycontact);
        system.debug(typez);
        system.debug(url);
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
        
        //Subject
        List<Ground__c> groundAux = [SELECT Id, Name, RecordType.Name, Start_Date__c, End_Date__c FROM Ground__c WHERE Id =: tripid];
        String dateIn = (groundAux[0].Start_Date__c != null ? Datetime.newInstance(groundAux[0].Start_Date__c.year(),groundAux[0].Start_Date__c.month(),groundAux[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateOut = (groundAux[0].End_Date__c != null ? Datetime.newInstance(groundAux[0].End_Date__c.year(),groundAux[0].End_Date__c.month(),groundAux[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        List<Opportunity> productionAux = [SELECT Id, Name, Alias_with_Production_Name__c FROM Opportunity WHERE Id =: opportunityid];
        List<Bid__c> bidAux = new List<Bid__c>();
        if(bidid != null && bidid != '') bidAux = [SELECT Id, Name, Vendor__c, Vendor__r.Name FROM Bid__c WHERE Id =: bidid];
        String subject;
        if(typez == 'datechange'){
            //subject = 'Date change Update - ' + productionAux[0].Name + ' - ' + dateIn + ' - ' + dateOut;
            //result.add(subject);
        }else if(typez == 'sendoptions'){
            //subject = 'Housing Options - ' + (groundAux[0].City__c != null ? groundAux[0].City__r.Name : '') + ' - ' + dateIn + '-' + dateOut + ' (' + groundAux[0].Name + ')';
            //result.add(subject);
        }else{
            if(typez != 'release_bid' && typez != 'release_bid2'){
                subject = 'Release Bid - ' + productionAux[0].Name + ' - ' + dateIn + '-' + dateOut; // + ' (' + bidAux[0].Name + ')';
                result.add(subject);
            }
        }
        
        //Body
        String body = '';
        List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Housing Coordinator')];
        /*if(typez == 'pdf'){
            body = 'Dear ' + primary_name +','+
                '<br /><br />Road Rebel, an entertainment touring and locations support company, has a client performing in your area with an interest in your property. The production is sensitive to rate, but service is key as well. Please provide your lowest possible commissionable rate for serious consideration.'+
                '<br /><br />Attached are the requirements for this group, followed by your Hotel Profile. Please update your hotel information as needed and scan and email back to me, along with your completed bid.'+
                '<br /><br />To discuss the specific group details, please call me at 619-640-1001.'+
                '<br /><br />Thank you in advance for your prompt response,'+
                '<br /><br />' + (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') +
                '<br /> Housing Coordinator';
            result.add(body);
        }else if(typez == 'link'){
            if(housingAux[0].RecordType.Name == 'Corporate Housing'){
                body = 'Dear ' + primary_name + ','+
                    '<br /><br /><strong>Road Rebel</strong>, an entertainment logistics support company, has a client coming to your area soon. Please take a look at the attached bid for the request details. Our client needs your lowest all-inclusive rate(s) for serious consideration.' +
                    '<br /><br />Your fully completed <strong>bid, property profile sheets,</strong> and any <strong>images, floor plans</strong> or <strong>furnishing packages</strong> need to be emailed to jana@road-rebel.com, or faxed to +1 619-640-1011 ASAP.' +
                    '<br /><br />Please call me to discuss the details at +1 619-640-1001.' +
                    '<br /><br />Thank you,' +
                    '<br />' + (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '');
            }else{
                body = 'Dear ' + primary_name + ','+
                    '<br /><br/>Road Rebel, an entertainment touring and locations support company, has a client performing in your area with an interest in your property. The production is sensitive to rate, but service is key as well. Please provide your lowest possible commissionable rate for serious consideration.'+
                    '<br /><br/>This link will take you to the requirements for this group, followed by your Hotel Profile. Please update your hotel information as needed and submit for review.'+
                    '<br /><br/>'+ (bidAux != null && bidAux.size() > 0 && bidAux[0].Vendor__c != null ? bidAux[0].Vendor__r.Name : '') + 
                    '<br /><br/> <a href="' + url + '/' + bidid + '" target="_blank">' + url + '/' + bidid + '</a>'+
                    '<br />To discuss the specific group details, please call me at 619-640-1001.'+
                    '<br /><br/>Thank you in advance for your prompt response,'+
                    '<br /><br/>' + (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') +
                    '<br />Housing Coordinator';
            }
            result.add(body);
        }else if(typez == 'datechange'){
            body = 'Dear ' + primary_name + ','+
                '<br /><br />The dates have changed for ' + productionAux[0].Name + ' that you are bidding on.'+
                '<br /><br />The NEW dates are ' + dateIn + ' - ' + dateOut +
                '<br />The OLD dates were ** XX/XX/XXXX - XX/XX/XXXX **.'+
                '<br /><br />If you have already returned your bid and can honor the same rate for the new dates, please reply to confirm. If you have not returned the previous bid or if the rates are affected by this date change, please fill out the newly updated attached bid or update the bid via this link ' +
                '<a href="' + url + '/' + bidid + '" target="_blank">' + url + '/' + bidid + '</a>'+         
                '<br /><br />Thank you,' +
                '<br />' + (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') +
                '<br />Housing Coordinator';
            result.add(body);
        }else if(typez == 'sendoptions'){
            body = 'Hi ' + primary_name + ',' +
                '<br /><br />Please find the Housing Options attached.' + 
                '<br /><br />Other Properties Contacted:' +
                '<br /><br />' +
                '<br />' +
                '<br /><br />' + (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') +
                '<br />Housing Coordinator';
            result.add(body);

            result.add(saveHousingOptionsAttachment(housingid, primarycontact));

        }else if(typez == 'release_bid'){
            List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE Name ='Release Bid'];
            subject = template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name).replace('{DateIn}',dateIn).replace('{DateOut}',dateOut) : '';
            result.add(subject);
            if(template.size() > 0) body = (template[0].HTMLValue != null ? template[0].HTMLValue.replace('{PrimaryHousingCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
                                            .replace('{ContactName}',primary_name)
                                            .replace('{VendorName}',bidAux[0].Vendor__r.Name)
                                            .replace('{ProductionName}',productionAux[0].Name)
                                            .replace('{DateIn}',dateIn)
                                            .replace('{DateOut}',dateOut) : '');
            result.add(body);
        }else*/ if(typez == 'release_bid2'){
            List<Ground__c> tripTemplate = [SELECT Id, Email_Subject_Release_Bid__c, Email_Body_Release_Bid__c FROM Ground__c WHERE Id =: tripid];
            if(tripTemplate.size() > 0 && tripTemplate[0].Email_Body_Release_Bid__c != null && tripTemplate[0].Email_Subject_Release_Bid__c != null){
                subject = tripTemplate[0].Email_Subject_Release_Bid__c.unescapeHtml4();
                result.add(subject);
                body = tripTemplate[0].Email_Body_Release_Bid__c.unescapeHtml4();
                result.add(body);
            }else{
                List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='GT_Release_Bid'];
                //subject = template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name).replace('{DateIn}',dateIn).replace('{DateOut}',dateOut) : '';
                subject = template.size() > 0 ? template[0].Subject.unescapeHtml4() : '';
                result.add(subject);
                if(template.size() > 0) body = template[0].HTMLValue != null ? template[0].HTMLValue.unescapeHtml4() : '';
                result.add(body);
            }
        }
        
        result.add(productionAux[0].Name);
        
        return result;
    }
    
    public void sendPreviewPdf(){
        emailMessage = '';
        try{
            emailMessage = sendEmail(emailbid_to,emailbid_cc,emailbid_bcc,emailbid_subject,releaseEmailBid_body,emailAttachs,opportunityId,tripViewId);
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
    public static User verifyEmailUser(String userId, String productionId, String tripId){
        User userActual = new User();
        Map<String,User> associationsMap = new Map<String,User>();
        Set<Id> userIds = new Set<Id>();
        for(Production_Associations__c pa : [SELECT Id, User__c, User__r.Name, User__r.Email, User__r.Phone, Team_Roles__c, Production_Opp__c, Ground__c FROM Production_Associations__c WHERE Production_Opp__c =: productionId AND RecordType.DeveloperName = 'Production_Coordinators' AND User__c <> NULL AND Team_Roles__c <> NULL]){
            if(pa.Team_Roles__c != null){
                for(String teamrole : pa.Team_Roles__c.split(';')){
                    if(pa.Production_Opp__c != null && teamrole.toLowerCase() != 'ground travel back-end coordinator'){
                        associationsMap.put(teamrole.toLowerCase(),new User(Id = pa.User__c));
                        userIds.add(pa.User__c);
                    }
                }
            }
        }
        List<Ground__c> groundList = [SELECT Id, Back_end_Coordinator__c FROM Ground__c WHERE Id =: tripId];
        if(!groundList.isEmpty()){
            associationsMap.put('ground travel back-end coordinator',new User(Id = groundList[0].Back_end_Coordinator__c));
            userIds.add(groundList[0].Back_end_Coordinator__c);
        }
        if(!associationsMap.isEmpty()){
            for(User us : [SELECT Id, Name, Email, Phone FROM User WHERE Id IN: userIds]){
                for(String key : associationsMap.keySet()){
                    if(associationsMap.get(key).Id == us.Id) associationsMap.put(key,us);
                }
            }
            if(associationsMap.get('primary gt coordinator') != null && associationsMap.get('primary gt coordinator').Id == userId) 
                userActual = associationsMap.get('primary gt coordinator');
            else if(associationsMap.get('ground travel back-end coordinator') != null && associationsMap.get('ground travel back-end coordinator').Id != null)
                userActual = associationsMap.get('ground travel back-end coordinator');
            else if(associationsMap.get('primary gt coordinator') != null)
                userActual = associationsMap.get('primary gt coordinator');
            
        }
        return userActual;
    }    
    public void sendEmailFormWithAttachs(){
        emailMessage = '';
        try{
            emailMessage = sendEmail(form_to,form_cc,form_bcc,form_subject,form_body,emailAttachs,opportunityId,tripViewId);
            //getBidJournals();
        }catch(DMLException e){
            emailMessage = e.getMessage();
        }
    }    
    public static String sendEmail(String toList, String ccList, String bccList, String subject, String body, String attachs, String oppid, String tripid){
        try{
            //TO
            Set<String> toAddress = new Set<String>();
            for(String k : toList.split(',')){
                if(k.trim() != '') toAddress.add(k.trim());
            }
            //CC
            Set<String> ccAddress = new Set<String>();
            for(String k : ccList.split(',')){
                if(k.trim() != '') ccAddress.add(k.trim());
            }
            //BCC
            Set<String> bccAddress = new Set<String>();
            for(String k : bccList.split(',')){
                if(k.trim() != '') bccAddress.add(k.trim());
            }
            
            //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: oppid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            User userActual = verifyEmailUser(UserInfo.getUserId(),oppid,tripid);
            
            List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
            Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
            if(userActual != null && userActual.Email != null && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(verifyWideAddress(userActual.Email));
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
                        efa.setFileName(cv.PathOnClient.subString(0,cv.PathOnClient.length()));
                        efa.setBody(cv.VersionData);
                        fileAttachments.add(efa);
                    }
                }
                if(fileAttachments.size() > 0) mail.setFileAttachments(fileAttachments);
            }
            system.debug(mail.getToAddresses());
            system.debug(mail.getCcAddresses());
            system.debug(mail.getBccAddresses());
            myEmails.add(mail);
            Messaging.SendEmailResult[] mailResult = Messaging.sendEmail(myEmails);
            if(!mailResult[0].isSuccess()){
                system.debug(mailResult[0].getErrors()[0].getMessage());
                return mailResult[0].getErrors()[0].getMessage();
            }
        }catch(System.EmailException e){
            system.debug(e.getMessage());
            return e.getMessage();
        }
        return '';
    }
    
    public void getSymbol(){
        for(SelectOption so : PickThePicklist('Revenue__c','CurrencyIsoCode')) symbolMap.put(so.getValue(),'');
        
        symbolMap.put('AED','?.?');
        symbolMap.put('AFN','Af');
        symbolMap.put('ALL','L');
        symbolMap.put('AMD','?');
        symbolMap.put('AOA','Kz');
        symbolMap.put('ARS','$');
        symbolMap.put('AUD','$');
        symbolMap.put('AWG','ƒ');
        symbolMap.put('AZN','???');
        symbolMap.put('BAM','??');
        symbolMap.put('BBD','$');
        symbolMap.put('BDT','?');
        symbolMap.put('BGN','??');
        symbolMap.put('BHD','?.?');
        symbolMap.put('BIF','?');
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
        symbolMap.put('CDF','?');
        symbolMap.put('CHF','?');
        symbolMap.put('CLP','$');
        symbolMap.put('CNY','¥');
        symbolMap.put('COP','$');
        symbolMap.put('CRC','¢');
        symbolMap.put('CUP','$');
        symbolMap.put('CVE','$');
        symbolMap.put('CZK','Kc');
        symbolMap.put('DJF','?');
        symbolMap.put('DKK','kr');
        symbolMap.put('DOP','$');
        symbolMap.put('DZD','?.?');
        symbolMap.put('EGP','£');
        symbolMap.put('ERN','Nfk');
        symbolMap.put('ETB','');
        symbolMap.put('EUR','€');
        symbolMap.put('FJD','$');
        symbolMap.put('FKP','£');
        symbolMap.put('GBP','£');
        symbolMap.put('GEL','?');
        symbolMap.put('GHS','?');
        symbolMap.put('GIP','£');
        symbolMap.put('GMD','D');
        symbolMap.put('GNF','?');
        symbolMap.put('GTQ','Q');
        symbolMap.put('GYD','$');
        symbolMap.put('HKD','$');
        symbolMap.put('HNL','L');
        symbolMap.put('HRK','Kn');
        symbolMap.put('HTG','G');
        symbolMap.put('HUF','Ft');
        symbolMap.put('IDR','Rp');
        symbolMap.put('ILS','?');
        symbolMap.put('INR','?');
        symbolMap.put('IQD','?.?');
        symbolMap.put('IRR','?');
        symbolMap.put('ISK','Kr');
        symbolMap.put('JMD','$');
        symbolMap.put('JOD','?.?');
        symbolMap.put('JPY','¥');
        symbolMap.put('KES','Sh');
        symbolMap.put('KGS','');
        symbolMap.put('KHR','?');
        symbolMap.put('KPW','?');
        symbolMap.put('KRW','?');
        symbolMap.put('KWD','?.?');
        symbolMap.put('KYD','$');
        symbolMap.put('KZT','?');
        symbolMap.put('LAK','?');
        symbolMap.put('LBP','?.?');
        symbolMap.put('LKR','Rs');
        symbolMap.put('LRD','$');
        symbolMap.put('LSL','L');
        symbolMap.put('LYD','?.?');
        symbolMap.put('MAD','?.?.');
        symbolMap.put('MDL','L');
        symbolMap.put('MGA','');
        symbolMap.put('MKD','???');
        symbolMap.put('MMK','K');
        symbolMap.put('MNT','?');
        symbolMap.put('MOP','P');
        symbolMap.put('MRU','UM');
        symbolMap.put('MUR','?');
        symbolMap.put('MVR','?.');
        symbolMap.put('MWK','MK');
        symbolMap.put('MXN','$');
        symbolMap.put('MYR','RM');
        symbolMap.put('MZN','MTn');
        symbolMap.put('NAD','$');
        symbolMap.put('NGN','?');
        symbolMap.put('NIO','C$');
        symbolMap.put('NOK','kr');
        symbolMap.put('NPR','?');
        symbolMap.put('NZD','$');
        symbolMap.put('OMR','?.?.');
        symbolMap.put('PAB','B/.');
        symbolMap.put('PEN','S/.');
        symbolMap.put('PGK','K');
        symbolMap.put('PHP','?');
        symbolMap.put('PKR','?');
        symbolMap.put('PLN','zl');
        symbolMap.put('PYG','?');
        symbolMap.put('QAR','?.?');
        symbolMap.put('RON','L');
        symbolMap.put('RSD','din');
        symbolMap.put('RUB','?.');
        symbolMap.put('RWF','?');
        symbolMap.put('SAR','?.?');
        symbolMap.put('SBD','$');
        symbolMap.put('SCR','?');
        symbolMap.put('SDG','£');
        symbolMap.put('SEK','kr');
        symbolMap.put('SGD','$');
        symbolMap.put('SHP','£');
        symbolMap.put('SLL','Le');
        symbolMap.put('SOS','Sh');
        symbolMap.put('SRD','$');
        symbolMap.put('STN','Db');
        symbolMap.put('SYP','?.?');
        symbolMap.put('SZL','L');
        symbolMap.put('THB','?');
        symbolMap.put('TJS','??');
        symbolMap.put('TMT','m');
        symbolMap.put('TND','?.?');
        symbolMap.put('TOP','T$');
        symbolMap.put('TRY','£');
        symbolMap.put('TTD','$');
        symbolMap.put('TWD','$');
        symbolMap.put('TZS','Sh');
        symbolMap.put('UAH','?');
        symbolMap.put('UGX','Sh');
        symbolMap.put('USD','$');
        symbolMap.put('UYU','$');
        symbolMap.put('UZS','');
        symbolMap.put('VEF','Bs F');
        symbolMap.put('VND','?');
        symbolMap.put('VUV','Vt');
        symbolMap.put('WST','T');
        symbolMap.put('XAF','?');
        symbolMap.put('XCD','$');
        symbolMap.put('XPF','?');
        symbolMap.put('YER','?');
        symbolMap.put('ZAR','R');
        symbolMap.put('ZMW','ZK');
        symbolMap.put('ZWL','$');
    }
    
    @RemoteAction
    global static String searchVehicleTrip(String query, String tripid){
        query = '%' + query + '%';
        List<wrapperData> vehicleList = new List<wrapperData>();
        String description;
        for(Ground__c g : [SELECT Id, Vehicle_Ref__c FROM Ground__c WHERE Vehicle_Ref__c LIKE: query AND GT_Trip_Details__c =: tripid  AND RecordType.Name = 'Vehicle Type' AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL]){
            vehicleList.add(new wrapperData(g.Id,g.Vehicle_Ref__c,''));
        }
        return JSON.serialize(vehicleList);
    }
    
    @RemoteAction
    global static Contact getDataContact(String contactId){
        return [SELECT Id, AccountId, FirstName, LastName, Phone, Work_Phone_Extension__c, Email, MobilePhone, Alternate_Email__c, Fax, Designation_title__c, Description, MailingStreet, MailingPostalCode, OtherStreet, City__c, City__r.Name FROM Contact WHERE Id =: contactId];
    }
    
    @RemoteAction
    global static Journal__c getDataJournal(String journalId){
        return [SELECT Id, Housing__c, Issue__c, Journal_Entry__c, Mark_Journal_trace_complete__c, Parent_Journal__c, Production__c, Production_checkbox__c, RecordTypeId, RecordType.Name, Sales__c, Trace_Coordinator__c, Trace_Date__c, Trace_Date_Formula__c, Vendor_Checkbox__c FROM Journal__c WHERE Id =: journalId];
    }
    
    @RemoteAction
    global static List<String> getDataJournalRelated(String journalId, String ztype){
        List<String> dataList = new List<String>();
        /*if(ztype == 'production_companies'){
            for(Related_Companies__c rc : [SELECT Id, Company__c FROM Related_Companies__c WHERE Journal__c =: journalId AND Company__c <> null]) dataList.add(rc.Company__c);
        }*/
        if(ztype == 'production_contacts'){
            for(Related_Contact__c rc : [SELECT Id, Contact__c FROM Related_Contact__c WHERE Journal__c =: journalId AND Contact__c <> null AND Type__c includes ('Production Contacts')]) dataList.add(rc.Contact__c);
        } 
        if(ztype == 'company_contacts'){
            for(Related_Contact__c rc : [SELECT Id, Contact__c FROM Related_Contact__c WHERE Journal__c =: journalId AND Contact__c <> null AND Type__c includes ('Company Contacts')]) dataList.add(rc.Contact__c);
        }
        system.debug(dataList);
        return dataList;
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
        List<Ground__c> groundAux = [SELECT Id, Name, RecordType.Name, Start_Date__c, End_Date__c FROM Ground__c WHERE Id =: tripid];
        List<Opportunity> productionAux = [SELECT Id, Name, Alias_with_Production_Name__c FROM Opportunity WHERE Id =: opportunityid];
        //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
        User userActual = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripid);
        List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName = 'GT_Release_Bid'];
        String dateIn = (groundAux[0].Start_Date__c != null ? Datetime.newInstance(groundAux[0].Start_Date__c.year(),groundAux[0].Start_Date__c.month(),groundAux[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateOut = (groundAux[0].End_Date__c != null ? Datetime.newInstance(groundAux[0].End_Date__c.year(),groundAux[0].End_Date__c.month(),groundAux[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        result.add(template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name).replace('{StartDate}',dateIn).replace('{EndDate}',dateOut) : '');
        result.add(template[0].HTMLValue != null ? template[0].HTMLValue.replace('{GroundTravelCoordinator}',userActual != null && userActual.Name != null ? userActual.Name : '')
                                        .replace('{VendorName}',bidAux.Vendor__r.Name)
                                        .replace('{ProductionName}',productionAux[0].Name)
                                        .replace('{StartDate}',dateIn)
                                        .replace('{EndDate}',dateOut) : '');
        return result;
    }
    
    @RemoteAction
    global static String validateDates(String datein, String dateout){
        Date todayDate = system.today();
        if(parseDate(datein) < todayDate || parseDate(dateout) < todayDate) return 'You can not create a trip for past dates';
        if(parseDate(datein) > parseDate(dateout)) return 'Cannot post-date Start or End Date';
        return '';
    }
    
    public static Date parseDate(String inDate) {
        Date dateRes = null;
        //	1 - Try locale specific mm/dd/yyyy or dd/mm/yyyy	
        try {
            String candDate		= inDate.substring(0,Math.min(10,inDate.length()));// grab date portion only m[m]/d[d]/yyyy , ignore time
            dateRes 	= Date.parse(candDate);
        }
        catch (Exception e) {}        
        if (dateRes == null) {
            //	2 - Try yyyy-mm-dd			
            try {
                String candDate		= inDate.substring(0,10);// grab date portion only, ignore time, if any
                dateRes				= Date.valueOf(candDate);
            }
            catch (Exception e) {} 
        }
        return dateRes;
    }
    
    @RemoteAction
    global static String searchCreditCard(String query, String opportunityId){
        query = '%' + query + '%';
        Set<String> contactIds = new Set<String>();
        for(Production_Associations__c pa : [SELECT Id, Contact__c FROM Production_Associations__c WHERE Production_Opp__c =: opportunityId AND Contact__c <> NULL AND RecordType.Name = 'Production Contacts' AND Status__c = 'Associated']){
            contactIds.add(pa.Contact__c);
        }
        system.debug(contactIds);
        
        List<wrapperData> ccList = new List<wrapperData>();
        for(Credit_Card__c cc : [SELECT Id, Credit_card_number__c, Contact__r.Name, Credit_Card_Full_Name__c FROM Credit_Card__c WHERE Contact__c IN: contactIds AND Purpose__c includes ('All','Ground Transportation Only','Secondary') AND (Credit_Card_Full_Name__c LIKE: query OR Name LIKE: query)]){
            ccList.add(new wrapperData(cc.Id,cc.Credit_Card_Full_Name__c,''));
        }
        system.debug(ccList);
        
        return JSON.serialize(ccList);
    }
    
    @RemoteAction
    global static String searchCity(String query){
        query = '%' + query + '%';
        List<wrapperData> cityList = new List<wrapperData>();
        for(City__c c : [SELECT Id, Name FROM City__c WHERE Name LIKE: query LIMIT 20]){
            cityList.add(new wrapperData(c.Id,c.Name,''));
        }
        return JSON.serialize(cityList);
    }
    
    @RemoteAction
    global static String searchFreight(String query, String productionid){
        query = '%' + query + '%';
        List<wrapperData> freightList = new List<wrapperData>();
        for(Freight__c freightTrip : [SELECT Id, Name, Start_Date__c, Start_city__r.Name, End_Date__c, End_city__r.Name FROM Freight__c WHERE Name LIKE: query AND Production__c =:productionid AND (RecordType.DeveloperName = 'Freight_Trip_Details') LIMIT 20]) freightList.add(new wrapperData(freightTrip.Id, (freightTrip.Start_Date__c != null ? Datetime.newInstance(freightTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('MM/dd/yyyy') : '') + (freightTrip.End_Date__c != null ? '-' + Datetime.newInstance(freightTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('MM/dd/yyyy') : '') + (freightTrip.Start_city__r.Name != null ? ' ' + freightTrip.Start_city__r.Name : '') + (freightTrip.End_city__r.Name != null ? '-' + freightTrip.End_city__r.Name : ''), ''));
        return JSON.serialize(freightList);
    }
    
    @RemoteAction
    global static String searchAccount(String query, String recordtype){
        query = '%' + query + '%';
        List<wrapperData> accountList = new List<wrapperData>();
        for(Account a : [SELECT Id, Name FROM Account WHERE Name LIKE: query AND RecordType.Name =: recordtype LIMIT 20]){
            accountList.add(new wrapperData(a.Id,a.Name,''));
        }
        return JSON.serialize(accountList);
    }
    
    @RemoteAction
    global static String searchAirport(String query){
        query = '%' + query + '%';
        List<wrapperData> airportList = new List<wrapperData>();
        String nameAux;
        for(Airport__c a : [SELECT Id, Name, Airport_Code__c, City__c, City__r.Name FROM Airport__c WHERE Name LIKE: query OR Airport_Code__c LIKE: query LIMIT 20]){
            nameAux = (a.Airport_Code__c != null ? a.Airport_Code__c + ' - ' : '') + a.Name + (a.City__c != null ? ' - ' + a.City__r.Name : '');
            airportList.add(new wrapperData(a.Id,nameAux,''));
        }
        return JSON.serialize(airportList);
    }
    
    @RemoteAction
    global static String searchVenue(String query){
        query = '%' + query + '%';
        List<wrapperData> venueList = new List<wrapperData>();
        for(Account a : [SELECT Id, Name FROM Account WHERE Name LIKE: query LIMIT 20]){
            venueList.add(new wrapperData(a.Id,a.Name,''));
        }
        return JSON.serialize(venueList);
    }
    
    @RemoteAction
    global static String searchProd(String query, Boolean all){
        query = '%' + query + '%';
        List<wrapperDataProd> prodList = new List<wrapperDataProd>();
        List<Opportunity> productionList;
        if(!all)  productionList = [SELECT Id, Alias_with_Production_Name__c, Name, StageName, Office_Location__c, Company__c FROM Opportunity WHERE Name LIKE: query AND StageName = 'Active' LIMIT 10];
        else productionList = [SELECT Id, Alias_with_Production_Name__c, Name, StageName, Office_Location__c, Company__c FROM Opportunity WHERE Name LIKE: query LIMIT 10];
            
        for(Opportunity o : productionList){
            prodList.add(new wrapperDataProd(o.Id,o.Name,o.StageName,o.Company__c != null ? o.Company__c : '',o.Office_Location__c != null ? o.Office_Location__c : ''));
        }
        return JSON.serialize(prodList);
    }
    
    @RemoteAction
    global static String searchContactByAccount(String query, String accountId){
        query = '%' + query + '%';
        Map<String,Contact> contactMap = new Map<String,Contact>();
        for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE AccountId =: accountId AND Name LIKE: query AND Email <> null]) contactMap.put(c.Id,c);
        
        for(AccountContactRelation acr : [SELECT Id, ContactId, Contact.Name, Contact.Email FROM AccountContactRelation WHERE AccountId =: accountId AND Contact.Name LIKE: query AND Contact.Email <> null]) contactMap.put(acr.ContactId,acr.Contact);
        
        List<wrapperData> contactList = new List<wrapperData>();
        for(String key : contactMap.keySet()) contactList.add(new wrapperData(key,contactMap.get(key).Name + ' <' + contactMap.get(key).Email + '>' ,contactMap.get(key).Email));        
        return JSON.serialize(contactList);
    }
    
    public static String validateError(String error){
        String message = '';
        if(error.contains('DUPLICATES_DETECTED')) message = 'You\'re creating a duplicate record. We recommend you use an existing record.';
        else message = error;
        return message;
    }
    
    global class wrapperSearchPL{
        public String dataid;
        public String dataname;
        public wrapperSearchPL(String cdataid, String cdataname){
            dataid = cdataid;
            dataname = cdataname;
        }
    }
    
    global class wrapperVendor{
        public String vendorid;
        public String vendorname;
        public wrapperVendor(String cvendorid, String cvendorname){
            vendorid = cvendorid;
            vendorname = cvendorname;
        }
    }
    
    global class wrapperData{
        public String data;
        public String value;
        public String extra1;
        
        public wrapperData(String cdata, String cvalue, String cextra1){
            data = cdata;
            value = cvalue;
            extra1 = cextra1;
        }
    }
    
    global class wrapperDataProd{
        public String data;
        public String value;
        public String extra1;
        public String extra2;
        public String extra3;
        
        public wrapperDataProd(String cdata, String cvalue, String cextra1, String cextra2, String cextra3){
            data = cdata;
            value = cvalue;
            extra1 = cextra1;
            extra2 = cextra2;
            extra3 = cextra3;
        }
    }
    
    //GT Trip Wrappers.
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
    //End GT Trip Wrappers.
    
    public static List<SelectOption> PickThePicklist(string YourObjectName,string YourFieldName){
        List<SelectOption> picklists = new List<SelectOption>(); 
        List<Schema.PicklistEntry> PicklistValues  = Schema.getGlobalDescribe().get(YourObjectName).getDescribe().fields.getMap().get(YourFieldName).getDescribe().getPicklistValues();
        for( Schema.PicklistEntry PicklistValue : PicklistValues){
            if(YourFieldName == 'CurrencyIsoCode'){
                picklists.add(new SelectOption(PicklistValue.getValue(),PicklistValue.getValue() + ' - ' + PicklistValue.getLabel()));
            }else{
                picklists.add(new SelectOption(PicklistValue.getValue(),PicklistValue.getLabel()));
            }
        }
        return picklists;
    }
    
    public static String verifyWideAddress(String email){
       String oweaId;
       List<OrgWideEmailAddress> oweaList;
       if(Test.isRunningTest()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; else oweaList = [select Id from OrgWideEmailAddress where Address =: email];
       if(oweaList.isEmpty()) oweaList = [select Id from OrgWideEmailAddress where Address =: Dashboard__c.getOrgDefaults().Email_Default__c]; //Email default
       oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
       return oweaId;
   }
    //GT Trip SendOptions Methods.
    public void openSendOptions(){
        contactsByProduction = new List<SelectOption>();
        contactWrapperByProduction = new List<ContactWrapper>();
        Map<Id, Contact> contactsMap = new Map<Id, Contact>();
        for(Production_Associations__c productionAssoc:[Select Id, Contact__c, Contact__r.Order__c, Contact__r.FirstName, Contact__r.LastName, Contact__r.Name, Designation_title__c, Contact__r.Email, Contact__r.Phone From Production_Associations__c Where Production_Opp__c =:opportunityid and Role__c includes ('Primary GT', 'CC: GT', 'Options') and Contact__c != null and Contact__r.Email != null order by Contact__r.Order__c asc Nulls Last]) contactsMap.put(productionAssoc.Contact__c, new Contact(id = productionAssoc.Contact__c, Order__c = productionAssoc.Contact__r.Order__c, FirstName = productionAssoc.Contact__r.FirstName, LastName = productionAssoc.Contact__r.LastName, Name__c = productionAssoc.Contact__r.Name, Designation_title__c = productionAssoc.Designation_title__c, Email = productionAssoc.Contact__r.Email, Phone = productionAssoc.Contact__r.Phone));
        for(Contact contact : contactsMap.values()){
            contactsByProduction.add(new SelectOption(contact.id, contact.Name__c));
            contactWrapperByProduction.add(new ContactWrapper(contact, contact.Order__c == 1, contact.Order__c == 1));
        }
        /**
        *  @Conga: Update for Conga.
        */
        List<Production_Associations__c> productionAssociations = [SELECT User__c, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =:opportunityid AND RecordType.DeveloperName = 'Production_Coordinators' and User__c != NULL and Team_Roles__c includes ('Primary GT Coordinator')];
        sendOptions_emailFromUserId = !productionAssociations.isEmpty() ? productionAssociations[0].User__c : null;
        sendOptions_congaEmailFromId = !productionAssociations.isEmpty() ? verifyWideAddress(productionAssociations[0].User__r.Email) : null;
        congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
        for(APXTConga4__Conga_Merge_Query__c congaQuery:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Merge_Query__c Where APXTConga4__Name__c in ('GT - BidsWithOptionsByGroundTravel', 'GT - SubTripsByTripId', 'GT - ContactById', 'GT - ProductionAssociationsByOppId', 'GT - UserById')]) congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
        sendOptions_congaQueriesJson = JSON.serialize(congaQueriesMap);
        List<APXTConga4__Conga_Template__c> congaTemplates = [Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c = 'GT - Ground Travel Options'];
        sendOptions_congaTemplateId = !congaTemplates.isEmpty() ? congaTemplates[0].id : null;
        List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id, APXTConga4__Subject__c From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c = 'GT - Options'];
        sendOptions_congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        if(!congaEmailTemplates.isEmpty() && String.isNotBlank(congaEmailTemplates[0].APXTConga4__Subject__c)) sendOptions_congaEmailSubject = congaEmailTemplates[0].APXTConga4__Subject__c.replace('{City}', tripView.Start_City__c != null ? tripView.Start_City__r.Name : '').replace('{StartDate}', tripView.Start_Date__c != null ? Datetime.newInstance(tripView.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{EndDate}', tripView.End_Date__c != null ? Datetime.newInstance(tripView.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{TripName}', tripView.Name);
        else sendOptions_congaEmailSubject = 'Ground Travel Options - ' + (tripView.Start_City__c != null ? tripView.Start_City__r.Name : '') + ' - ' + (tripView.Start_Date__c != null ? Datetime.newInstance(tripView.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' - ' + (tripView.End_Date__c != null ? Datetime.newInstance(tripView.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' (' + tripView.Name + ')';
        /**
        *  @/Conga
        */
    }
    public void changeContactProduction(){
        for(ContactWrapper contactWrapperItem : contactWrapperByProduction){
            if(sendOptions_primaryContactId == contactWrapperItem.c.Id){
                contactWrapperItem.selected = true;
                contactWrapperItem.disabled = true;
            }
            else{
                if(contactWrapperItem.selected && contactWrapperItem.disabled){
                    contactWrapperItem.selected = false;
                    contactWrapperItem.disabled = false;
                }
            }
        }
    }
    //End GT Trip Methods
    //sendLink Methods
    public void sendLink(){
        system.debug('communityNoteCoordinator :: ' + communityNoteCoordinator);
        system.debug('#sendLink()');
        Set<String> toAddresses = new Set<String>();
        Set<String> ccAddresses = new Set<String>();
        Contact primaryContact = new Contact();
        String primary_contact_name = '';
        String primary_contact_email = '';
        String primary_contact_designationtitle = '';
        String cc_contact_emails = '';
        for(ContactWrapper cw : contactWrapperByProduction){
            if(cw.selected && cw.disabled){
                primary_contact_name = cw.c.Name;
                primary_contact_email = cw.c.Email;
                primary_contact_designationtitle = cw.c.Designation_title__c;
                primaryContact = cw.c;
                toAddresses.add(cw.c.Email);
            }
            if(!cw.disabled && cw.selected){
                ccAddresses.add(cw.c.Email);
                    cc_contact_emails = cc_contact_emails + cw.c.Email + ', ';
            }
        }
        
        List<Ground__c> serviceMap = [SELECT Id, Name, /*City__c, City__r.Name,*/ Start_Date__c, End_Date__c, RecordType.DeveloperName FROM Ground__c WHERE Id =: tripView.id];
        String dateStart = (serviceMap[0].Start_Date__c != null ? Datetime.newInstance(serviceMap[0].Start_Date__c.year(),serviceMap[0].Start_Date__c.month(),serviceMap[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateEnd = (serviceMap[0].End_Date__c != null ? Datetime.newInstance(serviceMap[0].End_Date__c.year(),serviceMap[0].End_Date__c.month(),serviceMap[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        String subject;
    
        List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
        List<Messaging.SingleEmailMessage>  myEmails = new List<Messaging.SingleEmailMessage>();
        Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
        if(prodAssocAux.size() > 0 && !Test.isRunningTest()) mail.setOrgWideEmailAddressId(verifyWideAddress(prodAssocAux[0].User__r.Email));
        mail.setToAddresses(new List<String>(toAddresses));
        if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
        
        String body;
        subject = 'Community Link - Ground Travel Options - ' + /*(serviceMap[0].City__c != null ? serviceMap[0].City__r.Name : '') + ' - ' +*/ dateStart + '-' + dateEnd + ' (' + serviceMap[0].Name + ')';
        body = 'Hi ' + (String.isNotEmpty(primaryContact.FirstName) ? primaryContact.FirstName : '') + 
            '<br /><br />You have Ground Travel Options available for your review.' + 
            '<br /><br />Please log on to view:' + 
            //'<br /><br /><a href="https://ccdev-roadrebel.cs42.force.com/" target="_blank">Link to Community Portal</a>' + 
            '<br /><br /><a href="'+ (communityURLvalue != null ? communityURLvalue : '') +'/s/?service=ground&record=' + tripView.id + '" target="_blank">Link to Community Portal</a>' + 
            '<br /><br />Thank you,' + 
            '<br /><br />' + (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') + 
            '<br />Primary Ground Travel Coordinator';
    
        mail.setSubject(subject);
        mail.setHtmlBody(body);
        myEmails.add(mail);
        
        insert new Journal__c(
            RecordTypeId=journal_tripJournalRT,
            G__c=tripView.id,
            Journal_Entry__c='GT options has been sent to: ' + primary_contact_name + ' at ' + primary_contact_email + (cc_contact_emails != '' ? ', cc: ' + cc_contact_emails.substring(0,cc_contact_emails.length() - 2) : '')
        );
        
        if(tripView != null && (tripView.Status_Ground__c != 'Contracted' || tripView.Status_Ground__c != 'In Contracting')){
            tripView.Status_Ground__c = 'Pending Client Choice';
            update new Ground__c(id = tripView.id, Community_Notes__c = communityNoteCoordinator, Community_Note_Available__c = communityNoteCoordinator == null || communityNoteCoordinator == '' ? false : true, Status_Ground__c = 'Pending Client Choice', Options_sent_to_client__c = Datetime.now());
            List<Itinerary__c> itineraries =  [SELECT Id FROM Itinerary__c WHERE GT__c =:tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
            if(!itineraries.isEmpty()) update new Itinerary__c(Id = itineraries[0].Id, Status__c = 'Pending Client Choice');
            searchTrip();
        }
        
        if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
        //contactWrapperByProduction = new List<ContactWrapper>();
    }
	//End sendLink Methods
    /**
    *  @Conga: Conga Methods.
    */
    public void congaItineraryDetails(){
        if(String.isNotBlank(opportunityid)){
            Map<Id, Ground__c> tripsMap = new Map<Id, Ground__c>();
            for(Ground__c ground : [Select id from Ground__c where Production_Ground__c =:opportunityid and RecordType.DeveloperName = 'GT_Trip_Details']) tripsMap.put(ground.id, new Ground__c(id = ground.id, Bid_ID_Conga__c = ''));
            for(Bid__c bid : [Select id, GT__c, Name from Bid__c where GT__c in:tripsMap.keySet() and RecordType.DeveloperName = 'GT_Bid' and Status__c = 'Contracted']) tripsMap.get(bid.GT__c).Bid_ID_Conga__c = bid.Name;
            if(!tripsMap.values().isEmpty()){
                try{
                    update tripsMap.values();
                }
                catch(DmlException e){
                    System.debug('GTDashboardController.congaItineraryDetails() - DmlException: ' + e.getMessage());
                }
            }
        }
    }
    public void congaSendOptions(){
        List<String> congaParameters = new List<String>();
        String ccEmails = '';
        for(ContactWrapper contactWrapperItem : contactWrapperByProduction) if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
        congaParameters.add('&id=' + tripView.id + (congaQueriesMap.containsKey('GT - BidsWithOptionsByGroundTravel') ? '&QueryId=[Bid]' + congaQueriesMap.get('GT - BidsWithOptionsByGroundTravel').Id + '?pv0=' + tripView.id + (congaQueriesMap.containsKey('GT - SubTripsByTripId') ? ',[SubTrips]' + congaQueriesMap.get('GT - SubTripsByTripId').Id + '?pv0=' + tripView.id : '') + (congaQueriesMap.containsKey('GT - ContactById') ? ',[Contact]' + congaQueriesMap.get('GT - ContactById').Id + '?pv0=' + sendOptions_primaryContactId : '') + (congaQueriesMap.containsKey('GT - UserById') ? ',[EmailFromUser]' + congaQueriesMap.get('GT - UserById').Id + '?pv0=' + (String.isNotBlank(sendOptions_emailFromUserId) ? sendOptions_emailFromUserId : '') : '') : '') + (String.isNotBlank(sendOptions_congaEmailTemplateId) ? '&CongaEmailTemplateId=' + sendOptions_congaEmailTemplateId : '') + '&EmailSubject=' + sendOptions_congaEmailSubject.replace(' ', '+') + (String.isNotBlank(sendOptions_congaEmailFromId) ? '&EmailFromID=' + sendOptions_congaEmailFromId : '') + '&EmailToId=' + sendOptions_primaryContactId + '&EmailCC=' + ccEmails + (String.isNotBlank(sendOptions_congaTemplateId) ? '&TemplateId=' + sendOptions_congaTemplateId : '') + '&OFN=GT+Options');
        try{
            congaSendEmail(congaParameters);
            
            if(tripView != null && (tripView.Status_Ground__c != 'Contracted' || tripView.Status_Ground__c != 'In Contracting')){
                tripView.Status_Ground__c = 'Pending Client Choice';
                update new Ground__c(id = tripView.id, Status_Ground__c = 'Pending Client Choice', Options_sent_to_client__c = Datetime.now());
                List<Itinerary__c> itineraries =  [SELECT Id FROM Itinerary__c WHERE GT__c =:tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
                if(!itineraries.isEmpty()) update new Itinerary__c(Id = itineraries[0].Id, Status__c = 'Pending Client Choice');
                searchTrip();
            }
        }
        catch(Exception e){
            System.debug('###GTDashboardController.congaSendOptions() - Exception: ' + e.getMessage());
        }
    }
    public void congaSendBidRequest(){
        if(String.isNotBlank(sendBidRequest_accountIds)){
            Map<String,Contact> contactsMap = new Map<String,Contact>();
            for(String accountId:sendBidRequest_accountIds.split(',')) contactsMap.put(sendBidRequestMap.get(accountId).Vendor_Contact__c, new Contact());
            for(Contact contact:[Select Id, Name, Email from Contact where Id in:contactsMap.keySet()]) contactsMap.put(contact.Id, contact);
            Map<Id, Bid__c> bidUpdateMap = new Map<Id, Bid__c>();
            List<Journal__c> journals = new List<Journal__c>();
            String ccEmails = '';
            List<String> congaParameters = new List<String>();
            Integer i = 1;
            for(String accountId:sendBidRequest_accountIds.split(',')){
                for(ContactWrapper contactWrapperItem:contactsByVendor_bidRequestMap.get(accountId)) if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
                for(ContactWrapper contactWrapperItem:(sendBidRequestMap.get(accountId).Vendor__r.ParentId != null ? contactsByVendorParent_bidRequestMap.get(sendBidRequestMap.get(accountId).Vendor__r.ParentId) : new List<ContactWrapper>())) if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
                congaParameters.add('&id=' + sendBidRequestMap.get(accountId).id + (congaQueriesMap.containsKey('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap.get('GT - BidById').Id + '?pv0=' + sendBidRequestMap.get(accountId).id + (congaQueriesMap.containsKey('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap.get('GT - SubTripsByBidId').Id + '?pv0=' + sendBidRequestMap.get(accountId).id : '') + (congaQueriesMap.containsKey('GT - AssociatedCitiesByAccountId') ? ',[AssociatedCities]' + congaQueriesMap.get('GT - AssociatedCitiesByAccountId').Id + '?pv0=' + accountId : '') + (congaQueriesMap.containsKey('GT - ContactsByAccountId') ? ',[VendorContacts]' + congaQueriesMap.get('GT - ContactsByAccountId').Id + '?pv0=' + accountId : '') + (congaQueriesMap.containsKey('GT - ContactById') ? ',[Contact]' + congaQueriesMap.get('GT - ContactById').Id + '?pv0=' + contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).id : '') + (congaQueriesMap.containsKey('GT - UserById') ? ',[EmailFromUser]' + congaQueriesMap.get('GT - UserById').Id + '?pv0=' + (String.isNotBlank(sendBidRequest_emailFromUserId) ? sendBidRequest_emailFromUserId : '') : '') : '') + '&CongaEmailTemplateId='+ sendBidRequest_congaEmailTemplateId + '&EmailSubject=' + sendBidRequest_congaEmailSubject.replace('{BidName}', sendBidRequestMap.get(accountId).Name).replace(' ', '+') + (String.isNotBlank(sendBidRequest_congaEmailFromId) ? '&EmailFromID=' + sendBidRequest_congaEmailFromId : '') + '&EmailToId=' + contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).id + '&EmailCC=' + ccEmails + '&TemplateId=' + sendBidRequest_congaTemplateId1 + ',' + sendBidRequest_congaTemplateId2 + '&OFN=GT+Bid' + sendBidRequestMap.get(accountId).Name);
                if(sendBidRequest_accountIds.split(',').size() == i || i >= 100){
                    try{
                        congaSendEmail(congaParameters);
                    }
                    catch(Exception e){
                        System.debug('###GTDashboardController.congaSendBidRequest() - Exception: ' + e.getMessage());
                    }
                    i = 1;
                    congaParameters.clear();
                    ccEmails = '';
                }
                else i++;
                if(sendBidRequestMap.get(accountId) != null && sendBidRequestMap.get(accountId).Status__c != 'Contracted') bidUpdateMap.put(sendBidRequestMap.get(accountId).id, new Bid__c(Id = sendBidRequestMap.get(accountId).Id, Status__c = 'Sent'));
                journals.add(new Journal__c(RecordTypeId = journal_bidjournalRT, Bid__c = sendBidRequestMap.get(accountId).Id, Journal_Entry__c = 'GT Bid Request was sent to ' + (String.isNotBlank(contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Name) ? contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Name : '') + ' ' + (String.isNotBlank(contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Email) ? contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Email : '') + (String.isNotBlank(ccEmails) ? ', cc: ' + ccEmails : '')));
            }
            if(!bidUpdateMap.values().isEmpty()) update bidUpdateMap.values();
            if(tripView != null && (tripView.Status_Ground__c != 'Contracted' || tripView.Status_Ground__c != 'In Contracting')){
                system.debug(tripView);
                tripView.Status_Ground__c = 'Bid Request Stage';
                update new Ground__c(id = tripView.id, Status_Ground__c = 'Bid Request Stage', Email_Body_Bid_Request__c = null);
                List<Itinerary__c> itineraries =  [SELECT Id FROM Itinerary__c WHERE GT__c =:tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
                if(!itineraries.isEmpty()) update new Itinerary__c(Id = itineraries[0].Id, Status__c = 'Bid Request Stage');
            }
            if(!journals.isEmpty()) insert journals;
            isBidRequestRendered = false;
        }
    }
    public void congaSendEditBidRequest(){
        if(String.isNotBlank(sendBidRequest_accountIds)){
            Map<String,Contact> contactsMap = new Map<String,Contact>();
            for(String accountId:sendBidRequest_accountIds.split(',')) contactsMap.put(sendBidRequestMap.get(accountId).Vendor_Contact__c, new Contact());
            for(Contact contact:[Select Id, Name, Email from Contact where Id in:contactsMap.keySet()]) contactsMap.put(contact.Id, contact);
            User userActual = verifyEmailUser(UserInfo.getUserId(),opportunityid,tripViewId);
            APXTConga4__Conga_Email_Template__c congaEmailTemplate = new APXTConga4__Conga_Email_Template__c(APXTConga4__Name__c = 'GT Request - ' + tripView.Name, SObjectId__c = 'GTRequest-' + tripView.id, APXTConga4__HTMLBody__c = emailBody.replace('{GroundTravelCoordinator}', userActual != null ? userActual.Name : '').replace('{CoordinatorPhone}',userActual != null && userActual.Phone != null ? userActual.Phone : ''));
            try{
                upsert congaEmailTemplate SObjectId__c;
            }
            catch(Exception e){
                System.debug('###GTDashboardController.congaSendEditBidRequest() - Exception: ' + e.getMessage());
            }
            Map<Id, Bid__c> bidUpdateMap = new Map<Id, Bid__c>();
            List<Journal__c> journals = new List<Journal__c>();
            String ccEmails = '';
            List<String> congaParameters = new List<String>();
            Integer i = 1;
            for(String accountId:sendBidRequest_accountIds.split(',')){
                for(ContactWrapper contactWrapperItem:contactsByVendor_bidRequestMap.get(accountId)) if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
                for(ContactWrapper contactWrapperItem:(sendBidRequestMap.get(accountId).Vendor__r.ParentId != null ? contactsByVendorParent_bidRequestMap.get(sendBidRequestMap.get(accountId).Vendor__r.ParentId) : new List<ContactWrapper>())) if(!contactWrapperItem.disabled && contactWrapperItem.selected) ccEmails = String.isNotBlank(ccEmails) ? ccEmails + ', ' + contactWrapperItem.c.Email : contactWrapperItem.c.Email;
                congaParameters.add('&id=' + sendBidRequestMap.get(accountId).id + (congaQueriesMap.containsKey('GT - BidById') ? '&QueryId=[Bid]' + congaQueriesMap.get('GT - BidById').Id + '?pv0=' + sendBidRequestMap.get(accountId).id + (congaQueriesMap.containsKey('GT - SubTripsByBidId') ? ',[SubTrips]' + congaQueriesMap.get('GT - SubTripsByBidId').Id + '?pv0=' + sendBidRequestMap.get(accountId).id : '') + (congaQueriesMap.containsKey('GT - AssociatedCitiesByAccountId') ? ',[AssociatedCities]' + congaQueriesMap.get('GT - AssociatedCitiesByAccountId').Id + '?pv0=' + accountId : '') + (congaQueriesMap.containsKey('GT - ContactsByAccountId') ? ',[VendorContacts]' + congaQueriesMap.get('GT - ContactsByAccountId').Id + '?pv0=' + accountId : '') + (congaQueriesMap.containsKey('GT - ContactById') ? ',[Contact]' + congaQueriesMap.get('GT - ContactById').Id + '?pv0=' + contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).id : '') + (congaQueriesMap.containsKey('GT - UserById') ? ',[EmailFromUser]' + congaQueriesMap.get('GT - UserById').Id + '?pv0=' + (String.isNotBlank(sendBidRequest_emailFromUserId) ? sendBidRequest_emailFromUserId : '') : '') : '') + '&CongaEmailTemplateId='+ (String.isNotEmpty(congaEmailTemplate.id) ? congaEmailTemplate.id : sendBidRequest_congaEmailTemplateId) + '&EmailSubject=' + sendBidRequest_congaEmailSubject.replace('{BidName}', sendBidRequestMap.get(accountId).Name).replace(' ', '+') + (String.isNotBlank(sendBidRequest_congaEmailFromId) ? '&EmailFromID=' + sendBidRequest_congaEmailFromId : '') + '&EmailToId=' + contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).id + '&EmailCC=' + ccEmails + '&TemplateId=' + sendBidRequest_congaTemplateId1 + ',' + sendBidRequest_congaTemplateId2 + '&OFN=GT+Bid');
                if(sendBidRequest_accountIds.split(',').size() == i || i >= 100){
                    try{
                        congaSendEmail(congaParameters);
                    }
                    catch(Exception e){
                        System.debug('###GTDashboardController.congaSendBidRequest() - Exception: ' + e.getMessage());
                    }
                    i = 1;
                    congaParameters.clear();
                    ccEmails = '';
                }
                else i++;
                if(sendBidRequestMap.get(accountId) != null && sendBidRequestMap.get(accountId).Status__c != 'Contracted') bidUpdateMap.put(sendBidRequestMap.get(accountId).id, new Bid__c(Id = sendBidRequestMap.get(accountId).Id, Status__c = 'Sent'));
                journals.add(new Journal__c(RecordTypeId = journal_bidjournalRT, Bid__c = sendBidRequestMap.get(accountId).Id, Journal_Entry__c = 'GT Bid Request was sent to ' + (String.isNotBlank(contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Name) ? contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Name : '') + ' ' + (String.isNotBlank(contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Email) ? contactsMap.get(sendBidRequestMap.get(accountId).Vendor_Contact__c).Email : '') + (String.isNotBlank(ccEmails) ? ', cc: ' + ccEmails : '')));
            }
            if(!bidUpdateMap.values().isEmpty()) update bidUpdateMap.values();
            
            system.debug(tripView);
            if(tripView != null && (tripView.Status_Ground__c != 'Contracted' || tripView.Status_Ground__c != 'In Contracting')){
                tripView.Status_Ground__c = 'Bid Request Stage';
                update new Ground__c(id = tripView.id, Status_Ground__c = 'Bid Request Stage', Email_Body_Bid_Request__c = null);
                List<Itinerary__c> itineraries =  [SELECT Id FROM Itinerary__c WHERE GT__c =:tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
                if(!itineraries.isEmpty()) update new Itinerary__c(Id = itineraries[0].Id, Status__c = 'Bid Request Stage');
            }
            if(!journals.isEmpty()) insert journals;
            openSendBidRequest();
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
                System.debug('###GTDashboardController.congaEmail(parameters = ' + parameters + ') => Response Status Code: ' + response.getStatusCode() + ', Response Body: ' + (String.isNotEmpty(response.getBody()) ? response.getBody().left(255) : ''));
            }
            catch(Exception e){
                System.debug('###GTDashboardController.congaEmail() - Callout Exception: ' + e.getMessage());
            }
        }
    }
    /**
    *  @/Conga
    */
}
```


# Last Modified


# Usage

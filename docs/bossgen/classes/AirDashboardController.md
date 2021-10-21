---
layout: default
title: AirDashboardController
parent: classes
---
# Metadata Type
classes


# Filename 
AirDashboardController


# Raw XML
```
global class AirDashboardController {
  public String communityNoteCoordinator {get; set;}
  public Boolean renderedData { get; set; }
  public DashboardConfigurationWrapper vfpConfiguration { get; set; }
  public Opportunity opportunity { get; set; }
  public String opportunityId { get; set; }
  public String tabDefault { get; set; }
  public String tabGroundDefault { get; set; }
  public String ground_vehicletypeRT { get; set; }
  public String ground_salesGTDetailsRT { get; set; }
  public String ground_GTTripDetailsRT { get; set; }
  public String ground_GTSubStripDetailsRT { get; set; }
  public String ground_GTTravelDetailsRT { get; set; }
  public String itinerary_GTItineraryRT { get; set; }
  public String journal_tripJournalRT { get; set; }
  public String task_traceTaskRT { get; set; }
  public String bid_AirBidRT { get; set; }
  public String journal_bidjournalRT { get; set; }
  public List<SelectOption> ground_amenitiesPL { get; set; }
  public List<SelectOption> productionCompanyPL { get; set; }
  public List<SelectOption> productionContactPL { get; set; }
  public List<SelectOption> companyContactPL { get; set; }
  public List<SelectOption> teamMembers { get; set; }
  public String coordinatorGT { get; set; }
  public String coordinatorGTName { get; set; }
  public String backendcoordinatorGT { get; set; }
  public String messageCreateContact { get; set; }
  public String url { get; set; }
  public String dateToday { get; set; }
  public String grountypeJson { get; set; }
  public String concessionJson { get; set; }
  public String form_to { get; set; }
  public String form_cc { get; set; }
  public String form_bcc { get; set; }
  public String form_subject { get; set; }
  public String form_body { get; set; }
  public String form_date { get; set; }
  public String searchOption { get; set; }
  public String searchValue { get; set; }
  public Boolean renderBid { get; set; }

  //Sales Tab
  public List<Ground__c> vehiclesByProductionList { get; set; }
  public Ground__c new_vehicle { get; set; }
  public String vehicleIdActual { get; set; }

  public String aircraftIdActual { get; set; }
  public String aircraft_type { get; set; }
  public String aircraft_economyseats { get; set; }
  public String aircraft_cargocapacity { get; set; }
  public String aircraft_seatpitch { get; set; }
  public String aircraft_airlineid { get; set; }
  public String aircraft_position { get; set; }
  public String aircraft_tripcontents { get; set; }

  public List<Concessions__c> itemsByProductionList { get; set; }
  public Concessions__c new_item { get; set; }
  public String itemIdActual { get; set; }
  public String item_requested { get; set; }
  public String item_provided { get; set; }
  public Air__c sales { get; set; }
  public static List<String> billingoptionsPL { get; set; }

  //Air Itinerary Tab
  public String departure_cities { get; set; }
  public String arrival_cities { get; set; }
  public String newTripRecordType { get; set; }
  public List<AirSegmentWrapper> segmentList { get; set; }
  public Integer segmentListSize { get; set; }
  public Integer segmentListActual { get; set; }
  public Itinerary__c itineraryFilter { get; set; }
  public Date itinerary_startdate { get; set; }
  public Date itinerary_enddate { get; set; }
  public String itinerary_city { get; set; }
  public String itinerary_vendor { get; set; }
  public String itinerary_status { get; set; }
  public Boolean itinerary_showprior { get; set; }
  public Boolean itinerary_showcontracted { get; set; }
  public Boolean itinerary_showcancelled { get; set; }
  public List<Itinerary__c> itineraryList { get; set; }
  //public List<Itinerary__c> tournamentList {get;set;}
  public Air__c newtrip { get; set; }
  public Itinerary__c newitinerary { get; set; }
  public String newtrip_depaturecity { get; set; }
  public String newtrip_depaturecityid { get; set; }
  public String newtrip_arrivalcity { get; set; }
  public String newtrip_arrivalcityid { get; set; }
  public String newtrip_grouptype { get; set; }
  public Boolean newtrip_clear { get; set; }
  public Journal__c newJournal { get; set; }
  public String createjournal_id { get; set; }
  public String createjournal_productioncompanyids { get; set; }
  public String createjournal_productioncontactids { get; set; }
  public String createjournal_companycontactids { get; set; }
  public String createjournal_coordinator { get; set; }
  public Boolean createjournal_alert { get; set; }
  public String createjournal_type { get; set; }
  public String createjournal_tracedate { get; set; }
  public Map<String, List<Ground__c>> vehiclesByTripMap { get; set; }
  public String itineraryIdActual { get; set; }
  public String orderFieldTrip { get; set; }
  public String orderOrientationTrip { get; set; }
  public Boolean orderCheckTrip { get; set; }
  public Boolean orderChangeTrip { get; set; }
  public List<SelectOption> statusItineraryPL { get; set; }
  public static List<String> groupTypePL { get; set; }
  public Map<String, List<AirSegmentWrapper>> tripsItineraryMap { get; set; }
  public Map<String, Integer> tripsItineraryCountMap { get; set; }
  public Map<String, List<Ground__c>> travelsItineraryMap { get; set; }
  public Map<String, Integer> travelsItineraryCountMap { get; set; }
  public Map<String, Revenue__c> ratesByBidMap { get; set; }
  public Map<String, Bid__c> bidContractByAirMap { get; set; }

  //Air Trip Tab
  public Map<String, List<Revenue__c>> bidRevenueMap { get; set; }
  public Ground__c groundFilter { get; set; }
  public List<Air__c> tripList { get; set; }
  public Date trip_startdate { get; set; }
  public Date trip_enddate { get; set; }
  public String trip_city { get; set; }
  public String trip_vendor { get; set; }
  public String trip_status { get; set; }
  public Boolean trip_showprior { get; set; }
  public Boolean trip_showcontracted { get; set; }
  public Boolean trip_showcancelled { get; set; }
  public String tripViewId { get; set; }
  public String tripItineraryId { get; set; }
  public Air__c tripView { get; set; }
  public Itinerary__c itineraryView { get; set; }
  public String itineraryId { get; set; }
  public String modal { get; set; }
  public List<ContentDocument> documentTripList { get; set; }
  public String filename { get; set; }
  public transient String bodytrip { get; set; }
  public String documentRelationId { get; set; }
  public String documentIdActual { get; set; }
  public String emailMessage { get; set; }
  public String emailBody { get; set; }
  public String emailAttachs { get; set; }
  public String emailTo { get; set; }
  public String emailCC { get; set; }
  public String emailBCC { get; set; }
  public String emailSubject { get; set; }
  public String documentId { get; set; }
  public String documentTitle { get; set; }
  public String vendorsJson { get; set; }
  public List<Journal__c> journalByTripList { get; set; }
  public Map<String, List<Journal__c>> journalByTripMap { get; set; }
  public String tripJournalSearch { get; set; }
  public Boolean checkIssue { get; set; }
  public Boolean checkSales { get; set; }
  public String journalIdActual { get; set; }
  public String journalChildIdActual { get; set; }
  public Journal__c journalView { get; set; }
  public Journal__c journalChildView { get; set; }
  public String newJournalChildEntry { get; set; }
  public List<SelectOption> clientsByProduction { get; set; }
  public Contact clientByProduction { get; set; }
  public List<BidWrapper> bAuxWrapper { get; set; }
  public List<BidWrapper> bidsByTripShowList { get; set; }
  public Integer totalRecsBids { get; set; }
  public Integer OffsetSizeBids { get; set; }
  public Integer LimitSizeBids { get; set; }
  public String orderFieldBid { get; set; }
  public String orderOrientationBid { get; set; }
  public Boolean orderCheckBid { get; set; }
  public Boolean orderChangeBid { get; set; }
  public Boolean prevShowBid { get; set; }
  public Boolean nextShowBid { get; set; }
  public String bid_id { get; set; }
  public String bid_notes { get; set; }
  public Integer bid_option { get; set; }
  public Boolean refreshBidData { get; set; }
  public Integer tripBidNumber { get; set; }
  public String detailId { get; set; }
  public String searchVendor_CityGoogle { get; set; }
  public String orderFieldVendor { get; set; }
  public String orderOrientationVendor { get; set; }
  public Boolean orderCheckVendor { get; set; }
  public Boolean orderChangeVendor { get; set; }
  public String searchvendor_type { get; set; }
  public String searchvendor_status { get; set; }
  public String searchvendor_word { get; set; }
  public Set<String> vendorNotSelectedIds { get; set; }
  public List<Account> searchVendorList { get; set; }
  public String searchvendor_button { get; set; }
  public String searchvendor_vendor { get; set; }
  public String searchvendor_venue { get; set; }
  public String searchvendor_airportcode { get; set; }
  public String searchvendor_country { get; set; }
  public String searchvendor_address { get; set; }
  public String searchvendor_city { get; set; }
  public String searchvendor_state { get; set; }
  public String searchvendor_zip { get; set; }
  public String searchvendor_servicetype { get; set; }
  public String searchvendor_amenities { get; set; }
  public List<SelectOption> servicetypesPL { get; set; }
  public Account vendorFilter { get; set; }
  public String selectedVendors { get; set; }
  public String selectedTrips { get; set; }
  public Boolean bidSendBidFirstTime { get; set; }
  public Map<String, Bid__c> sendBidRequestMap { get; set; }
  public Integer sendBidRequestMapSize { get; set; }
  public Map<String, Boolean> sendBidRequestMapSelected { get; set; }
  public Map<String, List<ContactWrapper>> contactsByVendor_bidRequestMap {
    get;
    set;
  }
  public Map<String, List<ContactWrapper>> contactsByVendorParent_bidRequestMap {
    get;
    set;
  }
  public Map<String, List<SelectOption>> contactSelectOption_bidRequestMap {
    get;
    set;
  }
  public Map<String, Integer> contactSelectOption_bidRequestSizeMap {
    get;
    set;
  }
  public List<String> bidByTripIds { get; set; }
  public String vendoraccount_actual_id { get; set; }
  public String vendorcontact_actual_id { get; set; }
  public Contact vendorContact { get; set; }
  public String vendorContact_id { get; set; }
  public List<SelectOption> contact_DesignationTitlePL { get; set; }
  public String emailbid_body { get; set; }
  public String type_email { get; set; }
  public String dataids { get; set; }
  public List<SelectOption> contactsByProduction { get; set; }
  public List<ContactWrapper> contactWrapperByProduction { get; set; }
  public String sendOptions_primaryContactId { get; set; }
  public String sendOptions_congaEmailTemplateId { get; set; }
  public String sendOptions_congaEmailSubject { get; set; }
  public String sendOptions_congaTemplateId { get; set; }
  private Map<String, APXTConga4__Conga_Merge_Query__c> congaQueriesMap;
  public String sendOptions_congaQueriesJson { get; set; }
  public String sendBidRequest_congaQueriesJson { get; set; }
  public String sendBidRequest_accountIds { get; set; }
  public String sendBidRequest_congaEmailTemplateId { get; set; }
  public String sendBidRequest_congaEmailSubject { get; set; }
  public String sendBidRequest_congaTemplateId1 { get; set; }
  public String sendBidRequest_congaTemplateId2 { get; set; }
  public Map<String, Bid__c> sendBidRequestMapRelease { get; set; }
  public Integer sendBidRequestMapReleaseSize { get; set; }
  public Map<String, Boolean> sendBidRequestMapReleaseSelected { get; set; }
  public Map<String, List<ContactWrapper>> contactsByVendor_releaseMap {
    get;
    set;
  }
  public Map<String, List<ContactWrapper>> contactsByVendorParent_releaseMap {
    get;
    set;
  }
  public Map<String, List<SelectOption>> contactSelectOption_releaseMap {
    get;
    set;
  }
  public Map<String, Integer> contactSelectOption_releaseSizeMap { get; set; }
  public Boolean bidReleaseActive { get; set; }
  public Concessions__c newConcessionTrip { get; set; }
  public List<Concessions__c> concessionsRequestedTrip { get; set; }
  public String concessionActual { get; set; }
  public String concessionRequestedActual { get; set; }
  public String concessionNoteActual { get; set; }
  public Boolean concessionCreateInBid { get; set; }
  public List<SelectOption> concessions_concessionTypePL { get; set; }
  public Air__c newAircraftTrip { get; set; }
  public List<Air__c> aircraftsByTripList { get; set; }
  public List<Ground__c> subTripList { get; set; }
  public String subtripIdActual { get; set; }
  public Map<String, List<Ground__c>> travelsBySubTripMap { get; set; }
  public Map<String, Boolean> hasFreightMap { get; set; }
  public Ground__c newTravel { get; set; }
  public String travelActualId { get; set; }
  public String travelActualOrder { get; set; }
  public String newtravel_subtripid { get; set; }
  public String newtravel_line { get; set; }
  public String newtravel_vehicle { get; set; }
  public Datetime newtravel_startdate { get; set; }
  public Datetime newtravel_enddate { get; set; }
  public String newtravel_traveltype { get; set; }
  public String newtravel_grouptype { get; set; }
  public String newtravel_locationtype { get; set; }
  public String newtravel_locationpickup { get; set; }
  public String newtravel_locationdropoff { get; set; }
  public String newtravel_locationdetails { get; set; }
  public String newtravel_notes { get; set; }
  public Boolean newtravel_updatemaster { get; set; }
  public String searchlocation_type { get; set; }
  public String searchlocation_value1 { get; set; }
  public String searchlocation_value2 { get; set; }
  public String searchlocation_value3 { get; set; }
  public List<wrapperLocation> searchLocationList { get; set; }
  public List<wrapperLocation> searchLocationRelatedList { get; set; }
  public Boolean searchlocation_open { get; set; }
  public String tripview_typeinformation { get; set; }
  public Date tripview_dateinformation { get; set; }
  public Map<Integer, BidWrapper> bidDataMap { get; set; }
  public GTDashboard gtDashboard { get; set; }
  public Integer bidsCreated { get; set; }
  public String contactPrimarySelected { get; set; }
  public String contractingBidId { get; set; }
  public String contractingParentId { get; set; }
  public String prod_assoc_CoordinatorsRT { get; set; }
  public String prod_assoc_ContactsRT { get; set; }
  public String tripview_status { get; set; }
  public String dataBidIdsearch { get; set; }
  public String emailbid_to { get; set; }
  public String emailbid_cc { get; set; }
  public String emailbid_bcc { get; set; }
  public String emailbid_subject { get; set; }
  public String emailbid_id { get; set; }
  public String emailbid_type { get; set; }
  public String emailbid_primarycontactname { get; set; }
  public String decisionduedate_body { get; set; }
  public String decisionduedate_attention { get; set; }
  public String decisionduedate_salutation { get; set; }
  public String decisionduedate_closing { get; set; }
  public Contact decisionDueDateContact { get; set; }
  public Draft__c draft { get; set; }
  public Bid__c bidDataDecision { get; set; }
  public List<ContentDocument> attachDocumentList { get; set; }
  public String attachdocument_objectid { get; set; }
  transient public String body { get; set; }
  public String newattachment_id { get; set; }
  public String newattachment_name { get; set; }

  public String itinerary_chartertype { get; set; }
  public String itinerary_description { get; set; }
  public String itinerary_pax { get; set; }
  public Air__c newItineraryTrip { get; set; }
  public String newitinerary_id { get; set; }
  public String newitinerary_order { get; set; }
  public Date newitinerary_depdate { get; set; }
  public Date newitinerary_arrdate { get; set; }
  public String newitinerary_flight { get; set; }
  public String newitinerary_depcityid { get; set; }
  public String newitinerary_arrcityid { get; set; }
  public String newitinerary_deptime { get; set; }
  public String newitinerary_arrtime { get; set; }
  public Decimal newitinerary_durationhrs { get; set; }
  public Decimal newitinerary_durationmins { get; set; }
  public String newitinerary_equiptype { get; set; }
  public String newitinerary_notes { get; set; }
  public List<Air__c> itineraryTripList { get; set; }
  public Integer tripview_option { get; set; }
  public Boolean isProdJournalsRendered { get; set; }
  public String communityURLvalue { get; set; } //CS - victor
  public Map<String, String> symbolMap { get; set; }
  public Boolean isBidRequestRendered { get; set; }
  public Boolean isBidReleaseRendered { get; set; }

  //Pagination Itinerary
  public Integer limitItinerary { get; set; }
  public Integer offsetItinerary { get; set; }
  public String searchTypeItinerary { get; set; }
  public Integer totalPagesItinerary { get; set; }
  public Boolean orderCheckItinerary { get; set; }
  public Boolean orderChangeItinerary { get; set; }
  public String orderOrientationItinerary { get; set; }
  public String orderFieldItinerary { get; set; }
  public Id firstIdItinerary { get; set; }
  public Id lastIdItinerary { get; set; }
  public Object firstValueOfSortedFieldItinerary { get; set; }
  public Object lastValueOfSortedFieldItinerary { get; set; }

  //Pagination Trip
  public Integer limitTrip { get; set; }
  public Integer offsetTrip { get; set; }
  public String searchTypeTrip { get; set; }
  public Integer totalPagesTrip { get; set; }
  public Id firstId { get; set; }
  public Id lastId { get; set; }
  public Object firstValueOfSortedField { get; set; }
  public Object lastValueOfSortedField { get; set; }

  //Pagination Vendor
  public Integer limitVendor { get; set; }
  public Integer offsetVendor { get; set; }
  public String searchTypeVendor { get; set; }
  public Integer totalPagesVendor { get; set; }
  public Id firstIdVendor { get; set; }
  public Id lastIdVendor { get; set; }
  public Object firstValueOfSortedFieldVendor { get; set; }
  public Object lastValueOfSortedFieldVendor { get; set; }

  public AirDashboardController(
    ApexPages.StandardController standardController
  ) {
    vfpConfiguration = new DashboardConfigurationWrapper();
    Opportunity opp = (Opportunity) standardController.getRecord();
    Init();
    if (opp != null && opp.Id != null) {
      opportunity = [
        SELECT
          Id,
          Name,
          Alias_With_Production_Name__c, 
          AccountId,
          Account.Name,
          Parent_Production__c,
          RecordTypeId,
          RecordType.Name
        FROM Opportunity
        WHERE Id = :opp.Id
      ];
      opportunityId = opportunity.Id;
      //getDataProduction();
    }
  }

  public AirDashboardController() {
    Init();
  }

  public void Init() {
    limitTrip = 20;
    limitItinerary = 20;
    limitVendor = 20;
    isBidRequestRendered = false;
    isBidReleaseRendered = false;
    isProdJournalsRendered = false;
    renderBid = false;
    renderedData = false;
    tabDefault = 'sales';
    tabGroundDefault = 'trip_bids';
    Schema.DescribeFieldResult fieldResult;
    List<Schema.PicklistEntry> ple;
    dateToday = String.valueOf(Datetime.now().format('MM/dd/yyyy'));

    List<wrapperSearchPL> groupList = new List<wrapperSearchPL>();
    for (SelectOption so : PickThePicklist('Air__c', 'Group_Type__c')) {
      groupList.add(new wrapperSearchPL(so.getValue(), so.getValue()));
    }
    grountypeJson = JSON.serialize(groupList);

    task_traceTaskRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Task' AND Name = 'Trace Task'
    ]
    .Id;
    ground_vehicletypeRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Ground__c' AND Name = 'Vehicle Type'
    ]
    .Id;
    ground_salesGTDetailsRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Ground__c' AND Name = 'Sales GT Details'
    ]
    .Id;
    ground_GTTripDetailsRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Ground__c' AND Name = 'GT Trip Details'
    ]
    .Id;
    itinerary_GTItineraryRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Itinerary__c' AND Name = 'GT Itinerary'
    ]
    .Id;
    journal_tripJournalRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Journal__c' AND Name = 'Trip Journal'
    ]
    .Id;
    bid_AirBidRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Bid__c' AND DeveloperName = 'Air_Bid'
    ]
    .Id;
    journal_bidjournalRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Journal__c' AND Name = 'Bid Journal'
    ]
    .Id;
    ground_GTSubStripDetailsRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Ground__c' AND Name = 'GT Sub Trip Details'
    ]
    .Id;
    ground_GTTravelDetailsRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Ground__c' AND Name = 'GT Travel Details'
    ]
    .Id;
    prod_assoc_CoordinatorsRT = [
      SELECT Id
      FROM RecordType
      WHERE
        sObjectType = 'Production_Associations__c'
        AND DeveloperName = 'Production_Coordinators'
    ]
    .Id;
    prod_assoc_ContactsRT = [
      SELECT Id
      FROM RecordType
      WHERE
        sObjectType = 'Production_Associations__c'
        AND DeveloperName = 'Production_Contacts'
    ]
    .Id;

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
    for (Schema.PicklistEntry pickListVal : ple) {
      ground_amenitiesPL.add(
        new SelectOption(pickListVal.getValue(), pickListVal.getLabel())
      );
    }

    vehiclesByProductionList = new List<Ground__c>();
    new_vehicle = new Ground__c();
    itemsByProductionList = new List<Concessions__c>();
    new_item = new Concessions__c(Concession_Type__c = 'GT');
    sales = new Air__c();

    billingoptionsPL = new List<String>();
    for (SelectOption so : PickThePicklist('Ground__c', 'Billing_Options__c')) {
      billingoptionsPL.add(so.getValue());
    }

    //Itinerary
    orderFieldItinerary = 'Air__r.Departure_Date__c';
    orderOrientationItinerary = 'ASC';
    orderCheckItinerary = false;
    orderChangeItinerary = false;
    itineraryFilter = new Itinerary__c();
    itinerary_showcontracted = false;
    itinerary_showcancelled = false;
    itinerary_showprior = false;
    newtrip_clear = false;
    newJournal = new Journal__c();
    vehiclesByTripMap = new Map<String, List<Ground__c>>();
    statusItineraryPL = new List<SelectOption>();
    statusItineraryPL.add(new SelectOption('', '-- Select --'));
    statusItineraryPL.add(
      new SelectOption('Itinerary Received', 'Itinerary Received')
    );
    statusItineraryPL.add(
      new SelectOption('Bid Request Stage', 'Bid Request Stage')
    );
    statusItineraryPL.add(
      new SelectOption('Pending Client Choice', 'Pending Client Choice')
    );
    statusItineraryPL.add(new SelectOption('Contracted', 'Contracted'));
    statusItineraryPL.add(new SelectOption('Budgeting', 'Budgeting'));
    statusItineraryPL.add(new SelectOption('Cancelled', 'Cancelled'));
    statusItineraryPL.add(new SelectOption('Layoff', 'Layoff'));
    statusItineraryPL.add(
      new SelectOption('Contracted on Own', 'Contracted on Own')
    );
    statusItineraryPL.add(new SelectOption('In Contracting', 'In Contracting'));

    tripsItineraryMap = new Map<String, List<AirSegmentWrapper>>();
    travelsItineraryMap = new Map<String, List<Ground__c>>();
    tripsItineraryCountMap = new Map<String, Integer>();
    travelsItineraryCountMap = new Map<String, Integer>();
    bidContractByAirMap = new Map<String, Bid__c>();

    //Trip
    bidRevenueMap = new Map<String, List<Revenue__c>>();
    groundFilter = new Ground__c();
    tripList = new List<Air__c>();
    trip_showcontracted = false;
    trip_showcancelled = false;
    trip_showprior = false;
    //TripWrapper.orderFieldTrip = 'departure_date';
    //TripWrapper.orderOrientationTrip = 'ASC';
    orderFieldTrip = 'Departure_Date__c';
    orderOrientationTrip = 'ASC';
    orderCheckTrip = false;
    orderChangeTrip = false;
    documentTripList = new List<ContentDocument>();
    documentIdActual = null;
    vendorsJson = '[]';
    journalByTripList = new List<Journal__c>();
    journalByTripMap = new Map<String, List<Journal__c>>();
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
    //VendorWrapper.orderFieldVendor = 'created_date';
    //VendorWrapper.orderOrientationVendor = 'ASC';
    orderFieldVendor = 'Name';
    orderOrientationVendor = 'ASC';
    orderCheckVendor = false;
    orderChangeVendor = false;
    servicetypesPL = new List<SelectOption>();
    servicetypesPL.addAll(PickThePicklist('Account', 'Service_Types__c'));
    vendorFilter = new Account();
    bidSendBidFirstTime = true;
    contact_DesignationTitlePL = new List<SelectOption>();
    contact_DesignationTitlePL.add(new SelectOption('', ''));
    contact_DesignationTitlePL.addAll(
      PickThePicklist('Contact', 'Designation_title__c')
    );
    vendorContact = new Contact();
    emailBid_body = null;
    newConcessionTrip = new Concessions__c();
    concessionsRequestedTrip = new List<Concessions__c>();
    List<wrapperSearchPL> consValueList = new List<wrapperSearchPL>();
    Map<Object, List<String>> dependValuesByControlValue = getDependentPicklistValues(
      Concessions__c.Concessions_Requested__c
    );
    concessions_concessionTypePL = new List<SelectOption>();
    for (Object k1 : dependValuesByControlValue.keySet()) {
      if ((String) k1 == 'Air') {
        for (String k2 : dependValuesByControlValue.get(k1)) {
          concessions_concessionTypePL.add(new SelectOption(k2, k2));
          consValueList.add(new wrapperSearchPL(k2, k2));
        }
      }
    }
    concessionJson = JSON.serialize(consValueList);

    newAircraftTrip = new Air__c();
    aircraftsByTripList = new List<Air__c>();
    subTripList = new List<Ground__c>();
    travelsBySubTripMap = new Map<String, List<Ground__c>>();
    hasFreightMap = new Map<String, Boolean>();
    newTravel = new Ground__c();
    searchLocationList = new List<wrapperLocation>();
    searchLocationRelatedList = new List<wrapperLocation>();
    searchlocation_open = false;
    bidsCreated = 0;

    newItineraryTrip = new Air__c();

    //Contracting
    gtDashboard = new GTDashboard();

    //CS - victor
    Community_Settings__c comSetCS = Community_Settings__c.getInstance();
    communityURLvalue = comSetCS.Community_URL__c;
  }

  public static void refreshItineraryDataBids(String tripViewId) {
    List<Bid__c> bidExist = [
      SELECT Id, Air__c, Production__c
      FROM Bid__c
      WHERE Air__c = :tripViewId AND Status__c NOT IN ('Contracted')
    ];
    if (bidExist.size() > 0) {
      List<Air__c> itineraryBidList = [
        SELECT Id, Bid_Itinerary__c, Production__c
        FROM Air__c
        WHERE
          Bid_Itinerary__c IN :bidExist
          AND RecordType.DeveloperName = 'Air_Itinerary_Details'
      ];
      delete [
        SELECT Id
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Segments'
          AND Air_Itinerary_Details__c IN :itineraryBidList
      ];

      List<Air__c> itineraryByTripList = [
        SELECT
          Id,
          Trip_Type__c,
          RecordTypeId,
          Group_Type__c,
          Departure_Date__c,
          Departure_City__c,
          Arrival_Date__c,
          Arrival_City__c,
          Return_Date__c,
          PAX__c,
          Air_Preferences__c,
          Trace_Date__c,
          Decision_Due_Date__c,
          Return_Arrival_City__c,
          Return_Departure_City__c,
          Air_Charter__c,
          Air_Type__c,
          Air_Trip_Details__c,
          Departure_City__r.Airport_Code__c,
          Arrival_City__r.Airport_Code__c,
          Order__c,
          Flight_No__c,
          Dep_Time__c,
          Arr_Time__c,
          Flight_Duration_hrs__c,
          Flight_Duration_Mins__c,
          Class__c,
          Equip_Type__c,
          Operated_by__c,
          Departure_City__r.Full_Name__c,
          Arrival_City__r.Full_Name__c,
          Segment_Notes__c
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Segments'
          AND Production__c = :bidExist[0].Production__c
          AND Air_Trip_Details__c = :tripViewId
          AND Bid_Aircraft__c = NULL
        ORDER BY Departure_Date__c
      ];
      Air__c aAux;
      List<Air__c> aListAux = new List<Air__c>();
      for (Air__c b : itineraryBidList) {
        for (Air__c a : itineraryByTripList) {
          aAux = a.clone();
          aAux.Air_Itinerary_Details__c = b.Id;
          aAux.Air_Trip_Details__c = null;
          aAux.Production__c = b.Production__c;
          aAux.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Segments')
            .getRecordTypeId();
          aListAux.add(aAux);
        }
      }

      if (aListAux.size() > 0)
        insert aListAux;
    }
  }

  public void deleteItineraryTrip() {
    if (newitinerary_id != null && newitinerary_id != '') {
      delete [SELECT Id FROM Air__c WHERE Id = :newitinerary_id];
      refreshItineraryDataBids(tripViewId);
      getItineraryByTrip();
    }
  }

  public void saveItinerarySegmentTrip() {
    Air__c itinerary = new Air__c(
      Id = newitinerary_id != null &&
        newitinerary_id != ''
        ? newitinerary_id
        : null,
      RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Segments')
        .getRecordTypeId(),
      Order__c = newitinerary_order != null &&
        newitinerary_order != ''
        ? Decimal.valueOf(newitinerary_order)
        : null,
      Departure_Date__c = newitinerary_depdate,
      Arrival_Date__c = newitinerary_arrdate,
      Flight_No__c = newitinerary_flight,
      Departure_City__c = newitinerary_depcityid != null &&
        newitinerary_depcityid != ''
        ? newitinerary_depcityid
        : null,
      Arrival_City__c = newitinerary_arrcityid != null &&
        newitinerary_arrcityid != ''
        ? newitinerary_arrcityid
        : null,
      Dep_Time__c = newitinerary_deptime != null &&
        newitinerary_deptime != ''
        ? Time.newInstance(
            Integer.valueOf(newitinerary_deptime.split(':')[0]),
            newitinerary_deptime.split(':').size() > 0
              ? Integer.valueOf(newitinerary_deptime.split(':')[1])
              : 0,
            0,
            0
          )
        : null,
      Arr_Time__c = newitinerary_arrtime != null &&
        newitinerary_arrtime != ''
        ? Time.newInstance(
            Integer.valueOf(newitinerary_arrtime.split(':')[0]),
            newitinerary_arrtime.split(':').size() > 0
              ? Integer.valueOf(newitinerary_arrtime.split(':')[1])
              : 0,
            0,
            0
          )
        : null,
      Flight_Duration_hrs__c = newitinerary_durationhrs != null
        ? newitinerary_durationhrs
        : null,
      Flight_Duration_Mins__c = newitinerary_durationmins != null
        ? newitinerary_durationmins
        : null,
      Equip_Type__c = newitinerary_equiptype,
      Segment_Notes__c = newitinerary_notes
    );
    if (newitinerary_id == null || newitinerary_id == '') {
      itinerary.Production__c = opportunityId;
      itinerary.Air_Trip_Details__c = tripView.Id;
    }
    upsert itinerary;
    refreshItineraryDataBids(tripViewId);
    getItineraryByTrip();
  }

  public void getItineraryByTrip() {
    itineraryTripList = new List<Air__c>();
    if (tripView != null && tripView.Air_Charter__c == true) {
      itineraryTripList = [
        SELECT
          Id,
          Trip_Type__c,
          RecordTypeId,
          Group_Type__c,
          Departure_Date__c,
          Departure_City__c,
          Arrival_Date__c,
          Arrival_City__c,
          Return_Date__c,
          PAX__c,
          Air_Preferences__c,
          Trace_Date__c,
          Decision_Due_Date__c,
          Return_Arrival_City__c,
          Return_Departure_City__c,
          Air_Charter__c,
          Air_Type__c,
          Air_Trip_Details__c,
          Departure_City__r.Airport_Code__c,
          Arrival_City__r.Airport_Code__c,
          Order__c,
          Flight_No__c,
          Dep_Time__c,
          Arr_Time__c,
          Flight_Duration_hrs__c,
          Flight_Duration_Mins__c,
          Class__c,
          Equip_Type__c,
          Operated_by__c,
          Departure_City__r.Full_Name__c,
          Arrival_City__r.Full_Name__c,
          Segment_Notes__c
        FROM Air__c
        WHERE
          Air_Trip_Details__c = :tripView.Id
          AND RecordType.DeveloperName = 'Air_Segments'
        ORDER BY Departure_Date__c
      ];
      for (Air__c iti : itineraryTripList) {
        iti.Dep_Time_Text__c = iti.Departure_Date__c != null &&
          iti.Dep_Time__c != null
          ? Datetime.newInstance(iti.Departure_Date__c, iti.Dep_Time__c)
              .format('h:mm a')
          : (iti.Dep_Time__c != null
              ? Datetime.newInstance(system.today(), iti.Dep_Time__c)
                  .format('h:mm a')
              : '');
        iti.Arr_Time_Text__c = iti.Arrival_Date__c != null &&
          iti.Arr_Time__c != null
          ? Datetime.newInstance(iti.Arrival_Date__c, iti.Arr_Time__c)
              .format('h:mm a')
          : (iti.Departure_Date__c != null &&
              iti.Arr_Time__c != null
              ? Datetime.newInstance(iti.Departure_Date__c, iti.Arr_Time__c)
                  .format('h:mm a')
              : '');
      }
    }
  }
  public void saveItineraryTrip() {
    if (tripView != null && tripView.Id != null) {
      tripView.Charter_Type__c = itinerary_chartertype;
      tripView.Description__c = itinerary_description;
      tripView.PAX__c = itinerary_pax != null &&
        itinerary_pax != ''
        ? Decimal.valueOf(itinerary_pax.replace(',', ''))
        : null;
      update tripView;
    }
  }

  public void doAttachmentTrip() {
    if (filename != null && body != null) {
      try {
        ContentVersion conVer = new ContentVersion();
        conVer.PathOnClient = '/' + filename;
        conVer.Title = filename.split('\.')[0];
        conVer.VersionData = (!Test.isRunningTest()
          ? EncodingUtil.base64Decode(
              body.subString(0, 100).split(',')[1] +
              body.substring(100, body.length())
            )
          : Blob.valueOf('Test'));
        insert conVer;

        ContentVersion contentver = [
          SELECT ContentDocumentId, ContentDocument.FileExtension
          FROM ContentVersion
          WHERE Id = :conVer.Id
        ];

        //Create ContentDocumentLink
        ContentDocumentLink cDe = new ContentDocumentLink();
        cDe.ContentDocumentId = contentver.ContentDocumentId;
        cDe.LinkedEntityId = documentRelationId;
        cDe.ShareType = 'V';
        cDe.Visibility = 'AllUsers';
        insert cDe;

        newattachment_id = contentver.ContentDocumentId;
        newattachment_name = filename;
      } catch (Exception e) {
        system.debug(e.getMessage());
      }
    }
    filename = null;
    body = null;
  }

  public void openAttachDocs() {
    attachDocumentList = new List<ContentDocument>();
    if (attachdocument_objectid != null && attachdocument_objectid != '') {
      Set<String> contentDocumentIds = new Set<String>();
      for (ContentDocumentLink cdl : [
        SELECT Id, LinkedEntityId, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :attachdocument_objectid
      ])
        contentDocumentIds.add(cdl.ContentDocumentId);
      attachDocumentList = [
        SELECT Id, Title, FileExtension, CreatedDate
        FROM ContentDocument
        WHERE Id IN :contentDocumentIds
      ];
    }
  }

  public void sendEmailDecisionDueDate() {
    emailMessage = '';
    try {
      emailMessage = sendEmail(
        emailbid_to,
        emailbid_cc,
        emailbid_bcc,
        emailbid_subject,
        (decisionduedate_salutation != ''
          ? decisionduedate_salutation + '<br/>'
          : '') +
        decisionduedate_body +
        '<br/>' +
        decisionduedate_closing.replace('
', '<br/>'),
        emailAttachs,
        opportunityId,
        tripViewId
      );
      if (emailMessage == '') {
        tripView.Decision_Due_Date_Last_Send_By__c =
          UserInfo.getFirstName() +
          ' ' +
          UserInfo.getLastName();
        tripView.Decision_Due_Date_Last_Send_Date__c = system.now();
        update tripView;
      }
    } catch (DMLException e) {
      system.debug(e.getMessage());
      emailMessage = e.getMessage();
    }
  }

  public void deactivateDecisionDueDate() {
    delete draft;
    tripView.Form_Decision_Due_Date__c = null;
    update tripView;
  }

  public void saveDecisionDueDate() {
    draft.Body__c = decisionduedate_body;
    upsert draft;
  }

  public void changeAttention() {
    decisionDueDateContact = new Contact();
    if (decisionduedate_attention != null && decisionduedate_attention != '') {
      decisionDueDateContact = [
        SELECT Id, Name, FirstName, LastName, Email
        FROM Contact
        WHERE Id = :decisionduedate_attention
      ];
      draft.Salutation__c = 'Hi ' + decisionDueDateContact.FirstName + ',';
    }
  }

  public void openDecisionDueDate() {
    draft = new Draft__c();
    decisionDueDateContact = new Contact();
    if (String.isNotBlank(tripView.Form_Decision_Due_Date__c)) {
      draft = [
        SELECT
          Id,
          Name,
          Attention__c,
          Salutation__c,
          Production_Assoc_Type__c,
          Primary_Contact_Id__c,
          Production_Assoc_Contact_Id__c,
          CC__c,
          Subject__C,
          Date__c,
          BCC__c,
          Body__c,
          Terms__c,
          CreatedBy.Name,
          CreatedDate,
          LastModifiedBy.Name,
          LastModifiedDate,
          Closing__c
        FROM Draft__c
        WHERE Name = :tripView.Form_Decision_Due_Date__c
      ];
      if (draft.Attention__c != null) {
        decisionDueDateContact = [
          SELECT Id, Name, FirstName, LastName, Email
          FROM Contact
          WHERE Id = :draft.Attention__c
        ];
      }
    } else {
      for (Production_Associations__c pa : [
        SELECT
          Id,
          Production_Opp__c,
          Contact__c,
          Contact__r.Name,
          Contact__r.Firstname,
          Contact__r.LastName,
          Contact__r.Title,
          Contact__r.Order__c,
          Contact__r.Email,
          Contact__r.Phone,
          Contact__r.MobilePhone,
          User__c,
          Team_Roles__c,
          User__r.Name,
          Role__c
        FROM Production_Associations__c
        WHERE
          Production_Opp__c = :opportunityId
          AND Contact__c != NULL
          AND Role__c != NULL
        ORDER BY Contact__r.Name ASC
      ]) {
        if (pa.Role__c.contains('Primary Air')) {
          decisionDueDateContact = new Contact(
            Id = pa.Contact__c,
            FirstName = pa.Contact__r.FirstName,
            LastName = pa.Contact__r.LastName,
            Email = pa.Contact__r.Email
          );
          draft.Attention__c = pa.Contact__c;
          draft.Salutation__c = 'Hi ' + pa.Contact__r.FirstName + ',';
        }
      }

      List<Production_Associations__c> prodAssocAux = [
        SELECT Id, User__r.Name, User__r.Email
        FROM Production_Associations__c
        WHERE
          Production_Opp__c = :opportunityid
          AND User__c != NULL
          AND Team_Roles__c INCLUDES ('Primary Air Coordinator')
      ];

      String firstDate =
        (tripView.Departure_Date__c != null
          ? Datetime.newInstance(
                tripView.Departure_Date__c.year(),
                tripView.Departure_Date__c.month(),
                tripView.Departure_Date__c.day()
              )
              .format('dd') + ' '
          : '') +
        (tripView.Departure_Date__c != null
          ? Datetime.newInstance(
                  tripView.Departure_Date__c.year(),
                  tripView.Departure_Date__c.month(),
                  tripView.Departure_Date__c.day()
                )
                .format('dd MMMMM yy')
                .split(' ')[1]
              .subString(0, 3)
          : '') +
        (tripView.Departure_Date__c != null
          ? ' ' +
            Datetime.newInstance(
                tripView.Departure_Date__c.year(),
                tripView.Departure_Date__c.month(),
                tripView.Departure_Date__c.day()
              )
              .format('yy')
          : '');
      String lastDate =
        (tripView.Return_Date__c != null
          ? Datetime.newInstance(
                tripView.Return_Date__c.year(),
                tripView.Return_Date__c.month(),
                tripView.Return_Date__c.day()
              )
              .format('dd') + ' '
          : '') +
        (tripView.Return_Date__c != null
          ? Datetime.newInstance(
                  tripView.Return_Date__c.year(),
                  tripView.Return_Date__c.month(),
                  tripView.Return_Date__c.day()
                )
                .format('dd MMMMM yy')
                .split(' ')[1]
              .subString(0, 3)
          : '') +
        (tripView.Return_Date__c != null
          ? ' ' +
            Datetime.newInstance(
                tripView.Return_Date__c.year(),
                tripView.Return_Date__c.month(),
                tripView.Return_Date__c.day()
              )
              .format('yy')
          : '');
      String decisionDue =
        (tripView.Decision_Due_Date__c != null
          ? Datetime.newInstance(
                tripView.Decision_Due_Date__c.year(),
                tripView.Decision_Due_Date__c.month(),
                tripView.Decision_Due_Date__c.day()
              )
              .format('dd') + ' '
          : '') +
        (tripView.Decision_Due_Date__c != null
          ? Datetime.newInstance(
                  tripView.Decision_Due_Date__c.year(),
                  tripView.Decision_Due_Date__c.month(),
                  tripView.Decision_Due_Date__c.day()
                )
                .format('dd MMMMM yy')
                .split(' ')[1]
              .subString(0, 3)
          : '') +
        (tripView.Decision_Due_Date__c != null
          ? ' ' +
            Datetime.newInstance(
                tripView.Decision_Due_Date__c.year(),
                tripView.Decision_Due_Date__c.month(),
                tripView.Decision_Due_Date__c.day()
              )
              .format('yy')
          : '');

      String segments =
        (firstDate != '' ? firstDate + ' ' : '') +
        tripView.Departure_City__r.Airport_Code__c +
        '-' +
        tripView.Arrival_City__r.Airport_Code__c +
        (lastDate != '' ? ' ' + lastDate : '') +
        (tripView.Return_Departure_City__c != null ||
          tripView.Return_Arrival_City__c != null
          ? ' ' +
            tripView.Return_Departure_City__r.Airport_Code__c +
            '-' +
            tripView.Return_Arrival_City__r.Airport_Code__c
          : '');

      draft.Subject__c =
        opportunity.Name +
        ' ' +
        segments +
        ', ' +
        tripView.Group_Type__c +
        ', Decision Due' +
        (decisionDue != '' ? ' ' + decisionDue : '');
      draft.Body__c =
        'This is to remind you that a decision is Due on ' +
        (decisionDue != '' ? decisionDue + ' ' : '') +
        'for the ' +
        segments +
        ' trip.' +
        '<br/>Space will be released if we do not receive a decision by this date.';
      draft.Closing__c =
        'Thank You' +
        '
' +
        (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') +
        '
Air Travel Coordinator';
      if (String.isNotBlank(draft.Subject__c)) {
        insert draft;
        draft = [
          SELECT
            Id,
            Name,
            Attention__c,
            Salutation__c,
            Production_Assoc_Type__c,
            Primary_Contact_Id__c,
            Production_Assoc_Contact_Id__c,
            CC__c,
            Subject__C,
            Date__c,
            BCC__c,
            Body__c,
            Terms__c,
            CreatedBy.Name,
            CreatedDate,
            LastModifiedBy.Name,
            LastModifiedDate,
            Closing__c
          FROM Draft__c
          WHERE Id = :draft.Id
        ];
        update new Air__c(
          Id = tripView.Id,
          Form_Decision_Due_Date__c = draft.Name
        );
        tripView.Form_Decision_Due_Date__c = draft.Name;
      }
    }
  }

  /*public void sendBidRequestLink(){
        if(dataids != null && dataids.trim() != ''){
            Set<String> vendorContactIds = new Set<String>();
            for(String d : dataids.split(',')){
                vendorContactIds.add(sendBidRequestMap.get(d).Vendor_Contact__c);
            }
            
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id IN: vendorContactIds]) contactMap.put(c.Id,c);
            
            List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            String owaeId = prodAssocAux.size() > 0 ? verifyWideAddress(prodAssocAux[0].User__r.Email) : null;
            
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
                if(owaeId != null) mail.setOrgWideEmailAddressId(owaeId);
                toAddresses = new String[] {contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email};
                    mail.setToAddresses(toAddresses);
                if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));                
                subject = (templateLink.size() > 0 ? templateLink[0].Subject.replace('{ProductionName}',sendBidRequestMap.get(d).Production__r.Name)
                           .replace('{StartDate}',(sendBidRequestMap.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.Start_Date__c.year(),sendBidRequestMap.get(d).GT__r.Start_Date__c.month(),sendBidRequestMap.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                           .replace('{EndDate}',(sendBidRequestMap.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.End_Date__c.year(),sendBidRequestMap.get(d).GT__r.End_Date__c.month(),sendBidRequestMap.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                           .replace('{BidNumber}',sendBidRequestMap.get(d).Name)
                           : '');
                body = (templateLink.size() > 0 ? templateLink[0].HtmlValue.replace('{GroundTravelCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
                        .replace('{ContactName}',contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Name) 
                        .replace('{VendorURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Vendor__c + '" target="_blank">' + sendBidRequestMap.get(d).Vendor__r.Name + '</a>')
                        .replace('{BidURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Id + '" target="_blank">http://' + url + '/' + sendBidRequestMap.get(d).Id + '</a>')
                        : '');
                gAux.Email_Body_Bid_Request_Link__c = null;
                mail.setSubject(subject);
                mail.setHtmlBody(body);
                myEmails.add(mail);
            }    
            
            insert journalAuxList;
            
            update bidUpdateMap.values();
            
            if(tripViewId != null && tripView.Status__c != 'Contracted'){
                gAux.Status_Ground__c = 'Bid Request Stage';
                tripView.Status__c = 'Bid Request Stage';
                List<Itinerary__c> itineraryAuxList =  [SELECT Id FROM Itinerary__c WHERE GT__c =: tripViewId AND RecordType.DeveloperName = 'GT_Itinerary'];
                if(itineraryAuxList.size() > 0) update new Itinerary__c(Id=itineraryAuxList[0].Id,Status__c='Bid Request Stage');
            }
            gAux.Bid_Request__c = system.today();
            update gAux;
            
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
        }
    }*/

  public void saveStatusTrip() {
    if (tripViewId != null && tripViewId != '') {
      Air__c aAux = new Air__c(Id = tripViewId, Status__c = tripview_status);
      update aAux;
      tripView.Status__c = tripview_status;
      searchTrip();
    }
  }

  public void saveBackEndCoordinator() {
    if (tripView != null && tripView.Id != null) {
      tripView.Back_end_Coordinator__c = backendcoordinatorGT != null &&
        backendcoordinatorGT != ''
        ? backendcoordinatorGT
        : null;
      update tripView;
    }
  }

  public void viewContractingDetailByItinerary() {
    if (vfpConfiguration != null) {
      vfpConfiguration.bidId = contractingBidId;
      vfpConfiguration.parentId = contractingParentId;
      vfpConfiguration.productionId = opportunityId;
      vfpConfiguration.parentSObject = 'Air';
    }
  }

  public void changeClientTrip() {
    if (contactPrimarySelected != null && contactPrimarySelected != '') {
      clientByProduction = [
        SELECT Id, FirstName, Name, Phone, Email, Title, MobilePhone
        FROM Contact
        WHERE Id = :contactPrimarySelected
        LIMIT 1
      ];
      List<Production_Associations__c> paList = [
        SELECT Id, Contact__c, Role__c, Production_Opp__c
        FROM Production_Associations__c
        WHERE
          Production_Opp__c = :opportunityId
          AND Contact__c != NULL
          AND RecordType.DeveloperName = 'Production_Contacts'
      ];
      system.debug(paList);
      if (paList.size() > 0) {
        String roles;
        for (Production_Associations__c pAssoc : paList) {
          if (
            contactPrimarySelected != null &&
            contactPrimarySelected != '' &&
            pAssoc.Contact__c == contactPrimarySelected &&
            pAssoc.Role__c != null
          ) {
            if (
              pAssoc.Role__c != null && !pAssoc.Role__c.contains('Primary Air')
            ) {
              pAssoc.Role__c = pAssoc.Role__c + ';Primary Air;';
            } else {
              if (pAssoc.Role__c == null)
                pAssoc.Role__c = 'Primary Air;';
            }
          } else {
            roles = '';
            if (pAssoc.Role__c != null) {
              for (String tr : pAssoc.Role__c.split(';')) {
                if (tr != 'Primary Air')
                  roles = roles + tr + ';';
              }
            }
            pAssoc.Role__c = roles;
          }
        }
        update paList;
      } else {
        insert new Production_Associations__c(
          RecordTypeId = prod_assoc_ContactsRT,
          Production_Opp__c = opportunityId,
          Role__c = 'Primary Air;',
          Contact__c = contactPrimarySelected
        );
      }
    }
  }

  public void saveOtherInformation() {
    /*//Trace
        if(tripView.Id != null && tripview_typeinformation == 'tripview_tracedate' && tripview_dateinformation != null && coordinatorGT != null && tripView.Status__c != null){
            system.debug('# valid for trace...');
            Date actualTraceDate = [SELECT Trace_Date__c FROM Air__c WHERE Id =:tripView.Id].Trace_Date__c;
            if(actualTraceDate != tripview_dateinformation){
                system.debug('# creating trace...');
                Id recordTypeTT = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName().get('Trace_Task').getRecordTypeId();
                insert new Task(
                    recordTypeId = recordTypeTT,
                    WhatId=tripView.Id,
                    ActivityDate=tripview_dateinformation,
                    Deadline_Date__c=tripView.Deadline_Date__c != null ? tripView.Deadline_Date__c : null,
                    OwnerId=coordinatorGT,
                    Subject=tripView.Status__c,
                    Task_Type__c='Air Status Trace'
                );
            }
        }*/

    if (tripViewId != null && tripViewId != '') {
      Air__c airAux = new Air__c(Id = tripViewId);
      if (tripview_typeinformation == 'tripview_tracedate')
        airAux.Trace_Date__c = tripview_dateinformation;
      if (tripview_typeinformation == 'tripview_decisionduedate')
        airAux.Decision_Due_Date__c = tripview_dateinformation;
      if (tripview_typeinformation == 'tripview_deadlinedate')
        airAux.Deadline_Date__c = tripview_dateinformation;
      update airAux;
    }
  }

  /*public void searchLocation(){
        String strQuery;
        String nameAux;
        searchLocationList = new List<wrapperLocation>();
        searchLocationRelatedList = new List<wrapperLocation>();
        if(searchlocation_open){
            Map<String,Bid__c> bidAuxMap = new Map<String,Bid__c>();
            //Date StartDate = tripView.Start_Date__c;
            //Date EndDate = tripView.End_Date__c;
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
                strQuery += ' LIMIT 50000';
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
                strQuery += ' ORDER BY Name ASC LIMIT 50000';
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
                strQuery += ' ORDER BY Name ASC LIMIT 50000';
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
            Start_Date__c = newtravel_startdate != null ? newtravel_startdate.date() : null,
            Start_Date_Full__c = newtravel_startdate != null ? newtravel_startdate : null,
            Start_Date_Time__c = newtravel_startdate != null ? newtravel_startdate.time() : null,
            End_Date__c = newtravel_enddate != null ? newtravel_enddate.date() : null,
            End_Date_Full__c = newtravel_enddate != null ? newtravel_enddate : null,
            End_Date_Time__c = newtravel_enddate != null ? newtravel_enddate.time() : null,
            Travel_Type__c = newtravel_traveltype,
            Group_Type__c = newtravel_grouptype,
            Location_Type__c = newtravel_locationtype,
            Location_Pick_up__c = newtravel_locationpickup,
            Location_Drop_off__c = newtravel_locationdropoff,
            Location_Details__c = newtravel_locationdetails,
            Airline_Info_Special_Notes__c = newtravel_notes
        );
        if(newtravel_subtripid != null && newtravel_subtripid != '') travel.GT_Sub_Trip_Details__c = newtravel_subtripid;
        if(travelActualId == '') travel.Production_Ground__c = opportunityId;
        upsert travel;
        
        if(newtravel_updatemaster){
            Ground__c gAux = new Ground__c(Id = tripViewId);
            if(newtravel_startdate != null){
                //tripView.Start_Date__c = tripView.Start_Date__c != null ? (tripView.Start_Date__c <= newtravel_startdate.date() ? tripView.Start_Date__c : newtravel_startdate.date()) : newtravel_startdate.date();
                //gAux.Start_Date__c = tripView.Start_Date__c != null ? (tripView.Start_Date__c <= newtravel_startdate.date() ? tripView.Start_Date__c : newtravel_startdate.date()) : newtravel_startdate.date();
            }
            if(newtravel_enddate != null){
                //tripView.End_Date__c = tripView.End_Date__c != null ? (tripView.End_Date__c >= newtravel_enddate.date() ? tripView.End_Date__c : newtravel_enddate.date()) : newtravel_enddate.date();
                //gAux.End_Date__c = tripView.End_Date__c != null ? (tripView.End_Date__c >= newtravel_enddate.date() ? tripView.End_Date__c : newtravel_enddate.date()) : newtravel_enddate.date();
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
                Description__c = 'Airport transfer'
            );
            insert new_subtrip;
            refreshSubtripsDataBids(tripViewid);
            searchItinerary();
            getSubStripByTrip();
        }
    }
    
    public static void refreshSubtripsDataBids(String tripViewId){
        List<Bid__c> bidExist = [SELECT Id, GT__c, Production__c FROM Bid__c WHERE GT__c =: tripViewId AND Status__c NOT IN ('Contracted')];
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
                for(Ground__c g : [SELECT Id, Line__c, Vehicle_Ref__c, GT_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c,
                                   Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c
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
            for(Ground__c subtrip : [SELECT Id, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, GT_Trip_Details__c, GT_Freight__c
                                     FROM Ground__c 
                                     WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND GT_Trip_Details__c =: tripViewid ORDER BY Trip_Order__c ASC]){
                                         subTripList.add(subtrip);
                                         hasFreightMap.put(subtrip.Id,subtrip.GT_Freight__c != null ? true : false);
                                     }
            
            if(subTripList.size() > 0){
                List<Ground__c> travelAux;
                for(Ground__c g : [SELECT Id, Line__c, Vehicle_Ref__c, GT_Sub_Trip_Details__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c,
                                   Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c
                                   FROM Ground__c WHERE RecordType.Name = 'GT Travel Details' AND GT_Sub_Trip_Details__c =: subTripList ORDER BY Line__c ASC]){
                    travelAux = travelsBySubTripMap.get(g.GT_Sub_Trip_Details__c) != null ? travelsBySubTripMap.get(g.GT_Sub_Trip_Details__c) : new List<Ground__c>();
                    travelAux.add(g);
                    travelsBySubTripMap.put(g.GT_Sub_Trip_Details__c,travelAux.clone());
                }
                for(Ground__c subtrip : subTripList){
                    if(travelsBySubTripMap.get(subtrip.Id) == null) travelsBySubTripMap.put(subtrip.Id,new List<Ground__c>());
                }
            }
        }
    }*/

  public void saveEditAircraftTrip() {
    if (aircraftIdActual != null && aircraftIdActual != '') {
      Air__c aircraft = new Air__c(
        Id = aircraftIdActual,
        Aircraft_Type__c = aircraft_type,
        economy_seats__c = aircraft_economyseats != null &&
          aircraft_economyseats != ''
          ? Decimal.valueOf(aircraft_economyseats)
          : null,
        Cargo_capacity__c = aircraft_cargocapacity,
        Seat_pitch__c = aircraft_seatpitch,
        Airline__c = aircraft_airlineid != null &&
          aircraft_airlineid != ''
          ? aircraft_airlineid
          : null,
        Positioning_from_time__c = aircraft_position,
        Air_Charter_Trip_Contents__c = aircraft_tripcontents
      );
      update aircraft;

      refreshAircraftDataBids(tripViewId);
    }
    searchItinerary();
    getAircraftsByTrip();
  }

  public void addAircraftTrip() {
    if (
      opportunityId != null &&
      opportunityId != null &&
      tripViewId != null &&
      tripViewId != ''
    ) {
      newAircraftTrip.Id = null;
      newAircraftTrip.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Crafts')
        .getRecordTypeId();
      newAircraftTrip.Production__c = opportunityId;
      newAircraftTrip.Air_Crafts_Details__c = tripViewId;
      newAircraftTrip.Airline__c = aircraft_airlineid != null &&
        aircraft_airlineid != ''
        ? aircraft_airlineid
        : null;
      insert newAircraftTrip;

      refreshAircraftDataBids(tripViewId);
    }
    searchItinerary();
    getAircraftsByTrip();
  }

  public static void refreshAircraftDataBids(String tripViewId) {
    List<Bid__c> bidExist = [
      SELECT Id, Air__c, Production__c
      FROM Bid__c
      WHERE Air__c = :tripViewId AND Status__c NOT IN ('Contracted')
    ];
    if (bidExist.size() > 0) {
      delete [
        SELECT Id
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Crafts'
          AND Bid_Aircraft__c IN :bidExist
      ];

      List<Air__c> aircraftsByTripList = [
        SELECT
          Id,
          Production__c,
          RecordTypeId,
          RecordType.Name,
          Bid_Aircraft__c,
          Aircraft_Type__c,
          economy_seats__c,
          Cargo_capacity__c,
          Seat_pitch__c,
          Airline__c,
          Airline__r.Name,
          Positioning_from_time__c,
          Air_Charter_Trip_Contents__c,
          Air_Crafts_Details__c
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Crafts'
          AND Production__c = :bidExist[0].Production__c
          AND Air_Crafts_Details__c = :tripViewId
          AND Bid_Aircraft__c = NULL
      ];
      Air__c aAux;
      List<Air__c> aListAux = new List<Air__c>();
      for (Bid__c b : bidExist) {
        for (Air__c a : aircraftsByTripList) {
          aAux = a.clone();
          aAux.Bid_Aircraft__c = b.Id;
          aAux.Air_Crafts_Details__c = null;
          aAux.Production__c = b.Production__c;
          aAux.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Crafts')
            .getRecordTypeId();
          aListAux.add(aAux);
        }
      }

      if (aListAux.size() > 0)
        insert aListAux;
    }
  }

  public void getAircraftsByTrip() {
    aircraftsByTripList = new List<Air__c>();
    if (tripViewId != null && tripViewId != '') {
      aircraftsByTripList = [
        SELECT
          Id,
          Production__c,
          RecordTypeId,
          RecordType.Name,
          Bid_Aircraft__c,
          Aircraft_Type__c,
          economy_seats__c,
          Cargo_capacity__c,
          Seat_pitch__c,
          Airline__c,
          Airline__r.Name,
          Positioning_from_time__c,
          Air_Charter_Trip_Contents__c,
          Air_Crafts_Details__c
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Crafts'
          AND Production__c = :opportunityId
          AND Air_Crafts_Details__c = :tripViewId
          AND Bid_Aircraft__c = NULL
      ];
    }
  }

  public void saveEditConcessionTrip() {
    if (concessionActual != null && concessionActual != '') {
      newConcessionTrip = new Concessions__c(
        Id = concessionActual,
        Concession_Type__c = 'Air',
        Concessions_Requested__c = concessionRequestedActual,
        Create_in_Bid__c = concessionCreateInBid
      );
      update newConcessionTrip;
      refreshConcessionDataBids(tripViewId);
    }
    getConcessionsByTrip();
  }

  public void deleteConcession() {
    if (concessionActual != null && concessionActual != '') {
      delete [SELECT Id FROM Concessions__c WHERE Id = :concessionActual];
      refreshConcessionDataBids(tripViewId);
    }
    getConcessionsByTrip();
  }

  public void addConcessionTrip() {
    system.debug(tripViewId);
    if (tripViewId != null && tripViewId != '') {
      newConcessionTrip.Concession_Type__c = 'Air';
      newConcessionTrip.Production__c = opportunityId;
      newConcessionTrip.Air__c = tripViewId;
      newConcessionTrip.Create_in_Bid__c = concessionCreateInBid;
      newConcessionTrip.Concessions_Requested__c = concessionRequestedActual;
      insert newConcessionTrip;
      refreshConcessionDataBids(tripViewId);
    }
    getConcessionsByTrip();
  }

  public static void refreshConcessionDataBids(String tripViewId) {
    List<Bid__c> bidExist = [
      SELECT Id, Air__c, Production__c
      FROM Bid__c
      WHERE Air__c = :tripViewId AND Status__c NOT IN ('Contracted')
    ];
    if (bidExist.size() > 0) {
      delete [SELECT Id FROM Concessions__c WHERE Bid__c IN :bidExist];

      List<Concessions__c> concessionByTripList = [
        SELECT
          Id,
          Concessions_Requested__c,
          Concession_Type__c,
          Notes__c,
          Create_in_Bid__c
        FROM Concessions__c
        WHERE
          Production__c = :bidExist[0].Production__c
          AND Air__c = :tripViewId
          AND Create_in_Bid__c = TRUE
        ORDER BY CreatedDate DESC
      ];
      Concessions__c cAux;
      List<Concessions__c> cListAux = new List<Concessions__c>();
      for (Bid__c b : bidExist) {
        for (Concessions__c c : concessionByTripList) {
          cAux = c.clone();
          cAux.Bid__c = b.Id;
          cAux.Air__c = null;
          cAux.Production__c = b.Production__c;
          cAux.Concession_Type__c = 'Air';
          cListAux.add(cAux);
        }
      }

      if (cListAux.size() > 0)
        insert cListAux;
    }
  }

  public void getConcessionsByTrip() {
    concessionsRequestedTrip = new List<Concessions__c>();
    if (opportunityId != null && opportunityId != '') {
      if (tripViewId != null && tripViewId != '') {
        concessionsRequestedTrip = [
          SELECT
            Id,
            Concessions_Requested__c,
            Concession_Type__c,
            Notes__c,
            Create_in_Bid__c
          FROM Concessions__c
          WHERE Production__c = :opportunityId AND Air__c = :tripViewId
          ORDER BY CreatedDate DESC
        ];
      }
    }
  }

  public void newConcessionTrip() {
    newConcessionTrip = new Concessions__c(Concession_Type__c = 'GT');
  }

  public void sendEditReleaseBid() {
    if (dataids != null && dataids.trim() != '') {
      Set<String> vendorContactIds = new Set<String>();
      for (String d : dataids.split(',')) {
        vendorContactIds.add(sendBidRequestMapRelease.get(d).Vendor_Contact__c);
      }

      Map<String, Contact> contactMap = new Map<String, Contact>();
      for (Contact c : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE Id IN :vendorContactIds
      ])
        contactMap.put(c.Id, c);

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = verifyEmailUser(
        UserInfo.getUserId(),
        opportunityid,
        tripViewId
      );
      String owaeId = userActual != null &&
        userActual.Email != null
        ? verifyWideAddress(userActual.Email)
        : null;

      Journal__c journalAux;
      Bid__c bAux;
      List<Journal__c> journalAuxList = new List<Journal__c>();
      Map<String, Bid__c> bidUpdateMap = new Map<String, Bid__c>();
      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail;
      String[] toAddresses;
      Set<String> ccAddresses;
      String body = '';
      String startDate;
      String returnDate;
      for (String d : dataids.split(',')) {
        //New Journals
        journalAux = new Journal__c(
          RecordTypeId = journal_bidjournalRT,
          Bid__c = sendBidRequestMapRelease.get(d).Id,
          Journal_Entry__c = 'Release Bid has been sent to ' +
            contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c)
              .Name +
            ' at ' +
            contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c)
              .Email
        );
        journalAuxList.add(journalAux);

        //Bid update
        if (
          sendBidRequestMapRelease.get(d) != null &&
          sendBidRequestMapRelease.get(d).Status__c != 'Contracted'
        ) {
          bAux = new Bid__c(
            Id = sendBidRequestMapRelease.get(d).Id,
            Status__c = 'Bid Released'
          );
          bidUpdateMap.put(bAux.Id, bAux);
        }

        //EMAIL
        ccAddresses = new Set<String>();
        for (ContactWrapper cw : contactsByVendor_releaseMap.get(d)) {
          if (!cw.disabled && cw.selected)
            ccAddresses.add(cw.c.Email);
        }
        if (sendBidRequestMapRelease.get(d).Vendor__r.ParentId != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_releaseMap.get(
              sendBidRequestMapRelease.get(d).Vendor__r.ParentId
            )
          ) {
            if (!cw.disabled && cw.selected)
              ccAddresses.add(cw.c.Email);
          }
        }

        startDate = (sendBidRequestMapRelease.get(d).Air__r.Departure_Date__c !=
          null
          ? Datetime.newInstance(
                sendBidRequestMapRelease.get(d).Air__r.Departure_Date__c.year(),
                sendBidRequestMapRelease.get(d)
                  .Air__r.Departure_Date__c.month(),
                sendBidRequestMapRelease.get(d).Air__r.Departure_Date__c.day()
              )
              .format('dd MMMMM yyyy')
          : '');
        returnDate = (sendBidRequestMapRelease.get(d).Air__r.Return_Date__c !=
          null
          ? Datetime.newInstance(
                sendBidRequestMapRelease.get(d).Air__r.Return_Date__c.year(),
                sendBidRequestMapRelease.get(d).Air__r.Return_Date__c.month(),
                sendBidRequestMapRelease.get(d).Air__r.Return_Date__c.day()
              )
              .format('dd MMMMM yyyy')
          : '');

        mail = new Messaging.SingleEmailMessage();
        if (owaeId != null)
          mail.setOrgWideEmailAddressId(owaeId);
        toAddresses = new List<String>{
          contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c)
            .Email
        };
        mail.setToAddresses(toAddresses);
        if (ccAddresses.size() > 0)
          mail.setCcAddresses(new List<String>(ccAddresses));
        mail.setSubject(
          emailSubject.replace(
              '{ProductionName}',
              sendBidRequestMapRelease.get(d).Production__r.Name
            )
            .replace('{DepDate}', startDate)
            .replace(
              '{DepartureCity}',
              sendBidRequestMapRelease.get(d)
                  .Air__r.Departure_City__r.Airport_Code__c != null
                ? sendBidRequestMapRelease.get(d)
                    .Air__r.Departure_City__r.Airport_Code__c
                : ''
            )
            .replace(
              '{ArrivalCity}',
              sendBidRequestMapRelease.get(d)
                  .Air__r.Arrival_City__r.Airport_Code__c != null
                ? sendBidRequestMapRelease.get(d)
                    .Air__r.Arrival_City__r.Airport_Code__c
                : ''
            )
        );

        mail.setHtmlBody(
          emailBody.replace(
              '{VendorName}',
              sendBidRequestMapRelease.get(d).Vendor__r.Name
            )
            .replace(
              '{ProductionName}',
              sendBidRequestMapRelease.get(d).Production__r.Name
            )
            .replace(
              '{GroupType}',
              sendBidRequestMapRelease.get(d).Air__r.Group_Type__c != null
                ? sendBidRequestMapRelease.get(d).Air__r.Group_Type__c
                : ''
            )
            .replace('{TripStartDate}', startDate)
            .replace('{TripEndDate}', returnDate)
            .replace(
              '{AirCoordinator}',
              userActual != null &&
                userActual.Name != null
                ? userActual.Name
                : ''
            )
        );
        myEmails.add(mail);
      }

      Air__c aAux = new Air__c(
        Id = tripViewId,
        Email_Subject_Release_Bid__c = null,
        Email_Body_Release_Bid__c = null
      );
      update aAux;
      insert journalAuxList;
      update bidUpdateMap.values();
      if (myEmails.size() > 0)
        Messaging.sendEmail(myEmails);
      openReleaseBid();
    }
  }

  public void saveAndCloseReleaseBid() {
    List<Air__c> template = [
      SELECT Id, Email_Subject_Release_Bid__c, Email_Body_Release_Bid__c
      FROM Air__c
      WHERE Id = :tripViewId
    ];
    if (template.size() > 0) {
      template[0].Email_Subject_Release_Bid__c = emailSubject.unescapeHtml4();
      template[0].Email_Body_Release_Bid__c = emailBody.unescapeHtml4();
      update template[0];
    }
  }

  public void sendReleaseBid() {
    if (dataids != null && dataids.trim() != '') {
      Set<String> vendorContactIds = new Set<String>();
      Set<String> bidIds = new Set<String>();
      Set<String> airIds = new Set<String>();
      for (String d : dataids.split(',')) {
        bidIds.add(sendBidRequestMapRelease.get(d).Id);
        airIds.add(sendBidRequestMapRelease.get(d).Air__c);
        vendorContactIds.add(sendBidRequestMapRelease.get(d).Vendor_Contact__c);
      }

      Map<String, Contact> contactMap = new Map<String, Contact>();
      for (Contact c : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE Id IN :vendorContactIds
      ])
        contactMap.put(c.Id, c);

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = verifyEmailUser(
        UserInfo.getUserId(),
        opportunityid,
        tripViewId
      );
      String owaeId = userActual != null &&
        userActual.Email != null
        ? verifyWideAddress(userActual.Email)
        : null;

      String BidRecordLocatorAndSeatDetails;
      Map<String, String> revenueMap = new Map<String, String>();
      for (Revenue__c r : [
        SELECT Id, Bid__c, Record_Locator__c, of_seats__c
        FROM Revenue__c
        WHERE
          Bid__c IN :bidIds
          AND RecordType.DeveloperName = 'Air_Rate_Commission'
      ]) {
        BidRecordLocatorAndSeatDetails =
          'Record Locator: ' +
          (r.Record_Locator__c != null ? r.Record_Locator__c : '') +
          ' , no of seats: ' +
          (r.of_seats__c != null ? String.valueOf(r.of_seats__c) : '');
        revenueMap.put(
          r.Bid__c,
          revenueMap.get(r.Bid__c) != null
            ? revenueMap.get(r.Bid__c) +
              '<br/>' +
              BidRecordLocatorAndSeatDetails
            : BidRecordLocatorAndSeatDetails
        );
      }

      String segments;
      Map<String, String> segmentMap = new Map<String, String>();
      for (Air__c segment : [
        SELECT
          Id,
          Air_Trip_Details__c,
          Departure_Date__c,
          Return_Date__c,
          Departure_City__c,
          Arrival_City__c,
          Departure_City__r.Airport_Code__c,
          Departure_City__r.Name,
          Departure_City__r.City__c,
          Departure_City__r.City__r.Name,
          Arrival_City__r.Airport_Code__c,
          Arrival_City__r.Name,
          Arrival_City__r.City__c,
          Arrival_City__r.City__r.Name
        FROM Air__c
        WHERE
          Air_Trip_Details__c IN :airIds
          AND RecordType.DeveloperName = 'Air_Segments'
      ]) {
        segments =
          (segment.Departure_City__r.Airport_Code__c != null
            ? segment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (segment.Arrival_City__r.Airport_Code__c != null
            ? segment.Arrival_City__r.Airport_Code__c
            : '');
        segmentMap.put(
          segment.Air_Trip_Details__c,
          segmentMap.get(segment.Air_Trip_Details__c) != null
            ? segmentMap.get(segment.Air_Trip_Details__c) + ', ' + segments
            : segments
        );
      }

      Journal__c journalAux;
      Bid__c bAux;
      List<Journal__c> journalAuxList = new List<Journal__c>();
      Map<String, Bid__c> bidUpdateMap = new Map<String, Bid__c>();
      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail;
      String[] toAddresses;
      Set<String> ccAddresses;
      String body = '';
      List<EmailTemplate> template = [
        SELECT Id, Name, Subject, Body, HTMLValue
        FROM EmailTemplate
        WHERE DeveloperName = 'Air_Release_Bid'
      ];
      String subject;
      String startDate;
      String returnDate;
      for (String d : dataids.split(',')) {
        //New Journals
        journalAux = new Journal__c(
          RecordTypeId = journal_bidjournalRT,
          Bid__c = sendBidRequestMapRelease.get(d).Id,
          Journal_Entry__c = 'Release Bid has been sent to ' +
            contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c)
              .Name +
            ' at ' +
            contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c)
              .Email
        );
        journalAuxList.add(journalAux);

        //Bid update
        if (
          sendBidRequestMapRelease.get(d) != null &&
          sendBidRequestMapRelease.get(d).Status__c != 'Contracted'
        ) {
          bAux = new Bid__c(
            Id = sendBidRequestMapRelease.get(d).Id,
            Status__c = 'Bid Released'
          );
          bidUpdateMap.put(bAux.Id, bAux);
        }

        //EMAIL
        ccAddresses = new Set<String>();
        for (ContactWrapper cw : contactsByVendor_releaseMap.get(d)) {
          if (!cw.disabled && cw.selected)
            ccAddresses.add(cw.c.Email);
        }
        if (sendBidRequestMapRelease.get(d).Vendor__r.ParentId != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_releaseMap.get(
              sendBidRequestMapRelease.get(d).Vendor__r.ParentId
            )
          ) {
            if (!cw.disabled && cw.selected)
              ccAddresses.add(cw.c.Email);
          }
        }

        mail = new Messaging.SingleEmailMessage();
        if (owaeId != null)
          mail.setOrgWideEmailAddressId(owaeId);
        toAddresses = new List<String>{
          contactMap.get(sendBidRequestMapRelease.get(d).Vendor_Contact__c)
            .Email
        };
        mail.setToAddresses(toAddresses);
        if (ccAddresses.size() > 0)
          mail.setCcAddresses(new List<String>(ccAddresses));

        startDate = (sendBidRequestMapRelease.get(d).Air__r.Departure_Date__c !=
          null
          ? Datetime.newInstance(
                sendBidRequestMapRelease.get(d).Air__r.Departure_Date__c.year(),
                sendBidRequestMapRelease.get(d)
                  .Air__r.Departure_Date__c.month(),
                sendBidRequestMapRelease.get(d).Air__r.Departure_Date__c.day()
              )
              .format('dd MMMMM yyyy')
          : '');
        returnDate = (sendBidRequestMapRelease.get(d).Air__r.Return_Date__c !=
          null
          ? Datetime.newInstance(
                sendBidRequestMapRelease.get(d).Air__r.Return_Date__c.year(),
                sendBidRequestMapRelease.get(d).Air__r.Return_Date__c.month(),
                sendBidRequestMapRelease.get(d).Air__r.Return_Date__c.day()
              )
              .format('dd MMMMM yyyy')
          : '');

        subject = template.size() > 0 ? template[0].Subject : '';
        body = template[0].HTMLValue != null ? template[0].HTMLValue : '';
        mail.setSubject(
          subject.replace(
              '{ProductionName}',
              sendBidRequestMapRelease.get(d).Production__r.Name
            )
            .replace('{DepDate}', startDate)
            .replace(
              '{DepartureCity}',
              sendBidRequestMapRelease.get(d)
                  .Air__r.Departure_City__r.Airport_Code__c != null
                ? sendBidRequestMapRelease.get(d)
                    .Air__r.Departure_City__r.Airport_Code__c
                : ''
            )
            .replace(
              '{ArrivalCity}',
              sendBidRequestMapRelease.get(d)
                  .Air__r.Arrival_City__r.Airport_Code__c != null
                ? sendBidRequestMapRelease.get(d)
                    .Air__r.Arrival_City__r.Airport_Code__c
                : ''
            )
        );

        mail.setHtmlBody(
          body.replace(
              '{VendorName}',
              sendBidRequestMapRelease.get(d).Vendor__r.Name
            )
            .replace(
              '{ProductionName}',
              sendBidRequestMapRelease.get(d).Production__r.Name
            )
            .replace(
              '{GroupType}',
              sendBidRequestMapRelease.get(d).Air__r.Group_Type__c != null
                ? sendBidRequestMapRelease.get(d).Air__r.Group_Type__c
                : ''
            )
            .replace('{TripStartDate}', startDate)
            .replace('{TripEndDate}', returnDate)
            .replace(
              '{AirCoordinator}',
              userActual != null &&
                userActual.Name != null
                ? userActual.Name
                : ''
            )
            .replace(
              '{BidDescription}',
              segmentMap.get(sendBidRequestMapRelease.get(d).Air__c) != null
                ? segmentMap.get(sendBidRequestMapRelease.get(d).Air__c)
                : ''
            )
            .replace(
              '{BidRecordLocatorAndSeatDetails}',
              revenueMap.get(sendBidRequestMapRelease.get(d).Id) != null
                ? revenueMap.get(sendBidRequestMapRelease.get(d).Id)
                : 'Record Locator: , no of seats: '
            )
        );
        myEmails.add(mail);
      }

      Air__c aAux = new Air__c(
        Id = tripViewId,
        Email_Subject_Release_Bid__c = null,
        Email_Body_Release_Bid__c = null
      );
      update aAux;
      insert journalAuxList;
      update bidUpdateMap.values();
      if (myEmails.size() > 0)
        Messaging.sendEmail(myEmails);
      isBidReleaseRendered = false;
      getBidsByTrip();
    }
  }

  public void sendBidRequestEdit() {
    if (dataids != null && dataids.trim() != '') {
      Set<String> vendorContactIds = new Set<String>();
      Set<String> airIds = new Set<String>();
      for (String d : dataids.split(',')) {
        airIds.add(sendBidRequestMap.get(d).Air__c);
        vendorContactIds.add(sendBidRequestMap.get(d).Vendor_Contact__c);
      }

      List<Air__c> segmentList = [
        SELECT
          Id,
          Air_Trip_Details__c,
          Departure_Date__c,
          Return_Date__c,
          Departure_City__c,
          Arrival_City__c,
          Departure_City__r.Airport_Code__c,
          Departure_City__r.Name,
          Departure_City__r.City__c,
          Departure_City__r.City__r.Name,
          Arrival_City__r.Airport_Code__c,
          Arrival_City__r.Name,
          Arrival_City__r.City__c,
          Arrival_City__r.City__r.Name
        FROM Air__c
        WHERE
          Air_Trip_Details__c IN :airIds
          AND RecordType.DeveloperName = 'Air_Segments'
      ];
      Map<String, String> segmentMap = new Map<String, String>();
      if (segmentList.size() > 0) {
        String segmentsTravelDetails;
        for (Air__c segment : segmentList) {
          segmentsTravelDetails =
            '<br/>Travelling from: ' +
            (segment.Departure_City__r.Airport_Code__c != null
              ? segment.Departure_City__r.Airport_Code__c
              : '') +
            '<br/>Travelling to: ' +
            (segment.Arrival_City__r.Airport_Code__c != null
              ? segment.Arrival_City__r.Airport_Code__c
              : '') +
            '<br/>Date of travel: ' +
            (segmentList.size() < 2 ||
              segmentList.size() > 2
              ? DateTime.newInstance(
                    segment.Departure_Date__c,
                    Time.newInstance(0, 0, 0, 0)
                  )
                  .format('EEEE') +
                ', ' +
                (segment.Departure_Date__c != null
                  ? Datetime.newInstance(
                        segment.Departure_Date__c.year(),
                        segment.Departure_Date__c.month(),
                        segment.Departure_Date__c.day()
                      )
                      .format('dd MMMMM yyyy')
                  : '')
              : (segmentList.size() == 2 &&
                  segment.Return_Date__c != null
                  ? Datetime.newInstance(
                        segment.Return_Date__c.year(),
                        segment.Return_Date__c.month(),
                        segment.Return_Date__c.day()
                      )
                      .format('EEEE, dd MMMMM yyyy')
                  : '')) +
            '<br/>';

          segmentsTravelDetails = segmentMap.get(segment.Air_Trip_Details__c) !=
            null
            ? segmentMap.get(segment.Air_Trip_Details__c) +
              segmentsTravelDetails
            : segmentsTravelDetails;
          segmentMap.put(segment.Air_Trip_Details__c, segmentsTravelDetails);
        }
      }

      Map<String, Contact> contactMap = new Map<String, Contact>();
      for (Contact c : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE Id IN :vendorContactIds
      ])
        contactMap.put(c.Id, c);

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = verifyEmailUser(
        UserInfo.getUserId(),
        opportunityid,
        tripViewId
      );
      String owaeId = userActual != null &&
        userActual.Email != null
        ? verifyWideAddress(userActual.Email)
        : null;

      Journal__c journalAux;
      Bid__c bAux;
      List<Journal__c> journalAuxList = new List<Journal__c>();
      Map<String, Bid__c> bidUpdateMap = new Map<String, Bid__c>();
      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail;
      String[] toAddresses;
      Set<String> ccAddresses;
      String body = '';
      List<EmailTemplate> template = [
        SELECT Id, Name, Subject, Body, HTMLValue
        FROM EmailTemplate
        WHERE DeveloperName = 'Air_Bid_Request_All'
      ];

      String subject;
      String startDate;
      String returnDate;
      String segmentsTravelDetails;
      List<String> congaParameters = new List<String>();
      String ccEmails;
      Integer i = 1;
      APXTConga4__Conga_Email_Template__c congaEmailTemplate;
      if (tripView.Air_Charter__c) {
        congaEmailTemplate = new APXTConga4__Conga_Email_Template__c(
          APXTConga4__Name__c = 'Air Charter Bid Request - ' + tripView.Name,
          SObjectId__c = 'AirCharterBidRequest-' + tripView.id,
          APXTConga4__HTMLBody__c = emailBody.replace(
              '{VendorName}',
              '{{TableStart:Bid}}{{VENDOR_NAME}}{{TableEnd:Bid}}'
            )
            .replace(
              '{ProductionName}',
              '{{TableStart:Bid}}{{PRODUCTION_NAME}}{{TableEnd:Bid}}'
            )
            .replace(
              '{GroupType}',
              '{{TableStart:Bid}}{{AIR_GROUP_TYPE}}{{TableEnd:Bid}}'
            )
            .replace(
              '{TravelDetails}',
              '{{TableStart:BidItinerarySegments}}Travelling from: {{DEPARTURE_CITY_AIRPORT_CODE}}<br>Travelling to: {{ARRIVAL_CITY_AIRPORT_CODE}}<br>Date of travel: {{AIR_DEPARTURE_DATE \@ "dddd, dd MMMMM yyyy"}}<br>{{TableEnd:BidItinerarySegments}}'
            )
            .replace(
              '{NosOfSeats}',
              '{{TableStart:Bid}}{{AIR_PAX}}{{TableEnd:Bid}}'
            )
            .replace(
              '{AirCoordinator}',
              '{{TableStart:ProductionAssoc}}{{PRODUCTION_ASSOCIATIONS__CUSER_NAME}}{{TableEnd:ProductionAssoc}}'
            )
        );
        try {
          upsert congaEmailTemplate SObjectId__c;
        } catch (Exception e) {
          System.debug(
            '###AirDashboardController.sendBidRequestEdit() - Exception: ' +
            e.getMessage()
          );
        }
      }
      for (String d : dataids.split(',')) {
        segmentsTravelDetails = '';
        //New Journals
        journalAux = new Journal__c(
          RecordTypeId = journal_bidjournalRT,
          Bid__c = sendBidRequestMap.get(d).Id,
          Journal_Entry__c = 'Air Bid Request has been sent to ' +
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Name +
            ' at ' +
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email
        );
        journalAuxList.add(journalAux);

        //Bid update
        if (
          sendBidRequestMap.get(d) != null &&
          sendBidRequestMap.get(d).Status__c == 'Unsent'
        ) {
          bAux = new Bid__c(
            Id = sendBidRequestMap.get(d).Id,
            Status__c = 'Lead Sent',
            Lead_Sent__c = true
          );
          bidUpdateMap.put(bAux.Id, bAux);
        }

        //EMAIL
        ccAddresses = new Set<String>();
        ccEmails = '';
        for (ContactWrapper cw : contactsByVendor_bidRequestMap.get(d)) {
          if (!cw.disabled && cw.selected) {
            ccAddresses.add(cw.c.Email);
            ccEmails = String.isNotBlank(ccEmails)
              ? ccEmails + ', ' + cw.c.Email
              : cw.c.Email;
          }
        }
        if (sendBidRequestMap.get(d).Vendor__r.ParentId != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
              sendBidRequestMap.get(d).Vendor__r.ParentId
            )
          ) {
            if (!cw.disabled && cw.selected) {
              ccAddresses.add(cw.c.Email);
              ccEmails = String.isNotBlank(ccEmails)
                ? ccEmails + ', ' + cw.c.Email
                : cw.c.Email;
            }
          }
        }

        if (!tripView.Air_Charter__c) {
          mail = new Messaging.SingleEmailMessage();
          if (owaeId != null)
            mail.setOrgWideEmailAddressId(owaeId);
          toAddresses = new List<String>{
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email
          };
          mail.setToAddresses(toAddresses);
          if (ccAddresses.size() > 0)
            mail.setCcAddresses(new List<String>(ccAddresses));

          startDate = (sendBidRequestMap.get(d).Air__r.Departure_Date__c != null
            ? Datetime.newInstance(
                  sendBidRequestMap.get(d).Air__r.Departure_Date__c.year(),
                  sendBidRequestMap.get(d).Air__r.Departure_Date__c.month(),
                  sendBidRequestMap.get(d).Air__r.Departure_Date__c.day()
                )
                .format('dd MMMMM yyyy')
            : '');
          returnDate = (sendBidRequestMap.get(d).Air__r.Return_Date__c != null
            ? Datetime.newInstance(
                  sendBidRequestMap.get(d).Air__r.Return_Date__c.year(),
                  sendBidRequestMap.get(d).Air__r.Return_Date__c.month(),
                  sendBidRequestMap.get(d).Air__r.Return_Date__c.day()
                )
                .format('dd MMMMM yyyy')
            : '');

          subject = template.size() > 0 ? template[0].Subject : '';
          mail.setSubject(
            subject.replace(
                '{ProductionName}',
                sendBidRequestMap.get(d).Production__r.Name
              )
              .replace('{DepDate}', startDate)
              .replace(
                '{DepartureCity}',
                sendBidRequestMap.get(d)
                    .Air__r.Departure_City__r.Airport_Code__c != null
                  ? sendBidRequestMap.get(d)
                      .Air__r.Departure_City__r.Airport_Code__c
                  : ''
              )
              .replace(
                '{ArrivalCity}',
                sendBidRequestMap.get(d)
                    .Air__r.Arrival_City__r.Airport_Code__c != null
                  ? sendBidRequestMap.get(d)
                      .Air__r.Arrival_City__r.Airport_Code__c
                  : ''
              )
          );
          system.debug(sendBidRequestMap);
          mail.setHtmlBody(
            emailBody.replace(
                '{VendorName}',
                sendBidRequestMap.get(d).Vendor__r.Name
              )
              .replace(
                '{ProductionName}',
                sendBidRequestMap.get(d).Production__r.Name
              )
              .replace(
                '{GroupType}',
                sendBidRequestMap.get(d).Air__r.Group_Type__c != null
                  ? sendBidRequestMap.get(d).Air__r.Group_Type__c
                  : ''
              )
              .replace(
                '{TravelDetails}',
                segmentMap.get(sendBidRequestMap.get(d).Air__c) != null
                  ? segmentMap.get(sendBidRequestMap.get(d).Air__c)
                  : ''
              )
              .replace(
                '{AirCoordinator}',
                userActual != null &&
                  userActual.Name != null
                  ? userActual.Name
                  : ''
              )
              .replace(
                '{NosOfSeats}',
                sendBidRequestMap.get(d).Air__r.PAX__c != null
                  ? String.valueOf(sendBidRequestMap.get(d).Air__r.PAX__c)
                  : ''
              )
          );
          myEmails.add(mail);
        } else {
          /**
           *  @Conga: Update for Conga.
           */
          congaParameters.add(
            '&id=' +
            sendBidRequestMap.get(d).Id +
            (congaQueriesMap.containsKey('Air - AirCharterBidById')
              ? '&QueryId=[Bid]' +
                congaQueriesMap.get('Air - AirCharterBidById').Id +
                '?pv0=' +
                sendBidRequestMap.get(d).Id +
                (congaQueriesMap.containsKey(
                    'Air - BidItinerarySegmentsByBidId'
                  )
                  ? ',[BidItinerarySegments]' +
                    congaQueriesMap.get('Air - BidItinerarySegmentsByBidId')
                      .Id +
                    '?pv0=' +
                    sendBidRequestMap.get(d).Id
                  : '') +
                (congaQueriesMap.containsKey(
                    'Air - ProductionAssociationsByOppId'
                  )
                  ? ',[ProductionAssoc]' +
                    congaQueriesMap.get('Air - ProductionAssociationsByOppId')
                      .Id +
                    '?pv0=' +
                    opportunityId
                  : '')
              : '') +
            '&CongaEmailTemplateId=' +
            (String.isNotEmpty(congaEmailTemplate.id)
              ? congaEmailTemplate.id
              : sendBidRequest_congaEmailTemplateId) +
            '&EmailSubject=' +
            sendBidRequest_congaEmailSubject.replace(' ', '+') +
            (userActual != null &&
              userActual.Email != null
              ? '&EmailFromID=' + verifyWideAddress(userActual.Email)
              : '') +
            '&EmailToId=' +
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).id +
            '&EmailCC=' +
            ccEmails +
            '&TemplateId=' +
            sendBidRequest_congaTemplateId1
          );
          if (dataids.split(',').size() == i || i >= 100) {
            try {
              congaSendEmail(congaParameters);
            } catch (Exception e) {
              System.debug(
                '###AirDashboardController.sendBidRequest() - Exception: ' +
                e.getMessage()
              );
            }
            i = 1;
            congaParameters.clear();
          } else {
            i++;
          }
          /**
           *  @/Conga
           */
        }
      }

      Air__c aAux = new Air__c(
        Id = tripViewId,
        Email_Body_Bid_Request__c = null
      );
      update aAux;
      insert journalAuxList;
      update bidUpdateMap.values();

      if (myEmails.size() > 0)
        Messaging.sendEmail(myEmails);

      getBidsByTrip();
      openSendBidRequest();
    }
  }

  public void sendBidRequest() {
    if (dataids != null && dataids.trim() != '') {
      Set<String> vendorContactIds = new Set<String>();
      Set<String> airIds = new Set<String>();
      for (String d : dataids.split(',')) {
        airIds.add(sendBidRequestMap.get(d).Air__c);
        vendorContactIds.add(sendBidRequestMap.get(d).Vendor_Contact__c);
      }

      List<Air__c> segmentList = [
        SELECT
          Id,
          Air_Trip_Details__c,
          Departure_Date__c,
          Return_Date__c,
          Departure_City__c,
          Arrival_City__c,
          Departure_City__r.Airport_Code__c,
          Departure_City__r.Name,
          Departure_City__r.City__c,
          Departure_City__r.City__r.Name,
          Arrival_City__r.Airport_Code__c,
          Arrival_City__r.Name,
          Arrival_City__r.City__c,
          Arrival_City__r.City__r.Name
        FROM Air__c
        WHERE
          Air_Trip_Details__c IN :airIds
          AND RecordType.DeveloperName = 'Air_Segments'
      ];
      Map<String, String> segmentMap = new Map<String, String>();
      if (segmentList.size() > 0) {
        String segmentsTravelDetails;
        for (Air__c segment : segmentList) {
          segmentsTravelDetails =
            '<br/>Travelling from: ' +
            (segment.Departure_City__c != null &&
              segment.Departure_City__r.Airport_Code__c != null
              ? segment.Departure_City__r.Airport_Code__c
              : '') +
            '<br/>Travelling to: ' +
            (segment.Arrival_City__c != null &&
              segment.Arrival_City__r.Airport_Code__c != null
              ? segment.Arrival_City__r.Airport_Code__c
              : '') +
            '<br/>Date of travel: ' +
            (segmentList.size() < 2 ||
              segmentList.size() > 2
              ? (segment.Departure_Date__c != null
                  ? DateTime.newInstance(
                        segment.Departure_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('EEEE') + ', '
                  : '') +
                (segment.Departure_Date__c != null
                  ? Datetime.newInstance(
                        segment.Departure_Date__c.year(),
                        segment.Departure_Date__c.month(),
                        segment.Departure_Date__c.day()
                      )
                      .format('dd MMMMM yyyy')
                  : '')
              : (segmentList.size() == 2
                  ? (segment.Return_Date__c != null
                      ? DateTime.newInstance(
                            segment.Return_Date__c,
                            Time.newInstance(0, 0, 0, 0)
                          )
                          .format('EEEE') + ', '
                      : '') +
                    (segment.Return_Date__c != null
                      ? Datetime.newInstance(
                            segment.Return_Date__c.year(),
                            segment.Return_Date__c.month(),
                            segment.Return_Date__c.day()
                          )
                          .format('dd MMMMM yyyy')
                      : '')
                  : '')) +
            '<br/>';

          segmentsTravelDetails = segmentMap.get(segment.Air_Trip_Details__c) !=
            null
            ? segmentMap.get(segment.Air_Trip_Details__c) +
              segmentsTravelDetails
            : segmentsTravelDetails;
          segmentMap.put(segment.Air_Trip_Details__c, segmentsTravelDetails);
        }
      }

      Map<String, Contact> contactMap = new Map<String, Contact>();
      for (Contact c : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE Id IN :vendorContactIds
      ])
        contactMap.put(c.Id, c);

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = verifyEmailUser(
        UserInfo.getUserId(),
        opportunityid,
        tripViewId
      );
      String owaeId = userActual != null &&
        userActual.Email != null
        ? verifyWideAddress(userActual.Email)
        : null;

      Journal__c journalAux;
      Bid__c bAux;
      List<Journal__c> journalAuxList = new List<Journal__c>();
      Map<String, Bid__c> bidUpdateMap = new Map<String, Bid__c>();
      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail;
      String[] toAddresses;
      Set<String> ccAddresses;
      String body = '';
      List<EmailTemplate> template = [
        SELECT Id, Name, Subject, Body, HTMLValue
        FROM EmailTemplate
        WHERE DeveloperName = 'Air_Bid_Request_All'
      ];

      String subject;
      String startDate;
      String returnDate;
      String segmentsTravelDetails;
      List<String> congaParameters = new List<String>();
      String ccEmails;
      Integer i = 1;
      for (String d : dataids.split(',')) {
        segmentsTravelDetails = '';
        //New Journals
        journalAux = new Journal__c(
          RecordTypeId = journal_bidjournalRT,
          Bid__c = sendBidRequestMap.get(d).Id,
          Journal_Entry__c = 'Air Bid Request has been sent to ' +
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Name +
            ' at ' +
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email
        );
        journalAuxList.add(journalAux);

        //Bid update
        if (
          sendBidRequestMap.get(d) != null &&
          sendBidRequestMap.get(d).Status__c == 'Unsent'
        ) {
          bAux = new Bid__c(
            Id = sendBidRequestMap.get(d).Id,
            Status__c = 'Lead Sent',
            Lead_Sent__c = true
          );
          bidUpdateMap.put(bAux.Id, bAux);
        }

        //EMAIL
        ccAddresses = new Set<String>();
        ccEmails = '';
        for (ContactWrapper cw : contactsByVendor_bidRequestMap.get(d)) {
          if (!cw.disabled && cw.selected) {
            ccAddresses.add(cw.c.Email);
            ccEmails = String.isNotBlank(ccEmails)
              ? ccEmails + ', ' + cw.c.Email
              : cw.c.Email;
          }
        }
        if (sendBidRequestMap.get(d).Vendor__r.ParentId != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
              sendBidRequestMap.get(d).Vendor__r.ParentId
            )
          ) {
            if (!cw.disabled && cw.selected) {
              ccAddresses.add(cw.c.Email);
              ccEmails = String.isNotBlank(ccEmails)
                ? ccEmails + ', ' + cw.c.Email
                : cw.c.Email;
            }
          }
        }

        if (!tripView.Air_Charter__c) {
          mail = new Messaging.SingleEmailMessage();
          if (owaeId != null)
            mail.setOrgWideEmailAddressId(owaeId);
          toAddresses = new List<String>{
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email
          };
          mail.setToAddresses(toAddresses);
          if (ccAddresses.size() > 0)
            mail.setCcAddresses(new List<String>(ccAddresses));

          startDate = (sendBidRequestMap.get(d).Air__r.Departure_Date__c != null
            ? Datetime.newInstance(
                  sendBidRequestMap.get(d).Air__r.Departure_Date__c.year(),
                  sendBidRequestMap.get(d).Air__r.Departure_Date__c.month(),
                  sendBidRequestMap.get(d).Air__r.Departure_Date__c.day()
                )
                .format('dd MMMMM yyyy')
            : '');
          returnDate = (sendBidRequestMap.get(d).Air__r.Return_Date__c != null
            ? Datetime.newInstance(
                  sendBidRequestMap.get(d).Air__r.Return_Date__c.year(),
                  sendBidRequestMap.get(d).Air__r.Return_Date__c.month(),
                  sendBidRequestMap.get(d).Air__r.Return_Date__c.day()
                )
                .format('dd MMMMM yyyy')
            : '');

          subject = template.size() > 0 ? template[0].Subject : '';
          body = template[0].HTMLValue != null ? template[0].HTMLValue : '';
          mail.setSubject(
            subject.replace(
                '{ProductionName}',
                sendBidRequestMap.get(d).Production__r.Name
              )
              .replace('{DepDate}', startDate)
              .replace(
                '{DepartureCity}',
                sendBidRequestMap.get(d)
                    .Air__r.Departure_City__r.Airport_Code__c != null
                  ? sendBidRequestMap.get(d)
                      .Air__r.Departure_City__r.Airport_Code__c
                  : ''
              )
              .replace(
                '{ArrivalCity}',
                sendBidRequestMap.get(d)
                    .Air__r.Arrival_City__r.Airport_Code__c != null
                  ? sendBidRequestMap.get(d)
                      .Air__r.Arrival_City__r.Airport_Code__c
                  : ''
              )
          );

          mail.setHtmlBody(
            body.replace(
                '{VendorName}',
                sendBidRequestMap.get(d).Vendor__r.Name
              )
              .replace(
                '{ProductionName}',
                sendBidRequestMap.get(d).Production__r.Name
              )
              .replace(
                '{GroupType}',
                sendBidRequestMap.get(d).Air__r.Group_Type__c != null
                  ? sendBidRequestMap.get(d).Air__r.Group_Type__c
                  : ''
              )
              .replace(
                '{TravelDetails}',
                segmentMap.get(sendBidRequestMap.get(d).Air__c) != null
                  ? segmentMap.get(sendBidRequestMap.get(d).Air__c)
                  : ''
              )
              .replace(
                '{AirCoordinator}',
                userActual != null &&
                  userActual.Name != null
                  ? userActual.Name
                  : ''
              )
              .replace(
                '{NosOfSeats}',
                sendBidRequestMap.get(d).Air__r.PAX__c != null
                  ? String.valueOf(sendBidRequestMap.get(d).Air__r.PAX__c)
                  : ''
              )
          );
          myEmails.add(mail);
        } else {
          /**
           *  @Conga: Update for Conga.
           */
          congaParameters.add(
            '&id=' +
            sendBidRequestMap.get(d).Id +
            (congaQueriesMap.containsKey('Air - AirCharterBidById')
              ? '&QueryId=[Bid]' +
                congaQueriesMap.get('Air - AirCharterBidById').Id +
                '?pv0=' +
                sendBidRequestMap.get(d).Id +
                (congaQueriesMap.containsKey(
                    'Air - BidItinerarySegmentsByBidId'
                  )
                  ? ',[BidItinerarySegments]' +
                    congaQueriesMap.get('Air - BidItinerarySegmentsByBidId')
                      .Id +
                    '?pv0=' +
                    sendBidRequestMap.get(d).Id
                  : '') +
                (congaQueriesMap.containsKey(
                    'Air - ProductionAssociationsByOppId'
                  )
                  ? ',[ProductionAssoc]' +
                    congaQueriesMap.get('Air - ProductionAssociationsByOppId')
                      .Id +
                    '?pv0=' +
                    opportunityId
                  : '')
              : '') +
            '&CongaEmailTemplateId=' +
            sendBidRequest_congaEmailTemplateId +
            '&EmailSubject=' +
            sendBidRequest_congaEmailSubject.replace(' ', '+') +
            (userActual != null &&
              userActual.Email != null
              ? '&EmailFromID=' + verifyWideAddress(userActual.Email)
              : '') +
            '&EmailToId=' +
            contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).id +
            '&EmailCC=' +
            ccEmails +
            '&TemplateId=' +
            sendBidRequest_congaTemplateId1
          );
          if (dataids.split(',').size() == i || i >= 100) {
            try {
              congaSendEmail(congaParameters);
            } catch (Exception e) {
              System.debug(
                '###AirDashboardController.sendBidRequest() - Exception: ' +
                e.getMessage()
              );
            }
            i = 1;
            congaParameters.clear();
          } else {
            i++;
          }
          /**
           *  @/Conga
           */
        }
      }

      Air__c aAux = new Air__c(
        Id = tripViewId,
        Email_Body_Bid_Request__c = null
      );
      update aAux;
      insert journalAuxList;
      update bidUpdateMap.values();
      if (myEmails.size() > 0)
        Messaging.sendEmail(myEmails);
      isBidRequestRendered = false;
      getBidsByTrip();
    }
  }

  public void changeContactReleaseBid() {
    sendBidRequestMapRelease.get(vendoraccount_actual_id)
      .Vendor_Contact__c = vendorcontact_actual_id;
    for (
      ContactWrapper cw : contactsByVendor_releaseMap.get(
        vendoraccount_actual_id
      )
    ) {
      if (vendorcontact_actual_id == cw.c.Id) {
        cw.selected = true;
        cw.disabled = true;
      } else {
        if (cw.selected && cw.disabled) {
          cw.selected = false;
          cw.disabled = false;
        }
      }
    }
    if (
      sendBidRequestMapRelease.get(vendoraccount_actual_id)
        .Vendor__r.ParentId != null
    ) {
      for (
        ContactWrapper cw : contactsByVendorParent_releaseMap.get(
          sendBidRequestMapRelease.get(vendoraccount_actual_id)
            .Vendor__r.ParentId
        )
      ) {
        if (vendorcontact_actual_id == cw.c.Id) {
          cw.selected = true;
          cw.disabled = true;
        } else {
          if (cw.selected && cw.disabled) {
            cw.selected = false;
            cw.disabled = false;
          }
        }
      }
    }
  }

  public void openReleaseBid() {
    isBidReleaseRendered = true;
    sendBidRequestMapReleaseSize = 0;
    sendBidRequestMapRelease = new Map<String, Bid__c>();
    Set<String> parentIds = new Set<String>();
    if (
      sendBidRequestMapReleaseSelected == null ||
      sendBidRequestMapReleaseSelected.isEmpty()
    )
      sendBidRequestMapReleaseSelected = new Map<String, Boolean>();
    for (Bid__c b : [
      SELECT
        Id,
        Name,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.ParentId,
        Vendor_Contact__c,
        Status__c,
        Production__c,
        Production__r.Name,
        Air__c,
        Air__r.Departure_Date__c,
        Air__r.Return_Date__c,
        Air__r.Group_Type__c,
        Air__r.Departure_City__r.Airport_Code__c,
        Air__r.Arrival_City__r.Airport_Code__c
      FROM Bid__c
      WHERE
        Id IN :bidByTripIds
        AND Vendor__c != NULL
        AND Status__c IN (
          'Lead Sent',
          'Sent'
        ) /*NOT IN ('Contracted','Cancelled','Contracted On Own')*/
    ]) {
      sendBidRequestMapRelease.put(b.Vendor__c, b);
      if (sendBidRequestMapReleaseSelected.get(b.Vendor__c) == null)
        sendBidRequestMapReleaseSelected.put(b.Vendor__c, false);
      if (b.Vendor__r.ParentId != null)
        parentIds.add(b.Vendor__r.ParentId);
    }

    contactSelectOption_releaseMap = new Map<String, List<SelectOption>>();
    contactSelectOption_releaseSizeMap = new Map<String, Integer>();
    contactsByVendor_releaseMap = new Map<String, List<ContactWrapper>>();
    contactsByVendorParent_releaseMap = new Map<String, List<ContactWrapper>>();
    List<ContactWrapper> contactAuxList;
    List<SelectOption> contactAuxSelectOptions;

    for (Contact c : [
      SELECT
        Id,
        AccountId,
        Account.Name,
        Order__c,
        Account.ParentId,
        Name,
        Phone,
        Email,
        Fax,
        Designation_title__c
      FROM Contact
      WHERE AccountId IN :parentIds AND Email != NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendorParent_releaseMap.get(c.AccountId) !=
        null
        ? contactsByVendorParent_releaseMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(c, (c.Order__c == 1 ? true : false), false)
      );
      contactsByVendorParent_releaseMap.put(
        c.AccountId,
        contactAuxList.clone()
      );
    }

    for (Contact c : [
      SELECT
        Id,
        AccountId,
        Account.Name,
        Order__c,
        Account.ParentId,
        Name,
        Phone,
        Email,
        Fax,
        Designation_title__c
      FROM Contact
      WHERE
        AccountId IN :sendBidRequestMapRelease.keySet()
        AND Email != NULL
        AND Order__c != NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendor_releaseMap.get(c.AccountId) != null
        ? contactsByVendor_releaseMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(
          c,
          (c.Order__c == 1 ? true : false),
          (c.Order__c == 1 ? true : false)
        )
      );
      contactsByVendor_releaseMap.put(c.AccountId, contactAuxList.clone());
    }

    for (Contact c : [
      SELECT
        Id,
        AccountId,
        Account.Name,
        Order__c,
        Account.ParentId,
        Name,
        Phone,
        Email,
        Fax,
        Designation_title__c
      FROM Contact
      WHERE
        AccountId IN :sendBidRequestMapRelease.keySet()
        AND Email != NULL
        AND Order__c = NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendor_releaseMap.get(c.AccountId) != null
        ? contactsByVendor_releaseMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(
          c,
          (c.Order__c == 1 ? true : false),
          (c.Order__c == 1 ? true : false)
        )
      );
      contactsByVendor_releaseMap.put(c.AccountId, contactAuxList.clone());
    }

    String parentId;
    for (String key : sendBidRequestMapRelease.keySet()) {
      parentId = sendBidRequestMapRelease.get(key).Vendor__r.ParentId;
      if (
        contactsByVendor_releaseMap.get(key) == null &&
        (parentId != null &&
        contactsByVendorParent_releaseMap.get(parentId) == null)
      ) {
        //sendBidRequestMapRelease.remove(key);
      } else {
        if (contactsByVendorParent_releaseMap.get(parentId) != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_releaseMap.get(parentId)
          ) {
            contactAuxSelectOptions = contactSelectOption_releaseMap.get(key) !=
              null
              ? contactSelectOption_releaseMap.get(key)
              : new List<SelectOption>();
            contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
            contactSelectOption_releaseMap.put(
              key,
              contactAuxSelectOptions.clone()
            );
          }
        }
        if (contactsByVendor_releaseMap.get(key) != null) {
          for (ContactWrapper cw : contactsByVendor_releaseMap.get(key)) {
            contactAuxSelectOptions = contactSelectOption_releaseMap.get(key) !=
              null
              ? contactSelectOption_releaseMap.get(key)
              : new List<SelectOption>();
            contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
            contactSelectOption_releaseMap.put(
              key,
              contactAuxSelectOptions.clone()
            );
          }
        }
        if (contactsByVendor_releaseMap.get(key) == null)
          contactsByVendor_releaseMap.put(key, new List<ContactWrapper>());
        if (contactSelectOption_releaseMap.get(key) == null)
          contactSelectOption_releaseMap.put(key, new List<SelectOption>());
      }
    }
    for (String key : parentIds) {
      if (contactsByVendorParent_releaseMap.get(key) == null)
        contactsByVendorParent_releaseMap.put(key, new List<ContactWrapper>());
      if (contactSelectOption_releaseMap.get(key) == null)
        contactSelectOption_releaseMap.put(key, new List<SelectOption>());
    }
    Boolean haveDefault;
    for (String key : sendBidRequestMapRelease.keySet()) {
      if (contactsByVendor_releaseMap.get(key) == null)
        contactsByVendor_releaseMap.put(key, new List<ContactWrapper>());
      if (contactSelectOption_releaseMap.get(key) == null)
        contactSelectOption_releaseMap.put(key, new List<SelectOption>());

      if (sendBidRequestMapRelease.get(key).Vendor_Contact__c == null) {
        haveDefault = false;
        parentId = sendBidRequestMapRelease.get(key).Vendor__r.ParentId;
        if (contactsByVendorParent_releaseMap.get(parentId) != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_releaseMap.get(parentId)
          ) {
            if (!haveDefault) {
              cw.selected = true;
              haveDefault = true;
            }
          }
        }
        if (contactsByVendor_releaseMap.get(key) != null) {
          for (ContactWrapper cw : contactsByVendor_releaseMap.get(key)) {
            if (!haveDefault) {
              cw.selected = true;
              haveDefault = true;
            }
          }
        }
      }
    }
    for (String key : contactSelectOption_releaseMap.keySet()) {
      contactSelectOption_releaseSizeMap.put(
        key,
        contactSelectOption_releaseMap.get(key).size()
      );
    }
    sendBidRequestMapReleaseSize = sendBidRequestMapRelease.size();
  }

  /*public void sendEditAllEmail(){
        if(dataids != null && dataids.trim() != ''){
            Set<String> vendorContactIds = new Set<String>();
            for(String d : dataids.split(',')){
                vendorContactIds.add(sendBidRequestMap.get(d).Vendor_Contact__c);
            }
            
            Map<String,Contact> contactMap = new Map<String,Contact>();
            for(Contact c : [SELECT Id, Name, Email FROM Contact WHERE Id IN: vendorContactIds]) contactMap.put(c.Id,c);
            
            List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary GT Coordinator')];
            String owaeId = prodAssocAux.size() > 0 ? verifyWideAddress(prodAssocAux[0].User__r.Email) : null;
            
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
                    if(owaeId != null) mail.setOrgWideEmailAddressId(owaeId);
                    toAddresses = new String[] {contactMap.get(sendBidRequestMap.get(d).Vendor_Contact__c).Email};
                        mail.setToAddresses(toAddresses);
                    if(ccAddresses.size() > 0) mail.setCcAddresses(new List<String>(ccAddresses));
                    if(type_email == 'pdf'){
                        subject = (templatePDF.size() > 0 ? templatePDF[0].Subject.replace('{ProductionName}',sendBidRequestMap.get(d).Production__r.Name)
                                   .replace('{StartDate}',(sendBidRequestMap.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.Start_Date__c.year(),sendBidRequestMap.get(d).GT__r.Start_Date__c.month(),sendBidRequestMap.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{EndDate}',(sendBidRequestMap.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.End_Date__c.year(),sendBidRequestMap.get(d).GT__r.End_Date__c.month(),sendBidRequestMap.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{BidNumber}',sendBidRequestMap.get(d).Name)
                                   : '');
						body = emailBody.replace('{GroundTravelCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '');
                        gAux.Email_Body_Bid_Request__c = null;
                    }else{
                        subject = (templatePDF.size() > 0 ? templatePDF[0].Subject.replace('{ProductionName}',sendBidRequestMap.get(d).Production__r.Name)
                                   .replace('{StartDate}',(sendBidRequestMap.get(d).GT__r.Start_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.Start_Date__c.year(),sendBidRequestMap.get(d).GT__r.Start_Date__c.month(),sendBidRequestMap.get(d).GT__r.Start_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{EndDate}',(sendBidRequestMap.get(d).GT__r.End_Date__c != null ? Datetime.newInstance(sendBidRequestMap.get(d).GT__r.End_Date__c.year(),sendBidRequestMap.get(d).GT__r.End_Date__c.month(),sendBidRequestMap.get(d).GT__r.End_Date__c.day()).format('dd MMMMM yyyy') : ''))
                                   .replace('{BidNumber}',sendBidRequestMap.get(d).Name)
                                   : '');
                        body = emailBody.replace('{GroundTravelCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
                            .replace('{VendorURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Vendor__c + '" target="_blank">' + sendBidRequestMap.get(d).Vendor__r.Name + '</a>')
                            .replace('{BidURL}','<a href="http://' + url + '/' + sendBidRequestMap.get(d).Id + '" target="_blank">http://' + url + '/' + sendBidRequestMap.get(d).Id + '</a>');
                        gAux.Email_Body_Bid_Request_Link__c = null;
                    }
                    mail.setSubject(subject);
                    mail.setHtmlBody(body);
                    myEmails.add(mail);
                }
            }    
            
            insert journalAuxList;
            
            update bidUpdateMap.values();
            
            //if(housingStayView != null && housingStayView.Status_CC__c != 'Contracted'){
            //    hAux.Status_CC__c = 'Bid Request Stage';
            //    housingStayView.Status_CC__c = 'Bid Request Stage';
            //    List<Itinerary__c> itineraryAuxList =  [SELECT Id FROM Itinerary__c WHERE Housing__c =: housingStayViewId AND RecordType.Name = 'Housing Itinerary'];
            //    if(itineraryAuxList.size() > 0) update new Itinerary__c(Id=itineraryAuxList[0].Id,Status__c='Bid Request Stage');
            //}
            //gAux.Bid_Request__c = system.today();
            update gAux;
            
            if(myEmails.size() > 0) Messaging.sendEmail(myEmails);
        }
    }*/

  public void saveAndCloseBidRequest() {
    List<Air__c> template = [
      SELECT Id, Email_Body_Bid_Request__c
      /*, Email_Body_Bid_Request_Link__c*/ FROM Air__c
      WHERE Id = :tripViewid
    ];
    if (template.size() > 0) {
      if (type_email == 'pdf')
        template[0].Email_Body_Bid_Request__c = emailBody;
      //else template[0].Email_Body_Bid_Request_Link__c = emailBody;
      update template[0];
    }
  }

  public void openEditPDF() {
    List<Production_Associations__c> prodAssocAux = [
      SELECT Id, User__r.Name
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :opportunityid
        AND User__c != NULL
        AND Team_Roles__c INCLUDES ('Primary Air Coordinator')
    ];
    if (type_email == 'pdf') {
      List<Air__c> emailTemplate = [
        SELECT Id, Email_Body_Bid_Request__c
        FROM Air__c
        WHERE Id = :tripViewid
      ];
      if (
        emailTemplate.size() > 0 &&
        emailTemplate[0].Email_Body_Bid_Request__c != null
      ) {
        emailBid_body = emailTemplate[0]
          .Email_Body_Bid_Request__c.unescapeHtml4();
      } else {
        List<EmailTemplate> template = [
          SELECT Id, Name, Subject, Body, HTMLValue
          FROM EmailTemplate
          WHERE DeveloperName = 'Air_Bid_Request_All'
        ];
        if (template.size() > 0)
          emailBid_body = template[0].HTMLValue != null
            ? template[0].HTMLValue.unescapeHtml4()
            : '';
      }
    } else {
      /*List<Air__c> housingTemplate = [SELECT Id, Email_Body_Bid_Request_Link__c FROM Air__c WHERE Id =: tripViewid];
            if(housingTemplate.size() > 0 && housingTemplate[0].Email_Body_Bid_Request_Link__c != null){
                emailBid_body = housingTemplate[0].Email_Body_Bid_Request_Link__c.unescapeHtml4();
            }else{
                List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='GT_Bid_Request_Link_All'];
                if(template.size() > 0) emailBid_body = template[0].HTMLValue != null ? template[0].HTMLValue.unescapeHtml4() : '';
            }*/
    }
  }

  public void saveAddContactVendor() {
    messageCreateContact = '';
    try {
      vendorContact.Id = (vendorContact_id != null &&
        vendorContact_id.trim() != ''
        ? vendorContact_id
        : null);
      system.debug(vendorContact);
      upsert vendorContact;
    } catch (DMLException e) {
      messageCreateContact = validateError(e.getMessage());
    }

    Boolean exist = false;
    if (isBidRequestRendered) {
      if (contactsByVendor_bidRequestMap.get(vendorContact.AccountId) != null) {
        for (
          ContactWrapper cw : contactsByVendor_bidRequestMap.get(
            vendorContact.AccountId
          )
        ) {
          if (vendorContact.Id == cw.c.Id)
            exist = true;
        }
      }
      if (!exist) {
        Contact conAux = [
          SELECT
            Id,
            AccountId,
            Account.Name,
            Order__c,
            Account.ParentId,
            Name,
            Phone,
            Email,
            Fax,
            Designation_title__c
          FROM Contact
          WHERE Id = :vendorContact.Id
        ];
        if (contactsByVendor_bidRequestMap.get(vendorContact.AccountId) != null)
          contactsByVendor_bidRequestMap.get(vendorContact.AccountId)
            .add(new ContactWrapper(conAux, false, false));
        if (
          contactSelectOption_bidRequestMap.get(vendorContact.AccountId) != null
        )
          contactSelectOption_bidRequestMap.get(vendorContact.AccountId)
            .add(new SelectOption(conAux.Id, conAux.Name));
      }
    }
    if (isBidReleaseRendered) {
      if (contactsByVendor_releaseMap.get(vendorContact.AccountId) != null) {
        for (
          ContactWrapper cw : contactsByVendor_releaseMap.get(
            vendorContact.AccountId
          )
        ) {
          if (vendorContact.Id == cw.c.Id)
            exist = true;
        }
      }
      if (!exist) {
        Contact conAux = [
          SELECT
            Id,
            AccountId,
            Account.Name,
            Order__c,
            Account.ParentId,
            Name,
            Phone,
            Email,
            Fax,
            Designation_title__c
          FROM Contact
          WHERE Id = :vendorContact.Id
        ];
        if (contactsByVendor_releaseMap.get(vendorContact.AccountId) != null)
          contactsByVendor_releaseMap.get(vendorContact.AccountId)
            .add(new ContactWrapper(conAux, false, false));
        if (contactSelectOption_releaseMap.get(vendorContact.AccountId) != null)
          contactSelectOption_releaseMap.get(vendorContact.AccountId)
            .add(new SelectOption(conAux.Id, conAux.Name));
      }
    }
    //openSendBidRequest();
    //openReleaseBid();
  }

  public void changeContactVendorBid() {
    sendBidRequestMap.get(vendoraccount_actual_id)
      .Vendor_Contact__c = vendorcontact_actual_id;
    for (
      ContactWrapper cw : contactsByVendor_bidRequestMap.get(
        vendoraccount_actual_id
      )
    ) {
      if (vendorcontact_actual_id == cw.c.Id) {
        cw.selected = true;
        cw.disabled = true;
      } else {
        if (cw.selected && cw.disabled) {
          cw.selected = false;
          cw.disabled = false;
        }
      }
    }
    if (
      sendBidRequestMap.get(vendoraccount_actual_id).Vendor__r.ParentId != null
    ) {
      for (
        ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
          sendBidRequestMap.get(vendoraccount_actual_id).Vendor__r.ParentId
        )
      ) {
        if (vendorcontact_actual_id == cw.c.Id) {
          cw.selected = true;
          cw.disabled = true;
        } else {
          if (cw.selected && cw.disabled) {
            cw.selected = false;
            cw.disabled = false;
          }
        }
      }
    }
  }

  public void openSendBidRequest() {
    isBidRequestRendered = true;
    sendBidRequestMapSize = 0;
    sendBidRequestMap = new Map<String, Bid__c>();
    Set<String> parentIds = new Set<String>();
    if (
      sendBidRequestMapSelected == null || sendBidRequestMapSelected.isEmpty()
    )
      sendBidRequestMapSelected = new Map<String, Boolean>();

    for (Bid__c b : [
      SELECT
        Id,
        Name,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.ParentId,
        Vendor_Contact__c,
        Provider__c,
        Provider__r.Name,
        Provider__r.ParentId,
        Status__c,
        Production__c,
        Production__r.Name,
        Air__c,
        Air__r.Departure_Date__c,
        Air__r.Arrival_Date__c,
        Air__r.Return_Date__c,
        Air__r.Number_of_Seats__c,
        Air__r.Departure_City__c,
        Air__r.Arrival_City__c,
        Air__r.Departure_City__r.Airport_Code__c,
        Air__r.Arrival_City__r.Airport_Code__c,
        Air__r.Group_Type__c,
        Air__r.PAX__c
      FROM Bid__c
      WHERE
        Id IN :bidByTripIds
        AND Status__c NOT IN (
          'Contracted',
          'Cancelled',
          'Contracted On Own',
          'Bid Released'
        )
    ]) {
      if (b.Vendor__c != null) {
        sendBidRequestMap.put(b.Vendor__c, b);
        if (sendBidRequestMapSelected.get(b.Vendor__c) == null)
          sendBidRequestMapSelected.put(b.Vendor__c, false);
      }
      if (b.Vendor__c == null && b.Provider__c != null) {
        sendBidRequestMap.put(b.Provider__c, b);
        if (sendBidRequestMapSelected.get(b.Provider__c) == null)
          sendBidRequestMapSelected.put(b.Provider__c, false);
      }
      if (b.Vendor__r.ParentId != null)
        parentIds.add(b.Vendor__r.ParentId);
      if (b.Vendor__c == null && b.Provider__r.ParentId != null)
        parentIds.add(b.Provider__r.ParentId);
    }

    bidSendBidFirstTime = true;
    for (BidWrapper bw : bidsByTripShowList) {
      if (bw.b != null && bw.b.Status__c != 'Unsent')
        bidSendBidFirstTime = false;
    }
    system.debug(sendBidRequestMap);

    contactSelectOption_bidRequestMap = new Map<String, List<SelectOption>>();
    contactSelectOption_bidRequestSizeMap = new Map<String, Integer>();
    contactsByVendor_bidRequestMap = new Map<String, List<ContactWrapper>>();
    contactsByVendorParent_bidRequestMap = new Map<String, List<ContactWrapper>>();
    List<ContactWrapper> contactAuxList;
    List<SelectOption> contactAuxSelectOptions;

    for (Contact c : [
      SELECT
        Id,
        AccountId,
        Account.Name,
        Order__c,
        Account.ParentId,
        Name,
        Phone,
        Email,
        Fax,
        Designation_title__c
      FROM Contact
      WHERE AccountId IN :parentIds AND Email != NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendorParent_bidRequestMap.get(c.AccountId) !=
        null
        ? contactsByVendorParent_bidRequestMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(c, (c.Order__c == 1 ? true : false), false)
      );
      contactsByVendorParent_bidRequestMap.put(
        c.AccountId,
        contactAuxList.clone()
      );
    }

    for (Contact c : [
      SELECT
        Id,
        AccountId,
        Account.Name,
        Order__c,
        Account.ParentId,
        Name,
        Phone,
        Email,
        Fax,
        Designation_title__c
      FROM Contact
      WHERE
        AccountId IN :sendBidRequestMap.keySet()
        AND Email != NULL
        AND Order__c != NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendor_bidRequestMap.get(c.AccountId) != null
        ? contactsByVendor_bidRequestMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(
          c,
          (c.Order__c == 1 ? true : false),
          (c.Order__c == 1 ? true : false)
        )
      );
      contactsByVendor_bidRequestMap.put(c.AccountId, contactAuxList.clone());
      if (
        sendBidRequestMap.get(c.AccountId) != null &&
        sendBidRequestMap.get(c.AccountId).Vendor_Contact__c == null &&
        c.Order__c == 1
      )
        sendBidRequestMap.get(c.AccountId).Vendor_Contact__c = c.Id;
    }

    system.debug(contactsByVendor_bidRequestMap);

    for (Contact c : [
      SELECT
        Id,
        AccountId,
        Account.Name,
        Order__c,
        Account.ParentId,
        Name,
        Phone,
        Email,
        Fax,
        Designation_title__c
      FROM Contact
      WHERE
        AccountId IN :sendBidRequestMap.keySet()
        AND Email != NULL
        AND Order__c = NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendor_bidRequestMap.get(c.AccountId) != null
        ? contactsByVendor_bidRequestMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(
          c,
          (c.Order__c == 1 ? true : false),
          (c.Order__c == 1 ? true : false)
        )
      );
      contactsByVendor_bidRequestMap.put(c.AccountId, contactAuxList.clone());
    }

    String parentId;
    String parentIdProvider;
    for (String key : sendBidRequestMap.keySet()) {
      parentId = sendBidRequestMap.get(key).Vendor__r.ParentId;
      parentIdProvider = sendBidRequestMap.get(key).Provider__r.ParentId;
      if (
        contactsByVendor_bidRequestMap.get(key) == null &&
        contactsByVendorParent_bidRequestMap.get(parentId) == null
      ) {
        //sendBidRequestMap.remove(key);
      } else {
        if (contactsByVendorParent_bidRequestMap.get(parentId) != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
              parentId
            )
          ) {
            contactAuxSelectOptions = contactSelectOption_bidRequestMap.get(
                key
              ) != null
              ? contactSelectOption_bidRequestMap.get(key)
              : new List<SelectOption>();
            contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
            contactSelectOption_bidRequestMap.put(
              key,
              contactAuxSelectOptions.clone()
            );
          }
        }
        if (
          contactsByVendorParent_bidRequestMap.get(parentIdProvider) != null
        ) {
          for (
            ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
              parentIdProvider
            )
          ) {
            contactAuxSelectOptions = contactSelectOption_bidRequestMap.get(
                key
              ) != null
              ? contactSelectOption_bidRequestMap.get(key)
              : new List<SelectOption>();
            contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
            contactSelectOption_bidRequestMap.put(
              key,
              contactAuxSelectOptions.clone()
            );
          }
        }
        if (contactsByVendor_bidRequestMap.get(key) != null) {
          for (ContactWrapper cw : contactsByVendor_bidRequestMap.get(key)) {
            contactAuxSelectOptions = contactSelectOption_bidRequestMap.get(
                key
              ) != null
              ? contactSelectOption_bidRequestMap.get(key)
              : new List<SelectOption>();
            contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
            contactSelectOption_bidRequestMap.put(
              key,
              contactAuxSelectOptions.clone()
            );
          }
        }
        if (contactsByVendor_bidRequestMap.get(key) == null)
          contactsByVendor_bidRequestMap.put(key, new List<ContactWrapper>());
        if (contactSelectOption_bidRequestMap.get(key) == null)
          contactSelectOption_bidRequestMap.put(key, new List<SelectOption>());
      }
    }
    for (String key : parentIds) {
      if (contactsByVendorParent_bidRequestMap.get(key) == null)
        contactsByVendorParent_bidRequestMap.put(
          key,
          new List<ContactWrapper>()
        );
      if (contactSelectOption_bidRequestMap.get(key) == null)
        contactSelectOption_bidRequestMap.put(key, new List<SelectOption>());
    }
    Boolean haveDefault;
    for (String key : sendBidRequestMap.keySet()) {
      if (contactsByVendor_bidRequestMap.get(key) == null)
        contactsByVendor_bidRequestMap.put(key, new List<ContactWrapper>());
      if (contactSelectOption_bidRequestMap.get(key) == null)
        contactSelectOption_bidRequestMap.put(key, new List<SelectOption>());

      if (sendBidRequestMap.get(key).Vendor_Contact__c == null) {
        haveDefault = false;
        parentId = sendBidRequestMap.get(key).Vendor__r.ParentId;
        parentIdProvider = sendBidRequestMap.get(key).Provider__r.ParentId;
        if (contactsByVendorParent_bidRequestMap.get(parentId) != null) {
          for (
            ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
              parentId
            )
          ) {
            if (!haveDefault) {
              cw.selected = true;
              haveDefault = true;
            }
          }
        }
        if (
          contactsByVendorParent_bidRequestMap.get(parentIdProvider) != null
        ) {
          for (
            ContactWrapper cw : contactsByVendorParent_bidRequestMap.get(
              parentIdProvider
            )
          ) {
            if (!haveDefault) {
              cw.selected = true;
              haveDefault = true;
            }
          }
        }
        if (contactsByVendor_bidRequestMap.get(key) != null) {
          for (ContactWrapper cw : contactsByVendor_bidRequestMap.get(key)) {
            if (!haveDefault) {
              cw.selected = true;
              haveDefault = true;
            }
          }
        }
      }
    }

    for (String key : contactSelectOption_bidRequestMap.keySet()) {
      contactSelectOption_bidRequestSizeMap.put(
        key,
        contactSelectOption_bidRequestMap.get(key).size()
      );
    }

    sendBidRequestMapSize = sendBidRequestMap.size();

    List<Itinerary__c> itineraries = [
      SELECT Id
      FROM Itinerary__c
      WHERE Air__c = :tripViewId AND RecordType.DeveloperName = 'Air_Itinerary'
    ];
    itineraryId = !itineraries.isEmpty() ? itineraries[0].Id : null;

    //getDocumentsByProduction();
    /**
     *  @Conga: Update for Conga.
     */
    congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
    for (APXTConga4__Conga_Merge_Query__c congaQuery : [
      SELECT Id, APXTConga4__Name__c
      FROM APXTConga4__Conga_Merge_Query__c
      WHERE
        APXTConga4__Name__c IN (
          'Air - AirCharterBidById',
          'Air - BidItinerarySegmentsByBidId',
          'Air - ProductionAssociationsByOppId'
        )
    ])
      congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
    sendBidRequest_congaQueriesJson = JSON.serialize(congaQueriesMap);
    Map<String, APXTConga4__Conga_Template__c> congaTemplatesMap = new Map<String, APXTConga4__Conga_Template__c>();
    for (APXTConga4__Conga_Template__c congaTemplate : [
      SELECT Id, APXTConga4__Name__c
      FROM APXTConga4__Conga_Template__c
      WHERE APXTConga4__Name__c IN ('Air - Air Charter Bid')
    ])
      congaTemplatesMap.put(congaTemplate.APXTConga4__Name__c, congaTemplate);
    sendBidRequest_congaTemplateId1 = congaTemplatesMap.containsKey(
        'Air - Air Charter Bid'
      )
      ? congaTemplatesMap.get('Air - Air Charter Bid').id
      : null;
    List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [
      SELECT Id, APXTConga4__Subject__c
      FROM APXTConga4__Conga_Email_Template__c
      WHERE APXTConga4__Name__c = 'Air - Air Charter Bid Request'
    ];
    sendBidRequest_congaEmailTemplateId = !congaEmailTemplates.isEmpty()
      ? congaEmailTemplates[0].id
      : null;
    if (
      !congaEmailTemplates.isEmpty() &&
      String.isNotBlank(congaEmailTemplates[0].APXTConga4__Subject__c)
    )
      sendBidRequest_congaEmailSubject = congaEmailTemplates[0]
        .APXTConga4__Subject__c.replace('{ProductionName}', opportunity.Name)
        .replace(
          '{DepDate}',
          tripView.Departure_Date__c != null
            ? Datetime.newInstance(
                  tripView.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('dd MMMMM yyyy')
            : ''
        )
        .replace(
          '{DepartureCity}',
          String.isNotBlank(tripView.Departure_City__r.Airport_Code__c)
            ? tripView.Departure_City__r.Airport_Code__c
            : ''
        )
        .replace(
          '{ArrivalCity}',
          String.isNotBlank(tripView.Arrival_City__r.Airport_Code__c)
            ? tripView.Arrival_City__r.Airport_Code__c
            : ''
        );
    else
      sendBidRequest_congaEmailSubject =
        'New group flight request - ' +
        opportunity.Name +
        ' - ' +
        (tripView.Departure_Date__c != null
          ? Datetime.newInstance(
                tripView.Departure_Date__c,
                Time.newInstance(0, 0, 0, 0)
              )
              .format('dd MMMMM yyyy')
          : '') +
        ' ' +
        (String.isNotBlank(tripView.Departure_City__r.Airport_Code__c)
          ? tripView.Departure_City__r.Airport_Code__c
          : '') +
        ' - ' +
        (String.isNotBlank(tripView.Arrival_City__r.Airport_Code__c)
          ? tripView.Arrival_City__r.Airport_Code__c
          : '');
    /**
     *  @/Conga
     */
  }

  public void createBidRequest() {
    if (
      opportunityId != null &&
      opportunityId != '' &&
      selectedVendors != null &&
      selectedVendors != '' &&
      selectedTrips != null &&
      selectedTrips != ''
    ) {
      Set<String> accountIds = new Set<String>();
      for (String sv : selectedVendors.split(',')) {
        if (sv.trim() != '') {
          for (Account vw : searchVendorList) {
            if (vw.Id != null && sv.trim() == vw.Id) {
              accountIds.add(vw.Id);
            }
          }
        }
      }

      Map<String, String> accountContactMap = new Map<String, String>();
      for (Contact c : [
        SELECT Id, AccountId, Order__c
        FROM Contact
        WHERE AccountId IN :accountIds AND Order__c = 1
      ]) {
        accountContactMap.put(c.AccountId, c.Id);
      }

      Map<String, Account> accMap = new Map<String, Account>();
      for (Account acc : [
        SELECT Id, ParentId
        FROM Account
        WHERE Id IN :accountIds
      ]) {
        if (acc.ParentId != null) {
          accountIds.add(acc.ParentId);
          accMap.put(acc.Id, acc);
        }
      }

      List<Bid__c> bidList = new List<Bid__c>();
      Bid__c b;
      Set<String> tripSelectedIds = new Set<String>();
      for (String tv : selectedTrips.split(',')) {
        if (tv.trim() != '')
          tripSelectedIds.add(tv.trim());
      }

      Map<String, String> bidExistMap = new Map<String, String>();
      for (Bid__c bExist : [
        SELECT Id, Vendor__c, Air__c
        FROM Bid__c
        WHERE Air__c IN :tripSelectedIds AND Vendor__c != NULL
      ]) {
        bidExistMap.put(bExist.Air__c + '-' + bExist.Vendor__c, bExist.Id);
      }

      //Map<String,Air__c> airExistMap = new Map<String,Air__c>();
      //for(Air__c aExist : [SELECT Id, Start_City__c FROM Air__c WHERE Id IN: tripSelectedIds]) airExistMap.put(aExist.Id,aExist);

      Set<String> tripCreateIds = new Set<String>();
      for (String tv : selectedTrips.split(',')) {
        if (tv.trim() != '') {
          for (String sv : selectedVendors.split(',')) {
            if (sv.trim() != '') {
              if (bidExistMap.get(tv.trim() + '-' + sv.trim()) == null) {
                tripCreateIds.add(tv.trim());
                for (Account vw : searchVendorList) {
                  if (vw.Id != null && sv.trim() == vw.Id) {
                    b = new Bid__c(
                      RecordTypeId = bid_AirBidRT,
                      Production__c = opportunityId,
                      Air__c = tv.trim(),
                      Vendor__c = vw.Id,
                      //City__c = gtExistMap.get(tv.trim()) != null ? gtExistMap.get(tv.trim()).Start_City__c : null,
                      CurrencyIsoCode = vw.CurrencyIsoCode,
                      Status__c = 'Unsent',
                      Vendor_Contact__c = accountContactMap.get(vw.Id) != null
                        ? accountContactMap.get(vw.Id)
                        : null
                    );
                    bidList.add(b);
                  }
                }
              }
            }
          }
        }
      }

      bidsCreated = 0;
      if (bidList.size() > 0) {
        insert bidList;
        bidsCreated = bidList.size();

        Map<String, Bid__c> bidMap = new Map<String, Bid__c>();
        for (Bid__c bd : [
          SELECT
            Id,
            Air__r.Trip_Type__c,
            Air__r.Group_Type__c,
            Air__r.Description__c,
            Air__r.PAX__c
          FROM Bid__c
          WHERE Id IN :bidList
        ])
          bidMap.put(bd.Id, bd);

        List<Air__c> segmentsAux;
        Map<String, String> descriptionMap = new Map<String, String>();
        Map<String, List<Air__c>> segmentMap = new Map<String, List<Air__c>>();
        String segments;
        for (Air__c segment : [
          SELECT
            Id,
            Trip_Type__c,
            RecordTypeId,
            Group_Type__c,
            Departure_Date__c,
            Departure_City__c,
            Arrival_City__c,
            Return_Date__c,
            PAX__c,
            Air_Preferences__c,
            Trace_Date__c,
            Decision_Due_Date__c,
            Class__c,
            Return_Arrival_City__c,
            Return_Departure_City__c,
            Air_Charter__c,
            Air_Type__c,
            Air_Trip_Details__c,
            Arrival_Date__c,
            Departure_City__r.Airport_Code__c,
            Departure_City__r.Name,
            Departure_City__r.City__c,
            Departure_City__r.City__r.Name,
            Arrival_City__r.Airport_Code__c,
            Arrival_City__r.Name,
            Arrival_City__r.City__c,
            Arrival_City__r.City__r.Name,
            Dep_Time__c,
            Dep_Time_Text__c,
            Arr_Time__c,
            Arr_Time_Text__c,
            Segment_Notes__c
          FROM Air__c
          WHERE
            Air_Trip_Details__c IN :tripCreateIds
            AND RecordType.DeveloperName = 'Air_Segments'
        ]) {
          segmentsAux = segmentMap.get(segment.Air_Trip_Details__c) != null
            ? segmentMap.get(segment.Air_Trip_Details__c)
            : new List<Air__c>();
          segmentsAux.add(segment);
          segmentMap.put(segment.Air_Trip_Details__c, segmentsAux.clone());

          segments =
            (segment.Departure_City__r.Airport_Code__c != null
              ? segment.Departure_City__r.Airport_Code__c + ' - '
              : '') +
            (segment.Arrival_City__r.Airport_Code__c != null
              ? segment.Arrival_City__r.Airport_Code__c
              : '');
          descriptionMap.put(
            segment.Air_Trip_Details__c,
            descriptionMap.get(segment.Air_Trip_Details__c) != null
              ? descriptionMap.get(segment.Air_Trip_Details__c) +
                ', ' +
                segments
              : segments
          );
        }

        List<Air__c> aircraftAux;
        Map<String, List<Air__c>> aircraftMap = new Map<String, List<Air__c>>();
        for (Air__c aircraft : [
          SELECT
            Id,
            Production__c,
            RecordTypeId,
            RecordType.Name,
            Bid_Aircraft__c,
            Aircraft_Type__c,
            economy_seats__c,
            Cargo_capacity__c,
            Seat_pitch__c,
            Airline__c,
            Airline__r.Name,
            Positioning_from_time__c,
            Air_Charter_Trip_Contents__c,
            Air_Crafts_Details__c
          FROM Air__c
          WHERE
            RecordType.DeveloperName = 'Air_Crafts'
            AND Air_Crafts_Details__c IN :tripCreateIds
            AND Bid_Aircraft__c = NULL
        ]) {
          aircraftAux = aircraftMap.get(aircraft.Air_Crafts_Details__c) != null
            ? aircraftMap.get(aircraft.Air_Crafts_Details__c)
            : new List<Air__c>();
          aircraftAux.add(aircraft);
          aircraftMap.put(aircraft.Air_Crafts_Details__c, aircraftAux.clone());
        }

        List<Concessions__c> concessionAux;
        Map<String, List<Concessions__c>> concessionMap = new Map<String, List<Concessions__c>>();
        for (Concessions__c co : [
          SELECT
            Id,
            Concessions_Requested__c,
            Concession_Type__c,
            Notes__c,
            Create_in_Bid__c,
            Air__c
          FROM Concessions__c
          WHERE Air__c IN :tripCreateIds AND Create_in_Bid__c = TRUE
          ORDER BY CreatedDate DESC
        ]) {
          concessionAux = concessionMap.get(co.Air__c) != null
            ? concessionMap.get(co.Air__c)
            : new List<Concessions__c>();
          concessionAux.add(co);
          concessionMap.put(co.Air__c, concessionAux.clone());
        }

        Air__c newItinerary;
        Map<String, Air__c> itineraryMap = new Map<String, Air__c>();
        for (Bid__c bid : bidList) {
          newItinerary = new Air__c(
            Production__c = opportunityId,
            Bid_Itinerary__c = bid.Id,
            RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
              .get('Air_Itinerary_Details')
              .getRecordTypeId(),
            Trip_Type__c = bidMap.get(bid.Id).Air__r.Trip_Type__c,
            Group_Type__c = bidMap.get(bid.Id).Air__r.Group_Type__c,
            Description__c = descriptionMap.get(bid.Air__c) != null
              ? descriptionMap.get(bid.Air__c)
              : null,
            PAX__c = bidMap.get(bid.Id).Air__r.PAX__c
          );
          itineraryMap.put(bid.Id, newItinerary);
        }
        insert itineraryMap.values();

        Air__c newSegment;
        Air__c newAircraft;
        Concessions__c newConcession;
        segmentsAux = new List<Air__c>();
        concessionAux = new List<Concessions__c>();
        for (Bid__c bid : bidList) {
          if (segmentMap.get(bid.Air__c) != null) {
            for (Air__c segment : segmentMap.get(bid.Air__c)) {
              newSegment = segment.clone();
              newSegment.Production__c = opportunityId;
              newSegment.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
                .get('Air_Segments')
                .getRecordTypeId();
              newSegment.Air_Itinerary_Details__c = itineraryMap.get(bid.Id).Id;
              newSegment.Air_Trip_Details__c = null;
              segmentsAux.add(newSegment);
            }
          }
          if (aircraftMap.get(bid.Air__c) != null) {
            for (Air__c airc : aircraftMap.get(bid.Air__c)) {
              newAircraft = airc.clone();
              newAircraft.Production__c = opportunityId;
              newAircraft.Bid_Aircraft__c = b.Id;
              newAircraft.Air_Crafts_Details__c = null;
              newAircraft.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
                .get('Air_Crafts')
                .getRecordTypeId();
              segmentsAux.add(newAircraft);
            }
          }
          if (concessionMap.get(bid.Air__c) != null) {
            for (Concessions__c conc : concessionMap.get(bid.Air__c)) {
              newConcession = conc.clone();
              newConcession.Bid__c = bid.Id;
              newConcession.Air__c = null;
              newConcession.Production__c = opportunityId;
              newConcession.Concession_Type__c = 'Air';
              concessionAux.add(newConcession);
            }
          }
        }
        if (segmentsAux.size() > 0)
          insert segmentsAux;
        if (concessionAux.size() > 0)
          insert concessionAux;
      }

      getBidsByTrip();
    }
  }

  public void searchVendor() {
    vendorFilter = new Account();
    //VendorWrapper.orderFieldVendor = orderFieldVendor;
    detailId = null;
    String strQuery = '';
    searchVendorList = new List<Account>();

    strQuery =
      'SELECT Id, Name, Flag_icon__c, Airline_Code__c, Service_Types__c, City__c, City__r.Name, Status__c, CreatedDate, ShippingPostalCode, Preferred_formula__c, CurrencyIsoCode, ShippingState, ShippingStreet, ShippingCountry, ShippingCity ' +
      ' FROM Account' +
      ' WHERE';
    if (tripView.Air_Charter__c == true)
      strQuery += ' RecordType.DeveloperName IN (\'Air_Charter\')';
    else
      strQuery += ' RecordType.DeveloperName IN (\'Airline_Vendor\')';
    system.debug(searchvendor_status);
    system.debug(searchvendor_word);
    system.debug(searchvendor_type);
    if (searchvendor_status != null && searchvendor_status != 'All') {
      strQuery += ' AND Status__c =: searchvendor_status';
    }
    if (searchvendor_word != null && searchvendor_word != '') {
      searchvendor_word = '%' + searchvendor_word + '%';
      strQuery += ' AND (Name LIKE: searchvendor_word OR Airline_Code__c LIKE: searchvendor_word)';
    }
    if (searchvendor_type != 'multiple')
      strQuery += ' AND Id NOT IN: vendorNotSelectedIds';

    if (orderCheckVendor) {
      if (orderChangeVendor)
        orderOrientationVendor = 'ASC';
      else {
        if (orderOrientationVendor == 'ASC')
          orderOrientationVendor = 'DESC';
        else
          orderOrientationVendor = 'ASC';
      }
    }
    orderCheckVendor = false;

    Integer totalRecordsVendor = Database.countQuery(
      'Select count() from Account WHERE' + strQuery.substringAfter('WHERE')
    );
    totalPagesVendor = totalRecordsVendor != null &&
      totalRecordsVendor == 0
      ? 1
      : Integer.valueOf(
          (totalRecordsVendor / Decimal.valueOf(limitVendor))
            .round(System.RoundingMode.UP)
        );
    if (String.isBlank(searchTypeVendor)) {
      strQuery +=
        ' ORDER BY ' +
        orderFieldVendor +
        ' ' +
        orderOrientationVendor +
        ' NULLS LAST' +
        ', Id LIMIT :limitVendor';
      searchVendorList = Database.query(strQuery);
      offsetVendor = null;
    } else {
      if (searchTypeVendor == 'next') {
        offsetVendor = (offsetVendor != null ? offsetVendor : 0) + limitVendor;
        strQuery +=
          ' AND (' +
          orderFieldVendor +
          (orderOrientationVendor == 'ASC' ? ' >' : ' <') +
          ':lastValueOfSortedFieldVendor OR (' +
          orderFieldVendor +
          ' =:lastValueOfSortedFieldVendor AND Id >:lastId)) ORDER BY ' +
          orderFieldVendor +
          ' ' +
          orderOrientationVendor +
          ' NULLS LAST' +
          ', Id LIMIT :limitVendor';
        searchVendorList = Database.query(strQuery);
      } else if (searchTypeVendor == 'previous') {
        offsetVendor = (offsetVendor != null ? offsetVendor : 0) - limitVendor;
        strQuery +=
          ' AND (' +
          orderFieldVendor +
          (orderOrientationVendor == 'ASC' ? ' <' : ' >') +
          ':firstValueOfSortedFieldVendor OR (' +
          orderFieldVendor +
          ' =:firstValueOfSortedFieldVendor AND Id <:firstId)) ORDER BY ' +
          orderFieldVendor +
          ' ' +
          (orderOrientationVendor == 'ASC' ? 'DESC' : 'ASC') +
          ' NULLS LAST' +
          ', Id LIMIT :limitVendor';
        searchVendorList = Database.query(strQuery);
        List<Account> vendorsAir = new List<Account>();
        for (Integer i = searchVendorList.size() - 1; i >= 0; i--)
          vendorsAir.add(searchVendorList[i]);
        searchVendorList = vendorsAir;
      } else if (searchTypeVendor == 'first') {
        offsetVendor = null;
        strQuery +=
          ' ORDER BY ' +
          orderFieldVendor +
          ' ' +
          orderOrientationVendor +
          ' NULLS LAST' +
          ', Id LIMIT :limitVendor';
        searchVendorList = Database.query(strQuery);
      } else if (searchTypeVendor == 'last') {
        offsetVendor =
          limitVendor *
          (Integer.valueOf(
            (totalRecordsVendor / Decimal.valueOf(limitVendor))
              .round(System.RoundingMode.CEILING)
          ) - 1);
        strQuery +=
          ' ORDER BY ' +
          orderFieldVendor +
          ' ' +
          (orderOrientationVendor == 'ASC' ? 'DESC' : 'ASC') +
          ' NULLS LAST' +
          ', Id LIMIT ' +
          String.valueOf(totalRecordsVendor - offsetVendor);
        searchVendorList = Database.query(strQuery);
        List<Account> vendorsAir = new List<Account>();
        for (Integer i = searchVendorList.size() - 1; i >= 0; i--)
          vendorsAir.add(searchVendorList[i]);
        searchVendorList = vendorsAir;
      }
    }
    firstIdVendor = !searchVendorList.isEmpty() ? searchVendorList[0].Id : null;
    lastIdVendor = !searchVendorList.isEmpty()
      ? searchVendorList[searchVendorList.size() - 1].Id
      : null;
    firstValueOfSortedFieldVendor = !searchVendorList.isEmpty()
      ? searchVendorList[0].get(orderFieldVendor)
      : null;
    lastValueOfSortedFieldVendor = !searchVendorList.isEmpty()
      ? searchVendorList[searchVendorList.size() - 1].get(orderFieldVendor)
      : null;
    searchTypeVendor = null;
  }

  public void saveEditBid() {
    if (bid_id != null && bid_id.trim() != '') {
      Bid__c bidTemp;
      Integer orderOld;
      Integer orderNow;
      for (BidWrapper bw : bidsByTripShowList) {
        if (bw.b.Id == bid_id) {
          orderOld = Integer.valueOf(bw.b.Options__c);
          bw.b.Options__c = (bid_option != null
            ? (bid_option != 0 ? bid_option : null)
            : null);
          Bid__c b = new Bid__c(
            Id = bid_id,
            Internal_Notes__c = bid_notes,
            Options__c = (bid_option != null
              ? (bid_option != 0 ? bid_option : null)
              : null)
          );
          orderNow = Integer.valueOf(b.Options__c);
          bw.option_original = b.Options__c != null ? b.Options__c : 999999;
          bw.options = Integer.valueOf(b.Options__c);
          if (b.Options__c != null) {
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
      for (BidWrapper bw : bidsByTripShowList) {
        //system.debug('------');
        //system.debug('bw.b.Options__c: ' + bw.b.Options__c);
        if (bw.b.Options__c != null) {
          if (bw.b.Id != bid_id) {
            //system.debug('i: '+i);
            //system.debug('bw.option_original: '+ bw.option_original);
            if (i == orderNow) {
              if (orderOld != null && bw.option_original >= orderOld) {
                bw.b.Options__c = i - 1;
                //system.debug('enter 1');
              } else {
                bw.b.Options__c = i + 1;
                //system.debug('enter 2');
              }
              //system.debug('new: '+bw.b.Options__c);
              bidUpdateList.add(bw.b);
            } else {
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
      if (!bidUpdateList.isEmpty())
        update bidUpdateList;
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

  public void getBidsByTrip() {
    if (
      opportunityId != null &&
      opportunityId != '' &&
      tripViewId != null &&
      tripViewId != ''
    ) {
      /*if(refreshBidData) tripBidNumber = null;
       else refreshBidData = true;*/
      tripview_option = 0;
      BidWrapper.orderFieldBid = orderFieldBid;
      totalRecsBids = 0;
      OffsetSizeBids = 0;
      bidsByTripShowList = new List<BidWrapper>();
      bidByTripIds = new List<String>();
      vendorNotSelectedIds = new Set<String>();
      bidDataDecision = new Bid__c();
      bidReleaseActive = false;
      String strQuery =
        'SELECT Id, Air__c, Vendor__c, Vendor__r.Name, Vendor__r.Flag_icon__c, Status__c, Options__c, CreatedDate, Locked__c, Internal_notes__c, Vendor_Contact__c, Vendor_Contact__r.Name,' +
        ' Vendor__r.ShippingStreet, Vendor__r.ShippingState, Vendor__r.ShippingCity, Vendor__r.ShippingCountry, Vendor__r.ShippingPostalCode, Production__c, Air__r.PAX__c, No_Bid_reason__c, ' +
        ' Vendor__r.BillingStreet, Vendor__r.BillingState, Vendor__r.BillingCity, Vendor__r.BillingCountry, Vendor__r.BillingPostalCode, Air__r.Status__c, Air__r.Status_Previous__c, Status_Previous__c' +
        ' FROM Bid__c WHERE Air__c =: tripViewId and Status__c != \'Deactivated Bid\'';
      bAuxWrapper = new List<BidWrapper>();
      vendorsJson = '[]';
      Map<String, String> vendorMap = new Map<String, String>();
      BidWrapper bwAux;
      for (Bid__c b : Database.query(strQuery)) {
        bidByTripIds.add(b.Id);
        if (b.Options__c != null && b.Options__c > tripview_option)
          tripview_option = Integer.valueOf(b.Options__c);
        if (b.Vendor__c != null) {
          vendorNotSelectedIds.add(b.Vendor__c);
          vendorMap.put(b.Vendor__c, b.Vendor__r.Name);
        }
        if (b.Status__c == 'Contracted')
          bidDataDecision = b;
        if (b.Status__c != 'Unsent')
          bidReleaseActive = true;
        bwAux = new BidWrapper(
          b,
          b.Vendor__r.Flag_icon__c,
          b.Vendor__c != null ? b.Vendor__r.Name : '',
          b.Vendor_Contact__c != null ? b.Vendor_Contact__r.Name : '',
          b.Status__c,
          0,
          0,
          b.Internal_notes__c != null ? b.Internal_notes__c : '',
          (b.Options__c != null ? b.Options__c : 999999),
          b.CreatedDate.date(),
          (b.Options__c != null ? b.Options__c : 999999)
        );
        bwAux.orderfix = (b.Status__c != 'No Availability'
          ? (b.Options__c != null
              ? String.valueOf(b.Options__c)
              : 'W' + b.Status__c)
          : 'Z' + (b.Options__c != null ? String.valueOf(b.Options__c) : ''));
        //bAuxWrapper.add(bwAux);
        bidsByTripShowList.add(bwAux);
      }
      tripview_option++;
      system.debug(tripview_option);

      /*Map<String,Decimal> ratesMap = new Map<String,Decimal>();
            for(Revenue__c r : [Select id, Base_Cost__c, Commission__c, Rate__c, Gratuity__c, Total_Price__c, CurrencyIsoCode, Bid__c from Revenue__c where Bid__c IN: bidByTripIds and RecordType.DeveloperName = 'Ground_Rate_Travel_Commission' order by createdDate ASC])
                ratesMap.put(r.Bid__c,r.Total_Price__c);*/

      bidRevenueMap = new Map<String, List<Revenue__c>>();
      List<Revenue__c> revenueListAux;
      system.debug(bidByTripIds);
      getSymbol();
      for (Revenue__c r : [
        SELECT Id, Bid__c, Total_Price__c, of_seats__c, Total_Price_Currency__c
        FROM Revenue__c
        WHERE
          Bid__c IN :bidByTripIds
          AND RecordType.DeveloperName = 'Air_Rate_Commission'
        ORDER BY Total_Price__c ASC, of_seats__c ASC
      ]) {
        revenueListAux = bidRevenueMap.get(r.Bid__c) != null
          ? bidRevenueMap.get(r.Bid__c)
          : new List<Revenue__c>();
        revenueListAux.add(r);
        bidRevenueMap.put(r.Bid__c, revenueListAux.clone());
      }
      symbolMap.put(null, '');
      system.debug(bidRevenueMap);

      List<wrapperVendor> wrapperVendorList = new List<wrapperVendor>();
      for (String vk : vendorMap.keySet())
        wrapperVendorList.add(new wrapperVendor(vk, vendorMap.get(vk)));
      vendorsJson = JSON.serialize(wrapperVendorList);

      if (orderOrientationBid == null) {
        orderOrientationBid = 'ASC';
        BidWrapper.orderOrientationBid = 'ASC';
      } else
        BidWrapper.orderOrientationBid = orderOrientationBid;
      if (orderCheckBid) {
        if (orderChangeBid) {
          orderOrientationBid = 'ASC';
          BidWrapper.orderOrientationBid = 'ASC';
        } else {
          if (orderOrientationBid == 'ASC') {
            orderOrientationBid = 'DESC';
            BidWrapper.orderOrientationBid = 'DESC';
          } else {
            orderOrientationBid = 'ASC';
            BidWrapper.orderOrientationBid = 'ASC';
          }
        }
      }

      totalRecsBids = bidsByTripShowList.size();
      Integer p = 1;
      Integer j;
      bidDataMap = new Map<Integer, BidWrapper>();

      for (BidWrapper bw : bidsByTripShowList) {
        if (bidRevenueMap.get(bw.b.Id) == null) {
          bidRevenueMap.put(bw.b.Id, new List<Revenue__c>());
        } else {
          bw.fare = bw.b.Status__c != 'No Availability'
            ? (bidRevenueMap.get(bw.b.Id) != null &&
                bidRevenueMap.get(bw.b.Id)[0].Total_Price__c != null
                ? bidRevenueMap.get(bw.b.Id)[0].Total_Price__c
                : 0)
            : 0;
          bw.currency_code = bidRevenueMap.get(bw.b.Id)[0]
            .Total_Price_Currency__c;
          bw.pax = bidRevenueMap.get(bw.b.Id) != null &&
            bidRevenueMap.get(bw.b.Id)[0].of_seats__c != null
            ? bidRevenueMap.get(bw.b.Id)[0].of_seats__c
            : 0;
          j = 1;
          revenueListAux = new List<Revenue__c>();
          for (Revenue__c r : bidRevenueMap.get(bw.b.Id)) {
            if (j > 1)
              revenueListAux.add(r);
            j++;
          }
          bidRevenueMap.put(bw.b.Id, revenueListAux.clone());
        }
        bw.numberz = p;
        bidDataMap.put(p, bw);
        if (dataBidIdsearch != null && dataBidIdsearch == bw.b.Id) {
          system.debug(p);
          tripBidNumber = p;
        }
        p++;
      }
      bidsByTripShowList.sort();
      dataBidIdsearch = null;
      gtDashboard.bidDataMap = bidDataMap;
      /*if((OffsetSizeBids + LimitSizeBids) <= totalRecsBids){
                for(Integer i = 0; i<LimitSizeBids; i++)
                    bidsByTripShowList.add(bAuxWrapper.get(i));
                
            }else{
                for(Integer i=0;i<totalRecsBids;i++)
                    bidsByTripShowList.add(bAuxWrapper.get(i));
            }*/

      //if(refreshBidData){
      //getConcessionsByTrip();
      //getAircraftsByTrip();
      //getSubStripByTrip();
      //}

      //getprevBids();
      //getnxtBids();
    }
  }

  public void createJournal() {
    if (
      journalIdActual != null &&
      journalIdActual != '' &&
      journalView.Id != null
    ) {
      upsert new Journal__c(
        Id = (journalChildIdActual != '' ? journalChildIdActual : null),
        RecordTypeId = journal_tripJournalRT,
        Parent_Journal__c = journalIdActual,
        Journal_Entry__c = newJournalChildEntry,
        Production__c = journalView.Production__c,
        Air__c = journalView.Air__c
      );
    }
    journalIdActual = null;
    journalChildIdActual = null;
    newJournalChildEntry = null;
    searchTripJournalsByGT();
  }

  public void viewReplyJournal() {
    journalView = new Journal__c();
    journalChildView = new Journal__c();
    if (journalIdActual != null && journalIdActual != '')
      journalView = [
        SELECT
          Id,
          Name,
          Journal_Entry__c,
          CreatedDate,
          CreatedBy.Name,
          Production__c,
          Air__c
        FROM Journal__c
        WHERE Id = :journalIdActual
      ];
    if (journalChildIdActual != null && journalChildIdActual != '')
      journalChildView = [
        SELECT
          Id,
          Name,
          Journal_Entry__c,
          CreatedDate,
          CreatedBy.Name,
          Production__c,
          Air__c
        FROM Journal__c
        WHERE Id = :journalChildIdActual
      ];
  }

  public void searchTripJournalsByGT() {
    if (tripViewId != null && tripViewId != '') {
      journalByTripList = new List<Journal__c>();
      journalByTripMap = new Map<String, List<Journal__c>>();
      List<Journal__c> journalListAux;
      system.debug(tripViewId);
      String strQuery = 'SELECT Id, Name, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, G__c, Parent_Journal__c, Bid__c FROM Journal__c WHERE Air__c =: tripViewId AND Parent_Journal__c = NULL';
      if (checkIssue && checkSales) {
        strQuery += ' AND (Issue__c = true OR Sales__C = true)';
      } else {
        if (checkIssue != null && checkIssue)
          strQuery += ' AND Issue__c = true';
        if (checkSales != null && checkSales)
          strQuery += ' AND Sales__c = true';
      }
      strQuery += ' ORDER BY CreatedDate DESC';

      Set<String> journalParentIds = new Set<String>();
      Boolean wordSearch;
      for (Journal__c j : Database.query(strQuery)) {
        wordSearch = true;
        if (
          tripJournalSearch != null &&
          tripJournalSearch != '' &&
          j.Journal_Entry__c != null &&
          !j.Journal_Entry__c.containsIgnoreCase(tripJournalSearch)
        )
          wordSearch = false;
        if (wordSearch) {
          journalParentIds.add(j.Id);
          journalByTripList.add(j);
        }
      }

      strQuery = 'SELECT Id, Name, CreatedDate, CreatedById, Issue__c, Sales__c, Journal_Entry__c, CreatedBy.Name, G__c, Parent_Journal__c, Bid__c FROM Journal__c WHERE Air__c =: tripViewId AND Parent_Journal__c IN: journalParentIds ORDER BY CreatedDate DESC';
      system.debug(tripViewId);
      system.debug(journalParentIds);
      for (Journal__c j : Database.query(strQuery)) {
        wordSearch = true;
        if (
          tripJournalSearch != null &&
          tripJournalSearch != '' &&
          j.Journal_Entry__c != null &&
          !j.Journal_Entry__c.containsIgnoreCase(tripJournalSearch)
        )
          wordSearch = false;
        if (wordSearch) {
          journalListAux = journalByTripMap.get(j.Parent_Journal__c) != null
            ? journalByTripMap.get(j.Parent_Journal__c)
            : new List<Journal__c>();
          journalListAux.add(j);
          journalByTripMap.put(j.Parent_Journal__c, journalListAux.clone());
        }
      }

      for (Journal__c j : journalByTripList) {
        if (journalByTripMap.get(j.Id) == null)
          journalByTripMap.put(j.Id, new List<Journal__c>());
      }
    }
  }

  public void viewTripJournals() {
    newtrip = new Air__c();
    if (tripViewId != null && tripViewId != '') {
      journalByTripList = new List<Journal__c>();
      journalByTripMap = new Map<String, List<Journal__c>>();
      List<Journal__c> journalListAux;
      for (Journal__c j : [
        SELECT
          Id,
          Name,
          CreatedDate,
          CreatedById,
          Issue__c,
          Sales__c,
          Journal_Entry__c,
          CreatedBy.Name,
          G__c,
          Parent_Journal__c,
          Bid__c
        FROM Journal__c
        WHERE Air__c = :tripViewId
        ORDER BY CreatedDate DESC
      ]) {
        if (j.Parent_Journal__c == null) {
          journalByTripList.add(j);
        } else {
          journalListAux = journalByTripMap.get(j.Parent_Journal__c) != null
            ? journalByTripMap.get(j.Parent_Journal__c)
            : new List<Journal__c>();
          journalListAux.add(j);
          journalByTripMap.put(j.Parent_Journal__c, journalListAux.clone());
        }
      }

      for (Journal__c j : journalByTripList) {
        if (journalByTripMap.get(j.Id) == null)
          journalByTripMap.put(j.Id, new List<Journal__c>());
      }
    }
  }

  public void editDocumentTitle() {
    if (documentId != null && documentId != '') {
      update new ContentDocument(Id = documentId, Title = documentTitle);
      //for(ContentDocument document : documentBidList) if(document.Id == documentId) document.Title = documentTitle;
      for (ContentDocument document : documentTripList)
        if (document.Id == documentId)
          document.Title = documentTitle;
      documentId = '';
      documentTitle = '';
    }
  }

  public void deleteDocument() {
    if (documentIdActual != null && documentIdActual != '') {
      delete [SELECT Id FROM ContentDocument WHERE Id = :documentIdActual];
      getDocumentsByTrip();
    }
  }

  public void doAttachment() {
    system.debug(filename);
    system.debug(bodytrip);
    system.debug(documentRelationId);
    if (filename != null && bodytrip != null) {
      try {
        ContentVersion conVer = new ContentVersion();
        conVer.PathOnClient = '/' + filename;
        conVer.Title = filename.split('\.')[0];
        conVer.VersionData = (!Test.isRunningTest()
          ? EncodingUtil.base64Decode(
              bodytrip.subString(0, 100).split(',')[1] +
              bodytrip.substring(100, bodytrip.length())
            )
          : Blob.valueOf('Test'));
        insert conVer;

        Id conDoc = [
          SELECT ContentDocumentId
          FROM ContentVersion
          WHERE Id = :conVer.Id
        ]
        .ContentDocumentId;

        //Create ContentDocumentLink
        ContentDocumentLink cDe = new ContentDocumentLink();
        cDe.ContentDocumentId = conDoc;
        cDe.LinkedEntityId = documentRelationId;
        cDe.ShareType = 'V';
        cDe.Visibility = 'AllUsers';
        insert cDe;
      } catch (Exception e) {
        system.debug(e.getMessage());
      } finally {
        bodytrip = null;
        filename = null;
      }
    }
    getDocumentsByTrip();
  }

  public void getDocumentsByTrip() {
    documentTripList = new List<ContentDocument>();
    if (tripViewId != null && tripViewId != '') {
      Set<String> contentDocumentIds = new Set<String>();
      system.debug(tripViewId);
      for (ContentDocumentLink cdl : [
        SELECT Id, LinkedEntityId, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :tripViewId
      ]) {
        contentDocumentIds.add(cdl.ContentDocumentId);
      }
      if (!contentDocumentIds.isEmpty())
        documentTripList = [
          SELECT Id, Title, FileExtension, CreatedDate
          FROM ContentDocument
          WHERE Id IN :contentDocumentIds
        ];
    }
  }

  public void viewTripDetail() {
    if (tripViewId != null && tripViewId != '') {
      tripView = [
        SELECT
          Id,
          Name,
          Group_Type__c,
          Trace_Date__c,
          Status__c,
          Departure_Date__c,
          Return_Date__c,
          Decision_Due_Date__c,
          Departure_City__c,
          Departure_City__r.Airport_Code__c,
          Arrival_City__c,
          Arrival_City__r.Airport_Code__c,
          Form_Decision_Due_Date__c,
          Vendor__c,
          Vendor__r.Name,
          Vendor__r.City__r.Name,
          Vendor__r.City__c,
          RecordTypeId,
          RecordType.Name,
          Trip_Type__c,
          Return_Departure_City__c,
          Return_Arrival_City__c,
          Return_Departure_City__r.Airport_Code__c,
          Return_Arrival_City__r.Airport_Code__c,
          Decision_Due_Date_Last_Send_By__c,
          Decision_Due_Date_Last_Send_Date__c,
          Air_Charter__c,
          Charter_Type__c,
          Description__c,
          PAX__c,
          Deadline_Date__c,
          Back_end_Coordinator__c,
          Back_end_Coordinator__r.Name,
          (SELECT Id, Client_Notes__c FROM Itinerary__r)
        FROM Air__c
        WHERE Id = :tripViewId
      ];
      itineraryView = !tripView.Itinerary__r.isEmpty()
        ? tripView.Itinerary__r[0]
        : new Itinerary__c();
      tripItineraryId = itineraryView.Id != null ? itineraryView.Id : null;
      clientByProduction = new Contact();
      Map<String, String> contactAuxMap = new Map<String, String>();
      Map<String, String> userAuxMap = new Map<String, String>();
      if (tripView.Back_end_Coordinator__c != null)
        userAuxMap.put(
          tripView.Back_end_Coordinator__c,
          tripView.Back_end_Coordinator__r.Name
        );
      coordinatorGT = null;
      coordinatorGTName = null;
      tabGroundDefault = 'trip_bids';
      for (Production_Associations__c pa : [
        SELECT
          Id,
          Production_Opp__c,
          Air__c,
          Contact__c,
          Contact__r.Name,
          Contact__r.Title,
          Contact__r.Order__c,
          Contact__r.Email,
          Contact__r.Phone,
          Contact__r.MobilePhone,
          User__c,
          Team_Roles__c,
          User__r.Name,
          Role__c
        FROM Production_Associations__c
        WHERE Production_Opp__c = :opportunityId OR Air__c = :tripViewId
        ORDER BY Contact__r.Name ASC
      ]) {
        if (pa.Production_Opp__c != null) {
          if (
            pa.Contact__c != null &&
            pa.Role__c != null &&
            (pa.Role__c.contains('Primary Air') ||
            pa.Role__c.contains('CC: Air') ||
            pa.Role__c.contains('Contract Signer'))
          ) {
            contactAuxMap.put(pa.Contact__c, pa.Contact__r.Name);
            if (pa.Role__c.contains('Primary Air'))
              clientByProduction = new Contact(
                Id = pa.Contact__c,
                Email = pa.Contact__r.Email,
                Title = pa.Contact__r.Title,
                Phone = pa.Contact__r.Phone,
                MobilePhone = pa.Contact__r.MobilePhone
              );
          }
          if (pa.User__c != null) {
            userAuxMap.put(pa.User__c, pa.User__r.Name);
            if (pa.Team_Roles__c != null) {
              if (pa.Team_Roles__c.contains('Primary Air Coordinator')) {
                coordinatorGT = pa.User__c;
                coordinatorGTName = pa.User__r.Name;
              }
            }
          }
        }
      }

      clientsByProduction = new List<SelectOption>();
      clientsByProduction.add(new SelectOption('', '-- Select --'));
      for (String k1 : contactAuxMap.keySet()) {
        clientsByProduction.add(new SelectOption(k1, contactAuxMap.get(k1)));
      }

      teamMembers = new List<SelectOption>();
      teamMembers.add(new SelectOption('', '-- Not Assigned --'));
      Map<Id, Profile> profileIds = new Map<id, profile>(
        [
          SELECT Id, UserLicenseId
          FROM Profile
          WHERE
            UserLicenseId IN (
              SELECT Id
              FROM UserLicense
              WHERE name = 'Salesforce'
            )
        ]
      );
      for (User k1 : [
        SELECT Id, Name
        FROM User
        WHERE isActive = TRUE AND ProfileId IN :profileIds.Keyset()
        ORDER BY Name ASC
      ]) {
        teamMembers.add(new SelectOption(k1.Id, k1.Name));
      }

      getBidsByTrip();
      getConcessionsByTrip();
      getAircraftsByTrip();
      getItineraryByTrip();

      statusItineraryPL = new List<SelectOption>();
      statusItineraryPL.add(new SelectOption('', '-- Select --'));
      statusItineraryPL.add(
        new SelectOption('Itinerary Received', 'Itinerary Received')
      );
      statusItineraryPL.add(
        new SelectOption('Bid Request Stage', 'Bid Request Stage')
      );
      statusItineraryPL.add(
        new SelectOption('Pending Client Choice', 'Pending Client Choice')
      );
      statusItineraryPL.add(new SelectOption('Contracted', 'Contracted'));
      statusItineraryPL.add(new SelectOption('Budgeting', 'Budgeting'));
      statusItineraryPL.add(new SelectOption('Cancelled', 'Cancelled'));
      statusItineraryPL.add(new SelectOption('Layoff', 'Layoff'));
      statusItineraryPL.add(
        new SelectOption('Contracted on Own', 'Contracted on Own')
      );
      statusItineraryPL.add(
        new SelectOption('In Contracting', 'In Contracting')
      );

      Boolean addValue = true;
      for (SelectOption so : statusItineraryPL) {
        if (tripView.Status__c == so.getValue())
          addValue = false;
      }
      if (addValue && tripView.Status__c != null)
        statusItineraryPL.add(
          new SelectOption(tripView.Status__c, tripView.Status__c)
        );
    }
  }

  public void searchTrip() {
    //TripWrapper.orderFieldTrip = orderFieldTrip;
    tripList = new List<Air__c>();

    Set<String> tournamentIds = new Set<String>();
    String strQuery =
      'SELECT Id, Production__c, Name, Vendor__c, Vendor__r.Name, Departure_Date__c, Return_Date__c, PAX__c, Trip_Type__c, Group_Type__c, Baggage__c, Status__c, Decision_Due_Date__c, Dep_Arr__c, RT_Dep_Arr__c,' +
      ' Departure_City__r.Airport_Code__c, Arrival_City__r.Airport_Code__c, Return_Departure_City__c, Return_Arrival_City__c, Return_Departure_City__r.Airport_Code__c, Return_Arrival_City__r.Airport_Code__c' +
      ' FROM Air__c WHERE Production__c =: opportunityId AND RecordType.DeveloperName = \'Air_Trip_Details\' AND Departure_Date__c <> NULL';

    Date tdy = system.today();
    system.debug(trip_showprior);
    if (!trip_showprior) {
      if (trip_startdate != null && trip_enddate != null) {
        if (trip_startdate == trip_enddate) {
          strQuery += ' AND (Departure_Date__c <=: trip_enddate AND Return_Date__c >=: trip_enddate)';
        } else {
          strQuery +=
            ' AND (' +
            ' (Departure_Date__c >=: trip_startdate AND Return_Date__c <=: trip_enddate) OR ' +
            ' (Departure_Date__c <=: trip_startdate AND Return_Date__c >=: trip_startdate) OR ' +
            ' (Departure_Date__c <=: trip_enddate AND Return_Date__c >=: trip_enddate))';
        }
      } else {
        if (trip_startdate != null) {
          strQuery +=
            ' AND (' +
            '(Departure_Date__c <=: trip_startdate AND Return_Date__c >=: trip_startdate) OR ' +
            ' (Departure_Date__c =: trip_startdate OR Return_Date__c =: trip_startdate) ' +
            ')';
        }
        if (trip_enddate != null) {
          strQuery +=
            ' AND (' +
            ' (Departure_Date__c <=: trip_enddate AND Return_Date__c >=: trip_enddate) OR ' +
            ' (Departure_Date__c =: trip_enddate OR Return_Date__c =: trip_enddate) ' +
            ')';
        }
        if (trip_startdate == null && trip_enddate == null)
          strQuery += ' AND Departure_Date__c >=: tdy';
      }
    }
    if (trip_city != null && trip_city != '') {
      //trip_city = '%' + trip_city + '%';
      //strQuery += ' AND Start_City__r.Name LIKE: trip_city';
      List<String> searchSplit = trip_city.split(' - ');
      String str1;
      String str2;
      String str3;
      if (searchSplit.size() > 0) {
        if (searchSplit.size() == 3) {
          str1 = searchSplit[0] != null
            ? '%' + searchSplit[0].trim() + '%'
            : '%%';
          str2 = searchSplit[1] != null
            ? '%' + searchSplit[1].trim() + '%'
            : '%%';
          str3 = searchSplit[2] != null
            ? '%' + searchSplit[2].trim() + '%'
            : '%%';
          system.debug(str1);
          system.debug(str2);
          system.debug(str3);
          strQuery += ' AND ((Departure_City__r.Airport_Code__c LIKE: str1 OR Departure_City__r.Name LIKE: str2 OR Departure_City__r.City__r.Name LIKE: str3)';
          strQuery += ' OR (Arrival_City__r.Airport_Code__c LIKE: str1 OR Arrival_City__r.Name LIKE: str2 OR Arrival_City__r.City__r.Name LIKE: str3)';
          strQuery += ' OR (Return_Arrival_City__r.Airport_Code__c LIKE: str1 OR Return_Arrival_City__r.Name LIKE: str2 OR Return_Arrival_City__r.City__r.Name LIKE: str3)';
          strQuery += ' OR (Return_Departure_City__r.Airport_Code__c LIKE: str1 OR Return_Departure_City__r.Name LIKE: str2 OR Return_Departure_City__r.City__r.Name LIKE: str3))';
        } else if (searchSplit.size() == 2) {
          str1 = searchSplit[0] != null
            ? '%' + searchSplit[0].trim() + '%'
            : '%%';
          str2 = searchSplit[1] != null
            ? '%' + searchSplit[1].trim() + '%'
            : '%%';
          strQuery +=
            ' AND (Departure_City__r.Airport_Code__c LIKE: str1 OR Departure_City__r.Name LIKE: str1 OR Departure_City__r.City__r.Name LIKE: str1 OR Departure_City__r.Airport_Code__c LIKE: str2 OR Departure_City__r.Name LIKE: str2 OR Departure_City__r.City__r.Name LIKE: str2 ' +
            'OR Arrival_City__r.Airport_Code__c LIKE: str1 OR Arrival_City__r.Name LIKE: str1 OR Arrival_City__r.City__r.Name LIKE: str1 OR Arrival_City__r.Airport_Code__c LIKE: str2 OR Arrival_City__r.Name LIKE: str2 OR Arrival_City__r.City__r.Name LIKE: str2 ' +
            'OR Return_Arrival_City__r.Airport_Code__c LIKE: str1 OR Return_Arrival_City__r.Name LIKE: str1 OR Return_Arrival_City__r.City__r.Name LIKE: str1 OR Return_Arrival_City__r.Airport_Code__c LIKE: str2 OR Return_Arrival_City__r.Name LIKE: str2 OR Return_Arrival_City__r.City__r.Name LIKE: str2 ' +
            'OR Return_Departure_City__r.Airport_Code__c LIKE: str1 OR Return_Departure_City__r.Name LIKE: str1 OR Return_Departure_City__r.City__r.Name LIKE: str1 OR Return_Departure_City__r.Airport_Code__c LIKE: str2 OR Return_Departure_City__r.Name LIKE: str2 OR Return_Departure_City__r.City__r.Name LIKE: str2 ' +
            ')';
        } else {
          trip_city = '%' + trip_city + '%';
          strQuery +=
            ' AND (Departure_City__r.Name LIKE: trip_city OR Departure_City__r.Airport_Code__c LIKE: trip_city ' +
            'OR Arrival_City__r.Name LIKE: trip_city OR Arrival_City__r.Airport_Code__c LIKE: trip_city ' +
            'OR Return_Arrival_City__r.Name LIKE: trip_city OR Return_Arrival_City__r.Airport_Code__c LIKE: trip_city ' +
            'OR Return_Departure_City__r.Name LIKE: trip_city OR Return_Departure_City__r.Airport_Code__c LIKE: trip_city ' +
            ')';
        }
      } else {
        trip_city = '%' + trip_city + '%';
        strQuery +=
          ' AND (Departure_City__r.Name LIKE: trip_city OR Departure_City__r.Airport_Code__c LIKE: trip_city ' +
          'OR Arrival_City__r.Name LIKE: trip_city OR Arrival_City__r.Airport_Code__c LIKE: trip_city ' +
          'OR Return_Arrival_City__r.Name LIKE: trip_city OR Return_Arrival_City__r.Airport_Code__c LIKE: trip_city ' +
          'OR Return_Departure_City__r.Name LIKE: trip_city OR Return_Departure_City__r.Airport_Code__c LIKE: trip_city ' +
          ')';
      }
    }
    if (trip_vendor != null && trip_vendor != '') {
      trip_vendor = '%' + trip_vendor + '%';
      strQuery += ' AND Vendor__r.Name LIKE: trip_vendor';
    }
    if (!trip_showcancelled)
      strQuery += ' AND Status__c <> \'Cancelled\'';

    if (orderCheckTrip) {
      if (orderChangeTrip)
        orderOrientationTrip = 'ASC';
      else {
        if (orderOrientationTrip == 'ASC')
          orderOrientationTrip = 'DESC';
        else
          orderOrientationTrip = 'ASC';
      }
    }
    orderCheckTrip = false;

    Integer totalRecordsTrip = Database.countQuery(
      'Select count() from Air__c WHERE' + strQuery.substringAfter('WHERE')
    );
    totalPagesTrip = totalRecordsTrip != null &&
      totalRecordsTrip == 0
      ? 1
      : Integer.valueOf(
          (totalRecordsTrip / Decimal.valueOf(limitTrip))
            .round(System.RoundingMode.UP)
        );
    if (String.isBlank(searchTypeTrip)) {
      strQuery +=
        ' ORDER BY ' +
        orderFieldTrip +
        ' ' +
        orderOrientationTrip +
        ' NULLS LAST' +
        ', Id LIMIT :limitTrip';
      tripList = Database.query(strQuery);
      offsetTrip = null;
    } else {
      if (searchTypeTrip == 'next') {
        offsetTrip = (offsetTrip != null ? offsetTrip : 0) + limitTrip;
        strQuery +=
          ' AND (' +
          orderFieldTrip +
          (orderOrientationTrip == 'ASC' ? ' >' : ' <') +
          ':lastValueOfSortedField OR (' +
          orderFieldTrip +
          ' =:lastValueOfSortedField AND Id >:lastId)) ORDER BY ' +
          orderFieldTrip +
          ' ' +
          orderOrientationTrip +
          ' NULLS LAST' +
          ', Id LIMIT :limitTrip';
        tripList = Database.query(strQuery);
      } else if (searchTypeTrip == 'previous') {
        offsetTrip = (offsetTrip != null ? offsetTrip : 0) - limitTrip;
        strQuery +=
          ' AND (' +
          orderFieldTrip +
          (orderOrientationTrip == 'ASC' ? ' <' : ' >') +
          ':firstValueOfSortedField OR (' +
          orderFieldTrip +
          ' =:firstValueOfSortedField AND Id <:firstId)) ORDER BY ' +
          orderFieldTrip +
          ' ' +
          (orderOrientationTrip == 'ASC' ? 'DESC' : 'ASC') +
          ' NULLS LAST' +
          ', Id LIMIT :limitTrip';
        tripList = Database.query(strQuery);
        List<Air__c> airTrips = new List<Air__c>();
        for (Integer i = tripList.size() - 1; i >= 0; i--)
          airTrips.add(tripList[i]);
        tripList = airTrips;
      } else if (searchTypeTrip == 'first') {
        offsetTrip = null;
        strQuery +=
          ' ORDER BY ' +
          orderFieldTrip +
          ' ' +
          orderOrientationTrip +
          ' NULLS LAST' +
          ', Id LIMIT :limitTrip';
        tripList = Database.query(strQuery);
      } else if (searchTypeTrip == 'last') {
        offsetTrip =
          limitTrip *
          (Integer.valueOf(
            (totalRecordsTrip / Decimal.valueOf(limitTrip))
              .round(System.RoundingMode.CEILING)
          ) - 1);
        strQuery +=
          ' ORDER BY ' +
          orderFieldTrip +
          ' ' +
          (orderOrientationTrip == 'ASC' ? 'DESC' : 'ASC') +
          ' NULLS LAST' +
          ', Id LIMIT ' +
          String.valueOf(totalRecordsTrip - offsetTrip);
        tripList = Database.query(strQuery);
        List<Air__c> airTrips = new List<Air__c>();
        for (Integer i = tripList.size() - 1; i >= 0; i--)
          airTrips.add(tripList[i]);
        tripList = airTrips;
      }
    }
    firstId = !tripList.isEmpty() ? tripList[0].Id : null;
    lastId = !tripList.isEmpty() ? tripList[tripList.size() - 1].Id : null;
    firstValueOfSortedField = !tripList.isEmpty()
      ? (orderFieldTrip == 'Vendor__r.Name'
          ? tripList[0].Vendor__r.Name
          : tripList[0].get(orderFieldTrip))
      : null;
    lastValueOfSortedField = !tripList.isEmpty()
      ? (orderFieldTrip == 'Vendor__r.Name'
          ? tripList[tripList.size() - 1].Vendor__r.Name
          : tripList[tripList.size() - 1].get(orderFieldTrip))
      : null;
    searchTypeTrip = null;

    if (tripViewId != null && tripViewId != '')
      viewTripDetail();
  }

  public void deleteTrip() {
    if (itineraryIdActual != null && itineraryIdActual != '') {
      Air__c aAux = [SELECT Id FROM Air__c WHERE Id = :itineraryIdActual];
      delete [
        SELECT Id
        FROM Air__c
        WHERE
          Air_Trip_Details__c = :aAux.Id
          AND RecordType.DeveloperName = 'Air_Segments'
      ];
      //delete [SELECT Id FROM Concessions__c WHERE GT__c =: aAux.Id AND Bid__c = NULL];
      delete [SELECT Id FROM Itinerary__c WHERE Air__c = :aAux.Id];
      delete aAux;
      searchItinerary();
      orderFieldTrip = 'Departure_Date__c';
      //TripWrapper.orderFieldTrip = 'departure_date';
      searchTrip();
    }
  }

  public void editTrip() {
    newtrip = new Air__c();
    newitinerary = new Itinerary__c();
    if (itineraryIdActual != null && itineraryIdActual != '') {
      newitinerary = [
        SELECT Id, Air__c
        FROM Itinerary__c
        WHERE Id = :itineraryIdActual
      ];
      segmentList = new List<AirSegmentWrapper>();
      segmentListSize = 0;
      if (newitinerary.Air__c != null) {
        newtrip = [
          SELECT
            Id,
            Trip_Type__c,
            Departure_Date__c,
            Return_Date__c,
            Departure_City__c,
            Departure_City__r.Airport_Code__c,
            Departure_City__r.Name,
            Departure_City__r.City__c,
            Departure_City__r.City__r.Name,
            Arrival_City__c,
            Arrival_City__r.Airport_Code__c,
            Arrival_City__r.Name,
            Arrival_City__r.City__c,
            Arrival_City__r.City__r.Name,
            Air_Charter__c,
            Return_Arrival_City__c,
            Return_Departure_City__c,
            PAX__c,
            Air_Preferences__c,
            Status__c,
            Trace_Date__c,
            Decision_Due_Date__c,
            Group_Type__c,
            Baggage__c
          FROM Air__c
          WHERE Id = :newItinerary.Air__c
        ];
        //newtrip_startcity = newtrip.Start_City__r.Name;
        newtrip_depaturecity =
          (newtrip.Departure_City__r.Airport_Code__c != null
            ? newtrip.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          newtrip.Departure_City__r.Name +
          (newtrip.Departure_City__r.City__c != null
            ? ' - ' + newtrip.Departure_City__r.City__r.Name
            : '');
        newtrip_arrivalcity =
          (newtrip.Arrival_City__r.Airport_Code__c != null
            ? newtrip.Arrival_City__r.Airport_Code__c + ' - '
            : '') +
          newtrip.Arrival_City__r.Name +
          (newtrip.Arrival_City__r.City__c != null
            ? ' - ' + newtrip.Arrival_City__r.City__r.Name
            : '');
        newTripRecordType = (newtrip.Trip_Type__c == 'One Way'
          ? 'one-way'
          : (newtrip.Trip_Type__c == 'Round Trip'
              ? 'round-trip'
              : 'multi-city'));

        List<Air__c> segments = [
          SELECT
            Id,
            Air_Trip_Details__c,
            Departure_Date__c,
            Return_Date__c,
            Departure_City__c,
            Arrival_City__c,
            Departure_City__r.Airport_Code__c,
            Departure_City__r.Name,
            Departure_City__r.City__c,
            Departure_City__r.City__r.Name,
            Arrival_City__r.Airport_Code__c,
            Arrival_City__r.Name,
            Arrival_City__r.City__c,
            Arrival_City__r.City__r.Name
          FROM Air__c
          WHERE
            Air_Trip_Details__c = :newItinerary.Air__c
            AND RecordType.DeveloperName = 'Air_Segments'
        ];
        if (segments.size() > 0) {
          String aux1, aux2;
          for (Air__c segment : segments) {
            aux1 =
              (segment.Departure_City__r.Airport_Code__c != null
                ? segment.Departure_City__r.Airport_Code__c + ' - '
                : '') +
              segment.Departure_City__r.Name +
              (segment.Departure_City__r.City__c != null
                ? ' - ' + segment.Departure_City__r.City__r.Name
                : '');
            aux2 =
              (segment.Arrival_City__r.Airport_Code__c != null
                ? segment.Arrival_City__r.Airport_Code__c + ' - '
                : '') +
              segment.Arrival_City__r.Name +
              (segment.Arrival_City__r.City__c != null
                ? ' - ' + segment.Arrival_City__r.City__r.Name
                : '');
            segmentList.add(
              new AirSegmentWrapper(
                segment,
                segment.Departure_City__c,
                aux1,
                segment.Arrival_City__c,
                aux2
              )
            );
          }
        }
      }
    }
  }

  public void saveCreateJournal() {
    newJournal.Id = (createjournal_id != null &&
      createjournal_id != ''
      ? createjournal_id
      : null);
    if (createjournal_id == null || createjournal_id == '') {
      if (createjournal_type == 'trip' || createjournal_type == 'trip_stay') {
        newJournal.RecordTypeId = journal_tripJournalRT;
      } else {
        //newJournal.Bid__c = bidData.Id;
        //newJournal.RecordTypeId = journal_bidJournalRT;
      }
    }
    if (newJournal.Production_checkbox__c)
      newJournal.Production__c = opportunityId;
    //newJournal.Housing__c = (createjournal_type == 'housing_stay' ? newHousingStay.Id : housingStayViewId);
    if (createjournal_type == 'trip' && newtrip.Id != null)
      newJournal.Air__c = newtrip.Id;
    if (createjournal_type == 'trip_stay' && tripViewId != null)
      newJournal.Air__c = tripViewId;
    if (newJournal.Mark_Journal_trace_complete__c)
      newJournal.Trace_Date__c = null;
    //if(newJournal.Vendor_Checkbox__c) newJournal.Vendor__c = bidData.Vendor__c;
    system.debug(createjournal_tracedate);
    newJournal.Trace_Date__c = (createjournal_tracedate != null &&
      createjournal_tracedate != ''
      ? Date.parse(createjournal_tracedate)
      : null);
    if (createjournal_coordinator != null && createjournal_coordinator != '')
      newJournal.Trace_Coordinator__c = createjournal_coordinator;
    upsert newJournal;

    //delete [SELECT Id, Company__c FROM Related_Companies__c WHERE Journal__c =: newJournal.Id AND Company__c <> null];
    delete [
      SELECT Id, Contact__c
      FROM Related_Contact__c
      WHERE Journal__c = :newJournal.Id AND Contact__c != NULL
    ];

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
    Map<String, Related_Contact__c> rcoMapAux = new Map<String, Related_Contact__c>();
    if (
      createjournal_productioncontactids != null &&
      createjournal_productioncontactids.trim() != ''
    ) {
      for (String s : createjournal_productioncontactids.split(',')) {
        if (s.trim() != '') {
          rcoAux = new Related_Contact__c(
            Contact__c = s.trim(),
            Journal__c = newJournal.Id,
            Type__c = 'Production Contacts;'
          );
          rcoMapAux.put(rcoAux.Contact__c, rcoAux);
        }
      }
    }
    if (
      createjournal_companycontactids != null &&
      createjournal_companycontactids.trim() != ''
    ) {
      for (String s : createjournal_companycontactids.split(',')) {
        if (s.trim() != '') {
          rcoAux = new Related_Contact__c(
            Contact__c = s.trim(),
            Journal__c = newJournal.Id,
            Type__c = (rcoMapAux.get(s.trim()) != null
              ? rcoMapAux.get(s.trim()).Type__c + 'Company Contacts;'
              : 'Company Contacts;')
          );
          rcoMapAux.put(rcoAux.Contact__c, rcoAux);
        }
      }
    }

    if (createjournal_alert) {
      Set<String> userEmails = new Set<String>();
      for (Production_Associations__c pa : [
        SELECT Id, User__c, User__r.Name, User__r.Email
        FROM Production_Associations__c
        WHERE Production_Opp__c = :opportunityId AND User__c != NULL
      ])
        userEmails.add(pa.User__r.Email);
      if (userEmails.size() > 0) {
        List<Production_Associations__c> prodAssocAux = [
          SELECT Id, User__r.Name, User__r.Email
          FROM Production_Associations__c
          WHERE
            Production_Opp__c = :opportunityid
            AND User__c != NULL
            AND Team_Roles__c INCLUDES ('Primary Air Coordinator')
        ];

        List<String> userEmailsList = new List<String>(userEmails);
        Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
        if (prodAssocAux.size() > 0)
          mail.setOrgWideEmailAddressId(
            verifyWideAddress(prodAssocAux[0].User__r.Email)
          );
        mail.setToAddresses(userEmailsList);
        mail.setSubject('Urgent: Journal Entry for ' + opportunity.Name);
        String bodyAux =
          newJournal.Journal_Entry__c +
          '<br/><br/>' +
          '<a href="' +
          ApexPages.currentPage().getHeaders().get('Host') +
          '/' +
          newJournal.Id +
          '" target="_blank">Click here for the Journal entry</a><br/>' +
          //'<a href="'+ ApexPages.currentPage().getHeaders().get('Host') + '/' + housingStayViewId + '" target="_blank">Click here for the Trip Detail link</a><br/><br/>' +
          'Thanks, <br/>' +
          UserInfo.getUserName();
        mail.setHtmlBody(bodyAux);
        Messaging.sendEmail(new List<Messaging.SingleEmailMessage>{ mail });
      }
    }

    if (
      createjournal_coordinator != null &&
      createjournal_coordinator != '' &&
      (createjournal_id == '' ||
      createjournal_id == null)
    ) {
      Journal__c jAux = [
        SELECT Id, Task_ID__c
        FROM Journal__c
        WHERE Id = :newJournal.Id
      ];
      Task t = new Task(
        Id = (jAux.Task_ID__c != null ? jAux.Task_ID__c : null),
        Subject = (newJournal.Journal_Entry__c.length() > 40
          ? newJournal.Journal_Entry__c.subString(0, 40)
          : newJournal.Journal_Entry__c),
        RecordTypeId = task_traceTaskRT,
        ActivityDate = newJournal.Trace_Date__c,
        OwnerId = createjournal_coordinator,
        WhatId = newJournal.Id,
        Description = newJournal.Journal_Entry__c,
        Status = 'Open'
      );
      if (newJournal.Mark_Journal_trace_complete__c)
        t.Status = 'Completed';
      else
        t.Status = 'Open';
      upsert t;

      if (jAux.Task_ID__c == null) {
        newJournal.Task_ID__c = t.Id;
        update newJournal;
      }
    }

    //if(rcListAux.size() > 0) insert rcListAux;
    if (rcoMapAux.size() > 0)
      insert rcoMapAux.values();
    //searchStayJournal();
    if (createjournal_type == 'trip_stay')
      searchTripJournalsByGT();
  }

  public void saveTrip() {
    if (newtrip.Id == null)
      newtrip.Production__c = opportunityId;

    newtrip.Trip_Type__c = (newTripRecordType == 'one-way'
      ? 'One Way'
      : (newTripRecordType == 'round-trip'
          ? 'Round Trip'
          : (newTripRecordType == 'multi-city' ? 'Multi-City' : '')));
    newtrip.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
      .get('Air_Trip_Details')
      .getRecordTypeId();
    newtrip.Group_Type__c = newtrip_grouptype;
    newtrip.Departure_City__c = (newtrip_depaturecityid != null &&
      newtrip_depaturecityid != ''
      ? newtrip_depaturecityid
      : null);
    newtrip.Arrival_City__c = (newtrip_arrivalcityid != null &&
      newtrip_arrivalcityid != ''
      ? newtrip_arrivalcityid
      : null);
    upsert newtrip;

    if (newTripRecordType == 'one-way') {
      List<Air__c> airExist = [
        SELECT Id
        FROM Air__c
        WHERE
          Air_Trip_Details__c = :newtrip.Id
          AND RecordType.DeveloperName = 'Air_Segments'
      ];
      if (airExist.size() > 1)
        delete airExist;

      Air__c segment = newTrip.clone();
      segment.Id = (airExist.size() == 1 ? airExist[0].Id : null);
      segment.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Segments')
        .getRecordTypeId();
      segment.Air_Trip_Details__c = newtrip.Id;
      if (airExist.size() == 0)
        segment.Production__c = opportunityId;
      segment.Trip_Type__c = null;
      upsert segment;
    }
    if (
      newTripRecordType == 'round-trip' &&
      departure_cities != '' &&
      arrival_cities != ''
    ) {
      Air__c airAux;
      List<Air__c> segments = new List<Air__c>();
      Integer j = 0;
      system.debug(departure_cities);
      List<String> departure_citiesList = departure_cities.split(',');
      List<String> arrival_citiesList = arrival_cities.split(',');
      for (AirSegmentWrapper ase : segmentList) {
        system.debug(ase.air);
        system.debug(newtrip);
        system.debug(departure_citiesList[j]);
        system.debug(arrival_citiesList[j]);
        airAux = new Air__c(
          RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Segments')
            .getRecordTypeId(),
          Air_Trip_Details__c = newtrip.Id,
          Departure_City__c = departure_citiesList[j],
          Arrival_City__c = arrival_citiesList[j]
        );

        if (j == 0) {
          airAux.Departure_Date__c = ase.air.Departure_Date__c;
          newtrip.Departure_Date__c = ase.air.Departure_Date__c;
          newtrip.Departure_City__c = departure_citiesList[j];
          newtrip.Arrival_City__c = arrival_citiesList[j];
        }
        if (j == 1) {
          airAux.Return_Date__c = ase.air.Departure_Date__c;
          airAux.Departure_Date__c = ase.air.Departure_Date__c;
          newtrip.Return_Date__c = ase.air.Departure_Date__c;
          newtrip.Return_Departure_City__c = departure_citiesList[j];
          newtrip.Return_Arrival_City__c = arrival_citiesList[j];
        }

        if (ase.air.Id == null) {
          airAux.Production__c = opportunityId;
        } else {
          airAux.Id = ase.air.Id;
        }
        segments.add(airAux);
        j++;
      }

      if (segments.size() > 0)
        upsert segments;

      upsert newtrip;
    }
    if (
      newTripRecordType == 'multi-city' &&
      departure_cities != '' &&
      arrival_cities != ''
    ) {
      Air__c airAux;
      List<Air__c> segments = new List<Air__c>();
      Integer j = 0;
      List<String> departure_citiesList = departure_cities.split(',');
      List<String> arrival_citiesList = arrival_cities.split(',');
      Integer sizeAux = segmentList.size();
      for (AirSegmentWrapper ase : segmentList) {
        airAux = new Air__c(
          RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Segments')
            .getRecordTypeId(),
          Air_Trip_Details__c = newtrip.Id,
          Departure_Date__c = ase.air.Departure_Date__c,
          Departure_City__c = departure_citiesList[j],
          Arrival_City__c = arrival_citiesList[j]
        );

        if (j == 0) {
          newtrip.Departure_Date__c = ase.air.Departure_Date__c;
          newtrip.Departure_City__c = departure_citiesList[j];
          newtrip.Arrival_City__c = arrival_citiesList[j];
        }
        if ((j + 1) == sizeAux) {
          newtrip.Return_Date__c = ase.air.Departure_Date__c;
          newtrip.Return_Departure_City__c = departure_citiesList[j];
          newtrip.Return_Arrival_City__c = arrival_citiesList[j];
        }

        if (ase.air.Id == null) {
          airAux.Production__c = opportunityId;
        } else {
          airAux.Id = ase.air.Id;
        }
        segments.add(airAux);
        j++;
      }

      if (segments.size() > 0)
        upsert segments;
      upsert newtrip;
    }

    if (newitinerary.Id == null)
      newitinerary.Production__c = opportunityId;
    newitinerary.RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
      .get('Air_Itinerary')
      .getRecordTypeId();
    newitinerary.Air__c = newtrip.Id;
    newitinerary.Start_Date__c = newtrip.Departure_Date__c;
    //newitinerary.End_Date__c = newtrip.End_Date__c;
    newitinerary.Status__c = newtrip.Status__c;
    //newitinerary.City__c = newtrip.Start_City__c;
    upsert newitinerary;

    if (newtrip_clear)
      newTrip();

    searchItinerary();
    //orderFieldTrip = 'Departure_Date__c';
    //TripWrapper.orderFieldTrip = 'departure_date';
    //searchTrip();
  }

  public void deleteSegment() {
    if (segmentListActual != null) {
      Integer j = 0;
      for (AirSegmentWrapper s : segmentList) {
        if (segmentListActual == j) {
          segmentList.remove(j);
          break;
        }
        j++;
      }
      segmentListSize = segmentList.size();
    }
  }

  public void addSegment() {
    if (segmentList != null) {
      List<String> departure_citiesList = departure_cities.split(',');
      List<String> arrival_citiesList = arrival_cities.split(',');
      system.debug(arrival_cities);
      system.debug(arrival_citiesList);
      Integer j = 0;
      for (AirSegmentWrapper ase : segmentList) {
        ase.departure_cityid = departure_citiesList[j] == 'N/A'
          ? ''
          : departure_citiesList[j];
        ase.arrival_cityid = arrival_citiesList[j] == 'N/A'
          ? ''
          : arrival_citiesList[j];
        j++;
      }
      segmentList.add(new AirSegmentWrapper(new Air__c(), '', '', '', ''));
      segmentListSize = segmentList.size();
    }
  }

  public void changeTripType() {
    segmentList = new List<AirSegmentWrapper>();
    segmentListSize = 0;
    if (newtrip != null && newtrip.Id != null) {
      delete [
        SELECT Id
        FROM Air__c
        WHERE
          Air_Trip_Details__c = :newtrip.Id
          AND RecordTypeId = :Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Segments')
            .getRecordTypeId()
      ];
    }

    if (newTripRecordType == 'round-trip') {
      segmentList.add(new AirSegmentWrapper(new Air__c(), '', '', '', ''));
      segmentList.add(new AirSegmentWrapper(new Air__c(), '', '', '', ''));
    } else if (newTripRecordType == 'multi-city') {
      segmentList.add(new AirSegmentWrapper(new Air__c(), '', '', '', ''));
      segmentList.add(new AirSegmentWrapper(new Air__c(), '', '', '', ''));
    }
    segmentListSize = segmentList.size();
    system.debug(segmentList);
  }

  public void newTrip() {
    segmentList = new List<AirSegmentWrapper>();
    segmentListSize = 0;
    newtrip = new Air__c(
      RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Trip_Details')
        .getRecordTypeId(),
      Status__c = 'Itinerary Received',
      Air_Preferences__c = 'RRU'
    );
    newitinerary = new Itinerary__c(
      RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Itinerary')
        .getRecordTypeId()
    );
    newtrip_depaturecity = null;
    newtrip_arrivalcity = null;
    newTripRecordType = 'one-way';
  }

  public void cloneItinerary() {
    if (itineraryIdActual != null && itineraryIdActual != '') {
      Itinerary__c iti = [
        SELECT Id, Air__c, Production__c, Start_Date__c, Status__c, RecordTypeId
        FROM Itinerary__c
        WHERE Id = :itineraryIdActual
      ];
      Air__c air = [
        SELECT
          Id,
          Trip_Type__c,
          RecordTypeId,
          Group_Type__c,
          Departure_Date__c,
          Departure_City__c,
          Arrival_City__c,
          Return_Date__c,
          PAX__c,
          Air_Preferences__c,
          Trace_Date__c,
          Decision_Due_Date__c,
          Return_Arrival_City__c,
          Return_Departure_City__c,
          Air_Charter__c,
          Air_Type__c
        FROM Air__c
        WHERE Id = :iti.Air__c
      ];
      Air__c airNew = air.clone();
      airNew.Production__c = opportunityId;
      airNew.Vendor__c = null;
      airNew.Status__c = 'Itinerary Received';
      airNew.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Trip_Details')
        .getRecordTypeId();
      insert airNew;

      List<Air__c> segments = new List<Air__c>();
      Air__c segmentAux;
      for (Air__c segment : [
        SELECT
          Id,
          Trip_Type__c,
          RecordTypeId,
          Group_Type__c,
          Departure_Date__c,
          Departure_City__c,
          Arrival_City__c,
          Return_Date__c,
          PAX__c,
          Air_Preferences__c,
          Trace_Date__c,
          Decision_Due_Date__c,
          Return_Arrival_City__c,
          Return_Departure_City__c,
          Air_Charter__c,
          Air_Type__c
        FROM Air__c
        WHERE
          Air_Trip_Details__c = :air.Id
          AND RecordType.DeveloperName = 'Air_Segments'
      ]) {
        segmentAux = segment.clone();
        segmentAux.Production__c = opportunityId;
        segmentAux.Air_Trip_Details__c = airNew.Id;
        segmentAux.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
          .get('Air_Segments')
          .getRecordTypeId();
        segments.add(segmentAux);
      }
      if (segments.size() > 0)
        insert segments;

      Itinerary__c itiNew = iti.clone();
      itiNew.Production__c = opportunityId;
      itiNew.RecordTypeId = Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Itinerary')
        .getRecordTypeId();
      itiNew.Air__c = airNew.Id;
      insert itiNew;

      searchItinerary();
    }
  }

  public void searchItinerary() {
    itineraryList = new List<Itinerary__c>();
    //itineraryMap = new Map<String,List<Itinerary__c>>();
    List<Itinerary__c> itiAuxList;

    //itineraryCountMap = new Map<String,Integer>();
    //tournamentList = new List<Itinerary__c>();
    Set<String> tournamentIds = new Set<String>();
    String strQuery =
      'SELECT Id, Production__c, Status__c, Start_Date__c, End_Date__c, ' +
      'Housing__c, Air__r.Name, Air__r.RecordType.Name, Air__r.Trace_Date__c, Air__r.PAX__c, Air__r.Return_Date__c, Air__r.Preferred_Airline__c, ' +
      'City__c, City__r.Name, Air__r.Vendor__c,  Air__r.Group_Type__c, Air__r.Status__c, Air__r.Decision_Due_Date__c, Air__r.Departure_Date__c, Air__r.Trip_Type__c, ' +
      'Production__r.Parent_Production__c, Air__r.Vendor__r.Name, Air__r.Departure_City__r.Airport_Code__c, Air__r.Arrival_City__r.Airport_Code__c, ' +
      'Air__r.Return_Departure_City__r.Airport_Code__c, Air__r.Return_Arrival_City__r.Airport_Code__c, Air__r.Return_Departure_City__c, Air__r.Return_Arrival_City__c ' +
      'FROM Itinerary__c WHERE Production__c =: opportunityId AND RecordType.Name = \'Air Itinerary\' AND Air__r.Departure_Date__c <> NULL';

    Date tdy = system.today();
    system.debug(itinerary_showprior);
    if (!itinerary_showprior) {
      if (itinerary_startdate != null) {
        strQuery +=
          ' AND ((Air__r.Departure_Date__c =: itinerary_startdate) ' +
          ' OR (Air__r.Departure_Date__c <=: itinerary_startdate AND Air__r.Return_Date__c >=: itinerary_startdate) ' +
          //' OR (Air__r.Departure_Date__c >=: itinerary_startdate AND Air__r.Return_Date__c = NULL) ' +
          ')';
      } else {
        strQuery += ' AND Air__r.Departure_Date__c >=: tdy';
      }
      /*if(itinerary_startdate != null && itinerary_enddate != null){
                if(itinerary_startdate == itinerary_enddate){
                    strQuery += ' AND (Start_Date__c <=: itinerary_enddate AND End_Date__c >=: itinerary_enddate)';
                }else{
                    strQuery += ' AND ((Start_Date__c <=: itinerary_startdate AND End_Date__c >=: itinerary_startdate) OR (Start_Date__c <=: itinerary_enddate AND End_Date__c >=: itinerary_enddate))';
                }
            }else{
                if(itinerary_startdate != null) strQuery += ' AND (Start_Date__c >=: itinerary_startdate OR End_Date__c >=: itinerary_startdate)';
                if(itinerary_enddate != null) strQuery += ' AND (Start_Date__c >=: itinerary_enddate OR End_Date__c <=: itinerary_enddate)';
            }*/
    }
    if (itinerary_city != null && itinerary_city != '') {
      //strQuery += ' AND City__r.Name LIKE: itinerary_city';
      List<String> searchSplit = itinerary_city.split(' - ');
      String str1;
      String str2;
      String str3;
      if (searchSplit.size() > 0) {
        if (searchSplit.size() == 3) {
          str1 = searchSplit[0] != null
            ? '%' + searchSplit[0].trim() + '%'
            : '%%';
          str2 = searchSplit[1] != null
            ? '%' + searchSplit[1].trim() + '%'
            : '%%';
          str3 = searchSplit[2] != null
            ? '%' + searchSplit[2].trim() + '%'
            : '%%';
          system.debug(str1);
          system.debug(str2);
          system.debug(str3);
          strQuery += ' AND ((Air__r.Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Departure_City__r.Name LIKE: str2 OR Air__r.Departure_City__r.City__r.Name LIKE: str3)';
          strQuery += ' OR (Air__r.Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Arrival_City__r.Name LIKE: str2 OR Air__r.Arrival_City__r.City__r.Name LIKE: str3)';
          strQuery += ' OR (Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Arrival_City__r.Name LIKE: str2 OR Air__r.Return_Arrival_City__r.City__r.Name LIKE: str3)';
          strQuery += ' OR (Air__r.Return_Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Departure_City__r.Name LIKE: str2 OR Air__r.Return_Departure_City__r.City__r.Name LIKE: str3))';
        } else if (searchSplit.size() == 2) {
          str1 = searchSplit[0] != null
            ? '%' + searchSplit[0].trim() + '%'
            : '%%';
          str2 = searchSplit[1] != null
            ? '%' + searchSplit[1].trim() + '%'
            : '%%';
          strQuery +=
            ' AND (Air__r.Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Departure_City__r.Name LIKE: str1 OR Air__r.Departure_City__r.City__r.Name LIKE: str1 OR Air__r.Departure_City__r.Airport_Code__c LIKE: str2 OR Air__r.Departure_City__r.Name LIKE: str2 OR Air__r.Departure_City__r.City__r.Name LIKE: str2 ' +
            'OR Air__r.Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Arrival_City__r.Name LIKE: str1 OR Air__r.Arrival_City__r.City__r.Name LIKE: str1 OR Air__r.Arrival_City__r.Airport_Code__c LIKE: str2 OR Air__r.Arrival_City__r.Name LIKE: str2 OR Air__r.Arrival_City__r.City__r.Name LIKE: str2 ' +
            'OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Arrival_City__r.Name LIKE: str1 OR Air__r.Return_Arrival_City__r.City__r.Name LIKE: str1 OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: str2 OR Air__r.Return_Arrival_City__r.Name LIKE: str2 OR Air__r.Return_Arrival_City__r.City__r.Name LIKE: str2 ' +
            'OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: str1 OR Air__r.Return_Departure_City__r.Name LIKE: str1 OR Air__r.Return_Departure_City__r.City__r.Name LIKE: str1 OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: str2 OR Air__r.Return_Departure_City__r.Name LIKE: str2 OR Air__r.Return_Departure_City__r.City__r.Name LIKE: str2 ' +
            ')';
        } else {
          itinerary_city = '%' + itinerary_city + '%';
          strQuery +=
            ' AND (Air__r.Departure_City__r.Name LIKE: itinerary_city OR Air__r.Departure_City__r.Airport_Code__c LIKE: itinerary_city ' +
            'OR Air__r.Arrival_City__r.Name LIKE: itinerary_city OR Air__r.Arrival_City__r.Airport_Code__c LIKE: itinerary_city ' +
            'OR Air__r.Return_Arrival_City__r.Name LIKE: itinerary_city OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: itinerary_city ' +
            'OR Air__r.Return_Departure_City__r.Name LIKE: itinerary_city OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: itinerary_city ' +
            ')';
        }
      } else {
        itinerary_city = '%' + itinerary_city + '%';
        strQuery +=
          ' AND (Air__r.Departure_City__r.Name LIKE: itinerary_city OR Air__r.Departure_City__r.Airport_Code__c LIKE: itinerary_city ' +
          'OR Air__r.Arrival_City__r.Name LIKE: itinerary_city OR Air__r.Arrival_City__r.Airport_Code__c LIKE: itinerary_city ' +
          'OR Air__r.Return_Arrival_City__r.Name LIKE: itinerary_city OR Air__r.Return_Arrival_City__r.Airport_Code__c LIKE: itinerary_city ' +
          'OR Air__r.Return_Departure_City__r.Name LIKE: itinerary_city OR Air__r.Return_Departure_City__r.Airport_Code__c LIKE: itinerary_city ' +
          ')';
      }
    }
    if (itinerary_vendor != null && itinerary_vendor != '') {
      itinerary_vendor = '%' + itinerary_vendor + '%';
      strQuery += ' AND Air__r.Vendor__r.Name LIKE: itinerary_vendor';
    }
    if (itinerary_status != null && itinerary_status != '') {
      strQuery += ' AND Status__c IN (\'' + itinerary_status + '\'';
      if (itinerary_showcancelled)
        strQuery += ',\'Cancelled\'';
      strQuery += ')';
    }

    if (!itinerary_showcancelled)
      strQuery += ' AND Status__c <> \'Cancelled\'';

    //strQuery += ' ORDER BY Air__r.Departure_Date__c ASC LIMIT 100';
    if (orderCheckItinerary) {
      if (orderChangeItinerary) {
        orderOrientationItinerary = 'ASC';
      } else {
        if (orderOrientationItinerary == 'ASC')
          orderOrientationItinerary = 'DESC';
        else
          orderOrientationItinerary = 'ASC';
      }
    }
    orderCheckItinerary = false;

    /*Integer totalRecordsItinerary = Database.query(strQuery + ' LIMIT 50000').size();
        totalPagesItinerary = totalRecordsItinerary != null && totalRecordsItinerary == 0 ? 1 : Integer.valueOf((totalRecordsItinerary/Decimal.valueOf(limitItinerary)).round(System.RoundingMode.UP));
        if(searchTypeItinerary != null && searchTypeItinerary != ''){
            if(searchTypeItinerary == 'next') offsetItinerary = (offsetItinerary != null ? offsetItinerary : 0) + limitItinerary; 
            if(searchTypeItinerary == 'previous') offsetItinerary = (offsetItinerary != null ? offsetItinerary : 0) - limitItinerary;
            if(searchTypeItinerary == 'first') offsetItinerary = null;
            if(searchTypeItinerary == 'last') offsetItinerary = limitItinerary*(Integer.valueOf((totalRecordsItinerary/Decimal.valueOf(limitItinerary)).round(System.RoundingMode.CEILING)) - 1);
        }
        strQuery += ' ORDER BY ' + (orderFieldItinerary != null ? orderFieldItinerary : 'Air__r.Departure_Date__c') + ' ' + (orderOrientationItinerary != null ? orderOrientationItinerary : 'ASC') + ' NULLS LAST';
        if(offsetItinerary == null || offsetItinerary <= 0) strQuery += ' LIMIT :limitItinerary'; else strQuery += ' LIMIT :limitItinerary OFFSET :offsetItinerary';
        searchTypeItinerary = null;*/

    Integer totalRecordsItinerary = Database.countQuery(
      'Select count() from Itinerary__c WHERE' +
      strQuery.substringAfter('WHERE')
    );
    totalPagesItinerary = totalRecordsItinerary != null &&
      totalRecordsItinerary == 0
      ? 1
      : Integer.valueOf(
          (totalRecordsItinerary / Decimal.valueOf(limitItinerary))
            .round(System.RoundingMode.UP)
        );
    if (String.isBlank(searchTypeItinerary)) {
      strQuery +=
        ' ORDER BY ' +
        orderFieldItinerary +
        ' ' +
        orderOrientationItinerary +
        ' NULLS LAST' +
        ', Id LIMIT :limitItinerary';
      itineraryList = Database.query(strQuery);
      offsetItinerary = null;
    } else {
      if (searchTypeItinerary == 'next') {
        offsetItinerary =
          (offsetItinerary != null ? offsetItinerary : 0) + limitItinerary;
        strQuery +=
          ' AND (' +
          orderFieldItinerary +
          (orderOrientationItinerary == 'ASC' ? ' >' : ' <') +
          ':lastValueOfSortedFieldItinerary OR (' +
          orderFieldItinerary +
          ' =:lastValueOfSortedFieldItinerary AND Id >:lastIdItinerary)) ORDER BY ' +
          orderFieldItinerary +
          ' ' +
          orderOrientationItinerary +
          ' NULLS LAST' +
          ', Id LIMIT :limitItinerary';
        itineraryList = Database.query(strQuery);
      } else if (searchTypeItinerary == 'previous') {
        offsetItinerary =
          (offsetItinerary != null ? offsetItinerary : 0) - limitItinerary;
        strQuery +=
          ' AND (' +
          orderFieldItinerary +
          (orderOrientationItinerary == 'ASC' ? ' <' : ' >') +
          ':firstValueOfSortedFieldItinerary OR (' +
          orderFieldItinerary +
          ' =:firstValueOfSortedFieldItinerary AND Id <:firstIdItinerary)) ORDER BY ' +
          orderFieldItinerary +
          ' ' +
          (orderOrientationItinerary == 'ASC' ? 'DESC' : 'ASC') +
          ' NULLS LAST' +
          ', Id LIMIT :limitItinerary';
        itineraryList = Database.query(strQuery);
        List<Itinerary__c> airTrips = new List<Itinerary__c>();
        for (Integer i = itineraryList.size() - 1; i >= 0; i--)
          airTrips.add(itineraryList[i]);
        itineraryList = airTrips;
      } else if (searchTypeItinerary == 'first') {
        offsetItinerary = null;
        strQuery +=
          ' ORDER BY ' +
          orderFieldItinerary +
          ' ' +
          orderOrientationItinerary +
          ' NULLS LAST' +
          ', Id LIMIT :limitItinerary';
        itineraryList = Database.query(strQuery);
      } else if (searchTypeItinerary == 'last') {
        offsetItinerary =
          limitItinerary *
          (Integer.valueOf(
            (totalRecordsItinerary / Decimal.valueOf(limitItinerary))
              .round(System.RoundingMode.CEILING)
          ) - 1);
        strQuery +=
          ' ORDER BY ' +
          orderFieldItinerary +
          ' ' +
          (orderOrientationItinerary == 'ASC' ? 'DESC' : 'ASC') +
          ' NULLS LAST' +
          ', Id LIMIT ' +
          String.valueOf(totalRecordsItinerary - offsetItinerary);
        itineraryList = Database.query(strQuery);
        List<Itinerary__c> airTrips = new List<Itinerary__c>();
        for (Integer i = itineraryList.size() - 1; i >= 0; i--)
          airTrips.add(itineraryList[i]);
        itineraryList = airTrips;
      }
    }
    firstIdItinerary = !itineraryList.isEmpty() ? itineraryList[0].Id : null;
    lastIdItinerary = !itineraryList.isEmpty()
      ? itineraryList[itineraryList.size() - 1].Id
      : null;
    firstValueOfSortedFieldItinerary = !itineraryList.isEmpty()
      ? itineraryList[0].Start_Date__c
      : null;
    lastValueOfSortedFieldItinerary = !itineraryList.isEmpty()
      ? itineraryList[itineraryList.size() - 1].Start_Date__c
      : null;
    searchTypeItinerary = null;

    List<AirSegmentWrapper> lstGroundAux = new List<AirSegmentWrapper>();
    tripsItineraryMap = new Map<String, List<AirSegmentWrapper>>();
    Set<String> tripIds = new Set<String>();
    for (Itinerary__c iti : itineraryList)
      if (iti.Air__c != null)
        tripIds.add(iti.Air__c);

    bidContractByAirMap = new Map<String, Bid__c>();
    for (Bid__c b : [
      SELECT Id, Name, Air__c
      FROM Bid__c
      WHERE Air__c IN :tripIds AND Status__c = 'Contracted'
      ORDER BY createdDate ASC
    ])
      bidContractByAirMap.put(b.Air__c, b);

    ratesByBidMap = new Map<String, Revenue__c>();
    for (Revenue__c r : [
      SELECT id, Total_Price__c, Bid__c, Bid__r.Name, Bid__r.GT__c
      FROM Revenue__c
      WHERE
        Bid__r.GT__c IN :tripIds
        AND Bid__r.Status__c = 'Contracted'
        AND RecordType.DeveloperName = 'Ground_Rate_Travel_Commission'
      ORDER BY createdDate ASC
    ])
      ratesByBidMap.put(r.Bid__r.GT__c, r);

    system.debug(tripIds);
    //FOR ITINERARY TAB - TRIP
    vehiclesByTripMap = new Map<String, List<Ground__c>>();
    travelsItineraryMap = new Map<String, List<Ground__c>>();
    tripsItineraryCountMap = new Map<String, Integer>();
    travelsItineraryCountMap = new Map<String, Integer>();
    Set<String> subtripIds = new Set<String>();

    /*for(Air__c hd : [SELECT Id, Trip_Type__c, Departure_Date__c FROM Air__c WHERE Id IN: tripIds]){
            if(hd.Trip_Type__c == 'One Way'){
                lstGroundAux = tripsItineraryMap.get(hd.Id) != null ? tripsItineraryMap.get(hd.Id) : new List<AirSegmentWrapper>{new AirSegmentWrapper(hd, hd.Departure_Date__c)};
                    tripsItineraryMap.put(hd.Id,lstGroundAux.clone());
            }
        }*/
    for (Air__c hd : [
      SELECT
        Id,
        Name,
        RecordType.DeveloperName,
        Air_Trip_Details__c,
        Air_Trip_Details__r.Name,
        Air_Trip_Details__r.Trip_Type__c,
        Air_Trip_Details__r.Departure_Date__c,
        Departure_Date__c,
        Arrival_Date__c,
        Return_Date__c,
        Flight_Duration_hrs__c,
        Flight_Duration_Mins__c,
        Class__c,
        Equip_Type__c,
        Operated_by__c,
        Airline__c,
        Type_of_Equipment__c
      FROM Air__c
      WHERE Air_Trip_Details__c IN :tripIds
    ]) {
      /*if(hd.RecordType.DeveloperName == 'Vehicle_Type'){
                lstGroundAux = vehiclesByTripMap.get(hd.GT_Trip_Details__c) != null ? vehiclesByTripMap.get(hd.GT_Trip_Details__c) : new List<Ground__c>();
                lstGroundAux.add(hd);
                vehiclesByTripMap.put(hd.GT_Trip_Details__c,lstGroundAux.clone());
            }*/
      if (hd.RecordType.DeveloperName == 'Air_Segments') {
        if (hd.Air_Trip_Details__r.Trip_Type__c == 'One Way') {
          lstGroundAux = tripsItineraryMap.get(hd.Air_Trip_Details__c) != null
            ? tripsItineraryMap.get(hd.Air_Trip_Details__c)
            : new List<AirSegmentWrapper>();
          lstGroundAux.add(new AirSegmentWrapper(hd, hd.Departure_Date__c));
        } else if (hd.Air_Trip_Details__r.Trip_Type__c == 'Round Trip') {
          lstGroundAux = tripsItineraryMap.get(hd.Air_Trip_Details__c) != null
            ? tripsItineraryMap.get(hd.Air_Trip_Details__c)
            : new List<AirSegmentWrapper>();
          lstGroundAux.add(
            new AirSegmentWrapper(
              hd,
              lstGroundAux.size() == 1
                ? hd.Return_Date__c
                : hd.Departure_Date__c
            )
          );
        } else if (hd.Air_Trip_Details__r.Trip_Type__c == 'Multi-City') {
          lstGroundAux = tripsItineraryMap.get(hd.Air_Trip_Details__c) != null
            ? tripsItineraryMap.get(hd.Air_Trip_Details__c)
            : new List<AirSegmentWrapper>();
          lstGroundAux.add(new AirSegmentWrapper(hd, hd.Departure_Date__c));
        }

        tripsItineraryMap.put(hd.Air_Trip_Details__c, lstGroundAux.clone());
        //subtripIds.add(hd.Id);
      }
    }
    system.debug(tripsItineraryMap);
    /*for(Ground__c hd : [SELECT Id, GT_Sub_Trip_Details__c, Line__c, Vehicle_Ref__c, Start_Date__c, End_Date__c, Travel_Type__c, Group_Type__c, Location_Type__c, 
                            Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c, Sub_Trip_Notes__c
                            FROM Ground__c WHERE RecordType.DeveloperName = 'GT_Travel_Details' AND GT_Sub_Trip_Details__c IN: subtripIds]){
            lstGroundAux = travelsItineraryMap.get(hd.GT_Sub_Trip_Details__c) != null ? travelsItineraryMap.get(hd.GT_Sub_Trip_Details__c) : new List<Ground__c>();
            lstGroundAux.add(hd);
            travelsItineraryMap.put(hd.GT_Sub_Trip_Details__c,lstGroundAux.clone());
        }*/
    for (String sd : tripIds) {
      if (ratesByBidMap.get(sd) == null)
        ratesByBidMap.put(sd, new Revenue__c());
      if (bidContractByAirMap.get(sd) == null)
        bidContractByAirMap.put(sd, new Bid__c());
      if (vehiclesByTripMap.get(sd) == null)
        vehiclesByTripMap.put(sd, new List<Ground__c>());
      if (tripsItineraryMap.get(sd) == null) {
        tripsItineraryMap.put(sd, new List<AirSegmentWrapper>());
        tripsItineraryCountMap.put(sd, 0);
      } else {
        tripsItineraryCountMap.put(sd, tripsItineraryMap.size());
      }
    }
    /*for(String sd : subtripIds){
            if(travelsItineraryMap.get(sd) == null){
                travelsItineraryMap.put(sd,new List<Ground__c>());
                travelsItineraryCountMap.put(sd,0);
            }else{
                travelsItineraryCountMap.put(sd,travelsItineraryMap.size());
            }
        }*/
  }

  public void saveSale() {
    update sales;
  }

  /*public void saveEditItem(){
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
    }*/

  public void deleteAircraftTrip() {
    if (aircraftIdActual != null && aircraftIdActual != '') {
      delete [SELECT Id FROM Air__c WHERE Id = :aircraftIdActual];
      refreshAircraftDataBids(tripViewId);
    }
    searchItinerary();
    getAircraftsByTrip();
  }

  /*public void deleteVehicle(){
        if(vehicleIdActual != null && vehicleIdActual != '') delete [SELECT Id FROM Ground__c WHERE Id=:vehicleIdActual];
        searchItinerary();
        getVehiclesProduction();
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
                //Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null),
                Other_Amenities__c = vehicle_otheramenities
            );
            update new_vehicle;
        }
        getVehiclesProduction();
    }
    
    public void addVehicle(){
        system.debug(vehicle_amenities);
        if(opportunityId != null && opportunityId != null){
            new_vehicle.Id = null;
            new_vehicle.RecordTypeId = ground_vehicletypeRT;
            new_vehicle.Production_Ground__c = opportunityId;
            new_vehicle.Amenities__c = (vehicle_amenities != null && vehicle_amenities != '' ? vehicle_amenities.replace(',',';') : null);
            insert new_vehicle;
        }
        getVehiclesProduction();
    }
    
    public void newVehicle(){
    	new_vehicle = new Ground__c();
    }*/

  public void newAircraftTrip() {
    newAircraftTrip = new Air__c();
  }

  /*@RemoteAction
    global static List<String> getGroundAmenities(String groundid){
        List<String> dataList = new List<String>();
        Ground__c g = [SELECT Id, Amenities__c FROM Ground__c WHERE Id =: groundid];
        if(g.Amenities__c != null){
            for(String s : g.Amenities__c.split(';')){
                dataList.add(s);
            }
        }
        return dataList;
    }*/

  public void getVehiclesProduction() {
    vehiclesByProductionList = new List<Ground__c>();
    if (opportunityId != null && opportunityId != '') {
      vehiclesByProductionList = [
        SELECT
          Id,
          Production_Ground__c,
          RecordTypeId,
          RecordType.Name,
          Vehicle_Ref__c,
          Vehicle_Type__c,
          Capacity__c,
          Make__c,
          Model__c,
          Year__c,
          Amenities__c,
          Other_Amenities__c
        FROM Ground__c
        WHERE
          RecordType.Name = 'Vehicle Type'
          AND Production_Ground__c = :opportunityId
          AND Bid__c = NULL
          AND Bid_Sub_Trip__c = NULL
          AND GT_Sub_Trip_Details__c = NULL
          AND GT_Trip_Details__c = NULL
          AND Sales_GT_Details__c = NULL
      ];
    }
  }

  public void getRateDetailsProduction() {
    if (opportunityId != null && opportunityId != '') {
      itemsByProductionList = [
        SELECT
          Id,
          Concession_Type__c,
          Concession_Provided__c,
          Concessions_Requested__c
        FROM Concessions__c
        WHERE
          Concession_Type__c = 'GT'
          AND Production__c = :opportunityId
          AND Bid__c = NULL
          AND Housing__c = NULL
          AND Freight__c = NULL
      ];
    }
  }

  public void searchProduction() {
    List<Opportunity> searchOpportunity;
    opportunityId = null;
    opportunity = null;
    system.debug(searchOption);
    if (searchOption == 'searchByParent') {
      List<Air__c> searchAir = [
        SELECT Id, Production__c
        FROM Air__c
        WHERE
          Name = :searchValue
          AND RecordType.DeveloperName = 'Air_Trip_Details'
      ];
      system.debug(searchAir);
      if (searchAir.size() > 0) {
        opportunity = [
          SELECT
            Id,
            Name,
            Alias_With_Production_Name__c,
            AccountId,
            Account.Name,
            Parent_Production__c,
            RecordTypeId,
            RecordType.Name
          FROM Opportunity
          WHERE Id = :searchAir[0].Production__c
        ];
        opportunityId = opportunity.Id;
        getDataProduction();
        tripViewId = searchAir[0].Id;
        if (tripViewId != null && tripViewId != '')
          viewTripDetail();
      }
    } else if (searchOption == 'searchByBid') {
      List<Bid__c> searchBid = [
        SELECT Id, Name, Air__c, Air__r.Name, Status__c, Production__c
        FROM Bid__c
        WHERE
          Name = :searchValue
          AND Air__c != NULL
          AND RecordType.DeveloperName = 'Air_Bid'
      ];
      dataBidIdsearch = null;
      if (searchBid.size() > 0) {
        opportunity = [
          SELECT
            Id,
            Name,
            Alias_With_Production_Name__c, 
            AccountId,
            Account.Name,
            Parent_Production__c,
            RecordTypeId,
            RecordType.Name
          FROM Opportunity
          WHERE Id = :searchBid[0].Production__c
        ];
        opportunityId = opportunity.Id;
        //getDataByBid = true;
        getDataProduction();
        tripViewId = searchBid[0].Air__c;
        dataBidIdsearch = searchBid[0].Id;
        if (tripViewId != null && tripViewId != '')
          viewTripDetail();
        if (searchBid[0].Status__c == 'Contracted') {
          vfpConfiguration.bidId = searchBid[0].Id;
          vfpConfiguration.bidName = searchBid[0].Name;
          vfpConfiguration.parentId = searchBid[0].Air__c;
        }
      }
    }
  }

  public void getDataProduction() {
    if (opportunityId != null && opportunityId != '') {
      upsertSession(UserInfo.getUserId(), opportunityId); //SESSION CUSTOM SETTING
      tripViewId = null;
      tripView = null;
      tripBidNumber = null;

      vfpConfiguration = new DashboardConfigurationWrapper();
      system.debug(opportunityId);
      opportunity = [
        SELECT
          Id,
          Name,
          Alias_With_Production_Name__c, 
          AccountId,
          Account.Name,
          Parent_Production__c,
          RecordTypeId,
          RecordType.Name,
          Production_ID__c
        FROM Opportunity
        WHERE Id = :opportunityId
      ];
      opportunityId = opportunity.Id;

      getAssociationsByProduction(); //GET Associations PL
      getVehiclesProduction(); //GET Vehicles
      getRateDetailsProduction(); //GET Rate Details (Concessions)
      searchItinerary(); // GET Itinerary/Ground
      searchTrip(); //GET Trip Tab
      vfpConfiguration.productionId = opportunityId;
      vfpConfiguration.productionName = opportunity.Alias_With_Production_Name__c;
      vfpConfiguration.parentSObject = 'Air';
      Map<Id, DashboardClientWrapper> clientsMap = new Map<Id, DashboardClientWrapper>();
      for (Production_Associations__c pa : [
        SELECT
          Id,
          Production_Opp__c,
          Contact__c,
          Contact__r.FirstName,
          Contact__r.LastName,
          Contact__r.Title,
          Contact__r.Phone,
          Contact__r.MobilePhone,
          Contact__r.Work_Phone_Extension__c,
          Contact__r.Email,
          Contact__r.Alternate_Email__c,
          Contact__r.MailingStreet,
          Contact__r.MailingPostalCode,
          Contact__r.City__c,
          Contact__r.City__r.Name,
          Contact__r.Notes__c,
          Role__c
        FROM Production_Associations__c
        WHERE
          Production_Opp__c = :opportunityId
          AND Contact__c != NULL
          AND Role__c != NULL
        ORDER BY Contact__r.Name ASC
      ]) {
        if (
          pa.Role__c.contains('Primary Air') ||
          pa.Role__c.contains('CC: Air') ||
          pa.Role__c.contains('Contract Signer')
        )
          clientsMap.put(
            pa.Contact__c,
            new DashboardClientWrapper(
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
            )
          );
        //if(pa.Role__c.contains('Primary Housing')) contactAssociationPrimary = pa.Contact__c;
      }
      vfpConfiguration.clientMap = clientsMap.clone();
      for (Id clientId : clientsMap.keySet()) {
        vfpConfiguration.clientMap.put(clientId, clientsMap.get(clientId));
        vfpConfiguration.clients.add(
          new SelectOption(
            clientId,
            clientsMap.get(clientId).firstName +
            ' ' +
            clientsMap.get(clientId).lastName
          )
        );
      }
      System.debug(
        'vfpConfiguration.productionId -> ' + vfpConfiguration.productionId
      );
    }
  }

  public void getAssociationsByProduction() {
    productionCompanyPL = new List<SelectOption>();
    productionContactPL = new List<SelectOption>();
    companyContactPL = new List<SelectOption>();
    teamMembers = new List<SelectOption>();
    coordinatorGT = null;
    coordinatorGTName = null;

    Set<String> companyIds = new Set<String>();
    teamMembers.add(new SelectOption('', '---None---'));

    Map<String, String> compMap = new Map<String, String>();
    Map<String, String> prodContactMap = new Map<String, String>();

    for (Production_Associations__c pa : [
      SELECT
        Id,
        Company__c,
        Company__r.Name,
        Contact__c,
        Contact__r.Name,
        User__c,
        User__r.Name,
        Team_Roles__c,
        Production_Opp__c
      FROM Production_Associations__c
      WHERE Production_Opp__c = :opportunityId
      ORDER BY User__r.Name ASC
    ]) {
      if (pa.Company__c != null) {
        compMap.put(pa.Company__c, pa.Company__r.Name);
        companyIds.add(pa.Company__c);
      }
      if (pa.Contact__c != null)
        prodContactMap.put(pa.Contact__c, pa.Contact__r.Name);
      if (pa.User__c != null && pa.Team_Roles__c != null) {
        teamMembers.add(new SelectOption(pa.User__c, pa.User__r.Name));
        if (pa.Team_Roles__c.contains('Primary Air Coordinator')) {
          coordinatorGT = pa.User__c;
          coordinatorGTName = pa.User__r.Name;
        }
      }
    }

    for (String k1 : compMap.keySet()) {
      productionCompanyPL.add(new SelectOption(k1, compMap.get(k1)));
    }
    for (String k1 : prodContactMap.keySet()) {
      productionContactPL.add(new SelectOption(k1, prodContactMap.get(k1)));
    }

    Map<String, String> contactMap = new Map<String, String>();
    for (Contact c : [
      SELECT Id, Name
      FROM Contact
      WHERE AccountId IN :companyIds
    ])
      contactMap.put(c.Id, c.Name);
    for (AccountContactRelation acr : [
      SELECT Id, AccountId, ContactId, Contact.Name
      FROM AccountContactRelation
      WHERE AccountId IN :companyIds AND IsActive = TRUE
    ])
      contactMap.put(acr.ContactId, acr.Contact.Name);

    for (String keyc : contactMap.keySet()) {
      companyContactPL.add(new SelectOption(keyc, contactMap.get(keyc)));
    }
    vfpConfiguration.companies = productionCompanyPL.clone();
    vfpConfiguration.contacts = productionContactPL.clone();
    vfpConfiguration.companyContacts = companyContactPL.clone();
    vfpConfiguration.teamMembers = teamMembers.clone();
  }

  public void verifySales() {
    String ContractBidId = apexpages.currentpage()
      .getparameters()
      .get('ContractBidId');
    String OpenBidId = apexpages.currentpage().getparameters().get('OpenBidId');
    String ServiceId = apexpages.currentpage().getparameters().get('ServiceId');
    if (ContractBidId != null && ContractBidId != '') {
      dataBidIdsearch = ContractBidId;
      List<Bid__c> searchBid = [
        SELECT Id, Name, Air__c, Air__r.Name, Status__c, Production__c
        FROM Bid__c
        WHERE Id = :dataBidIdsearch
      ];
      if (searchBid.size() > 0) {
        opportunity = [
          SELECT
            Id,
            Name,
          Alias_With_Production_Name__c, 
            AccountId,
            Account.Name,
            Parent_Production__c,
            RecordTypeId,
            RecordType.Name
          FROM Opportunity
          WHERE Id = :searchBid[0].Production__c
        ];
        opportunityId = opportunity.Id;
        getDataProduction();
        tripViewId = searchBid[0].Air__c;
        dataBidIdsearch = searchBid[0].Id;
        if (tripViewId != null && tripViewId != '')
          viewTripDetail();
        if (searchBid[0].Status__c == 'Contracted') {
          vfpConfiguration.bidId = searchBid[0].Id;
          vfpConfiguration.bidName = searchBid[0].Name;
          vfpConfiguration.parentId = searchBid[0].Air__c;
          tabDefault = 'gt-contracting';
        }
      }
    } else if (ServiceId != null && ServiceId != '') {
      List<Air__c> searchService = [
        SELECT Id, Name, Production__c
        FROM Air__c
        WHERE Id = :ServiceId
      ];
      if (searchService.size() > 0) {
        opportunity = [
          SELECT
            Id,
            Name,
          	Alias_With_Production_Name__c, 
            AccountId,
            Account.Name,
            Parent_Production__c,
            RecordTypeId,
            RecordType.Name,
            RecordType.DeveloperName,
            Production_ID__c,
            Office_Location__c
          FROM Opportunity
          WHERE Id = :searchService[0].Production__c
        ];
        opportunityId = opportunity.Id;
        getDataProduction();
        tripViewId = searchService[0].Id;
        viewTripDetail();
        tabDefault = 'gt-trip';
      }
    } else if (OpenBidId != null && OpenBidId != '') {
      dataBidIdsearch = OpenBidId;
      List<Bid__c> searchBid = [
        SELECT Id, Name, Air__c, Air__r.Name, Status__c, Production__c
        FROM Bid__c
        WHERE Id = :dataBidIdsearch
      ];
      if (searchBid.size() > 0) {
        opportunity = [
          SELECT
            Id,
            Name,
          	Alias_With_Production_Name__c, 
            AccountId,
            Account.Name,
            Parent_Production__c,
            RecordTypeId,
            RecordType.Name
          FROM Opportunity
          WHERE Id = :searchBid[0].Production__c
        ];
        opportunityId = opportunity.Id;
        getDataProduction();
        tripViewId = searchBid[0].Air__c;
        dataBidIdsearch = searchBid[0].Id;
        if (tripViewId != null && tripViewId != '')
          viewTripDetail();
        if (searchBid[0].Status__c == 'Contracted') {
          vfpConfiguration.bidId = searchBid[0].Id;
          vfpConfiguration.bidName = searchBid[0].Name;
          vfpConfiguration.parentId = searchBid[0].Air__c;
        }
        renderBid = true;
      }
    } else {
      if (opportunityId != null && opportunityId != '') {
        List<Air__c> saleList = [
          SELECT Id, Air_Internal_Notes__c
          FROM Air__c
          WHERE
            Production__c = :opportunityId
            AND RecordType.DeveloperName = 'Sales_Air_Details'
          ORDER BY CreatedDate ASC
          LIMIT 1
        ];
        if (saleList.size() > 0)
          sales = saleList[0];
        else
          createSalesAir();
        getDataProduction(); //upsertSession(UserInfo.getUserId(),opportunityId);
      } else {
        Dashboard_Session__c ds = Dashboard_Session__c.getValues(
          UserInfo.getUserId()
        );
        dataBidIdsearch = null;
        if (ds != null && ds.Id != null && ds.Production_ID__c != null) {
          List<Opportunity> oppList = [
            SELECT
              Id,
              Name,
              Alias_With_Production_Name__c, 
              AccountId,
              Account.Name,
              Parent_Production__c,
              RecordTypeId,
              RecordType.Name
            FROM Opportunity
            WHERE Id = :ds.Production_ID__c
          ];
          if (!oppList.isEmpty()) {
            opportunity = oppList[0];
            opportunityId = ds.Production_ID__c;
            List<Air__c> saleList = [
              SELECT Id, Air_Internal_Notes__c
              FROM Air__c
              WHERE
                Production__c = :opportunityId
                AND RecordType.DeveloperName = 'Sales_Air_Details'
              ORDER BY CreatedDate ASC
              LIMIT 1
            ];
            if (saleList.size() > 0)
              sales = saleList[0];
            else
              createSalesAir();
            getDataProduction();
          }
        }
      }
    }
  }

  public static void upsertSession(String userid, String opportunityid) {
    Dashboard_Session__c ds = Dashboard_Session__c.getValues(userid);
    if (ds == null) {
      Dashboard_Session__c dsnew = new Dashboard_Session__c();
      dsnew.Production_ID__c = opportunityid;
      dsnew.SetupOwnerId = userid;
      insert dsnew;
    } else {
      ds.Production_ID__c = opportunityid;
      upsert ds;
    }
  }

  public void createSalesAir() {
    if (opportunityId != null && opportunityId != '') {
      sales = new Air__c(
        RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
          .get('Sales_Air_Details')
          .getRecordTypeId(),
        Production__c = opportunityId,
        Air_Internal_Notes__c = null
      );
      insert sales;
    }
  }

  public static Map<Object, List<String>> getDependentPicklistValues(
    Schema.sObjectField dependToken
  ) {
    Schema.DescribeFieldResult depend = dependToken.getDescribe();
    Schema.sObjectField controlToken = depend.getController();
    if (controlToken == null)
      return null;
    Schema.DescribeFieldResult control = controlToken.getDescribe();
    List<Schema.PicklistEntry> controlEntries = (control.getType() ==
      Schema.DisplayType.Boolean
      ? null
      : control.getPicklistValues());

    String base64map = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/';
    Map<Object, List<String>> dependentPicklistValues = new Map<Object, List<String>>();
    for (Schema.PicklistEntry entry : depend.getPicklistValues())
      if (entry.isActive()) {
        List<String> base64chars = String.valueOf(
            ((Map<String, Object>) JSON.deserializeUntyped(
                JSON.serialize(entry)
              ))
              .get('validFor')
          )
          .split('');
        for (
          Integer index = 0;
          index < (controlEntries != null ? controlEntries.size() : 2);
          index++
        ) {
          Object controlValue = (controlEntries == null
            ? (Object) (index == 1)
            : (Object) (controlEntries[index].isActive()
                ? controlEntries[index].getLabel()
                : null));
          Integer bitIndex = index / 6, bitShift = 5 - Math.mod(index, 6);
          if (
            controlValue == null ||
            (base64map.indexOf(base64chars[bitIndex]) & (1 << bitShift)) == 0
          )
            continue;
          if (!dependentPicklistValues.containsKey(controlValue)) {
            dependentPicklistValues.put(controlValue, new List<String>());
          }
          dependentPicklistValues.get(controlValue).add(entry.getLabel());
        }
      }
    return dependentPicklistValues;
  }

  @RemoteAction
  global static List<String> getDataEmailBid(
    String opportunityid,
    String tripid,
    String bidid,
    String primarycontact,
    String typez,
    String url
  ) {
    List<String> result = new List<String>();
    system.debug(opportunityid);
    system.debug(tripid);
    system.debug(bidid);
    system.debug(primarycontact);
    system.debug(typez);
    system.debug(url);
    //To
    String primary_name = '';
    List<Contact> contactList = [
      SELECT Id, Name, Email
      FROM Contact
      WHERE Id = :primarycontact
    ];
    if (contactList.size() > 0) {
      primary_name = contactList[0].Name;
      if (contactList[0].Email != null)
        result.add(contactList[0].Email);
      else
        result.add('');
    } else {
      result.add('');
    }

    List<Air__c> airAux = [
      SELECT
        Id,
        Name,
        RecordType.Name,
        Departure_Date__c,
        Return_Date__c,
        Departure_City__r.Airport_Code__c,
        Arrival_City__r.Airport_Code__c,
        Group_Type__c,
        Number_of_Seats__c,
        PAX__c
      FROM Air__c
      WHERE Id = :tripid
    ];
    String startDate = (airAux[0].Departure_Date__c != null
      ? Datetime.newInstance(
            airAux[0].Departure_Date__c.year(),
            airAux[0].Departure_Date__c.month(),
            airAux[0].Departure_Date__c.day()
          )
          .format('dd MMMMM yyyy')
      : '');
    String returnDate = (airAux[0].Return_Date__c != null
      ? Datetime.newInstance(
            airAux[0].Return_Date__c.year(),
            airAux[0].Return_Date__c.month(),
            airAux[0].Return_Date__c.day()
          )
          .format('dd MMMMM yyyy')
      : '');
    List<Opportunity> productionAux = [
      SELECT Id, Name, Alias_With_Production_Name__c 
      FROM Opportunity
      WHERE Id = :opportunityid
    ];
    List<Bid__c> bidAux = new List<Bid__c>();
    if (bidid != null && bidid != '')
      bidAux = [
        SELECT Id, Name, Vendor__c, Vendor__r.Name
        FROM Bid__c
        WHERE Id = :bidid
      ];
    String subject;
    String segments = '';
    String segmentsTravelDetails = '';

    List<Air__c> segmentList = [
      SELECT
        Id,
        Air_Trip_Details__c,
        Departure_Date__c,
        Return_Date__c,
        Departure_City__c,
        Arrival_City__c,
        Departure_City__r.Airport_Code__c,
        Departure_City__r.Name,
        Departure_City__r.City__c,
        Departure_City__r.City__r.Name,
        Arrival_City__r.Airport_Code__c,
        Arrival_City__r.Name,
        Arrival_City__r.City__c,
        Arrival_City__r.City__r.Name
      FROM Air__c
      WHERE
        Air_Trip_Details__c = :tripid
        AND RecordType.DeveloperName = 'Air_Segments'
    ];
    if (segmentList.size() > 0) {
      for (Air__c segment : segmentList) {
        segments =
          segments +
          (segment.Departure_City__r.Airport_Code__c != null
            ? segment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (segment.Arrival_City__r.Airport_Code__c != null
            ? segment.Arrival_City__r.Airport_Code__c
            : '') +
          ', ';
        segmentsTravelDetails =
          segmentsTravelDetails +
          '<br/>Travelling from: ' +
          (segment.Departure_City__r.Airport_Code__c != null
            ? segment.Departure_City__r.Airport_Code__c
            : '') +
          '<br/>Travelling to: ' +
          (segment.Arrival_City__r.Airport_Code__c != null
            ? segment.Arrival_City__r.Airport_Code__c
            : '') +
          '<br/>Date of travel: ' +
          (segmentList.size() < 2 ||
            segmentList.size() > 2
            ? (segment.Departure_Date__c != null
                ? DateTime.newInstance(
                      segment.Departure_Date__c,
                      Time.newInstance(0, 0, 0, 0)
                    )
                    .format('EEEE') + ', '
                : '') +
              (segment.Departure_Date__c != null
                ? Datetime.newInstance(
                      segment.Departure_Date__c.year(),
                      segment.Departure_Date__c.month(),
                      segment.Departure_Date__c.day()
                    )
                    .format('dd MMMMM yyyy')
                : '')
            : (segmentList.size() == 2
                ? (segment.Return_Date__c != null
                    ? DateTime.newInstance(
                          segment.Return_Date__c,
                          Time.newInstance(0, 0, 0, 0)
                        )
                        .format('EEEE') + ', '
                    : '') +
                  (segment.Return_Date__c != null
                    ? Datetime.newInstance(
                          segment.Return_Date__c.year(),
                          segment.Return_Date__c.month(),
                          segment.Return_Date__c.day()
                        )
                        .format('dd MMMMM yyyy')
                    : '')
                : '')) +
          '<br/>';
      }
      segments = segments.subString(0, segments.length() - 2);
    }
    system.debug(airAux);
    String body = '';
    //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
    User userActual = verifyEmailUser(
      UserInfo.getUserId(),
      opportunityid,
      tripid
    );
    if (typez == 'release_bid') {
      String BidRecordLocatorAndSeatDetails = '';
      for (Revenue__c r : [
        SELECT Id, Record_Locator__c, of_seats__c
        FROM Revenue__c
        WHERE
          Bid__c = :bidid
          AND RecordType.DeveloperName = 'Air_Rate_Commission'
      ]) {
        BidRecordLocatorAndSeatDetails =
          BidRecordLocatorAndSeatDetails +
          'Record Locator: ' +
          (r.Record_Locator__c != null ? r.Record_Locator__c : '') +
          ' , no of seats: ' +
          (r.of_seats__c != null ? String.valueOf(r.of_seats__c) : '') +
          '<br/>';
      }
      if (BidRecordLocatorAndSeatDetails == '')
        BidRecordLocatorAndSeatDetails = 'Record Locator: , no of seats:';
      else
        BidRecordLocatorAndSeatDetails = BidRecordLocatorAndSeatDetails.substring(
          0,
          BidRecordLocatorAndSeatDetails.length() - 5
        );

      List<Air__c> tripTemplate = [
        SELECT Id, Email_Subject_Release_Bid__c, Email_Body_Release_Bid__c
        FROM Air__c
        WHERE Id = :tripid
      ];
      if (
        tripTemplate.size() > 0 &&
        tripTemplate[0].Email_Body_Release_Bid__c != null &&
        tripTemplate[0].Email_Subject_Release_Bid__c != null
      ) {
        subject = tripTemplate[0]
          .Email_Subject_Release_Bid__c.unescapeHtml4()
          .replace('{ProductionName}', productionAux[0].Name)
          .replace('{DepDate}', startDate)
          .replace(
            '{DepartureCity}',
            airAux[0].Departure_City__r.Airport_Code__c != null
              ? airAux[0].Departure_City__r.Airport_Code__c
              : ''
          )
          .replace(
            '{ArrivalCity}',
            airAux[0].Arrival_City__r.Airport_Code__c != null
              ? airAux[0].Arrival_City__r.Airport_Code__c
              : ''
          );
        result.add(subject);
        body = tripTemplate[0]
          .Email_Body_Release_Bid__c.unescapeHtml4()
          .replace('{VendorName}', bidAux[0].Vendor__r.Name)
          .replace('{ProductionName}', productionAux[0].Name)
          .replace(
            '{GroupType}',
            airAux[0].Group_Type__c != null ? airAux[0].Group_Type__c : ''
          )
          .replace('{TripStartDate}', startDate)
          .replace('{TripEndDate}', returnDate)
          .replace(
            '{AirCoordinator}',
            userActual != null && userActual.Name != null ? userActual.Name : ''
          )
          .replace('{BidDescription}', segments)
          .replace(
            '{BidRecordLocatorAndSeatDetails}',
            BidRecordLocatorAndSeatDetails
          );
        result.add(body);
      } else {
        List<EmailTemplate> template = [
          SELECT Id, Name, Subject, Body, HTMLValue
          FROM EmailTemplate
          WHERE DeveloperName = 'Air_Release_Bid'
        ];
        subject = template.size() > 0
          ? template[0]
              .Subject.unescapeHtml4()
              .replace('{ProductionName}', productionAux[0].Name)
              .replace('{DepDate}', startDate)
              .replace(
                '{DepartureCity}',
                airAux[0].Departure_City__r.Airport_Code__c != null
                  ? airAux[0].Departure_City__r.Airport_Code__c
                  : ''
              )
              .replace(
                '{ArrivalCity}',
                airAux[0].Arrival_City__r.Airport_Code__c != null
                  ? airAux[0].Arrival_City__r.Airport_Code__c
                  : ''
              )
          : '';
        result.add(subject);
        if (template.size() > 0)
          body = template[0].HTMLValue != null
            ? template[0]
                .HTMLValue.unescapeHtml4()
                .replace('{VendorName}', bidAux[0].Vendor__r.Name)
                .replace('{ProductionName}', productionAux[0].Name)
                .replace(
                  '{GroupType}',
                  airAux[0].Group_Type__c != null ? airAux[0].Group_Type__c : ''
                )
                .replace('{TripStartDate}', startDate)
                .replace('{TripEndDate}', returnDate)
                .replace(
                  '{AirCoordinator}',
                  userActual != null &&
                    userActual.Name != null
                    ? userActual.Name
                    : ''
                )
                .replace('{BidDescription}', segments)
                .replace(
                  '{BidRecordLocatorAndSeatDetails}',
                  BidRecordLocatorAndSeatDetails
                )
            : '';
        result.add(body);
      }
    } else if (typez == 'release_bid2') {
      List<Air__c> tripTemplate = [
        SELECT Id, Email_Subject_Release_Bid__c, Email_Body_Release_Bid__c
        FROM Air__c
        WHERE Id = :tripid
      ];
      if (
        tripTemplate.size() > 0 &&
        tripTemplate[0].Email_Body_Release_Bid__c != null &&
        tripTemplate[0].Email_Subject_Release_Bid__c != null
      ) {
        subject = tripTemplate[0].Email_Subject_Release_Bid__c.unescapeHtml4();
        result.add(subject);
        body = tripTemplate[0].Email_Body_Release_Bid__c.unescapeHtml4();
        result.add(body);
      } else {
        List<EmailTemplate> template = [
          SELECT Id, Name, Subject, Body, HTMLValue
          FROM EmailTemplate
          WHERE DeveloperName = 'Air_Release_Bid'
        ];
        //subject = template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name).replace('{DateIn}',dateIn).replace('{DateOut}',dateOut) : '';
        subject = template.size() > 0
          ? template[0].Subject.unescapeHtml4()
          : '';
        result.add(subject);
        if (template.size() > 0)
          body = template[0].HTMLValue != null
            ? template[0].HTMLValue.unescapeHtml4()
            : '';
        result.add(body);
      }
    } else if (typez == 'send_bid_request') {
      List<Air__c> tripTemplate = [
        SELECT Id, Email_Body_Bid_Request__c
        FROM Air__c
        WHERE Id = :tripid
      ];
      if (
        tripTemplate.size() > 0 &&
        tripTemplate[0].Email_Body_Bid_Request__c != null
      ) {
        List<EmailTemplate> template = [
          SELECT Id, Name, Subject, Body, HTMLValue
          FROM EmailTemplate
          WHERE DeveloperName = 'Air_Bid_Request_All'
        ];
        subject = template.size() > 0
          ? template[0]
              .Subject.unescapeHtml4()
              .replace('{ProductionName}', productionAux[0].Name)
              .replace('{DepDate}', startDate)
              .replace(
                '{DepartureCity}',
                airAux[0].Departure_City__r.Airport_Code__c != null
                  ? airAux[0].Departure_City__r.Airport_Code__c
                  : ''
              )
              .replace(
                '{ArrivalCity}',
                airAux[0].Arrival_City__r.Airport_Code__c != null
                  ? airAux[0].Arrival_City__r.Airport_Code__c
                  : ''
              )
          : '';
        result.add(subject);
        body = tripTemplate[0]
          .Email_Body_Bid_Request__c.unescapeHtml4()
          .replace('{VendorName}', bidAux[0].Vendor__r.Name)
          .replace('{ProductionName}', productionAux[0].Name)
          .replace(
            '{GroupType}',
            airAux[0].Group_Type__c != null ? airAux[0].Group_Type__c : ''
          )
          .replace('{TravelDetails}', segmentsTravelDetails)
          .replace(
            '{AirCoordinator}',
            userActual != null && userActual.Name != null ? userActual.Name : ''
          )
          .replace(
            '{NosOfSeats}',
            airAux[0].PAX__c != null ? String.valueOf(airAux[0].PAX__c) : ''
          );
        result.add(body);
      } else {
        List<EmailTemplate> template = [
          SELECT Id, Name, Subject, Body, HTMLValue
          FROM EmailTemplate
          WHERE DeveloperName = 'Air_Bid_Request_All'
        ];
        subject = template.size() > 0
          ? template[0]
              .Subject.unescapeHtml4()
              .replace('{ProductionName}', productionAux[0].Name)
              .replace('{DepDate}', startDate)
              .replace(
                '{DepartureCity}',
                airAux[0].Departure_City__r.Airport_Code__c != null
                  ? airAux[0].Departure_City__r.Airport_Code__c
                  : ''
              )
              .replace(
                '{ArrivalCity}',
                airAux[0].Arrival_City__r.Airport_Code__c != null
                  ? airAux[0].Arrival_City__r.Airport_Code__c
                  : ''
              )
          : '';
        result.add(subject);
        if (template.size() > 0)
          body = template[0].HTMLValue != null
            ? template[0]
                .HTMLValue.unescapeHtml4()
                .replace('{VendorName}', bidAux[0].Vendor__r.Name)
                .replace('{ProductionName}', productionAux[0].Name)
                .replace(
                  '{GroupType}',
                  airAux[0].Group_Type__c != null ? airAux[0].Group_Type__c : ''
                )
                .replace('{TravelDetails}', segmentsTravelDetails)
                .replace(
                  '{AirCoordinator}',
                  userActual != null &&
                    userActual.Name != null
                    ? userActual.Name
                    : ''
                )
                .replace(
                  '{NosOfSeats}',
                  airAux[0].PAX__c != null
                    ? String.valueOf(airAux[0].PAX__c)
                    : ''
                )
            : '';
        result.add(body);
      }
    }

    result.add(productionAux[0].Name);

    return result;
  }

  public void sendPreviewPdf() {
    emailMessage = '';
    try {
      emailMessage = sendEmail(
        emailbid_to,
        emailbid_cc,
        emailbid_bcc,
        emailbid_subject,
        emailBid_body,
        emailAttachs,
        opportunityId,
        tripViewId
      );
      if (emailMessage == '') {
        Journal__c journalAux;
        if (emailbid_type == 'release_bid') {
          journalAux = new Journal__c(
            RecordTypeId = journal_bidjournalRT,
            Bid__c = emailbid_id,
            Journal_Entry__c = 'Release Bid has been sent to ' +
              emailbid_primarycontactname +
              ' at ' +
              emailbid_to
          );
          List<Bid__c> bidAux = [
            SELECT Id, Status__c
            FROM Bid__c
            WHERE Id = :emailbid_id
          ];
          if (bidAux.size() > 0 && bidAux[0].Status__c != 'Contracted') {
            Bid__c b = new Bid__c(Id = emailbid_id, Status__c = 'Bid Released');
            update b;
          }
        } else if (emailbid_type == 'send_bid_request') {
          journalAux = new Journal__c(
            RecordTypeId = journal_bidjournalRT,
            Bid__c = emailbid_id,
            Journal_Entry__c = 'Air Bid Request has been sent to ' +
              emailbid_primarycontactname +
              ' at ' +
              emailbid_to
          );
          List<Bid__c> bidAux = [
            SELECT Id, Status__c
            FROM Bid__c
            WHERE Id = :emailbid_id
          ];
          if (bidAux.size() > 0 && bidAux[0].Status__c == 'Unsent') {
            Bid__c b = new Bid__c(
              Id = emailbid_id,
              Status__c = 'Lead Sent',
              Lead_Sent__c = true
            );
            update b;
          }
        }

        if (journalAux != null)
          insert journalAux;
      }
    } catch (DMLException e) {
      system.debug(e.getMessage());
      emailMessage = e.getMessage();
    }
  }

  public static User verifyEmailUser(
    String userId,
    String productionId,
    String tripId
  ) {
    User userActual;
    Map<String, User> associationsMap = new Map<String, User>();
    Set<Id> userIds = new Set<Id>();
    for (Production_Associations__c pa : [
      SELECT
        Id,
        User__c,
        User__r.Email,
        Team_Roles__c,
        Production_Opp__c,
        Air__c
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :productionId
        AND RecordType.DeveloperName = 'Production_Coordinators'
        AND User__c != NULL
        AND Team_Roles__c != NULL
    ]) {
      if (pa.Team_Roles__c != null) {
        for (String teamrole : pa.Team_Roles__c.split(';')) {
          if (
            pa.Production_Opp__c != null &&
            teamrole.toLowerCase() != 'air back-end coordinator'
          ) {
            associationsMap.put(
              teamrole.toLowerCase(),
              new User(Id = pa.User__c)
            );
            userIds.add(pa.User__c);
          }
        }
      }
    }
    List<Air__c> airList = [
      SELECT Id, Back_end_Coordinator__c
      FROM Air__c
      WHERE Id = :tripId
    ];
    if (!airList.isEmpty()) {
      associationsMap.put(
        'air back-end coordinator',
        new User(Id = airList[0].Back_end_Coordinator__c)
      );
      userIds.add(airList[0].Back_end_Coordinator__c);
    }
    if (!associationsMap.isEmpty()) {
      for (User us : [
        SELECT Id, Name, Email, Phone
        FROM User
        WHERE Id IN :userIds
      ]) {
        for (String key : associationsMap.keySet()) {
          if (associationsMap.get(key).Id == us.Id)
            associationsMap.put(key, us);
        }
      }
      if (
        associationsMap.get('primary air coordinator') != null &&
        associationsMap.get('primary air coordinator').Id == userId
      )
        userActual = associationsMap.get('primary air coordinator');
      else if (
        associationsMap.get('air back-end coordinator') != null &&
        associationsMap.get('air back-end coordinator').Id != null
      )
        userActual = associationsMap.get('air back-end coordinator');
      else if (associationsMap.get('primary air coordinator') != null)
        userActual = associationsMap.get('primary air coordinator');
    }
    return userActual;
  }
  public void sendEmailFormWithAttachs() {
    emailMessage = '';
    try {
      emailMessage = sendEmail(
        form_to,
        form_cc,
        form_bcc,
        form_subject,
        form_body,
        emailAttachs,
        opportunityId,
        tripViewId
      );
      //getBidJournals();
    } catch (DMLException e) {
      emailMessage = e.getMessage();
    }
  }

  public static String sendEmail(
    String toList,
    String ccList,
    String bccList,
    String subject,
    String body,
    String attachs,
    String oppid,
    String tripid
  ) {
    try {
      //TO
      Set<String> toAddress = new Set<String>();
      for (String k : toList.split(',')) {
        if (k.trim() != '')
          toAddress.add(k.trim());
      }
      //CC
      Set<String> ccAddress = new Set<String>();
      for (String k : ccList.split(',')) {
        if (k.trim() != '')
          ccAddress.add(k.trim());
      }
      //BCC
      Set<String> bccAddress = new Set<String>();
      for (String k : bccList.split(',')) {
        if (k.trim() != '')
          bccAddress.add(k.trim());
      }

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: oppid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = verifyEmailUser(UserInfo.getUserId(), oppid, tripid);

      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
      if (userActual != null && userActual.Email != null)
        mail.setOrgWideEmailAddressId(verifyWideAddress(userActual.Email));
      mail.setToAddresses(new List<String>(toAddress));
      if (ccAddress.size() > 0)
        mail.setCcAddresses(new List<String>(ccAddress));
      if (bccAddress.size() > 0)
        mail.setBccAddresses(new List<String>(bccAddress));
      mail.setSubject(subject);
      mail.setHtmlBody(body);

      if (attachs != null) {
        Set<String> attachIds = new Set<String>();
        for (String att : attachs.split(',')) {
          if (att.trim() != '')
            attachIds.add(att.trim());
        }
        system.debug(attachIds);
        //Attachment
        List<ContentVersion> contentVersions = [
          SELECT Id, ContentDocumentId, Title, PathOnClient, VersionData
          FROM ContentVersion
          WHERE ContentDocumentId IN :attachIds
        ];
        List<Messaging.Emailfileattachment> fileAttachments = new List<Messaging.Emailfileattachment>();
        if (contentVersions.size() > 0) {
          Messaging.Emailfileattachment efa;
          for (ContentVersion cv : contentVersions) {
            efa = new Messaging.Emailfileattachment();
            efa.setFileName(
              cv.PathOnClient.subString(1, cv.PathOnClient.length())
            );
            efa.setBody(cv.VersionData);
            fileAttachments.add(efa);
          }
        }
        if (fileAttachments.size() > 0)
          mail.setFileAttachments(fileAttachments);
      }
      system.debug(mail.getToAddresses());
      system.debug(mail.getCcAddresses());
      system.debug(mail.getBccAddresses());
      myEmails.add(mail);
      Messaging.SendEmailResult[] mailResult = Messaging.sendEmail(myEmails);
      if (!mailResult[0].isSuccess()) {
        system.debug(mailResult[0].getErrors()[0].getMessage());
        return mailResult[0].getErrors()[0].getMessage();
      }
    } catch (System.EmailException e) {
      system.debug(e.getMessage());
      return e.getMessage();
    }
    return '';
  }

  public void getSymbol() {
    symbolMap = new Map<String, String>();
    for (
      SelectOption so : AirDashboardController.PickThePicklist(
        'Revenue__c',
        'CurrencyIsoCode'
      )
    )
      symbolMap.put(so.getValue(), '');

    symbolMap.put('AED', 'د.إ');
    symbolMap.put('AFN', 'Af');
    symbolMap.put('ALL', 'L');
    symbolMap.put('AMD', 'Դ');
    symbolMap.put('AOA', 'Kz');
    symbolMap.put('ARS', '$');
    symbolMap.put('AUD', '$');
    symbolMap.put('AWG', 'ƒ');
    symbolMap.put('AZN', 'ман');
    symbolMap.put('BAM', 'КМ');
    symbolMap.put('BBD', '$');
    symbolMap.put('BDT', '৳');
    symbolMap.put('BGN', 'лв');
    symbolMap.put('BHD', 'ب.د');
    symbolMap.put('BIF', '₣');
    symbolMap.put('BMD', '$');
    symbolMap.put('BND', '$');
    symbolMap.put('BOB', 'Bs.');
    symbolMap.put('BRL', 'R$');
    symbolMap.put('BSD', '$');
    symbolMap.put('BTN', '');
    symbolMap.put('BWP', 'P');
    symbolMap.put('BYN', 'Br');
    symbolMap.put('BZD', '$');
    symbolMap.put('CAD', '$');
    symbolMap.put('CDF', '₣');
    symbolMap.put('CHF', '₣');
    symbolMap.put('CLP', '$');
    symbolMap.put('CNY', '¥');
    symbolMap.put('COP', '$');
    symbolMap.put('CRC', '₡');
    symbolMap.put('CUP', '$');
    symbolMap.put('CVE', '$');
    symbolMap.put('CZK', 'Kč');
    symbolMap.put('DJF', '₣');
    symbolMap.put('DKK', 'kr');
    symbolMap.put('DOP', '$');
    symbolMap.put('DZD', 'د.ج');
    symbolMap.put('EGP', '£');
    symbolMap.put('ERN', 'Nfk');
    symbolMap.put('ETB', '');
    symbolMap.put('EUR', '€');
    symbolMap.put('FJD', '$');
    symbolMap.put('FKP', '£');
    symbolMap.put('GBP', '£');
    symbolMap.put('GEL', 'ლ');
    symbolMap.put('GHS', '₵');
    symbolMap.put('GIP', '£');
    symbolMap.put('GMD', 'D');
    symbolMap.put('GNF', '₣');
    symbolMap.put('GTQ', 'Q');
    symbolMap.put('GYD', '$');
    symbolMap.put('HKD', '$');
    symbolMap.put('HNL', 'L');
    symbolMap.put('HRK', 'Kn');
    symbolMap.put('HTG', 'G');
    symbolMap.put('HUF', 'Ft');
    symbolMap.put('IDR', 'Rp');
    symbolMap.put('ILS', '₪');
    symbolMap.put('INR', '₹');
    symbolMap.put('IQD', 'ع.د');
    symbolMap.put('IRR', '﷼');
    symbolMap.put('ISK', 'Kr');
    symbolMap.put('JMD', '$');
    symbolMap.put('JOD', 'د.ا');
    symbolMap.put('JPY', '¥');
    symbolMap.put('KES', 'Sh');
    symbolMap.put('KGS', '');
    symbolMap.put('KHR', '៛');
    symbolMap.put('KPW', '₩');
    symbolMap.put('KRW', '₩');
    symbolMap.put('KWD', 'د.ك');
    symbolMap.put('KYD', '$');
    symbolMap.put('KZT', '〒');
    symbolMap.put('LAK', '₭');
    symbolMap.put('LBP', 'ل.ل');
    symbolMap.put('LKR', 'Rs');
    symbolMap.put('LRD', '$');
    symbolMap.put('LSL', 'L');
    symbolMap.put('LYD', 'ل.د');
    symbolMap.put('MAD', 'د.م.');
    symbolMap.put('MDL', 'L');
    symbolMap.put('MGA', '');
    symbolMap.put('MKD', 'ден');
    symbolMap.put('MMK', 'K');
    symbolMap.put('MNT', '₮');
    symbolMap.put('MOP', 'P');
    symbolMap.put('MRU', 'UM');
    symbolMap.put('MUR', '₨');
    symbolMap.put('MVR', 'ރ.');
    symbolMap.put('MWK', 'MK');
    symbolMap.put('MXN', '$');
    symbolMap.put('MYR', 'RM');
    symbolMap.put('MZN', 'MTn');
    symbolMap.put('NAD', '$');
    symbolMap.put('NGN', '₦');
    symbolMap.put('NIO', 'C$');
    symbolMap.put('NOK', 'kr');
    symbolMap.put('NPR', '₨');
    symbolMap.put('NZD', '$');
    symbolMap.put('OMR', 'ر.ع.');
    symbolMap.put('PAB', 'B/.');
    symbolMap.put('PEN', 'S/.');
    symbolMap.put('PGK', 'K');
    symbolMap.put('PHP', '₱');
    symbolMap.put('PKR', '₨');
    symbolMap.put('PLN', 'zł');
    symbolMap.put('PYG', '₲');
    symbolMap.put('QAR', 'ر.ق');
    symbolMap.put('RON', 'L');
    symbolMap.put('RSD', 'din');
    symbolMap.put('RUB', 'р.');
    symbolMap.put('RWF', '₣');
    symbolMap.put('SAR', 'ر.س');
    symbolMap.put('SBD', '$');
    symbolMap.put('SCR', '₨');
    symbolMap.put('SDG', '£');
    symbolMap.put('SEK', 'kr');
    symbolMap.put('SGD', '$');
    symbolMap.put('SHP', '£');
    symbolMap.put('SLL', 'Le');
    symbolMap.put('SOS', 'Sh');
    symbolMap.put('SRD', '$');
    symbolMap.put('STN', 'Db');
    symbolMap.put('SYP', 'ل.س');
    symbolMap.put('SZL', 'L');
    symbolMap.put('THB', '฿');
    symbolMap.put('TJS', 'ЅМ');
    symbolMap.put('TMT', 'm');
    symbolMap.put('TND', 'د.ت');
    symbolMap.put('TOP', 'T$');
    symbolMap.put('TRY', '₤');
    symbolMap.put('TTD', '$');
    symbolMap.put('TWD', '$');
    symbolMap.put('TZS', 'Sh');
    symbolMap.put('UAH', '₴');
    symbolMap.put('UGX', 'Sh');
    symbolMap.put('USD', '$');
    symbolMap.put('UYU', '$');
    symbolMap.put('UZS', '');
    symbolMap.put('VEF', 'Bs F');
    symbolMap.put('VND', '₫');
    symbolMap.put('VUV', 'Vt');
    symbolMap.put('WST', 'T');
    symbolMap.put('XAF', '₣');
    symbolMap.put('XCD', '$');
    symbolMap.put('XPF', '₣');
    symbolMap.put('YER', '﷼');
    symbolMap.put('ZAR', 'R');
    symbolMap.put('ZMW', 'ZK');
    symbolMap.put('ZWL', '$');
  }

  @RemoteAction
  global static Map<String, String> validateDates(
    String traceDate,
    String decisionDueDate
  ) {
    Map<String, String> response = new Map<String, String>();
    Date todayDate = system.today();
    system.debug(traceDate);
    system.debug(parseDate(traceDate));
    system.debug(todayDate);
    if (traceDate != '' && parseDate(traceDate) < todayDate) {
      response.put('newtrip_tracedate', 'Cannot post-date for trace date');
    }
    if (decisionDueDate != '' && parseDate(decisionDueDate) < todayDate) {
      response.put(
        'newtrip_decisionduedate',
        'Cannot post-date for decision due date'
      );
    }
    return response;
  }

  @RemoteAction
  global static Map<String, String> validateDatesForToday(String data) {
    Map<String, String> response = new Map<String, String>();
    Date todayDate = system.today();

    Map<String, Object> datesMap = (Map<String, Object>) JSON.deserializeUntyped(
      data
    );
    system.debug(datesMap);
    String dataDate;
    for (String key : datesMap.keySet()) {
      dataDate = (String) datesMap.get(key);
      if (
        key != '' &&
        dataDate.split('=')[1] != '' &&
        parseDate(dataDate.split('=')[1]) < todayDate
      ) {
        response.put(key, dataDate.split('=')[0]);
      }
    }
    return response;
  }

  @RemoteAction
  global static Boolean validateDatesCompare(String date1, String date2) {
    if (parseDate(date1) > parseDate(date2)) {
      return true;
    }
    return false;
  }

  public static Date parseDate(String inDate) {
    Date dateRes = null;
    //	1 - Try locale specific mm/dd/yyyy or dd/mm/yyyy
    try {
      String candDate = inDate.substring(0, Math.min(10, inDate.length())); // grab date portion only m[m]/d[d]/yyyy , ignore time
      dateRes = Date.parse(candDate);
    } catch (Exception e) {
    }
    if (dateRes == null) {
      //	2 - Try yyyy-mm-dd
      try {
        String candDate = inDate.substring(0, 10); // grab date portion only, ignore time, if any
        dateRes = Date.valueOf(candDate);
      } catch (Exception e) {
      }
    }
    return dateRes;
    /*Date dateRes = null;
        try {
            dateRes = Date.parse(inDate);
        }
        catch (Exception e) { 
            system.debug(e.getMessage());
            try {
                dateRes = Date.valueOf(inDate);
            }
            catch (Exception e2) { 
                system.debug(e2.getMessage());
            }  
        }  
        return dateRes;**/
  }

  /*@RemoteAction
    global static String searchAircraftTrip(String query, String tripid){
        query = '%' + query + '%';
        List<wrapperData> aircraftList = new List<wrapperData>();
        String description;
        for(Ground__c g : [SELECT Id, Vehicle_Ref__c FROM Ground__c WHERE Vehicle_Ref__c LIKE: query AND GT_Trip_Details__c =: tripid  AND RecordType.Name = 'Vehicle Type' AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL]){
            aircraftList.add(new wrapperData(g.Vehicle_Ref__c,g.Vehicle_Ref__c,''));
        }
        return JSON.serialize(aircraftList);
    }*/

  @RemoteAction
  global static Contact getDataContact(String contactId) {
    return [
      SELECT
        Id,
        AccountId,
        FirstName,
        LastName,
        Phone,
        Work_Phone_Extension__c,
        Email,
        MobilePhone,
        Alternate_Email__c,
        Fax,
        Designation_title__c,
        Description,
        MailingStreet,
        MailingPostalCode,
        OtherStreet,
        City__c,
        City__r.Name
      FROM Contact
      WHERE Id = :contactId
    ];
  }

  @RemoteAction
  global static Journal__c getDataJournal(String journalId) {
    return [
      SELECT
        Id,
        Housing__c,
        Issue__c,
        Journal_Entry__c,
        Mark_Journal_trace_complete__c,
        Parent_Journal__c,
        Production__c,
        Production_checkbox__c,
        RecordTypeId,
        RecordType.Name,
        Sales__c,
        Trace_Coordinator__c,
        Trace_Date__c,
        Trace_Date_Formula__c,
        Vendor_Checkbox__c
      FROM Journal__c
      WHERE Id = :journalId
    ];
  }

  @RemoteAction
  global static List<String> getDataJournalRelated(
    String journalId,
    String ztype
  ) {
    List<String> dataList = new List<String>();
    /*if(ztype == 'production_companies'){
            for(Related_Companies__c rc : [SELECT Id, Company__c FROM Related_Companies__c WHERE Journal__c =: journalId AND Company__c <> null]) dataList.add(rc.Company__c);
        }*/
    if (ztype == 'production_contacts') {
      for (Related_Contact__c rc : [
        SELECT Id, Contact__c
        FROM Related_Contact__c
        WHERE
          Journal__c = :journalId
          AND Contact__c != NULL
          AND Type__c INCLUDES ('Production Contacts')
      ])
        dataList.add(rc.Contact__c);
    }
    if (ztype == 'company_contacts') {
      for (Related_Contact__c rc : [
        SELECT Id, Contact__c
        FROM Related_Contact__c
        WHERE
          Journal__c = :journalId
          AND Contact__c != NULL
          AND Type__c INCLUDES ('Company Contacts')
      ])
        dataList.add(rc.Contact__c);
    }
    system.debug(dataList);
    return dataList;
  }

  @RemoteAction
  global static String searchCreditCard(String query, String opportunityId) {
    query = '%' + query + '%';
    Set<String> contactIds = new Set<String>();
    for (Production_Associations__c pa : [
      SELECT Id, Contact__c
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :opportunityId
        AND Contact__c != NULL
        AND RecordType.Name = 'Production Contacts'
        AND Status__c = 'Associated'
    ]) {
      contactIds.add(pa.Contact__c);
    }
    system.debug(contactIds);

    List<wrapperData> ccList = new List<wrapperData>();
    for (Credit_Card__c cc : [
      SELECT
        Id,
        Credit_card_number__c,
        Contact__r.Name,
        Credit_Card_Full_Name__c
      FROM Credit_Card__c
      WHERE
        Contact__c IN :contactIds
        AND Purpose__c INCLUDES (
          'All',
          'Ground Transportation Only',
          'Secondary'
        )
        AND (Credit_Card_Full_Name__c LIKE :query
        OR Name LIKE :query)
    ]) {
      ccList.add(new wrapperData(cc.Id, cc.Credit_Card_Full_Name__c, ''));
    }
    system.debug(ccList);

    return JSON.serialize(ccList);
  }

  @RemoteAction
  global static String searchCity(String query) {
    query = '%' + query + '%';
    List<wrapperData> cityList = new List<wrapperData>();
    for (City__c c : [
      SELECT Id, Name
      FROM City__c
      WHERE Name LIKE :query
      LIMIT 20
    ]) {
      cityList.add(new wrapperData(c.Id, c.Name, ''));
    }
    return JSON.serialize(cityList);
  }

  @RemoteAction
  global static String searchAccount(String query, String recordtype) {
    query = '%' + query + '%';
    List<wrapperData> accountList = new List<wrapperData>();
    for (Account a : [
      SELECT Id, Name
      FROM Account
      WHERE Name LIKE :query AND RecordType.Name = :recordtype
      LIMIT 20
    ]) {
      accountList.add(new wrapperData(a.Id, a.Name, ''));
    }
    return JSON.serialize(accountList);
  }

  @RemoteAction
  global static String searchAirport(String query) {
    query = '%' + query + '%';
    List<wrapperData> airportList = new List<wrapperData>();
    String nameAux;
    for (Airport__c a : [
      SELECT Id, Name, Airport_Code__c, City__c, City__r.Name
      FROM Airport__c
      WHERE Name LIKE :query OR Airport_Code__c LIKE :query
      LIMIT 20
    ]) {
      nameAux =
        (a.Airport_Code__c != null ? a.Airport_Code__c + ' - ' : '') +
        a.Name +
        (a.City__c != null ? ' - ' + a.City__r.Name : '');
      airportList.add(new wrapperData(a.Id, nameAux, ''));
    }
    return JSON.serialize(airportList);
  }

  @RemoteAction
  global static String searchVenue(String query) {
    query = '%' + query + '%';
    List<wrapperData> venueList = new List<wrapperData>();
    for (Account a : [
      SELECT Id, Name
      FROM Account
      WHERE Name LIKE :query
      LIMIT 20
    ]) {
      venueList.add(new wrapperData(a.Id, a.Name, ''));
    }
    return JSON.serialize(venueList);
  }

  @RemoteAction
  global static String searchProd(String query, Boolean all) {
    query = '%' + query + '%';
    List<wrapperDataProd> prodList = new List<wrapperDataProd>();
    List<Opportunity> productionList;
    if (!all)
      productionList = [
        SELECT Id, Name, Alias_With_Production_Name__c, StageName, Office_Location__c, Company__c
        FROM Opportunity
        WHERE Name LIKE :query AND StageName = 'Active'
        LIMIT 10
      ];
    else
      productionList = [
        SELECT Id, Name, Alias_With_Production_Name__c, StageName, Office_Location__c, Company__c
        FROM Opportunity
        WHERE Name LIKE :query
        LIMIT 10
      ];

    for (Opportunity o : productionList) {
      prodList.add(
        new wrapperDataProd(
          o.Id,
          o.Name,
          o.StageName,
          o.Company__c != null ? o.Company__c : '',
          o.Office_Location__c != null ? o.Office_Location__c : ''
        )
      );
    }
    return JSON.serialize(prodList);
  }

  @RemoteAction
  global static String searchContactByAccount(String query, String accountId) {
    query = '%' + query + '%';
    Map<String, Contact> contactMap = new Map<String, Contact>();
    for (Contact c : [
      SELECT Id, Name, Email
      FROM Contact
      WHERE AccountId = :accountId AND Name LIKE :query AND Email != NULL
    ])
      contactMap.put(c.Id, c);

    for (AccountContactRelation acr : [
      SELECT Id, ContactId, Contact.Name, Contact.Email
      FROM AccountContactRelation
      WHERE
        AccountId = :accountId
        AND Contact.Name LIKE :query
        AND Contact.Email != NULL
    ])
      contactMap.put(acr.ContactId, acr.Contact);

    List<wrapperData> contactList = new List<wrapperData>();
    for (String key : contactMap.keySet())
      contactList.add(
        new wrapperData(
          key,
          contactMap.get(key).Name +
          ' <' +
          contactMap.get(key).Email +
          '>',
          contactMap.get(key).Email
        )
      );
    return JSON.serialize(contactList);
  }

  public static String validateError(String error) {
    String message = '';
    if (error.contains('DUPLICATES_DETECTED'))
      message = 'You\'re creating a duplicate record. We recommend you use an existing record.';
    else
      message = error;
    return message;
  }

  global class wrapperSearchPL {
    public String dataid;
    public String dataname;
    public wrapperSearchPL(String cdataid, String cdataname) {
      dataid = cdataid;
      dataname = cdataname;
    }
  }

  global class wrapperVendor {
    public String vendorid;
    public String vendorname;
    public wrapperVendor(String cvendorid, String cvendorname) {
      vendorid = cvendorid;
      vendorname = cvendorname;
    }
  }

  global class wrapperData {
    public String data;
    public String value;
    public String extra1;

    public wrapperData(String cdata, String cvalue, String cextra1) {
      data = cdata;
      value = cvalue;
      extra1 = cextra1;
    }
  }

  global class wrapperDataProd {
    public String data;
    public String value;
    public String extra1;
    public String extra2;
    public String extra3;

    public wrapperDataProd(
      String cdata,
      String cvalue,
      String cextra1,
      String cextra2,
      String cextra3
    ) {
      data = cdata;
      value = cvalue;
      extra1 = cextra1;
      extra2 = cextra2;
      extra3 = cextra3;
    }
  }

  //Air Trip Wrappers.
  global class ContactWrapper {
    public Contact c { get; set; }
    public Boolean selected { get; set; }
    public Boolean disabled { get; set; }

    public ContactWrapper(Contact cc, Boolean cselected, Boolean cdisabled) {
      c = cc;
      selected = cselected;
      disabled = cdisabled;
    }
  }
  //End Air Trip Wrappers.

  public static List<SelectOption> PickThePicklist(
    string YourObjectName,
    string YourFieldName
  ) {
    List<SelectOption> picklists = new List<SelectOption>();
    List<Schema.PicklistEntry> PicklistValues = Schema.getGlobalDescribe()
      .get(YourObjectName)
      .getDescribe()
      .fields.getMap()
      .get(YourFieldName)
      .getDescribe()
      .getPicklistValues();
    for (Schema.PicklistEntry PicklistValue : PicklistValues) {
      if (YourFieldName == 'CurrencyIsoCode') {
        picklists.add(
          new SelectOption(
            PicklistValue.getValue(),
            PicklistValue.getValue() +
            ' - ' +
            PicklistValue.getLabel()
          )
        );
      } else {
        picklists.add(
          new SelectOption(PicklistValue.getValue(), PicklistValue.getLabel())
        );
      }
    }
    return picklists;
  }

  public static String verifyWideAddress(String email) {
    String oweaId;
    List<OrgWideEmailAddress> oweaList;
    if (Test.isRunningTest())
      oweaList = [
        SELECT Id
        FROM OrgWideEmailAddress
        WHERE Address = :Dashboard__c.getOrgDefaults().Email_Default__c
      ];
    else
      oweaList = [SELECT Id FROM OrgWideEmailAddress WHERE Address = :email];
    if (oweaList.isEmpty())
      oweaList = [
        SELECT Id
        FROM OrgWideEmailAddress
        WHERE Address = :Dashboard__c.getOrgDefaults().Email_Default__c
      ]; //Email default
    oweaId = oweaList.isEmpty() ? '' : oweaList[0].Id;
    return oweaId;
  }
  //Air Trip PreviewOptions Methods.
  public void openPreviewOptions() {
    Map<Id, Air__c> itinerariesMap = new Map<Id, Air__c>();
    Map<Id, Air__c> deviationsMap = new Map<Id, Air__c>();
    Map<Id, String> rateDetailsMap = new Map<Id, String>();
    Map<Id, Integer> deviationsOrderMap = new Map<Id, Integer>();
    Integer deviationOrder = 1;
    User user = [
      SELECT id, Housing_Preference__c
      FROM User
      WHERE id = :UserInfo.getUserId()
    ];
    for (Air__c air : [
      SELECT
        id,
        Air_Itinerary_Details__c,
        Air_Itinerary_Details__r.Bid_Itinerary__c,
        Air_Deviation_Details__c,
        Order__c,
        Departure_Date__c,
        Dep_Time__c,
        Departure_City__c,
        Departure_City__r.Name,
        Arrival_Date__c,
        Arr_Time__c,
        Arrival_City__c,
        Arrival_City__r.Name,
        Flight_No__c,
        Flight_Duration_hrs__c,
        Flight_Duration_Mins__c,
        Class__c,
        Equip_Type__c,
        Number_of_Seats__c,
        Operated_by__c
      FROM Air__c
      WHERE
        ((Air_Itinerary_Details__r.Bid_Itinerary__r.Air__c = :tripView.id
        AND Air_Itinerary_Details__r.Bid_Itinerary__r.Options__c != NULL)
        OR (Air_Deviation_Details__r.Bid_Deviation__r.Air__c = :tripView.id
        AND Air_Deviation_Details__r.Bid_Deviation__r.Options__c != NULL))
        AND RecordType.DeveloperName = 'Air_Segments'
      ORDER BY Departure_Date__c
    ]) {
      if (String.isNotEmpty(air.Air_Itinerary_Details__c)) {
        if (!itinerariesMap.containsKey(air.Air_Itinerary_Details__c))
          itinerariesMap.put(
            air.Air_Itinerary_Details__c,
            new Air__c(
              id = air.Air_Itinerary_Details__c,
              Bid_Itinerary__c = air.Air_Itinerary_Details__r.Bid_Itinerary__c,
              Travel_Date_Conga__c = air.Departure_Date__c,
              Travel_Information_Conga__c = ''
            )
          );
        itinerariesMap.get(air.Air_Itinerary_Details__c)
            .Travel_Information_Conga__c +=
          '<tr><td width="726"><table width="740" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><thead><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><td width="726" height="20" align="left" style="padding:3px 4px;border-bottom:1px solid black;font-size:14px;"><strong>' +
          (air.Departure_Date__c != null
            ? Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                )
            : '') +
          '</strong>' +
          (air.Departure_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE')
                .toUpperCase()
            : '') +
          '</td></tr></table></td></tr></thead><tbody><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><th width="70" height="20" align="left" style="padding:3px 4px;">FROM</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_City__c != null ? air.Departure_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">FLT #</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Flight_No__c) ? air.Flight_No__c : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">TO</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Arrival_City__c != null ? air.Arrival_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">DEPARTS</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Dep_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Dep_Time__c)
                .format('h:mm a')
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">DUR</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Flight_Duration_hrs__c != null
            ? String.valueOf(air.Flight_Duration_hrs__c) + 'HRS '
            : '') +
          (air.Flight_Duration_Mins__c != null
            ? String.valueOf(air.Flight_Duration_Mins__c) + 'MINS'
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">ARRIVES</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Arr_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Arr_Time__c)
                .format('h:mm a')
            : '') +
          (air.Departure_Date__c != null &&
            air.Arrival_Date__c != null &&
            !air.Departure_Date__c.isSameDay(air.Arrival_Date__c)
            ? ' - <strong style="color:red;">' +
              Datetime.newInstance(
                  air.Arrival_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                ) +
              '</strong>'
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;"></th><td width="253" height="20" align="left" style="padding:3px 4px;"></td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">AIRCRAFT</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Equip_Type__c) ? air.Equip_Type__c : '') +
          '</td></tr></table></td></tr></tbody></table></td></tr>';
      } else {
        if (!deviationsMap.containsKey(air.Air_Deviation_Details__c))
          deviationsMap.put(
            air.Air_Deviation_Details__c,
            new Air__c(
              id = air.Air_Deviation_Details__c,
              Travel_Information_Conga__c = ''
            )
          );
        deviationsMap.get(air.Air_Deviation_Details__c)
            .Travel_Information_Conga__c +=
          '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top"><thead><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><td width="726" height="20" align="left" style="padding:3px 4px;border-bottom:1px solid black;font-size:14px;"><strong>' +
          (air.Departure_Date__c != null
            ? Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                )
            : '') +
          '</strong>' +
          (air.Departure_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  air.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('EEEE')
                .toUpperCase()
            : '') +
          '</td></tr></table></td></tr></thead><tbody><tr><td width="726" height="20" align="left" valign="top"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><tr><th width="70" height="20" align="left" style="padding:3px 4px;">FROM</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_City__c != null ? air.Departure_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">FLT #</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Flight_No__c) ? air.Flight_No__c : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">TO</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Arrival_City__c != null ? air.Arrival_City__r.Name : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">DEPARTS</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Dep_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Dep_Time__c)
                .format('h:mm a')
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;">DUR</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Flight_Duration_hrs__c != null
            ? String.valueOf(air.Flight_Duration_hrs__c) + 'HRS '
            : '') +
          (air.Flight_Duration_Mins__c != null
            ? String.valueOf(air.Flight_Duration_Mins__c) + 'MINS'
            : '') +
          '</td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">ARRIVES</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (air.Departure_Date__c != null &&
            air.Arr_Time__c != null
            ? Datetime.newInstance(air.Departure_Date__c, air.Arr_Time__c)
                .format('h:mm a')
            : '') +
          (air.Departure_Date__c != null &&
            air.Arrival_Date__c != null &&
            !air.Departure_Date__c.isSameDay(air.Arrival_Date__c)
            ? ' - <strong style="color:red;">' +
              Datetime.newInstance(
                  air.Arrival_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format(
                  user.Housing_Preference__c == 'RRE'
                    ? 'dd-MMM-yyyy'
                    : 'MMM-dd-yyyy'
                ) +
              '</strong>'
            : '') +
          '</td></tr><tr><th width="70" height="20" align="left" style="padding:3px 4px;"></th><td width="253" height="20" align="left" style="padding:3px 4px;"></td><th width="10" height="20" align="left" style="padding:3px 4px;"></th><th width="90" height="20" align="left" style="padding:3px 4px;">AIRCRAFT</th><td width="253" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
          (String.isNotBlank(air.Equip_Type__c) ? air.Equip_Type__c : '') +
          '</td></tr></table></td></tr></tbody></table></td></tr>';
      }
    }
    for (Revenue__c rate : [
      SELECT
        id,
        Bid__c,
        Rate_currency__c,
        Service_Fees__c,
        Additional_Fees__c,
        Total_Taxes__c,
        Total_Price__c,
        of_seats__c,
        Record_Locator__c,
        Deviation__c
      FROM Revenue__c
      WHERE
        Bid__r.Air__c = :tripView.id
        AND Bid__r.Options__c != NULL
        AND RecordType.DeveloperName = 'Air_Rate_Commission'
    ]) {
      if (
        !rateDetailsMap.containsKey(
          String.isNotEmpty(rate.Deviation__c) ? rate.Deviation__c : rate.Bid__c
        )
      )
        rateDetailsMap.put(
          String.isNotEmpty(rate.Deviation__c)
            ? rate.Deviation__c
            : rate.Bid__c,
          ''
        );
      rateDetailsMap.put(
        String.isNotEmpty(rate.Deviation__c) ? rate.Deviation__c : rate.Bid__c,
        rateDetailsMap.get(
          String.isNotEmpty(rate.Deviation__c) ? rate.Deviation__c : rate.Bid__c
        ) +
        '<tr><td width="110" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Rate_currency__c != null
          ? '$ ' + String.valueOf(rate.Rate_currency__c)
          : '') +
        '</td><td width="106" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Total_Taxes__c != null
          ? '$ ' + String.valueOf(rate.Total_Taxes__c)
          : '') +
        '</td><td width="110" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Service_Fees__c != null
          ? '$ ' + String.valueOf(rate.Service_Fees__c)
          : '') +
        '</td><td width="140" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.Total_Price__c != null
          ? '$ ' + String.valueOf(rate.Total_Price__c)
          : '') +
        '</td><td width="140" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (String.isNotBlank(rate.Record_Locator__c)
          ? rate.Record_Locator__c
          : '') +
        '</td><td width="120" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black;">' +
        (rate.of_seats__c != null ? String.valueOf(rate.of_seats__c) : '') +
        '</td></tr>'
      );
    }
    for (Air__c itinerary : itinerariesMap.values())
      itinerary.Travel_Information_Conga__c =
        '<table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top">' +
        (rateDetailsMap.containsKey(itinerary.Bid_Itinerary__c)
          ? '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">BASE FARE</th><th width="106" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TAXES</th><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">SERVICE FEE</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TOTAL PER TICKET</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">RECORD LOCATOR</th><th width="120" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;"># OF SEATS</th></tr></thead><tbody>' +
            rateDetailsMap.get(itinerary.Bid_Itinerary__c) +
            '</tbody></table></td></tr>'
          : '') +
        (rateDetailsMap.containsKey(itinerary.Bid_Itinerary__c)
          ? '<tr><td width="726" height="20"></td></tr>'
          : '') +
        itinerary.Travel_Information_Conga__c +
        '</table>';
    for (Air__c deviation : deviationsMap.values())
      deviation.Travel_Information_Conga__c =
        '<table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="top">' +
        (rateDetailsMap.containsKey(deviation.id)
          ? '<tr><td width="726"><table width="726" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">BASE FARE</th><th width="106" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TAXES</th><th width="110" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">SERVICE FEE</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">TOTAL PER TICKET</th><th width="140" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;">RECORD LOCATOR</th><th width="120" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black;"># OF SEATS</th></tr></thead><tbody>' +
            rateDetailsMap.get(deviation.id) +
            '</tbody></table></td></tr>'
          : '') +
        (rateDetailsMap.containsKey(deviation.id)
          ? '<tr><td width="726" height="20"></td></tr>'
          : '') +
        deviation.Travel_Information_Conga__c +
        '</table>';
    for (Air__c deviation : [
      SELECT id, Bid_Deviation__c
      FROM Air__c
      WHERE id IN :deviationsMap.keySet()
    ]) {
      if (!deviationsOrderMap.containsKey(deviation.Bid_Deviation__c))
        deviationsOrderMap.put(deviation.Bid_Deviation__c, 0);
      deviationsOrderMap.put(
        deviation.Bid_Deviation__c,
        deviationsOrderMap.get(deviation.Bid_Deviation__c) + 1
      );
      deviationsMap.get(deviation.id)
        .Deviation_Order_Conga__c = deviationsOrderMap.get(
        deviation.Bid_Deviation__c
      );
    }
    try {
      if (!itinerariesMap.values().isEmpty())
        update itinerariesMap.values();
      if (!deviationsMap.values().isEmpty())
        update deviationsMap.values();
    } catch (DmlException e) {
      System.debug(
        'AirDashboardController.openPreviewOptions() - DmlException: ' +
        e.getMessage()
      );
    }
    String airSegmentCities = '';
    for (Air__c airSegment : [
      SELECT
        Id,
        Air_Trip_Details__c,
        Departure_Date__c,
        Return_Date__c,
        Departure_City__c,
        Arrival_City__c,
        Departure_City__r.Airport_Code__c,
        Departure_City__r.Name,
        Departure_City__r.City__c,
        Departure_City__r.City__r.Name,
        Arrival_City__r.Airport_Code__c,
        Arrival_City__r.Name,
        Arrival_City__r.City__c,
        Arrival_City__r.City__r.Name
      FROM Air__c
      WHERE
        Air_Trip_Details__c = :tripView.Id
        AND RecordType.DeveloperName = 'Air_Segments'
    ]) {
      airSegmentCities = String.isNotBlank(airSegmentCities)
        ? airSegmentCities +
          ', ' +
          (airSegment.Departure_City__r.Airport_Code__c != null
            ? airSegment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (airSegment.Arrival_City__r.Airport_Code__c != null
            ? airSegment.Arrival_City__r.Airport_Code__c
            : '')
        : (airSegment.Departure_City__r.Airport_Code__c != null
            ? airSegment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (airSegment.Arrival_City__r.Airport_Code__c != null
            ? airSegment.Arrival_City__r.Airport_Code__c
            : '');
    }
    List<Bid__c> contractedBids = [
      SELECT Id, Client_Deposit_Due_Date__c
      FROM Bid__c
      WHERE
        Air__c = :tripView.Id
        AND RecordType.DeveloperName = 'Air_Bid'
        AND Status__c = 'Contracted'
      LIMIT 1
    ];
    congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
    for (APXTConga4__Conga_Merge_Query__c congaQuery : [
      SELECT Id, APXTConga4__Name__c
      FROM APXTConga4__Conga_Merge_Query__c
      WHERE
        APXTConga4__Name__c IN (
          'Air - BidsWithOptionsByAirTrip',
          'Air - ContactById',
          'Air - ProductionAssociationsByOppId'
        )
    ])
      congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
    sendOptions_congaQueriesJson = JSON.serialize(congaQueriesMap);
    List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [
      SELECT Id, APXTConga4__Subject__c
      FROM APXTConga4__Conga_Email_Template__c
      WHERE APXTConga4__Name__c = 'Air - Options'
    ];
    sendOptions_congaEmailTemplateId = !congaEmailTemplates.isEmpty()
      ? congaEmailTemplates[0].id
      : null;
    if (
      !congaEmailTemplates.isEmpty() &&
      String.isNotBlank(congaEmailTemplates[0].APXTConga4__Subject__c)
    )
      sendOptions_congaEmailSubject = congaEmailTemplates[0]
        .APXTConga4__Subject__c.replace(
          '{ProductionName}',
          opportunity != null ? opportunity.Name : ''
        )
        .replace(
          '{TravelDates}',
          (tripView.Departure_Date__c != null
            ? Datetime.newInstance(
                  tripView.Departure_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('dd MMMMM yyyy')
            : '') +
          (tripView.Return_Date__c != null
            ? ' - ' +
              Datetime.newInstance(
                  tripView.Return_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('dd MMMMM yyyy')
            : '')
        )
        .replace(
          '{TripCities}',
          String.isNotBlank(airSegmentCities) ? airSegmentCities : ''
        )
        .replace(
          '{TripGroupType}',
          String.isNotEmpty(tripView.Group_Type__c)
            ? tripView.Group_Type__c
            : ''
        )
        .replace(
          '{ClientDueDate}',
          !contractedBids.isEmpty() &&
            contractedBids[0].Client_Deposit_Due_Date__c != null
            ? 'Deposit Due ' +
              Datetime.newInstance(
                  contractedBids[0].Client_Deposit_Due_Date__c,
                  Time.newInstance(0, 0, 0, 0)
                )
                .format('dd MMMMM yyyy')
            : ''
        );
    else
      sendOptions_congaEmailSubject =
        'Air Travel Options ' +
        (opportunity != null ? opportunity.Name : '') +
        (tripView.Departure_Date__c != null
          ? ', ' +
            Datetime.newInstance(
                tripView.Departure_Date__c,
                Time.newInstance(0, 0, 0, 0)
              )
              .format('dd MMMMM yyyy')
          : '') +
        (tripView.Return_Date__c != null
          ? ' - ' +
            Datetime.newInstance(
                tripView.Return_Date__c,
                Time.newInstance(0, 0, 0, 0)
              )
              .format('dd MMMMM yyyy')
          : '') +
        (String.isNotBlank(airSegmentCities) ? ', ' + airSegmentCities : '') +
        (String.isNotEmpty(tripView.Group_Type__c)
          ? ', ' + tripView.Group_Type__c
          : '') +
        (!contractedBids.isEmpty() &&
          contractedBids[0].Client_Deposit_Due_Date__c != null
          ? ', Deposit Due ' +
            Datetime.newInstance(
                contractedBids[0].Client_Deposit_Due_Date__c,
                Time.newInstance(0, 0, 0, 0)
              )
              .format('dd MMMMM yyyy')
          : '');
    List<APXTConga4__Conga_Template__c> congaTemplates = [
      SELECT Id
      FROM APXTConga4__Conga_Template__c
      WHERE APXTConga4__Name__c = 'Air - Options'
    ];
    sendOptions_congaTemplateId = !congaTemplates.isEmpty()
      ? congaTemplates[0].id
      : null;
  }
  //End Air Trip PreviewOptions Methods
  //Air Trip SendOptions Methods.
  public void openSendOptions() {
    openPreviewOptions();
    contactsByProduction = new List<SelectOption>();
    contactsByProduction.add(new SelectOption('', '-- Select --'));
    contactWrapperByProduction = new List<ContactWrapper>();
    Map<Id, Contact> contactsMap = new Map<Id, Contact>();
    for (Production_Associations__c productionAssoc : [
      SELECT
        Id,
        Contact__c,
        Contact__r.Order__c,
        Contact__r.Name,
        Contact__r.FirstName,
        Contact__r.LastName,
        Designation_title__c,
        Contact__r.Account.Name,
        Contact__r.Email,
        Contact__r.Phone
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :opportunityid
        AND Role__c INCLUDES ('Primary Air', 'CC: Air', 'Options')
        AND Contact__c != NULL
        AND Contact__r.Email != NULL
      ORDER BY Contact__r.Order__c ASC NULLS LAST
    ])
      contactsMap.put(
        productionAssoc.Contact__c,
        new Contact(
          id = productionAssoc.Contact__c,
          Order__c = productionAssoc.Contact__r.Order__c,
          FirstName = productionAssoc.Contact__r.FirstName,
          LastName = productionAssoc.Contact__r.LastName,
          Name__c = productionAssoc.Contact__r.Name,
          Designation_title__c = productionAssoc.Designation_title__c,
          Email = productionAssoc.Contact__r.Email,
          Account_Name__c = productionAssoc.Contact__r.Account.Name
        )
      );
    for (Contact contact : contactsMap.values()) {
      contactsByProduction.add(new SelectOption(contact.id, contact.Name__c));
      contactWrapperByProduction.add(
        new ContactWrapper(
          contact,
          contact.Order__c == 1,
          contact.Order__c == 1
        )
      );
      if (contact.Order__c == 1)
        sendOptions_primaryContactId = contact.id;
    }
  }
  public void changeContactProduction() {
    for (ContactWrapper contactWrapperItem : contactWrapperByProduction) {
      if (sendOptions_primaryContactId == contactWrapperItem.c.Id) {
        contactWrapperItem.selected = true;
        contactWrapperItem.disabled = true;
      } else {
        if (contactWrapperItem.selected && contactWrapperItem.disabled) {
          contactWrapperItem.selected = false;
          contactWrapperItem.disabled = false;
        }
      }
    }
  }
  public void reRenderTripFields() {
    List<Air__c> airTrips = [
      SELECT Id, Status__c
      FROM Air__c
      WHERE Id = :tripViewId
    ];
    if (!airTrips.isEmpty()) {
      tripView.Status__c = airTrips[0].Status__c;
    }
    Map<Id, BidWrapper> airBidsMap = new Map<Id, BidWrapper>();
    for (BidWrapper airBid : bidsByTripShowList)
      airBidsMap.put(airBid.b.id, airBid);
    for (Bid__c airBid : [
      SELECT id, Status__c
      FROM Bid__c
      WHERE id IN :airBidsMap.keySet()
    ]) {
      if (airBid.Status__c != 'Unsent')
        bidReleaseActive = true;
      airBidsMap.get(airBid.id).status = airBid.Status__c;
    }
  }
  //End Air SendOptions Methods
  //Air Trip sendLink Methods. (Victor)
  public void sendLink() {
    //system.debug('##sendLink - tripView.id = ' + tripView.id);
    //system.debug('##sendLink - tripViewId = ' + tripViewId);
    system.debug('#sendLink()');
    Set<String> toAddresses = new Set<String>();
    Set<String> ccAddresses = new Set<String>();
    Contact primaryContact = new Contact();
    String primary_contact_name = '';
    String primary_contact_email = '';
    String primary_contact_designationtitle = '';
    String cc_contact_emails = '';
    for (ContactWrapper cw : contactWrapperByProduction) {
      if (cw.selected && cw.disabled) {
        primary_contact_name = cw.c.Name;
        primary_contact_email = cw.c.Email;
        primary_contact_designationtitle = cw.c.Designation_title__c;
        primaryContact = cw.c;
        toAddresses.add(cw.c.Email);
      }
      if (!cw.disabled && cw.selected) {
        ccAddresses.add(cw.c.Email);
        cc_contact_emails = cc_contact_emails + cw.c.Email + ', ';
      }
    }
    system.debug('# toAddresses = ' + toAddresses);
    system.debug('# ccAddresses = ' + toAddresses);
    system.debug('# primaryContact = ' + primaryContact);

    ///List<Housing__c> serviceMap = [SELECT Id, Name, City__c, City__r.Name, Date_In__c, Date_Out__c, RecordType.DeveloperName FROM Housing__c WHERE Id =: housingStayViewId];
    List<Air__c> serviceMap = [
      SELECT
        Id,
        Name,
        /*City__c, City__r.Name,*/ Departure_Date__c,
        Arrival_Date__c,
        Return_Date__c,
        RecordType.DeveloperName
      FROM Air__c
      WHERE Id = :tripViewId
    ];

    String dateStart = (serviceMap[0].Departure_Date__c != null
      ? Datetime.newInstance(
            serviceMap[0].Departure_Date__c.year(),
            serviceMap[0].Departure_Date__c.month(),
            serviceMap[0].Departure_Date__c.day()
          )
          .format('dd MMMMM yyyy')
      : '');
    String dateEnd = (serviceMap[0].Return_Date__c != null
      ? Datetime.newInstance(
            serviceMap[0].Return_Date__c.year(),
            serviceMap[0].Return_Date__c.month(),
            serviceMap[0].Return_Date__c.day()
          )
          .format('dd MMMMM yyyy')
      : '');
    //Arrival_Date__c
    String subject;

    //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Housing Coordinator')];
    List<Production_Associations__c> prodAssocAux = [
      SELECT Id, User__r.Name, User__r.Email
      FROM Production_Associations__c
      WHERE
        Production_Opp__c = :opportunityid
        AND User__c != NULL
        AND Team_Roles__c INCLUDES ('Primary Air Coordinator')
    ];

    List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
    Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
    if (prodAssocAux.size() > 0)
      mail.setOrgWideEmailAddressId(
        verifyWideAddress(prodAssocAux[0].User__r.Email)
      );
    mail.setToAddresses(new List<String>(toAddresses));
    if (ccAddresses.size() > 0)
      mail.setCcAddresses(new List<String>(ccAddresses));

    String body;
    subject =
      'Community Link - Air Options - ' +
      /*(serviceMap[0].City__c != null ? serviceMap[0].City__r.Name : '') + ' - ' +*/ dateStart +
      '-' +
      dateEnd +
      ' (' +
      serviceMap[0].Name +
      ')';
    body =
      'Hi ' +
      (String.isNotEmpty(primaryContact.FirstName)
        ? primaryContact.FirstName
        : '') +
      '<br /><br />You have Air Options available for your review.' +
      '<br /><br />Please log on to view:' +
      //'<br /><br /><a href="https://ccdev-roadrebel.cs42.force.com/" target="_blank">Link to Community Portal</a>' +
      '<br /><br /><a href="' +
      (communityURLvalue != null ? communityURLvalue : '') +
      '/s/?service=air&record=' +
      tripViewId +
      '" target="_blank">Link to Community Portal</a>' +
      '<br /><br />Thank you,' +
      //'<br /><br />' + (String.isNotEmpty(primaryContact.FirstName) ? primaryContact.FirstName : '') + ' ' + (String.isNotEmpty(primaryContact.LastName) ? primaryContact.LastName : '') +
      '<br /><br />' +
      (prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '') +
      //'<br /><br />' + (String.isNotEmpty(primary_contact_designationtitle) ? primary_contact_designationtitle : '');
      '<br />Primary Air Coordinator';

    mail.setSubject(subject);
    mail.setHtmlBody(body);
    myEmails.add(mail);

    insert new Journal__c(
      RecordTypeId = journal_tripJournalRT,
      Air__c = tripViewId,
      Journal_Entry__c = 'GT options has been sent to: ' +
        primary_contact_name +
        ' at ' +
        primary_contact_email +
        (cc_contact_emails != ''
          ? ', cc: ' +
            cc_contact_emails.substring(0, cc_contact_emails.length() - 2)
          : '')
    );

    if (
      tripView != null &&
      (tripView.Status__c != 'Contracted' ||
      tripView.Status__c != 'In Contracting')
    ) {
      tripView.Status__c = 'Pending Client Choice';
      update new Air__c(
        id = tripView.id,
        Status__c = 'Pending Client Choice',
        Options_Sent_to_Client__c = Datetime.now(),
        Community_Notes__c = communityNoteCoordinator,
        Community_Note_Available__c = communityNoteCoordinator == null || communityNoteCoordinator == '' ? false : true

      );
      List<Itinerary__c> itineraries = [
        SELECT Id
        FROM Itinerary__c
        WHERE
          Air__c = :tripViewId
          AND RecordType.DeveloperName = 'Air_Itinerary'
      ];
      if (!itineraries.isEmpty())
        update new Itinerary__c(
          Id = itineraries[0].Id,
          Status__c = 'Pending Client Choice'
        );
      searchTrip();
    }

    if (myEmails.size() > 0)
      Messaging.sendEmail(myEmails);
    //contactWrapperByProduction = new List<ContactWrapper>();
  }
  //End Air SendOptions Methods
  /**
   *  @Conga: Conga Methods.
   */
  public void congaSendOptions() {
    openPreviewOptions();
    List<String> congaParameters = new List<String>();
    String ccEmails = '';
    for (ContactWrapper contactWrapperItem : contactWrapperByProduction)
      if (!contactWrapperItem.disabled && contactWrapperItem.selected)
        ccEmails = String.isNotBlank(ccEmails)
          ? ccEmails + ', ' + contactWrapperItem.c.Email
          : contactWrapperItem.c.Email;
    congaParameters.add(
      '&id=' +
      tripView.id +
      '&QueryId=' +
      (congaQueriesMap.get('Air - BidsWithOptionsByAirTrip') != null
        ? '[Bids]' +
          congaQueriesMap.get('Air - BidsWithOptionsByAirTrip').id +
          '?pv0=' +
          tripView.id
        : '') +
      (congaQueriesMap.get('Air - ContactById') != null
        ? ',[Contact]' +
          congaQueriesMap.get('Air - ContactById').id +
          '?pv0=' +
          sendOptions_primaryContactId
        : '') +
      (congaQueriesMap.get('Air - ProductionAssociationsByOppId') != null
        ? ',[ProductionAssoc]' +
          congaQueriesMap.get('Air - ProductionAssociationsByOppId').id +
          '?pv0=' +
          opportunityid
        : '') +
      (String.isNotBlank(sendOptions_congaEmailTemplateId)
        ? '&CongaEmailTemplateId=' + sendOptions_congaEmailTemplateId
        : '') +
      '&EmailSubject=' +
      sendOptions_congaEmailSubject.replace(' ', '+') +
      '&EmailToId=' +
      sendOptions_primaryContactId +
      '&EmailCC=' +
      ccEmails +
      (String.isNotBlank(sendOptions_congaTemplateId)
        ? '&TemplateId=' + sendOptions_congaTemplateId
        : '') +
      '&OFN=Air+Options&DS7=2&SC0=1&SC1=SalesforceFile'
    );
    try {
      congaSendEmail(congaParameters);
      Air__c airTrip = new Air__c(
        Id = tripView.id,
        Options_sent_to_client__c = Datetime.now()
      );
      if (
        tripView.Status__c != 'Contracted' ||
        tripView.Status__c != 'In Contracting'
      ) {
        airTrip.Status__c = tripView.Status__c = 'Pending Client Choice';
        if (String.isNotBlank(tripItineraryId))
          update new Itinerary__c(
            Id = tripItineraryId,
            Status__c = 'Pending Client Choice'
          );
      }
      update airTrip;
    } catch (Exception e) {
      System.debug(
        '###AirDashboardController.congaSendOptions() - Exception: ' +
        e.getMessage()
      );
    }
  }
  @future(callout=true)
  public static void congaSendEmail(List<String> congaParameters) {
    HttpRequest request = new HttpRequest();
    request.setMethod('GET');
    request.setTimeout(120000);
    Http http = new Http();
    HTTPResponse response;
    for (String parameters : congaParameters) {
      request.setEndpoint(
        'https://composer.congamerge.com/composer8/index.html?sessionId=' +
        UserInfo.getOrganizationId() +
        '' +
        UserInfo.getSessionId().SubString(15) +
        '&serverUrl=' +
        EncodingUtil.urlEncode(
          System.Url.getSalesforceBaseUrl().toExternalForm() +
          '/services/Soap/u/29.0/' +
          UserInfo.getOrganizationId(),
          'UTF-8'
        ) +
        parameters +
        '&DefaultPDF=1&APIMode=12'
      );
      try {
        response = http.send(request);
        System.debug(
          '###AirDashboardController.congaEmail(parameters = ' +
          parameters +
          ') => Response Status Code: ' +
          response.getStatusCode() +
          ', Response Body: ' +
          (String.isNotEmpty(response.getBody())
            ? response.getBody().left(255)
            : '')
        );
      } catch (Exception e) {
        System.debug(
          '###AirDashboardController.congaEmail() - Callout Exception: ' +
          e.getMessage()
        );
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

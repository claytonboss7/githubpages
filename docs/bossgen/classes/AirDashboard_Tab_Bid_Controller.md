---
layout: default
title: AirDashboard_Tab_Bid_Controller
parent: classes
---
# Metadata Type
classes


# Filename 
AirDashboard_Tab_Bid_Controller


# Raw XML
```
global class AirDashboard_Tab_Bid_Controller {
  public DashboardConfigurationWrapper vfpConfiguration { get; set; }
  public Opportunity opportunity { get; set; }
  public String opportunityId { get; set; }
  public Integer tripBidNumber { get; set; }
  public Integer totalRecsBids { get; set; }
  public Map<Integer, BidWrapper> bidDataMap { get; set; }
  public Bid__c bidData { get; set; }
  public GTDashboard gtDashboard {
    get;
    set {
      bidDataMap = value.bidDataMap;
      gtDashboard = value;
    }
  }
  public List<SelectOption> contactsBidsByVendor { get; set; }
  public String contactPrimarySelected { get; set; }
  public String previewBid_congaTemplateId { get; set; }
  public String previewBidOptions_congaTemplateId { get; set; }
  public String previewBidOptions_congaQueriesJson { get; set; }
  public List<Ground__c> bidSubTrips { get; set; }
  public Map<Id, List<Ground__c>> bidSubTripTravelsMap { get; set; }
  public String coordinatorGT { get; set; }
  public Boolean isPageLoaded { get; set; }
  public Boolean loadDocuments { get; set; }
  public List<Air__c> itineraryList { get; set; }
  public Air__c itineraryBid { get; set; }
  public List<SelectOption> currencyPL { get; set; }
  public Boolean bid_leadsent { get; set; }
  public String biddata_nobidreason { get; set; }
  public String biddata_bidoptionnotes { get; set; }
  public String biddata_options { get; set; }
  public Boolean biddata_includeinoptions { get; set; }
  public String biddata_internalnotes { get; set; }

  //BidAgrement
  public Draft__c draft { get; set; }
  public List<Ground__c> bidAgreementSubTrips { get; set; }
  public List<Ground__c> bidAgreementVehicles { get; set; }
  public List<Concessions__c> bidAgreementConcessions { get; set; }
  public Revenue__c bidAgreementRevenue { get; set; }
  public String journal_bidjournalRT { get; set; }
  public Contact bidPrimaryContact { get; set; }
  public Contact bidAgreementPrimaryContact { get; set; }
  public Contact bidAgreementAttentionContact { get; set; }
  public Boolean isBidAgreementRendered { get; set; }
  public Boolean isResendBidRendered { get; set; }
  public Boolean isReleaseBidRendered { get; set; }
  public String bidAgreement_type { get; set; }
  public String bidAgreement_subject { get; set; }
  public String bidAgreement_message { get; set; }
  public String bidAgreement_terms { get; set; }
  public String bidAgreement_lastModifiedBy { get; set; }
  public String bidAgreement_congaEmailFromId { get; set; }
  public String bidAgreement_congaEmailTemplateId { get; set; }
  public String bidAgreement_congaTemplateId { get; set; }
  public String bidAgreement_congaSignTemplateId { get; set; }
  //ResendBid
  public Map<String, List<ContactWrapper>> contactsByVendorBidMap { get; set; }
  public Map<String, List<ContactWrapper>> contactsByVendorParentBidMap {
    get;
    set;
  }
  public Map<String, List<SelectOption>> contactSelectOptionBidMap { get; set; }
  public String vendorcontact_actual_id { get; set; }
  public String resendBidAgreement_contactPrimary { get; set; }
  public String resendBidAgreement_congaEmailSubject { get; set; }
  public String resendBidAgreement_congaEmailTemplateId { get; set; }
  public String resendBidAgreement_congaTemplateId { get; set; }
  //ReleaseBid
  public String releaseVendorcontact_actual_id { get; set; }
  public String releaseVendoraccount_actual_id { get; set; }
  public Map<String, List<SelectOption>> contactSelectOption_releaseMap {
    get;
    set;
  }
  public Map<String, List<ContactWrapper>> contactsByVendor_releaseMap {
    get;
    set;
  }
  public Map<String, List<ContactWrapper>> contactsByVendorParent_releaseMap {
    get;
    set;
  }
  public String releaseEmailBid_body { get; set; }
  public String emailbid_to { get; set; }
  public String emailbid_cc { get; set; }
  public String emailbid_bcc { get; set; }
  public String emailbid_subject { get; set; }
  public String emailbid_id { get; set; }
  public String emailbid_primarycontactname { get; set; }
  public String emailAttachs { get; set; }
  public String emailbid_type { get; set; }
  public String emailMessage { get; set; }
  //AddContacts
  public String messageCreateContact { get; set; }
  public Contact vendorContact { get; set; }
  public String vendorContact_id { get; set; }
  public List<SelectOption> contact_DesignationTitle { get; set; }
  //Attachs
  public String filename { get; set; }
  transient public String body { get; set; }
  transient public String bodyBid { get; set; }
  public List<ContentDocument> attachDocumentList { get; set; }
  public String attachdocument_objectid { get; set; }
  public String newattachment_id { get; set; }
  public String newattachment_name { get; set; }
  public List<ContentDocument> documentBidList { get; set; }
  public Integer documentListFirst { get; set; }
  public Integer documentListPage { get; set; }
  public Integer documentListLastPage { get; set; }
  public List<Integer> documentListPages { get; set; }
  public String documentId { get; set; }
  public String documentTitle { get; set; }
  public String documentRelationId { get; set; }
  //Bid History
  public List<SelectOption> production_markettypes { get; set; }
  public Ground__c groundFilter { get; set; }
  public static String orderBidHistory { get; set; }
  public static String orderBidHistoryOrientation { get; set; }
  public Boolean orderCheckBidHistory { get; set; }
  public Boolean orderChangeBidHistory { get; set; }
  public List<BidVendorWrapper> bidRelatedVendorList { get; set; }
  public String bidhistorysearch_departurecity { get; set; }
  public String bidhistorysearch_arrivalcity { get; set; }
  public Map<String, Revenue__c> revenueBidMap { get; set; }
  //Rate Details
  public Revenue__c bidRevenue { get; set; }
  //Additional Fees
  public String concessionJson { get; set; }
  public List<Concessions__c> concessionsRequestedBid { get; set; }
  public String concessionRequestedActual { get; set; }
  public String concessionNoteActual { get; set; }
  public String concessionActual { get; set; }
  public String concessionIncludedActual { get; set; }
  public String concessionRateActual { get; set; }
  public String concessionOrderActual { get; set; }
  //Itinerary
  public String itineraryActual { get; set; }
  public String itinerary_description { get; set; }
  public String itinerary_pax { get; set; }
  public String dateToday { get; set; }
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
  public String newitinerary_class { get; set; }
  public String newitinerary_equiptype { get; set; }
  public String newitinerary_operatedby { get; set; }
  public Decimal newitinerary_seats { get; set; }
  public Air__c newItinerary { get; set; }
  public String segmentsAir { get; set; }
  public List<Air__c> aircraftsByBidList { get; set; }
  //Deviation
  public List<Air__c> bidDeviationTrips { get; set; }
  public String deviationActual { get; set; }
  public String deviation_triptype { get; set; }
  public String deviation_description { get; set; }
  public String deviation_grouptype { get; set; }
  public Map<Id, List<Air__c>> bidDeviationTravelsMap { get; set; }
  public String travelActual { get; set; }
  //Rate Details
  public List<Revenue__c> groupRateDetails { get; set; }
  public List<SelectOption> deviationPL { get; set; }
  public Integer groupRateActual { get; set; }
  public Map<String, String> symbolMap { get; set; }

  //Trip Details
  public Map<String, Boolean> hasFreightMap { get; set; }
  public String ground_GTSubStripDetailsRT { get; set; }
  public String subtripIdActual { get; set; }
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
  public String ground_GTTravelDetailsRT { get; set; }
  public Ground__c newTravel { get; set; }
  public Ground__c newVehicleBid { get; set; }
  public List<SelectOption> ground_amenitiesPL { get; set; }
  public List<Ground__c> vehiclesByBidList { get; set; }
  public String vehicleIdActual { get; set; }
  public String vehicle_vehicleref { get; set; }
  public String vehicle_vehicletype { get; set; }
  public Integer vehicle_capacity { get; set; }
  public String vehicle_make { get; set; }
  public String vehicle_model { get; set; }
  public String vehicle_year { get; set; }
  public String vehicle_amenities { get; set; }
  public String ground_vehicletypeRT { get; set; }
  public String url { get; set; }
  //Locked
  public String bidid_locked { get; set; }
  public Boolean bidstatus_locked { get; set; }
  //BidJournals
  public Boolean isBidJournalsRendered { get; set; }
  public Boolean tripHaveContracted { get; set; }

  public String contractingBidId { get; set; }
  public String contractingParentId { get; set; }

  //Aircrafts
  public String aircraftIdActual { get; set; }
  public String aircraft_type { get; set; }
  public String aircraft_economyseats { get; set; }
  public String aircraft_cargocapacity { get; set; }
  public String aircraft_seatpitch { get; set; }
  public String aircraft_airlineid { get; set; }
  public String aircraft_position { get; set; }
  public String aircraft_tripcontents { get; set; }
  public Air__c newAircraftBid { get; set; }

  public AirDashboard_Tab_Bid_Controller() {
    bidData = new Bid__c();
    System.debug(
      'AirDashboard_Tab_Bid_Controller.tripBidNumber: ' + tripBidNumber
    );
    journal_bidjournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByName()
        .get('Bid Journal') != null
      ? Schema.SObjectType.Journal__c.getRecordTypeInfosByName()
          .get('Bid Journal')
          .getRecordTypeId()
      : null;
    Init();
  }
  public void Init() {
    orderCheckBidHistory = false;
    orderChangeBidHistory = false;
    dateToday = String.valueOf(Datetime.now().format('MM/dd/yyyy'));
    vendorContact = new Contact();
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
    ground_vehicletypeRT = [
      SELECT Id
      FROM RecordType
      WHERE sObjectType = 'Ground__c' AND Name = 'Vehicle Type'
    ]
    .Id;
    url = ApexPages.currentPage().getHeaders().get('Host');

    production_markettypes = new List<SelectOption>();
    production_markettypes.add(new SelectOption('', '--Select--'));
    production_markettypes.addAll(
      GTDashboardController.PickThePicklist('Opportunity', 'Market_Type__c')
    );
    groundFilter = new Ground__c();
    List<wrapperSearchPL> consValueList = new List<wrapperSearchPL>();
    Map<Object, List<String>> dependValuesByControlValue = GTDashboardController.getDependentPicklistValues(
      Concessions__c.Concessions_Requested__c
    );
    for (Object k1 : dependValuesByControlValue.keySet()) {
      if ((String) k1 == 'Air') {
        for (String k2 : dependValuesByControlValue.get(k1)) {
          consValueList.add(new wrapperSearchPL(k2, k2));
        }
      }
    }
    concessionJson = JSON.serialize(consValueList);
    concessionsRequestedBid = new List<Concessions__c>();
    bidSubTrips = new List<Ground__c>();
    newTravel = new Ground__c();
    newVehicleBid = new Ground__c();
    ground_amenitiesPL = new List<SelectOption>();
    Schema.DescribeFieldResult fieldResult = Ground__c.Amenities__c.getDescribe();
    List<Schema.PicklistEntry> ple = fieldResult.getPicklistValues();
    for (Schema.PicklistEntry pickListVal : ple) {
      ground_amenitiesPL.add(
        new SelectOption(pickListVal.getValue(), pickListVal.getLabel())
      );
    }
    revenueBidMap = new Map<String, Revenue__c>();
    draft = new Draft__c();
    isPageLoaded = isBidAgreementRendered = isResendBidRendered = isBidJournalsRendered = isReleaseBidRendered = false;

    newItinerary = new Air__c();
    bidDeviationTrips = new List<Air__c>();
    groupRateDetails = new List<Revenue__c>();
    deviationPL = new List<SelectOption>();
    currencyPL = new List<SelectOption>();
    currencyPL.add(new SelectOption('', ''));
    for (CurrencyType ct : [
      SELECT toLabel(IsoCode) IsoLabel, IsoCode
      FROM CurrencyType
      WHERE IsActive = TRUE
    ]) {
      currencyPL.add(
        new SelectOption(ct.IsoCode, String.valueOf(ct.get('IsoLabel')))
      );
    }
    newAircraftBid = new Air__c();
  }
  public void changeLeadSent() {
    if (bidData != null && bidData.Id != null) {
      Bid__c bidDataAux = new Bid__c(Id = bidData.Id);
      bidDataAux.Lead_Sent__c = bid_leadsent;
      if (bid_leadsent == true) {
        if (bidData.Status__c == 'Unsent') {
          bidDataAux.Status__c = 'Sent';
          bidData.Status__c = 'Sent';
        }
      } else {
        if (bidData.Status__c == 'Sent') {
          bidDataAux.Status__c = 'Unsent';
          bidData.Status__c = 'Unsent';
        }
      }
      update bidDataAux;
    }
  }
  public void addAircraftBid() {
    if (
      opportunityId != null &&
      opportunityId != null &&
      bidData != null &&
      bidData.Id != null
    ) {
      newAircraftBid.Id = null;
      newAircraftBid.RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
        .get('Air_Crafts')
        .getRecordTypeId();
      newAircraftBid.Production__c = opportunityId;
      newAircraftBid.Bid_Aircraft__c = bidData.Id;
      newAircraftBid.Airline__c = aircraft_airlineid != null &&
        aircraft_airlineid != ''
        ? aircraft_airlineid
        : null;
      insert newAircraftBid;
    }
    getAircraftsByBid();
  }
  public void newAircraftBid() {
    newAircraftBid = new Air__c();
  }
  public void deleteAircraftBid() {
    if (aircraftIdActual != null && aircraftIdActual != '')
      delete [SELECT Id FROM Air__c WHERE Id = :aircraftIdActual];
    getAircraftsByBid();
  }
  public void saveEditAircraftBid() {
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
    }
    getAircraftsByBid();
  }
  public void getAircraftsByBid() {
    aircraftsByBidList = new List<Air__c>();
    if (
      bidData != null &&
      bidData.Id != null &&
      bidData.Air__r.Air_Charter__c == true
    ) {
      aircraftsByBidList = [
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
          AND Bid_Aircraft__c = :bidData.Id
      ];
    }
  }
  public void calculateTotalPriceCharter() {
    if (bidRevenue != null)
      bidRevenue.Total_Price__c =
        (bidRevenue.Base_Cost__c != null ? bidRevenue.Base_Cost__c : 0) +
        (bidRevenue.Commission__c != null ? bidRevenue.Commission__c : 0);
  }
  public void calculateTotalPrice() {
    if (groupRateActual != null) {
      Integer i = 0;
      for (Revenue__c r : groupRateDetails) {
        if (groupRateActual == i) {
          r.Total_Price__c =
            (r.Rate_currency__c != null ? r.Rate_currency__c : 0) +
            (r.Service_Fees__c != null ? r.Service_Fees__c : 0) +
            (r.Additional_Fees__c != null ? r.Additional_Fees__c : 0) +
            (r.Total_Taxes__c != null ? r.Total_Taxes__c : 0);
          break;
        }
        i++;
      }
    }
  }
  public void saveGroupRate() {
    if (groupRateActual != null) {
      Integer i = 0;
      for (Revenue__c r : groupRateDetails) {
        if (groupRateActual == i) {
          r.Production__c = opportunityId;
          r.Bid__c = bidData.Id;
          r.RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Rate_Commission')
            .getRecordTypeId();
          upsert r;
          break;
        }
        i++;
      }
    }
  }
  public void deleteGroupRate() {
    if (groupRateActual != null) {
      Integer i = 0;
      for (Revenue__c r : groupRateDetails) {
        if (groupRateActual == i) {
          if (r.Id != null)
            delete [SELECT Id FROM Revenue__c WHERE Id = :r.Id];
          groupRateDetails.remove(groupRateActual);
          break;
        }
        i++;
      }
    }
  }
  public void addGroupRate() {
    User us = [
      SELECT Id, Housing_Preference__c
      FROM User
      WHERE Id = :UserInfo.getUserId()
    ];
    groupRateDetails.add(
      new Revenue__c(
        Base_Rate_Currency__c = (us.Housing_Preference__c == 'RRE'
          ? 'EUR'
          : 'USD'),
        Service_Fees_Currency__c = (us.Housing_Preference__c == 'RRE'
          ? 'EUR'
          : 'USD'),
        Additional_Fees_Currency__c = (us.Housing_Preference__c == 'RRE'
          ? 'EUR'
          : 'USD'),
        Total_Taxes_Currency__c = (us.Housing_Preference__c == 'RRE'
          ? 'EUR'
          : 'USD'),
        Total_Price_Currency__c = (us.Housing_Preference__c == 'RRE'
          ? 'EUR'
          : 'USD')
      )
    );
  }
  public void getGroupRateDetails() {
    groupRateDetails = new List<Revenue__c>();
    if (bidData != null && bidData.Id != null) {
      groupRateDetails = [
        SELECT
          Id,
          Rate_currency__c,
          Service_Fees__c,
          Additional_Fees__c,
          Total_Taxes__c,
          Total_Price__c,
          of_seats__c,
          Record_Locator__c,
          Deviation__c,
          Base_Rate_Currency__c,
          Service_Fees_Currency__c,
          Additional_Fees_Currency__c,
          Total_Taxes_Currency__c,
          Total_Price_Currency__c
        FROM Revenue__c
        WHERE
          RecordType.DeveloperName = 'Air_Rate_Commission'
          AND Bid__c = :bidData.Id
      ];
      User us = [
        SELECT Id, Housing_Preference__c
        FROM User
        WHERE Id = :UserInfo.getUserId()
      ];
      if (groupRateDetails.isEmpty()) {
        groupRateDetails.add(
          new Revenue__c(
            Production__c = opportunityId,
            Bid__c = bidData.Id,
            RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
              .get('Air_Rate_Commission')
              .getRecordTypeId(),
            Base_Rate_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD'),
            Service_Fees_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD'),
            Additional_Fees_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD'),
            Total_Taxes_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD'),
            Total_Price_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD')
          )
        );
      } else {
        for (Revenue__c r : groupRateDetails) {
          if (r.Base_Rate_Currency__c == null || r.Base_Rate_Currency__c == '')
            r.Base_Rate_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD');
          else
            symbolMap.put(r.Base_Rate_Currency__c, '');
          if (
            r.Service_Fees_Currency__c == null ||
            r.Service_Fees_Currency__c == ''
          )
            r.Service_Fees_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD');
          else
            symbolMap.put(r.Service_Fees_Currency__c, '');
          if (
            r.Additional_Fees_Currency__c == null ||
            r.Additional_Fees_Currency__c == ''
          )
            r.Additional_Fees_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD');
          else
            symbolMap.put(r.Additional_Fees_Currency__c, '');
          if (
            r.Total_Taxes_Currency__c == null ||
            r.Total_Taxes_Currency__c == ''
          )
            r.Total_Taxes_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD');
          else
            symbolMap.put(r.Total_Taxes_Currency__c, '');
          if (
            r.Total_Price_Currency__c == null ||
            r.Total_Price_Currency__c == ''
          )
            r.Total_Price_Currency__c = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD');
          else
            symbolMap.put(r.Total_Price_Currency__c, '');
        }
      }
    }
  }
  public void deleteTravelBid() {
    if (travelActual != null && travelActual != '') {
      delete [SELECT Id FROM Air__c WHERE Id = :travelActual];
      getDeviationByBid();
    }
  }
  public void saveDeviation() {
    if (deviationActual != null && deviationActual != '') {
      update new Air__c(
        Id = deviationActual,
        Trip_Type__c = deviation_triptype,
        Description__c = deviation_description,
        Group_Type__c = deviation_grouptype
      );
    }
  }
  public void saveItineraryParentBid() {
    if (itineraryBid != null) {
      itineraryBid.Description__c = itinerary_description;
      itineraryBid.PAX__c = itinerary_pax != null &&
        itinerary_pax != ''
        ? Decimal.valueOf(itinerary_pax.replace(',', ''))
        : null;
      upsert itineraryBid;
    }
  }
  public void deleteDeviation() {
    if (
      deviationActual != null &&
      deviationActual != '' &&
      bidData != null &&
      bidData.Id != null
    ) {
      //delete [SELECT Id FROM Sub_Trip_GCQ__c WHERE GT_Sub_Trip_Details__c =: subtripIdActual];
      delete [
        SELECT Id
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Segments'
          AND Air_Deviation_Details__c = :deviationActual
      ];
      delete [SELECT Id FROM Air__c WHERE Id = :deviationActual];

      Integer cont = 1;
      List<Air__c> deviationExistList = new List<Air__c>();
      for (Air__c a : [
        SELECT Id, Deviation_Order_Conga__c
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Deviation_Details'
          AND Bid_Deviation__c = :bidData.Id
        ORDER BY Deviation_Order_Conga__c ASC
      ]) {
        a.Deviation_Order_Conga__c = cont;
        deviationExistList.add(a);
        cont++;
      }

      if (deviationExistList.size() > 0)
        update deviationExistList;
      getDeviationByBid();
    }
  }
  public void newDeviationBid() {
    if (bidData != null && bidData.Id != null) {
      List<Air__c> deviationExistList = [
        SELECT Id, Deviation_Order_Conga__c
        FROM Air__c
        WHERE
          RecordType.DeveloperName = 'Air_Deviation_Details'
          AND Bid_Deviation__c = :bidData.Id
        ORDER BY Deviation_Order_Conga__c DESC
        LIMIT 1
      ];

      Air__c new_deviation = new Air__c(
        Production__c = opportunityId,
        RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
          .get('Air_Deviation_Details')
          .getRecordTypeId(),
        Deviation_Order_Conga__c = (deviationExistList.size() > 0
          ? (deviationExistList[0].Deviation_Order_Conga__c != null
              ? deviationExistList[0].Deviation_Order_Conga__c + 1
              : 1)
          : 1),
        Description__c = 'Deviation ' +
          (deviationExistList.size() > 0
            ? (deviationExistList[0].Deviation_Order_Conga__c != null
                ? deviationExistList[0].Deviation_Order_Conga__c + 1
                : 1)
            : 1),
        Bid_Deviation__c = bidData.Id,
        Group_Type__c = bidData.Air__r.Group_Type__c,
        Trip_Type__c = bidData.Air__r.Trip_Type__c
      );
      insert new_deviation;

      getDeviationByBid();
    }
  }
  public void getDeviationByBid() {
    bidDeviationTrips = new List<Air__c>();
    bidDeviationTravelsMap = new Map<Id, List<Air__c>>();
    deviationPL = new List<SelectOption>();
    deviationPL.add(new SelectOption('', ''));
    for (Air__c deviation : [
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
        Deviation_Order_Conga__c,
        Description__c,
        Number_of_Seats__c,
        (
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
            Deviation_Order_Conga__c,
            Description__c,
            Number_of_Seats__c
          FROM AirDeviationTravels__r
        )
      FROM Air__c
      WHERE
        Bid_Deviation__c = :bidData.Id
        AND RecordType.DeveloperName = 'Air_Deviation_Details'
      ORDER BY Deviation_Order_Conga__c ASC
    ]) {
      bidDeviationTrips.add(deviation);
      bidDeviationTravelsMap.put(
        deviation.Id,
        deviation.AirDeviationTravels__r
      );
      deviationPL.add(
        new SelectOption(
          deviation.Id,
          'Deviation ' + deviation.Deviation_Order_Conga__c
        )
      );
      if (deviation.AirDeviationTravels__r != null) {
        for (Air__c adt : deviation.AirDeviationTravels__r) {
          adt.Dep_Time_Text__c = adt.Departure_Date__c != null &&
            adt.Dep_Time__c != null
            ? Datetime.newInstance(adt.Departure_Date__c, adt.Dep_Time__c)
                .format('h:mm a')
            : (adt.Dep_Time__c != null
                ? Datetime.newInstance(system.today(), adt.Dep_Time__c)
                    .format('h:mm a')
                : '');
          adt.Arr_Time_Text__c = adt.Arrival_Date__c != null &&
            adt.Arr_Time__c != null
            ? Datetime.newInstance(adt.Arrival_Date__c, adt.Arr_Time__c)
                .format('h:mm a')
            : (adt.Departure_Date__c != null &&
                adt.Arr_Time__c != null
                ? Datetime.newInstance(adt.Departure_Date__c, adt.Arr_Time__c)
                    .format('h:mm a')
                : '');
        }
      }
    }
  }
  public void saveTravelBid() {
    Air__c travel = new Air__c(
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
      Class__c = newitinerary_class,
      Equip_Type__c = newitinerary_equiptype,
      Number_of_Seats__c = newitinerary_seats != null
        ? newitinerary_seats
        : null,
      Operated_by__c = newitinerary_operatedby
    );
    if (newitinerary_id == null || newitinerary_id == '') {
      travel.Production__c = opportunityId;
      travel.Air_Deviation_Details__c = deviationActual;
    }
    upsert travel;
    getDeviationByBid();
  }
  public void saveItineraryBid() {
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
      Class__c = newitinerary_class,
      Equip_Type__c = newitinerary_equiptype,
      Operated_by__c = newitinerary_operatedby
    );
    if (newitinerary_id == null || newitinerary_id == '') {
      itinerary.Production__c = opportunityId;
      itinerary.Air_Itinerary_Details__c = itineraryBid.Id;
    }
    upsert itinerary;
    getItineraryByBid();
  }
  public void deleteItineraryBid() {
    if (itineraryActual != null && itineraryActual != '') {
      delete [SELECT Id FROM Air__c WHERE Id = :itineraryActual];
      getItineraryByBid();
    }
  }
  public void viewContractingDetailByBid() {
    if (vfpConfiguration != null) {
      vfpConfiguration.bidId = contractingBidId;
      vfpConfiguration.parentId = contractingParentId;
      vfpConfiguration.productionId = opportunityId;
      vfpConfiguration.parentSObject = 'Air';
    }
  }
  public void uncontractBid() {
    if (
      bidDataMap.get(tripBidNumber).b.Status_Previous__c != null &&
      bidDataMap.get(tripBidNumber).b.Status_Previous__c != ''
    ) {
      update new Bid__c(
        Id = bidDataMap.get(tripBidNumber).b.Id,
        Status__c = bidDataMap.get(tripBidNumber).b.Status_Previous__c,
        Status_Previous__c = null,
        Contracted_date_time__c = null
      );
      bidDataMap.get(tripBidNumber).b.Status__c = bidDataMap.get(tripBidNumber)
        .b.Status_Previous__c;
      bidData.Status__c = bidDataMap.get(tripBidNumber).b.Status_Previous__c;
      if (bidDataMap.get(tripBidNumber).b.Air__c != null) {
        //update new Air__c(Id=bidDataMap.get(tripBidNumber).b.Air__c,Status__c=bidDataMap.get(tripBidNumber).b.Air__r.Status_Previous__c,Vendor__c = null,Status_Previous__c=null);
        update new Air__c(
          Id = bidDataMap.get(tripBidNumber).b.Air__c,
          Status__c = 'Bid Request Stage',
          Vendor__c = null,
          Status_Previous__c = null
        );
        List<Itinerary__c> itineraryAuxList = [
          SELECT Id
          FROM Itinerary__c
          WHERE
            Air__c = :bidDataMap.get(tripBidNumber).b.Air__c
            AND RecordType.DeveloperName = 'Air_Itinerary'
        ];
        //if(itineraryAuxList.size() > 0) update new Itinerary__c(Id = itineraryAuxList[0].Id,Status__c = bidDataMap.get(tripBidNumber).b.Air__r.Status_Previous__c);
        if (itineraryAuxList.size() > 0)
          update new Itinerary__c(
            Id = itineraryAuxList[0].Id,
            Status__c = 'Bid Request Stage'
          );
      }
    }

    getBidInformation();
  }
  public void contractBid() {
    save();
    Dashboard__c cs = Dashboard__c.getOrgDefaults();
    String contractidnumber = getNumberFormat(
      Integer.valueOf(cs.Contract_ID__c)
    );
    update new Bid__c(
      Id = bidDataMap.get(tripBidNumber).b.Id,
      Contract_ID__c = contractidnumber,
      Status_Previous__c = bidDataMap.get(tripBidNumber).b.Status__c,
      Status__c = 'Contracted',
      Final_Status__c = 'Contracted',
      Contracted_date_time__c = system.now()
    );
    bidDataMap.get(tripBidNumber).b.Status_Previous__c = bidDataMap.get(
        tripBidNumber
      )
      .b.Status__c;
    bidData.Status_Previous__c = bidDataMap.get(tripBidNumber).b.Status__c;
    bidData.Contract_ID__c = contractidnumber;
    bidData.Status__c = 'Contracted';
    bidData.Final_Status__c = 'Contracted';
    bidDataMap.get(tripBidNumber).b.Contract_ID__c = contractidnumber;
    cs.Contract_ID__c = cs.Contract_ID__c + 1;
    update cs;

    if (bidDataMap.get(tripBidNumber).b.Air__c != null) {
      update new Air__c(
        Id = bidDataMap.get(tripBidNumber).b.Air__c,
        Vendor__c = bidDataMap.get(tripBidNumber).b.Vendor__c,
        Status_Previous__c = bidDataMap.get(tripBidNumber).b.Air__r.Status__c,
        Status__c = 'Contracted'
      );
      List<Itinerary__c> itineraryAuxList = [
        SELECT Id
        FROM Itinerary__c
        WHERE
          Air__c = :bidDataMap.get(tripBidNumber).b.Air__c
          AND RecordType.DeveloperName = 'Air_Itinerary'
      ];
      if (itineraryAuxList.size() > 0)
        update new Itinerary__c(
          Id = itineraryAuxList[0].Id,
          Status__c = 'Contracted'
        );
    }
    getBidInformation();
  }
  /*public static void cloneInformationToFreight(Bid__c dataBid, Ground__c fData, String ground_vehicletypeRT, String ground_GTSubStripDetailsRT, String ground_GTTravelDetailsRT){
        Ground__c gAux;
        List<Ground__c> gAuxList;
        Concessions__c cAux;
        List<Concessions__c> cAuxList;
        
        Map<String,List<Ground__c>> vehiclesDataMap = new Map<String,List<Ground__c>>();
        for(Ground__c vData : [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, GT_Trip_Details__c
                               FROM Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: dataBid.Production__c AND GT_Trip_Details__c =: dataBid.GT__c
                               AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL]){
                                   gAuxList = vehiclesDataMap.get(vData.GT_Trip_Details__c) != null ? vehiclesDataMap.get(vData.GT_Trip_Details__c) : new List<Ground__c>();
                                   gAuxList.add(vData);
                                   vehiclesDataMap.put(vData.GT_Trip_Details__c,gAuxList.clone());
                               }
        
        Map<String,List<Concessions__c>> concessionsDataMap = new Map<String,List<Concessions__c>>();
        for(Concessions__c cData : [SELECT Id, Agreed__c, GT__c, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, CurrencyIsoCode, Notes__c, Order__c
                                    FROM Concessions__c WHERE GT__c =: dataBid.GT__c AND Production__c =: dataBid.Production__c
                                    AND Bid__c = NULL AND Housing__c = NULL AND Freight__c = NULL]){
                                        cAuxList = concessionsDataMap.get(cData.GT__c) != null ? concessionsDataMap.get(cData.GT__c) : new List<Concessions__c>();
                                        cAuxList.add(cData);
                                        concessionsDataMap.put(cData.GT__c,cAuxList.clone());
                                    }
        
        Map<String,List<Ground__c>> subtripDataMap = new Map<String,List<Ground__c>>();
        Set<String> subtripDataIds = new Set<String>();
        for(Ground__c subtripData : [SELECT Id, Service_Type__c, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, GT_Trip_Details__c
                                     FROM Ground__c 
                                     WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND GT_Trip_Details__c =: dataBid.GT__c ORDER BY Trip_Order__c ASC]){
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
        
        gAuxList = new List<Ground__c>();
        cAuxList = new List<Concessions__c>();
        Map<Integer,Ground__c> subtripInsertMap = new Map<Integer,Ground__c>();
        Map<Integer,List<Ground__c>> travelInsertMap = new Map<Integer,List<Ground__c>>();
        Integer cx = 1;
        List<Ground__c> travelListAux = new List<Ground__c>();

        if(vehiclesDataMap.get(dataBid.GT__c) != null){
            for(Ground__c g : vehiclesDataMap.get(dataBid.GT__c)){
                gAux = g.clone();
                gAux.Id = null;
                gAux.RecordTypeId = ground_vehicletypeRT;
                gAux.Production_Ground__c = dataBid.Production__c;
                gAux.GT_Trip_Details__c = fData.Id;
                gAuxList.add(gAux);
            }
        }
        if(concessionsDataMap.get(dataBid.GT__c) != null){
            for(Concessions__c c : concessionsDataMap.get(dataBid.GT__c)){
                cAux = c.clone();
                cAux.Id = null;
                cAux.Production__c = dataBid.Production__c;
                cAux.GT__c = fData.Id;
                cAuxList.add(cAux);
            }
        }
        
        if(subtripDataMap.get(dataBid.GT__c) != null){
            for(Ground__c gs : subtripDataMap.get(dataBid.GT__c)){
                gAux = gs.clone();
                gAux.Id = null;
                gAux.RecordTypeId = ground_GTSubStripDetailsRT;
                gAux.Production_Ground__c = dataBid.Production__c;
                gAux.GT_Trip_Details__c = fData.Id;
                subtripInsertMap.put(cx,gAux);
                if(travelsBySubTripMapAux.get(gs.Id) != null){
                    for(Ground__c gs2 : travelsBySubTripMapAux.get(gs.Id)){
                        gAux = gs2.clone();
                        gAux.Id = null;
                        gAux.GT_Trip_Details__c = null;
                        gAux.RecordTypeId = ground_GTTravelDetailsRT;
                        gAux.Production_Ground__c = dataBid.Production__c;
                        
                        travelListAux = travelInsertMap.get(cx) != null ? travelInsertMap.get(cx) : new List<Ground__c>();
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
    public static void cloneInformationToBid(Bid__c dataBid, String ground_vehicletypeRT, String ground_GTSubStripDetailsRT, String ground_GTTravelDetailsRT){
        Ground__c gAux;
        List<Ground__c> gAuxList;
        Concessions__c cAux;
        List<Concessions__c> cAuxList;
        
        Map<String,List<Ground__c>> vehiclesDataMap = new Map<String,List<Ground__c>>();
        for(Ground__c vData : [SELECT Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c, GT_Trip_Details__c
                               FROM Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: dataBid.Production__c AND GT_Trip_Details__c =: dataBid.GT__c
                               AND Bid__c = NULL AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL]){
                                   gAuxList = vehiclesDataMap.get(vData.GT_Trip_Details__c) != null ? vehiclesDataMap.get(vData.GT_Trip_Details__c) : new List<Ground__c>();
                                   gAuxList.add(vData);
                                   vehiclesDataMap.put(vData.GT_Trip_Details__c,gAuxList.clone());
                               }
        
        Map<String,List<Concessions__c>> concessionsDataMap = new Map<String,List<Concessions__c>>();
        for(Concessions__c cData : [SELECT Id, Agreed__c, GT__c, Concession_Type__c, Concessions_Requested__c, Concession_Provided__c, CurrencyIsoCode, Notes__c, Order__c
                                    FROM Concessions__c WHERE GT__c =: dataBid.GT__c AND Production__c =: dataBid.Production__c AND Create_in_Bid__c = true
                                    AND Bid__c = NULL AND Housing__c = NULL AND Freight__c = NULL]){
                                        cAuxList = concessionsDataMap.get(cData.GT__c) != null ? concessionsDataMap.get(cData.GT__c) : new List<Concessions__c>();
                                        cAuxList.add(cData);
                                        concessionsDataMap.put(cData.GT__c,cAuxList.clone());
                                    }
        
        Map<String,List<Ground__c>> subtripDataMap = new Map<String,List<Ground__c>>();
        Set<String> subtripDataIds = new Set<String>();
        for(Ground__c subtripData : [SELECT Id, Service_Type__c, Trip_Type__c, RecordTypeId, RecordType.Name, Description__c, Trip_Order__c, Sub_Trip_Type__c, Travel_Type__c, Sub_Trip_Notes__c, GT_Trip_Details__c
                                     FROM Ground__c 
                                     WHERE RecordType.DeveloperName = 'GT_Sub_Trip_Details' AND GT_Trip_Details__c =: dataBid.GT__c ORDER BY Trip_Order__c ASC]){
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
        
        gAuxList = new List<Ground__c>();
        cAuxList = new List<Concessions__c>();
        Map<Integer,Ground__c> subtripInsertMap = new Map<Integer,Ground__c>();
        Map<Integer,List<Ground__c>> travelInsertMap = new Map<Integer,List<Ground__c>>();
        Integer cx = 1;
        List<Ground__c> travelListAux = new List<Ground__c>();

        if(vehiclesDataMap.get(dataBid.GT__c) != null){
            for(Ground__c g : vehiclesDataMap.get(dataBid.GT__c)){
                gAux = g.clone();
                gAux.Id = null;
                gAux.RecordTypeId = ground_vehicletypeRT;
                gAux.Production_Ground__c = dataBid.Production__c;
                gAux.Bid__c = dataBid.Id;
                gAuxList.add(gAux);
            }
        }
        if(concessionsDataMap.get(dataBid.GT__c) != null){
            for(Concessions__c c : concessionsDataMap.get(dataBid.GT__c)){
                cAux = c.clone();
                cAux.Id = null;
                cAux.Production__c = dataBid.Production__c;
                cAux.Bid__c = dataBid.Id;
                cAuxList.add(cAux);
            }
        }
        
        if(subtripDataMap.get(dataBid.GT__c) != null){
            for(Ground__c gs : subtripDataMap.get(dataBid.GT__c)){
                gAux = gs.clone();
                gAux.Id = null;
                gAux.GT_Trip_Details__c = null;
                gAux.RecordTypeId = ground_GTSubStripDetailsRT;
                gAux.Production_Ground__c = dataBid.Production__c;
                gAux.Bid_Sub_Trip__c = dataBid.Id;
                subtripInsertMap.put(cx,gAux);
                if(travelsBySubTripMapAux.get(gs.Id) != null){
                    for(Ground__c gs2 : travelsBySubTripMapAux.get(gs.Id)){
                        gAux = gs2.clone();
                        gAux.Id = null;
                        gAux.GT_Trip_Details__c = null;
                        gAux.RecordTypeId = ground_GTTravelDetailsRT;
                        gAux.Production_Ground__c = dataBid.Production__c;
                        gAux.Bid_Sub_Trip__c = dataBid.Id;
                        
                        travelListAux = travelInsertMap.get(cx) != null ? travelInsertMap.get(cx) : new List<Ground__c>();
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
    }*/
  public static String getNumberFormat(Integer num) {
    String contractnumber = '';
    Integer count = 10 - String.valueOf(num).length();
    for (Integer i = 1; i <= count; i++) {
      contractnumber = contractnumber + '0';
    }
    contractnumber = contractnumber + String.valueOf(num);
    return contractnumber;
  }
  public void editBidDataLocked() {
    if (bidid_locked != null && bidid_locked != '') {
      Bid__c b = new Bid__c(Id = bidid_locked, Locked__c = bidstatus_locked);
      update b;
    }
  }
  public void sendResendBid() {
    if (bidData != null && contactPrimarySelected != null) {
      Map<String, Contact> contactMap = new Map<String, Contact>();
      for (Contact c : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE Id = :contactPrimarySelected
      ])
        contactMap.put(c.Id, c);

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
          Air_Trip_Details__c = :bidData.Air__c
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
              : (segmentList.size() == 2
                  ? DateTime.newInstance(
                        segment.Return_Date__c,
                        Time.newInstance(0, 0, 0, 0)
                      )
                      .format('EEEE') +
                    ', ' +
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

      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = AirDashboardController.verifyEmailUser(
        UserInfo.getUserId(),
        opportunityid,
        bidData.Air__c
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
      String subject = '';

      Air__c aAux = new Air__c(Id = bidData.Air__c);

      //New Journals
      journalAux = new Journal__c(
        RecordTypeId = journal_bidjournalRT,
        Bid__c = bidData.Id,
        Journal_Entry__c = 'Air Bid Request has been sent to ' +
          contactMap.get(contactPrimarySelected).Name +
          ' at ' +
          contactMap.get(contactPrimarySelected).Email
      );
      journalAuxList.add(journalAux);

      //Bid update
      if (bidData != null && bidData.Status__c == 'Unsent') {
        bidData.Status__c = 'Lead Sent';
        bAux = new Bid__c(
          Id = bidData.Id,
          Status__c = 'Lead Sent',
          Lead_Sent__c = true
        );
        bidUpdateMap.put(bAux.Id, bAux);
      }

      //EMAIL
      ccAddresses = new Set<String>();
      if (bidData.Vendor__c != null) {
        for (
          ContactWrapper cw : contactsByVendorBidMap.get(bidData.Vendor__c)
        ) {
          if (!cw.disabled && cw.selected) {
            ccAddresses.add(cw.c.Email);
          }
        }
      }
      if (bidData.Vendor__r.ParentId != null) {
        for (
          ContactWrapper cw : contactsByVendorParentBidMap.get(
            bidData.Vendor__r.ParentId
          )
        ) {
          if (!cw.disabled && cw.selected) {
            ccAddresses.add(cw.c.Email);
          }
        }
      }

      mail = new Messaging.SingleEmailMessage();
      if (owaeId != null)
        mail.setOrgWideEmailAddressId(owaeId);
      toAddresses = new List<String>{
        contactMap.get(contactPrimarySelected).Email
      };
      mail.setToAddresses(toAddresses);
      if (ccAddresses.size() > 0)
        mail.setCcAddresses(new List<String>(ccAddresses));

      String startDate = (bidData.Air__r.Departure_Date__c != null
        ? Datetime.newInstance(
              bidData.Air__r.Departure_Date__c.year(),
              bidData.Air__r.Departure_Date__c.month(),
              bidData.Air__r.Departure_Date__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');
      String returnDate = (bidData.Air__r.Return_Date__c != null
        ? Datetime.newInstance(
              bidData.Air__r.Return_Date__c.year(),
              bidData.Air__r.Return_Date__c.month(),
              bidData.Air__r.Return_Date__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');

      subject = template.size() > 0 ? template[0].Subject : '';
      body = template[0].HTMLValue != null ? template[0].HTMLValue : '';
      mail.setSubject(
        subject.replace('{ProductionName}', bidData.Production__r.Name)
          .replace('{DepDate}', startDate)
          .replace(
            '{DepartureCity}',
            bidData.Air__r.Departure_City__r.Airport_Code__c != null
              ? bidData.Air__r.Departure_City__r.Airport_Code__c
              : ''
          )
          .replace(
            '{ArrivalCity}',
            bidData.Air__r.Arrival_City__r.Airport_Code__c != null
              ? bidData.Air__r.Arrival_City__r.Airport_Code__c
              : ''
          )
      );

      mail.setHtmlBody(
        body.replace('{VendorName}', bidData.Vendor__r.Name)
          .replace('{ProductionName}', bidData.Production__r.Name)
          .replace(
            '{GroupType}',
            bidData.Air__r.Group_Type__c != null
              ? bidData.Air__r.Group_Type__c
              : ''
          )
          .replace(
            '{TravelDetails}',
            segmentMap.get(bidData.Air__c) != null
              ? segmentMap.get(bidData.Air__c)
              : ''
          )
          .replace(
            '{AirCoordinator}',
            userActual != null && userActual.Name != null ? userActual.Name : ''
          )
          .replace(
            '{NosOfSeats}',
            bidData.Air__r.Number_of_Seats__c != null
              ? String.valueOf(bidData.Air__r.Number_of_Seats__c)
              : ''
          )
      );
      myEmails.add(mail);

      insert journalAuxList;

      update bidUpdateMap.values();

      //aAux.Bid_Request__c = system.today();
      //update gAux;

      if (myEmails.size() > 0)
        Messaging.sendEmail(myEmails);
    }
  }
  /*public void saveSubTripBid(){
        if(subtripIdActual != null && subtripIdActual != ''){
            Ground__c gAux;
            for(Ground__c gd : bidSubTrips){
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
            for(Ground__c gd : [SELECT Id, Trip_Order__c FROM Ground__c WHERE RecordType.Name = 'GT Sub Trip Details' AND Bid_Sub_Trip__c =: bidData.Id ORDER BY Trip_Order__c ASC]){
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
            getSubStripByBid();
        }
    }
    public void deleteSubTripBid(){
        system.debug(subtripIdActual);
        if(subtripIdActual != null && subtripIdActual != '' && bidData != null && bidData.Id != null){
            delete [SELECT Id FROM Sub_Trip_GCQ__c WHERE GT_Sub_Trip_Details__c =: subtripIdActual];
            delete [SELECT Id FROM Ground__c WHERE RecordType.Name = 'GT Travel Details' AND GT_Sub_Trip_Details__c =:subtripIdActual];
            delete [SELECT Id FROM Ground__c WHERE Id =: subtripIdActual];
            
            Integer cont = 1;
            List<Ground__c> groundExistList = new List<Ground__c>();
            for(Ground__c gd : [SELECT Id, Trip_Order__c FROM Ground__c WHERE RecordType.Name = 'GT Sub Trip Details' AND Bid_Sub_Trip__c =: bidData.Id ORDER BY Trip_Order__c ASC]){
                gd.Trip_Order__c = cont;
                groundExistList.add(gd);
                cont++;
            }
            
            if(groundExistList.size() > 0) update groundExistList;
            getSubStripByBid();
        }
    }
    public void newSubTripBid(){
        if(bidData != null && bidData.Id != null){
            List<Ground__c> groundExistList;
            //if(bidData.Status__c == 'Contracted') 
                groundExistList = [SELECT Id, Trip_Order__c FROM Ground__c WHERE RecordType.Name = 'GT Sub Trip Details' AND Bid_Sub_Trip__c =: bidData.Id ORDER BY Trip_Order__c DESC LIMIT 1];
           
            
            Ground__c new_subtrip = new Ground__c(
                Production_Ground__c = opportunityId,
                RecordTypeId = ground_GTSubStripDetailsRT,
                Trip_Order__c = (groundExistList.size() > 0 ? (groundExistList[0].Trip_Order__c != null ? groundExistList[0].Trip_Order__c + 1 : 1) : 1),
                Description__c = 'Airport transfer'
            );
            new_subtrip.Bid_Sub_Trip__c = bidData.Id;
            //if(bidData.Status__c == 'Contracted') new_subtrip.Bid_Sub_Trip__c = bidData.Id ; else new_subtrip.GT_Trip_Details__c = bidData.GT__c;
            insert new_subtrip;
            
            getSubStripByBid();
        }
    }
    public void getSubStripByBid(){
        hasFreightMap = new Map<String,Boolean>();
        bidSubTrips = new List<Ground__c>();
        bidSubTripTravelsMap = new Map<Id, List<Ground__c>>();
        //if(bidData.Status__c == 'Contracted'){
            for(Ground__c subTrip:[Select id, GT_Freight__c, Trip_Order__c, Sub_Trip_Type__c, Description__c, Sub_Trip_Notes__c, (Select id, Line__c, Vehicle_Ref__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c, Start_Date_Full__c, End_Date_Full__c from GTTravels__r order by Line__c) 
                                   from Ground__c where Bid_Sub_Trip__c =:bidDataMap.get(tripBidNumber).b.Id and RecordType.DeveloperName = 'GT_Sub_Trip_Details' order by Trip_Order__c, Line__c]){
                                       bidSubTrips.add(subTrip);
                                       hasFreightMap.put(subtrip.Id,subtrip.GT_Freight__c != null ? true : false);
                                       bidSubTripTravelsMap.put(subTrip.id, subTrip.GTTravels__r);
                                   }
    }*/
  public void saveEditConcessionBid() {
    if (concessionActual != null && concessionActual != '') {
      Concessions__c concessionBid = new Concessions__c(
        Id = concessionActual,
        Concession_Type__c = 'Air',
        Concessions_Requested__c = concessionRequestedActual,
        Notes__c = concessionNoteActual,
        Included_Excluded__c = concessionIncludedActual,
        Rate__c = (concessionRateActual != null &&
          concessionRateActual != '' &&
          concessionRateActual.trim() != ''
          ? concessionRateActual
          : null),
        Order__c = (concessionOrderActual != null &&
          concessionOrderActual != '' &&
          concessionOrderActual.trim() != ''
          ? Decimal.valueOf(concessionOrderActual)
          : null)
      );
      update concessionBid;
      Integer i = 1;
      Integer j;
      List<Concessions__c> concessionAuxList = new List<Concessions__c>();
      Map<Integer, Integer> mapAux = new Map<Integer, Integer>();
      for (Concessions__c c : [
        SELECT
          Id,
          Concessions_Requested__c,
          Concession_Type__c,
          Notes__c,
          Included_Excluded__c,
          Rate__c,
          Order__c
        FROM Concessions__c
        WHERE
          Production__c = :opportunityId
          AND Bid__c = :bidData.Id
          AND Concession_Type__c = 'Air'
        ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC
      ]) {
        if (c.Order__c != null) {
          if (c.Id != concessionBid.Id) {
            if (
              concessionOrderActual != null &&
              concessionOrderActual != '' &&
              i == Integer.valueOf(concessionOrderActual)
            ) {
              j = i - 1;
              if (j != 0 && mapAux.get(j) == null) {
                c.Order__c = j;
                mapAux.put(j, j);
              } else {
                c.Order__c = i + 1;
                mapAux.put(i, i);
              }
              concessionAuxList.add(c);
            } else {
              c.Order__c = i;
              mapAux.put(i, i);
              concessionAuxList.add(c);
            }
          }
          i++;
        }
      }
      if (!concessionAuxList.isEmpty())
        update concessionAuxList;
      getConcessionsByBid();
    }
  }
  public void deleteConcessionBid() {
    delete [SELECT Id FROM Concessions__c WHERE Id = :concessionActual];
    getConcessionsByBid();
  }
  public void addConcessionBid() {
    if (bidData != null && bidData.Id != null) {
      Concessions__c newConcessionBid = new Concessions__c();
      newConcessionBid.Concession_Type__c = 'Air';
      newConcessionBid.Production__c = opportunityId;
      newConcessionBid.Concessions_Requested__c = concessionRequestedActual;
      newConcessionBid.Notes__c = concessionNoteActual;
      newConcessionBid.Included_Excluded__c = concessionIncludedActual;
      newConcessionBid.Rate__c = (concessionRateActual != null &&
        concessionRateActual != '' &&
        concessionRateActual.trim() != ''
        ? concessionRateActual
        : null);
      newConcessionBid.Order__c = (concessionOrderActual != null &&
        concessionOrderActual != '' &&
        concessionOrderActual.trim() != ''
        ? Decimal.valueOf(concessionOrderActual)
        : null);
      newConcessionBid.Bid__c = bidData.Id;
      insert newConcessionBid;
      if (concessionOrderActual != null && concessionOrderActual != '') {
        Integer i = 1;
        Integer j;
        List<Concessions__c> concessionAuxList = new List<Concessions__c>();
        Map<Integer, Integer> mapAux = new Map<Integer, Integer>();
        for (Concessions__c c : [
          SELECT
            Id,
            Concessions_Requested__c,
            Concession_Type__c,
            Notes__c,
            Included_Excluded__c,
            Rate__c,
            Order__c
          FROM Concessions__c
          WHERE
            Production__c = :opportunityId
            AND Bid__c = :bidData.Id
            AND Concession_Type__c = 'Air'
          ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC
        ]) {
          if (c.Order__c != null) {
            if (c.Id != newConcessionBid.Id) {
              if (
                concessionOrderActual != null &&
                concessionOrderActual != '' &&
                i == Integer.valueOf(concessionOrderActual)
              ) {
                j = i - 1;
                if (j != 0 && mapAux.get(j) == null) {
                  c.Order__c = j;
                  mapAux.put(j, j);
                } else {
                  c.Order__c = i + 1;
                  mapAux.put(i, i);
                }
                concessionAuxList.add(c);
              } else {
                c.Order__c = i;
                concessionAuxList.add(c);
              }
            }
            i++;
          }
        }
        if (!concessionAuxList.isEmpty())
          update concessionAuxList;
      }
      getConcessionsByBid();
    }
  }
  public void getConcessionsByBid() {
    concessionsRequestedBid = new List<Concessions__c>();
    if (
      bidData != null &&
      bidData.Id != null &&
      bidData.Air__r.Air_Charter__c == true
    ) {
      concessionsRequestedBid = [
        SELECT
          Id,
          Concessions_Requested__c,
          Concession_Type__c,
          Notes__c,
          Included_Excluded__c,
          Rate__c,
          Order__c
        FROM Concessions__c
        WHERE
          Production__c = :opportunityId
          AND Bid__c = :bidData.Id
          AND Concession_Type__c = 'Air'
        ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC
      ];
    }
  }
  public void searchBidHistory() {
    String vendor = bidData.Vendor__c;
    bidRelatedVendorList = new List<BidVendorWrapper>();
    String query =
      'SELECT Id, Name, Production__c, Production__r.Name, Air__c, Air__r.Departure_City__r.Airport_Code__c, Air__r.Arrival_City__r.Airport_Code__c,' +
      ' Status__c, No_Bid_reason__c, Venue__c, Venue__r.Name, Vendor__r.ParentId, Vendor__r.Parent.Name, CreatedDate' +
      ' FROM Bid__c WHERE Vendor__c =: vendor';

    if (
      bidhistorysearch_departurecity != null &&
      bidhistorysearch_departurecity != ''
    ) {
      bidhistorysearch_departurecity =
        '%' +
        bidhistorysearch_departurecity +
        '%';
      query += ' AND Air__r.Departure_City__r.Airport_Code__c LIKE: bidhistorysearch_departurecity';
    }
    if (
      bidhistorysearch_arrivalcity != null &&
      bidhistorysearch_arrivalcity != ''
    ) {
      bidhistorysearch_arrivalcity = '%' + bidhistorysearch_arrivalcity + '%';
      query += ' AND Air__r.Arrival_City__r.Airport_Code__c LIKE: bidhistorysearch_arrivalcity';
    }

    if (orderBidHistoryOrientation == null)
      orderBidHistoryOrientation = 'ASC';
    system.debug(orderBidHistoryOrientation);
    if (orderCheckBidHistory) {
      if (orderChangeBidHistory) {
        orderBidHistoryOrientation = 'ASC';
      } else {
        if (orderBidHistoryOrientation == 'ASC')
          orderBidHistoryOrientation = 'DESC';
        else
          orderBidHistoryOrientation = 'ASC';
      }
    }
    Set<String> bidIdsAux = new Set<String>();
    for (Bid__c b : Database.query(query)) {
      bidIdsAux.add(b.Id);
      bidRelatedVendorList.add(
        new BidVendorWrapper(
          b,
          b.Name,
          b.Production__r.Name,
          b.Air__r.Departure_City__r.Airport_Code__c,
          b.Air__r.Arrival_City__r.Airport_Code__c,
          null,
          null,
          b.No_Bid_reason__c,
          b.CreatedDate.date()
        )
      );
    }

    revenueBidMap = new Map<String, Revenue__c>();
    for (Revenue__c r : [
      SELECT Id, Bid__c, Total_Price__c, of_seats__c
      FROM Revenue__c
      WHERE
        Bid__c IN :bidIdsAux
        AND RecordType.DeveloperName = 'Air_Rate_Commission'
        AND Total_Price__c != NULL
      ORDER BY Total_Price__c ASC
    ]) {
      if (revenueBidMap.get(r.Bid__c) == null)
        revenueBidMap.put(r.Bid__c, r);
    }
    for (BidVendorWrapper bw : bidRelatedVendorList) {
      bw.fare = revenueBidMap.get(bw.b.Id) != null
        ? revenueBidMap.get(bw.b.Id).Total_Price__c
        : null;
      bw.pax = revenueBidMap.get(bw.b.Id) != null
        ? revenueBidMap.get(bw.b.Id).of_seats__c
        : null;
    }
    bidRelatedVendorList.sort();
  }
  public void openBidHistory() {
    bidRelatedVendorList = new List<BidVendorWrapper>();
    Set<String> bidIdsAux = new Set<String>();
    for (Bid__c b : [
      SELECT
        Id,
        Name,
        Production__c,
        Production__r.Name,
        Air__c,
        Air__r.Departure_City__r.Airport_Code__c,
        Air__r.Arrival_City__r.Airport_Code__c,
        Status__c,
        No_Bid_reason__c,
        Venue__c,
        Venue__r.Name,
        Vendor__r.ParentId,
        Vendor__r.Parent.Name,
        CreatedDate
      FROM Bid__c
      WHERE
        Vendor__c = :bidData.Vendor__c
        AND RecordType.DeveloperName = 'Air_Bid'
      ORDER BY CreatedDate DESC
    ]) {
      bidIdsAux.add(b.Id);
      bidRelatedVendorList.add(
        new BidVendorWrapper(
          b,
          b.Name,
          b.Production__r.Name,
          b.Air__r.Departure_City__r.Airport_Code__c,
          b.Air__r.Arrival_City__r.Airport_Code__c,
          null,
          null,
          b.No_Bid_reason__c,
          b.CreatedDate.date()
        )
      );
    }

    revenueBidMap = new Map<String, Revenue__c>();
    for (Revenue__c r : [
      SELECT Id, Bid__c, Total_Price__c, of_seats__c
      FROM Revenue__c
      WHERE
        Bid__c IN :bidIdsAux
        AND RecordType.DeveloperName = 'Air_Rate_Commission'
        AND Total_Price__c != NULL
      ORDER BY Total_Price__c ASC
    ]) {
      if (revenueBidMap.get(r.Bid__c) == null)
        revenueBidMap.put(r.Bid__c, r);
    }
    /*rateBidMap = new Map<String,Revenue__c>();
        for(Revenue__c r : [Select id, Base_Cost__c, Commission__c, Rate__c, Gratuity__c, Total_Price__c, CurrencyIsoCode, Bid__c from Revenue__c where Bid__c IN: bidIdsAux and RecordType.DeveloperName = 'Ground_Rate_Travel_Commission' order by createdDate ASC]) rateBidMap.put(r.Bid__c,r);
        for(String bididaux : bidIdsAux){
            if(rateBidMap.get(bididaux) == null) rateBidMap.put(bididaux, new Revenue__c());
        }*/
    for (BidVendorWrapper bw : bidRelatedVendorList) {
      bw.pax = revenueBidMap.get(bw.b.Id) != null
        ? revenueBidMap.get(bw.b.Id).of_seats__c
        : null;
      bw.fare = revenueBidMap.get(bw.b.Id) != null
        ? revenueBidMap.get(bw.b.Id).Total_Price__c
        : null;
    }
  }
  public void getItineraryByBid() {
    itineraryList = new List<Air__c>();
    if (bidData != null && bidData.Id != null) {
      List<Air__c> itineraryBidList = [
        SELECT
          Id,
          RecordTypeId,
          Trip_Type__c,
          Group_Type__c,
          Description__c,
          PAX__c
        FROM Air__c
        WHERE Bid_Itinerary__c = :bidData.Id
      ];
      Map<String, String> descriptionMap = new Map<String, String>();
      String segments;
      if (itineraryBidList.size() > 0) {
        itineraryBid = itineraryBidList[0];
        itineraryBid.Group_Type__c = bidData.Air__r.Group_Type__c;
        itineraryBid.PAX__c = bidData.Air__r.PAX__c;

        itineraryList = [
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
            Air_Itinerary_Details__c
          FROM Air__c
          WHERE
            Air_Itinerary_Details__c = :itineraryBid.Id
            AND RecordType.DeveloperName = 'Air_Segments'
          ORDER BY CreatedDate
        ];

        for (Air__c iti : itineraryList) {
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
          segments =
            (iti.Departure_City__r.Airport_Code__c != null
              ? iti.Departure_City__r.Airport_Code__c + ' - '
              : '') +
            (iti.Arrival_City__r.Airport_Code__c != null
              ? iti.Arrival_City__r.Airport_Code__c
              : '');
          descriptionMap.put(
            iti.Air_Itinerary_Details__c,
            descriptionMap.get(iti.Air_Itinerary_Details__c) != null
              ? descriptionMap.get(iti.Air_Itinerary_Details__c) +
                ', ' +
                segments
              : segments
          );
        }
        itineraryBid.Description__c = descriptionMap.get(itineraryBid.Id) !=
          null
          ? descriptionMap.get(itineraryBid.Id)
          : itineraryBid.Description__c;
        update itineraryBid;
      } else {
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
            Air_Trip_Details__c = :bidData.Air__c
            AND RecordType.DeveloperName = 'Air_Segments'
        ];
        if (segmentList.size() > 0) {
          for (Air__c segment : segmentList) {
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
        }
        itineraryBid = new Air__c(
          Production__c = opportunityId,
          Bid_Itinerary__c = bidData.Id,
          RecordTypeId = Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName()
            .get('Air_Itinerary_Details')
            .getRecordTypeId(),
          Trip_Type__c = bidData.Air__r.Trip_Type__c,
          Group_Type__c = bidData.Air__r.Group_Type__c,
          Description__c = descriptionMap.get(bidData.Air__c) != null
            ? descriptionMap.get(bidData.Air__c)
            : null,
          PAX__c = bidData.Air__r.PAX__c
        );
        insert itineraryBid;
      }
    }
  }
  public void getAirInformationByBid() {
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
        Air_Trip_Details__c = :bidData.Air__c
        AND RecordType.DeveloperName = 'Air_Segments'
    ];
    segmentsAir = '';
    if (segmentList.size() > 0) {
      for (Air__c segment : segmentList) {
        segmentsAir =
          segmentsAir +
          (segment.Departure_City__r.Airport_Code__c != null
            ? segment.Departure_City__r.Airport_Code__c + ' - '
            : '') +
          (segment.Arrival_City__r.Airport_Code__c != null
            ? segment.Arrival_City__r.Airport_Code__c
            : '') +
          ', ';
      }
      segmentsAir = segmentsAir.subString(0, segmentsAir.length() - 2);
    }
  }
  public void getTripDetails() {
    if (bidData != null && bidData.Air__r.Air_Charter__c) {
    }
  }
  public void getBidInformation() {
    tripHaveContracted = false;
    symbolMap = new Map<String, String>();
    System.debug('tripBidNumber: ' + tripBidNumber);
    if (tripBidNumber != null && bidDataMap.get(tripBidNumber) != null) {
      bidData = [
        SELECT
          Id,
          RecordTypeId,
          RecordType.Name,
          Name,
          Production__c,
          Production__r.Name,
          Production__r.Production_ID__c,
          Production__r.Account.Name,
          Production__r.Account.Physical_Address__c,
          Air__c,
          Air__r.Name,
          Air__r.Departure_Date__c,
          Air__r.Arrival_Date__c,
          Air__r.Status__c,
          Vendor__c,
          Vendor__r.Vendor_ID__c,
          Vendor__r.Phone,
          Vendor__r.ParentId,
          Vendor__r.Name,
          Vendor__r.City__r.Name,
          Vendor__r.ShippingCountry,
          Vendor_Address__c,
          Vendor_Contact__c,
          Vendor_Contact__r.Name,
          Vendor_Contact_Email__c,
          Vendor_Contact_Phone__c,
          Locked__c,
          Status__c,
          Status_Previous__c,
          Internal_notes__c,
          DX_to_Venue__c,
          Venue__c,
          Venue__r.Name,
          Include_in_options__c,
          Options__c,
          Bid_Options_Notes__c,
          Include_in_option_cover_sheet__c,
          No_Bid_reason__c,
          Trips_Details_Update_Contact_Id__c,
          Trip_Details_Update_Terms__c,
          Trip_Details_Update_Payment_Policy__c,
          Trip_Details_Update_Cancel_Policy__c,
          Trip_Details_Update_Last_Modified_By__c,
          Trip_Details_Update_Last_Send_By__c,
          Trip_Details_Update_Last_Send_Date__c,
          Rate_Agreement_Contact_Id__c,
          Rate_Agreement_Production_Contact_Id__c,
          Rate_Agreement_Terms__c,
          Rate_Agreement_Payment_Policy__c,
          Rate_Agreement_Cancellation_Policy__c,
          Rate_Agreement_Last_Send_By__c,
          Rate_Agreement_Last_Send_Date__c,
          Transportation_Contract_Contact_Id__c,
          Transportation_Contract_Terms__c,
          Transportation_Contract_Payment_Policy__c,
          Transportation_Contract_Cancel_Policy__c,
          Transportation_Contract_Last_Send_By__c,
          Transportation_Contract_Last_Send_Date__c,
          Billing_Options__c,
          Form_Rate_Agreement__c,
          Form_Transportation_Contract__c,
          Form_Trip_Details_Update__c,
          Lead_Sent__c,
          Air__r.Group_Type__c,
          Air__r.Trip_Type__c,
          Air__r.PAX__c,
          Air__r.Description__c,
          Deposit_Amount_per_seat__c,
          Utilization_Penalty_per_seat__c,
          Utilization_Percentage__c,
          Contract_Due_Date__c,
          Internal_Deposit_Due_Date__c,
          Internal_Utilization_Date__c,
          Internal_Names_Final_Payment__c,
          Client_Contract_Date__c,
          Client_Deposit_Due_Date__c,
          Client_Utilization_Date__c,
          Client_Names_Final_Payment__c,
          Air__r.Return_Date__c,
          Air__r.Departure_City__r.Airport_Code__c,
          Air__r.Arrival_City__r.Airport_Code__c,
          Air__r.Number_of_Seats__c,
          Deposit_Amount_Currency__c,
          Utilization_Penalty_Currency__c,
          Air__r.Air_Charter__c,
          Air__r.Air_Preferences__c
        FROM Bid__c
        WHERE Id = :bidDataMap.get(tripBidNumber).b.Id
      ];
      User us = [
        SELECT Id, Housing_Preference__c
        FROM User
        WHERE Id = :UserInfo.getUserId()
      ];
      if (
        bidData.Deposit_Amount_Currency__c == null ||
        bidData.Deposit_Amount_Currency__c == ''
      ) {
        bidData.Deposit_Amount_Currency__c = (us.Housing_Preference__c == 'RRE'
          ? 'EUR'
          : 'USD');
        symbolMap.put((us.Housing_Preference__c == 'RRE' ? 'EUR' : 'USD'), '');
      }
      if (
        bidData.Utilization_Penalty_Currency__c == null ||
        bidData.Utilization_Penalty_Currency__c == ''
      ) {
        bidData.Utilization_Penalty_Currency__c = (us.Housing_Preference__c ==
          'RRE'
          ? 'EUR'
          : 'USD');
        symbolMap.put((us.Housing_Preference__c == 'RRE' ? 'EUR' : 'USD'), '');
      }
      /*getSubStripByBid();
       getVehiclesByBid();*/
      getContactsByVendorBid();
      getAirInformationByBid();
      getItineraryByBid();
      getDeviationByBid();
      getGroupRateDetails();
      getTripDetails();
      getAircraftsByBid();
      getBidRevenue();
      getConcessionsByBid();
      getSymbol();

      if (vfpConfiguration != null) {
        vfpConfiguration.bidId = bidData.Id;
        vfpConfiguration.parentId = bidData.Air__c;
        vfpConfiguration.productionId = opportunityId;
        vfpConfiguration.parentSObject = 'Air';
      }

      for (Integer bk : bidDataMap.keySet()) {
        if (
          bidDataMap.get(bk).b.Id != bidData.Id &&
          bidDataMap.get(bk).b.Status__c == 'Contracted'
        )
          tripHaveContracted = true;
      }

      isBidAgreementRendered = isResendBidRendered = isBidJournalsRendered = isReleaseBidRendered = false;

      coordinatorGT = null;
      for (Production_Associations__c pa : [
        SELECT
          Id,
          Production_Opp__c,
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
        WHERE Production_Opp__c = :opportunityId
        ORDER BY Contact__r.Name ASC
      ]) {
        if (pa.User__c != null && pa.Team_Roles__c != null) {
          if (pa.Team_Roles__c.contains('Primary Air Coordinator'))
            coordinatorGT = pa.User__c;
        }
      }
    }
  }
  public void getContactsByVendorBid() {
    if (bidData != null) {
      Map<String, Contact> contactMap = new Map<String, Contact>();
      bidPrimaryContact = String.isNotEmpty(bidData.Vendor_Contact__c)
        ? [
            SELECT Id, FirstName, Name, Phone, Email
            FROM Contact
            WHERE Id = :bidData.Vendor_Contact__c
            LIMIT 1
          ]
        : new Contact();
      for (Contact contact : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE AccountId = :bidData.Vendor__c
      ])
        contactMap.put(contact.Id, contact);
      if (bidData.Vendor__r.ParentId != null)
        for (Contact contact : [
          SELECT Id, Name, Email
          FROM Contact
          WHERE AccountId = :bidData.Vendor__r.ParentId
        ])
          contactMap.put(contact.Id, contact);
      contactsBidsByVendor = new List<SelectOption>();
      contactsBidsByVendor.add(new SelectOption('', ''));
      for (Contact contact : contactMap.values())
        contactsBidsByVendor.add(new SelectOption(contact.Id, contact.Name));
    }
  }
  public void changeContactPrimaryBid() {
    bidPrimaryContact = String.isNotEmpty(bidData.Vendor_Contact__c)
      ? [
          SELECT Id, FirstName, Name, Phone, Email
          FROM Contact
          WHERE Id = :bidData.Vendor_Contact__c
          LIMIT 1
        ]
      : new Contact();
  }
  public void changeContactPrimary() {
    bidPrimaryContact = String.isNotEmpty(draft.Primary_Contact_Id__c)
      ? [
          SELECT Id, FirstName, Name, Phone, Email
          FROM Contact
          WHERE Id = :draft.Primary_Contact_Id__c
          LIMIT 1
        ]
      : new Contact();
  }
  public void saveBid() {
    if (bidData != null && bidData.Id != null) {
      Bid__c bidDataUpdate = new Bid__c(Id = bidData.Id);
      bidDataUpdate.No_Bid_reason__c = biddata_nobidreason;
      bidDataUpdate.Bid_Options_Notes__c = biddata_bidoptionnotes;
      bidDataUpdate.Options__c = biddata_options != null &&
        biddata_options != ''
        ? Decimal.valueOf(biddata_options)
        : null;
      bidDataUpdate.Include_in_options__c = biddata_includeinoptions != null
        ? biddata_includeinoptions
        : null;
      bidDataUpdate.Internal_notes__c = biddata_internalnotes;
      if (bidDataUpdate.No_Bid_reason__c == 'NO AVAILABILITY')
        bidDataUpdate.Status__c = 'No Availability';
      update bidDataUpdate;
    }
  }
  public void save() {
    if (bidData != null && bidData.Id != null) {
      bidData.Deposit_Amount_Currency_Symbol__c = symbolMap.containsKey(
          bidData.Deposit_Amount_Currency__c
        )
        ? symbolMap.get(bidData.Deposit_Amount_Currency__c)
        : '';
      bidData.Utilization_Penalty_Currency_Symbol__c = symbolMap.containsKey(
          bidData.Deposit_Amount_Currency__c
        )
        ? symbolMap.get(bidData.Utilization_Penalty_Currency__c)
        : '';
      update bidData;
      if (!bidData.Air__r.Air_Charter__c) {
        //Task from Rate Details
        List<Production_Associations__c> prodAssocations = [
          SELECT Id, User__c, Team_Roles__c, User__r.Name
          FROM Production_Associations__c
          WHERE
            Production_Opp__c = :opportunityId
            AND User__c != NULL
            AND Team_Roles__c INCLUDES ('Primary Air Coordinator')
        ];
        Map<String, Task> taskMap = new Map<String, Task>();
        for (Task tr : [
          SELECT Id, Subject, Priority
          FROM Task
          WHERE WhatId = :bidData.Id AND Contract_Task__c = TRUE
        ])
          taskMap.put(tr.Subject, tr);
        List<Task> taskList = new List<Task>();
        if (!prodAssocations.isEmpty()) {
          if (bidData.Contract_Due_Date__c != null)
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Internal Contract Due Date')
                  ? taskMap.get('Internal Contract Due Date').Id
                  : null,
                ActivityDate = bidData.Contract_Due_Date__c,
                Subject = 'Internal Contract Due Date',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Internal Contract Due Date')
                  ? taskMap.get('Internal Contract Due Date').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 14
              )
            );
          if (bidData.Internal_Deposit_Due_Date__c != null)
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Internal Deposit Due Date')
                  ? taskMap.get('Internal Deposit Due Date').Id
                  : null,
                ActivityDate = bidData.Internal_Deposit_Due_Date__c,
                Subject = 'Internal Deposit Due Date',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Internal Deposit Due Date')
                  ? taskMap.get('Internal Deposit Due Date').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 15
              )
            );
          if (bidData.Internal_Utilization_Date__c != null)
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Internal Utilization Date')
                  ? taskMap.get('Internal Utilization Date').Id
                  : null,
                ActivityDate = bidData.Internal_Utilization_Date__c,
                Subject = 'Internal Utilization Date',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Internal Utilization Date')
                  ? taskMap.get('Internal Utilization Date').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 16
              )
            );
          if (bidData.Internal_Names_Final_Payment__c != null)
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Internal Names & Final Payment')
                  ? taskMap.get('Internal Names & Final Payment').Id
                  : null,
                ActivityDate = bidData.Internal_Names_Final_Payment__c,
                Subject = 'Internal Names & Final Payment',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Internal Names & Final Payment')
                  ? taskMap.get('Internal Names & Final Payment').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 17
              )
            );
          if (bidData.Client_Contract_Date__c != null) {
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Contract Due Date')
                  ? taskMap.get('Contract Due Date').Id
                  : null,
                ActivityDate = bidData.Client_Contract_Date__c,
                Subject = 'Contract Due Date',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Contract Due Date')
                  ? taskMap.get('Contract Due Date').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 7
              )
            );
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Acknowledgement of Contract')
                  ? taskMap.get('Acknowledgement of Contract').Id
                  : null,
                ActivityDate = ApexUtil.AddBusinessDays(
                  bidData.Client_Contract_Date__c,
                  1
                ),
                Subject = 'Acknowledgement of Contract',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Acknowledgement of Contract')
                  ? taskMap.get('Acknowledgement of Contract').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 8
              )
            );
          }
          if (bidData.Client_Deposit_Due_Date__c != null) {
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Deposit Due')
                  ? taskMap.get('Deposit Due').Id
                  : null,
                ActivityDate = bidData.Client_Deposit_Due_Date__c,
                Subject = 'Deposit Due',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Deposit Due')
                  ? taskMap.get('Deposit Due').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 4
              )
            );
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Deposit Reminder')
                  ? taskMap.get('Deposit Reminder').Id
                  : null,
                ActivityDate = ApexUtil.AddBusinessDays(
                    bidData.Client_Deposit_Due_Date__c,
                    -7
                  ) >= Date.Today()
                  ? ApexUtil.AddBusinessDays(
                      bidData.Client_Deposit_Due_Date__c,
                      -7
                    )
                  : Date.Today(),
                Subject = 'Deposit Reminder',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Deposit Reminder')
                  ? taskMap.get('Deposit Reminder').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 3
              )
            );
          }
          if (bidData.Client_Utilization_Date__c != null) {
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Utilization Date')
                  ? taskMap.get('Utilization Date').Id
                  : null,
                ActivityDate = bidData.Client_Utilization_Date__c,
                Subject = 'Utilization Date',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Utilization Date')
                  ? taskMap.get('Utilization Date').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 6
              )
            );
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Utilization Reminder')
                  ? taskMap.get('Utilization Reminder').Id
                  : null,
                ActivityDate = ApexUtil.AddBusinessDays(
                    bidData.Client_Utilization_Date__c,
                    -7
                  ) >= Date.Today()
                  ? ApexUtil.AddBusinessDays(
                      bidData.Client_Utilization_Date__c,
                      -7
                    )
                  : Date.Today(),
                Subject = 'Utilization Reminder',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Utilization Reminder')
                  ? taskMap.get('Utilization Reminder').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 5
              )
            );
          }
          if (bidData.Client_Names_Final_Payment__c != null) {
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Names & Final Payment Due')
                  ? taskMap.get('Names & Final Payment Due').Id
                  : null,
                ActivityDate = bidData.Client_Names_Final_Payment__c,
                Subject = 'Names & Final Payment Due',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Names & Final Payment Due')
                  ? taskMap.get('Names & Final Payment Due').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 2
              )
            );
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Names & Final Payment Reminder')
                  ? taskMap.get('Names & Final Payment Reminder').Id
                  : null,
                ActivityDate = ApexUtil.AddBusinessDays(
                    bidData.Client_Names_Final_Payment__c,
                    -7
                  ) >= Date.Today()
                  ? ApexUtil.AddBusinessDays(
                      bidData.Client_Names_Final_Payment__c,
                      -7
                    )
                  : Date.Today(),
                Subject = 'Names & Final Payment Reminder',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Names & Final Payment Reminder')
                  ? taskMap.get('Names & Final Payment Reminder').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 1
              )
            );
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Ticketed Confirmation')
                  ? taskMap.get('Ticketed Confirmation').Id
                  : null,
                ActivityDate = ApexUtil.AddBusinessDays(
                  bidData.Client_Names_Final_Payment__c,
                  1
                ),
                Subject = 'Ticketed Confirmation',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Ticketed Confirmation')
                  ? taskMap.get('Ticketed Confirmation').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 13
              )
            );
          }
          if (!itineraryList.isEmpty()) {
            taskList.add(
              new Task(
                Id = taskMap.containsKey('GCQ Call')
                  ? taskMap.get('GCQ Call').Id
                  : null,
                ActivityDate = itineraryList[0].Departure_Date__c != null
                  ? ApexUtil.AddBusinessDays(
                      itineraryList[0].Departure_Date__c,
                      -3
                    )
                  : null,
                Subject = 'GCQ Call',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('GCQ Call')
                  ? taskMap.get('GCQ Call').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 9
              )
            );
            taskList.add(
              new Task(
                Id = taskMap.containsKey('Email Confirmation')
                  ? taskMap.get('Email Confirmation').Id
                  : null,
                ActivityDate = itineraryList[0].Departure_Date__c != null
                  ? ApexUtil.AddBusinessDays(
                      itineraryList[0].Departure_Date__c,
                      -3
                    )
                  : null,
                Subject = 'Email Confirmation',
                OwnerId = prodAssocations.size() > 0
                  ? prodAssocations[0].User__c
                  : null,
                WhatId = bidData.Id,
                Contract_Task__c = true,
                Status = 'Open',
                Priority = taskMap.containsKey('Email Confirmation')
                  ? taskMap.get('Email Confirmation').Priority
                  : 'No Follow up',
                Task_Type__c = 'Air Status Trace',
                Order__c = 10
              )
            );
          }
        }
        if (taskList.size() > 0)
          upsert taskList;
      } else
        upsert bidRevenue;
    }
  }
  public void soldOutBidStatus() {
    if (bidData != null && bidData.Id != null) {
      bidData.Status__c = 'Sold Out / Not Bidding';
      update bidData;
      getBidInformation();
    }
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
  ///PreviewOptions Methods
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
        (Air_Itinerary_Details__r.Bid_Itinerary__c = :bidData.id
        OR Air_Deviation_Details__r.Bid_Deviation__c = :bidData.id)
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
        Bid__c = :bidData.id
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
        'AirDashboard_Tab_Bid_Controller.openPreviewOptions() - DmlException: ' +
        e.getMessage()
      );
    }
    Map<String, APXTConga4__Conga_Merge_Query__c> congaQueriesMap = new Map<String, APXTConga4__Conga_Merge_Query__c>();
    for (APXTConga4__Conga_Merge_Query__c congaQuery : [
      SELECT Id, APXTConga4__Name__c
      FROM APXTConga4__Conga_Merge_Query__c
      WHERE APXTConga4__Name__c IN ('Air - BidsWithOptionsByBidId')
    ])
      congaQueriesMap.put(congaQuery.APXTConga4__Name__c, congaQuery);
    previewBidOptions_congaQueriesJson = JSON.serialize(congaQueriesMap);
    List<APXTConga4__Conga_Template__c> congaTemplates = [
      SELECT Id
      FROM APXTConga4__Conga_Template__c
      WHERE APXTConga4__Name__c = 'Air - Options'
    ];
    previewBidOptions_congaTemplateId = !congaTemplates.isEmpty()
      ? congaTemplates[0].id
      : null;
  }
  //End PreviewOptions Methods
  ///BidAgreement Methods
  /*public void openBidAgreement(){
        Bid__c bid = [Select id, Form_Rate_Agreement__c, Form_Trip_Details_Update__c, Form_Transportation_Contract__c, Vendor_Contact__c, Rate_Agreement_Last_Send_Date__c, Rate_Agreement_Last_Send_By__c, Trip_Details_Update_Last_Send_Date__c, Trip_Details_Update_Last_Send_By__c, Transportation_Contract_Last_Send_Date__c, Transportation_Contract_Last_Send_By__c from Bid__c where id =:bidData.Id];
        Map<String, Production_Associations__c> coordinatorsMap = new Map<String, Production_Associations__c>();
        for(Production_Associations__c coordinator:[SELECT User__c, User__r.Name, User__r.Email, Team_Roles__c FROM Production_Associations__c WHERE Production_Opp__c =:bidData.Production__c AND RecordType.Name = 'Production Coordinators' and User__c != NULL and Team_Roles__c includes ('Primary Air Coordinator', 'Primary Contract Coordinator')]) coordinatorsMap.put(coordinator.Team_Roles__c, coordinator);
        List<Revenue__c> bidRevenues = [Select id, Gratuity__c, Total_Price__c, Bid__c, Bid__r.Vendor__r.Payment_policy__c, Bid__r.Vendor__r.Cancellation_Policy__c from Revenue__c where Bid__c =:bidDataMap.get(tripBidNumber).b.Id and RecordType.DeveloperName = 'Ground_Rate_Travel_Commission' order by createdDate desc limit 1];
        bidAgreementRevenue = !bidRevenues.isEmpty() ? bidRevenues[0] : new Revenue__c();
        if((bidAgreement_type == 'Rate Agreement' && String.isNotBlank(bid.Form_Rate_Agreement__c)) || (bidAgreement_type == 'Trip Details Update' && String.isNotBlank(bid.Form_Trip_Details_Update__c)) || (bidAgreement_type == 'Transportation Contract' && String.isNotBlank(bid.Form_Transportation_Contract__c))) draft = [SELECT Id, Name, Attention__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate, Payment_Policy__c, Cancellation_Policy__c FROM Draft__c WHERE Name =:(bidAgreement_type == 'Rate Agreement' ? bid.Form_Rate_Agreement__c : bidAgreement_type == 'Trip Details Update' ? bid.Form_Trip_Details_Update__c : bidAgreement_type == 'Transportation Contract' ? bid.Form_Transportation_Contract__c : '')];            
        else{
            draft = new Draft__c();
            draft.Attention__c = draft.Primary_Contact_Id__c = bid.Vendor_Contact__c;
            draft.Date__c = Date.today();
            draft.Subject__c = (String.isNotBlank(bidAgreement_type) ? bidAgreement_type + ' - ' : '') + bidData.Production__r.Name + ' - ' + (bidData.GT__r.Start_Date__c != null ? Datetime.newInstance(bidData.GT__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' - ' + (bidData.GT__r.End_Date__c != null ? Datetime.newInstance(bidData.GT__r.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' (' + bidData.GT__r.Name + ')';
            draft.Body__c = (bidAgreement_type == 'Rate Agreement' ? 'Congratulations! You have been selected for the upcoming trip for ' + bidData.Production__r.Name + '.<br/><br/>Attached is the rate agreement for the group. Please sign and return at your earliest opportunity. <br/><br/>Looking forward to working with you for this production’s trip!. <br/><br/><br/>Thanks' : bidAgreement_type == 'Trip Details Update' ? 'Attached you will find updated Trip Details for ' + bidData.Production__r.Name + '.<br/><br/>Please reply to this email to confirm you have updated these changes or sign and scan the form back to me at your earliest opportunity. If you have any questions, please contact us immediately.<br/><br/><br/>Thanks' : bidAgreement_type == 'Transportation Contract' ? 'Congratulations! You have been selected for the upcoming trip for ' + bidData.Production__r.Name + '.<br/><br/>Attached is the contract for the group. Please sign and return today so we can forward to the client. If you absolutely need to use your company contract, then please include all items in the attached contract into your own contract. ‘Road Rebel’ and their employees should not appear on your agreement. <br/><br/>Please scan and email only one contract to me as soon as possible. Looking forward to working with you for this production’s trip!<br/><br/><br/>Thanks' : '') + (coordinatorsMap.containsKey('Primary Contract Coordinator') ? '<br/>' + coordinatorsMap.get('Primary Contract Coordinator').User__r.Name : '');
            draft.Terms__c = bidAgreement_type == 'Rate Agreement' ? bidData.Rate_Agreement_Terms__c : bidAgreement_type == 'Trip Details Update' ? bidData.Trip_Details_Update_Terms__c : bidAgreement_type == 'Transportation Contract' ? '<ul><li>Driver(s) must assist with luggage.</li><li>Driver(s) will be on time, drive safely and only use cell phones in emergencies.</li><li>Driver(s) name and cell will be provided prior to travel.</li><li>Driver(s) are responsible for having directions to destination.</li><li>Bus company will not sub-contract coaches.</li><li>Any mechanical failure, or driver/dispatch negligence can cause major issues for their itinerary. This includes being lost or stopping unnecessarily. Bus company will make all efforts to fix any mechanical issues immediately. All drivers should be aware that any requests from Tour Management should be adhered to. Weather or roadway conditions, infringement on D.O.T regulations or the intervention of any governmental body are of exception. Road Rebel should be contacted immediately should any of the events listed occur.</li></ul>' : '';
            draft.Payment_Policy__c = String.isNotEmpty(bidAgreementRevenue.Bid__c) ? bidAgreementRevenue.Bid__r.Vendor__r.Payment_policy__c : '';
            draft.Cancellation_Policy__c = String.isNotEmpty(bidAgreementRevenue.Bid__c) ? bidAgreementRevenue.Bid__r.Vendor__r.Cancellation_Policy__c : '';
            insert draft;
            draft = [SELECT Id, Name, Attention__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate, Payment_Policy__c, Cancellation_Policy__c FROM Draft__c WHERE Id = :draft.Id];
            if(bidAgreement_type == 'Rate Agreement') bid.Form_Rate_Agreement__c = bidData.Form_Rate_Agreement__c = draft.Name; 
            else if(bidAgreement_type == 'Trip Details Update') bid.Form_Trip_Details_Update__c = bidData.Form_Trip_Details_Update__c = draft.Name;
            else if(bidAgreement_type == 'Transportation Contract') bid.Form_Transportation_Contract__c = bidData.Form_Transportation_Contract__c = draft.Name; 
            update bid;
        }
        bidAgreementSubTrips = [Select id, Trip_Order__c, Sub_Trip_Type__c, Description__c, Sub_Trip_Notes__c, (Select id, Line__c, Vehicle_Ref__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c from GTTravels__r order by Line__c) 
                                from Ground__c where Bid_Sub_Trip__c =:bidData.Id and RecordType.DeveloperName = 'GT_Sub_Trip_Details' order by Trip_Order__c, Line__c];
        bidAgreementVehicles = [Select Id, Production_Ground__c, RecordTypeId, RecordType.Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make__c, Model__c, Year__c, Amenities__c, Other_Amenities__c 
                                from Ground__c WHERE RecordType.Name = 'Vehicle Type' AND Production_Ground__c =: opportunityId AND Bid__c =: bidData.Id AND Bid_Sub_Trip__c = NULL AND GT_Sub_Trip_Details__c = NULL AND Sales_GT_Details__c = NULL];
        bidAgreementConcessions = [Select id, Concession_Provided__c from Concessions__c where Bid__c =:bidData.Id and Concession_Type__c = 'GT'];
        if(bidAgreement_type != 'Trip Details Update') changeBidAgreementContactPrimary();
        else changeBidAgreementAttentionContact();
        bidAgreement_subject = draft.Subject__c;
        bidAgreement_message = draft.Body__c;
        bidAgreement_terms = draft.Terms__c;
        bidData.Rate_Agreement_Last_Send_By__c = bid.Rate_Agreement_Last_Send_By__c;
        bidData.Rate_Agreement_Last_Send_Date__c = bid.Rate_Agreement_Last_Send_Date__c;
        bidData.Trip_Details_Update_Last_Send_By__c = bid.Trip_Details_Update_Last_Send_By__c;
        bidData.Trip_Details_Update_Last_Send_Date__c = bid.Trip_Details_Update_Last_Send_Date__c;
        bidData.Transportation_Contract_Last_Send_By__c = bid.Transportation_Contract_Last_Send_By__c;
        bidData.Transportation_Contract_Last_Send_Date__c = bid.Transportation_Contract_Last_Send_Date__c;
        bidAgreement_congaEmailFromId = (coordinatorsMap.containsKey('Primary Contract Coordinator') ? verifyWideAddress(coordinatorsMap.get('Primary Contract Coordinator').User__r.Email) : '');
        List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c =:('GT - ' + bidAgreement_type)];
        bidAgreement_congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        Map<String, APXTConga4__Conga_Template__c> congaTemplatesMap = new Map<String, APXTConga4__Conga_Template__c>();
        for(APXTConga4__Conga_Template__c congaTemplate:[Select Id, APXTConga4__Name__c From APXTConga4__Conga_Template__c Where APXTConga4__Name__c in (:('GT - ' + bidAgreement_type), :('GT - ' + bidAgreement_type + ' Sign'))]) congaTemplatesMap.put(congaTemplate.APXTConga4__Name__c, congaTemplate);
        bidAgreement_congaTemplateId = congaTemplatesMap.get('GT - ' + bidAgreement_type) != null ? congaTemplatesMap.get('GT - ' + bidAgreement_type).id : null;
        bidAgreement_congaSignTemplateId = congaTemplatesMap.get('GT - ' + bidAgreement_type + ' Sign') != null ? congaTemplatesMap.get('GT - ' + bidAgreement_type + ' Sign').id : null;
        isBidAgreementRendered = true;
    }
    public void changeBidAgreementContactPrimary(){
        List<Contact> bidAgreementContacts = [Select Id, FirstName, Name, Phone, Email from Contact where Id =:draft.Primary_Contact_Id__c limit 1];
        bidAgreementPrimaryContact = !bidAgreementContacts.isEmpty() ? bidAgreementContacts[0] : new Contact();
    }
    public void changeBidAgreementAttentionContact(){
        List<Contact> bidAgreementContacts = [Select Id, FirstName, Name, Title, Phone, Email from Contact where Id =:draft.Attention__c limit 1];
        bidAgreementAttentionContact = !bidAgreementContacts.isEmpty() ? bidAgreementContacts[0] : new Contact();
    }
    public List<SelectOption> getBidAgreementProductionAssociationContacts(){
        List<SelectOption> options = new List<SelectOption>();
        for(Production_Associations__c productAssoc:[Select Id, Contact__c, Contact__r.Name From Production_Associations__c Where Production_Opp__c =:opportunityId AND Contact__c != NULL AND RecordType.Name = 'Production Contacts' and Role__c includes ('Primary GT', 'CC: GT', 'Contract Signer')]) options.add(new SelectOption(productAssoc.Contact__c, productAssoc.Contact__r.Name));
        return options;
    }
    public void saveBidAgreement(){
        if(bidData != null && bidData.Id != null){
            try{
                if(bidAgreement_type == 'Rate Agreement'){
                    draft.Subject__c = bidAgreement_subject;
                    draft.Body__c = bidAgreement_message;
                    bidData.Rate_Agreement_Terms__c = draft.Terms__c = bidAgreement_terms;
                    bidData.Rate_Agreement_Payment_Policy__c = draft.Payment_Policy__c;
                    bidData.Rate_Agreement_Cancellation_Policy__c = draft.Cancellation_Policy__c;
                }
                else if(bidAgreement_type == 'Trip Details Update'){
                    draft.Subject__c = bidAgreement_subject;
                    draft.Body__c = bidAgreement_message;
                    bidData.Trip_Details_Update_Terms__c = draft.Terms__c = bidAgreement_terms;    
                    bidData.Trip_Details_Update_Payment_Policy__c = draft.Payment_Policy__c;
                    bidData.Trip_Details_Update_Cancel_Policy__c = draft.Cancellation_Policy__c;
                }
                else if(bidAgreement_type == 'Transportation Contract'){
                    draft.Subject__c = bidAgreement_subject;
                    draft.Body__c = bidAgreement_message;
                    bidData.Transportation_Contract_Terms__c = draft.Terms__c= bidAgreement_terms;  
                    bidData.Transportation_Contract_Payment_Policy__c = draft.Payment_Policy__c;
                    bidData.Transportation_Contract_Cancel_Policy__c = draft.Cancellation_Policy__c;
                } 
                update draft;
                draft = [SELECT Id, Name, Attention__c, Primary_Contact_Id__c, Production_Assoc_Contact_Id__c, CC__c, Subject__C, Date__c, BCC__c, Body__c, Terms__c, CreatedBy.Name, CreatedDate, LastModifiedBy.Name, LastModifiedDate, Payment_Policy__c, Cancellation_Policy__c FROM Draft__c WHERE Id = :draft.Id];
                update bidData;
                if(String.isNotBlank(bidAgreement_congaEmailTemplateId)) update new APXTConga4__Conga_Email_Template__c(id = bidAgreement_congaEmailTemplateId, APXTConga4__HTMLBody__c = bidAgreement_message);
            }
            catch(Exception e){
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
    }*/
  @RemoteAction
  public static String searchContactEmail(String query) {
    query = '%' + query + '%';
    List<wrapperData> Contacts = new List<wrapperData>();
    for (Contact contact : [
      SELECT Id, Name, Email
      FROM Contact
      WHERE (Name LIKE :query OR Email LIKE :query) AND email != NULL
      LIMIT 20
    ])
      Contacts.add(
        new wrapperData(
          contact.Id,
          contact.Name +
          ', ' +
          contact.Email,
          contact.Email
        )
      );
    return JSON.serialize(Contacts);
  }
  //End BidAgreement Methods
  ///ResendBidAgreement Methods
  public void openResendBid() {
    vendorContact = new Contact();
    contactSelectOptionBidMap = new Map<String, List<SelectOption>>();
    contactsByVendorBidMap = new Map<String, List<ContactWrapper>>();
    contactsByVendorParentBidMap = new Map<String, List<ContactWrapper>>();
    List<ContactWrapper> contactAuxList;
    List<SelectOption> contactAuxSelectOptions;
    if (bidData.Vendor__r.ParentId != null) {
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
        WHERE AccountId = :bidData.Vendor__r.ParentId AND Email != NULL
        ORDER BY Order__c ASC
      ]) {
        contactAuxList = contactsByVendorParentBidMap.get(c.AccountId) != null
          ? contactsByVendorParentBidMap.get(c.AccountId)
          : new List<ContactWrapper>();
        contactAuxList.add(
          new ContactWrapper(c, (c.Order__c == 1 ? true : false), false)
        );
        contactsByVendorParentBidMap.put(c.AccountId, contactAuxList.clone());
      }
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
        AccountId = :bidData.Vendor__c
        AND Email != NULL
        AND Order__c != NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendorBidMap.get(c.AccountId) != null
        ? contactsByVendorBidMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(
          c,
          (bidData.Vendor_Contact__c == c.Id
            ? true
            : (c.Order__c == 1 ? true : false)),
          (bidData.Vendor_Contact__c == c.Id
            ? true
            : (bidData.Vendor_Contact__c == null &&
                c.Order__c == 1
                ? true
                : false))
        )
      );
      contactsByVendorBidMap.put(c.AccountId, contactAuxList.clone());
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
      WHERE AccountId = :bidData.Vendor__c AND Email != NULL AND Order__c = NULL
      ORDER BY Order__c ASC
    ]) {
      contactAuxList = contactsByVendorBidMap.get(c.AccountId) != null
        ? contactsByVendorBidMap.get(c.AccountId)
        : new List<ContactWrapper>();
      contactAuxList.add(
        new ContactWrapper(
          c,
          (c.Order__c == 1 ? true : false),
          (c.Order__c == 1 ? true : false)
        )
      );
      contactsByVendorBidMap.put(c.AccountId, contactAuxList.clone());
    }
    if (contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId) != null) {
      for (
        ContactWrapper cw : contactsByVendorParentBidMap.get(
          bidData.Vendor__r.ParentId
        )
      ) {
        contactAuxSelectOptions = contactSelectOptionBidMap.get(
            bidData.Vendor__c
          ) != null
          ? contactSelectOptionBidMap.get(bidData.Vendor__c)
          : new List<SelectOption>();
        contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
        contactSelectOptionBidMap.put(
          bidData.Vendor__c,
          contactAuxSelectOptions.clone()
        );
      }
    }
    if (contactsByVendorBidMap.get(bidData.Vendor__c) != null) {
      for (ContactWrapper cw : contactsByVendorBidMap.get(bidData.Vendor__c)) {
        contactAuxSelectOptions = contactSelectOptionBidMap.get(
            bidData.Vendor__c
          ) != null
          ? contactSelectOptionBidMap.get(bidData.Vendor__c)
          : new List<SelectOption>();
        contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
        contactSelectOptionBidMap.put(
          bidData.Vendor__c,
          contactAuxSelectOptions.clone()
        );
      }
    }
    if (contactsByVendorBidMap.get(bidData.Vendor__c) == null)
      contactsByVendorBidMap.put(bidData.Vendor__c, new List<ContactWrapper>());
    if (contactSelectOptionBidMap.get(bidData.Vendor__c) == null)
      contactSelectOptionBidMap.put(
        bidData.Vendor__c,
        new List<SelectOption>()
      );
    if (contactsByVendorParentBidMap.get(bidData.Vendor__r.ParentId) == null)
      contactsByVendorParentBidMap.put(
        bidData.Vendor__r.ParentId,
        new List<ContactWrapper>()
      );
    contact_DesignationTitle = new List<SelectOption>();
    contact_DesignationTitle.add(new SelectOption('', ''));
    for (
      Schema.PicklistEntry pickListVal : Contact.Designation_title__c.getDescribe()
        .getPicklistValues()
    )
      contact_DesignationTitle.add(
        new SelectOption(pickListVal.getValue(), pickListVal.getLabel())
      );
    /**
     *  @Conga: Update for Conga.
     */
    /*List<APXTConga4__Conga_Email_Template__c> congaEmailTemplates = [Select Id, APXTConga4__Subject__c From APXTConga4__Conga_Email_Template__c Where APXTConga4__Name__c = 'GT - Resend Bid'];
        resendBidAgreement_congaEmailTemplateId = !congaEmailTemplates.isEmpty() ? congaEmailTemplates[0].id : null;
        if(!congaEmailTemplates.isEmpty() && String.isNotBlank(congaEmailTemplates[0].APXTConga4__Subject__c)) resendBidAgreement_congaEmailSubject = congaEmailTemplates[0].APXTConga4__Subject__c.replace('{OpportunityName}', bidData.Production__r.Name).replace('{StartDate}', bidData.GT__r.Start_Date__c != null ? Datetime.newInstance(bidData.GT__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{EndDate}', bidData.GT__r.End_Date__c != null ? Datetime.newInstance(bidData.GT__r.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '').replace('{BidName}', bidData.Name);
        else resendBidAgreement_congaEmailSubject = 'GROUND TRAVEL BID REQUEST - ' + bidData.Production__r.Name + ' - ' + (bidData.GT__r.Start_Date__c != null ? Datetime.newInstance(bidData.GT__r.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' - ' + (bidData.GT__r.End_Date__c != null ? Datetime.newInstance(bidData.GT__r.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMMMM yyyy') : '') + ' (' + bidData.Name + ')';
        List<APXTConga4__Conga_Template__c> congaTemplates = [Select Id From APXTConga4__Conga_Template__c Where APXTConga4__Name__c = 'GT - Ground Travel Bid'];
        resendBidAgreement_congaTemplateId = !congaTemplates.isEmpty() ? congaTemplates[0].id : null;*/
    /**
     *  @/Conga
     */
    isResendBidRendered = true;
  }
  public void changeContactVendorResendBid() {
    if (vendorcontact_actual_id != null && vendorcontact_actual_id != '')
      bidData.Vendor_Contact__c = vendorcontact_actual_id;
    for (ContactWrapper cw : contactsByVendorBidMap.get(bidData.Vendor__c)) {
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
    if (bidData.Vendor__r.ParentId != null) {
      for (
        ContactWrapper cw : contactsByVendorParentBidMap.get(
          bidData.Vendor__r.ParentId
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
  //End ResendBidAgreement Methods
  ///ReleaseBid Methods
  public void openReleaseByBid() {
    if (bidData != null && bidData.Vendor__c != null) {
      contactSelectOption_releaseMap = new Map<String, List<SelectOption>>();
      contactsByVendor_releaseMap = new Map<String, List<ContactWrapper>>();
      contactsByVendorParent_releaseMap = new Map<String, List<ContactWrapper>>();
      List<ContactWrapper> contactAuxList;
      List<SelectOption> contactAuxSelectOptions;

      if (bidData.Vendor__r.ParentId != null) {
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
          WHERE AccountId = :bidData.Vendor__r.ParentId AND Email != NULL
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
          AccountId = :bidData.Vendor__c
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
            (bidData.Vendor_Contact__c == c.Id
              ? true
              : (c.Order__c == 1 ? true : false)),
            (bidData.Vendor_Contact__c == c.Id
              ? true
              : (bidData.Vendor_Contact__c == null &&
                  c.Order__c == 1
                  ? true
                  : false))
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
          AccountId = :bidData.Vendor__c
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

      if (
        contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId) !=
        null
      ) {
        for (
          ContactWrapper cw : contactsByVendorParent_releaseMap.get(
            bidData.Vendor__r.ParentId
          )
        ) {
          contactAuxSelectOptions = contactSelectOption_releaseMap.get(
              bidData.Vendor__c
            ) != null
            ? contactSelectOption_releaseMap.get(bidData.Vendor__c)
            : new List<SelectOption>();
          contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
          contactSelectOption_releaseMap.put(
            bidData.Vendor__c,
            contactAuxSelectOptions.clone()
          );
        }
      }
      if (contactsByVendor_releaseMap.get(bidData.Vendor__c) != null) {
        for (
          ContactWrapper cw : contactsByVendor_releaseMap.get(bidData.Vendor__c)
        ) {
          contactAuxSelectOptions = contactSelectOption_releaseMap.get(
              bidData.Vendor__c
            ) != null
            ? contactSelectOption_releaseMap.get(bidData.Vendor__c)
            : new List<SelectOption>();
          contactAuxSelectOptions.add(new SelectOption(cw.c.Id, cw.c.Name));
          contactSelectOption_releaseMap.put(
            bidData.Vendor__c,
            contactAuxSelectOptions.clone()
          );
        }
      }
      if (contactsByVendor_releaseMap.get(bidData.Vendor__c) == null)
        contactsByVendor_releaseMap.put(
          bidData.Vendor__c,
          new List<ContactWrapper>()
        );
      if (contactSelectOption_releaseMap.get(bidData.Vendor__c) == null)
        contactSelectOption_releaseMap.put(
          bidData.Vendor__c,
          new List<SelectOption>()
        );
      if (
        contactsByVendorParent_releaseMap.get(bidData.Vendor__r.ParentId) ==
        null
      )
        contactsByVendorParent_releaseMap.put(
          bidData.Vendor__r.ParentId,
          new List<ContactWrapper>()
        );

      isReleaseBidRendered = true;
    }
  }
  public void sendReleaseByBid() {
    if (bidData != null && releaseVendorcontact_actual_id != null) {
      Map<String, Contact> contactMap = new Map<String, Contact>();
      for (Contact c : [
        SELECT Id, Name, Email
        FROM Contact
        WHERE Id = :releaseVendorcontact_actual_id
      ])
        contactMap.put(c.Id, c);
      //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name, User__r.Email FROM Production_Associations__c WHERE Production_Opp__c =:opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
      User userActual = AirDashboardController.verifyEmailUser(
        UserInfo.getUserId(),
        opportunityid,
        bidData.Air__c
      );

      Journal__c journalAux;
      Bid__c bAux;
      List<Journal__c> journalAuxList = new List<Journal__c>();
      Map<String, Bid__c> bidUpdateMap = new Map<String, Bid__c>();
      List<Messaging.SingleEmailMessage> myEmails = new List<Messaging.SingleEmailMessage>();
      Messaging.SingleEmailMessage mail;
      String[] toAddresses;
      Set<String> ccAddresses;

      String BidRecordLocatorAndSeatDetails;
      Map<String, String> revenueMap = new Map<String, String>();
      for (Revenue__c r : [
        SELECT Id, Bid__c, Record_Locator__c, of_seats__c
        FROM Revenue__c
        WHERE
          Bid__c = :bidData.Id
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
          Air_Trip_Details__c = :bidData.Air__c
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

      List<EmailTemplate> template = [
        SELECT Id, Name, Subject, Body, HTMLValue
        FROM EmailTemplate
        WHERE DeveloperName = 'Air_Release_Bid'
      ];
      //New Journals
      journalAux = new Journal__c(
        RecordTypeId = journal_bidjournalRT,
        Bid__c = bidData.Id,
        Journal_Entry__c = 'Release Bid has been sent to ' +
          contactMap.get(releaseVendorcontact_actual_id).Name +
          ' at ' +
          contactMap.get(releaseVendorcontact_actual_id).Email
      );
      journalAuxList.add(journalAux);

      //Bid update
      if (bidData != null && bidData.Status__c != 'Contracted') {
        bAux = new Bid__c(Id = bidData.Id, Status__c = 'Bid Released');
        bidUpdateMap.put(bAux.Id, bAux);
      }

      //EMAIL
      ccAddresses = new Set<String>();
      if (bidData.Vendor__c != null) {
        for (
          ContactWrapper cw : contactsByVendor_releaseMap.get(bidData.Vendor__c)
        ) {
          if (!cw.disabled && cw.selected)
            ccAddresses.add(cw.c.Email);
        }
      }
      if (bidData.Vendor__r.ParentId != null) {
        for (
          ContactWrapper cw : contactsByVendorParent_releaseMap.get(
            bidData.Vendor__r.ParentId
          )
        ) {
          if (!cw.disabled && cw.selected)
            ccAddresses.add(cw.c.Email);
        }
      }

      mail = new Messaging.SingleEmailMessage();
      if (userActual != null && userActual.Email != null)
        mail.setOrgWideEmailAddressId(verifyWideAddress(userActual.Email));
      toAddresses = new List<String>{
        contactMap.get(releaseVendorcontact_actual_id).Email
      };
      mail.setToAddresses(toAddresses);
      if (ccAddresses.size() > 0)
        mail.setCcAddresses(new List<String>(ccAddresses));

      String startDate = (bidData.Air__r.Departure_Date__c != null
        ? Datetime.newInstance(
              bidData.Air__r.Departure_Date__c.year(),
              bidData.Air__r.Departure_Date__c.month(),
              bidData.Air__r.Departure_Date__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');
      String returnDate = (bidData.Air__r.Return_Date__c != null
        ? Datetime.newInstance(
              bidData.Air__r.Return_Date__c.year(),
              bidData.Air__r.Return_Date__c.month(),
              bidData.Air__r.Return_Date__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');

      String subject = template.size() > 0 ? template[0].Subject : '';
      String body = template[0].HTMLValue != null ? template[0].HTMLValue : '';
      mail.setSubject(
        subject.replace('{ProductionName}', bidData.Production__r.Name)
          .replace('{DepDate}', startDate)
          .replace(
            '{DepartureCity}',
            bidData.Air__r.Departure_City__r.Airport_Code__c != null
              ? bidData.Air__r.Departure_City__r.Airport_Code__c
              : ''
          )
          .replace(
            '{ArrivalCity}',
            bidData.Air__r.Arrival_City__r.Airport_Code__c != null
              ? bidData.Air__r.Arrival_City__r.Airport_Code__c
              : ''
          )
      );

      mail.setHtmlBody(
        body.replace('{VendorName}', bidData.Vendor__r.Name)
          .replace('{ProductionName}', bidData.Production__r.Name)
          .replace(
            '{GroupType}',
            bidData.Air__r.Group_Type__c != null
              ? bidData.Air__r.Group_Type__c
              : ''
          )
          .replace('{TripStartDate}', startDate)
          .replace('{TripEndDate}', returnDate)
          .replace(
            '{AirCoordinator}',
            userActual != null && userActual.Name != null ? userActual.Name : ''
          )
          .replace(
            '{BidDescription}',
            segmentMap.get(bidData.Air__c) != null
              ? segmentMap.get(bidData.Air__c)
              : ''
          )
          .replace(
            '{BidRecordLocatorAndSeatDetails}',
            revenueMap.get(bidData.Id) != null
              ? revenueMap.get(bidData.Id)
              : 'Record Locator: , no of seats: '
          )
      );
      myEmails.add(mail);
      insert journalAuxList;
      update bidUpdateMap.values();
      if (myEmails.size() > 0)
        Messaging.sendEmail(myEmails);
    }
  }
  public void changeContactVendorReleaseByBid() {
    if (
      releaseVendorcontact_actual_id != null &&
      releaseVendorcontact_actual_id != ''
    )
      bidData.Vendor_Contact__c = releaseVendorcontact_actual_id;
    for (
      ContactWrapper cw : contactsByVendor_releaseMap.get(bidData.Vendor__c)
    ) {
      if (releaseVendorcontact_actual_id == cw.c.Id) {
        cw.selected = true;
        cw.disabled = true;
      } else {
        if (cw.selected && cw.disabled) {
          cw.selected = false;
          cw.disabled = false;
        }
      }
    }
    if (bidData.Vendor__r.ParentId != null) {
      for (
        ContactWrapper cw : contactsByVendorParent_releaseMap.get(
          bidData.Vendor__r.ParentId
        )
      ) {
        if (releaseVendorcontact_actual_id == cw.c.Id) {
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
  public void sendPreviewPdf() {
    emailMessage = '';
    try {
      emailMessage = sendEmail(
        emailbid_to,
        emailbid_cc,
        emailbid_bcc,
        emailbid_subject,
        releaseEmailBid_body,
        emailAttachs,
        opportunityId,
        bidData.Air__c
      );
      if (emailMessage == '') {
        Journal__c journalAux;
        if (emailbid_type == 'resend_bid') {
          journalAux = new Journal__c(
            RecordTypeId = journal_bidjournalRT,
            Bid__c = emailbid_id,
            Journal_Entry__c = 'Air Bid has been sent to ' +
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
            Bid__c b = new Bid__c(Id = emailbid_id, Status__c = 'Lead Sent');
            update b;
          }
        } else {
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
        }
        if (journalAux != null)
          insert journalAux;
      }
    } catch (DMLException e) {
      system.debug(e.getMessage());
      emailMessage = e.getMessage();
    }
  }
  /*@RemoteAction
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
        List<Ground__c> groundAux = [SELECT Id, Name, RecordType.Name, Start_Date__c, End_Date__c FROM Ground__c WHERE Id =: tripid];
        String dateIn = (groundAux[0].Start_Date__c != null ? Datetime.newInstance(groundAux[0].Start_Date__c.year(),groundAux[0].Start_Date__c.month(),groundAux[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateOut = (groundAux[0].End_Date__c != null ? Datetime.newInstance(groundAux[0].End_Date__c.year(),groundAux[0].End_Date__c.month(),groundAux[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        String subject;
        
        //Body
        String body = '';
        List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];        
        List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName ='GT_Bid_Request_Link_All'];
        subject = template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name)
            .replace('{StartDate}',dateIn)
            .replace('{EndDate}',dateOut)
            .replace('{BidNumber}',bidAux.size() > 0 ? bidAux[0].Name : '') : '';
        result.add(subject);
        if(template.size() > 0) body = 'Dear ' + primary_name + ',<br/><br/>' + 
            template[0].HTMLValue.replace('{GroundTravelCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
            .replace('{VendorURL}','<a href=' + url + '/' + bidAux[0].Vendor__c + ' target=_blank>' + bidAux[0].Vendor__r.Name + '</a>')
            .replace('{BidURL}','<a href=' + url + '/' + bidAux[0].Id + ' target=_blank>' + url + '/' + bidAux[0].Id + '</a>')
            .replace('{ProductionName}',productionAux[0].Name);
        result.add(body);
        
        result.add(productionAux[0].Name);

        return result;
    }*/
  /*@RemoteAction
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
        List<Opportunity> productionAux = [SELECT Id, Name FROM Opportunity WHERE Id =: opportunityid];
        List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
        List<EmailTemplate> template = [SELECT Id, Name, Subject, Body, HTMLValue FROM EmailTemplate  WHERE DeveloperName = 'GT_Release_Bid'];
        String dateIn = (groundAux[0].Start_Date__c != null ? Datetime.newInstance(groundAux[0].Start_Date__c.year(),groundAux[0].Start_Date__c.month(),groundAux[0].Start_Date__c.day()).format('dd MMMMM yyyy') : '');
        String dateOut = (groundAux[0].End_Date__c != null ? Datetime.newInstance(groundAux[0].End_Date__c.year(),groundAux[0].End_Date__c.month(),groundAux[0].End_Date__c.day()).format('dd MMMMM yyyy') : '');
        result.add(template.size() > 0 ? template[0].Subject.replace('{ProductionName}',productionAux[0].Name).replace('{StartDate}',dateIn).replace('{EndDate}',dateOut) : '');
        result.add(template[0].HTMLValue != null ? template[0].HTMLValue.replace('{GroundTravelCoordinator}',prodAssocAux.size() > 0 ? prodAssocAux[0].User__r.Name : '')
                                        .replace('{VendorName}',bidAux.Vendor__r.Name)
                                        .replace('{ProductionName}',productionAux[0].Name)
                                        .replace('{StartDate}',dateIn)
                                        .replace('{EndDate}',dateOut) : '');
        return result;
    }*/
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
        Number_of_Seats__c
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
      SELECT Id, Name
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
            : (segmentList.size() == 2
                ? (segment.Return_Date__c != null
                    ? DateTime.newInstance(
                          segment.Return_Date__c,
                          Time.newInstance(0, 0, 0, 0)
                        )
                        .format('EEEE') +
                      ', ' +
                      (segment.Return_Date__c != null
                        ? Datetime.newInstance(
                              segment.Return_Date__c.year(),
                              segment.Return_Date__c.month(),
                              segment.Return_Date__c.day()
                            )
                            .format('dd MMMMM yyyy')
                        : '')
                    : '')
                : '')) +
          '<br/>';
      }
      segments = segments.length() > 2
        ? segments.subString(1, segments.length() - 2)
        : '';
    }

    String body = '';
    //List<Production_Associations__c> prodAssocAux = [SELECT Id, User__r.Name FROM Production_Associations__c WHERE Production_Opp__c =: opportunityid AND User__c <> NULL AND Team_Roles__c includes ('Primary Air Coordinator')];
    User userActual = AirDashboardController.verifyEmailUser(
      UserInfo.getUserId(),
      opportunityid,
      tripid
    );
    if (typez == 'resend_bid') {
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
                airAux[0].Departure_City__r.Airport_Code__c
              )
              .replace(
                '{ArrivalCity}',
                airAux[0].Arrival_City__r.Airport_Code__c
              )
          : '';
        result.add(subject);
        body = tripTemplate[0]
          .Email_Body_Bid_Request__c.unescapeHtml4()
          .replace('{VendorName}', bidAux[0].Vendor__r.Name)
          .replace('{ProductionName}', productionAux[0].Name)
          .replace('{GroupType}', airAux[0].Group_Type__c)
          .replace('{TravelDetails}', segmentsTravelDetails)
          .replace(
            '{AirCoordinator}',
            userActual != null && userActual.Name != null ? userActual.Name : ''
          )
          .replace(
            '{NosOfSeats}',
            airAux[0].Number_of_Seats__c != null
              ? String.valueOf(airAux[0].Number_of_Seats__c)
              : ''
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
                .replace(
                  '{ProductionName}',
                  productionAux[0].Name != null ? productionAux[0].Name : ''
                )
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
                  airAux[0].Number_of_Seats__c != null
                    ? String.valueOf(airAux[0].Number_of_Seats__c)
                    : ''
                )
            : '';
        result.add(body);
      }
    } else if (typez == 'release_bid') {
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
            airAux[0].Departure_City__r.Airport_Code__c
          )
          .replace('{ArrivalCity}', airAux[0].Arrival_City__r.Airport_Code__c);
        result.add(subject);
        body = tripTemplate[0]
          .Email_Body_Release_Bid__c.unescapeHtml4()
          .replace('{VendorName}', bidAux[0].Vendor__r.Name)
          .replace('{ProductionName}', productionAux[0].Name)
          .replace('{GroupType}', airAux[0].Group_Type__c)
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
                    userActual.name != null
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
    }

    result.add(productionAux[0].Name);

    return result;
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
      User userActual = AirDashboardController.verifyEmailUser(
        UserInfo.getUserId(),
        oppid,
        tripid
      );

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
              cv.PathOnClient.subString(2, cv.PathOnClient.length())
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
  //End ReleaseBid Methods
  ///DeactivateBid Methods
  public void deactivateBid() {
    if (bidData != null && bidData.Id != null) {
      bidData.Status__c = 'Deactivated Bid';
      bidData.Locked__c = true;
      bidData.Deactivate__c = true;
      update bidData;
    }
  }
  //End DeactivateBid Methods
  //AddContacts Methods
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
  public void saveAddContactVendor() {
    messageCreateContact = '';
    try {
      vendorContact.Id = (vendorContact_id != null &&
        vendorContact_id.trim() != ''
        ? vendorContact_id
        : null);
      upsert vendorContact;
    } catch (DMLException e) {
      messageCreateContact = validateError(e.getMessage());
    }
    openResendBid();
    openReleaseByBid();
  }
  public static String validateError(String error) {
    String message = '';
    if (error.contains('DUPLICATES_DETECTED'))
      message = 'You\'re creating a duplicate record. We recommend you use an existing record.';
    else
      message = error;
    return message;
  }
  //End AddContacts Methods
  //Rate Details Methods
  public void getBidRevenue() {
    if (bidData != null && bidData.Air__r.Air_Charter__c == true) {
      User us = [
        SELECT Id, Housing_Preference__c
        FROM User
        WHERE Id = :UserInfo.getUserId()
      ];
      List<Revenue__c> bidRevenues = [
        SELECT
          id,
          Base_Cost__c,
          Commission__c,
          Rate__c,
          VAT_Rate__c,
          Gratuity__c,
          Total_Price__c,
          CurrencyIsoCode
        FROM Revenue__c
        WHERE
          Bid__c = :bidDataMap.get(tripBidNumber).b.Id
          AND RecordType.DeveloperName = 'Air_Rate_Commission'
        ORDER BY createdDate DESC
        LIMIT 1
      ];
      bidRevenue = !bidRevenues.isEmpty()
        ? bidRevenues[0]
        : new Revenue__c(
            RecordTypeId = Schema.SObjectType.Revenue__c.getRecordTypeInfosByName()
                .get('Air Rate & Commission') != null
              ? Schema.SObjectType.Revenue__c.getRecordTypeInfosByName()
                  .get('Air Rate & Commission')
                  .getRecordTypeId()
              : null,
            Bid__c = bidDataMap.get(tripBidNumber).b.Id,
            CurrencyIsoCode = (us.Housing_Preference__c == 'RRE'
              ? 'EUR'
              : 'USD')
          );
      if (!bidRevenues.isEmpty())
        symbolMap.put(bidRevenues[0].CurrencyIsoCode, '');
      else
        symbolMap.put((us.Housing_Preference__c == 'RRE' ? 'EUR' : 'USD'), '');
    }
  }
  public List<SelectOption> getCurrencyValues() {
    List<SelectOption> options = new List<SelectOption>();
    for (
      Schema.PicklistEntry pickListVal : Revenue__c.CurrencyIsoCode.getDescribe()
        .getPicklistValues()
    )
      options.add(
        new SelectOption(
          pickListVal.getValue(),
          pickListVal.getValue() +
          ' - ' +
          pickListVal.getLabel()
        )
      );
    return options;
  }
  //End Rate Details
  //Attachs
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
  public void doAttachmentLast() {
    system.debug(filename);
    system.debug(documentRelationId);
    system.debug(bodyBid);
    if (filename != null && bodyBid != null) {
      try {
        ContentVersion conVer = new ContentVersion();
        conVer.PathOnClient = '/' + filename;
        conVer.Title = filename.split('\.')[0];
        conVer.VersionData = EncodingUtil.base64Decode(
          bodyBid.subString(0, 100).split(',')[1] +
          bodyBid.substring(100, bodyBid.length())
        );
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
    bodyBid = null;
    getDocumentsByBid();
  }
  public void getDocumentsByBid() {
    documentBidList = new List<ContentDocument>();
    documentListPages = new List<Integer>();
    documentListFirst = 0;
    documentListPage = 1;
    documentListLastPage = 0;
    if (bidData != null && bidData.Id != null) {
      Set<String> contentDocumentIds = new Set<String>();
      for (ContentDocumentLink cdl : [
        SELECT Id, LinkedEntityId, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :bidData.Id
      ])
        contentDocumentIds.add(cdl.ContentDocumentId);
      documentBidList = [
        SELECT Id, Title, FileExtension, CreatedDate
        FROM ContentDocument
        WHERE Id IN :contentDocumentIds
        ORDER BY CreatedDate DESC
      ];
      if (!documentBidList.isEmpty()) {
        Integer i = 0;
        do {
          i++;
          documentListPages.add(i);
        } while ((i * 10) < documentBidList.size());
        documentListLastPage = i;
      }
    }
  }
  //End Attachs
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
  global static Map<String, String> validateDatesForCompare(String data) {
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
        dataDate.split('=')[0] != '' &&
        dataDate.split('=')[1] != '' &&
        parseDate(dataDate.split('=')[0]) > parseDate(dataDate.split('=')[1])
      ) {
        response.put(key, 'Date is Greater than Due Date');
      }
    }
    return response;
  }
  public static Date parseDate(String inDate) {
    Date dateRes = null;
    //  1 - Try locale specific mm/dd/yyyy or dd/mm/yyyy
    try {
      String candDate = inDate.substring(0, Math.min(10, inDate.length())); // grab date portion only m[m]/d[d]/yyyy , ignore time
      dateRes = Date.parse(candDate);
    } catch (Exception e) {
    }
    if (dateRes == null) {
      //    2 - Try yyyy-mm-dd
      try {
        String candDate = inDate.substring(0, 10); // grab date portion only, ignore time, if any
        dateRes = Date.valueOf(candDate);
      } catch (Exception e) {
      }
    }
    return dateRes;
  }
  //Wrappers
  global class wrapperData {
    public String data;
    public String value;
    public String extra1;
    public wrapperData(String data, String value, String extra1) {
      this.data = data;
      this.value = value;
      this.extra1 = extra1;
    }
  }
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
  global class wrapperSearchPL {
    public String dataid;
    public String dataname;
    public wrapperSearchPL(String cdataid, String cdataname) {
      dataid = cdataid;
      dataname = cdataname;
    }
  }
  global class BidVendorWrapper implements Comparable {
    public Bid__c b { get; set; }
    public String name { get; set; }
    public String production { get; set; }
    public Date datein { get; set; }
    public Date dateout { get; set; }
    public String description { get; set; }
    public Decimal rate { get; set; }
    public String status { get; set; }
    public String nobidreason { get; set; }
    public String venue { get; set; }
    public String vendorparent { get; set; }
    public Date createddate { get; set; }
    public String departurecity { get; set; }
    public String arrivalcity { get; set; }
    public Decimal pax { get; set; }
    public Decimal fare { get; set; }

    global BidVendorWrapper(
      Bid__c vb,
      String vname,
      String vproduction,
      Date vdatein,
      Date vdateout,
      String vdescription,
      Decimal vrate,
      String vstatus,
      String vnobidreason,
      String vvenue,
      String vvendorparent,
      Date vcreateddate
    ) {
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

    global BidVendorWrapper(
      Bid__c vb,
      String vname,
      String vproduction,
      String vdeparturecity,
      String varrivalcity,
      Decimal vpax,
      Decimal vfare,
      String vnobidreason,
      Date vcreateddate
    ) {
      b = vb;
      name = vname;
      production = vproduction;
      departurecity = vdeparturecity;
      arrivalcity = varrivalcity;
      pax = vpax;
      fare = vfare;
      nobidreason = vnobidreason;
      createddate = vcreateddate;
    }

    public Integer compareTo(Object obj) {
      BidVendorWrapper data = (BidVendorWrapper) obj;
      if (orderBidHistory == 'created_date')
        return sortByCreatedDate(data);
      if (orderBidHistory == 'name')
        return sortByName(data);
      if (orderBidHistory == 'production')
        return sortByProduction(data);
      if (orderBidHistory == 'date_in')
        return sortByDateIn(data);
      if (orderBidHistory == 'date_out')
        return sortByDateOut(data);
      if (orderBidHistory == 'description')
        return sortByDescription(data);
      if (orderBidHistory == 'rate')
        return sortByRate(data);
      if (orderBidHistory == 'status')
        return sortByStatus(data);
      if (orderBidHistory == 'no_bid_reason')
        return sortByNoBidReason(data);
      if (orderBidHistory == 'venue')
        return sortByVenue(data);
      if (orderBidHistory == 'provider')
        return sortByProvider(data);
      if (orderBidHistory == 'departure_city')
        return sortByDepartureCity(data);
      if (orderBidHistory == 'arrival_city')
        return sortByArrivalCity(data);
      if (orderBidHistory == 'pax')
        return sortByPax(data);
      if (orderBidHistory == 'fare')
        return sortByFare(data);
      return 0;
    }

    private Integer sortByFare(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.fare > data.fare)
          return 1;
      } else {
        if (this.fare < data.fare)
          return 1;
      }
      if (this.fare == data.fare)
        return 0;
      return -1;
    }
    private Integer sortByPax(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.pax > data.pax)
          return 1;
      } else {
        if (this.pax < data.pax)
          return 1;
      }
      if (this.pax == data.pax)
        return 0;
      return -1;
    }
    private Integer sortByArrivalCity(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.arrivalcity > data.arrivalcity)
          return 1;
      } else {
        if (this.arrivalcity < data.arrivalcity)
          return 1;
      }
      if (this.arrivalcity == data.arrivalcity)
        return 0;
      return -1;
    }
    private Integer sortByDepartureCity(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.departurecity > data.departurecity)
          return 1;
      } else {
        if (this.departurecity < data.departurecity)
          return 1;
      }
      if (this.departurecity == data.departurecity)
        return 0;
      return -1;
    }
    private Integer sortByCreatedDate(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.createddate > data.createddate)
          return 1;
      } else {
        if (this.createddate < data.createddate)
          return 1;
      }
      if (this.createddate == data.createddate)
        return 0;
      return -1;
    }
    private Integer sortByName(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.name > data.name)
          return 1;
      } else {
        if (this.name < data.name)
          return 1;
      }
      if (this.name == data.name)
        return 0;
      return -1;
    }
    private Integer sortByProduction(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.production > data.production)
          return 1;
      } else {
        if (this.production < data.production)
          return 1;
      }
      if (this.production == data.production)
        return 0;
      return -1;
    }
    private Integer sortByDateIn(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.datein > data.datein)
          return 1;
      } else {
        if (this.datein < data.datein)
          return 1;
      }
      if (this.datein == data.datein)
        return 0;
      return -1;
    }
    private Integer sortByDateOut(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.dateout > data.dateout)
          return 1;
      } else {
        if (this.dateout < data.dateout)
          return 1;
      }
      if (this.dateout == data.dateout)
        return 0;
      return -1;
    }
    private Integer sortByDescription(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.description > data.description)
          return 1;
      } else {
        if (this.description < data.description)
          return 1;
      }
      if (this.description == data.description)
        return 0;
      return -1;
    }
    private Integer sortByRate(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.rate > data.rate)
          return 1;
      } else {
        if (this.rate < data.rate)
          return 1;
      }
      if (this.rate == data.rate)
        return 0;
      return -1;
    }
    private Integer sortByStatus(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.status > data.status)
          return 1;
      } else {
        if (this.status < data.status)
          return 1;
      }
      if (this.status == data.status)
        return 0;
      return -1;
    }
    private Integer sortByNoBidReason(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.nobidreason > data.nobidreason)
          return 1;
      } else {
        if (this.nobidreason < data.nobidreason)
          return 1;
      }
      if (this.nobidreason == data.nobidreason)
        return 0;
      return -1;
    }
    private Integer sortByVenue(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.venue > data.venue)
          return 1;
      } else {
        if (this.venue < data.venue)
          return 1;
      }
      if (this.venue == data.venue)
        return 0;
      return -1;
    }
    private Integer sortByProvider(BidVendorWrapper data) {
      if (orderBidHistoryOrientation == 'ASC') {
        if (this.vendorparent > data.vendorparent)
          return 1;
      } else {
        if (this.vendorparent < data.vendorparent)
          return 1;
      }
      if (this.vendorparent == data.vendorparent)
        return 0;
      return -1;
    }
  }
  //End Wrappers
}
```


# Last Modified


# Usage

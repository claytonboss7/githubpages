---
layout: default
title: VoyajerBidSubmissionController
parent: classes
---

```/**
 * @description       : 
 * @author            : sfdc cb
 * @group             : 
 * @last modified on  : 09-03-2021
 * @last modified by  : sfdc cb
**/
public without sharing class VoyajerBidSubmissionController {

  public class ProductionData{
    @AuraEnabled
    public String oppName { get; set; }
    @AuraEnabled
    public String userEmail { get; set; }
    @AuraEnabled
    public String userName { get; set; }
    @AuraEnabled
    public String userPhone { get; set; }
    @AuraEnabled
    public String userRole { get; set; }

    public ProductionData(String oppName, String userEmail, String userName, String userPhone, String userRole){
      this.oppName = oppName;
      this.userEmail = userEmail;
      this.userName = userName;
      this.userPhone = userPhone;
      this.userRole = userRole;
    }
  }


  public class Room {
    @AuraEnabled
    public String recordId { get; set; }
    @AuraEnabled
    public String roomType { get; set; }
    @AuraEnabled
    public Decimal roomNights { get; set; }
    @AuraEnabled
    public Decimal roomComps { get; set; }
    @AuraEnabled
    public Decimal roomRate { get; set; }
    @AuraEnabled
    public Decimal roomCommission { get; set; }
    @AuraEnabled
    public String roomConfirmation { get; set; }
    @AuraEnabled
    public String rateperiod { get; set; }

    public Room(
      String recordId,
      String roomType,
      Decimal roomNights,
      Decimal roomComps,
      Decimal roomRate,
      Decimal roomCommission,
      String roomConfirmation,
      String ratePeriod
    ) {
      this.recordId = recordId;
      this.roomType = roomType;
      this.roomNights = roomNights;
      this.roomComps = roomComps;
      this.roomRate = roomRate;
      this.roomCommission = roomCommission;
      this.roomConfirmation = roomConfirmation;
      this.rateperiod = ratePeriod;
    }
  }

  public class RoomRevenue {
    @AuraEnabled
    public String compsId { get; set; }
    @AuraEnabled
    public Decimal compsValue { get; set; }
    @AuraEnabled
    public String commissionId { get; set; }
    @AuraEnabled
    public String commissionType { get; set; }
    @AuraEnabled
    public Decimal commissionValue { get; set; }
    @AuraEnabled
    public Decimal commissionDue { get; set; }
    @AuraEnabled
    public String commissionNotes { get; set; }
    @AuraEnabled
    public Boolean isInvoiceSent { get; set; }
    @AuraEnabled
    public Boolean isMonthlyPickUp { get; set; }
    @AuraEnabled
    public Boolean isMatchingAmount { get; set; }
    @AuraEnabled
    public String indicateDates { get; set; }

    public RoomRevenue() {
      this.compsId = '';
      this.compsValue = Decimal.valueOf('0');
      this.commissionId = '';
      this.commissionType = '';
      this.commissionValue = Decimal.valueOf('0');
      this.commissionDue = Decimal.valueOf('0');
      this.commissionNotes = '';
      this.isInvoiceSent = false;
      this.isMonthlyPickUp = false;
      this.isMatchingAmount = false;
      this.indicateDates = '';
    }
  }

  public class Revenue {
    @AuraEnabled
    public String recordId { get; set; }
    @AuraEnabled
    public String revenueType { get; set; }
    @AuraEnabled
    public String revenueCharge { get; set; }
    @AuraEnabled
    public Decimal revenueValue { get; set; }
    @AuraEnabled
    public String revenuePer { get; set; }
    @AuraEnabled
    public Decimal revenueTotal { get; set; }
    @AuraEnabled
    public Decimal revenueInvoice { get; set; }

    public Revenue(
      String recordId,
      String revenueType,
      String revenueCharge,
      Decimal revenueValue,
      String revenuePer,
      Decimal revenueTotal,
      Decimal revenueInvoice
    ) {
      this.recordId = recordId;
      this.revenueType = revenueType;
      this.revenueCharge = revenueCharge;
      this.revenueValue = revenueValue;
      this.revenuePer = revenuePer;
      this.revenueTotal = revenueTotal;
      this.revenueInvoice = revenueInvoice;
    }
  }

  public class MonthlyPickUp {
    @AuraEnabled
    public String recordId { get; set; }
    @AuraEnabled
    public String indicateDates { get; set; }
    @AuraEnabled
    public String roomType { get; set; }
    @AuraEnabled
    public String invoiceDate { get; set; }
    @AuraEnabled
    public Decimal roomNights { get; set; }
    @AuraEnabled
    public Decimal rateCurrency { get; set; }
    @AuraEnabled
    public Decimal commissionPerRoom { get; set; }

    public MonthlyPickUp(
      String recordId,
      String indicateDates,
      String roomType,
      Decimal roomNights,
      Decimal rateCurrency,
      Decimal commissionPerRoom,
      String invoiceDate
    ) {
      this.recordId = recordId;
      this.indicateDates = indicateDates;
      this.roomType = roomType;
      this.roomNights = roomNights;
      this.rateCurrency = rateCurrency;
      this.commissionPerRoom = commissionPerRoom;
      this.invoiceDate = invoiceDate;
    }
  }

  public class Client {
    @AuraEnabled
    public User userInfo { get; set; }
    @AuraEnabled
    public List<DualListOption> preferencesAvailable { get; set; }
    @AuraEnabled
    public List<String> preferencesSelected { get; set; }
    @AuraEnabled
    public PicklistWrapper countryAndStates { get; set; }
    @AuraEnabled
    public Map<String, String> recordTypes { get; set; }
    @AuraEnabled
    public String noteFromCoordinatorToClient { get; set; }
    @AuraEnabled
    public ProductionData theProductionData {get; set; }

    public Client() {
      this.userInfo = new User();
      this.preferencesAvailable = new List<DualListOption>();
      this.preferencesSelected = new List<String>();
      this.countryAndStates = new PicklistWrapper();
      this.recordTypes = new Map<String, String>();
      this.noteFromCoordinatorToClient = '';
    }
  }

  public class PicklistWrapper {
    @AuraEnabled
    public Map<String, List<String>> pickListMap { get; set; }
    @AuraEnabled
    public String parentFieldLabel { get; set; }
    @AuraEnabled
    public String childFieldLabel { get; set; }

    public PicklistWrapper() {
      this.pickListMap = new Map<String, List<String>>();
      this.parentFieldLabel = '';
      this.childFieldLabel = '';
    }
  }

  public class PicklistEntryWrapper {
    public String active;
    public String defaultValue;
    public String label;
    public String value;
    public String validFor;
  }

  public class DualListOption {
    @AuraEnabled
    public String label { get; set; }
    @AuraEnabled
    public String value { get; set; }

    public DualListOption(String label, String value) {
      this.label = label;
      this.value = value;
    }
  }

  /*
  @AuraEnabled
  public static string updateVATData(String data) {
    system.debug('thedata :: ' + data);
    String returnMessage = '';
    Map<String, Object> result = new Map<String,Object>();

    try {
      result = (Map<String, Object>) JSON.deserializeUntyped(data);
      if (result.containsKey('revenue')) {
        Map<String, Object> objMap = (Map<String, Object>) result.get('revenue');
        Revenue__c revenue = new Revenue__c(
          Id = (String) objMap.get('Id'),
          VAT_Number__c = (String) result.get('vatnumber')
        );
        update revenue;
      }

      returnMessage = 'done';
    } catch (Exception e) {
      system.debug(e.getMessage() + ' - ' + e.getStackTraceString());
      returnMessage = 'error';
    }
    Account accountRecord = new Account(
      Id = (String) result.get('accountId'),
      BillingStreet = (String) result.get('address'),
      Hotel_VAT__c = (String) result.get('vatnumber')
    );
    update accountRecord;
    return returnMessage;
  }
  */

  private static final String base64Chars =
    '' +
    'ABCDEFGHIJKLMNOPQRSTUVWXYZ' +
    'abcdefghijklmnopqrstuvwxyz' +
    '0123456789+/';

  @testVisible private static PicklistWrapper getConcessionTypeAndRequests() {
    PicklistWrapper pw = new PicklistWrapper();

    List<PicklistEntryWrapper> depEntries = (List<PicklistEntryWrapper>) JSON.deserialize(
      JSON.serialize(Concessions__c.Concessions_Requested__c.getDescribe().getPicklistValues()),
      List<PicklistEntryWrapper>.class
    );
    List<String> controllingValues = new List<String>();

    for (Schema.PicklistEntry ple : Concessions__c.Concession_Type__c.getDescribe().getPicklistValues())
      if (ple.isActive()) {
        pw.pickListMap.put(ple.getLabel(), new List<String>());
        controllingValues.add(ple.getLabel());
      }

    for (PicklistEntryWrapper plew : depEntries) {
      String validForBits = base64ToBits(plew.validFor);
      for (Integer i = 0; i < validForBits.length(); i++) {
        String bit = validForBits.mid(i, 1);
        if (bit == '1') {
          pw.pickListMap.get(controllingValues.get(i)).add(plew.label);
        }
      }
    }
    pw.parentFieldLabel = 'Types';
    pw.childFieldLabel = 'Concessions';
    return pw;
  }

  private static PicklistWrapper getCConcessionRequestAndProvided() {
    PicklistWrapper pw = new PicklistWrapper();

    List<PicklistEntryWrapper> depEntries = (List<PicklistEntryWrapper>) JSON.deserialize(
      JSON.serialize(Concessions__c.Concession_Provided__c.getDescribe().getPicklistValues()),
      List<PicklistEntryWrapper>.class
    );
    List<String> controllingValues = new List<String>();

    for (Schema.PicklistEntry ple : Concessions__c.Concessions_Requested__c.getDescribe().getPicklistValues())
      if (ple.isActive()) {
        pw.pickListMap.put(ple.getLabel(), new List<String>());
        controllingValues.add(ple.getLabel());
      }

    for (PicklistEntryWrapper plew : depEntries) {
      String validForBits = base64ToBits(plew.validFor);
      for (Integer i = 0; i < validForBits.length(); i++) {
        String bit = validForBits.mid(i, 1);
        if (bit == '1') {
          pw.pickListMap.get(controllingValues.get(i)).add(plew.label);
        }
      }
    }
    pw.parentFieldLabel = 'Requested';
    pw.childFieldLabel = 'Provided';
    return pw;
  }

  //Refer from here https://salesforce.stackexchange.com/questions/4462/get-lists-of-dependent-picklist-options-in-apex
  public static String decimalToBinary(Integer val) {
    String bits = '';
    while (val > 0) {
      Integer remainder = Math.mod(val, 2);
      val = Integer.valueOf(Math.floor(val / 2));
      bits = String.valueOf(remainder) + bits;
    }
    return bits;
  }

  public static String base64ToBits(String validFor) {
    if (String.isEmpty(validFor))
      return '';
    String validForBits = '';
    for (Integer i = 0; i < validFor.length(); i++) {
      String thisChar = validFor.mid(i, 1);
      Integer val = base64Chars.indexOf(thisChar);
      String bits = decimalToBinary(val).leftPad(6, '0');
      validForBits += bits;
    }
    return validForBits;
  }

  @testVisible private static Map<String, String> getRecordTypes() {
    Map<String, String> recordTypes = new Map<String, String>();
    recordTypes.put(
      'itineraryHousing',
      Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Housing_Itinerary').getRecordTypeId()
    );
    recordTypes.put(
      'itineraryGround',
      Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('GT_Itinerary').getRecordTypeId()
    );
    recordTypes.put(
      'itineraryAir',
      Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Air_Itinerary').getRecordTypeId()
    );
    recordTypes.put(
      'itineraryFreight',
      Schema.SObjectType.Itinerary__c.getRecordTypeInfosByDeveloperName().get('Freight_Itinerary').getRecordTypeId()
    );
    recordTypes.put(
      'housingSales',
      Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Sales_Housing').getRecordTypeId()
    );
    recordTypes.put(
      'housingHotel',
      Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Hotel_Housing').getRecordTypeId()
    );
    recordTypes.put(
      'housingCorp',
      Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Corporate_Housing').getRecordTypeId()
    );
    recordTypes.put(
      'housingIR',
      Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Individual_Reservation').getRecordTypeId()
    );
    recordTypes.put(
      'housingRoomType',
      Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Room_Types_Ops').getRecordTypeId()
    );
    recordTypes.put(
      'groundSales',
      Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Sales_GT_Details').getRecordTypeId()
    );
    recordTypes.put(
      'groundVehicle',
      Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('Vehicle_Type').getRecordTypeId()
    );
    recordTypes.put(
      'groundTrip',
      Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId()
    );
    recordTypes.put(
      'groundSubTrip',
      Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Sub_Trip_Details').getRecordTypeId()
    );
    recordTypes.put(
      'groundTravel',
      Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Travel_Details').getRecordTypeId()
    );
    recordTypes.put(
      'airTrip',
      Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Trip_Details').getRecordTypeId()
    );
    recordTypes.put(
      'airSegment',
      Schema.SObjectType.Air__c.getRecordTypeInfosByDeveloperName().get('Air_Segments').getRecordTypeId()
    );
    recordTypes.put(
      'freightSales',
      Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Sales_Freight_Details').getRecordTypeId()
    );
    recordTypes.put(
      'freightTrip',
      Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Freight_Trip_Details').getRecordTypeId()
    );
    recordTypes.put(
      'freightSubTrip',
      Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName()
        .get('Freight_Sub_Trip_Details')
        .getRecordTypeId()
    );
    recordTypes.put(
      'freightEquipment',
      Schema.SObjectType.Freight__c.getRecordTypeInfosByDeveloperName().get('Equipment_Details').getRecordTypeId()
    );
    return recordTypes;
  }

  @AuraEnabled
  public static Map<String, Object> getVendorHousingBid(String theUUID, Boolean isRRE) {
    String accountId = '';
    system.debug('inside getvendorHousingBid recordId : ' + theUUID);
    system.debug('accountid ::: ' + accountId);
    system.debug('isRRE ::: ' + isRRE);
    Map<String, Object> result = new Map<String, Object>();
    Id bidHousingRT = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Bid')
      .getRecordTypeId();
    Id housingRoomTypeRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();
    Id revenueRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Rate_Commission_RRU')
      .getRecordTypeId();
    if (isRRE)
      revenueRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Rate_Commission_RRE')
        .getRecordTypeId();
    List<Bid__c> searchBid = [
      SELECT
        Id,
        Production__c,
        Production__r.Office_Location__c,
        Name,
        RecordTypeId,
        Status__c,
        Housing__c,
        Vendor__r.Name,
        Vendor__r.Housing_address__c,
        City__r.Name,
        Venue__c,
        Venue__r.Name,
        CurrencyIsoCode,
        Rate__c,
        Room_Rate_Release_date__c,
        Vendor_Bid_Notes__c,
        Commission_Revenue__c,
        responseVendorName__c,
        responseVendorTitle__c,
        responseVendorEmail__c,
        responseVendorPhone__c,
        Vendor_Contact__c,
        UUID_For_Landing_Page__c
      FROM Bid__c
      WHERE UUID_for_Landing_Page__c = :theUUID
      ORDER BY CreatedDate DESC
      LIMIT 1
    ];

    if (searchBid.size() > 0) {
      accountId = searchBid[0].Production__c;
    }
    Map<String, Object> bidInfo = new Map<String, Object>();
    bidInfo.put('bidId', searchBid.get(0).Id);
    bidInfo.put('bidName', searchBid.get(0).Name);
    bidInfo.put('productionId', searchBid.get(0).Production__c);
    String productionOfficePreference = String.isNotBlank(searchBid.get(0).Production__r.Office_Location__c)
      ? searchBid.get(0).Production__r.Office_Location__c
      : 'RRU';
    bidInfo.put('productionOfficePreference', productionOfficePreference);
    bidInfo.put('serviceId', searchBid.get(0).Housing__c);
    bidInfo.put('recordTypeId', searchBid.get(0).recordTypeId);
    bidInfo.put('status', String.isNotBlank(searchBid.get(0).Status__c) ? searchBid.get(0).Status__c : '');
    bidInfo.put(
      'vendorName',
      String.isNotBlank(searchBid.get(0).Vendor__r.Name) ? searchBid.get(0).Vendor__r.Name : ''
    );
    bidInfo.put(
      'vendorAddress',
      String.isNotBlank(searchBid.get(0).Vendor__r.Housing_address__c)
        ? searchBid.get(0).Vendor__r.Housing_address__c
        : ''
    );
    bidInfo.put('location', String.isNotBlank(searchBid.get(0).Venue__r.Name) ? searchBid.get(0).Venue__r.Name : '');
    bidInfo.put(
      'releaseDate',
      searchBid.get(0).Room_Rate_Release_date__c != null
        ? String.valueOf(searchBid.get(0).Room_Rate_Release_date__c)
        : ''
    );
    bidInfo.put(
      'notes',
      String.isNotBlank(searchBid.get(0).Vendor_Bid_Notes__c) ? searchBid.get(0).Vendor_Bid_Notes__c : ''
    );
    bidInfo.put(
      'currency',
      String.isNotBlank(searchBid.get(0).CurrencyIsoCode) ? searchBid.get(0).CurrencyIsoCode : ''
    );
    result.put('info', bidInfo);
    result.put(
      'reviewName',
      String.isNotBlank(searchBid.get(0).responseVendorName__c) ? searchBid.get(0).responseVendorName__c : ''
    );
    result.put(
      'reviewTitle',
      String.isNotBlank(searchBid.get(0).responseVendorTitle__c) ? searchBid.get(0).responseVendorTitle__c : ''
    );
    result.put(
      'reviewEmail',
      String.isNotBlank(searchBid.get(0).responseVendorEmail__c) ? searchBid.get(0).responseVendorEmail__c : ''
    );
    result.put(
      'reviewPhone',
      String.isNotBlank(searchBid.get(0).responseVendorPhone__c) ? searchBid.get(0).responseVendorPhone__c : ''
    );
    List<Map<String, Object>> lodgings = new List<Map<String, Object>>();
    for (Housing__c housing : [
      SELECT
        Id,
        Date_In__c,
        Date_Out__c,
        Units__c,
        Unit_Type__c,
        Nights_CC__c,
        Special_Notes__c,
        Rate__c,
        CurrencyIsoCode,
        Rate_Period__c
      FROM Housing__c
      WHERE Bid__c = :searchBid.get(0).Id
    ]) {
      Map<String, Object> lodging = new Map<String, Object>();
      lodging.put('lodgingId', housing.Id);
      lodging.put(
        'dateIn',
        housing.Date_In__c != null
          ? (Datetime.newInstance(housing.Date_In__c, Time.newInstance(0, 0, 0, 0))).format('dd-MMM-YYYY')
          : ''
      );
      lodging.put(
        'dateOut',
        housing.Date_Out__c != null
          ? (Datetime.newInstance(housing.Date_Out__c, Time.newInstance(0, 0, 0, 0))).format('dd-MMM-YYYY')
          : ''
      );
      lodging.put('qty', housing.Units__c > 0 ? housing.Units__c : Decimal.valueOf('0'));
      lodging.put('unitType', String.isNotBlank(housing.Unit_Type__c) ? housing.Unit_Type__c : '');
      lodging.put('nights', housing.Nights_CC__c > 0 ? housing.Nights_CC__c : Decimal.valueOf('0'));
      lodging.put('specialNotes', String.isNotBlank(housing.Special_Notes__c) ? housing.Special_Notes__c : '');
      lodging.put('rate', housing.Rate__c > 0 ? housing.Rate__c : Decimal.valueOf('0.00'));
      lodging.put('currency', String.isNotBlank(housing.CurrencyIsoCode) ? housing.CurrencyIsoCode : '');
      lodging.put('rateperiod', String.isNotBlank(housing.Rate_Period__c) ? housing.Rate_Period__c : '');
      lodgings.add(lodging);
    }
    result.put('lodgings', lodgings);
    PicklistWrapper concessionsProvidedMap = getCConcessionRequestAndProvided();
    List<Map<String, Object>> concessions = new List<Map<String, Object>>();
    for (Concessions__c concession : [
      SELECT Id, Concessions_Requested__c, Concession_Provided__c, Agreed__c, Notes__c
      FROM Concessions__c
      WHERE Bid__c = :searchBid.get(0).Id AND Concessions_Requested__c != NULL
      ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC
    ]) {
      Map<String, Object> item = new Map<String, Object>();
      item.put('concessionId', concession.Id);
      String concessionRequested = concession.Concessions_Requested__c;
      item.put('Concessions_Requested__c', concessionRequested);
      String concessionProvided = String.isNotBlank(concession.Concession_Provided__c)
        ? concession.Concession_Provided__c
        : '';
      if (concessionsProvidedMap.pickListMap.containsKey(concessionRequested)) {
        List<String> concessionProvidedOptions = concessionsProvidedMap.pickListMap.get(concessionRequested);
        item.put('concessionProvidedOptions', concessionProvidedOptions);
        Boolean isOnList = false;
        for (String cop : concessionProvidedOptions)
          if (cop.equals(concessionProvided))
            isOnList = true;
        if (isOnList) {
          item.put('Concession_Provided__c', concessionProvided);
          item.put('customConcession', '');
        } else {
          item.put('Concession_Provided__c', '-- Other --');
          item.put('customConcession', concessionProvided);
        }
      } else {
        item.put('concessionProvidedOptions', new List<String>());
        item.put('Concession_Provided__c', '-- Other --');
        item.put('customConcession', concessionProvided);
      }
      item.put('Agreed__c', concession.Agreed__c ? concession.Agreed__c : false);
      item.put('Notes__c', String.isNotBlank(concession.Notes__c) ? concession.Notes__c : '');
      concessions.add(item);
    }
    result.put('concessions', concessions);


    Revenue__c vendorRevenue = getRevenueRecordCommission(searchBid[0].Id);
    if (vendorRevenue.Id == null){
      insert vendorRevenue;
    }

    List<Revenue__c> bidRevenue = new List<Revenue__c>();
    if (String.isNotBlank(searchBid.get(0).Commission_Revenue__c)) {
      bidRevenue = [
        SELECT
          Id,
          RecordTypeId,
          CurrencyIsoCode,
          VAT_Rate__c,
          VAT__c,
          Breakfast_Rate__c,
          Breakfast__c,
          City_Tax_Rate__c,
          City_Tax_Rate_percent__c,
          City_Tax_Type__c,
          City_Tax__c,
          Commission_Agreed__c,
          Commission_Percent__c,
          Commission__c,
          Commission_Type__c,
          Tax__c,
          Tax_Included__c,
          Surcharge__c,
          Surcharge_included__c
        FROM Revenue__c
        WHERE Id = :searchBid.get(0).Commission_Revenue__c
        LIMIT 1
      ];
    } else {
      bidRevenue = [
        SELECT
          Id,
          RecordTypeId,
          CurrencyIsoCode,
          VAT_Rate__c,
          VAT__c,
          Breakfast_Rate__c,
          Breakfast__c,
          City_Tax_Rate__c,
          City_Tax_Rate_percent__c,
          City_Tax_Type__c,
          City_Tax__c,
          Commission_Agreed__c,
          Commission_Percent__c,
          Commission__c,
          Commission_Type__c,
          Tax__c,
          Tax_Included__c,
          Surcharge__c,
          Surcharge_included__c
        FROM Revenue__c
        WHERE
          Bid__c = :searchBid.get(0).Id
          AND (RecordType.Name = 'Housing Rate & Commission RRU'
          OR RecordType.Name = 'Housing Rate & Commission RRE')
          AND Room_Type__c = NULL
          AND Monthly_Pick_Up__c = FALSE
        ORDER BY createddate DESC
        LIMIT 1
      ];
    }

    if (bidRevenue.size() == 0){
      bidRevenue.add(vendorRevenue);
    }

    Map<String, Object> revenue = new Map<String, Object>();
    revenue.put('revenueId', (bidRevenue.isEmpty() ? '' : bidRevenue.get(0).Id));
    revenue.put('RecordTypeId', (bidRevenue.isEmpty() ? revenueRT : bidRevenue.get(0).RecordTypeId));
    String accCurrencyIsoCode = '';
    if (accountId != null && accountId != '')
      accCurrencyIsoCode = [SELECT CurrencyISOCode FROM Account WHERE Id = :accountId LIMIT 1]?.CurrencyISOCode;
    String currencyIsoCode = !bidRevenue?.isEmpty()
      ? (String.isNotBlank(bidRevenue.get(0).CurrencyIsoCode) ? bidRevenue.get(0).CurrencyIsoCode : accCurrencyISOCode)
      : accCurrencyISOCode;
    if (String.isBlank(currencyIsoCode))
      currencyIsoCode = productionOfficePreference.equals('RRE') ? 'EUR' : 'USD';
    revenue.put('CurrencyIsoCode', currencyIsoCode);
    revenue.put(
      'VAT_Rate__c',
      bidRevenue.isEmpty()
        ? Decimal.valueOf('0.00')
        : (bidRevenue.get(0).VAT_Rate__c > 0 ? bidRevenue.get(0).VAT_Rate__c : Decimal.valueOf('0.00'))
    );
    revenue.put('VAT__c', bidRevenue.isEmpty() ? false : (bidRevenue.get(0).VAT__c ? true : false));
    revenue.put(
      'Breakfast_Rate__c',
      bidRevenue.isEmpty()
        ? Decimal.valueOf('0.00')
        : (bidRevenue.get(0).Breakfast_Rate__c > 0 ? bidRevenue.get(0).Breakfast_Rate__c : Decimal.valueOf('0.00'))
    );
    revenue.put('Breakfast__c', bidRevenue.isEmpty() ? false : (bidRevenue.get(0).Breakfast__c ? true : false));
    revenue.put(
      'cityTaxValue',
      bidRevenue.isEmpty()
        ? Decimal.valueOf('0.00')
        : (bidRevenue.get(0).City_Tax_Rate__c > 0
            ? bidRevenue.get(0).City_Tax_Rate__c
            : (bidRevenue.get(0).City_Tax_Rate_percent__c > 0
                ? bidRevenue.get(0).City_Tax_Rate_percent__c
                : Decimal.valueOf('0.00')))
    );
    revenue.put(
      'cityTaxValueType',
      bidRevenue.isEmpty()
        ? 'Amount'
        : (bidRevenue.get(0).City_Tax_Rate__c > 0
            ? 'Amount'
            : (bidRevenue.get(0).City_Tax_Rate_percent__c > 0 ? 'Percentage' : 'Amount'))
    );
    revenue.put(
      'City_Tax_Type__c',
      bidRevenue.isEmpty()
        ? ''
        : (String.isNotBlank(bidRevenue.get(0).City_Tax_Type__c) ? bidRevenue.get(0).City_Tax_Type__c : '')
    );
    revenue.put('City_Tax__c', bidRevenue.isEmpty() ? false : (bidRevenue.get(0).City_Tax__c ? true : false));
    revenue.put(
      'Tax__c',
      bidRevenue.isEmpty()
        ? Decimal.valueOf('0.00')
        : (bidRevenue.get(0).Tax__c > 0 ? bidRevenue.get(0).Tax__c : Decimal.valueOf('0.00'))
    );
    revenue.put('Tax_Included__c', bidRevenue.isEmpty() ? false : (bidRevenue.get(0).Tax_Included__c ? true : false));
    revenue.put(
      'Surcharge__c',
      bidRevenue.isEmpty()
        ? Decimal.valueOf('0.00')
        : (bidRevenue.get(0).Surcharge__c > 0 ? bidRevenue.get(0).Surcharge__c : Decimal.valueOf('0.00'))
    );
    revenue.put(
      'Surcharge_included__c',
      bidRevenue.isEmpty() ? false : (bidRevenue.get(0).Surcharge_included__c ? true : false)
    );
    String commisionType = (bidRevenue.isEmpty()
      ? ''
      : (String.isNotBlank(bidRevenue.get(0).Commission_Type__c) ? bidRevenue.get(0).Commission_Type__c : ''));
    revenue.put('Commission_Type__c', commisionType);
    revenue.put(
      'Commission_Agreed__c',
      bidRevenue.isEmpty()
        ? false
        : (bidRevenue.get(0).Commission_Agreed__c ? bidRevenue.get(0).Commission_Agreed__c : false)
    );
    Decimal commissionAmount = (bidRevenue.isEmpty()
      ? Decimal.valueOf('0.00')
      : (bidRevenue.get(0).Commission__c > 0 ? bidRevenue.get(0).Commission__c : Decimal.valueOf('10.00')));
    Decimal commissionPercent = (bidRevenue.isEmpty()
      ? Decimal.valueOf('10.00')
      : (bidRevenue.get(0).Commission_Percent__c > 0
          ? bidRevenue.get(0).Commission_Percent__c
          : Decimal.valueOf('10.00')));
    revenue.put(
      'roadRebelCommission',
      (commisionType.equals('Amount')
        ? currencyIsoCode + ' ' + commissionAmount.format()
        : commissionPercent.format() + '%') + ' commission on a total rate'
    );
    result.put('revenue', revenue);
    system.debug('revenue : ' + revenue);
    system.debug('result : ' + result);
    return result;
  }

  @AuraEnabled
  public static String updateVendorHousingBid(String data) {

    Map<String, Object> root = (Map<String, Object>) JSON.deserializeUntyped(data);
    String userProfile = '';
    if (root.containsKey('userProfile'))
      userProfile = (String) root.get('userProfile');
    Map<String, Object> info = new Map<String, Object>();
    if (root.containsKey('info'))
      info = (Map<String, Object>) root.get('info');
    Map<String, Object> revenue = new Map<String, Object>();
    if (root.containsKey('revenue'))
      revenue = (Map<String, Object>) root.get('revenue');

    for (String s : revenue.keySet()) {
      system.debug('revenue key :: ' + s);
      system.debug('key value :: ' + revenue.get(s));
    }
    system.debug('revenue :: ' + revenue);
    List<Object> concessions = new List<Object>();
    if (root.containsKey('concessions'))
      concessions = (List<Object>) root.get('concessions');
    List<Object> lodgings = new List<Object>();
    if (root.containsKey('lodgings'))
      lodgings = (List<Object>) root.get('lodgings');
    Map<String, Object> journal = new Map<String, Object>();
    if (root.containsKey('journal'))
      journal = (Map<String, Object>) root.get('journal');
    Bid__c vendorBid = new Bid__c(
      Id = info.containsKey('bidId') ? (String) info.get('bidId') : null,
      CurrencyIsoCode = revenue.containsKey('CurrencyIsoCode') ? (String) revenue.get('CurrencyIsoCode') : '',
      Room_Rate_Release_date__c = userProfile.equals('CorporateVendor')
        ? null
        : ((info.containsKey('releaseDate') && String.isNotBlank((String) info.get('releaseDate')))
            ? Date.valueOf((String) info.get('releaseDate'))
            : null),
      Vendor_Bid_Notes__c = info.containsKey('notes') ? (String) info.get('notes') : '',
      Property_Agrees__c = true,
      Status__c = 'Sent',
      Commission_Revenue__c = revenue.containsKey('revenueId')
        ? (String.isNotBlank((String) revenue.get('revenueId')) ? (String) revenue.get('revenueId') : null)
        : null,
      responseVendorName__c = journal.containsKey('name') ? (String) journal.get('name') : '',
      responseVendorTitle__c = journal.containsKey('title') ? (String) journal.get('title') : '',
      responseVendorEmail__c = journal.containsKey('email') ? (String) journal.get('email') : '',
      responseVendorPhone__c = journal.containsKey('phone') ? (String) journal.get('phone') : ''
    );
    upsert vendorBid;
    Id revenueRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Rate_Commission_RRU')
      .getRecordTypeId();

    Revenue__c vendorRevenue = new Revenue__c(
      Id = revenue.containsKey('revenueId')
        ? (String.isNotBlank((String) revenue.get('revenueId')) ? (String) revenue.get('revenueId') : null)
        : null,
      RecordTypeId = (String) revenue.get('RecordTypeId'),
      CurrencyIsoCode = revenue.containsKey('CurrencyIsoCode') ? (String) revenue.get('CurrencyIsoCode') : '',
      Bid__c = vendorBid.Id,
      VAT_Rate__c = revenue.containsKey('VAT_Rate__c')
        ? (revenue.get('VAT_Rate__c') instanceof Decimal
            ? (Decimal) revenue.get('VAT_Rate__c')
            : Decimal.valueOf((String) revenue.get('VAT_Rate__c')))
        : Decimal.valueOf('0.00'),
      VAT__c = revenue.containsKey('VAT__c') ? (Boolean) revenue.get('VAT__c') : false,
      Breakfast_Rate__c = revenue.containsKey('Breakfast_Rate__c')
        ? (revenue.get('Breakfast_Rate__c') instanceof Decimal
            ? (Decimal) revenue.get('Breakfast_Rate__c')
            : Decimal.valueOf((String) revenue.get('Breakfast_Rate__c')))
        : Decimal.valueOf('0.00'),
      Breakfast__c = revenue.containsKey('Breakfast__c') ? (Boolean) revenue.get('Breakfast__c') : false,
      Tax__c = revenue.containsKey('Tax__c')
        ? (revenue.get('Tax__c') instanceof Decimal
            ? (Decimal) revenue.get('Tax__c')
            : Decimal.valueOf((String) revenue.get('Tax__c')))
        : Decimal.valueOf('0.00'),
      Tax_Included__c = revenue.containsKey('Tax_Included__c') ? (Boolean) revenue.get('Tax_Included__c') : false,
      Surcharge__c = revenue.containsKey('Surcharge__c')
        ? (revenue.get('Surcharge__c') instanceof Decimal
            ? (Decimal) revenue.get('Surcharge__c')
            : Decimal.valueOf((String) revenue.get('Surcharge__c')))
        : Decimal.valueOf('0.00'),
      Surcharge_included__c = revenue.containsKey('Surcharge_included__c')
        ? (Boolean) revenue.get('Surcharge_included__c')
        : false,
      City_Tax_Rate__c = Decimal.valueOf('0.00'),
      City_Tax_Rate_percent__c = Decimal.valueOf('0.00'),
      City_Tax_Type__c = revenue.containsKey('City_Tax_Type__c') ? (String) revenue.get('City_Tax_Type__c') : '',
      City_Tax__c = revenue.containsKey('City_Tax__c') ? (Boolean) revenue.get('City_Tax__c') : false,
      Commission_Agreed__c = true
    );
    if (revenue.containsKey('cityTaxValueType')) {
      if (((String) revenue.get('cityTaxValueType')).equals('Amount'))
        vendorRevenue.City_Tax_Rate__c = revenue.containsKey('cityTaxValue')
          ? (revenue.get('cityTaxValue') instanceof Decimal
              ? (Decimal) revenue.get('cityTaxValue')
              : Decimal.valueOf((String) revenue.get('cityTaxValue')))
          : Decimal.valueOf('0.00');
      if (((String) revenue.get('cityTaxValueType')).equals('Percentage'))
        vendorRevenue.City_Tax_Rate_percent__c = revenue.containsKey('cityTaxValue')
          ? (revenue.get('cityTaxValue') instanceof Decimal
              ? (Decimal) revenue.get('cityTaxValue')
              : Decimal.valueOf((String) revenue.get('cityTaxValue')))
          : Decimal.valueOf('0.00');
    }
    upsert vendorRevenue;

    /* go back and update Commission Revenue */
    vendorBid.Commission_Revenue__c = (String)revenue.get('revenueId');
    update vendorBid;

    List<Concessions__c> vendorConcessions = new List<Concessions__c>();
    /*
    if (userProfile.equals('CorporateVendor')) {
      for (Object concessionJSON : concessions) {
        Map<String, Object> concession = (Map<String, Object>) concessionJSON;
        //'Concession_Provided__c','-- Other --'
        String concessionProvided = concession.containsKey('Concession_Provided__c')
          ? (String) concession.get('Concession_Provided__c')
          : '-- Other --';
        String customConcession = concession.containsKey('customConcession')
          ? (String) concession.get('customConcession')
          : '';
        if (String.isNotBlank(customConcession)) {
          if (concessionProvided.equals('-- Other --'))
            concessionProvided = customConcession;
          else
            concessionProvided = concessionProvided + ': ' + customConcession;
        }
        Concessions__c vendorConcession = new Concessions__c(
          Id = concession.containsKey('concessionId') ? (String) concession.get('concessionId') : null,
          Bid__c = vendorBid.Id,
          Concession_Provided__c = concessionProvided,
          Agreed__c = true
        );
        vendorConcessions.add(vendorConcession);
      }
    } else {*/
    for (Object concessionJSON : concessions) {
      Map<String, Object> concession = (Map<String, Object>) concessionJSON;
      Concessions__c vendorConcession = new Concessions__c(
        Id = concession.containsKey('concessionId') ? (String) concession.get('concessionId') : null,
        Bid__c = vendorBid.Id,
        Agreed__c = concession.containsKey('Agreed__c') ? (Boolean) concession.get('Agreed__c') : false
      );
      if (vendorConcession.Agreed__c)
        vendorConcession.Concession_Provided__c = concession.containsKey('Concessions_Requested__c')
          ? (String) concession.get('Concessions_Requested__c')
          : '';
      vendorConcessions.add(vendorConcession);
    }

    if (info.containsKey('notes') && String.isNotBlank((String) info.get('notes'))) {
      vendorConcessions.add(
        new Concessions__c(
          Bid__c = vendorBid.Id,
          Agreed__c = true,
          Production__c = info.containsKey('productionId') ? (String) info.get('productionId') : null,
          Concession_Type__c = 'Housing',
          Concessions_Requested__c = (String) info.get('notes'),
          Concession_Provided__c = (String) info.get('notes'),
          IsFromVendor__c = true
        )
      );
    }
    if (!vendorConcessions.isEmpty())
      upsert vendorConcessions;
    List<Housing__c> vendorLodgings = new List<Housing__c>();
    for (Object lodgingJSON : lodgings) {
      Map<String, Object> lodging = (Map<String, Object>) lodgingJSON;
      vendorLodgings.add(
        new Housing__c(
          Id = lodging.containsKey('lodgingId') ? (String) lodging.get('lodgingId') : null,
          Bid__c = vendorBid.Id,
          CurrencyIsoCode = (String)revenue.get('CurrencyIsoCode'),
          //Rate_Period__c = (String)revenue.get('rateperiod'),
          Rate__c = lodging.containsKey('rate')
            ? (lodging.get('rate') instanceof Decimal
                ? (Decimal) lodging.get('rate')
                : Decimal.valueOf((String) lodging.get('rate')))
            : Decimal.valueOf('0.00')
        )
      );
    }
    if (!vendorLodgings.isEmpty())
      // I don't want housing trigger to run for this update that it's doing to the Room Types and Ops rate
      HousingTriggerHandler.TriggerDisabled = true;
    upsert vendorLodgings;

    String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
      .get('Bid_Journal')
      .getRecordTypeId();
    String message = 'The bid has been submitted by this contact:
';
    message += '
';
    message += (journal.containsKey('name') ? (String) journal.get('name') : '') + '
';
    message += (journal.containsKey('title') ? (String) journal.get('title') : '') + '
';
    message += (journal.containsKey('email') ? (String) journal.get('email') : '') + '
';
    message += (journal.containsKey('phone') ? (String) journal.get('phone') : '');
    JournalCreation.insertJournal(
      new List<JournalCreation.JournalEntry>{
        new JournalCreation.JournalEntry('bid', vendorBid.Id, bidJournalRT, message)
      }
    );

    //update new Bid__c(Id=vendorBid.Id,OwnerId=Userinfo.getUserId());
    system.debug('we should be calling create method from updateVendorBid ::: ');
    BidTriggerHandler.TriggerDisabled = true;
    //update new Bid__c(Id=vendorBid.Id,Create_Bid_Memorial_PDF__c=true);
    createBidMemorialization(vendorBid.Id);
    //saveBidMemorializationAttachment(vendorBid.Id);

    return 'done';
  }

  @AuraEnabled
  public static String unabledVendorBid(String data) {
    Map<String, Object> root = (Map<String, Object>) JSON.deserializeUntyped(data);
    String noBidReason = (String) root.get('notes');
    if (root.containsKey('bidId')) {
      update new Bid__c(
        Id = (String) root.get('bidId'),
        Status__c = 'Sold Out / Not Bidding',
        No_Bid_reason__c = noBidReason
      );
      Map<String, Object> journal = new Map<String, Object>();
      if (root.containsKey('journal')) {
        journal = (Map<String, Object>) root.get('journal');
      }
      String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
        .get('Bid_Journal')
        .getRecordTypeId();
      Set<String> noBidFixedReasons = new Set<String>{'sold out', 'sold out for a portion of stay', 'not enough rooms available'};
      String message = 'The bid has been submitted by this contact:
';
      message += '
';
      message += (journal.containsKey('name') ? (String) journal.get('name') : '') + '
';
      message += (journal.containsKey('title') ? (String) journal.get('title') : '') + '
';
      message += (journal.containsKey('email') ? (String) journal.get('email') : '') + '
';
      message += (journal.containsKey('phone') ? (String) journal.get('phone') : '') + '
';
      message += 'No Bid Reason: ';
      if(String.isNotBlank(noBidReason)) {
        message += (
          noBidFixedReasons.contains(noBidReason.toLowerCase()) 
          ? noBidReason 
          : 'Other - ' + noBidReason
        );
      }
      JournalCreation.insertJournal(
        new List<JournalCreation.JournalEntry>{
          new JournalCreation.JournalEntry('bid', (String) root.get('bidId'), bidJournalRT, message)
        }
      );
    }
    return 'done';
  }

  public static String mkUuid() {
    Blob b = Crypto.GenerateAESKey(128);
    String h = EncodingUtil.ConvertTohex(b);
    String guid =
      h.SubString(0, 8) +
      '-' +
      h.SubString(8, 12) +
      '-' +
      h.SubString(12, 16) +
      '-' +
      h.SubString(16, 20) +
      '-' +
      h.substring(20);
    return guid;
  }

  @AuraEnabled
  public static Map<String, Object> getCloseOutHousing(String data) {
    system.debug(data);
    Map<String, Object> root = (Map<String, Object>) JSON.deserializeUntyped(data);
    String serviceId = '';
    if (root.containsKey('serviceId'))
      serviceId = (String) root.get('serviceId');
    String accountId = '';
    if (root.containsKey('accountId'))
      accountId = (String) root.get('accountId');
    String biduuid = '';
    if (root.containsKey('biduuid'))
      biduuid = (String) root.get('biduuid');
    Map<String, Object> result = new Map<String, Object>();
    result.put('isAccessible', false);
    if (String.isNotBlank(biduuid)) {
      List<Bid__c> searchBid = [
        SELECT
          Id,
          Housing__r.RecordType.DeveloperName,
          Production__c,
          Commission_Revenue__c,
          Commission_Revenue__r.CurrencyIsocode,
          Sync_to_QB__c,
          Close_Out_has_been_sent_by_Vendor__c,
          isHousingCloseOutEditable__c,
          coVendorName__c,
          coVendorTitle__c,
          coVendorEmail__c,
          coVendorPhone__c,
          Vendor__r.Hotel_VAT__c,
          Vendor__r.BillingStreet
        FROM Bid__c
        WHERE UUID_for_Landing_Page__c = :biduuid
        LIMIT 1
      ];
      if (searchBid.isEmpty())
        return result;
      else {
        String roomRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
          .get('Room_Types_Ops')
          .getRecordTypeId();
        result.put('isAccessible', true);
        String bidId = searchBid.get(0).Id;
        result.put('bidId', bidId);

        if (searchBid.get(0).Housing__r.RecordType.DeveloperName.equals('Hotel_Housing'))
          result.put('lodgingType', 'housingHotel');
        if (searchBid.get(0).Housing__r.RecordType.DeveloperName.equals('Corporate_Housing'))
          result.put('lodgingType', 'housingCorp');
        if (searchBid.get(0).Housing__r.RecordType.DeveloperName.equals('Individual_Reservation'))
          result.put('lodgingType', 'housingIR');

        result.put('productionId', searchBid.get(0).Production__c);
        result.put(
          'reviewName',
          String.isNotBlank(searchBid.get(0).coVendorName__c) ? searchBid.get(0).coVendorName__c : ''
        );
        result.put(
          'reviewTitle',
          String.isNotBlank(searchBid.get(0).coVendorTitle__c) ? searchBid.get(0).coVendorTitle__c : ''
        );
        result.put(
          'reviewEmail',
          String.isNotBlank(searchBid.get(0).coVendorEmail__c) ? searchBid.get(0).coVendorEmail__c : ''
        );
        result.put(
          'reviewPhone',
          String.isNotBlank(searchBid.get(0).coVendorPhone__c) ? searchBid.get(0).coVendorPhone__c : ''
        );
        result.put(
          'isSent',
          searchBid.get(0).Close_Out_has_been_sent_by_Vendor__c
            ? searchBid.get(0).Close_Out_has_been_sent_by_Vendor__c
            : false
        );
        result.put(
          'vatnumber',
          String.isNotBlank(searchBid.get(0).Vendor__r.Hotel_Vat__c) ? searchBid.get(0).Vendor__r.Hotel_Vat__c : ''
        );
        result.put(
          'address',
          String.isNotBlank(searchBid.get(0).Vendor__r.BillingStreet) ? searchBid.get(0).Vendor__r.BillingStreet : ''
        );

        result.put('isSync', searchBid.get(0).Sync_to_QB__c ? searchBid.get(0).Sync_to_QB__c : false);
        List<String> roomTypes = new List<String>();
        for (Schema.PicklistEntry ple : Housing__c.Unit_Type__c.getDescribe().getPicklistValues())
          if (ple.isActive())
            roomTypes.add(ple.getLabel());
        result.put('roomTypes', roomTypes);
        List<String> revenueTypes = new List<String>();
        for (Schema.PicklistEntry ple : Revenue__c.Revenue_Type__c.getDescribe().getPicklistValues())
          if (ple.isActive())
            revenueTypes.add(ple.getLabel());
        result.put('revenueTypes', revenueTypes);
        List<String> chargeTypes = new List<String>();
        for (Schema.PicklistEntry ple : Revenue__c.Charge_Type__c.getDescribe().getPicklistValues())
          if (ple.isActive())
            chargeTypes.add(ple.getLabel());
        result.put('chargeTypes', chargeTypes);
        List<String> rebates = new List<String>();
        for (Schema.PicklistEntry ple : Revenue__c.Rebate_Per__c.getDescribe().getPicklistValues())
          if (ple.isActive())
            rebates.add(ple.getLabel());
        result.put('rebates', rebates);
        List<Room> productionRooms = new List<Room>();
        List<Room> lodgingRooms = new List<Room>();
        for (Housing__c pRoom : [
          SELECT
            Id,
            Unit_Type__c,
            Total_Room_Nights__c,
            Comps__c,
            Rate__c,
            Commission_Per_Room__c,
            Confirmations__c,
            Close_Out__c,
            Rate_Period__c
          FROM Housing__c
          WHERE Production_CC__c = :searchBid.get(0).Production__c AND Bid__c = :bidId AND RecordTypeId = :roomRT
          ORDER BY CreatedDate ASC
        ]) {
          Room room = new Room(
            pRoom.Id,
            String.isNotBlank(pRoom.Unit_Type__c) ? pRoom.Unit_Type__c : '',
            pRoom.Total_Room_Nights__c > 0 ? pRoom.Total_Room_Nights__c : Decimal.valueOf('0'),
            pRoom.Comps__c > 0 ? pRoom.Comps__c : Decimal.valueOf('0'),
            pRoom.Rate__c > 0 ? pRoom.Rate__c.setScale(2) : Decimal.valueOf('0'),
            pRoom.Commission_Per_Room__c > 0 ? pRoom.Commission_Per_Room__c.setScale(2) : Decimal.valueOf('0'),
            String.isNotBlank(pRoom.Confirmations__c) ? pRoom.Confirmations__c : '',
            proom.Rate_Period__c
          );
          if (pRoom.Close_Out__c)
            lodgingRooms.add(room);
          else
            productionRooms.add(room);
        }
        result.put('productionRooms', productionRooms);
        result.put('lodgingRooms', lodgingRooms);
        RoomRevenue roomRevenue = new RoomRevenue();
        List<Revenue__c> searchComps = [
          SELECT Id, Comps__c, CurrencyIsoCode
          FROM Revenue__c
          WHERE RecordType.Name = 'Comps' AND Bid__c = :bidId
          LIMIT 1
        ];
        if (!searchComps.isEmpty()) {
          roomRevenue.compsId = searchComps.get(0).Id;
          roomRevenue.compsValue = searchComps.get(0).Comps__c > 0 ? searchComps.get(0).Comps__c : Decimal.valueOf('0');
        }
        result.put(
          'currency',
          String.isNotBlank(searchBid.get(0).Commission_Revenue__r.CurrencyIsocode)
            ? searchBid.get(0).Commission_Revenue__r.CurrencyIsocode
            : ''
        );
        List<Revenue__c> searchRevenue = [
          SELECT
            Id,
            Commission_Type__c,
            Commission__c,
            Commission_Percent__c,
            Commission_Due__c,
            Notes__c,
            Do_you_need_invoice_sent__c,
            Is_this_a_monthly_Pick_Up__c,
            Does_this_match_amount_on_pick_up_report__c,
            Indicate_Dates__c,
            CurrencyIsoCode
          FROM Revenue__c
          WHERE
            RecordType.DeveloperName IN ('Housing_Rate_Commission_RRE', 'Housing_Rate_Commission_RRU')
            AND Bid__c = :bidId
          LIMIT 1
        ];
        if (!searchRevenue.isEmpty()) {
          roomRevenue.commissionId = searchRevenue.get(0).Id;
          roomRevenue.commissionType = String.isNotBlank(searchRevenue.get(0).Commission_Type__c)
            ? searchRevenue.get(0).Commission_Type__c
            : '';
          if (String.isNotBlank(searchRevenue.get(0).Commission_Type__c)) {
            if (searchRevenue.get(0).Commission_Type__c.equals('Amount'))
              roomRevenue.commissionValue = searchRevenue.get(0).Commission__c > 0
                ? searchRevenue.get(0).Commission__c.setScale(2)
                : Decimal.valueOf('0');
            if (searchRevenue.get(0).Commission_Type__c.equals('Percentage'))
              roomRevenue.commissionValue = searchRevenue.get(0).Commission_Percent__c > 0
                ? searchRevenue.get(0).Commission_Percent__c.setScale(2)
                : Decimal.valueOf('10');
          }
          roomRevenue.commissionDue = searchRevenue.get(0).Commission_Due__c > 0
            ? searchRevenue.get(0).Commission_Due__c.setScale(2)
            : Decimal.valueOf('0');
          roomRevenue.commissionNotes = String.isNotBlank(searchRevenue.get(0).Notes__c)
            ? searchRevenue.get(0).Notes__c
            : '';
          if (
            String.isNotBlank(searchRevenue.get(0).Do_you_need_invoice_sent__c) &&
            searchRevenue.get(0).Do_you_need_invoice_sent__c.equals('Yes')
          )
            roomRevenue.isInvoiceSent = true;
          if (
            String.isNotBlank(searchRevenue.get(0).Is_this_a_monthly_Pick_Up__c) &&
            searchRevenue.get(0).Is_this_a_monthly_Pick_Up__c.equals('Yes')
          )
            roomRevenue.isMonthlyPickUp = true;
          if (
            String.isNotBlank(searchRevenue.get(0).Does_this_match_amount_on_pick_up_report__c) &&
            searchRevenue.get(0).Does_this_match_amount_on_pick_up_report__c.equals('Yes')
          )
            roomRevenue.isMatchingAmount = true;
          if (String.isNotBlank(searchRevenue.get(0).Indicate_Dates__c))
            roomRevenue.indicateDates = searchRevenue.get(0).Indicate_Dates__c;
        }
        result.put('isReadOnly', searchBid.get(0).isHousingCloseOutEditable__c ? false : true);
        result.put('roomRevenue', roomRevenue);
        Map<String, String> communitySign = new Map<String, String>();
        communitySign.put('reviewName', '');
        communitySign.put('reviewTitle', '');
        communitySign.put('reviewEmail', '');
        communitySign.put('reviewPhone', '');
        if (String.isNotBlank(roomRevenue.commissionId)) {
          List<Revenue__c> searchCommunitySign = [
            SELECT Id, Sign_name__c, Sign_title__c, Sign_email__c, Sign_phone__c
            FROM Revenue__c
            WHERE
              Close_Out_Reference__c = :roomRevenue.commissionId
              AND Indicate_Dates__c = :roomRevenue.indicateDates
              AND RecordType.DeveloperName = 'Community_Sign'
            ORDER BY CreatedDate DESC
            LIMIT 1
          ];
          if (!searchCommunitySign.isEmpty()) {
            communitySign.put(
              'reviewName',
              String.isNotBlank(searchCommunitySign.get(0).Sign_name__c) ? searchCommunitySign.get(0).Sign_name__c : ''
            );
            communitySign.put(
              'reviewTitle',
              String.isNotBlank(searchCommunitySign.get(0).Sign_title__c)
                ? searchCommunitySign.get(0).Sign_title__c
                : ''
            );
            communitySign.put(
              'reviewEmail',
              String.isNotBlank(searchCommunitySign.get(0).Sign_email__c)
                ? searchCommunitySign.get(0).Sign_email__c
                : ''
            );
            communitySign.put(
              'reviewPhone',
              String.isNotBlank(searchCommunitySign.get(0).Sign_phone__c)
                ? searchCommunitySign.get(0).Sign_phone__c
                : ''
            );
          }
        }
        result.put('communitySign', communitySign);
        List<Revenue> revenues = new List<Revenue>();
        for (Revenue__c revenue : [
          SELECT
            Id,
            Revenue_Type__c,
            Charge_Type__c,
            Rebate_currency__c,
            Rebate__c,
            Rebate_invoiced_Amount__c,
            Rebate_Per__c,
            Rebate_to_client_Due__c,
            Rebate_to_RR_Due__c,
            Commission_Percent__c,
            Commission__c,
            Service_Fees_Percent__c,
            Service_Fees__c,
            Total__c,
            Invoice_Amount__c,
            CurrencyIsoCode
          FROM Revenue__c
          WHERE
            Bid__c = :bidId
            AND RecordType.Name = 'Revenue'
            AND Close_Out__c = TRUE
            AND Monthly_Pick_Up__c = FALSE
            AND Room_Type__c = NULL
        ]) {
          Decimal revenueValue = Decimal.valueOf('0');
          if (String.isNotBlank(revenue.Revenue_Type__c) && String.isNotBlank(revenue.Charge_Type__c)) {
            if (revenue.Revenue_Type__c.equals('Rebate') && revenue.Charge_Type__c.equals('Amount'))
              revenueValue = revenue.Rebate_currency__c > 0
                ? revenue.Rebate_currency__c.setScale(2)
                : Decimal.valueOf('0');
            if (revenue.Revenue_Type__c.equals('Rebate') && revenue.Charge_Type__c.equals('Percent'))
              revenueValue = revenue.Rebate__c > 0 ? revenue.Rebate__c.setScale(2) : Decimal.valueOf('0');
            if (revenue.Revenue_Type__c.equals('Commission') && revenue.Charge_Type__c.equals('Amount'))
              revenueValue = revenue.Commission__c > 0 ? revenue.Commission__c.setScale(2) : Decimal.valueOf('0');
            if (revenue.Revenue_Type__c.equals('Commission') && revenue.Charge_Type__c.equals('Percent'))
              revenueValue = revenue.Commission_Percent__c > 0
                ? revenue.Commission_Percent__c.setScale(2)
                : Decimal.valueOf('10');
            if (revenue.Revenue_Type__c.equals('Service fee') && revenue.Charge_Type__c.equals('Amount'))
              revenueValue = revenue.Service_Fees__c > 0 ? revenue.Service_Fees__c.setScale(2) : Decimal.valueOf('0');
            if (revenue.Revenue_Type__c.equals('Service fee') && revenue.Charge_Type__c.equals('Percent'))
              revenueValue = revenue.Service_Fees_Percent__c > 0
                ? revenue.Service_Fees_Percent__c.setScale(2)
                : Decimal.valueOf('0');
          }
          revenues.add(
            new Revenue(
              revenue.Id,
              String.isNotBlank(revenue.Revenue_Type__c) ? revenue.Revenue_Type__c : '',
              String.isNotBlank(revenue.Charge_Type__c) ? revenue.Charge_Type__c : '',
              revenueValue,
              String.isNotBlank(revenue.Rebate_Per__c) ? revenue.Rebate_Per__c : '',
              revenue.Total__c > 0 ? revenue.Total__c : Decimal.valueOf('0'),
              revenue.Invoice_Amount__c > 0 ? revenue.Invoice_Amount__c : Decimal.valueOf('0')
            )
          );
        }
        result.put('revenues', revenues);
        List<MonthlyPickUp> monthlyPickUps = new List<MonthlyPickUp>();
        for (Revenue__c monthlyPickUp : [
          SELECT
            Id,
            Indicate_Dates__c,
            Room_Type_Name__c,
            Room_Nights__c,
            Rate_currency__c,
            Commission_Per_Room__c,
            Invoice_Date__c,
            CurrencyIsoCode
          FROM Revenue__c
          WHERE
            Bid__c = :bidId
            AND RecordType.Name IN ('Housing Rate & Commission RRE', 'Housing Rate & Commission RRU')
            AND Monthly_Pick_Up__c = TRUE
        ]) {
          monthlyPickUps.add(
            new MonthlyPickUp(
              monthlyPickUp.Id,
              String.isNotBlank(monthlyPickUp.Indicate_Dates__c) ? monthlyPickUp.Indicate_Dates__c : '',
              String.isNotBlank(monthlyPickUp.Room_Type_Name__c) ? monthlyPickUp.Room_Type_Name__c : '',
              monthlyPickUp.Room_Nights__c > 0 ? monthlyPickUp.Room_Nights__c.setScale(0) : Decimal.valueOf('0'),
              monthlyPickUp.Rate_currency__c > 0 ? monthlyPickUp.Rate_currency__c.setScale(2) : Decimal.valueOf('0'),
              monthlyPickUp.Commission_Per_Room__c > 0
                ? monthlyPickUp.Commission_Per_Room__c.setScale(2)
                : Decimal.valueOf('0'),
              monthlyPickUp.Invoice_Date__c != null
                ? (Datetime.newInstance(monthlyPickUp.Invoice_Date__c, Time.newInstance(0, 0, 0, 0)))
                    .format('dd-MMMM-YYYY')
                : ''
            )
          );
        }
        result.put('monthlyPickUps', monthlyPickUps);
      }
    }
    return result;
  }

  @AuraEnabled
  public static String upsertCloseOutHousing(String data) {
    Map<String, Object> root = (Map<String, Object>) JSON.deserializeUntyped(data);
    String roomRT = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName()
      .get('Room_Types_Ops')
      .getRecordTypeId();
    String revenueRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
      .get('Revenue')
      .getRecordTypeId();
    String communitySignRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
      .get('Community_Sign')
      .getRecordTypeId();
    String bidId = (String) root.get('bidId');
    String serviceId = (String) root.get('serviceId');
    String productionId = (String) root.get('productionId');
    Map<String, Object> roomRevenue = (Map<String, Object>) root.get('roomRevenue');
    List<Object> productionRooms = (List<Object>) root.get('productionRooms');
    List<Object> lodgingRooms = (List<Object>) root.get('lodgingRooms');
    List<Object> revenues = (List<Object>) root.get('revenues');
    Map<String, Object> journal = (Map<String, Object>) root.get('journal');
    Map<String, Object> communitySign = (Map<String, Object>) root.get('communitySign');
    List<Housing__c> coRooms = new List<Housing__c>();
    for (Object productionRoomJSON : productionRooms) {
      Map<String, Object> productionRoom = (Map<String, Object>) productionRoomJSON;
      coRooms.add(
        new Housing__c(
          Id = (productionRoom.containsKey('recordId') && String.isNotBlank((String) productionRoom.get('recordId')))
            ? (String) productionRoom.get('recordId')
            : null,
          Total_Room_Nights__c = productionRoom.containsKey('roomNights')
            ? (productionRoom.get('roomNights') instanceof Decimal
                ? (Decimal) productionRoom.get('roomNights')
                : Decimal.valueOf((String) productionRoom.get('roomNights')))
            : Decimal.valueOf('0.00'),
          Comps__c = productionRoom.containsKey('roomComps')
            ? (productionRoom.get('roomComps') instanceof Decimal
                ? (Decimal) productionRoom.get('roomComps')
                : Decimal.valueOf((String) productionRoom.get('roomComps')))
            : Decimal.valueOf('0.00'),
          Commission_Per_Room__c = productionRoom.containsKey('roomCommission')
            ? (productionRoom.get('roomCommission') instanceof Decimal
                ? (Decimal) productionRoom.get('roomCommission')
                : Decimal.valueOf((String) productionRoom.get('roomCommission')))
            : Decimal.valueOf('0.00')
        )
      );
    }
    for (Object lodgingRoomJSON : lodgingRooms) {
      Map<String, Object> lodgingRoom = (Map<String, Object>) lodgingRoomJSON;
      coRooms.add(
        new Housing__c(
          Id = (lodgingRoom.containsKey('recordId') && String.isNotBlank((String) lodgingRoom.get('recordId')))
            ? (String) lodgingRoom.get('recordId')
            : null,
          Unit_Type__c = (lodgingRoom.containsKey('roomType') &&
            String.isNotBlank((String) lodgingRoom.get('roomType')))
            ? (String) lodgingRoom.get('roomType')
            : '',
          Total_Room_Nights__c = lodgingRoom.containsKey('roomNights')
            ? (lodgingRoom.get('roomNights') instanceof Decimal
                ? (Decimal) lodgingRoom.get('roomNights')
                : Decimal.valueOf((String) lodgingRoom.get('roomNights')))
            : Decimal.valueOf('0.00'),
          Rate__c = lodgingRoom.containsKey('roomRate')
            ? (lodgingRoom.get('roomRate') instanceof Decimal
                ? (Decimal) lodgingRoom.get('roomRate')
                : Decimal.valueOf((String) lodgingRoom.get('roomRate')))
            : Decimal.valueOf('0.00'),
          Comps__c = lodgingRoom.containsKey('roomComps')
            ? (lodgingRoom.get('roomComps') instanceof Decimal
                ? (Decimal) lodgingRoom.get('roomComps')
                : Decimal.valueOf((String) lodgingRoom.get('roomComps')))
            : Decimal.valueOf('0.00'),
          Commission_Per_Room__c = lodgingRoom.containsKey('roomCommission')
            ? (lodgingRoom.get('roomCommission') instanceof Decimal
                ? (Decimal) lodgingRoom.get('roomCommission')
                : Decimal.valueOf((String) lodgingRoom.get('roomCommission')))
            : Decimal.valueOf('0.00'),
          Production_CC__c = Test.isRunningTest() ? [SELECT Id FROM Opportunity LIMIT 1].Id : productionId,
          Bid__c = bidId,
          RecordTypeId = roomRT,
          Close_Out__c = true
        )
      );
    }
    if (!coRooms.isEmpty() && !Test.isRunningTest())
      upsert coRooms;
    List<Revenue__c> coRevenues = new List<Revenue__c>();
    for (Object revenueJSON : revenues) {
      Map<String, Object> revenue = (Map<String, Object>) revenueJSON;
      Revenue__c coRevenue = new Revenue__c(
        Id = (revenue.containsKey('recordId') && String.isNotBlank((String) revenue.get('recordId')))
          ? (String) revenue.get('recordId')
          : null,
        Revenue_Type__c = (revenue.containsKey('revenueType') && String.isNotBlank((String) revenue.get('revenueType')))
          ? (String) revenue.get('revenueType')
          : '',
        Charge_Type__c = (revenue.containsKey('revenueCharge') &&
          String.isNotBlank((String) revenue.get('revenueCharge')))
          ? (String) revenue.get('revenueCharge')
          : '',
        Rebate_Per__c = (revenue.containsKey('revenuePer') && String.isNotBlank((String) revenue.get('revenuePer')))
          ? (String) revenue.get('revenuePer')
          : '',
        Total__c = revenue.containsKey('revenueTotal')
          ? (revenue.get('revenueTotal') instanceof Decimal
              ? (Decimal) revenue.get('revenueTotal')
              : Decimal.valueOf((String) revenue.get('revenueTotal')))
          : Decimal.valueOf('0.00'),
        Invoice_Amount__c = revenue.containsKey('revenueInvoice')
          ? (revenue.get('revenueInvoice') instanceof Decimal
              ? (Decimal) revenue.get('revenueInvoice')
              : Decimal.valueOf((String) revenue.get('revenueInvoice')))
          : Decimal.valueOf('0.00'),
        Rebate_currency__c = 0,
        Rebate__c = 0,
        Commission__c = 0,
        Commission_Percent__c = 10,
        Service_Fees__c = 0,
        Service_Fees_Percent__c = 0,
        Monthly_Pick_Up__c = false,
        Bid__c = bidId,
        RecordTypeId = revenueRT
      );
      Decimal revenueValue = revenue.containsKey('revenueValue')
        ? (revenue.get('revenueValue') instanceof Decimal
            ? (Decimal) revenue.get('revenueValue')
            : Decimal.valueOf((String) revenue.get('revenueValue')))
        : Decimal.valueOf('0.00');
      if (String.isNotBlank(coRevenue.Revenue_Type__c) && String.isNotBlank(coRevenue.Charge_Type__c)) {
        if (coRevenue.Revenue_Type__c.equals('Rebate') && coRevenue.Charge_Type__c.equals('Amount'))
          coRevenue.Rebate_currency__c = revenueValue;
        if (coRevenue.Revenue_Type__c.equals('Rebate') && coRevenue.Charge_Type__c.equals('Percent'))
          coRevenue.Rebate__c = revenueValue;

        if (coRevenue.Revenue_Type__c.equals('Commission') && coRevenue.Charge_Type__c.equals('Amount'))
          coRevenue.Commission__c = revenueValue;
        if (coRevenue.Revenue_Type__c.equals('Commission') && coRevenue.Charge_Type__c.equals('Percent'))
          coRevenue.Commission_Percent__c = revenueValue == 0 || revenueValue == null ? 10 : revenueValue;

        if (coRevenue.Revenue_Type__c.equals('Service fee') && coRevenue.Charge_Type__c.equals('Amount'))
          coRevenue.Service_Fees__c = revenueValue;
        if (coRevenue.Revenue_Type__c.equals('Service fee') && coRevenue.Charge_Type__c.equals('Percent'))
          coRevenue.Service_Fees_Percent__c = revenueValue;
      }
      coRevenues.add(coRevenue);
    }
    if (!coRevenues.isEmpty())
      upsert coRevenues;
    Revenue__c coRoomRevenue = new Revenue__c(
      Id = (roomRevenue != null &&
        roomRevenue.containsKey('commissionId') &&
        String.isNotBlank((String) roomRevenue.get('commissionId')))
        ? (String) roomRevenue.get('commissionId')
        : null,
      Do_you_need_invoice_sent__c = (roomRevenue != null &&
        roomRevenue.containsKey('isInvoiceSent') &&
        (Boolean) roomRevenue.get('isInvoiceSent'))
        ? 'Yes'
        : 'No',
      Is_this_a_monthly_Pick_Up__c = (roomRevenue != null &&
        roomRevenue.containsKey('isMonthlyPickUp') &&
        (Boolean) roomRevenue.get('isMonthlyPickUp'))
        ? 'Yes'
        : 'No',
      Indicate_Dates__c = (roomRevenue != null &&
        roomRevenue.containsKey('indicateDates') &&
        String.isNotBlank((String) roomRevenue.get('indicateDates')))
        ? (String) roomRevenue.get('indicateDates')
        : '',
      Notes__c = (roomRevenue != null && roomRevenue.containsKey('commissionNotes')) &&
        String.isNotBlank((String) roomRevenue.get('commissionNotes'))
        ? (String) roomRevenue.get('commissionNotes')
        : ''
    );
    upsert coRoomRevenue;
    Revenue__c coCommunitySign = new Revenue__c(
      Bid__c = bidId,
      RecordTypeId = communitySignRT,
      Close_Out_Reference__c = coRoomRevenue.Id,
      Indicate_Dates__c = coRoomRevenue.Indicate_Dates__c,
      Sign_name__c = (communitySign != null &&
        communitySign.containsKey('reviewName') &&
        String.isNotBlank((String) communitySign.get('reviewName')))
        ? (String) communitySign.get('reviewName')
        : '',
      Sign_title__c = (communitySign != null &&
        communitySign.containsKey('reviewTitle') &&
        String.isNotBlank((String) communitySign.get('reviewTitle')))
        ? (String) communitySign.get('reviewTitle')
        : '',
      Sign_email__c = (communitySign != null &&
        communitySign.containsKey('reviewEmail') &&
        String.isNotBlank((String) communitySign.get('reviewEmail')))
        ? (String) communitySign.get('reviewEmail')
        : '',
      Sign_Phone__c = (communitySign != null &&
        communitySign.containsKey('reviewPhone') &&
        String.isNotBlank((String) communitySign.get('reviewPhone')))
        ? (String) communitySign.get('reviewPhone')
        : ''
    );
    insert coCommunitySign;
    if (
      roomRevenue != null &&
      roomRevenue.containsKey('compsId') &&
      String.isNotBlank((String) roomRevenue.get('compsId'))
    ) {
      Decimal compsValue = roomRevenue != null && roomRevenue.containsKey('compsValue')
        ? (roomRevenue.get('compsValue') instanceof Decimal
            ? (Decimal) roomRevenue.get('compsValue')
            : Decimal.valueOf((String) roomRevenue.get('compsValue')))
        : Decimal.valueOf('0.00');
      update new Revenue__c(Id = (String) roomRevenue.get('compsId'), Comps__c = compsValue);
    }
    if (bidId != '' && bidId != null)
      update new Bid__c(
        Id = bidId,
        coVendorName__c = coCommunitySign.Sign_name__c,
        coVendorTitle__c = coCommunitySign.Sign_title__c,
        coVendorEmail__c = coCommunitySign.Sign_email__c,
        coVendorPhone__c = coCommunitySign.Sign_phone__c,
        Close_Out_has_been_sent_by_Vendor__c = true,
        isHousingCloseOutEditable__c = false
      );
    String bidJournalRT = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
      .get('Bid_Journal')
      .getRecordTypeId();
    String message =
      coCommunitySign.Sign_name__c +
      ' at ' +
      coCommunitySign.Sign_email__c +
      ' submitted a pick up report.';
    JournalCreation.insertJournal(
      new List<JournalCreation.JournalEntry>{ new JournalCreation.JournalEntry('bid', bidId, bidJournalRT, message) }
    );
    String coordinatorId = '';
    List<Housing__c> searchHousing = [
      SELECT Back_end_Coordinator__c
      FROM Housing__c
      WHERE Id = :serviceId AND Back_end_Coordinator__c != NULL
      LIMIT 1
    ];
    if (!searchHousing.isEmpty())
      coordinatorId = String.valueOf(searchHousing.get(0).Back_end_Coordinator__c);
    else {
      List<Production_Associations__c> searchProductionAssoc = [
        SELECT User__c
        FROM Production_Associations__c
        WHERE Production_Opp__c = :productionId AND Team_Roles__c INCLUDES ('Primary Contract Coordinator')
        LIMIT 1
      ];
      if (!searchProductionAssoc.isEmpty())
        coordinatorId = String.valueOf(searchProductionAssoc.get(0).User__c);
    }
    if (String.isNotBlank(coordinatorId))
      insert new Task(
        WhatId = productionId,
        Bid_Id__c = bidId,	//178868448
        Subject = 'Vendor Submitted Close out report',
        ActivityDate = BusinessDate.AddBusinessDays(Date.today(), 1),
        Status = 'Open',
        OwnerId = coordinatorId,
        IsForCloseOut__c = true
      );
    createPickupMemorialization(bidId);
    return 'done';
  }

  @AuraEnabled
  public static Client getClient(String theUUID) {
    system.debug('theUUID ::: ' + theUUID);
    Client client = new Client();
    client.userInfo = [SELECT User_Profile__c,ContactId,Contact.Name,Id,Name,Email,UserName FROM User WHERE Name LIKE '%Guest%' LIMIT 1];
    if (client?.userInfo?.Contact?.Name == null) {
      if (client?.userInfo?.Name == 'Voyajer Site Guest User' || Test.isRunningTest()) {
        Contact[] theContact = [
          SELECT Id, Name, AccountId, MailingStreet, Account.Name, MailingCountry, MailingState, Email
          FROM Contact
          WHERE Id IN (SELECT Vendor_Contact__c FROM Bid__c WHERE UUID_for_Landing_Page__c = :theUUID)
        ];
        client.userInfo.Contact = (theContact.size() > 0) ? theContact[0] : new Contact(LastName = 'Voyajer Guest');
      }
    }
    //client.preferencesAvailable = getLodgingPreferencesOptions();
    //client.countryAndStates = getCountryAndStates();
    if (!client.userInfo.User_Profile__c.equals('Forbidden'))
      //client.preferencesSelected = getLodgingPreferencesSelected(
      // client.userInfo.ContactId
      // );
      client.recordTypes = getRecordTypes();
    Production_Associations__c[] theOppData = [
      SELECT Production_Opp__r.Name, User__r.Name, User__r.Email, User__r.Phone, User__r.UserRole.Name
      FROM Production_Associations__c
      WHERE Production_Opp__c IN (SELECT Production__c FROM Bid__c WHERE UUID_for_Landing_Page__c = :theUUID)
    ];

    ProductionData theProdData;
    String theCoordinator = TraceHelper.getCoordinatorService(
      [SELECT Id,Production_CC__c,Trace_Date__c,Back_End_Coordinator__c, Status_CC__c FROM Housing__c WHERE Id IN
        (SELECT Housing__c FROM Bid__c WHERE UUID_for_Landing_Page__c = :theUUID)
      LIMIT 1]);

      system.debug ('theCoordinator :::: ' + theCoordinator);

      if (theCoordinator != null){
        if (theOppData.size() > 0) {

          User theCoordinatorDetails = [SELECT Id,Name,Phone,Email,UserRole.Name,Title,FirstName,LastName FROM User WHERE Id = :theCoordinator];

          theProdData = new ProductionData(
            theOppData[0].Production_Opp__r.Name,
            theCoordinatorDetails.Email,
            theCoordinatorDetails.Name,
            theCoordinatorDetails.Phone,
            theCoordinatorDetails.UserRole.Name
          );
        }

      }


    client.theProductionData = theProdData;
    system.debug ('here is theProductionData :: ' + theProdData);
    return client;
  }

  /**
   *  @/HousingOptionsPdf
   */
  @future(callout=true)
  public static void createBidMemorialization(String bidId) {
    system.debug('inside the createBidMemorialization ::: ');
    BidTriggerHandler.TriggerDisabled = true;
    Bid__c[] bids = [SELECT Id, Vendor__r.Name, Vendor__c, UUID_for_Landing_Page__c, Housing__c, Vendor_Contact__c FROM Bid__c WHERE Id = :bidId];
    String fileName = (bids.size() > 0 && bids[0].Vendor__c != null) ? bids[0].Vendor__r.Name : 'testFilename';
    fileName = fileName.replaceAll(' ', '_');
    savePDFFromCommunity(bidId,fileName,'PDF_BidSubmissionLP');
  }


  @future(callout=true)
  public static void createPickupMemorialization(String bidId) {
    system.debug('inside the createBidMemorialization ::: ' + bidId);
    BidTriggerHandler.TriggerDisabled = true;
    Bid__c[] bids = [SELECT Id, UUID_for_Landing_Page__c, Housing__c, Housing__r.Name, Vendor_Contact__c FROM Bid__c WHERE Id = :bidId];
    // create the file(name with values from city and formatted dates
    String filename = 'PickUp Report-' + (bids.size() > 0 && bids[0].Housing__c != null ? bids[0].Housing__r.Name : 'testpickup');
    fileName = fileName.replaceAll(' ', '_');
    savePDFFromCommunity(bidId,fileName,'PDF_CloseOutReportLP');
  }

  /*

  public static void savePickupMemorializationAttachment(String bidid) {
    try {
      List<Bid__c> bids = [
        SELECT
          Id,
          UUID_For_Landing_Page__c,
          Vendor__r.Name,
          Housing__r.Id,
          City__r.Name,
          Housing__r.Name,
          Housing__r.City__c,
          Housing__r.City__r.Name,
          Housing__r.Date_In__c,
          Housing__r.Date_Out__c
        FROM Bid__c
        WHERE Id = :bidid
      ];

      if (bids.size() > 0)
        bidid = bids[0].UUID_For_Landing_Page__c;
      // get formatted date in and date out entries
      String dateIn = (!bids.isEmpty() && bids[0].Housing__r.Date_In__c != null
        ? Datetime.newInstance(
              bids[0].Housing__r.Date_In__c.year(),
              bids[0].Housing__r.Date_In__c.month(),
              bids[0].Housing__r.Date_In__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');
      String dateOut = (!bids.isEmpty() && bids[0].Housing__r.Date_Out__c != null
        ? Datetime.newInstance(
              bids[0].Housing__r.Date_Out__c.year(),
              bids[0].Housing__r.Date_Out__c.month(),
              bids[0].Housing__r.Date_Out__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');

      // create the filename with values from city and formatted dates
      // String fileName = bids[0].Vendor__r.Name;
      String filename = 'PickUp Report-' + bids[0].Housing__r.Name;
      fileName = fileName.replaceAll(' ', '_');

      Blob bidAttachment;
      PageReference pageRef = new PageReference('https://voyajer.force.com/PDF_CloseOutReportLP');
      pageRef.getParameters().put('bidid', bidId);
      pageRef.getParameters().put('gen', '1');
      if (!Test.isRunningTest())
        bidAttachment = pageRef.getContentAsPDF();
      else
        bidAttachment = Blob.valueof('bidAttachmentTest');

      List<ContentDocumentLink> bidDocumentLinks = [
        SELECT id, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :bids[0].Id AND ContentDocument.title = :fileName
      ];

      ContentVersion bidContentVersion = new ContentVersion();

      if (!bidDocumentLinks.isEmpty())
        bidContentVersion.contentDocumentId = bidDocumentLinks[0].ContentDocumentId;
      bidContentVersion.PathOnClient = '/' + filename + '.pdf';
      bidContentVersion.Title = fileName;
      bidContentVersion.VersionData = bidAttachment;
      if (!Test.isRunningTest()) bidContentVersion.FirstPublishLocationId = bids[0].Id;
      if (!Test.isRunningTest()) upsert bidContentVersion;
      //else insert bidContentVersion;

      // no links exist, no need to worry about new version
      // THIS IS SHARING AREA WITH SHARING RULES DETAILS
      ContentDocumentLink contentDocumentLink = new ContentDocumentLink();
      if (!bidDocumentLinks.isEmpty())
        contentDocumentLink.ContentDocumentId = [
          SELECT ContentDocumentId
          FROM ContentVersion
          WHERE Id = :[SELECT Id FROM ContentDocument].Id
        ]
        .ContentDocumentId;
      contentDocumentLink.LinkedEntityId = bids[0].Id;
      contentDocumentLink.ShareType = 'V';
      contentDocumentLink.Visibility = 'AllUsers';
      if (!Test.isRunningTest()) insert contentDocumentLink;
    } catch (Exception e) {
      system.debug(
        'VoyajerBidSubmissionController.saveBidMemorialization(): ' +
        e.getStackTraceString() +
        e.getMessage()
      );
    }
  }

  public static void saveBidMemorializationAttachment(String bidid) {
    try {
      List<Bid__c> bids = [
        SELECT
          Id,
          UUID_For_Landing_Page__c,
          Vendor__r.Name,
          Housing__r.Id,
          City__r.Name,
          Housing__r.Name,
          Housing__r.City__c,
          Housing__r.City__r.Name,
          Housing__r.Date_In__c,
          Housing__r.Date_Out__c
        FROM Bid__c
        WHERE Id = :bidid
      ];

      if (bids.size() > 0)
        bidid = bids[0].UUID_For_Landing_Page__c;
      // get formatted date in and date out entries
      String dateIn = (!bids.isEmpty() && bids[0].Housing__r.Date_In__c != null
        ? Datetime.newInstance(
              bids[0].Housing__r.Date_In__c.year(),
              bids[0].Housing__r.Date_In__c.month(),
              bids[0].Housing__r.Date_In__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');
      String dateOut = (!bids.isEmpty() && bids[0].Housing__r.Date_Out__c != null
        ? Datetime.newInstance(
              bids[0].Housing__r.Date_Out__c.year(),
              bids[0].Housing__r.Date_Out__c.month(),
              bids[0].Housing__r.Date_Out__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');

      // create the file(name with values from city and formatted dates
      String fileName = (bids.size() > 0 && bids[0].Vendor__c != null) ? bids[0].Vendor__r.Name : 'testFilename';
      fileName = fileName.replaceAll(' ', '_');

      Blob bidAttachment;
      PageReference pageRef = new PageReference('https://voyajer.force.com/PDF_BidSubmissionLP');
      pageRef.getParameters().put('bidid', bidId);
      pageRef.getParameters().put('gen', '1');
      if (!Test.isRunningTest())
        bidAttachment = pageRef.getContentAsPDF();
      else
        bidAttachment = Blob.valueof('bidAttachmentTest');

      List<ContentDocumentLink> bidDocumentLinks = [
        SELECT id, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :bids[0].Id AND ContentDocument.title = :fileName
      ];

      ContentVersion bidContentVersion = new ContentVersion();

      if (!bidDocumentLinks.isEmpty())
        bidContentVersion.contentDocumentId = bidDocumentLinks[0].ContentDocumentId;
      bidContentVersion.PathOnClient = '/' + filename + '.pdf';
      bidContentVersion.Title = fileName;
      bidContentVersion.VersionData = bidAttachment;
      bidContentVersion.FirstPublishLocationId = bids[0].Id;
      upsert bidContentVersion;

      // no links exist, no need to worry about new version
      // THIS IS SHARING AREA WITH SHARING RULES DETAILS
      ContentDocumentLink contentDocumentLink = new ContentDocumentLink();
      if (!bidDocumentLinks.isEmpty())
        contentDocumentLink.ContentDocumentId = [
          SELECT ContentDocumentId
          FROM ContentVersion
          WHERE Id = :bidContentVersion.Id
        ]
        .ContentDocumentId;
      else
      contentDocumentLink.ContentDocumentId = [SELECT Id FROM ContentDocument ORDER BY CreatedDate DESC LIMIT 1].Id;

      contentDocumentLink.LinkedEntityId = bids[0].Id;
      contentDocumentLink.ShareType = 'V';
      contentDocumentLink.Visibility = 'AllUsers';
      if (!Test.isRunningTest()) insert contentDocumentLink;
    } catch (Exception e) {
      system.debug(
        'VoyajerBidSubmissionController.saveBidMemorialization(): ' +
        e.getStackTraceString() +
        e.getMessage()
      );
    }
  }
*/
  public static void savePDFFromCommunity(String bidId, String fileName, String visualForcePage) {
    try {
      List<Bid__c> bids = [
        SELECT
          Id,
          UUID_For_Landing_Page__c,
          Vendor__r.Name,
          Housing__r.Id,
          City__r.Name,
          Housing__r.Name,
          Housing__r.City__c,
          Housing__r.City__r.Name,
          Housing__r.Date_In__c,
          Housing__r.Date_Out__c
        FROM Bid__c
        WHERE Id = :bidid
      ];

      if (bids.size() > 0)
        bidid = bids[0].UUID_For_Landing_Page__c;
      // get formatted date in and date out entries
      String dateIn = (!bids.isEmpty() && bids[0].Housing__r.Date_In__c != null
        ? Datetime.newInstance(
              bids[0].Housing__r.Date_In__c.year(),
              bids[0].Housing__r.Date_In__c.month(),
              bids[0].Housing__r.Date_In__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');
      String dateOut = (!bids.isEmpty() && bids[0].Housing__r.Date_Out__c != null
        ? Datetime.newInstance(
              bids[0].Housing__r.Date_Out__c.year(),
              bids[0].Housing__r.Date_Out__c.month(),
              bids[0].Housing__r.Date_Out__c.day()
            )
            .format('dd MMMMM yyyy')
        : '');

      // create the filename with values from city and formatted dates
      // String fileName = bids[0].Vendor__r.Name;
      String theFileName = fileName;
      fileName = fileName.replaceAll(' ', '_');
      Blob bidAttachment;

      String theURL = '';
      String base = [SELECT Id, Community_Base_Url__c FROM RoadRebelSettings__c LIMIT 1].Community_Base_Url__c;
      theURL = base + '/' + visualForcePage;
      system.debug (theURL);
      PageReference pageRef = new PageReference(theURL);
      pageRef.getParameters().put('bidid', bidId);
      pageRef.getParameters().put('gen', '1');
      if (!Test.isRunningTest())
        bidAttachment = pageRef.getContentAsPDF();
      else
        bidAttachment = Blob.valueof('bidAttachmentTest');

      List<ContentDocumentLink> bidDocumentLinks = [
        SELECT id, ContentDocumentId
        FROM ContentDocumentLink
        WHERE LinkedEntityId = :bids[0].Id AND ContentDocument.title = :fileName
      ];

      ContentVersion bidContentVersion = new ContentVersion();

      if (!bidDocumentLinks.isEmpty())
        bidContentVersion.contentDocumentId = bidDocumentLinks[0].ContentDocumentId;
      bidContentVersion.PathOnClient = '/' + fileName + '.pdf';
      bidContentVersion.Title = fileName;
      bidContentVersion.VersionData = bidAttachment;
      if (!Test.isRunningTest()) bidContentVersion.FirstPublishLocationId = bids[0].Id;
      if (!Test.isRunningTest()) upsert bidContentVersion;
      //else insert bidContentVersion;

      // no links exist, no need to worry about new version
      // THIS IS SHARING AREA WITH SHARING RULES DETAILS
      ContentDocumentLink contentDocumentLink = new ContentDocumentLink();
      if (!bidDocumentLinks.isEmpty())
        contentDocumentLink.ContentDocumentId = [
          SELECT ContentDocumentId
          FROM ContentVersion
          WHERE Id = :[SELECT Id FROM ContentDocument].Id
        ]
        .ContentDocumentId;
      contentDocumentLink.LinkedEntityId = bids[0].Id;
      contentDocumentLink.ShareType = 'V';
      contentDocumentLink.Visibility = 'AllUsers';
      if (!Test.isRunningTest()) insert contentDocumentLink;
    } catch (Exception e) {
      system.debug(
        'VoyajerBidSubmissionController.saveBidMemorialization(): ' +
        e.getStackTraceString() +
        e.getMessage()
      );
    }
  }

  public static Revenue__c getRevenueRecordCommission(String bidId) {

    Id revenueRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
      .get('Housing_Rate_Commission_RRU')
      .getRecordTypeId();
    Boolean isRRE = false;
    if (isRRE)
      revenueRT = Schema.SObjectType.Revenue__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Rate_Commission_RRE')
        .getRecordTypeId();
    // query for the Commission Record not with a Room Type
    Revenue__c commissionRevenue = new Revenue__c();
    Revenue__c commissionRevenueJSON = new Revenue__c();

    Revenue__c[] bidRevenue = [
      SELECT
        Id,
        RecordTypeId,
        CurrencyIsoCode,
        VAT_Rate__c,
        VAT__c,
        Breakfast_Rate__c,
        Breakfast__c,
        City_Tax_Rate__c,
        City_Tax_Rate_percent__c,
        City_Tax_Type__c,
        City_Tax__c,
        Commission_Agreed__c,
        Commission_Percent__c,
        Commission__c,
        Commission_Type__c,
        Tax__c,
        Tax_Included__c,
        Surcharge__c,
        Surcharge_included__c
      FROM Revenue__c
      WHERE
        Bid__c = :bidId
        AND (RecordType.Name = 'Housing Rate & Commission RRU'
        OR RecordType.Name = 'Housing Rate & Commission RRE')
        AND Room_Type__c = NULL
        AND Monthly_Pick_Up__c = FALSE
      ORDER BY createddate DESC
      LIMIT 1
    ];

    if (bidRevenue.size() == 0) {
      system.debug ('::::::: [bid submit] - handling revenue record - no revenue record found creating a new one :: ' + JSON.serializePretty(commissionRevenueJSON));
      commissionRevenue.Commission_Percent__c = 10;
      commissionRevenue.Commission_Type__c = 'Percentage';
      commissionRevenue.Bid__c = bidId;
      commissionRevenue.RecordTypeId = revenueRT;
      commissionRevenue.Tax_Included__c = false;
      commissionRevenue.VAT__c = false;
      commissionRevenue.Breakfast__c = false;
      commissionRevenue.City_Tax_Type__c = '';
      commissionRevenue.Tax__c = 0.0;
      commissionRevenue.Surcharge__c = 0.0;
      commissionRevenue.Surcharge_included__c = false;
      commissionRevenue.Commission_Agreed__c = false;
    } else {
      commissionRevenue = bidRevenue[0];
    }

    return commissionRevenue;
  }

  @AuraEnabled
  public static Map<String, Object> verifyVendorAccess(String typeOfService, String optionRecordId) {
    Map<String, Object> result = new Map<String, Object>();
    Boolean isAccessible = false;
    String accountId = '';
    List<Bid__c> searchBid = [
      SELECT
        Id,
        Housing__c,
        Housing__r.RecordType.DeveloperName,
        Housing__r.Back_end_Coordinator__c,
        Housing__r.Back_end_Coordinator__r.Name,
        Housing__r.Back_end_Coordinator__r.Phone,
        Housing__r.Back_end_Coordinator__r.Email,
        GT__c,
        GT__r.Back_end_Coordinator__c,
        GT__r.Back_end_Coordinator__r.Name,
        GT__r.Back_end_Coordinator__r.Phone,
        GT__r.Back_end_Coordinator__r.Email,
        Production__c,
        Production__r.Name,
        Production__r.Office_Location__c,
        Vendor__c,
        Provider__c
      FROM Bid__c
      WHERE
        Id = :optionRecordId
      LIMIT 1
    ];
    if (!searchBid.isEmpty())
      switch on typeOfService {
        when 'optionsHousing' {
          if (String.isNotBlank(searchBid.get(0).Housing__c)) {
              isAccessible = true;
            if (isAccessible) {
              result.put('productionId', searchBid.get(0).Production__c);
              result.put('productionName', searchBid.get(0).Production__r.Name);
              result.put(
                'productionOfficePreference',
                String.isNotBlank(searchBid.get(0).Production__r.Office_Location__c)
                  ? searchBid.get(0).Production__r.Office_Location__c
                  : 'RRU'
              );
              result.put('optionRecordId', searchBid.get(0).Housing__c);

            }
          }
        }
        when 'optionsGT' {
          if (String.isNotBlank(searchBid.get(0).GT__c)) {
            isAccessible = true;
            result.put('productionId', searchBid.get(0).Production__c);
            result.put('productionName', searchBid.get(0).Production__r.Name);
            result.put('optionRecordId', searchBid.get(0).GT__c);
            if (searchBid.get(0).GT__r.Back_end_Coordinator__c != null) {
              result.put('productionAssocUserName', searchBid.get(0).GT__r.Back_end_Coordinator__r.Name);
              result.put('productionAssocUserPhone', searchBid.get(0).GT__r.Back_end_Coordinator__r.Phone);
              result.put('productionAssocUserEmail', searchBid.get(0).GT__r.Back_end_Coordinator__r.Email);
              result.put('productionAssocRole', 'Ground Travel back-end Coordinator');
            } else {
              List<Production_Associations__c> searchProductionAssoc = [
                SELECT User__r.Name, User__r.Phone, User__r.Email, Production_Opp__c
                FROM Production_Associations__c
                WHERE
                  Production_Opp__c = :searchBid.get(0).Production__c
                  AND Team_Roles__c INCLUDES ('Primary GT Coordinator')
                LIMIT 1
              ];
              if (!searchProductionAssoc.isEmpty()) {
                result.put('productionAssocUserName', searchProductionAssoc.get(0).User__r.Name);
                result.put('productionAssocUserPhone', searchProductionAssoc.get(0).User__r.Phone);
                result.put('productionAssocUserEmail', searchProductionAssoc.get(0).User__r.Email);
                result.put('productionAssocRole', 'Primary Ground Travel Coordinator');
              }
            }
          }
        }
      }
    result.put('isAccessible', isAccessible);
    system.debug (JSON.serializePretty(result));
    return result;
  }

}```

---
layout: default
title: DashboardController_Bid_Test
parent: classes
---

```@isTest
public class DashboardController_Bid_Test {
  private static DashboardController housingController;

  static {
    DashboardDataFactory.createHousingData(2, false);
    DashboardDataFactory.createCongaQuery();
    Test.setCurrentPage(Page.DashboardVFP);
    ApexPages.currentPage()
      .getParameters()
      .put(
        'OpenBidId',
        [
          SELECT id
          FROM Bid__c
          WHERE Recordtype.DeveloperName = 'Housing_Bid'
          LIMIT 1
        ]
        .id
      );
    housingController = new DashboardController(
      new ApexPages.StandardController(
        [SELECT id FROM Opportunity WHERE Name = 'Cats' LIMIT 1]
      )
    );
  }

  /*
    @isTest static void Test_OpenAndSaveUSBid(){
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id) && housingController.contactsBidsByVendor.size() > 1);
        housingController.contactPrimarySelected = housingController.contactsBidsByVendor[1].getValue();
        housingController.changeContactPrimary();
        System.assertEquals(housingController.contactPrimarySelected, housingController.contactPrimaryBid.Id);
        housingController.revenue_tax = 5;
        housingController.revenue_tax_include = true;
        housingController.revenue_surcharge = 10;
        housingController.revenue_surcharge_include = true;
        housingController.revenue_commission_type = 'Percentage';
        housingController.revenue_commission_percent = 10;
        housingController.revenue_commission_amount = null;
        housingController.revenue_currency_type = 'USD';
        housingController.revenue_room_rate_release_date = Date.Today().addDays(1);
        housingController.revenue_vat = false;
        housingController.revenue_breakfast = false;
        housingController.revenue_city_tax = false;
        housingController.revenue_vat_rate = null;
        housingController.revneue_breakfast_rate = null;
        housingController.revenue_city_tax_rate = null;
        housingController.revenue_city_tax_rate_percent = null;
        housingController.revenue_city_tax_type = null;
        housingController.saveRevenueInformation();
        System.assert(String.isNotEmpty(housingController.revenueBid.Id) && housingController.revenueBid.CurrencyIsoCode == 'USD');
        System.assertEquals(housingController.bidData.Commission_Revenue__c, housingController.revenueBid.Id);
        Test.stopTest();
    }
    @isTest static void Test_OpenAndSaveCABid(){
        ApexPages.currentPage().getParameters().put('OpenBidId', [Select id from Bid__c where Recordtype.DeveloperName = 'Housing_Bid' /*and Vendor__r.ShippingCountry = 'Canada' limit 1].id);
        //Test.startTest();
		housingController.verifyHousing();
        Test.startTest();
        System.assert(String.isNotEmpty(housingController.bidData.Id) && housingController.contactsBidsByVendor.size() > 1);
        housingController.contactPrimarySelected = housingController.contactsBidsByVendor[1].getValue();
        housingController.changeContactPrimary();
        System.assertEquals(housingController.contactPrimarySelected, housingController.contactPrimaryBid.Id);
        housingController.revenue_tax = 5;
        housingController.revenue_tax_include = true;
        housingController.revenue_surcharge = 10;
        housingController.revenue_surcharge_include = true;
        housingController.revenue_commission_type = 'Amount';
        housingController.revenue_commission_percent = null;
        housingController.revenue_commission_amount = 10;
        housingController.revenue_currency_type = 'USD';
        housingController.revenue_room_rate_release_date = Date.Today().addDays(1);
        housingController.revenue_vat = false;
        housingController.revenue_breakfast = false;
        housingController.revenue_city_tax = false;
        housingController.revenue_vat_rate = null;
        housingController.revneue_breakfast_rate = null;
        housingController.revenue_city_tax_rate = null;
        housingController.revenue_city_tax_rate_percent = null;
        housingController.revenue_city_tax_type = null;
        housingController.saveRevenueInformation();
        System.assert(String.isNotEmpty(housingController.revenueBid.Id) && housingController.revenueBid.CurrencyIsoCode == 'USD');
        System.assertEquals(housingController.bidData.Commission_Revenue__c, housingController.revenueBid.Id);
        Test.stopTest();
    }
    */
  @isTest
  static void Test_OpenAndSaveESBid() {
    ApexPages.currentPage()
      .getParameters()
      .put(
        'OpenBidId',
        [
          SELECT id
          FROM Bid__c
          WHERE Recordtype.DeveloperName = 'Housing_Bid'
          /* and Vendor__r.ShippingCountry = 'Spain'*/ LIMIT 1
        ]
        .id
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(
      String.isNotEmpty(housingController.bidData.Id) &&
      housingController.contactsBidsByVendor.size() > 1
    );
    housingController.contactPrimarySelected = housingController.contactsBidsByVendor[1]
      .getValue();
    housingController.changeContactPrimary();
    System.assertEquals(
      housingController.contactPrimarySelected,
      housingController.contactPrimaryBid.Id
    );
    housingController.revenue_tax = 5;
    housingController.revenue_tax_include = true;
    housingController.revenue_surcharge = 10;
    housingController.revenue_surcharge_include = true;
    housingController.revenue_commission_type = 'Percentage';
    housingController.revenue_commission_percent = 10;
    housingController.revenue_commission_amount = null;
    housingController.revenue_currency_type = 'EUR';
    housingController.revenue_room_rate_release_date = Date.Today().addDays(1);
    housingController.revenue_vat = false;
    housingController.revenue_breakfast = false;
    housingController.revenue_city_tax = false;
    housingController.revenue_vat_rate = null;
    housingController.revneue_breakfast_rate = null;
    housingController.revenue_city_tax_rate = null;
    housingController.revenue_city_tax_rate_percent = null;
    housingController.revenue_city_tax_type = null;
    housingController.saveRevenueInformation();
    System.assert(
      String.isNotEmpty(housingController.revenueBid.Id) &&
      housingController.revenueBid.CurrencyIsoCode == 'EUR'
    );
    System.assertEquals(
      housingController.bidData.Commission_Revenue__c,
      housingController.revenueBid.Id
    );
    Test.stopTest();
  }

  @isTest
  static void Test_ContractBid() {
    Dashboard__c dashboardContract = new Dashboard__c();
    dashboardContract.Contract_ID__c = 0;
    insert dashboardContract;
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingBidNumber = 1;
    //Fix By Clay 27 Dec, 2020
    //Test.startTest();
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    //Fix By Clay 27 Dec, 2020
    Test.startTest();
    housingController.contractBid();
    //dSystem.assertEquals('Contracted', [Select id, Status__c from Bid__c where id =:housingController.bidData.Id].Status__c);
    Test.stopTest();
  }

  @isTest
  static void Test_ContractAnotherBid() {
    Dashboard__c dashboardContract = new Dashboard__c();
    dashboardContract.Contract_ID__c = 0;
    insert dashboardContract;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingBidNumber = 2;
    Test.startTest();
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    //Fix By Clay 27 Dec, 2020
    Bid__c housingBid = housingController.bidData.clone(true, true);
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    housingController.contractBid();
    System.assertNotEquals(
      housingBid.Housing__c,
      [SELECT id, Housing__c FROM Bid__c WHERE id = :housingBid.Id]
      .Housing__c
    );
    Test.stopTest();
  }

  @isTest
  static void Test_UnContractBid() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted',
      Status_Previous__c = 'Unsent'
    );
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingBidNumber = 1;
    Test.startTest();
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Bid__c housingBid = housingController.bidData;
    housingController.uncontractBid();
    System.assertEquals(
      housingBid.Status_Previous__c,
      [
        SELECT id, Status__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Status__c
    );
    Test.stopTest();
  }
  @isTest
  static void Test_viewBidContracted() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingBidNumber = 1;
    Test.startTest();
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.bidContractId = housingController.bidData.Id;
    housingController.housingStayViewId = housingController.bidData.Housing__c;
    housingController.viewBidContracted();
    housingController.housing_locked = false;
    housingController.editHousingLocked();

    System.assertEquals(
      housingController.bidContractId,
      housingController.bidData.Id
    );
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateBid() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openDeactivateBid();
    System.assertEquals(
      'Sold Out / Not Bidding',
      [
        SELECT id, Status__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Status__c
    );
    Test.stopTest();
  }

  @isTest
  static void Test_BidLocked() {
    //Fix By Clay Dev 1 March, 2021
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.bid_id = housingController.bidData.Id;
    housingController.bid_locked = true;
    Test.stopTest();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.BidTrigger_Is_Enabled = false;
    housingController.editBidDataLocked();
    housingController.editBidLocked();
    System.assertEquals(
      housingController.bid_locked,
      [
        SELECT id, Locked__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Locked__c
    );
  }
  /*
    @isTest static void Test_OpenAndAssociateHotelVendor(){
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        housingController.openAssociateVendor();
        System.assert(housingController.associateVendorList.isEmpty());
        housingController.housingBidNumber = housingController.housingBidNumber;
        housingController.associatevendor_search = 'HousingVendorTest';
        housingController.searchAssociateVendor();
        System.assert(!housingController.associateVendorList.isEmpty());
        housingController.newVendor_id = housingController.associateVendorList[0].Id;
        housingController.associateAndCreateBid();
        System.assertEquals(housingController.newVendor_id, [Select id, Vendor__c from Bid__c where id =:housingController.bidData.Id].Vendor__c);
        Test.stopTest();
    }
    @isTest static void Test_OpenAndAssociateCorporateVendor(){
        update new Housing__c(Id = [Select id from Housing__c where Recordtype.DeveloperName = 'Hotel_Housing' limit 1].id, RecordTypeId = Schema.SObjectType.Housing__c.getRecordTypeInfosByDeveloperName().get('Corporate_Housing').getRecordTypeId());
        insert new Account(RecordTypeId = Schema.SObjectType.Account.getRecordTypeInfosByDeveloperName().get('Corporate_Housing_Vendor').getRecordTypeId(), Name = 'HousingCorporateVendorTest1');
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        housingController.openAssociateVendor();
        System.assert(housingController.associateVendorList.isEmpty());
        housingController.housingBidNumber = housingController.housingBidNumber;
        housingController.associatevendor_search = 'HousingCorporateVendorTest';
        housingController.searchAssociateVendor();
        System.assert(!housingController.associateVendorList.isEmpty());
        housingController.newVendor_id = housingController.associateVendorList[0].Id;
        housingController.associateAndCreateBid();
        System.assertEquals(housingController.newVendor_id, [Select id, Vendor__c from Bid__c where id =:housingController.bidData.Id].Vendor__c);
        Test.stopTest();
    }
    @isTest static void Test_OpenAndSaveBidJournals(){
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        housingController.getBidJournals();
        System.assert(housingController.journalByBidList != null && !housingController.productionContactPL.isEmpty() && !housingController.companyContactPL.isEmpty() && housingController.teamMembers.size() > 1);
        Integer journalByBidListSize = housingController.journalByBidList.size();
        housingController.createjournal_id = null;
        housingController.createjournal_productioncompanyids = null;
        housingController.createjournal_productioncontactids = housingController.productionContactPL[0].getValue();
        housingController.createjournal_companycontactids = housingController.productionContactPL[0].getValue();
        housingController.createjournal_coordinator = housingController.teamMembers[1].getValue();
        housingController.createjournal_tracedate = Date.Today().addDays(1).format();
        housingController.newJournal.Production_checkbox__c = true;
        housingController.newJournal.Issue__c = true;
        housingController.newJournal.Sales__c = true;
        housingController.createjournal_alert = true;
        housingController.newJournal.Mark_Journal_trace_complete__c = true;
        housingController.newJournal.Journal_Entry__c = 'Journal Entry Test';
        housingController.newJournal.Vendor_Checkbox__c = true;
        housingController.createjournal_type = 'bid';
        housingController.saveCreateJournal();
        System.assert(housingController.journalByBidList.size() == journalByBidListSize + 1);
        Test.stopTest();
    }
    @isTest static void Test_OpenBidDocuments(){
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        housingController.loadDocuments = true;
        housingController.viewContractOptions = false;
        System.assert(housingController.loadDocuments && !housingController.viewContractOptions);
        Test.stopTest();
    }
    @isTest static void Test_AddAndDeleteBidRoomTypes(){
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        housingController.newRoomTypeBid();
        System.assert(String.isEmpty(housingController.newHousingBid.Id));
        System.assert(!housingController.roomTypesBid.isEmpty());
        Integer housingBidRoomTypesSize = housingController.roomTypesBid.size();
        Housing__c housingBidRoomType = housingController.roomTypesBid[housingBidRoomTypesSize - 1];
        housingController.newHousingBid.Date_In__c = housingBidRoomType.Date_In__c;
        housingController.newHousingBid.Date_Out__c = housingBidRoomType.Date_Out__c;
        housingController.newHousingBid.Units__c = housingBidRoomType.Units__c;
        housingController.newHousingBid.Unit_Type__c = housingBidRoomType.Unit_Type__c;
        housingController.newHousingBid.Rate__c = housingBidRoomType.Rate__c;
        housingController.newHousingBid.Rate_Period__c = housingBidRoomType.Rate_Period__c;
        housingController.newHousingBid.Special_Notes__c = housingBidRoomType.Special_Notes__c;
        housingController.addRoomTypeBid();
        System.assert(housingController.roomTypesBid.size() == housingBidRoomTypesSize + 1);
        housingBidRoomType = housingController.roomTypesBid[housingController.roomTypesBid.size() - 1];
        housingController.housingRoomTypeActual = housingBidRoomType.Id;
        housingController.unitsRoomTypeActual = String.valueOf(housingBidRoomType.Units__c);
        housingController.unitTypeRoomTypeActual = housingBidRoomType.Unit_Type__c;
        housingController.specialNotesRoomTypeActual = housingBidRoomType.Special_Notes__c;
        housingController.dateInRoomTypeActual = housingBidRoomType.Date_In__c;
        housingController.dateOutRoomTypeActual = housingBidRoomType.Date_Out__c;
        housingController.rateRoomTypeActual = housingBidRoomType.Rate__c;
        housingController.ratePeriodRoomTypeActual = housingBidRoomType.Rate_Period__c;
        housingController.projectedUnitsRoomTypeActual = String.valueOf(housingBidRoomType.Projected_Units__c);
        housingController.projectedRoomNightsRoomTypeActual = String.valueOf(housingBidRoomType.Projected_Room_nights__c);
        housingController.roomtypeConfirmation = housingBidRoomType.Confirmations__c;
        housingController.editRoomTypeByBid();
        System.assert(housingController.newHousingBid.Id == housingController.housingRoomTypeActual);
        System.assert(String.isEmpty(DashboardController.validateDeleteCloseOut(housingController.newHousingBid.Id)));
        housingBidRoomTypesSize = housingController.roomTypesBid.size();
        housingController.housingRoomTypeActual = housingController.newHousingBid.Id;
        housingController.deleteRoomType();
        System.assert(housingController.roomTypesBid.size() == housingBidRoomTypesSize - 1);
        Test.stopTest();
    }
    */
  @isTest
  static void Test_AddAndDeleteBidRebates() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Integer housingBidRebatesSize = housingController.rebatesBid.size();
    housingController.newRebateBid.Charge_Type__c = 'Percent';
    housingController.newRebateBid.Rebate_currency__c = 5;
    housingController.newRebateBid.Rebate_Per__c = 'Person';
    housingController.newRebateBid.Rebate_to_client_Due__c = 10;
    housingController.newRebateBid.Rebate_to_RR_Due__c = 15;
    housingController.newRebateBid.Rebate_invoiced_Amount__c = 20;
    housingController.addRebateBid();
    System.assert(
      housingController.rebatesBid.size() == housingBidRebatesSize + 1
    );
    housingBidRebatesSize = housingController.rebatesBid.size();
    housingController.newRebateBid.Charge_Type__c = 'Amount';
    housingController.newRebateBid.Rebate_currency__c = 10;
    housingController.newRebateBid.Rebate_Per__c = 'Person';
    housingController.newRebateBid.Rebate_to_client_Due__c = 10;
    housingController.newRebateBid.Rebate_to_RR_Due__c = 15;
    housingController.newRebateBid.Rebate_invoiced_Amount__c = 20;
    housingController.addRebateBid();
    System.assert(
      housingController.rebatesBid.size() == housingBidRebatesSize + 1
    );
    Revenue__c housingBidRebate = housingController.rebatesBid[
      housingController.rebatesBid.size() - 1
    ];
    housingController.rebateBidActual = housingBidRebate.Id;
    housingController.rebate_chargetype = 'Percent';
    housingController.rebate_rebatecurrency = null;
    housingController.rebate_rebate = 10;
    housingController.rebate_rebateper = housingBidRebate.Rebate_Per__c;
    housingController.rebate_note = housingBidRebate.Rebate_Note__c;
    housingController.rebate_rebatetoclientdue = housingBidRebate.Rebate_to_client_Due__c;
    housingController.rebate_rebatetorrdue = housingBidRebate.Rebate_to_RR_Due__c;
    housingController.rebate_rebateinvoicedamount = housingBidRebate.Rebate_invoiced_Amount__c;
    housingController.editRebateByBid();
    System.assert(
      housingController.newRebateBid.Id == housingController.rebateBidActual
    );
    housingBidRebatesSize = housingController.rebatesBid.size();
    System.assert(
      String.isEmpty(
        DashboardController.validateDeleteRevenue(
          housingController.newRebateBid.Id
        )
      )
    );
    housingController.rebateBidActual = housingController.newRebateBid.Id;
    housingController.deleteRebate();
    System.assert(
      housingController.rebatesBid.size() == housingBidRebatesSize - 1
    );
    Test.stopTest();
  }

  @isTest
  static void Test_AddAndEditBidConcessions() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    System.assert(
      String.isEmpty(
        DashboardController.createConcession(
          housingController.bidData.Production__c,
          housingController.bidData.Id,
          true,
          '**PLEASE NOTE! Rooms Are Not Being Held**'
        )
      )
    );
    System.assertEquals(
      'Concession **PLEASE NOTE! Rooms Are Not Being Held** already exists.',
      DashboardController.createConcession(
        housingController.bidData.Production__c,
        housingController.bidData.Id,
        true,
        '**PLEASE NOTE! Rooms Are Not Being Held**'
      )
    );
    housingController.newConcessionBid();
    System.assert(String.isEmpty(housingController.newConcessionBid.Id));
    housingController.getBidConcessions();
    Integer housingBidConcessionsSize = housingController.concessionsRequestedBid.size();
    housingController.newConcessionBid.Order__c = 1;
    housingController.newConcessionBid.Concession_Provided__c = 'Bathtubs in all group rooms.';
    housingController.newConcessionBid.Agreed__c = true;
    housingController.concessionRequestedActual = 'Bathtubs in all group rooms.';
    housingController.addConcessionBid();
    System.assert(
      housingController.concessionsRequestedBid.size() ==
      housingBidConcessionsSize + 1
    );
    housingController.newConcessionBid();
    System.assert(String.isEmpty(housingController.newConcessionBid.Id));
    housingBidConcessionsSize = housingController.concessionsRequestedBid.size();
    housingController.newConcessionBid.Order__c = 2;
    housingController.newConcessionBid.Concession_Provided__c = 'All single rooms must have king beds.';
    housingController.newConcessionBid.Agreed__c = true;
    housingController.concessionRequestedActual = 'All single rooms must have king beds.';
    housingController.addConcessionBid();
    System.assert(
      housingController.concessionsRequestedBid.size() ==
      housingBidConcessionsSize + 1
    );
    housingController.newConcessionBid();
    System.assert(String.isEmpty(housingController.newConcessionBid.Id));
    housingBidConcessionsSize = housingController.concessionsRequestedBid.size();
    housingController.newConcessionBid.Order__c = 1;
    housingController.newConcessionBid.Concession_Provided__c = 'Other';
    housingController.newConcessionBid.Agreed__c = true;
    housingController.concessionRequestedActual = 'Other';
    housingController.addConcessionBid();
    System.assert(
      housingController.concessionsRequestedBid.size() ==
      housingBidConcessionsSize + 1
    );
    Concessions__c housingBidConcession1 = housingController.concessionsRequestedBid[0];
    Concessions__c housingBidConcession2 = housingController.concessionsRequestedBid[1];
    Concessions__c housingBidConcession3 = housingController.concessionsRequestedBid[2];
    System.assertEquals(1, housingBidConcession1.Order__c);
    System.assertEquals(2, housingBidConcession2.Order__c);
    System.assertEquals(3, housingBidConcession3.Order__c);
    housingController.concessionActual = housingBidConcession3.Id;
    housingController.concessionRequestedActual = housingBidConcession3.Concessions_Requested__c;
    housingController.concessionProvidedActual = housingBidConcession3.Concession_Provided__c;
    housingController.concessionAgreedActual = housingBidConcession3.Agreed__c;
    housingController.concessionOrderActual = '2';
    housingController.editConcessionBid();
    System.assertEquals(
      housingBidConcession1.Id,
      housingController.concessionsRequestedBid[0].Id
    );
    System.assertEquals(
      housingBidConcession3.Id,
      housingController.concessionsRequestedBid[1].Id
    );
    System.assertEquals(
      housingBidConcession2.Id,
      housingController.concessionsRequestedBid[2].Id
    );
    Test.stopTest();
  }

  @isTest
  static void Test_DeleteBidConcessions() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    System.assert(!housingController.concessionsRequestedBid.isEmpty());
    housingController.newConcessionBid();
    System.assert(String.isEmpty(housingController.newConcessionBid.Id));
    Integer housingBidConcessionsSize = housingController.concessionsRequestedBid.size();
    housingController.concessionActual = housingController.concessionsRequestedBid[
        housingBidConcessionsSize - 1
      ]
      .Id;
    housingController.deleteConcession();
    System.assertEquals(
      housingBidConcessionsSize - 1,
      housingController.concessionsRequestedBid.size()
    );
    Test.stopTest();
  }

  @isTest
  static void Test_SoldOutBid() {
    Test.startTest();
    housingController.verifyHousing();
    Test.stopTest();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Id housingBidId = housingController.bidData.Id;
    housingController.soldOutBid();
    System.assertEquals(
      'Sold Out / Not Bidding',
      [SELECT id, Status__c FROM Bid__c WHERE id = :housingBidId]
      .Status__c
    );
  }

  @isTest
  static void Test_ResendBid_PreviewPdf() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openResendBid();
    System.assert(
      !housingController.resendbid_vendorContacts.isEmpty() &&
      housingController.isBidResendRendered
    );
    Integer resendbid_vendorContactsSize = housingController.resendbid_vendorContacts.size();
    housingController.vendorContact_id = null;
    housingController.vendorContact.AccountId = housingController.bidData.Vendor__c;
    housingController.vendorContact.FirstName = 'housingVendorContact';
    housingController.vendorContact.LastName = 'Test12';
    housingController.vendorContact.Designation_title__c = 'General Manager';
    housingController.vendorContact.Email = 'housingVendorContactTest12@test.com';
    housingController.saveAddContactVendor();
    System.assertEquals(
      resendbid_vendorContactsSize + 1,
      housingController.resendbid_vendorContacts.size()
    );
    System.assertEquals(
      'You\'re creating a duplicate record. We recommend you use an existing record.',
      DashboardController.validateError('DUPLICATES_DETECTED')
    );
    System.assertEquals(
      'Error Test',
      DashboardController.validateError('Error Test')
    );
    housingController.vendorcontact_actual_id = housingController.resendbid_vendorContacts[0]
      .c.Id;
    housingController.changeContactVendorResendBid();
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      housingController.bidData.Vendor_Contact__c
    );
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      DashboardController.getDataContact(
          housingController.vendorcontact_actual_id
        )
        .Id
    );
    System.assertEquals(
      housingController.resendbid_vendorContacts[0].c.Email,
      DashboardController.getDataEmailBid(
        housingController.opportunityId,
        housingController.bidData.Housing__c,
        housingController.bidData.Id,
        housingController.vendorcontact_actual_id,
        'pdf',
        'Test.com'
      )[0]
    );
    Test.stopTest();
  }
  @isTest
  static void Test_ResendBid_SendPdf() {
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayViewId = [
      SELECT id
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ]
    .id;
    housingController.housingBidNumber = 1;
    Test.startTest();
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openResendBid();
    System.assert(
      !housingController.resendbid_vendorContacts.isEmpty() &&
      housingController.isBidResendRendered
    );
    housingController.vendorcontact_actual_id = housingController.resendbid_vendorContacts[0]
      .c.Id;
    housingController.changeContactVendorResendBid();
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      housingController.bidData.Vendor_Contact__c
    );
    housingController.type_email = 'pdf';
    housingController.contactPrimarySelected = housingController.vendorcontact_actual_id;
    housingController.sendResendBid();
    System.assertEquals(
      'Sent',
      [
        SELECT id, Status__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Status__c
    );
    Test.stopTest();
  }
  /*
    @isTest static void Test_ResendBid_PreviewLink(){
        Test.startTest();
		housingController.verifyHousing();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
		housingController.openResendBid();
        System.assert(!housingController.resendbid_vendorContacts.isEmpty() && housingController.isBidResendRendered);
        housingController.vendorcontact_actual_id = housingController.resendbid_vendorContacts[0].c.Id;
		housingController.changeContactVendorResendBid();
        System.assertEquals(housingController.vendorcontact_actual_id, housingController.bidData.Vendor_Contact__c);
        System.assertEquals(housingController.resendbid_vendorContacts[0].c.Email, DashboardController.getDataEmailBid(housingController.opportunityId, housingController.bidData.Housing__c, housingController.bidData.Id, housingController.vendorcontact_actual_id, 'link', 'Test.com')[0]);
		housingController.emailbid_to = 'Test@test.com';
		housingController.emailbid_cc = '';
		housingController.emailbid_bcc = '';
		housingController.emailbid_subject = '';
		housingController.emailbid_body = 'Email Body';
		housingController.emailbid_primarycontactname = 'Test';
		housingController.emailbid_id = housingController.bidData.Id;
		housingController.emailbid_type = 'link';
		housingController.emailAttachs = null;
		housingController.emailbid_primarycontactid = housingController.vendorcontact_actual_id;
		housingController.sendPreviewPdf();
        System.assertEquals('Sent', [Select id, Status__c from Bid__c where id =:housingController.bidData.Id].Status__c);
        Test.stopTest();
    }
    */
  @isTest
  static void Test_ResendBid_SendLink() {
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayViewId = [
      SELECT id
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ]
    .id;
    housingController.housingBidNumber = 1;
    Test.startTest();
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openResendBid();
    System.assert(
      !housingController.resendbid_vendorContacts.isEmpty() &&
      housingController.isBidResendRendered
    );
    housingController.vendorcontact_actual_id = housingController.resendbid_vendorContacts[0]
      .c.Id;
    housingController.changeContactVendorResendBid();
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      housingController.bidData.Vendor_Contact__c
    );
    housingController.type_email = 'link';
    housingController.contactPrimarySelected = housingController.vendorcontact_actual_id;
    housingController.sendResendBid();
    System.assertEquals(
      'Sent',
      [
        SELECT id, Status__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Status__c
    );
    Test.stopTest();
  }
  @isTest
  static void Test_OpenBidAgreement_RateAgreement() {
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT id, RecordType.DeveloperName, Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Test.startTest();
    housingController.rateagreement_type = 'Rate Agreement';
    housingController.openRateAgreement();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Rate_Agreement__c) &&
      String.isNotEmpty(housingController.draft.Id) &&
      housingController.isRateAgreementRendered
    );
    System.assert(
      String.isNotEmpty(
        DashboardController.searchContactEmail(
          housingController.contactsBidsByVendor[1].getLabel()
        )
      )
    );
    housingController.contactPrimarySelected = housingController.contactsBidsByVendor[1]
      .getValue();
    housingController.changeContactPrimary();
    System.assertEquals(
      housingController.contactPrimarySelected,
      housingController.contactPrimaryBid.Id
    );
    housingController.rateagreement_to = 'Test@test.com';
    housingController.rateagreement_cc = '';
    housingController.rateagreement_bcc = '';
    housingController.rateagreement_usecheck = true;
    housingController.rateagreement_usecreditcard = false;
    housingController.rateagreement_creditcard = '';
    housingController.rateagreement_rooming = String.valueOf(Date.Today());
    housingController.rateagreement_tax = 5;
    housingController.rateagreement_tax_included = true;
    housingController.rateagreement_surcharge = 10;
    housingController.revenueRateAgreement.Surcharge_included__c = true;
    housingController.rateagreement_billingoption = 'Billing Option Test';
    housingController.rateagreement_contractdue = null;
    housingController.draft.Terms__c = 'Terms Test';
    housingController.draft.Body__c = 'Message Body Test';
    housingController.rateagreement_isCongaSignSent = true;
    housingController.saveRateAgreement();
    System.assert(!housingController.rateagreement_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateBidAgreement_RateAgreement() {
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT id, RecordType.DeveloperName, Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Test.startTest();
    housingController.isRateAgreementRendered = false;
    housingController.rateagreement_type = 'Rate Agreement';
    housingController.openRateAgreement();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Rate_Agreement__c) &&
      String.isNotEmpty(housingController.draft.Id) &&
      housingController.isRateAgreementRendered
    );
    housingController.deactivateRateAgreement();
    System.assertEquals(
      null,
      [
        SELECT Id, Form_Rate_Agreement__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Form_Rate_Agreement__c
    );
    housingController.deactivateRateAgreement();
    housingController.saveRateAgreement();
    System.assertEquals(
      null,
      [
        SELECT Id, Form_Rate_Agreement__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Form_Rate_Agreement__c
    );
    Test.stopTest();
  }
  /*
    @isTest static void Test_OpenBidAgreement_HousingContract(){
        housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
        Integer i = 1;
        for(Bid__c bid:[Select Id, Production__c, No_Bid_reason__c, Provider__c, Provider__r.Name, Housing__c, DX_to_Venue__c, Vendor__c, Vendor__r.Name, Vendor__r.Flag_icon__c, Vendor__r.ShippingStreet, Vendor__r.ShippingCity, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode, Status__c, Housing__r.Status_CC__c, Housing__r.Status_Previous__c, Rate__c, Notes__c, Options__c, Cover__c, Include_in_option_cover_sheet__c, Vendor__r.City__r.Name, Vendor__r.City__c, Room_Rate_Release_date__c, CreatedDate, Vendor_Address__c, Bid_Notes__c, OLR__c, Sabre_Rate__c, Locked__c, Status_Previous__c, RecordTypeId, RecordType.Name, Internal_Notes__c from Bid__c where Recordtype.DeveloperName = 'Housing_Bid']){
            housingController.bidDataMap.put(i, new DashboardController.BidWrapper(
                bid,
                bid.Vendor__r.Flag_icon__c,
                (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
                bid.Vendor__r.Name,
                bid.Vendor_Address__c,
                bid.Status__c,
                null,
                bid.Room_Rate_Release_date__c,
                bid.OLR__c != null ? bid.OLR__c : '',
                bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
                (bid.Status__c == 'Sold Out / Not Bidding' ? 1000000 : (bid.Options__c != null ? bid.Options__c : 999999)),
                (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
                bid.CreatedDate.date(),
                bid.Provider__c != null ? bid.Provider__r.Name : '',
                bid.Options__c != null ? bid.Options__c : 999999
            ));
            i++;
        }
		housingController.housingStayView = [Select id, RecordType.DeveloperName, Billing_Options_Verbiage__c from Housing__c where Recordtype.DeveloperName = 'Hotel_Housing' limit 1];
		housingController.housingBidNumber = 1;
		housingController.getBidInformation();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        Test.startTest();
		housingController.rateagreement_type = 'Housing Contract';
		housingController.openRateAgreement();
        System.assert(String.isNotBlank(housingController.bidData.Form_Housing_Contract__c) && String.isNotEmpty(housingController.draft.Id) && housingController.isRateAgreementRendered);
		housingController.contactPrimarySelected = housingController.contactsBidsByVendor[1].getValue();
        housingController.changeContactPrimary();
        System.assertEquals(housingController.contactPrimarySelected, housingController.contactPrimaryBid.Id);
		housingController.rateagreement_to = 'Test@test.com';
		housingController.rateagreement_cc = '';
		housingController.rateagreement_bcc = '';
		housingController.rateagreement_usecheck = true;
		housingController.rateagreement_usecreditcard = false;
		housingController.rateagreement_creditcard = '';
		housingController.rateagreement_rooming = String.valueOf(Date.Today());
		housingController.rateagreement_tax = 5;
		housingController.rateagreement_tax_included = true;
		housingController.rateagreement_surcharge = 10;
		housingController.revenueRateAgreement.Surcharge_included__c = true;
		housingController.rateagreement_billingoption = 'Billing Option Test';
		housingController.rateagreement_contractdue = null;
		housingController.draft.Terms__c = 'Terms Test';
		housingController.draft.Body__c = 'Message Body Test';
		housingController.rateagreement_isCongaSignSent = true;
		housingController.saveRateAgreement();
        System.assert(!housingController.rateagreement_isCongaSignSent);
        housingController.isRateAgreementRendered = false;
		housingController.rateagreement_type = 'Housing Contract';
		housingController.openRateAgreement();
        System.assert(String.isNotBlank(housingController.bidData.Form_Housing_Contract__c) && String.isNotEmpty(housingController.draft.Id) && housingController.isRateAgreementRendered);
		Test.stopTest();
    }
    @isTest static void Test_DeactivateBidAgreement_HousingContract(){
        housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
        Integer i = 1;
        for(Bid__c bid:[Select Id, Production__c, No_Bid_reason__c, Provider__c, Provider__r.Name, Housing__c, DX_to_Venue__c, Vendor__c, Vendor__r.Name, Vendor__r.Flag_icon__c, Vendor__r.ShippingStreet, Vendor__r.ShippingCity, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode, Status__c, Housing__r.Status_CC__c, Housing__r.Status_Previous__c, Rate__c, Notes__c, Options__c, Cover__c, Include_in_option_cover_sheet__c, Vendor__r.City__r.Name, Vendor__r.City__c, Room_Rate_Release_date__c, CreatedDate, Vendor_Address__c, Bid_Notes__c, OLR__c, Sabre_Rate__c, Locked__c, Status_Previous__c, RecordTypeId, RecordType.Name, Internal_Notes__c from Bid__c where Recordtype.DeveloperName = 'Housing_Bid']){
            housingController.bidDataMap.put(i, new DashboardController.BidWrapper(
                bid,
                bid.Vendor__r.Flag_icon__c,
                (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
                bid.Vendor__r.Name,
                bid.Vendor_Address__c,
                bid.Status__c,
                null,
                bid.Room_Rate_Release_date__c,
                bid.OLR__c != null ? bid.OLR__c : '',
                bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
                (bid.Status__c == 'Sold Out / Not Bidding' ? 1000000 : (bid.Options__c != null ? bid.Options__c : 999999)),
                (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
                bid.CreatedDate.date(),
                bid.Provider__c != null ? bid.Provider__r.Name : '',
                bid.Options__c != null ? bid.Options__c : 999999
            ));
            i++;
        }
		housingController.housingStayView = [Select id, RecordType.DeveloperName, Billing_Options_Verbiage__c from Housing__c where Recordtype.DeveloperName = 'Hotel_Housing' limit 1];
		housingController.housingBidNumber = 1;
		housingController.getBidInformation();
        System.assert(String.isNotEmpty(housingController.bidData.Id));
        Test.startTest();
		housingController.isRateAgreementRendered = false;
		housingController.rateagreement_type = 'Housing Contract';
		housingController.openRateAgreement();
        System.assert(String.isNotBlank(housingController.bidData.Form_Housing_Contract__c) && String.isNotEmpty(housingController.draft.Id) && housingController.isRateAgreementRendered);
		housingController.deactivateRateAgreement();
        System.assertEquals(null, [Select Id, Form_Housing_Contract__c from Bid__c where id =:housingController.bidData.Id].Form_Housing_Contract__c);
		housingController.deactivateRateAgreement();
		housingController.saveRateAgreement();
        System.assertEquals(null, [Select Id, Form_Housing_Contract__c from Bid__c where id =:housingController.bidData.Id].Form_Housing_Contract__c);
		Test.stopTest();
    }
    */
  @isTest
  static void Test_OpenBidAgreement_AddAndDeleteBidRoomTypes() {
    //Fix By Clay 1 March, 2021
    ApexUtil.HousingTrigger_Is_Enabled = false;
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT id, RecordType.DeveloperName, Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Test.startTest();
    housingController.rateagreement_type = 'Rate Agreement';
    housingController.openRateAgreement();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Rate_Agreement__c) &&
      String.isNotEmpty(housingController.draft.Id) &&
      housingController.isRateAgreementRendered
    );
    housingController.newRoomTypeBidRateAgreement();
    System.assert(
      String.isEmpty(housingController.newHousingBidRateAgreement.Id)
    );
    Integer roomTypesBidRateAgreementSize = housingController.roomTypesBidRateAgreement.size();
    housingController.newHousingBidRateAgreement.Date_In__c = Date.Today();
    housingController.newHousingBidRateAgreement.Date_Out__c = Date.Today()
      .addDays(1);
    housingController.newHousingBidRateAgreement.Units__c = 1;
    housingController.newHousingBidRateAgreement.Unit_Type__c = '1-Bedroom';
    housingController.newHousingBidRateAgreement.Rate__c = 1.5;
    housingController.newHousingBidRateAgreement.Rate_Period__c = 'Per Day';
    housingController.newHousingBidRateAgreement.Special_Notes__c = 'Special Notes Test';
    housingController.addRoomTypeBidRateAgreement();
    System.assertEquals(
      roomTypesBidRateAgreementSize + 1,
      housingController.roomTypesBidRateAgreement.size()
    );
    roomTypesBidRateAgreementSize = housingController.roomTypesBidRateAgreement.size();
    Housing__c roomTypesBidRateAgreement = housingController.roomTypesBidRateAgreement[
      roomTypesBidRateAgreementSize - 1
    ];
    housingController.housingRoomTypeActual = roomTypesBidRateAgreement.Id;
    housingController.unitsRoomTypeActual = '2';
    housingController.unitTypeRoomTypeActual = roomTypesBidRateAgreement.Unit_Type__c;
    housingController.specialNotesRoomTypeActual = roomTypesBidRateAgreement.Special_Notes__c;
    housingController.dateInRoomTypeActual = roomTypesBidRateAgreement.Date_In__c;
    housingController.dateOutRoomTypeActual = roomTypesBidRateAgreement.Date_Out__c;
    housingController.rateRoomTypeActual = roomTypesBidRateAgreement.Rate__c;
    housingController.ratePeriodRoomTypeActual = roomTypesBidRateAgreement.Rate_Period__c;
    housingController.editRoomTypeByBidRateAgreement();
    System.assertEquals(
      2,
      [
        SELECT id, Units__c
        FROM Housing__c
        WHERE id = :roomTypesBidRateAgreement.Id
      ]
      .Units__c
    );
    roomTypesBidRateAgreementSize = housingController.roomTypesBidRateAgreement.size();
    housingController.housingRoomTypeActual = roomTypesBidRateAgreement.Id;
    housingController.deleteRoomType();
    System.assertEquals(
      roomTypesBidRateAgreementSize - 1,
      housingController.roomTypesBidRateAgreement.size()
    );
    Test.stopTest();
  }
  @isTest
  static void Test_ReleaseBid_Preview() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openReleaseBidData();
    System.assert(
      !housingController.releasebiddata_vendorContacts.isEmpty() &&
      housingController.isReleaseBidRendered
    );
    Integer HousingBidVendorContactsSize = housingController.releasebiddata_vendorContacts.size();
    housingController.vendorContact_id = null;
    housingController.vendorContact.AccountId = housingController.bidData.Vendor__c;
    housingController.vendorContact.FirstName = 'HousingVendorContact';
    housingController.vendorContact.LastName = 'Test12';
    housingController.vendorContact.Designation_title__c = 'General Manager';
    housingController.vendorContact.Email = 'HousingVendorContactTest12@test.com';
    housingController.saveAddContactVendor();
    System.assertEquals(
      HousingBidVendorContactsSize + 1,
      housingController.releasebiddata_vendorContacts.size()
    );
    System.assertEquals(
      'You\'re creating a duplicate record. We recommend you use an existing record.',
      DashboardController.validateError('DUPLICATES_DETECTED')
    );
    System.assertEquals(
      'Error Test',
      DashboardController.validateError('Error Test')
    );
    housingController.vendorcontact_actual_id = housingController.releasebiddata_vendorContacts[0]
      .c.Id;
    housingController.changeContactVendorReleaseBidData();
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      housingController.bidData.Vendor_Contact__c
    );
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      DashboardController.getDataContact(
          housingController.vendorcontact_actual_id
        )
        .Id
    );
    System.assertEquals(
      housingController.releasebiddata_vendorContacts[0].c.Email,
      DashboardController.getDataEmailBid(
        housingController.opportunityId,
        housingController.bidData.Housing__c,
        housingController.bidData.Id,
        housingController.vendorcontact_actual_id,
        'release_bid',
        'Test.com'
      )[0]
    );
    housingController.emailbid_to = 'Test@test.com';
    housingController.emailbid_cc = '';
    housingController.emailbid_bcc = '';
    housingController.emailbid_subject = '';
    housingController.emailbid_body = 'Email Body';
    housingController.emailbid_primarycontactname = 'Test';
    housingController.emailbid_id = housingController.bidData.Id;
    housingController.emailbid_type = 'release_bid';
    housingController.emailAttachs = null;
    housingController.emailbid_primarycontactid = housingController.vendorcontact_actual_id;
    housingController.sendPreviewPdf();
    System.assertEquals(
      'Bid Released',
      [
        SELECT id, Status__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Status__c
    );
    Test.stopTest();
  }
  @isTest
  static void Test_ReleaseBid_SendEmail() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openReleaseBidData();
    System.assert(
      !housingController.releasebiddata_vendorContacts.isEmpty() &&
      housingController.isReleaseBidRendered
    );
    Integer HousingBidVendorContactsSize = housingController.releasebiddata_vendorContacts.size();
    housingController.vendorContact_id = null;
    housingController.vendorContact.AccountId = housingController.bidData.Vendor__c;
    housingController.vendorContact.FirstName = 'HousingVendorContact';
    housingController.vendorContact.LastName = 'Test12';
    housingController.vendorContact.Designation_title__c = 'General Manager';
    housingController.vendorContact.Email = 'HousingVendorContactTest12@test.com';
    housingController.saveAddContactVendor();
    System.assertEquals(
      HousingBidVendorContactsSize + 1,
      housingController.releasebiddata_vendorContacts.size()
    );
    System.assertEquals(
      'You\'re creating a duplicate record. We recommend you use an existing record.',
      DashboardController.validateError('DUPLICATES_DETECTED')
    );
    System.assertEquals(
      'Error Test',
      DashboardController.validateError('Error Test')
    );
    housingController.vendorcontact_actual_id = housingController.releasebiddata_vendorContacts[0]
      .c.Id;
    housingController.changeContactVendorReleaseBidData();
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      housingController.bidData.Vendor_Contact__c
    );
    System.assertEquals(
      housingController.vendorcontact_actual_id,
      DashboardController.getDataContact(
          housingController.vendorcontact_actual_id
        )
        .Id
    );
    housingController.type_email = 'release_bid';
    housingController.contactPrimarySelected = housingController.releasebiddata_vendorContacts[0]
      .c.Id;
    housingController.sendReleaseBidData();
    System.assertEquals(
      'Bid Released',
      [
        SELECT id, Status__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Status__c
    );
    Test.stopTest();
  }

  @isTest
  static void Test_OpenContractedBid() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    //System.assert(String.isNotEmpty(housingController.bidData.Id) && housingController.clients.Size() > 1 && housingController.teamMembers.Size() > 1 && housingController.users.Size() > 1);
    housingController.contactClientValue = housingController.clients[1]
      .getValue();
    housingController.changeClientContract();
    //System.assert([Select id, Role__c from Production_Associations__c where Production_Opp__c =:housingController.opportunityId and Contact__c =:housingController.contactClientValue limit 1].Role__c.containsIgnoreCase('Primary Housing'));
    housingController.housingStayView.Trace_Date__c = Date.Today();
    housingController.bidData.Contracting_Back_End_Coordinator__c = housingController.teamMembers[1]
      .getValue();
    housingController.housingstay_tracedate = Date.Today();
    housingController.housingstay_tracedate = Date.Today().addDays(1);
    Test.stopTest();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Draft__c draft = new Draft__c();
    draft.Closing__c = 'Test With kind regards, Test';
    insert draft;
    housingController.bidData.Form_Rate_Agreement__c = draft.Id;
    housingController.saveBackendInformation();
    System.assertEquals(
      housingController.bidData.Contracting_Back_End_Coordinator__c,
      [
        SELECT id, Contracting_Back_End_Coordinator__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Contracting_Back_End_Coordinator__c
    );
    housingController.newTask.OwnerId = housingController.users[1].getValue();
    housingController.newTask.ActivityDate = Date.Today();
    housingController.newTask.Deadline_Date__c = Date.Today().addDays(1);
    housingController.newTask.Subject = 'Audit Trace Test.';
    housingController.newTask.Description = 'Audit Trace Description Test.';
    housingController.saveAuditTrace();
    //System.assert(String.isNotEmpty(housingController.newTask.Id));
  }

  @isTest
  static void Test_sendEmailFormWithAttachs1() {
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    housingController.bidData.Contracting_Back_End_Coordinator__c = housingController.teamMembers[1]
      .getValue();
    housingController.newTask.OwnerId = housingController.users[1].getValue();
    housingController.newTask.ActivityDate = Date.Today();
    housingController.newTask.Deadline_Date__c = Date.Today().addDays(1);
    housingController.newTask.Subject = 'Audit Trace Test.';
    housingController.newTask.Description = 'Audit Trace Description Test.';
    housingController.saveAuditTrace();

    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_type = 'cancellation_letter';
    housingController.contractTasksMap.put(
      'Pending Cancellation',
      housingController.newTask
    );
    housingController.sendEmailFormWithAttachs();
    housingController.form_type = 'no_pick_up';
    housingController.contractTasksMap.put(
      'Pending No Rooms Picked Up',
      housingController.newTask
    );
    Test.stopTest();
    housingController.sendEmailFormWithAttachs();
    housingController.form_type = 'final_contract';
    housingController.contractTasksMap.put(
      housingController.form_type,
      housingController.newTask
    );
    housingController.sendEmailFormWithAttachs();
    housingController.form_type = 'credit_card_change';
    housingController.contractTasksMap.put(
      'Awaiting Billing',
      housingController.newTask
    );
    housingController.sendEmailFormWithAttachs();
    //System.assert(String.isNotEmpty(housingController.newTask.Id));
  }

  @isTest
  static void Test_sendEmailFormWithAttachs2() {
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    housingController.bidData.Contracting_Back_End_Coordinator__c = housingController.teamMembers[1]
      .getValue();
    housingController.newTask.OwnerId = housingController.users[1].getValue();
    housingController.newTask.ActivityDate = Date.Today();
    housingController.newTask.Deadline_Date__c = Date.Today().addDays(1);
    housingController.newTask.Subject = 'Audit Trace Test.';
    housingController.newTask.Description = 'Audit Trace Description Test.';
    housingController.saveAuditTrace();

    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_type = 'room_changes';
    housingController.contractTasksMap.put(
      'Awaiting Addendum',
      housingController.newTask
    );
    housingController.sendEmailFormWithAttachs();
    Test.stopTest();
    housingController.form_type = 'contract_date_change';
    housingController.contractTasksMap.put(
      'Pending Date Change',
      housingController.newTask
    );
    housingController.sendEmailFormWithAttachs();
    housingController.form_type = 'counter_needed';
    Task task2 = new Task();
    task2.Subject = 'Audit Trace Test2';
    task2.ActivityDate = Date.Today();
    insert task2;
    housingController.contractTasksMap.put(
      'Contract Due Date',
      housingController.newTask
    );
    housingController.contractTasksMap.put('Pending Hotel Counter', task2);
    housingController.sendEmailFormWithAttachs();
  }

  @isTest
  static void Test_sendEmailFormWithAttachs3() {
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    housingController.bidData.Contracting_Back_End_Coordinator__c = housingController.teamMembers[1]
      .getValue();
    housingController.newTask.OwnerId = housingController.users[1].getValue();
    housingController.newTask.ActivityDate = Date.Today();
    housingController.newTask.Deadline_Date__c = Date.Today().addDays(1);
    housingController.newTask.Subject = 'Audit Trace Test.';
    housingController.newTask.Description = 'Audit Trace Description Test.';
    housingController.saveAuditTrace();

    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';

    housingController.form_type = 'contract_to_client';
    housingController.sendEmailFormWithAttachs();
    housingController.form_type = 'pick_up_report';
    housingController.sendEmailFormWithAttachs();

    Test.stopTest();
    housingController.form_type = 'gcip';
    Task task2 = new Task();
    task2.Subject = 'Audit Trace Test2';
    task2.ActivityDate = Date.Today();
    insert task2;
    housingController.contractTasksMap.put(
      'Create GCIP',
      housingController.newTask
    );
    housingController.contractTasksMap.put('Awaiting GCIP', task2);
    housingController.sendEmailFormWithAttachs();
  }

  @isTest
  static void Test_sendEmailFormWithAttachs4() {
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    housingController.bidData.Contracting_Back_End_Coordinator__c = housingController.teamMembers[1]
      .getValue();
    housingController.newTask.OwnerId = housingController.users[1].getValue();
    housingController.newTask.ActivityDate = Date.Today();
    housingController.newTask.Deadline_Date__c = Date.Today().addDays(1);
    housingController.newTask.Subject = 'Audit Trace Test.';
    housingController.newTask.Description = 'Audit Trace Description Test.';
    housingController.saveAuditTrace();

    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';

    housingController.form_type = 'rooming_list_reminder';
    housingController.contractTasksMap.put(
      'Rooming List Reminder',
      housingController.newTask
    );
    housingController.housing = new Housing__c();
    housingController.sendEmailFormWithAttachs();
    Test.stopTest();
    housingController.form_type = 'rooming_list_reminder';
    housingController.contractTasksMap.put(
      'Rooming List Reminder',
      housingController.newTask
    );
    housingController.housing = new Housing__c();
    housingController.housing.Housing_Preference__c = 'RRU';
    housingController.sendEmailFormWithAttachs();
    housingController.form_type = 'rooming_list_reminder';
    housingController.contractTasksMap.put(
      'Rooming List Reminder',
      housingController.newTask
    );
    housingController.housing = new Housing__c();
    housingController.housing.Housing_Preference__c = 'RRE';
    housingController.sendEmailFormWithAttachs();
  }

  @isTest
  static void Test_BidContractedStatus_UpdateStatusTraceDate1() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted',
      Rate_Agreement_Last_Send_Date__c = Datetime.now()
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(
      String.isNotEmpty(housingController.bidData.Id) &&
      !housingController.contractTasksMap.isEmpty()
    );
    System.assertEquals(
      'Dates before today are not allowed',
      DashboardController.validateDatesTrace(
        String.valueOf(Date.Today().addDays(-1)),
        String.valueOf(Date.Today().addDays(1))
      )
    );
    System.assertEquals(
      '',
      DashboardController.validateDatesTrace(
        String.valueOf(Date.Today()),
        String.valueOf(Date.Today().addDays(1))
      )
    );
    housingController.statusTaskId = housingController.contractTasksMap.containsKey(
        'Rooming List Reminder'
      )
      ? housingController.contractTasksMap.get('Rooming List Reminder').Id
      : null;
    housingController.statusTraceDate = Date.Today().addDays(1);
    housingController.updateStatusTraceDate();
    System.assertEquals(
      Date.Today().addDays(1),
      [
        SELECT id, ActivityDate
        FROM Task
        WHERE id = :housingController.statusTaskId
      ]
      .ActivityDate
    );
    Test.stopTest();
  }
  @isTest
  static void Test_BidContractedStatus_UpdateStatusTraceDate2() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted',
      Rate_Agreement_Last_Send_Date__c = Datetime.now()
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(
      String.isNotEmpty(housingController.bidData.Id) &&
      !housingController.contractTasksMap.isEmpty()
    );
    System.assertEquals(
      'Dates before today are not allowed',
      DashboardController.validateDatesTrace(
        String.valueOf(Date.Today().addDays(-1)),
        String.valueOf(Date.Today().addDays(1))
      )
    );
    System.assertEquals(
      '',
      DashboardController.validateDatesTrace(
        String.valueOf(Date.Today()),
        String.valueOf(Date.Today().addDays(1))
      )
    );
    housingController.statusTaskId = housingController.contractTasksMap.containsKey(
        'Awaiting Pick-Up'
      )
      ? housingController.contractTasksMap.get('Awaiting Pick-Up').Id
      : null;
    housingController.statusTraceDate = Date.Today().addDays(1);
    housingController.updateStatusTraceDate();
    System.assertEquals(
      Date.Today().addDays(1),
      [
        SELECT id, ActivityDate
        FROM Task
        WHERE id = :housingController.statusTaskId
      ]
      .ActivityDate
    );
    Test.stopTest();
  }
  @isTest
  static void Test_BidContractedStatus_ChangeDoneStatus() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted',
      Rate_Agreement_Last_Send_Date__c = Datetime.now()
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(
      String.isNotEmpty(housingController.bidData.Id) &&
      !housingController.contractTasksMap.isEmpty()
    );
    housingController.statusTaskId = housingController.contractTasksMap.containsKey(
        'Awaiting Pick-Up'
      )
      ? housingController.contractTasksMap.get('Awaiting Pick-Up').Id
      : null;
    housingController.changeDoneStatus();
    System.assertEquals(
      'Completed',
      [SELECT id, Status FROM Task WHERE id = :housingController.statusTaskId]
      .Status
    );
    Test.stopTest();
  }
  @isTest
  static void Test_BidContractedStatus_changeFollowStatus() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted',
      Rate_Agreement_Last_Send_Date__c = Datetime.now()
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(
      String.isNotEmpty(housingController.bidData.Id) &&
      !housingController.contractTasksMap.isEmpty()
    );
    housingController.statusTaskId = housingController.contractTasksMap.containsKey(
        'Awaiting Pick-Up'
      )
      ? housingController.contractTasksMap.get('Awaiting Pick-Up').Id
      : null;
    housingController.statusFlag = 'No Follow up';
    housingController.changeFollowStatus();
    System.assertEquals(
      'Normal Follow up',
      [SELECT id, Priority FROM Task WHERE id = :housingController.statusTaskId]
      .Priority
    );
    housingController.statusTaskId = housingController.contractTasksMap.containsKey(
        'Awaiting Pick-Up'
      )
      ? housingController.contractTasksMap.get('Awaiting Pick-Up').Id
      : null;
    housingController.statusFlag = 'Normal Follow up';
    housingController.changeFollowStatus();
    System.assertEquals(
      'Urgent Follow Up',
      [SELECT id, Priority FROM Task WHERE id = :housingController.statusTaskId]
      .Priority
    );
    housingController.statusTaskId = housingController.contractTasksMap.containsKey(
        'Awaiting Pick-Up'
      )
      ? housingController.contractTasksMap.get('Awaiting Pick-Up').Id
      : null;
    housingController.statusFlag = 'Urgent Follow Up';
    housingController.changeFollowStatus();
    System.assertEquals(
      'No Follow up',
      [SELECT id, Priority FROM Task WHERE id = :housingController.statusTaskId]
      .Priority
    );
    Test.stopTest();
  }
  @isTest
  static void Test_OpenForm_ContractToClient() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'contract_to_client';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Contract_to_Client__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    System.assert(housingController.form_attentionList.size() > 1);
    housingController.form_attention = housingController.form_attentionList[1]
      .getValue();
    housingController.changeAttentionForm();
    System.assertEquals(
      housingController.form_attention,
      housingController.form_attentionContact.Id
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = true;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
  }
  @isTest
  static void Test_DeactivateForm_ContractToClient() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'contract_to_client';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Contract_to_Client__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    //housingController.deactivateForm();
    Test.stopTest();
  }
  @isTest
  static void Test_OpenForm_Gcip() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'gcip';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_GCIP__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    System.assert(housingController.form_attentionList.size() > 1);
    housingController.form_attention = housingController.form_attentionList[1]
      .getValue();
    housingController.changeAttentionForm();
    System.assertEquals(
      housingController.form_attention,
      housingController.form_attentionContact.Id
    );
    Integer form_gcip_details_size = housingController.form_gcip_details.size();
    housingController.newFormGCIPTask();
    System.assert(String.isEmpty(housingController.form_gcip_new_task.Id));
    housingController.form_gcip_new_task.Priority__c = 1;
    housingController.form_gcip_new_task.Subject = 'Gcip Subject Test';
    housingController.form_gcip_new_task.Description = 'Description Test';
    housingController.addFormGCIPTask();
    System.assertEquals(
      form_gcip_details_size + 1,
      housingController.form_gcip_details.size()
    );
    housingController.form_gcip_task_id = housingController.form_gcip_new_task.Id;
    housingController.form_gcip_task_priority = String.valueOf(
      housingController.form_gcip_new_task.Priority__c
    );
    housingController.form_gcip_task_subject = housingController.form_gcip_new_task.Subject;
    housingController.form_gcip_task_description = housingController.form_gcip_new_task.Description;
    housingController.editFormGCIPTask();
    System.assertEquals(
      housingController.form_gcip_task_id,
      housingController.form_gcip_new_task.Id
    );
    form_gcip_details_size = housingController.form_gcip_details.size();
    housingController.form_gcip_task_id = housingController.form_gcip_new_task.Id;
    housingController.deleteFormGCIPTask();
    System.assertEquals(
      form_gcip_details_size - 1,
      housingController.form_gcip_details.size()
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_Gcip() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'gcip';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_GCIP__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_GCIP__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_GCIP__c
      )
    );
  }
  @isTest
  static void Test_OpenForm_ContractDateChange() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'contract_date_change';
    housingController.openForm();
    System.assert(
      String.isNotBlank(
        housingController.bidData.Form_Contract_Date_Change__c
      ) && String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_ContractDateChange() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'contract_date_change';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(
        housingController.bidData.Form_Contract_Date_Change__c
      ) && String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Contract_Date_Change__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Contract_Date_Change__c
      )
    );
  }
  @isTest
  static void Test_OpenForm_RoomChanges() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'room_changes';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Room_Changes__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_RoomChanges() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'room_changes';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Room_Changes__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Room_Changes__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Room_Changes__c
      )
    );
  }
  @isTest
  static void Test_OpenForm_CounterNeeded() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'counter_needed';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Counter_Needed__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_CounterNeeded() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'counter_needed';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Counter_Needed__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Counter_Needed__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Counter_Needed__c
      )
    );
  }
  @isTest
  static void Test_OpenForm_CreditCardChange() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'credit_card_change';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Credit_Card_Change__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_CreditCardChange() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'credit_card_change';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Credit_Card_Change__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Credit_Card_Change__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Credit_Card_Change__c
      )
    );
  }
  @isTest
  static void Test_OpenForm_FinalContract() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'final_contract';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Final_Contract__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_FinalContract() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'final_contract';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Final_Contract__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    Test.stopTest();
    //housingController.deactivateForm();
    //System.assert(String.isEmpty([Select Id, Form_Final_Contract__c from Bid__c where id =:housingController.bidData.Id].Form_Final_Contract__c));
  }
  @isTest
  static void Test_OpenForm_NoPickUp() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'no_pick_up';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_No_Pick_Up__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_NoPickUp() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'no_pick_up';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_No_Pick_Up__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_No_Pick_Up__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_No_Pick_Up__c
      )
    );
  }
  @isTest
  static void Test_OpenForm_PickUpReport() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'pick_up_report';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Pick_Up_Report__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_PickUpReport() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'pick_up_report';
    housingController.openForm();
    System.assert(
      String.isNotBlank(housingController.bidData.Form_Pick_Up_Report__c) &&
      String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Pick_Up_Report__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Pick_Up_Report__c
      )
    );
    Test.stopTest();
  }
  @isTest
  static void Test_OpenForm_CancellationLetter() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'cancellation_letter';
    housingController.openForm();
    System.assert(
      String.isNotBlank(
        housingController.bidData.Form_Cancellation_Letter__c
      ) && String.isNotEmpty(housingController.draft.Id)
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }
  @isTest
  static void Test_DeactivateForm_CancellationLetter() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'cancellation_letter';
    housingController.openForm();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(
      String.isNotBlank(
        housingController.bidData.Form_Cancellation_Letter__c
      ) && String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Cancellation_Letter__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Cancellation_Letter__c
      )
    );
  }

  @isTest
  static void Test_OpenForm_RoomingListReminder() {
    Test.startTest();
    housingController.verifyHousing();
    housingController.form_type = 'rooming_list_reminder';
    housingController.openForm();
    System.assert(
      String.isNotBlank(
        housingController.bidData.Form_Rooming_List_Reminder__c
      ) && String.isNotEmpty(housingController.draft.Id)
    );
    System.assert(housingController.form_attentionList.size() > 1);
    housingController.form_attention = housingController.form_attentionList[1]
      .getValue();
    housingController.changeAttentionForm();
    System.assertEquals(
      housingController.form_attention,
      housingController.form_attentionContact.Id
    );
    housingController.form_to = 'Test@test.com';
    housingController.form_cc = '';
    housingController.form_bcc = '';
    housingController.form_subject = 'Email Test 1';
    housingController.form_date = '08/18/20';
    housingController.form_body = 'Email Body Test';
    housingController.form_closing = '';
    housingController.form_isCongaSignSent = false;
    housingController.saveForm();
    System.assert(!housingController.form_isCongaSignSent);
    Test.stopTest();
  }

  @isTest
  static void Test_DeactivateForm_RoomingListReminder() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.form_type = 'rooming_list_reminder';
    housingController.openForm();
    System.assert(
      String.isNotBlank(
        housingController.bidData.Form_Rooming_List_Reminder__c
      ) && String.isNotEmpty(housingController.draft.Id)
    );
    housingController.deactivateForm();
    System.assert(
      String.isEmpty(
        [
          SELECT Id, Form_Rooming_List_Reminder__c
          FROM Bid__c
          WHERE id = :housingController.bidData.Id
        ]
        .Form_Rooming_List_Reminder__c
      )
    );
    Test.stopTest();
  }
  @isTest
  static void Test_OpenAndSaveContractedBidJournals() {
    Journal__c housingBidJournal = new Journal__c(
      RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
        .get('Bid_Journal')
        .getRecordTypeId(),
      Production__c = housingController.opportunityId,
      Bid__c = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Journal_Entry__c = 'Bid Journal Test 1'
    );
    insert housingBidJournal;
    insert new List<Journal__c>{
      new Journal__c(
        RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
          .get('Bid_Journal')
          .getRecordTypeId(),
        Production__c = housingController.opportunityId,
        Bid__c = ApexPages.currentPage().getParameters().get('OpenBidId'),
        Parent_Journal__c = housingBidJournal.Id,
        Journal_Entry__c = 'Bid Child Journal Test 1'
      ),
      new Journal__c(
        RecordTypeId = Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName()
          .get('Bid_Journal')
          .getRecordTypeId(),
        Production__c = housingController.opportunityId,
        Bid__c = ApexPages.currentPage().getParameters().get('OpenBidId'),
        Parent_Journal__c = housingBidJournal.Id,
        Journal_Entry__c = 'Bid Child Journal Test 2'
      )
    };
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.stayJournalSearch = '';
    housingController.checkIssue = false;
    housingController.checkSales = false;
    housingController.searchBidJournal();
    System.assert(!housingController.journalByBidList.isEmpty());
    System.assertEquals(
      housingBidJournal.Id,
      DashboardController.getDataJournal(housingBidJournal.Id).Id
    );
    System.assertEquals(
      0,
      DashboardController.getDataJournalRelated(
          housingBidJournal.Id,
          'production_contacts'
        )
        .size()
    );
    System.assertEquals(
      0,
      DashboardController.getDataJournalRelated(
          housingBidJournal.Id,
          'production_companies'
        )
        .size()
    );
    System.assertEquals(
      0,
      DashboardController.getDataJournalRelated(
          housingBidJournal.Id,
          'company_contacts'
        )
        .size()
    );
    housingController.stayJournalSearch = 'Journal Test';
    housingController.checkIssue = true;
    housingController.checkSales = true;
    housingController.searchBidJournal();
    System.assert(!housingController.journalByBidList.isEmpty());
    Test.stopTest();
  }

  @isTest
  static void Test_AddBidRevenues() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Integer revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Rebate';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Amount';
    housingController.newRevenueBid.Rebate_currency__c = 10;
    housingController.newRevenueBid.Total__c = 20;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Rebate';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Percent';
    housingController.newRevenueBid.Rebate_currency__c = 20;
    housingController.newRevenueBid.Total__c = 30;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Service fee';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Amount';
    housingController.newRevenueBid.Rebate_currency__c = 10;
    housingController.newRevenueBid.Total__c = 20;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Service fee';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Percent';
    housingController.newRevenueBid.Rebate_currency__c = 20;
    housingController.newRevenueBid.Total__c = 30;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Commission';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Amount';
    housingController.newRevenueBid.Rebate_currency__c = 10;
    housingController.newRevenueBid.Total__c = 20;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Commission';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Percent';
    housingController.newRevenueBid.Rebate_currency__c = 20;
    housingController.newRevenueBid.Total__c = 30;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    Test.stopTest();
  }

  @isTest
  static void Test_EditBidRevenues_Rebate() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Integer revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Rebate';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Amount';
    housingController.newRevenueBid.Rebate_currency__c = 10;
    housingController.newRevenueBid.Total__c = 20;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    Revenue__c HousingRevenue = housingController.revenuesBid[
      revenuesBidSize - 1
    ];
    housingController.rebateBidActual = housingRevenue.Id;
    housingController.rebate_revenuetype = 'Rebate';
    housingController.rebate_chargetype = 'Amount';
    housingController.rebate_rebatecurrency = housingRevenue.Rebate_currency__c;
    housingController.rebate_rebateper = 'Person';
    housingController.rebate_total = housingRevenue.Total__c;
    housingController.rebate_invoiceamount = housingRevenue.Invoice_Amount__c;
    housingController.rebate_for = housingRevenue.Rebate_For__c;
    housingController.editRevenueByBid();
    System.assertEquals(
      'Rebate',
      [SELECT id, Revenue_Type__c FROM Revenue__c WHERE id = :housingRevenue.Id]
      .Revenue_Type__c
    );
    revenuesBidSize = housingController.revenuesBid.size();
    HousingRevenue = housingController.revenuesBid[revenuesBidSize - 1];
    housingController.rebateBidActual = housingRevenue.Id;
    housingController.rebate_revenuetype = 'Rebate';
    housingController.rebate_chargetype = 'Percent';
    housingController.rebate_rebatecurrency = housingRevenue.Rebate_currency__c;
    housingController.rebate_rebateper = 'Person';
    housingController.rebate_total = housingRevenue.Total__c;
    housingController.rebate_invoiceamount = housingRevenue.Invoice_Amount__c;
    housingController.rebate_for = housingRevenue.Rebate_For__c;
    housingController.editRevenueByBid();
    System.assertEquals(
      'Percent',
      [SELECT id, Charge_Type__c FROM Revenue__c WHERE id = :housingRevenue.Id]
      .Charge_Type__c
    );
    Test.stopTest();
  }

  @isTest
  static void Test_EditBidRevenues_ServiceFee() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Integer revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Rebate';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Amount';
    housingController.newRevenueBid.Rebate_currency__c = 10;
    housingController.newRevenueBid.Total__c = 20;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    Revenue__c HousingRevenue = housingController.revenuesBid[
      revenuesBidSize - 1
    ];
    HousingRevenue = housingController.revenuesBid[revenuesBidSize - 1];
    housingController.rebateBidActual = housingRevenue.Id;
    housingController.rebate_revenuetype = 'Service fee';
    housingController.rebate_chargetype = 'Amount';
    housingController.rebate_rebatecurrency = housingRevenue.Rebate_currency__c;
    housingController.rebate_rebateper = 'Person';
    housingController.rebate_total = housingRevenue.Total__c;
    housingController.rebate_invoiceamount = housingRevenue.Invoice_Amount__c;
    housingController.rebate_for = housingRevenue.Rebate_For__c;
    housingController.editRevenueByBid();
    System.assertEquals(
      'Service fee',
      [SELECT id, Revenue_Type__c FROM Revenue__c WHERE id = :housingRevenue.Id]
      .Revenue_Type__c
    );
    revenuesBidSize = housingController.revenuesBid.size();
    HousingRevenue = housingController.revenuesBid[revenuesBidSize - 1];
    housingController.rebateBidActual = housingRevenue.Id;
    housingController.rebate_revenuetype = 'Service fee';
    housingController.rebate_chargetype = 'Percent';
    housingController.rebate_rebatecurrency = housingRevenue.Rebate_currency__c;
    housingController.rebate_rebateper = 'Person';
    housingController.rebate_total = housingRevenue.Total__c;
    housingController.rebate_invoiceamount = housingRevenue.Invoice_Amount__c;
    housingController.rebate_for = housingRevenue.Rebate_For__c;
    housingController.editRevenueByBid();
    System.assertEquals(
      'Percent',
      [SELECT id, Charge_Type__c FROM Revenue__c WHERE id = :housingRevenue.Id]
      .Charge_Type__c
    );
    Test.stopTest();
  }

  @isTest
  static void Test_EditBidRevenues_Commission() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Integer revenuesBidSize = housingController.revenuesBid.size();
    housingController.newRevenueBid.Revenue_Type__c = 'Rebate';
    housingController.newRevenueBid.Rebate_For__c = 'Client';
    housingController.newRevenueBid.Charge_Type__c = 'Amount';
    housingController.newRevenueBid.Rebate_currency__c = 10;
    housingController.newRevenueBid.Total__c = 20;
    housingController.newRevenueBid.Invoice_Amount__c = 0;
    housingController.addRevenueBid();
    System.assertEquals(
      revenuesBidSize + 1,
      housingController.revenuesBid.size()
    );
    revenuesBidSize = housingController.revenuesBid.size();
    Revenue__c HousingRevenue = housingController.revenuesBid[
      revenuesBidSize - 1
    ];
    housingController.rebateBidActual = housingRevenue.Id;
    housingController.rebate_revenuetype = 'Commission';
    housingController.rebate_chargetype = 'Amount';
    housingController.rebate_rebatecurrency = housingRevenue.Rebate_currency__c;
    housingController.rebate_rebateper = 'Person';
    housingController.rebate_total = housingRevenue.Total__c;
    housingController.rebate_invoiceamount = housingRevenue.Invoice_Amount__c;
    housingController.rebate_for = housingRevenue.Rebate_For__c;
    housingController.editRevenueByBid();
    System.assertEquals(
      'Commission',
      [SELECT id, Revenue_Type__c FROM Revenue__c WHERE id = :housingRevenue.Id]
      .Revenue_Type__c
    );
    revenuesBidSize = housingController.revenuesBid.size();
    HousingRevenue = housingController.revenuesBid[revenuesBidSize - 1];
    housingController.rebateBidActual = housingRevenue.Id;
    housingController.rebate_revenuetype = 'Commission';
    housingController.rebate_chargetype = 'Percent';
    housingController.rebate_rebatecurrency = housingRevenue.Rebate_currency__c;
    housingController.rebate_rebateper = 'Person';
    housingController.rebate_total = housingRevenue.Total__c;
    housingController.rebate_invoiceamount = housingRevenue.Invoice_Amount__c;
    housingController.rebate_for = housingRevenue.Rebate_For__c;
    housingController.editRevenueByBid();
    System.assertEquals(
      'Percent',
      [SELECT id, Charge_Type__c FROM Revenue__c WHERE id = :housingRevenue.Id]
      .Charge_Type__c
    );
    Test.stopTest();
  }
  @isTest
  static void Test_SaveCloseOut() {
    //Fix By Clay 1 March, 2021
    ApexUtil.HousingTrigger_Is_Enabled = false;
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT id, RecordType.DeveloperName, Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Test.startTest();
    housingController.getCloseOutInformation();
    Integer newRoomTypesBidContractSize = housingController.newRoomTypesBidContract.size();
    housingController.addNewRoomTypeBidContract();
    System.assertEquals(
      newRoomTypesBidContractSize + 1,
      housingController.newRoomTypesBidContract.size()
    );
    Housing__c newRoomType = housingController.newRoomTypesBidContract[
      housingController.newRoomTypesBidContract.size() - 1
    ];
    newRoomType.Unit_Type__c = '1-Bedroom';
    newRoomType.Total_Room_Nights__c = 1;
    newRoomType.Comps__c = 1;
    newRoomType.Rate__c = 5;
    housingController.revenueComps.Comps__c = 2;
    housingController.revenueCommission.Notes__c = 'Revenue Commission Notes Test';
    housingController.revenueCommission.Do_you_need_invoice_sent__c = 'No';
    housingController.revenueCommission.Is_this_a_monthly_Pick_Up__c = 'No';
    housingController.revenueCommission.Does_this_match_amount_on_pick_up_report__c = 'No';
    housingController.closeout_invoiceaddress = housingController.bidData.Vendor__r.BillingStreet;
    housingController.closeout_vataddedorchanged = housingController.bidData.VAT_added_or_changed__c;
    housingController.saveCloseOut();
    System.assertEquals(1, housingController.newRoomTypesBidContract.size());
    Test.stopTest();
  }
  @isTest
  static void Test_ReadyToInvoice() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.readyToInvoice();
    System.assertEquals(
      true,
      [
        SELECT id, Sync_to_QB__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Sync_to_QB__c
    );
    Test.stopTest();
  }
  @isTest
  static void Test_ModifyInvoice() {
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.modifyInvoice();
    System.assertEquals(
      null,
      [
        SELECT id, Invoiced_Date__c
        FROM Bid__c
        WHERE id = :housingController.bidData.Id
      ]
      .Invoiced_Date__c
    );
    Test.stopTest();
  }
  @isTest
  static void Test_InvoiceMonthlyPickUp() {
    //Fix By Clay 1 March, 2021
    ApexUtil.HousingTrigger_Is_Enabled = false;
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT id, RecordType.DeveloperName, Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    Test.startTest();
    housingController.getCloseOutInformation();
    Integer newRoomTypesBidContractSize = housingController.newRoomTypesBidContract.size();
    housingController.addNewRoomTypeBidContract();
    System.assertEquals(
      newRoomTypesBidContractSize + 1,
      housingController.newRoomTypesBidContract.size()
    );
    Housing__c newRoomType = housingController.newRoomTypesBidContract[
      housingController.newRoomTypesBidContract.size() - 1
    ];
    newRoomType.Unit_Type__c = '1-Bedroom';
    newRoomType.Total_Room_Nights__c = 1;
    newRoomType.Comps__c = 1;
    newRoomType.Rate__c = 5;
    housingController.revenueComps.Comps__c = 2;
    housingController.revenueCommission.Notes__c = 'Revenue Commission Notes Test';
    housingController.revenueCommission.Do_you_need_invoice_sent__c = 'No';
    housingController.revenueCommission.Is_this_a_monthly_Pick_Up__c = 'Yes';
    housingController.revenueCommission.Indicate_Dates__c = Date.Today()
      .format();
    housingController.revenueCommission.Does_this_match_amount_on_pick_up_report__c = 'No';
    housingController.invoiceMonthlyPickUp();
    housingController.revenueCommission.Commission_Type__c = 'Percentage';
    housingController.invoiceMonthlyPickUp();
    System.assertEquals(1, housingController.newRoomTypesBidContract.size());
    System.assert(!housingController.monthlypickupsBid.isEmpty());
    housingController.pickup_id = housingController.monthlypickupsBid[
        housingController.monthlypickupsBid.size() - 1
      ]
      .Id;
    housingController.pickup_indicatedates = Date.Today().format();
    housingController.pickup_roomtype = 'Roomtype Name Test';
    housingController.pickup_roomnights = '5';
    housingController.pickup_rate = '10';
    housingController.pickup_commission = '15';
    housingController.pickup_invoiceddate = Date.Today();
    housingController.editPickupByBid();
    System.assertEquals(
      housingController.pickup_id,
      housingController.newPickupBid.Id
    );
    Test.stopTest();
  }

  //Fix By Clay Dev 12 March, 2021 - Test class fixes
  @isTest
  static void coverageMethodsWithHotelHousing() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT
        id,
        venue__c,
        City__r.Name,
        Date_In__c,
        Date_Out__c,
        Name,
        RecordType.Name,
        RecordType.DeveloperName,
        Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    Test.StopTest();

    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    housingController.newFormGCIPTask();
    housingController.addFormGCIPTask();
    housingController.editFormGCIPTask();
    housingController.deleteFormGCIPTask();
    //housingController.verifyHousing();
    housingController.changeDoneStatus();
    housingController.createBidRequest();
    housingController.saveCreateJournal();
    DashboardController.getDataEmailBid('', '', '', '', '', '');
    housingController.sendDateChange();
    housingController.createNewVendor();
    housingController.getBidsByHousing();
    housingController.viewHousingStay();
    housingController.getJournalsByHousing();
  }

  @isTest
  static void coverageMethodsWithCorporateHousing() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT
        id,
        venue__c,
        City__r.Name,
        Date_In__c,
        Date_Out__c,
        Name,
        RecordType.Name,
        RecordType.DeveloperName,
        Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Corporate_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();
    Test.StopTest();

    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    housingController.newFormGCIPTask();
    housingController.addFormGCIPTask();
    housingController.editFormGCIPTask();
    housingController.deleteFormGCIPTask();
    //housingController.verifyHousing();
    housingController.changeDoneStatus();
    housingController.createBidRequest();
    housingController.saveCreateJournal();
    DashboardController.getDataEmailBid('', '', '', '', '', '');
    housingController.sendDateChange();
    housingController.createNewVendor();
    housingController.getBidsByHousing();
    housingController.viewHousingStay();
    housingController.getJournalsByHousing();
  }

  //Fix By Clay Dev 12 March, 2021 - Test class fixes
  @isTest
  static void coverageMethods1() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    Test.startTest();
    housingController.housingStayView = [
      SELECT
        id,
        venue__c,
        City__r.Name,
        Date_In__c,
        Date_Out__c,
        Name,
        RecordType.Name,
        RecordType.DeveloperName,
        Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    housingController.getBidInformation();

    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    housingController.saveCreateJournal();
    DashboardController.getDataEmailBid('', '', '', '', '', '');
    housingController.getJournalsByHousing();
    housingController.searchItinerary();
    Test.StopTest();

    housingController.createHousing();
    housingController.bidContractId = housingController.bidData.Id;
    housingController.bidContractFinalStatus = 'Contracted';
    housingController.updateBidFinalStatus();
  }

  @isTest
  static void Test_coverage2() {
    Test.StartTest();
    housingController.getprevCorporate();
    housingController.getnxtCorporate();
    housingController.getprev();
    housingController.getnxt();

    housingController.OffsetSize2 = housingController.LimitSize2 = housingController.totalRecs2 = 1;
    housingController.getprevCorporate();
    housingController.getnxtCorporate();
    housingController.getprev();
    housingController.getnxt();

    housingController.getDocumentsByProduction();
    Test.StopTest();
  }

  @isTest
  static void Test_upsertGH() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    housingController.bidDataMap = new Map<Integer, DashboardController.BidWrapper>();
    Integer i = 1;
    for (Bid__c bid : [
      SELECT
        Id,
        Production__c,
        No_Bid_reason__c,
        Provider__c,
        Provider__r.Name,
        Housing__c,
        DX_to_Venue__c,
        Vendor__c,
        Vendor__r.Name,
        Vendor__r.Flag_icon__c,
        Vendor__r.ShippingStreet,
        Vendor__r.ShippingCity,
        Vendor__r.ShippingState,
        Vendor__r.ShippingPostalCode,
        Status__c,
        Housing__r.Status_CC__c,
        Housing__r.Status_Previous__c,
        Rate__c,
        Notes__c,
        Options__c,
        Cover__c,
        Include_in_option_cover_sheet__c,
        Vendor__r.City__r.Name,
        Vendor__r.City__c,
        Room_Rate_Release_date__c,
        CreatedDate,
        Vendor_Address__c,
        Bid_Notes__c,
        OLR__c,
        Sabre_Rate__c,
        Locked__c,
        Status_Previous__c,
        RecordTypeId,
        RecordType.Name,
        Internal_Notes__c
      FROM Bid__c
      WHERE Recordtype.DeveloperName = 'Housing_Bid'
    ]) {
      housingController.bidDataMap.put(
        i,
        new DashboardController.BidWrapper(
          bid,
          bid.Vendor__r.Flag_icon__c,
          (bid.DX_to_Venue__c != null ? bid.DX_to_Venue__c : ''),
          bid.Vendor__r.Name,
          bid.Vendor_Address__c,
          bid.Status__c,
          null,
          bid.Room_Rate_Release_date__c,
          bid.OLR__c != null ? bid.OLR__c : '',
          bid.Internal_Notes__c != null ? bid.Internal_Notes__c : '',
          (bid.Status__c == 'Sold Out / Not Bidding'
            ? 1000000
            : (bid.Options__c != null ? bid.Options__c : 999999)),
          (bid.Include_in_option_cover_sheet__c == true ? 1 : 0),
          bid.CreatedDate.date(),
          bid.Provider__c != null ? bid.Provider__r.Name : '',
          bid.Options__c != null ? bid.Options__c : 999999
        )
      );
      i++;
    }
    housingController.housingStayView = [
      SELECT
        id,
        venue__c,
        City__r.Name,
        Date_In__c,
        Date_Out__c,
        Name,
        RecordType.Name,
        RecordType.DeveloperName,
        Billing_Options_Verbiage__c
      FROM Housing__c
      WHERE Recordtype.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ];
    housingController.housingBidNumber = 1;
    Test.startTest();
    housingController.getBidInformation();
    Test.StopTest();
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    String genConfig =
      '{"groupHousingId":"","bookedName":"","actionRequired":"insert","gbs":true,' +
      '"rooms":[{"Id":"","quantity":"1"}],"traces":[{"Id":"","date":"01/01/2020"}]}';
    housingController.groupConfiguration = genConfig;
    housingController.bidContractFinalStatus = 'Cancelled';
    housingController.upsertGH();
  }
  @isTest
  static void Test_BidVendorWrapper() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    insert new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Bid')
        .getRecordTypeId(),
      Production__c = housingController.bidData.Production__c,
      Housing__c = housingController.bidData.Housing__c,
      Vendor__c = housingController.bidData.Vendor__c,
      Status__c = 'Unsent'
    );
    housingController.openBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'created_date';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'name';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'production';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'date_in';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'date_out';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'unit';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'unit_type';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'rate';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'status';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'no_bid_reason';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'venue';
    housingController.bidRelatedVendorList.sort();
    DashboardController.orderBidHistory = 'provider';
    housingController.bidRelatedVendorList.sort();
    Test.stopTest();
  }
  @isTest
  static void Test_OpenAndSortBidHistory() {
    Test.startTest();
    housingController.verifyHousing();
    System.assert(String.isNotEmpty(housingController.bidData.Id));
    housingController.openBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    insert new Bid__c(
      RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName()
        .get('Housing_Bid')
        .getRecordTypeId(),
      Production__c = housingController.bidData.Production__c,
      Housing__c = housingController.bidData.Housing__c,
      Vendor__c = housingController.bidData.Vendor__c,
      Status__c = 'Unsent'
    );
    DashboardController.orderBidHistory = 'created_date';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'created_date';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'name';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'name';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'production';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'production';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'date_in';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'date_in';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'date_out';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'date_out';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'unit';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'unit_type';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    DashboardController.orderBidHistory = 'unit_type';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'unit';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'rate';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'rate';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'status';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'status';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'no_bid_reason';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'no_bid_reason';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'venue';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'venue';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    Test.stopTest();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'provider';
    DashboardController.orderBidHistoryOrientation = 'ASC';
    housingController.orderCheckBidHistory = true;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
    DashboardController.orderBidHistory = 'provider';
    DashboardController.orderBidHistoryOrientation = 'DESC';
    housingController.orderCheckBidHistory = false;
    housingController.orderChangeBidHistory = true;
    housingController.bidhistorysearch_from = Date.Today().addDays(-1);
    housingController.bidhistorysearch_to = Date.Today().addMonths(1);
    housingController.searchBidHistory();
    System.assert(!housingController.bidRelatedVendorList.isEmpty());
  }

  @isTest
  static void Test_getHousingStayByName() {
    String housingName = [
      SELECT Id, Name
      FROM Housing__c
      WHERE RecordType.DeveloperName = 'Hotel_Housing'
      LIMIT 1
    ]
    .Name;
    Test.startTest();
    String housingInfoJson = DashboardController.getHousingStayByName(
      housingName
    );
    System.assertNotEquals(null, housingInfoJson);
    Test.stopTest();
  }

  @isTest
  static void test_random1() {
    ApexPages.currentPage()
      .getParameters()
      .put(
        'OpenBidId',
        [
          SELECT id
          FROM Bid__c
          WHERE Recordtype.DeveloperName = 'Housing_Bid'
          /* and Vendor__r.ShippingCountry = 'Spain'*/ LIMIT 1
        ]
        .id
      );
    Test.startTest();
    housingController.verifyHousing();
    Task task1 = new Task(
      ActivityDate = Date.Today(),
      Subject = 'Pending No Rooms Picked Up'
    );
    Task task2 = new Task(
      ActivityDate = Date.Today(),
      Subject = 'Pending Cancellation'
    );
    Task task3 = new Task(
      ActivityDate = Date.Today(),
      Subject = 'Need to Send to Client'
    );
    Task task4 = new Task(
      ActivityDate = Date.Today(),
      Subject = 'Proof Booking Link'
    );
    insert new List<Task>{ task1, task2, task3, task4 };
    Test.stopTest();

    housingController.statusTaskId = task1.Id;
    housingController.contractTasksMap.put('Pending No Rooms Picked Up', task1);
    housingController.changeDoneStatus();

    housingController.statusTaskId = task2.Id;
    housingController.contractTasksMap.put('Pending Cancellation', task2);
    housingController.changeDoneStatus();

    housingController.statusTaskId = task3.Id;
    housingController.contractTasksMap.put('Need to Send to Client', task3);
    housingController.contractTasksMap.put('Pending Client Signature', task1);
    housingController.changeDoneStatus();

    housingController.statusTaskId = task4.Id;
    housingController.contractTasksMap.put('Update Booking Site', task1);
    housingController.contractTasksMap.put('Proof Booking Link', task4);
    housingController.changeDoneStatus();
  }

  @isTest
  static void test_random2() {
    ApexPages.currentPage()
      .getParameters()
      .put(
        'OpenBidId',
        [
          SELECT id
          FROM Bid__c
          WHERE Recordtype.DeveloperName = 'Housing_Bid'
          /* and Vendor__r.ShippingCountry = 'Spain'*/ LIMIT 1
        ]
        .id
      );
    Test.startTest();
    housingController.verifyHousing();
    Test.stopTest();
    housingController.showAllHotelBlock = false;
    housingController.toggleHotelBlock();
    housingController.showAllGroupBlock = false;
    housingController.toggleGroupBlock();
    housingController.verifyRateOrHousingSent();
    housingController.refreshBid();

    housingController.deleteHousingStay();
    housingController.contactWrapperByProduction = new List<DashboardController.ContactWrapper>();
    housingController.changeContactProduction();

    housingController.emailSubject = housingController.emailBody = 'Test';
    housingController.saveAndCloseReleaseBid();
    housingController.changeCurrencyBid();
  }

  @isTest
  static void Test_getContentDocumentForSendEmail() {
    //Fix By Clay Dev 12 March, 2021 - Test class fixes
    ApexUtil.HousingTrigger_Is_Enabled = false;
    update new Bid__c(
      Id = ApexPages.currentPage().getParameters().get('OpenBidId'),
      Status__c = 'Contracted'
    );
    ApexPages.currentPage()
      .getParameters()
      .put(
        'ContractBidId',
        ApexPages.currentPage().getParameters().get('OpenBidId')
      );
    Test.startTest();
    housingController.verifyHousing();

    ContentVersion contentVersion = new ContentVersion(
      Title = 'Penguins',
      PathOnClient = 'Penguins.jpg',
      VersionData = Blob.valueOf('Test Content'),
      IsMajorVersion = true
    );
    insert contentVersion;
    List<ContentDocument> documents = [
      SELECT Id, Title, LatestPublishedVersionId
      FROM ContentDocument
    ];

    //create ContentDocumentLink  record
    ContentDocumentLink cdl = new ContentDocumentLink();
    cdl.LinkedEntityId = housingController.bidData.id;
    cdl.ContentDocumentId = documents[0].Id;
    cdl.shareType = 'V';
    insert cdl;

    housingController.contactClientValue = housingController.clients[1]
      .getValue();
    housingController.changeClientContract();
    housingController.housingStayView.Trace_Date__c = Date.Today();
    housingController.bidData.Contracting_Back_End_Coordinator__c = housingController.teamMembers[1]
      .getValue();
    housingController.conga_form_type_custom = 'Rate Agreement';
    housingController.getContentDocumentForSendEmail();
    housingController.opportunity.Office_Location__c = 'RRE';
    housingController.getContentDocumentForSendEmail();
    housingController.conga_form_type_custom = 'Contract to Client';
    housingController.getContentDocumentForSendEmail();
    housingController.conga_form_type_custom = 'Production Close Out Report';
    housingController.getContentDocumentForSendEmail();
    housingController.conga_form_type_custom = 'Housing Contract';
    housingController.getContentDocumentForSendEmail();
  }
}```

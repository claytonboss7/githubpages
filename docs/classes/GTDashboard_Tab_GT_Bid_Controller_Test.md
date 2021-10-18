---
layout: default
title: GTDashboard_Tab_GT_Bid_Controller_Test
parent: classes
---

```@isTest
public class GTDashboard_Tab_GT_Bid_Controller_Test{
    private static GTDashboard_Tab_GT_Bid_Controller gtBidController;
    static{
        DashboardDataFactory.createGTData(3);
		gtBidController = new GTDashboard_Tab_GT_Bid_Controller();
        gtBidController.vfpConfiguration = new DashboardConfigurationWrapper();
        gtBidController.vfpConfiguration.parentSObject = 'Ground';
        gtBidController.vfpConfiguration.productionId = gtBidController.opportunityId = [Select id, Name from Opportunity where Name = 'Cats'].Id;
        gtBidController.vfpConfiguration.clientMap = new Map<Id, DashboardClientWrapper>();
        GTDashboard gtDashboard = new GTDashboard();
        gtDashboard.bidDataMap = new Map<Integer, BidWrapper>();
        Integer i = 1;
        for(Bid__c bid:[Select id, CreatedDate, Production__c, GT__c, GT__r.Status_Ground__c, GT__r.Status_Previous__c, Vendor__c, Vendor__r.Flag_icon__c, Vendor__r.Name, Status__c, Internal_notes__c, Options__c from Bid__c where Recordtype.DeveloperName = 'GT_Bid']){
            gtDashboard.bidDataMap.put(i, new BidWrapper(
                bid,
                bid.Vendor__r.Flag_icon__c,
                String.isNotEmpty(bid.Vendor__c) ? bid.Vendor__r.Name : '',
                bid.Status__c,
                null,
                String.isNotBlank(bid.Internal_notes__c) ? bid.Internal_notes__c : '',
                (bid.Options__c != null ? bid.Options__c : 999999),
                bid.CreatedDate.date(),
                bid.Options__c != null ? bid.Options__c : 999999
            ));
            i++;
        } 
        gtBidController.gtDashboard = gtDashboard;
        gtBidController.totalRecsBids = gtDashboard.bidDataMap.size();
        insert new Dashboard__c(Contract_ID__c = 1, Email_Default__c = 'jcerdan@cloudcreations.com');
    }
    @isTest static void Test_OpenAndSaveBid(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id) && gtBidController.contactsBidsByVendor.size() > 1);
        System.assert(!gtBidController.getCurrencyValues().isEmpty());
        gtBidController.bidData.Vendor_Contact__c = gtBidController.contactsBidsByVendor[1].getValue();
        gtBidController.changeContactPrimaryBid();
        System.assert(String.isNotEmpty(gtBidController.bidData.Vendor_Contact__c));
        gtBidController.newSubTripBid();
        System.assert(!gtBidController.bidSubTrips.isEmpty());
        Ground__c gtBidSubtrip = gtBidController.bidSubTrips[0];
        gtBidSubtrip.Sub_Trip_Type__c = 'Airport Transfer';
        gtBidSubtrip.Description__c = 'Airport Transfer Description';
        gtBidController.subtripIdActual = gtBidSubtrip.Id;
        gtBidController.saveSubTripBid();
        System.assertEquals('Airport Transfer', [Select Id, Sub_Trip_Type__c from Ground__c where RecordType.DeveloperName = 'GT_Sub_Trip_Details' and Bid_Sub_Trip__c =:gtBidController.bidData.Id order by Trip_Order__c limit 1].Sub_Trip_Type__c);
        System.assert(!gtBidSubtrip.GTTravels__r.isEmpty());
        Ground__c gtBidTravel = gtBidSubtrip.GTTravels__r[0];
        gtBidController.travelActualOrder = String.valueOf(gtBidSubtrip.GTTravels__r.size() - 1);
        gtBidController.travelActualId = null;
        gtBidController.newtravel_subtripid = gtBidSubtrip.Id;
        gtBidController.newtravel_line = String.valueOf(gtBidTravel.Line__c);
        gtBidController.newtravel_vehicle = gtBidTravel.Vehicle_Ref__c;
        gtBidController.newtravel_vehicleid = null;
        gtBidController.newtravel_startdate = gtBidTravel.Start_Date__c.addDays(1);
        gtBidController.newtravel_starttime = String.valueOf(gtBidTravel.Start_Date_Time__c);
        gtBidController.newtravel_enddate = gtBidTravel.End_Date__c.addDays(1);
        gtBidController.newtravel_endtime = String.valueOf(gtBidTravel.End_Date_Time__c);
        gtBidController.newtravel_traveltype = gtBidTravel.Travel_Type__c;
        gtBidController.newtravel_grouptype = gtBidTravel.Group_Type__c;
        gtBidController.newtravel_locationpickuptype = gtBidTravel.Location_Type__c;
        gtBidController.newtravel_locationpickupdetails = gtBidTravel.Location_Details__c;
        gtBidController.newtravel_locationdropofftype = gtBidTravel.Location_Drop_Off_Type__c;
        gtBidController.newtravel_locationdropoffdetails = gtBidTravel.Location_Details_Drop_Off__c;
        gtBidController.newtravel_notes = gtBidTravel.Airline_Info_Special_Notes__c;
        gtBidController.newtravel_updatemaster = true;
        gtBidController.saveTravelBid();
        System.assert(gtBidController.bidSubTrips[0].GTTravels__r.size() == gtBidSubtrip.GTTravels__r.size() + 1);
        System.assert(String.isNotEmpty(GTDashboard_Tab_GT_Bid_Controller.searchVehicleTrip(gtBidTravel.Vehicle_Ref__c, gtBidController.bidData.Id)));
        gtBidController.save();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id) && String.isNotEmpty(gtBidController.bidRevenue.Id));
        gtBidSubtrip = gtBidController.bidSubTrips[0];
        gtBidController.travelActualId = gtBidSubtrip.GTTravels__r[gtBidSubtrip.GTTravels__r.size() - 1].Id;
        gtBidController.deleteTravelBid();
        System.assert(gtBidController.bidSubTrips[0].GTTravels__r.size() == gtBidSubtrip.GTTravels__r.size() - 1);
        List<Ground__c> gtBidSubtrips = gtBidController.bidSubTrips;
        gtBidController.subtripIdActual = gtBidSubtrips[gtBidSubtrips.size() - 1].Id;
        gtBidController.deleteSubTripBid();
        System.assert(gtBidController.bidSubTrips.size() == gtBidSubtrips.size() - 1);
        gtBidController.bidRevenue.Base_Cost__c = 5;
        gtBidController.bidRevenue.Commission__c = 10;
        gtBidController.bidRevenue.Gratuity__c = 15;
        gtBidController.calculateTotalPrice();
        System.assertEquals(gtBidController.bidRevenue.Base_Cost__c + gtBidController.bidRevenue.Commission__c + gtBidController.bidRevenue.Gratuity__c, gtBidController.bidRevenue.Total_Price__c);
        gtBidController.calculateRevenue();
        System.assertEquals((gtBidController.bidRevenue.Commission__c * 100) / gtBidController.bidRevenue.Base_Cost__c, gtBidController.bidRevenue.Rate__c);
        gtBidController.calculateRevenueByCommission();
        System.assertEquals((gtBidController.bidRevenue.Commission__c * 100) / gtBidController.bidRevenue.Base_Cost__c, gtBidController.bidRevenue.Rate__c);
        gtBidController.calculateRevenueByRate();
        System.assertEquals((gtBidController.bidRevenue.Base_Cost__c * gtBidController.bidRevenue.Rate__c) / 100, gtBidController.bidRevenue.Commission__c);
        gtBidController.bidRevenue.Commission__c = null;
        gtBidController.calculateRevenue();
        System.assertEquals((gtBidController.bidRevenue.Base_Cost__c * gtBidController.bidRevenue.Rate__c) / 100, gtBidController.bidRevenue.Commission__c);
        Test.stopTest();
    }
    @isTest static void Test_ContractBid(){
        gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        //Fix By Clay 27 Dec, 2020
        gtBidController.tripHaveContracted = true;
        gtBidController.contractBid();
        System.assertEquals('Contracted', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        Test.stopTest();
    }
    @isTest static void Test_ContractAnotherBid(){
        update new Bid__c(Id = gtBidController.gtDashboard.bidDataMap.get(1).b.Id, Status__c = 'Contracted');
        Integer i = 1;
        for(Bid__c bid:[Select id, CreatedDate, Production__c, GT__c, GT__r.Status_Ground__c, GT__r.Status_Previous__c, Vendor__c, Vendor__r.Flag_icon__c, Vendor__r.Name, Status__c, Internal_notes__c, Options__c from Bid__c where Recordtype.DeveloperName = 'GT_Bid']){
            gtBidController.gtDashboard.bidDataMap.put(i, new BidWrapper(
                bid,
                bid.Vendor__r.Flag_icon__c,
                String.isNotEmpty(bid.Vendor__c) ? bid.Vendor__r.Name : '',
                bid.Status__c,
                null,
                String.isNotBlank(bid.Internal_notes__c) ? bid.Internal_notes__c : '',
                (bid.Options__c != null ? bid.Options__c : 999999),
                bid.CreatedDate.date(),
                bid.Options__c != null ? bid.Options__c : 999999
            ));
            i++;
        } 
		gtBidController.tripBidNumber = 2;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        Bid__c gtBid = gtBidController.bidData.clone(true, true);
        gtBidController.contractBid();
        System.assertNotEquals(gtBid.GT__c, [Select id, GT__c from Bid__c where id =:gtBid.Id].GT__c);
        Test.stopTest();
    }
    @isTest static void Test_UnContractBid(){
        gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        //Fix By Clay 27 Dec, 2020
        gtBidController.tripHaveContracted = true;
        gtBidController.contractBid();
        System.assertEquals('Contracted', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        //Fix By Clay 27 Dec, 2020
        gtBidController.tripBidNumber = 1;
        Bid__c gtBid = gtBidController.bidData;
        gtBidController.uncontractBid();
        //Fix By Clay 27 Dec, 2020
        //System.assertEquals(gtBid.Status_Previous__c, [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        Test.stopTest();
    }
    @isTest static void Test_ViewContractingBid(){
        gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        //Fix By Clay 27 Dec, 2020
        gtBidController.tripHaveContracted = true;
        gtBidController.contractBid();
        System.assertEquals('Contracted', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
		gtBidController.contractingBidId = gtBidController.bidData.Id;
		gtBidController.contractingParentId = gtBidController.bidData.GT__c;
        gtBidController.viewContractingDetailByBid();
        System.assertEquals(gtBidController.contractingBidId, gtBidController.vfpConfiguration.bidId);
        Test.stopTest();
    }
    @isTest static void Test_DeactivateBid(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        gtBidController.deactivateBid();
        System.assertEquals('Deactivated Bid', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        Test.stopTest();
    }
    @isTest static void Test_BidLocked(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        gtBidController.bidid_locked = gtBidController.bidData.Id;
        gtBidController.bidstatus_locked = true;
        gtBidController.editBidDataLocked();
        System.assertEquals(gtBidController.bidstatus_locked , [Select id, Locked__c from Bid__c where id =:gtBidController.bidData.Id].Locked__c);
        Test.stopTest();
    }
    @isTest static void Test_OpenAndSortBidHistory(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id) && String.isNotEmpty(gtBidController.bidData.Vendor__c));
		gtBidController.openBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
        insert new Bid__c(RecordTypeId = Schema.SObjectType.Bid__c.getRecordTypeInfosByDeveloperName().get('GT_Bid').getRecordTypeId(), Production__c = gtBidController.bidData.Production__c, GT__c = gtBidController.bidData.GT__c, Vendor__c = gtBidController.bidData.Vendor__c, Status__c = 'Unsent');
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'created_date';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'created_date';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'name';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'name';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'production';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'production';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'date_in';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'date_in';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'date_out';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'date_out';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'description';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'description';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'rate';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'rate';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'status';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'status';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'no_bid_reason';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'no_bid_reason';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'venue';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'venue';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'provider';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'ASC';
		gtBidController.orderCheckBidHistory = true;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistory = 'provider';
		GTDashboard_Tab_GT_Bid_Controller.orderBidHistoryOrientation = 'DESC';
		gtBidController.orderCheckBidHistory = false;
		gtBidController.orderChangeBidHistory = true;
		gtBidController.bidhistorysearch_from = Date.Today().addDays(-1);
		gtBidController.bidhistorysearch_to = Date.Today().addMonths(1);
        gtBidController.searchBidHistory();
        System.assert(!gtBidController.bidRelatedVendorList.isEmpty());
        Test.stopTest();
    }
    @isTest static void Test_OpenJournals(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        gtBidController.isBidJournalsRendered = true;
		gtBidController.tripBidNumber = 2;
		gtBidController.getBidInformation();
        System.assert(!gtBidController.isBidJournalsRendered);
        Test.stopTest();
    }
    @isTest static void Test_OpenBidDocuments(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        gtBidController.loadDocuments = true;
		gtBidController.tripBidNumber = 2;
		gtBidController.getBidInformation();
        System.assert(gtBidController.loadDocuments);
        Test.stopTest();
    }
    @isTest static void Test_AddAndDeleteBidVehicles(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        gtBidController.newVehicleBid();
        System.assert(String.isEmpty(gtBidController.newVehicleBid.Id));
        System.assert(!gtBidController.vehiclesByBidList.isEmpty());
        Integer gtBidVehiclesSize = gtBidController.vehiclesByBidList.size();
        Ground__c gtBidVehicle = gtBidController.vehiclesByBidList[gtBidVehiclesSize - 1];
        gtBidController.newVehicleBid.Vehicle_Ref__c = String.valueOf(Integer.valueOf(gtBidVehicle.Vehicle_Ref__c) + 1);
        gtBidController.newVehicleBid.Vehicle_Type__c = gtBidVehicle.Vehicle_Type__c;
        gtBidController.newVehicleBid.Capacity__c = gtBidVehicle.Capacity__c;
        gtBidController.newVehicleBid.Year__c = gtBidVehicle.Year__c;
        gtBidController.newVehicleBid.Gear_Luggage_Space__c = gtBidVehicle.Gear_Luggage_Space__c;
        gtBidController.newVehicleBid.Other_Amenities__c = gtBidVehicle.Other_Amenities__c;
        gtBidController.vehicle_amenities = gtBidVehicle.Amenities__c;
        gtBidController.vehicle_make = gtBidVehicle.Make__c;
        gtBidController.vehicle_model = gtBidVehicle.Model__c;
        gtBidController.addVehicleBid();
        System.assert(gtBidController.vehiclesByBidList.size() == gtBidVehiclesSize + 1);
        gtBidVehicle = gtBidController.vehiclesByBidList[gtBidController.vehiclesByBidList.size() - 1];
        gtBidController.vehicleIdActual = gtBidVehicle.Id;
        gtBidController.vehicle_vehicleref = gtBidVehicle.Vehicle_Ref__c;
        gtBidController.vehicle_vehicletype = gtBidVehicle.Vehicle_Type__c;
        gtBidController.vehicle_capacity = Integer.valueOf(gtBidVehicle.Capacity__c);
        gtBidController.vehicle_make = gtBidVehicle.Make__c;
        gtBidController.vehicle_model = gtBidVehicle.Model__c;
        gtBidController.vehicle_year = gtBidVehicle.Year__c;
        gtBidController.vehicle_amenities = gtBidVehicle.Amenities__c;
        gtBidController.vehicle_otheramenities = gtBidVehicle.Other_Amenities__c;
        gtBidController.vehicle_luggage = gtBidVehicle.Gear_Luggage_Space__c;
        gtBidController.saveEditVehicleBid();
        System.assert(gtBidController.newVehicleBid.Id == gtBidController.vehicleIdActual);
        System.assert(!GTDashboard_Tab_GT_Bid_Controller.getGroundAmenities(gtBidController.newVehicleBid.Id).isEmpty());
        gtBidVehiclesSize = gtBidController.vehiclesByBidList.size();
        gtBidVehicle = gtBidController.vehiclesByBidList[gtBidController.vehiclesByBidList.size() - 1];
        gtBidController.vehicleIdActual = gtBidVehicle.Id;
        gtBidController.deleteVehicleBid();
        System.assert(gtBidController.vehiclesByBidList.size() == gtBidVehiclesSize - 1);
        Test.stopTest();
    }
    @isTest static void Test_AddAndDeleteBidConcessions(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
        System.assert(gtBidController.concessionsRequestedBid.isEmpty());
        gtBidController.concessionRequestedActual = 'Driver Lodging';
        gtBidController.concessionNoteActual = 'Driver Test';
        gtBidController.concessionIncludedActual = 'Included';
        gtBidController.concessionRateActual = '10';
        gtBidController.concessionOrderActual = '1';
        gtBidController.addConcessionBid();
        System.assert(!gtBidController.concessionsRequestedBid.isEmpty());
        Integer gtBidConcessionsSize = gtBidController.concessionsRequestedBid.size();
        gtBidController.concessionRequestedActual = 'Gratuity';
        gtBidController.concessionNoteActual = 'Gratuity Test';
        gtBidController.concessionIncludedActual = 'Excluded';
        gtBidController.concessionRateActual = '10';
        gtBidController.concessionOrderActual = '2';
        gtBidController.addConcessionBid();
        System.assert(gtBidController.concessionsRequestedBid.size() == gtBidConcessionsSize + 1);
        Concessions__c gtBidConcession1 = gtBidController.concessionsRequestedBid[0];
        Concessions__c gtBidConcession2 = gtBidController.concessionsRequestedBid[1];
        System.assert(gtBidConcession1.Order__c == 1 && gtBidConcession2.Order__c == 2);
        gtBidController.concessionActual = gtBidConcession1.Id;
        gtBidController.concessionRequestedActual = gtBidConcession1.Concessions_Requested__c;
        gtBidController.concessionNoteActual = gtBidConcession1.Notes__c;
        gtBidController.concessionIncludedActual = gtBidConcession1.Included_Excluded__c;
        gtBidController.concessionRateActual = gtBidConcession1.Rate__c;
        gtBidController.concessionOrderActual = '2';
        gtBidController.saveEditConcessionBid();
        System.assert(gtBidController.concessionsRequestedBid[0].Id == gtBidConcession2.Id);
        gtBidController.concessionActual = gtBidConcession2.Id;
        gtBidController.concessionRequestedActual = gtBidConcession2.Concessions_Requested__c;
        gtBidController.concessionNoteActual = gtBidConcession2.Notes__c;
        gtBidController.concessionIncludedActual = gtBidConcession2.Included_Excluded__c;
        gtBidController.concessionRateActual = gtBidConcession2.Rate__c;
        gtBidController.concessionOrderActual = null;
        gtBidController.saveEditConcessionBid();
        System.assert(gtBidController.concessionsRequestedBid[0].Id == gtBidConcession1.Id);
        gtBidConcessionsSize = gtBidController.concessionsRequestedBid.size();
        gtBidController.concessionRequestedActual = 'Tolls';
        gtBidController.concessionNoteActual = 'Tolls Test';
        gtBidController.concessionIncludedActual = 'Included';
        gtBidController.concessionRateActual = '10';
        gtBidController.concessionOrderActual = null;
        gtBidController.addConcessionBid();
        System.assert(gtBidController.concessionsRequestedBid.size() == gtBidConcessionsSize + 1);
        gtBidConcessionsSize = gtBidController.concessionsRequestedBid.size();
        gtBidController.concessionActual = gtBidController.concessionsRequestedBid[gtBidConcessionsSize - 1].Id;
        gtBidController.deleteConcessionBid();
        System.assert(gtBidController.concessionsRequestedBid.size() == gtBidConcessionsSize - 1);
        Test.stopTest();
    }
    @isTest static void Test_SoldOutBidStatus(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
		gtBidController.soldOutBidStatus();
        System.assertEquals('Sold Out / Not Bidding', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        Test.stopTest();
    }
    @isTest static void Test_ResendBid(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
		gtBidController.openResendBid();
        System.assert(!gtBidController.contactsByVendorBidMap.isEmpty() && gtBidController.isResendBidRendered);
        Integer gtBidVendorContactsSize = gtBidController.contactsByVendorBidMap.get(gtBidController.bidData.Vendor__c).size();
        gtBidController.vendorContact_id = null;
        gtBidController.vendorContact.AccountId = gtBidController.bidData.Vendor__c;
        gtBidController.vendorContact.FirstName = 'GtVendorContact';
        gtBidController.vendorContact.LastName = 'Test12';
        gtBidController.vendorContact.Designation_title__c = 'General Manager';
        gtBidController.vendorContact.Email = 'GtVendorContactTest12@test.com';
		gtBidController.saveAddContactVendor();
        System.assert(gtBidController.contactsByVendorBidMap.get(gtBidController.bidData.Vendor__c).size() == gtBidVendorContactsSize + 1);
        System.assertEquals('You\'re creating a duplicate record. We recommend you use an existing record.', GTDashboard_Tab_GT_Bid_Controller.validateError('DUPLICATES_DETECTED'));
        System.assertEquals('Error Test', GTDashboard_Tab_GT_Bid_Controller.validateError('Error Test'));
        gtBidController.vendorcontact_actual_id = gtBidController.contactsByVendorBidMap.get(gtBidController.bidData.Vendor__c)[0].c.Id;
		gtBidController.changeContactVendorResendBid();
        System.assert(gtBidController.bidData.Vendor_Contact__c == gtBidController.vendorcontact_actual_id);
        System.assertEquals(gtBidController.vendorcontact_actual_id, GTDashboard_Tab_GT_Bid_Controller.getDataContact(gtBidController.vendorcontact_actual_id).Id);
        gtBidController.resendBidAgreement_contactPrimary = gtBidController.bidData.Vendor_Contact__c;
		gtBidController.congaResendBid();
        System.assertEquals('Sent', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
		gtBidController.modal = 'myModalResendBid';
        gtBidController.resendBidAgreement_contactPrimary = gtBidController.contactsByVendorBidMap.get(gtBidController.bidData.Vendor__c)[0].c.Id;
		gtBidController.changeContactVendorResendBid();
        System.assertEquals(gtBidController.contactsByVendorBidMap.get(gtBidController.bidData.Vendor__c)[0].c.Email, GTDashboard_Tab_GT_Bid_Controller.getDataPreviewResendBid(gtBidController.opportunityId, gtBidController.bidData.GT__c, gtBidController.bidData.Id, gtBidController.resendBidAgreement_contactPrimary, 'Test.com')[0]);
        gtBidController.contactPrimarySelected = gtBidController.resendBidAgreement_contactPrimary;
		gtBidController.sendResendBid();
        System.assertEquals('Sent', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        Test.stopTest();
    }
    @isTest static void Test_ReleaseBid(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id));
		gtBidController.openReleaseByBid();
        System.assert(!gtBidController.contactsByVendor_releaseMap.isEmpty() && gtBidController.isReleaseBidRendered);
        Integer gtBidVendorContactsSize = gtBidController.contactsByVendor_releaseMap.get(gtBidController.bidData.Vendor__c).size();
        gtBidController.vendorContact_id = null;
        gtBidController.vendorContact.AccountId = gtBidController.bidData.Vendor__c;
        gtBidController.vendorContact.FirstName = 'GtVendorContact';
        gtBidController.vendorContact.LastName = 'Test12';
        gtBidController.vendorContact.Designation_title__c = 'General Manager';
        gtBidController.vendorContact.Email = 'GtVendorContactTest12@test.com';
		gtBidController.saveAddContactVendor();
        System.assert(gtBidController.contactsByVendor_releaseMap.get(gtBidController.bidData.Vendor__c).size() == gtBidVendorContactsSize + 1);
        System.assertEquals('You\'re creating a duplicate record. We recommend you use an existing record.', GTDashboard_Tab_GT_Bid_Controller.validateError('DUPLICATES_DETECTED'));
        System.assertEquals('Error Test', GTDashboard_Tab_GT_Bid_Controller.validateError('Error Test'));
        gtBidController.releaseVendorcontact_actual_id = gtBidController.contactsByVendor_releaseMap.get(gtBidController.bidData.Vendor__c)[0].c.Id;
		gtBidController.changeContactVendorReleaseByBid();
        System.assert(gtBidController.bidData.Vendor_Contact__c == gtBidController.releaseVendorcontact_actual_id);
        System.assertEquals(gtBidController.releaseVendorcontact_actual_id, GTDashboard_Tab_GT_Bid_Controller.getDataContact(gtBidController.releaseVendorcontact_actual_id).Id);
        System.assertEquals(gtBidController.contactsByVendor_releaseMap.get(gtBidController.bidData.Vendor__c)[0].c.Email, GTDashboard_Tab_GT_Bid_Controller.getDataPreviewReleaseBid(gtBidController.opportunityId, gtBidController.bidData.GT__c, gtBidController.bidData.Id, gtBidController.releaseVendorcontact_actual_id)[0]);
		gtBidController.sendReleaseByBid();
        System.assertEquals('Sold Out / Not Bidding', [Select id, Status__c from Bid__c where id =:gtBidController.bidData.Id].Status__c);
        Test.stopTest();
    }
    @isTest static void Test_OpenBidAgreement_RateAgreement(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id) && gtBidController.contactsBidsByVendor.size() > 1);
		gtBidController.bidAgreement_type = 'Rate Agreement';
		gtBidController.openBidAgreement();
		gtBidController.getContactsByVendorBid();
		gtBidController.getBidAgreementProductionAssociationContacts();
        System.assert(String.isNotBlank(gtBidController.bidData.Form_Rate_Agreement__c) && String.isNotEmpty(gtBidController.draft.Id) && gtBidController.isBidAgreementRendered);
        System.assert(String.isNotEmpty(GTDashboard_Tab_GT_Bid_Controller.searchContactEmail(gtBidController.contactsBidsByVendor[1].getLabel())));
		gtBidController.draft.Primary_Contact_Id__c = gtBidController.contactsBidsByVendor[1].getValue();
        gtBidController.changeBidAgreementContactPrimary();
        System.assert(gtBidController.bidAgreementPrimaryContact.Id == gtBidController.draft.Primary_Contact_Id__c);
		gtBidController.bidAgreement_to = 'Test@test.com';
		gtBidController.bidAgreement_cc = '';
		gtBidController.bidAgreement_bcc = '';
		gtBidController.isCongaSignSent = true;
		gtBidController.saveBidAgreement();
		gtBidController.draft.Id = null;
		gtBidController.saveBidAgreement();
		gtBidController.isBidAgreementRendered = false;
		gtBidController.bidAgreement_type = 'Rate Agreement';
		gtBidController.openBidAgreement();
        System.assert(String.isNotBlank(gtBidController.bidData.Form_Rate_Agreement__c) && String.isNotEmpty(gtBidController.draft.Id) && gtBidController.isBidAgreementRendered);
		gtBidController.deactivateBidAgreement();
        System.assert(String.isEmpty([Select Id, Form_Rate_Agreement__c from Bid__c where id =:gtBidController.bidData.Id].Form_Rate_Agreement__c));
		gtBidController.deactivateBidAgreement();
		Test.stopTest();
    }
    //
    @isTest static void Test_OpenBidAgreement_TransportationContract(){
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id) && gtBidController.contactsBidsByVendor.size() > 1);
		gtBidController.bidAgreement_type = 'Transportation Contract';
		gtBidController.openBidAgreement();
		gtBidController.getContactsByVendorBid();
		gtBidController.getBidAgreementProductionAssociationContacts();
		gtBidController.getBidAgreementCreditCards();
        System.assert(String.isNotBlank(gtBidController.bidData.Form_Transportation_Contract__c) && String.isNotEmpty(gtBidController.draft.Id) && gtBidController.isBidAgreementRendered);
        System.assert(String.isNotEmpty(GTDashboard_Tab_GT_Bid_Controller.searchContactEmail(gtBidController.contactsBidsByVendor[1].getLabel())));
		gtBidController.draft.Primary_Contact_Id__c = gtBidController.contactsBidsByVendor[1].getValue();
        gtBidController.changeBidAgreementContactPrimary();
        System.assert(gtBidController.bidAgreementPrimaryContact.Id == gtBidController.draft.Primary_Contact_Id__c);
        gtBidController.saveBidAgreement();
		gtBidController.isBidAgreementRendered = false;
		gtBidController.bidAgreement_type = 'Transportation Contract';
		gtBidController.openBidAgreement();
        System.assert(String.isNotBlank(gtBidController.bidData.Form_Transportation_Contract__c) && String.isNotEmpty(gtBidController.draft.Id) && gtBidController.isBidAgreementRendered);
		Test.stopTest();
	}
    @isTest static void Test_OpenBidAgreement_TripDetailsUpdate(){
		ContentVersion contentVersionTest1 = new ContentVersion(Title = 'DocumentTest1', PathOnClient = '/DocumentTest1.txt', VersionData = Blob.valueOf('DocumentTest1'));
		insert contentVersionTest1;
		Id contentDocumentId = [Select Id, ContentDocumentId From ContentVersion Where Id =:contentVersionTest1.Id].ContentDocumentId;
		gtBidController.tripBidNumber = 1;
        Test.startTest();
		gtBidController.getBidInformation();
        System.assert(String.isNotEmpty(gtBidController.bidData.Id) && gtBidController.contactsBidsByVendor.size() > 1);
		gtBidController.bidAgreement_type = 'Trip Details Update';
		gtBidController.openBidAgreement();
		gtBidController.getContactsByVendorBid();
        System.assert(String.isNotBlank(gtBidController.bidData.Form_Trip_Details_Update__c) && String.isNotEmpty(gtBidController.draft.Id) && gtBidController.isBidAgreementRendered);
        System.assert(String.isNotEmpty(GTDashboard_Tab_GT_Bid_Controller.searchContactEmail(gtBidController.contactsBidsByVendor[1].getLabel())));
		gtBidController.draft.Attention__c = gtBidController.contactsBidsByVendor[1].getValue();
        gtBidController.changeBidAgreementAttentionContact();
        System.assert(gtBidController.bidAgreementAttentionContact.Id == gtBidController.draft.Attention__c);
        gtBidController.saveBidAgreement();
		gtBidController.isBidAgreementRendered = false;
		gtBidController.bidAgreement_type = 'Trip Details Update';
		gtBidController.openBidAgreement();
        System.assert(String.isNotBlank(gtBidController.bidData.Form_Trip_Details_Update__c) && String.isNotEmpty(gtBidController.draft.Id) && gtBidController.isBidAgreementRendered);
		gtBidController.attachdocument_objectid = gtBidController.bidData.Id;
		gtBidController.openAttachDocs();
        System.assert(gtBidController.attachDocumentList.isEmpty());
		gtBidController.documentRelationId = gtBidController.bidData.Id;
		gtBidController.filename = 'Attach Test 1';
		gtBidController.body = 'data:text/plain;base64,VGVzdA==';
		gtBidController.doAttachmentLast();
        System.assert(String.isNotEmpty(gtBidController.newattachment_id) && String.isNotBlank(gtBidController.newattachment_name));
		gtBidController.documentRelationId = null;
		gtBidController.filename = 'Attach Test 2';
		gtBidController.body = 'data:text/plain;base64,VGVzdA==';
		gtBidController.newattachment_id = null;
		gtBidController.newattachment_name = null;
		gtBidController.doAttachmentLast();
        System.assert(String.isEmpty(gtBidController.newattachment_id) && String.isBlank(gtBidController.newattachment_name));
        System.assert(String.isEmpty(GTDashboard_Tab_GT_Bid_Controller.sendEmail('Test@test.com', '', '', 'Email Subject Test', 'Email Body Test', contentDocumentId, gtBidController.opportunityId, gtBidController.bidData.GT__c)));
		Test.stopTest();
	}
}```

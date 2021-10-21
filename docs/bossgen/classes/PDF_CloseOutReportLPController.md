---
layout: default
title: PDF_CloseOutReportLPController
parent: classes
---
# Metadata Type
classes


# Filename 
PDF_CloseOutReportLPController


# Raw XML
```
/**
 * @description       : used by the landing page to generate a PDF, opposed to storing it and making it publically available.
 *                      there is a PDF attachment that gets attached to the Pickup Report landing page submit, but the sharing for the Force.com
 *                      site and storage makes it more efficient to just generate on demand and let the browser handle it.
 * @author            : clay b
 * @group             :
 * @last modified on  : 06-24-2021
 * @last modified by  : clay b
 * Modifications Log
 * Ver   Date         Author   Modification
 * 1.0   06-23-2021   clay b   Initial Version
 **/
public without sharing class PDF_CloseOutReportLPController {
  public Housing__c housing { get; set; }
  public Bid__c thebid { get; set; }
  public Revenue__c therevenue { get; set; }
  public Map<Integer, List<Bid__c>> bidsMap { get; set; }
  public Map<Id, List<Concessions__c>> bidConcessionsMap { get; set; }
  public Decimal theRoomTypeTotal { get; set; }
  public Decimal theCommissionTotal { get; set; }
  public String theIndicateDates { get; set; }
  public Boolean showError { get; set; }

  /**
  * @description constructor , gets the data for the PDF body
  * @author clay b | 06-23-2021
  **/
  public PDF_CloseOutReportLPController() {

    try {
      Housing__c theHousing = new Housing__c();
      theHousing = [
        SELECT
          Id,
          Name,
          Date_Out__c,
          Date_In__c,
          City__c,
          City__r.Name,
          Venue__r.Name,
          Venue__c,
          Production_CC__c,
          Status_CC__c,
          Status__c,
          Production_CC__r.Name,
          Production_CC__r.Office_Location__c,
          Production_CC__r.Account.Name
        FROM Housing__c
        WHERE
          Id IN (
            SELECT Housing__c
            FROM Bid__c
            WHERE UUID_for_Landing_Page__c = :ApexPages.currentPage().getParameters().get('bidid')
          )
        LIMIT 1
      ];

      housing = theHousing;
      Revenue__c[] theRevenues = new List<Revenue__c>();
      therevenue = new Revenue__c();
      bidsMap = new Map<Integer, List<Bid__c>>();
      bidConcessionsMap = new Map<Id, List<Concessions__c>>();
      for (Bid__c bid : [
        SELECT
          responseVendorName__c,
          Id,
          UUID_for_landing_page__c,
          coVendorName__c,
          City__c,
          Housing__c,
          CreatedDate,
          Vendor_Comments__c,
          No_Bid_Reason__c,
          Name,
          Production_Office_Location__c,
          LastModifiedDate,
          Options__c,
          Production__c,
          Room_Rate_Release_date__c,
          Vendor__c,
          is_Vendor_European__c,
          Vendor__r.Name,
          Provider__r.Name,
          Venue__c,
          DX_to_Venue__c,
          Vendor_Contact__r.Name,
          Vendor_Contact__c,
          Vendor__r.Website,
          Vendor__r.ShippingStreet,
          Vendor__r.ShippingCity,
          Vendor__r.ShippingState,
          Vendor__r.ShippingPostalCode,
          Vendor__r.Phone,
          Vendor__r.Fax,
          Vendor__r.Metro_Area__c,
          Vendor__r.Check_In_Time__c,
          Vendor__r.Check_In_Time_Formatted__c,
          Vendor__r.Check_out_time__c,
          Vendor__r.Check_out_time_formatted__c,
          Vendor__r.Number_of_rooms__c,
          Vendor__r.Number_of_suites__c,
          Vendor__r.Star_Rating__c,
          Vendor__r.Year_built__c,
          Vendor__r.Year_renovated__c,
          Vendor__r.X100_Non_Smoking__c,
          Vendor__r.Lift_Elevator__c,
          Vendor__r.Property_Entry__c,
          Vendor__r.X24_hour_doorman__c,
          Vendor__r.X24_Hour_FD__c,
          Vendor__r.Washer_dryer_in_unit__c,
          Vendor__r.Washer_Dryer_Type__c,
          Vendor__r.Washer_Dryer__c,
          Vendor__r.Pool__c,
          Vendor__r.Pool_Seasonal__c,
          Vendor__r.Hot_Tub__c,
          Vendor__r.Hot_tub_seasonal__c,
          Vendor__r.Parking_on_site__c,
          Vendor__r.On_site_parking_charge__c,
          Vendor__r.On_site_parking_charge_type__c,
          Vendor__r.Do_you_own_the_lot__c,
          Vendor__r.Porterage__c,
          Vendor__r.Windows_Open__c,
          Vendor__r.Air_conditioning__c,
          Vendor__r.High_Speed_Internet__c,
          Vendor__r.Connection__c,
          Vendor__r.Internet_Charge__c,
          Vendor__r.Internet_Charge_Type__c,
          Vendor__r.Pets_Allowed__c,
          Vendor__r.Pets_charge__c,
          Vendor__r.Pets_charge_type__c,
          Vendor__r.Pets_max_LBS__c,
          Vendor__r.Refrigerator__c,
          Vendor__r.Refrigerator_Size__c,
          Vendor__r.Refrigerator_Location__c,
          Vendor__r.Refrigerator_charge__c,
          Vendor__r.Refrigerator_charge_type__c,
          Vendor__r.Microwave__c,
          Vendor__r.Microwave_Location__c,
          Vendor__r.Microwave_charge__c,
          Vendor__r.Microwave_charge_type__c,
          Vendor__r.Oven__c,
          Vendor__r.Oven_Location__c,
          Vendor__r.Burners__c,
          Vendor__r.of_burners__c,
          Vendor__r.Burners_location__c,
          Vendor__r.Hobs__c,
          Vendor__r.of_Hobs__c,
          Vendor__r.Hobs_Location__c,
          Vendor__r.Coffee_Maker__c,
          Vendor__r.Hairdryers__c,
          Vendor__r.Bathtub__c,
          Vendor__r.Safe__c,
          Vendor__r.Safe_Comments__c,
          Vendor__r.Fitness_room__c,
          Vendor__r.Fitness_Room_Type__c,
          Vendor__r.On_site_Day_Spa_RRE__c,
          Vendor__r.Hotel_Shuttle__c,
          Vendor__r.Airport_Shuttle__c,
          Vendor__r.Hotel_Bars__c,
          Vendor__r.hotel_bars_2__c,
          Vendor__r.Hotel_bar_hours__c,
          Vendor__r.Restaurants__c,
          Vendor__r.Restaurants_2__c,
          Vendor__r.Restaurants_hours__c,
          Vendor__r.Breakfast__c,
          Vendor__r.Breakfast_type__c,
          Vendor__r.Room_Service__c,
          Vendor__r.Room_Service_hours__c,
          Vendor__r.Self_Parking__c,
          Vendor__r.Self_Parking_Charge__c,
          Vendor__r.Self_Parking_Charge_Type__c,
          Vendor__r.Valet_Parking__c,
          Vendor__r.Valet_Parking_Charge__c,
          Vendor__r.Valet_Parking_Charge_Type__c,
          Vendor__r.Coach_Bus_Parking__c,
          Vendor__r.Coach_Bus_Charge__c,
          Vendor__r.Coach_Bus_Charge_Type__c,
          Vendor__r.Walk_to_Restaurant__c,
          Vendor__r.restaurants_within_0_5_mile_1_KM__c,
          Vendor__r.Laundromat_near__c,
          Vendor__r.Restaurant_near__c,
          Vendor__r.Shopping_Mall_near__c,
          Vendor__r.Gym_near__c,
          Vendor__r.Grocery_store_near__c,
          Vendor__r.Housing_Address__c,
          (
            SELECT
              id,
              Date_In__c,
              Date_Out__c,
              Comps__c,
              Units__c,
              Nights_CC__c,
              Unit_Type__c,
              Rate__c,
              Rate_Symbol_Conga__c,
              Special_Notes__c,
              Nights__c,
              Total_Room_Nights__c,
              Total_Night_Rev__c,
              Room_Nights_x_Rate_Pickup_Report__c
            FROM Housing__r
            WHERE RecordType.DeveloperName = 'Room_Types_Ops'
            ORDER BY createdDate DESC
          ),
          (SELECT id, Bid__c, Concessions_Requested__c, Concession_Provided__c
          FROM Concessions__r
          ORDER BY Order__c ASC NULLS LAST, CreatedDate DESC)
        FROM Bid__c
        WHERE UUID_for_landing_page__c = :ApexPages.currentPage().getParameters().get('bidid')
      ]) {
        thebid = bid;
        theRoomTypeTotal = 0;
        doTotalRoomRevenue();
        doTotalCommission();
        bidsMap.put(0,new List<Bid__c>{bid});
        bidConcessionsMap.put(thebid.Id, new List<Concessions__c>());
        for (Concessions__c concession : bid.Concessions__r)
          bidConcessionsMap.get(concession.Bid__c).add(concession);
      }
      showError=false;
    } catch (Exception e) {
      showError=true;
      system.debug (e.getMessage() + ' - ' + e.getStackTraceString());
    }

  }

  /**
  * @description calculation that is displayed for the Room type records attached to the bids and their rates
  * @author clay b | 06-23-2021
  **/
  private void doTotalRoomRevenue() {
    Decimal roomTypeTotal = 0;
    for (Housing__c roomtype : thebid.Housing__r) {
      Decimal therate = roomtype.Rate__c != null ? roomtype.Rate__c : 0;
      Decimal thetotalroomnights = roomtype.Total_Room_Nights__c != null ? roomtype.Total_Room_Nights__c : 0;
      Decimal thecomps = roomtype.Comps__c != null ? roomtype.Comps__c : 0;

      roomTypeTotal = roomTypeTotal + (therate * (thetotalroomnights - thecomps));
    }
    theRoomTypeTotal = roomTypeTotal;
  }

  /**
  * @description calculation for commission that should reside on the revenue__c record in Commission_Percent__c
  * @author clay b | 06-23-2021
  **/
  private void doTotalCommission() {
    Decimal roomTypeTotal = 0;
    Decimal commissionTotal = 0;
    Decimal commissionPercent = 0;
    Revenue__c[] theRevenues = new List<Revenue__c>();

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
        CurrencyIsoCode,
        Rate_Currency__c,
        Tax__c,
        Surcharge__c,
        Tax_Included__c,
        Surcharge_Included__c,
        Commission_Agreed__c,
        Sign_name__c
      FROM Revenue__c
      WHERE
        RecordType.DeveloperName IN ('Housing_Rate_Commission_RRE', 'Housing_Rate_Commission_RRU')
        AND Room_Type__c = NULL
        AND Bid__c IN (SELECT Id FROM Bid__c WHERE UUID_for_landing_page__c = :thebid.UUID_for_landing_page__c)
      LIMIT 1
    ];
    theRevenues = searchRevenue;
    if (theRevenues.size() > 0) {
      therevenue = new Revenue__c();
      therevenue = theRevenues[0];
    }

    commissionPercent = therevenue.Commission_Percent__c != null &&
      therevenue.Commission_Percent__c != 0
      ? therevenue.Commission_Percent__c
      : 10;
    for (Housing__c roomtype : thebid.Housing__r) {
      Decimal therate = roomtype.Rate__c != null ? roomtype.Rate__c : 0;
      Decimal thetotalroomnights = roomtype.Total_Room_Nights__c != null ? roomtype.Total_Room_Nights__c : 0;
      Decimal thecomps = roomtype.Comps__c != null ? roomtype.Comps__c : 0;

      roomTypeTotal = roomTypeTotal + (therate * (thetotalroomnights - thecomps));
    }

    commissionTotal = roomTypeTotal * (commissionPercent / 100);
    theCommissionTotal = commissionTotal;

    theIndicateDates = therevenue.Indicate_Dates__c;
  }
}
```


# Last Modified


# Usage

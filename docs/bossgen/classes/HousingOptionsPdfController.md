---
layout: default
title: HousingOptionsPdfController
parent: classes
---
# Metadata Type
classes


# Filename 
HousingOptionsPdfController


# Raw XML
```
public class HousingOptionsPdfController{
    public Housing__c housing {get;set;}
    public String ProductionName {get;set;}
    public Contact contact {get;set;}
    public Map<Integer, List<Bid__c>> bidsMap {get;set;}
    public Integer bidsMapSize {get;set;}
    public Map<Id, List<Concessions__c>> bidConcessionsMap {get;set;}
    public Map<Id, Vendor_Venue__c> vendorVenueMap {get;set;}
    public Map<Id, Set<String>> vendorProdutionsMap {get;set;}
    public Map<Id, List<Vendor_Airport_Association__c>> vendorAirportsMap {get;set;}
    public Date LastUpdatedDate {get;set;}
    public Date RoomsReleaseDate {get;set;}
    public HousingOptionsPdfController(ApexPages.StandardController stdController){
        List<Housing__c> housings = [Select id, RecordType.DeveloperName, Production_CC__r.Name, Date_In__c, Date_Out__c, Venue__c, Venue__r.Name, City__r.Name, is_Vendor_European__c from Housing__c where id =:((Housing__c)stdController.getRecord()).id];
        housing = !housings.isEmpty() ? housings[0] : new Housing__c();
        ProductionName = housing.Production_CC__r.Name;
        List<Contact> contacts = [Select id, Housing_Options_Preferred__c from Contact where id =:ApexPages.currentPage().getParameters().get('contactId')];
        contact = !contacts.isEmpty() ? contacts[0] : new Contact(Housing_Options_Preferred__c = 'true');
        bidsMap = new Map<Integer, List<Bid__c>>();
        bidConcessionsMap = new Map<Id, List<Concessions__c>>();
        vendorVenueMap = new Map<Id, Vendor_Venue__c>();
        vendorProdutionsMap = new Map<Id, Set<String>>();
        vendorAirportsMap = new Map<Id, List<Vendor_Airport_Association__c>>();
        Integer column = 1;
        Integer columns = 3;
        Integer key = 0;
        for(Bid__c bid:[Select id, Housing__c, LastModifiedDate, Options__c, Production__c, Room_Rate_Release_date__c, Vendor__c, is_Vendor_European__c, Vendor__r.Name, Provider__r.Name, Venue__c, DX_to_Venue__c, Vendor__r.Website, Vendor__r.ShippingStreet, Vendor__r.ShippingCity, Vendor__r.ShippingState, Vendor__r.ShippingPostalCode, Vendor__r.Phone, Vendor__r.Fax, Vendor__r.Metro_Area__c, Vendor__r.Check_In_Time__c, Vendor__r.Check_In_Time_Formatted__c, Vendor__r.Check_out_time__c, Vendor__r.Check_out_time_formatted__c, Vendor__r.Number_of_rooms__c, Vendor__r.Number_of_suites__c, Vendor__r.Star_Rating__c, Vendor__r.Year_built__c, Vendor__r.Year_renovated__c, Vendor__r.X100_Non_Smoking__c, Vendor__r.Lift_Elevator__c, Vendor__r.Property_Entry__c, Vendor__r.X24_hour_doorman__c, Vendor__r.X24_Hour_FD__c, Vendor__r.Washer_dryer_in_unit__c, Vendor__r.Washer_Dryer_Type__c, Vendor__r.Washer_Dryer__c, Vendor__r.Pool__c, Vendor__r.Pool_Seasonal__c, Vendor__r.Hot_Tub__c, Vendor__r.Hot_tub_seasonal__c, Vendor__r.Parking_on_site__c, Vendor__r.On_site_parking_charge__c, Vendor__r.On_site_parking_charge_type__c, Vendor__r.Do_you_own_the_lot__c, Vendor__r.Porterage__c, Vendor__r.Windows_Open__c, Vendor__r.Air_conditioning__c, Vendor__r.High_Speed_Internet__c, Vendor__r.Connection__c, Vendor__r.Internet_Charge__c, Vendor__r.Internet_Charge_Type__c, Vendor__r.Pets_Allowed__c, Vendor__r.Pets_charge__c, Vendor__r.Pets_charge_type__c, Vendor__r.Pets_max_LBS__c, Vendor__r.Refrigerator__c, Vendor__r.Refrigerator_Size__c, Vendor__r.Refrigerator_Location__c, Vendor__r.Refrigerator_charge__c, Vendor__r.Refrigerator_charge_type__c, Vendor__r.Microwave__c, Vendor__r.Microwave_Location__c, Vendor__r.Microwave_charge__c, Vendor__r.Microwave_charge_type__c, Vendor__r.Oven__c, Vendor__r.Oven_Location__c, Vendor__r.Burners__c, Vendor__r.of_burners__c, Vendor__r.Burners_location__c, Vendor__r.Hobs__c, Vendor__r.of_Hobs__c, Vendor__r.Hobs_Location__c, Vendor__r.Coffee_Maker__c, Vendor__r.Hairdryers__c, Vendor__r.Bathtub__c, Vendor__r.Safe__c, Vendor__r.Safe_Comments__c, Vendor__r.Fitness_room__c, Vendor__r.Fitness_Room_Type__c, Vendor__r.On_site_Day_Spa_RRE__c, Vendor__r.Hotel_Shuttle__c, Vendor__r.Airport_Shuttle__c, Vendor__r.Hotel_Bars__c, Vendor__r.hotel_bars_2__c, Vendor__r.Hotel_bar_hours__c, Vendor__r.Restaurants__c, Vendor__r.Restaurants_2__c, Vendor__r.Restaurants_hours__c, Vendor__r.Breakfast__c, Vendor__r.Breakfast_type__c, Vendor__r.Room_Service__c, Vendor__r.Room_Service_hours__c, Vendor__r.Self_Parking__c, Vendor__r.Self_Parking_Charge__c, Vendor__r.Self_Parking_Charge_Type__c, Vendor__r.Valet_Parking__c, Vendor__r.Valet_Parking_Charge__c, Vendor__r.Valet_Parking_Charge_Type__c, Vendor__r.Coach_Bus_Parking__c, Vendor__r.Coach_Bus_Charge__c, Vendor__r.Coach_Bus_Charge_Type__c, Vendor__r.Walk_to_Restaurant__c, Vendor__r.restaurants_within_0_5_mile_1_KM__c, Vendor__r.Laundromat_near__c, Vendor__r.Restaurant_near__c, Vendor__r.Shopping_Mall_near__c, Vendor__r.Gym_near__c, Vendor__r.Grocery_store_near__c, 
                        (Select id, Date_In__c, Date_Out__c, Units__c, Unit_Type__c, Rate__c, Rate_Symbol_Conga__c from Housing__r where RecordType.DeveloperName = 'Room_Types_Ops' order by createdDate desc), 
                        (Select Id, Tax__c, Tax_Conga__c, Tax_Included__c, Surcharge__c, Surcharge_included__c, VAT__c, VAT_Conga__c, Breakfast__c, Breakfast_Conga__c, City_Tax__c, City_Tax_Conga__c, CurrencyIsoCode FROM Rate_Commission__r order by LastModifiedDate desc limit 1) 
                        from Bid__c where Housing__c =:housing.id and Options__c != null AND Include_in_options__c = true AND Status__c != 'Deactivated Bid' order by Options__c asc]){
            if(bidsMap.get(key) == null) bidsMap.put(key, new List<Bid__c>());
            bidsMap.get(key).add(bid);
            bidConcessionsMap.put(bid.id, new List<Concessions__c>());   
            LastUpdatedDate = LastUpdatedDate != null ? (bid.LastModifiedDate.Date() > LastUpdatedDate ? bid.LastModifiedDate.Date() : LastUpdatedDate) : bid.LastModifiedDate.Date();
            RoomsReleaseDate = RoomsReleaseDate != null ? (bid.Room_Rate_Release_date__c != null && bid.Room_Rate_Release_date__c < RoomsReleaseDate ? bid.Room_Rate_Release_date__c : RoomsReleaseDate) : bid.Room_Rate_Release_date__c;
            if(String.isNotEmpty(bid.Vendor__c)){
                vendorVenueMap.put(bid.Vendor__c, new Vendor_Venue__c());   
                vendorProdutionsMap.put(bid.Vendor__c, new Set<String>());   
                vendorAirportsMap.put(bid.Vendor__c, new List<Vendor_Airport_Association__c>());   
            }
            if(column >= columns){
                column = 1;
                key++;
            } 
            else column++;
        }
        while(bidsMap.size() > 0 && bidsMap.get(bidsMap.size() - 1).size() < columns) bidsMap.get(bidsMap.size() - 1).add(new Bid__c());
        bidsMapSize = bidsMap.size();
        for(Vendor_Venue__c vendorVenue:(String.isNotEmpty(housing.Venue__c) ? [Select id, Vendor__c, Distance_formula__c from Vendor_Venue__c where Venue__c =:housing.Venue__c] : new List<Vendor_Venue__c>())) vendorVenueMap.put(vendorVenue.Vendor__c, vendorVenue);
        for(Bid__c bid:[Select id, Production__r.Name, Vendor__c from Bid__c where Vendor__c in:vendorProdutionsMap.keySet() and Status__c = 'Contracted']) vendorProdutionsMap.get(bid.Vendor__c).add(bid.Production__r.Name);
        for(Concessions__c concession:[Select id, Bid__c, Concessions_Requested__c, Concession_Provided__c from Concessions__c where Bid__c in:bidConcessionsMap.keySet() and Agreed__c = true Order By Order__c ASC NULLS LAST, CreatedDate DESC]) bidConcessionsMap.get(concession.Bid__c).add(concession);
        for(Vendor_Airport_Association__c airportAssociation:[Select id, Vendor__c, Airport__r.Name, Distance__c, Distance_Type__c from Vendor_Airport_Association__c where Vendor__c in:vendorAirportsMap.keySet()]) vendorAirportsMap.get(airportAssociation.Vendor__c).add(airportAssociation);
    }
}
```


# Last Modified


# Usage

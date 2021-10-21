---
layout: default
title: VoyajerItineraryOverviewController
parent: classes
---
# Metadata Type
classes


# Filename 
VoyajerItineraryOverviewController


# Raw XML
```
public without sharing class VoyajerItineraryOverviewController {
    
    //Fix By Clay Dev 27 Feb, 2021 #177024410
	@AuraEnabled
	public static String searchItineraries(String opportunityId, String startDate, String endDate, String cityId) {
        Boolean isShowAll = (String.isBlank(startDate) && String.isBlank(endDate)) ? true : false;
        Map<Date, List<Itinerary>> searchItinerariesMap = new Map<Date, List<Itinerary>>();
		Map<Id, List<Ground__c>> groundSubtripDetailsMap = new Map<Id, List<Ground__c>>();
		Map<Id, List<Freight__c>> freightSubtripDetailsMap = new Map<Id, List<Freight__c>>();
		Map<Id, Revenue__c> revenuesMap = new Map<Id, Revenue__c>();
		Itinerary itinerary;
		
		//Fix By Clay Dev 6 March, 2021 #176911471 - Added Status_cc__c != \'Deleted\'
		String housingQuery = 'SELECT id, Name, Date_In__c, Date_Out__c, Status_CC__c, Vendor_lookup__r.Name, Vendor_lookup__r.ShippingStreet,' +
        	' Vendor_lookup__r.ShippingCity, Vendor_lookup__r.ShippingState, Vendor_lookup__r.ShippingCountryCode, Vendor_lookup__r.Phone,' +
			' Venue__r.Name, City__r.Name, City__r.City__c, City__r.State__c,' +
			' (SELECT Id, Units__c, Unit_Type__c, Special_Notes__c, Date_In__c, Date_Out__c, Rate__c, Nights_CC__c, Sales_Housing__c, Room_Type__c FROM Housing__r' + 
			' WHERE RecordType.DeveloperName = \'Room_Types_Ops\' AND Bid__c = NULL ORDER BY CreatedDate DESC )' +
			' FROM Housing__c WHERE Production_CC__c = :opportunityId AND Status_cc__c != \'Deleted\' AND (RecordType.DeveloperName = \'Hotel_Housing\' OR RecordType.DeveloperName = \'Corporate_Housing\'' +
			' OR RecordType.DeveloperName = \'Individual_Reservation\') ';
			
		Date startDateValue, endDateValue;
		if(!isShowAll) {
            if(String.isNotBlank(startDate) && String.isNotBlank(endDate)) {
                startDateValue = Date.valueOf(startDate);
                endDateValue = Date.valueOf(endDate);
                for(Integer i = 0; i <= startDateValue.daysBetween(endDateValue); i++) {
                    searchItinerariesMap.put(startDateValue.addDays(i), new List<Itinerary>());    
                }
                housingQuery += ' AND ((Date_In__c >= :startDateValue AND Date_In__c <= :endDateValue)' +
                    ' OR (Date_Out__c >= :startDateValue AND Date_Out__c <= :endDateValue) OR (Date_In__c < :startDateValue' +
                    ' AND Date_Out__c > :endDateValue) OR (Date_In__c >= :startDateValue AND Date_Out__c = NULL))';
            }
        }
		housingQuery += ' ORDER BY Date_In__c';
        
        List<Housing__c> housings = Database.query(housingQuery);
		
        List<String> statusList = new List<String>{'Decision', 'In Contracting', 'Contracted', 'Pending Client Signature', 
            'Pending Hotel Counter', 'Pending Update'};
		List<Housing__c> roomTypes = [SELECT Id, CurrencyIsoCode, Bid__r.Housing__c, Units__c, Unit_Type__c, Special_Notes__c, Date_In__c, 
        	Date_Out__c, Rate__c, Nights_CC__c, Rate_Period__c, 
			Sales_Housing__c, Room_Type__c FROM Housing__c WHERE RecordType.DeveloperName = 'Room_Types_Ops' 
            AND Bid__c != NULL AND Bid__r.Status__c IN: statusList
			AND Bid__r.Housing__c IN: housings ORDER BY CreatedDate DESC];
		
		Map<Id, Bid__c> bidIdToRecMap = new Map<Id, Bid__c>([SELECT Id, (Select Id, CurrencyIsoCode from Rate_Commission__r where CurrencyIsoCode != null LIMIT 1) FROM Bid__c 
			WHERE Status__c IN: statusList AND Housing__c IN: housings ORDER BY CreatedDate DESC]);
		
		Map<String, List<Housing__c>> salesHousingIdToContractedRoomTypesMap = new Map<String, List<Housing__c>>();
		for(Housing__c rt : roomTypes) {
			if(!salesHousingIdToContractedRoomTypesMap.containsKey(rt.Bid__r.Housing__c)) {
				salesHousingIdToContractedRoomTypesMap.put(rt.Bid__r.Housing__c, new List<Housing__c>());
			}
			String currencyISOCode = rt.CurrencyIsoCode;
			if(bidIdToRecMap.containsKey(rt.Bid__c) && bidIdToRecMap.get(rt.Bid__c).Rate_Commission__r.size() > 0) {
				currencyISOCode = bidIdToRecMap.get(rt.Bid__c).Rate_Commission__r[0].CurrencyIsoCode;
			}
			rt.CurrencyIsoCode = currencyISOCode != null ? DashboardController.getSymbol(currencyISOCode) : '';
			salesHousingIdToContractedRoomTypesMap.get(rt.Bid__r.Housing__c).add(rt);
		}
        for (Housing__c housingStay : housings) {
            if(salesHousingIdToContractedRoomTypesMap.containsKey(housingStay.Id)) {
				itinerary = new Itinerary(housingStay, salesHousingIdToContractedRoomTypesMap.get(housingStay.Id));
			} else {
				itinerary = new Itinerary(housingStay, housingStay.Housing__r);
			}
            if(String.isNotBlank(cityId)) {
				String theItinerary = itinerary.toString();
				if(!theItinerary.contains(cityId)) {
					continue;
				}
			}
			system.debug('current city:: ' + housingStay.City__c + 'current city:: ' + housingStay.City__r.Name);
			system.debug('inside city query');
            
			housingStay.Date_In_Text__c = housingStay.Date_In__c != null
				? Datetime.newInstance(housingStay.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			housingStay.Date_Out_Text__c = housingStay.Date_Out__c != null
				? Datetime.newInstance(housingStay.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Housing__c roomType : (List<Housing__c>)itinerary.relatedRecords) {
				roomType.Date_In_Text__c = roomType.Date_In__c != null
					? Datetime.newInstance(roomType.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				roomType.Date_Out_Text__c = roomType.Date_Out__c != null
					? Datetime.newInstance(roomType.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
			}
			//Fix By Clay Dev 27 Feb, 2021 #177024410
			if(isShowAll) {
				if(housingStay.Date_In__c != null) {
					if(housingStay.Date_Out__c != null) {
						for(Integer i = 0; i <= housingStay.Date_In__c.daysBetween(housingStay.Date_Out__c); i++) {
							if(!searchItinerariesMap.containsKey(housingStay.Date_In__c.addDays(i))) {
								searchItinerariesMap.put(housingStay.Date_In__c.addDays(i), new List<Itinerary>());
							}
			                searchItinerariesMap.get(housingStay.Date_In__c.addDays(i)).add(itinerary);
			            }
					} else {
						if(!searchItinerariesMap.containsKey(housingStay.Date_In__c)) {
							searchItinerariesMap.put(housingStay.Date_In__c, new List<Itinerary>());
						}
						searchItinerariesMap.get(housingStay.Date_In__c).add(itinerary);
					}
				}
			} else {
				for (Date itineraryDate : searchItinerariesMap.keySet()) {
					if (
						housingStay.Date_In__c != null &&
						((housingStay.Date_Out__c != null && itineraryDate >= housingStay.Date_In__c && itineraryDate <= housingStay.Date_Out__c) ||
						(housingStay.Date_In__c == itineraryDate))
					)
						searchItinerariesMap.get(itineraryDate).add(itinerary);
				}
			}
		}
        
        String groundQuery = 'SELECT id, GT_Trip_Details__c, (SELECT id, GT_Sub_Trip_Details__c, Vehicle_Ref__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, ' +
			' Travel_Type__c, Group_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Location_Details_Drop_Off__c, Airline_Info_Special_Notes__c'+
			' FROM GTTravels__r WHERE RecordType.DeveloperName = \'GT_Travel_Details\' ORDER BY Line__c) FROM Ground__c WHERE Production_Ground__c = :opportunityId'+
			' AND RecordType.DeveloperName = \'GT_Sub_Trip_Details\'';
		
		if(!isShowAll) {	
			groundQuery += ' AND ((GT_Trip_Details__r.Start_Date__c >= :startDateValue AND GT_Trip_Details__r.Start_Date__c <= :endDateValue)'+
				' OR (GT_Trip_Details__r.End_Date__c >= :startDateValue AND GT_Trip_Details__r.End_Date__c <= :endDateValue)'+
				' OR (GT_Trip_Details__r.Start_Date__c < :startDateValue AND GT_Trip_Details__r.End_Date__c > :endDateValue)'+
				' OR (GT_Trip_Details__r.Start_Date__c >= :startDateValue AND GT_Trip_Details__r.End_Date__c = NULL))';
		}
		groundQuery += ' ORDER BY Trip_Order__c';
		for (Ground__c groundSubtrip : Database.query(groundQuery)) {
			if (!groundSubtripDetailsMap.containsKey(groundSubtrip.GT_Trip_Details__c))
				groundSubtripDetailsMap.put(groundSubtrip.GT_Trip_Details__c, new List<Ground__c>());
			groundSubtripDetailsMap.get(groundSubtrip.GT_Trip_Details__c).add(groundSubtrip);
			for (Ground__c groundTravel : groundSubtrip.GTTravels__r) {
				groundTravel.Start_Date_Text__c = groundTravel.Start_Date__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.End_Date_Text__c = groundTravel.End_Date__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.Start_Date_Time_Text__c = groundTravel.Start_Date__c != null &&
					groundTravel.Start_Date_Time__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, groundTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				groundTravel.End_Date_Time_Text__c = groundTravel.End_Date__c != null &&
					groundTravel.End_Date_Time__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, groundTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.GT__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.GT__c = :groundSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Ground_Rate_Travel_Commission'
		])
			revenuesMap.put(rate.Bid__r.GT__c, rate);
        
        String groundQuery2 = 'SELECT id, Name, Start_Date__c, End_Date__c, Status_Ground__c, Vendor_lookup__r.Name, Vendor_lookup__r.ShippingStreet, '+
			' Vendor_lookup__r.BillingCity, Vendor_lookup__r.BillingState, Vendor_lookup__r.BillingCountryCode, Vendor_lookup__r.Phone, Start_city__r.City__c, '+
			' Start_city__r.State__c, (SELECT id, Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make_Model__c, Year__c, Amenities__c FROM Ground__r'+
			' WHERE RecordType.DeveloperName = \'Vehicle_Type\' ORDER BY Vehicle_Ref__c) FROM Ground__c WHERE Production_Ground__c = :opportunityId AND'+
            ' RecordType.DeveloperName = \'GT_Trip_Details\'';
        
        if(!isShowAll) {
			groundQuery2 += ' AND ((Start_Date__c >= :startDateValue AND Start_Date__c <= :endDateValue) OR '+
                ' (End_Date__c >= :startDateValue  AND End_Date__c <= :endDateValue) OR (Start_Date__c < :startDateValue AND '+
                ' End_Date__c > :endDateValue) OR (Start_Date__c >= :startDateValue AND End_Date__c = NULL))';
        }
        groundQuery2 += ' ORDER BY Start_Date__c';
		for (Ground__c groundTrip : Database.query(groundQuery2)) {
			itinerary = new Itinerary(groundTrip);
			if(String.isNotBlank(cityId)) {
				String theItinerary = itinerary.toString();
				if(!theItinerary.contains(cityId)) {
					continue;
				}
			}
			//Fix By Clay Dev 27 Feb, 2021 #177024410
			if(isShowAll) {
				if(groundTrip.Start_Date__c != null) {
					if(groundTrip.End_Date__c != null) {
						for (Integer i = 0; i <= groundTrip.Start_Date__c.daysBetween(groundTrip.End_Date__c); i++) {
			                if(!searchItinerariesMap.containsKey(groundTrip.Start_Date__c.addDays(i))) {
								searchItinerariesMap.put(groundTrip.Start_Date__c.addDays(i), new List<Itinerary>());
							}
							searchItinerariesMap.get(groundTrip.Start_Date__c.addDays(i)).add(itinerary);
			            }
					} else {
						if(!searchItinerariesMap.containsKey(groundTrip.Start_Date__c)) {
							searchItinerariesMap.put(groundTrip.Start_Date__c, new List<Itinerary>());
						}
						searchItinerariesMap.get(groundTrip.Start_Date__c).add(itinerary);
					}
				}
			} else {
				for (Date itineraryDate : searchItinerariesMap.keySet()) {
					if (
						groundTrip.Start_Date__c != null &&
						((groundTrip.End_Date__c != null && itineraryDate >= groundTrip.Start_Date__c && itineraryDate <= groundTrip.End_Date__c) ||
						(groundTrip.Start_Date__c == itineraryDate))
					) {
						searchItinerariesMap.get(itineraryDate).add(itinerary);
					}
				}
			}
			groundTrip.Start_Date_Text__c = groundTrip.Start_Date__c != null
				? Datetime.newInstance(groundTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			groundTrip.End_Date_Text__c = groundTrip.End_Date__c != null
				? Datetime.newInstance(groundTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (groundSubtripDetailsMap.containsKey(groundTrip.id))
				itinerary.relatedRecords = groundSubtripDetailsMap.get(groundTrip.id);
			if (revenuesMap.containsKey(groundTrip.id))
				groundTrip.Total_Price__c = revenuesMap.get(groundTrip.id).Total_Price__c;
		}
		
		String freightQuery = 'SELECT id, Freight_Trip_Details__c, (SELECT id, Freight_Sub_Trip_Details__c, Vehicle_Ref__c, Start_Date__c, Start_Date_Time__c, '+
			' End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Location_Details_Drop_Off__c,'+
			' Airline_Info_Special_Notes__c, Freight_Truck_Sq_Ft__c FROM FreightEquipments__r WHERE RecordType.DeveloperName = \'Equipment_Details\' ORDER BY Line__c)'+
			' FROM Freight__c WHERE Production__c = :opportunityId AND RecordType.DeveloperName = \'Freight_Sub_Trip_Details\'';
			
		if(!isShowAll) {
			freightQuery += 'AND ((Freight_Trip_Details__r.Start_Date__c >= :startDateValue AND Freight_Trip_Details__r.Start_Date__c <= :endDateValue)'+
				' OR (Freight_Trip_Details__r.End_Date__c >= :startDateValue AND Freight_Trip_Details__r.End_Date__c <= :endDateValue)'+
				' OR (Freight_Trip_Details__r.Start_Date__c < :startDateValue AND Freight_Trip_Details__r.End_Date__c > :endDateValue)'+
				' OR (Freight_Trip_Details__r.Start_Date__c >= :startDateValue AND Freight_Trip_Details__r.End_Date__c = NULL))';
		}
		freightQuery += ' ORDER BY Trip_Order__c';
		for (Freight__c freightSubtrip : Database.query(freightQuery)) {
			if (!freightSubtripDetailsMap.containsKey(freightSubtrip.Freight_Trip_Details__c))
				freightSubtripDetailsMap.put(freightSubtrip.Freight_Trip_Details__c, new List<Freight__c>());
			freightSubtripDetailsMap.get(freightSubtrip.Freight_Trip_Details__c).add(freightSubtrip);
			for (Freight__c freightTravel : freightSubtrip.FreightEquipments__r) {
				freightTravel.Start_Date_Text__c = freightTravel.Start_Date__c != null
					? Datetime.newInstance(freightTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				freightTravel.End_Date_Text__c = freightTravel.End_Date__c != null
					? Datetime.newInstance(freightTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				freightTravel.Start_Date_Time_Text__c = freightTravel.Start_Date__c != null &&
					freightTravel.Start_Date_Time__c != null
					? Datetime.newInstance(freightTravel.Start_Date__c, freightTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				freightTravel.End_Date_Time_Text__c = freightTravel.End_Date__c != null &&
					freightTravel.End_Date_Time__c != null
					? Datetime.newInstance(freightTravel.End_Date__c, freightTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.Freight__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.Freight__c = :freightSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Freight_Rate_Commission'
		])
			revenuesMap.put(rate.Bid__r.Freight__c, rate);
			
		String revenueQuery = 'SELECT id, Name, Start_Date__c, End_Date__c, Status__c, Vendor_lookup__r.Name, Vendor_lookup__r.BillingStreet, '+
			' Vendor_lookup__r.BillingCity, Vendor_lookup__r.BillingState, Vendor_lookup__r.BillingCountryCode, Vendor_lookup__r.Phone, Start_city__r.City__c,'+
			'  Start_city__r.State__c, (SELECT id, Equipment__c, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make_Model__c, Year__c, Freight_Truck_Sq_Ft__c,'+
			' Amenities__c FROM FreightSubTrips__r WHERE RecordType.DeveloperName = \'Vehicle_Type\' ORDER BY Equipment__c) FROM Freight__c'+
			' WHERE Production__c = :opportunityId AND RecordType.DeveloperName = \'Freight_Trip_Details\'';
			
		if(!isShowAll) {
			revenueQuery += ' AND ((Start_Date__c >= :startDateValue AND Start_Date__c <= :endDateValue) OR (End_Date__c >= :startDateValue'+
				' AND End_Date__c <= :endDateValue) OR (Start_Date__c < :startDateValue AND End_Date__c > :endDateValue)'+
				' OR (Start_Date__c >= :startDateValue AND End_Date__c = NULL))';
		}	
		revenueQuery += ' ORDER BY Start_Date__c';
		for (Freight__c freightTrip : Database.query(revenueQuery)) {
			itinerary = new Itinerary(freightTrip);
			if(String.isNotBlank(cityId)) {
				String theItinerary = itinerary.toString();
				if(!theItinerary.contains(cityId)) {
					continue;
				}
			}
			//Fix By Clay Dev 27 Feb, 2021 #177024410
			if(isShowAll) {
				if(freightTrip.Start_Date__c != null) {
					if(freightTrip.End_Date__c != null) {
						for (Integer i = 0; i <= freightTrip.Start_Date__c.daysBetween(freightTrip.End_Date__c); i++) {
							if(!searchItinerariesMap.containsKey(freightTrip.Start_Date__c.addDays(i))) {
								searchItinerariesMap.put(freightTrip.Start_Date__c.addDays(i), new List<Itinerary>());
							}
			                searchItinerariesMap.get(freightTrip.Start_Date__c.addDays(i)).add(itinerary);
			            }
					} else {
						if(!searchItinerariesMap.containsKey(freightTrip.Start_Date__c)) {
							searchItinerariesMap.put(freightTrip.Start_Date__c, new List<Itinerary>());
						}
						searchItinerariesMap.get(freightTrip.Start_Date__c).add(itinerary);
					}
				}
			} else {
				for (Date itineraryDate : searchItinerariesMap.keySet()) {
					if (
						freightTrip.Start_Date__c != null &&
						((freightTrip.End_Date__c != null && itineraryDate >= freightTrip.Start_Date__c && itineraryDate <= freightTrip.End_Date__c) ||
						(freightTrip.Start_Date__c == itineraryDate))
					)
						searchItinerariesMap.get(itineraryDate).add(itinerary);
				}
			}
			freightTrip.Start_Date_Text__c = freightTrip.Start_Date__c != null
				? Datetime.newInstance(freightTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			freightTrip.End_Date_Text__c = freightTrip.End_Date__c != null
				? Datetime.newInstance(freightTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (freightSubtripDetailsMap.containsKey(freightTrip.id))
				itinerary.relatedRecords = freightSubtripDetailsMap.get(freightTrip.id);
			if (revenuesMap.containsKey(freightTrip.id))
				freightTrip.Total_Price__c = revenuesMap.get(freightTrip.id).Total_Price__c;
		}
		
		String revenueQuery2 = 'SELECT id, Bid__r.Air__c, Total_Price__c FROM Revenue__c WHERE Bid__r.Production__c = :opportunityId AND'+
			' RecordType.DeveloperName = \'Air_Rate_Commission\' AND Deviation__c = NULL';
			
		if(!isShowAll) {
			revenueQuery2 += ' AND ((Bid__r.Air__r.Departure_Date__c >= :startDateValue AND Bid__r.Air__r.Departure_Date__c <= :endDateValue)'+
				' OR (Bid__r.Air__r.Return_Date__c >= :startDateValue AND Bid__r.Air__r.Return_Date__c <= :endDateValue)'+
				' OR (Bid__r.Air__r.Departure_Date__c < :startDateValue AND Bid__r.Air__r.Return_Date__c > :endDateValue)'+
				' OR (Bid__r.Air__r.Departure_Date__c >= :startDateValue AND Bid__r.Air__r.Return_Date__c = NULL))';
		}
		
		for (Revenue__c rate : Database.query(revenueQuery2))
			revenuesMap.put(rate.Bid__r.Air__c, rate);
		System.debug(searchItinerariesMap);
		
		String airQuery = 'SELECT id, Name, Status__c, Departure_Date__c, Departure_City__r.Name, Departure_City__r.City__r.Name, Departure_City__r.City__r.City__c,'+
			' Departure_City__r.City__r.State__c, Return_Date__c, Return_Departure_City__r.Name, Return_Departure_City__r.City__r.Name, Return_Arrival_City__r.Name,'+
			' Return_Arrival_City__r.City__r.Name, Vendor__r.Name, Vendor__r.BillingStreet, Vendor__r.BillingCity, Vendor__r.BillingState, Vendor__r.BillingCountryCode,'+
			' Vendor__r.Phone, (SELECT id, Departure_Date__c, Dep_Time__c, Departure_City__r.Name, Departure_City__r.City__r.City__c, Departure_City__r.City__r.State__c,'+
			' Arrival_Date__c, Arr_Time__c, Arrival_City__r.Name, Arrival_City__r.City__r.City__c, Arrival_City__r.City__r.State__c, Flight_Duration_hrs__c,'+
			' Flight_Duration_Mins__c, Number_of_Seats__c, Equip_Type__c FROM Air_Segments__r WHERE RecordType.DeveloperName = \'Air_Segments\') FROM Air__c'+
			' WHERE Production__c = :opportunityId AND RecordType.DeveloperName = \'Air_Trip_Details\'';
		
		if(!isShowAll) {
			airQuery += ' AND ((Departure_Date__c >= :startDateValue AND Departure_Date__c <= :endDateValue) OR (Return_Date__c >= :startDateValue'+
				' AND Return_Date__c <= :endDateValue) OR (Departure_Date__c < :startDateValue AND Return_Date__c > :endDateValue)'+
				' OR (Departure_Date__c >= :startDateValue AND Return_Date__c = NULL))';
		}
		airQuery += ' ORDER BY Departure_Date__c';
		for (Air__c airTrip : Database.query(airQuery)) {
			itinerary = new Itinerary(airTrip);
			if(String.isNotBlank(cityId)) {
				String theItinerary = itinerary.toString();
				if(!theItinerary.contains(cityId)) {
					continue;
				}
			}
			//Fix By Clay Dev 27 Feb, 2021 #177024410
			if(isShowAll) {
				if(airTrip.Departure_Date__c != null) {
					if(airTrip.Return_Date__c != null) {
						for (Integer i = 0; i <= airTrip.Departure_Date__c.daysBetween(airTrip.Return_Date__c); i++) {
							if(!searchItinerariesMap.containsKey(airTrip.Departure_Date__c.addDays(i))) {
								searchItinerariesMap.put(airTrip.Departure_Date__c.addDays(i), new List<Itinerary>());
							}
			                searchItinerariesMap.get(airTrip.Departure_Date__c.addDays(i)).add(itinerary);
			            }
					} else {
						if(!searchItinerariesMap.containsKey(airTrip.Departure_Date__c)) {
							searchItinerariesMap.put(airTrip.Departure_Date__c, new List<Itinerary>());
						}
						searchItinerariesMap.get(airTrip.Departure_Date__c).add(itinerary);
					}
				}
			} else {
				for (Date itineraryDate : searchItinerariesMap.keySet()) {
					if (
						airTrip.Departure_Date__c != null &&
						((airTrip.Return_Date__c != null && itineraryDate >= airTrip.Departure_Date__c && itineraryDate <= airTrip.Return_Date__c) ||
						(airTrip.Departure_Date__c == itineraryDate))
					)
						searchItinerariesMap.get(itineraryDate).add(itinerary);
				}
			}
			airTrip.Departure_Date_Text__c = airTrip.Departure_Date__c != null
				? Datetime.newInstance(airTrip.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			airTrip.Return_Date_Text__c = airTrip.Return_Date__c != null
				? Datetime.newInstance(airTrip.Return_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Air__c airSegment : airTrip.Air_Segments__r) {
				airSegment.Departure_Date_Text__c = airSegment.Departure_Date__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Arrival_Date_Text__c = airSegment.Arrival_Date__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Dep_Time_Text__c = airSegment.Departure_Date__c != null &&
					airSegment.Dep_Time__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, airSegment.Dep_Time__c).format('h:mm a')
					: '';
				airSegment.Arr_Time_Text__c = airSegment.Arrival_Date__c != null &&
					airSegment.Arr_Time__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, airSegment.Arr_Time__c).format('h:mm a')
					: '';
			}
			if (revenuesMap.containsKey(airTrip.id))
				airTrip.Total_Price__c = revenuesMap.get(airTrip.id).Total_Price__c;
			System.debug(airTrip);
		}

		return JSON.serialize(searchItinerariesMap);
	}
    
	/**Fix By Clay Dev 27 Feb, 2021 #177024410
    @AuraEnabled
	public static String searchItineraries(String opportunityId, String startDate, String endDate, String cityId) {
		Map<Date, List<Itinerary>> searchItinerariesMap = new Map<Date, List<Itinerary>>();
		Map<Id, List<Ground__c>> groundSubtripDetailsMap = new Map<Id, List<Ground__c>>();
		Map<Id, List<Freight__c>> freightSubtripDetailsMap = new Map<Id, List<Freight__c>>();
		Map<Id, Revenue__c> revenuesMap = new Map<Id, Revenue__c>();
		Itinerary itinerary;

		for (Integer i = 0; i <= Date.valueOf(startDate).daysBetween(Date.valueOf(endDate)); i++)
			searchItinerariesMap.put(Date.valueOf(startDate).addDays(i), new List<Itinerary>());
		for (Housing__c housingStay : [
			SELECT
				id,
				Name,
				Date_In__c,
				Date_Out__c,
				Status_CC__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.ShippingStreet,
				Vendor_lookup__r.ShippingCity,
				Vendor_lookup__r.ShippingState,
				Vendor_lookup__r.ShippingCountryCode,
				Vendor_lookup__r.Phone,
				Venue__r.Name,
				City__r.Name,
				City__r.City__c,
				City__r.State__c,
				(
					SELECT
						Id,
						Units__c,
						Unit_Type__c,
						Special_Notes__c,
						Date_In__c,
						Date_Out__c,
						Rate__c,
						Nights_CC__c,
						Sales_Housing__c,
						Room_Type__c
					FROM Housing__r
					WHERE RecordType.DeveloperName = 'Room_Types_Ops' AND Bid__c = NULL
					ORDER BY CreatedDate DESC
				)
			FROM Housing__c
			WHERE
				Production_CC__c = :opportunityId
				AND (RecordType.DeveloperName = 'Hotel_Housing'
				OR RecordType.DeveloperName = 'Corporate_Housing'
				OR RecordType.DeveloperName = 'Individual_Reservation')
				AND ((Date_In__c >= :Date.valueOf(startDate)
				AND Date_In__c <= :Date.valueOf(endDate))
				OR (Date_Out__c >= :Date.valueOf(startDate)
				AND Date_Out__c <= :Date.valueOf(endDate))
				OR (Date_In__c < :Date.valueOf(startDate)
				AND Date_Out__c > :Date.valueOf(endDate))
				OR (Date_In__c >= :Date.valueOf(startDate)
				AND Date_Out__c = NULL))
			ORDER BY Date_In__c
		]) {
			Boolean isStayCityOurCityLookup = false;
			if (cityId != null) {
				isStayCityOurCityLookup = housingStay.City__c == null
					? true
					: housingStay.City__c != null && (String)housingStay.City__c == cityId ? true : false;
			}
			system.debug('current city:: ' + housingStay.City__c + 'current city:: ' + housingStay.City__r.Name);
			system.debug('inside city query');
			itinerary = new Itinerary(housingStay);
			for (Date itineraryDate : searchItinerariesMap.keySet()) {
				if (
					housingStay.Date_In__c != null &&
					((housingStay.Date_Out__c != null && itineraryDate >= housingStay.Date_In__c && itineraryDate <= housingStay.Date_Out__c) ||
					(housingStay.Date_In__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
				housingStay.Date_In_Text__c = housingStay.Date_In__c != null
					? Datetime.newInstance(housingStay.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
					: '';
				housingStay.Date_Out_Text__c = housingStay.Date_Out__c != null
					? Datetime.newInstance(housingStay.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
					: '';
				for (Housing__c roomType : housingStay.Housing__r) {
					roomType.Date_In_Text__c = roomType.Date_In__c != null
						? Datetime.newInstance(roomType.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
						: '';
					roomType.Date_Out_Text__c = roomType.Date_Out__c != null
						? Datetime.newInstance(roomType.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
						: '';
				}
			}
		}
		for (Ground__c groundSubtrip : [
			SELECT
				id,
				GT_Trip_Details__c,
				(
					SELECT
						id,
						GT_Sub_Trip_Details__c,
						Vehicle_Ref__c,
						Start_Date__c,
						Start_Date_Time__c,
						End_Date__c,
						End_Date_Time__c,
						Travel_Type__c,
						Group_Type__c,
						Location_Pick_up__c,
						Location_Drop_off__c,
						Location_Details__c,
						Location_Details_Drop_Off__c,
						Airline_Info_Special_Notes__c
					FROM GTTravels__r
					WHERE RecordType.DeveloperName = 'GT_Travel_Details'
					ORDER BY Line__c
				)
			FROM Ground__c
			WHERE
				Production_Ground__c = :opportunityId
				AND RecordType.DeveloperName = 'GT_Sub_Trip_Details'
				AND ((GT_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND GT_Trip_Details__r.Start_Date__c <= :Date.valueOf(endDate))
				OR (GT_Trip_Details__r.End_Date__c >= :Date.valueOf(startDate)
				AND GT_Trip_Details__r.End_Date__c <= :Date.valueOf(endDate))
				OR (GT_Trip_Details__r.Start_Date__c < :Date.valueOf(startDate)
				AND GT_Trip_Details__r.End_Date__c > :Date.valueOf(endDate))
				OR (GT_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND GT_Trip_Details__r.End_Date__c = NULL))
			ORDER BY Trip_Order__c
		]) {
			if (!groundSubtripDetailsMap.containsKey(groundSubtrip.GT_Trip_Details__c))
				groundSubtripDetailsMap.put(groundSubtrip.GT_Trip_Details__c, new List<Ground__c>());
			groundSubtripDetailsMap.get(groundSubtrip.GT_Trip_Details__c).add(groundSubtrip);
			for (Ground__c groundTravel : groundSubtrip.GTTravels__r) {
				groundTravel.Start_Date_Text__c = groundTravel.Start_Date__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.End_Date_Text__c = groundTravel.End_Date__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.Start_Date_Time_Text__c = groundTravel.Start_Date__c != null &&
					groundTravel.Start_Date_Time__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, groundTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				groundTravel.End_Date_Time_Text__c = groundTravel.End_Date__c != null &&
					groundTravel.End_Date_Time__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, groundTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.GT__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.GT__c = :groundSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Ground_Rate_Travel_Commission'
		])
			revenuesMap.put(rate.Bid__r.GT__c, rate);
		for (Ground__c groundTrip : [
			SELECT
				id,
				Name,
				Start_Date__c,
				End_Date__c,
				Status_Ground__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.ShippingStreet,
				Vendor_lookup__r.BillingCity,
				Vendor_lookup__r.BillingState,
				Vendor_lookup__r.BillingCountryCode,
				Vendor_lookup__r.Phone,
				Start_city__r.City__c,
				Start_city__r.State__c,
				(
					SELECT id, Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make_Model__c, Year__c, Amenities__c
					FROM Ground__r
					WHERE RecordType.DeveloperName = 'Vehicle_Type'
					ORDER BY Vehicle_Ref__c
				)
			FROM Ground__c
			WHERE
				Production_Ground__c = :opportunityId
				AND RecordType.DeveloperName = 'GT_Trip_Details'
				AND ((Start_Date__c >= :Date.valueOf(startDate)
				AND Start_Date__c <= :Date.valueOf(endDate))
				OR (End_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c <= :Date.valueOf(endDate))
				OR (Start_Date__c < :Date.valueOf(startDate)
				AND End_Date__c > :Date.valueOf(endDate))
				OR (Start_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c = NULL))
			ORDER BY Start_Date__c
		]) {
			itinerary = new Itinerary(groundTrip);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					groundTrip.Start_Date__c != null &&
					((groundTrip.End_Date__c != null && itineraryDate >= groundTrip.Start_Date__c && itineraryDate <= groundTrip.End_Date__c) ||
					(groundTrip.Start_Date__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			groundTrip.Start_Date_Text__c = groundTrip.Start_Date__c != null
				? Datetime.newInstance(groundTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			groundTrip.End_Date_Text__c = groundTrip.End_Date__c != null
				? Datetime.newInstance(groundTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (groundSubtripDetailsMap.containsKey(groundTrip.id))
				itinerary.relatedRecords = groundSubtripDetailsMap.get(groundTrip.id);
			if (revenuesMap.containsKey(groundTrip.id))
				groundTrip.Total_Price__c = revenuesMap.get(groundTrip.id).Total_Price__c;
		}
		for (Freight__c freightSubtrip : [
			SELECT
				id,
				Freight_Trip_Details__c,
				(
					SELECT
						id,
						Freight_Sub_Trip_Details__c,
						Vehicle_Ref__c,
						Start_Date__c,
						Start_Date_Time__c,
						End_Date__c,
						End_Date_Time__c,
						Travel_Type__c,
						Group_Type__c,
						Location_Pick_up__c,
						Location_Drop_off__c,
						Location_Details__c,
						Location_Details_Drop_Off__c,
						Airline_Info_Special_Notes__c,
						Freight_Truck_Sq_Ft__c
					FROM FreightEquipments__r
					WHERE RecordType.DeveloperName = 'Equipment_Details'
					ORDER BY Line__c
				)
			FROM Freight__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'
				AND ((Freight_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.Start_Date__c <= :Date.valueOf(endDate))
				OR (Freight_Trip_Details__r.End_Date__c >= :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.End_Date__c <= :Date.valueOf(endDate))
				OR (Freight_Trip_Details__r.Start_Date__c < :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.End_Date__c > :Date.valueOf(endDate))
				OR (Freight_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.End_Date__c = NULL))
			ORDER BY Trip_Order__c
		]) {
			if (!freightSubtripDetailsMap.containsKey(freightSubtrip.Freight_Trip_Details__c))
				freightSubtripDetailsMap.put(freightSubtrip.Freight_Trip_Details__c, new List<Freight__c>());
			freightSubtripDetailsMap.get(freightSubtrip.Freight_Trip_Details__c).add(freightSubtrip);
			for (Freight__c freightTravel : freightSubtrip.FreightEquipments__r) {
				freightTravel.Start_Date_Text__c = freightTravel.Start_Date__c != null
					? Datetime.newInstance(freightTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				freightTravel.End_Date_Text__c = freightTravel.End_Date__c != null
					? Datetime.newInstance(freightTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				freightTravel.Start_Date_Time_Text__c = freightTravel.Start_Date__c != null &&
					freightTravel.Start_Date_Time__c != null
					? Datetime.newInstance(freightTravel.Start_Date__c, freightTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				freightTravel.End_Date_Time_Text__c = freightTravel.End_Date__c != null &&
					freightTravel.End_Date_Time__c != null
					? Datetime.newInstance(freightTravel.End_Date__c, freightTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.Freight__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.Freight__c = :freightSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Freight_Rate_Commission'
		])
			revenuesMap.put(rate.Bid__r.Freight__c, rate);
		for (Freight__c freightTrip : [
			SELECT
				id,
				Name,
				Start_Date__c,
				End_Date__c,
				Status__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.BillingStreet,
				Vendor_lookup__r.BillingCity,
				Vendor_lookup__r.BillingState,
				Vendor_lookup__r.BillingCountryCode,
				Vendor_lookup__r.Phone,
				Start_city__r.City__c,
				Start_city__r.State__c,
				(
					SELECT
						id,
						Equipment__c,
						Vehicle_Ref__c,
						Vehicle_Type__c,
						Capacity__c,
						Make_Model__c,
						Year__c,
						Freight_Truck_Sq_Ft__c,
						Amenities__c
					FROM FreightSubTrips__r
					WHERE RecordType.DeveloperName = 'Vehicle_Type'
					ORDER BY Equipment__c
				)
			FROM Freight__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Freight_Trip_Details'
				AND ((Start_Date__c >= :Date.valueOf(startDate)
				AND Start_Date__c <= :Date.valueOf(endDate))
				OR (End_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c <= :Date.valueOf(endDate))
				OR (Start_Date__c < :Date.valueOf(startDate)
				AND End_Date__c > :Date.valueOf(endDate))
				OR (Start_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c = NULL))
			ORDER BY Start_Date__c
		]) {
			itinerary = new Itinerary(freightTrip);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					freightTrip.Start_Date__c != null &&
					((freightTrip.End_Date__c != null && itineraryDate >= freightTrip.Start_Date__c && itineraryDate <= freightTrip.End_Date__c) ||
					(freightTrip.Start_Date__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			freightTrip.Start_Date_Text__c = freightTrip.Start_Date__c != null
				? Datetime.newInstance(freightTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			freightTrip.End_Date_Text__c = freightTrip.End_Date__c != null
				? Datetime.newInstance(freightTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (freightSubtripDetailsMap.containsKey(freightTrip.id))
				itinerary.relatedRecords = freightSubtripDetailsMap.get(freightTrip.id);
			if (revenuesMap.containsKey(freightTrip.id))
				freightTrip.Total_Price__c = revenuesMap.get(freightTrip.id).Total_Price__c;
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.Air__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Air_Rate_Commission'
				AND ((Bid__r.Air__r.Departure_Date__c >= :Date.valueOf(startDate)
				AND Bid__r.Air__r.Departure_Date__c <= :Date.valueOf(endDate))
				OR (Bid__r.Air__r.Return_Date__c >= :Date.valueOf(startDate)
				AND Bid__r.Air__r.Return_Date__c <= :Date.valueOf(endDate))
				OR (Bid__r.Air__r.Departure_Date__c < :Date.valueOf(startDate)
				AND Bid__r.Air__r.Return_Date__c > :Date.valueOf(endDate))
				OR (Bid__r.Air__r.Departure_Date__c >= :Date.valueOf(startDate)
				AND Bid__r.Air__r.Return_Date__c = NULL))
				AND Deviation__c = NULL
		])
			revenuesMap.put(rate.Bid__r.Air__c, rate);
		System.debug(searchItinerariesMap);
		for (Air__c airTrip : [
			SELECT
				id,
				Name,
				Status__c,
				Departure_Date__c,
				Departure_City__r.Name,
				Departure_City__r.City__r.Name,
				Departure_City__r.City__r.City__c,
				Departure_City__r.City__r.State__c,
				Return_Date__c,
				Return_Departure_City__r.Name,
				Return_Departure_City__r.City__r.Name,
				Return_Arrival_City__r.Name,
				Return_Arrival_City__r.City__r.Name,
				Vendor__r.Name,
				Vendor__r.BillingStreet,
				Vendor__r.BillingCity,
				Vendor__r.BillingState,
				Vendor__r.BillingCountryCode,
				Vendor__r.Phone,
				(
					SELECT
						id,
						Departure_Date__c,
						Dep_Time__c,
						Departure_City__r.Name,
						Departure_City__r.City__r.City__c,
						Departure_City__r.City__r.State__c,
						Arrival_Date__c,
						Arr_Time__c,
						Arrival_City__r.Name,
						Arrival_City__r.City__r.City__c,
						Arrival_City__r.City__r.State__c,
						Flight_Duration_hrs__c,
						Flight_Duration_Mins__c,
						Number_of_Seats__c,
						Equip_Type__c
					FROM Air_Segments__r
					WHERE RecordType.DeveloperName = 'Air_Segments'
				)
			FROM Air__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Air_Trip_Details'
				AND ((Departure_Date__c >= :Date.valueOf(startDate)
				AND Departure_Date__c <= :Date.valueOf(endDate))
				OR (Return_Date__c >= :Date.valueOf(startDate)
				AND Return_Date__c <= :Date.valueOf(endDate))
				OR (Departure_Date__c < :Date.valueOf(startDate)
				AND Return_Date__c > :Date.valueOf(endDate))
				OR (Departure_Date__c >= :Date.valueOf(startDate)
				AND Return_Date__c = NULL))
			ORDER BY Departure_Date__c
		]) {
			itinerary = new Itinerary(airTrip);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					airTrip.Departure_Date__c != null &&
					((airTrip.Return_Date__c != null && itineraryDate >= airTrip.Departure_Date__c && itineraryDate <= airTrip.Return_Date__c) ||
					(airTrip.Departure_Date__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			airTrip.Departure_Date_Text__c = airTrip.Departure_Date__c != null
				? Datetime.newInstance(airTrip.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			airTrip.Return_Date_Text__c = airTrip.Return_Date__c != null
				? Datetime.newInstance(airTrip.Return_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Air__c airSegment : airTrip.Air_Segments__r) {
				airSegment.Departure_Date_Text__c = airSegment.Departure_Date__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Arrival_Date_Text__c = airSegment.Arrival_Date__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Dep_Time_Text__c = airSegment.Departure_Date__c != null &&
					airSegment.Dep_Time__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, airSegment.Dep_Time__c).format('h:mm a')
					: '';
				airSegment.Arr_Time_Text__c = airSegment.Arrival_Date__c != null &&
					airSegment.Arr_Time__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, airSegment.Arr_Time__c).format('h:mm a')
					: '';
			}
			if (revenuesMap.containsKey(airTrip.id))
				airTrip.Total_Price__c = revenuesMap.get(airTrip.id).Total_Price__c;
			System.debug(airTrip);
		}

		String theFilteredJSON = getFilteredItineraryRecordByCity(searchItinerariesMap,cityId);
		return theFilteredJSON;
	}**/

	/*
	@AuraEnabled
	public static String searchItinerariesWithCity(String opportunityId, String startDate, String endDate, String cityId) {
		system.debug('cityId :: ' + cityId);
		Map<Date, List<Itinerary>> searchItinerariesMap = new Map<Date, List<Itinerary>>();
		Map<Id, List<Ground__c>> groundSubtripDetailsMap = new Map<Id, List<Ground__c>>();
		Map<Id, List<Freight__c>> freightSubtripDetailsMap = new Map<Id, List<Freight__c>>();
		Map<Id, Revenue__c> revenuesMap = new Map<Id, Revenue__c>();
		Itinerary itinerary;
		for (Integer i = 0; i <= Date.valueOf(startDate).daysBetween(Date.valueOf(endDate)); i++)
			searchItinerariesMap.put(Date.valueOf(startDate).addDays(i), new List<Itinerary>());
		for (Housing__c housingStay : [
			SELECT
				id,
				Name,
				Date_In__c,
				Date_Out__c,
				Status_CC__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.ShippingStreet,
				Vendor_lookup__r.ShippingCity,
				Vendor_lookup__r.ShippingState,
				Vendor_lookup__r.ShippingCountryCode,
				Vendor_lookup__r.Phone,
				Venue__r.Name,
				City__r.City__c,
				City__r.State__c,
				(
					SELECT
						Id,
						Units__c,
						Unit_Type__c,
						Special_Notes__c,
						Date_In__c,
						Date_Out__c,
						Rate__c,
						Nights_CC__c,
						Sales_Housing__c,
						Room_Type__c
					FROM Housing__r
					WHERE RecordType.DeveloperName = 'Room_Types_Ops' AND Bid__c = NULL
					ORDER BY CreatedDate DESC
				)
			FROM Housing__c
			WHERE
				Production_CC__c = :opportunityId
				AND (RecordType.DeveloperName = 'Hotel_Housing'
				OR RecordType.DeveloperName = 'Corporate_Housing'
				OR RecordType.DeveloperName = 'Individual_Reservation')
				AND ((Date_In__c >= :Date.valueOf(startDate)
				AND Date_In__c <= :Date.valueOf(endDate))
				OR (Date_Out__c >= :Date.valueOf(startDate)
				AND Date_Out__c <= :Date.valueOf(endDate))
				OR (Date_In__c < :Date.valueOf(startDate)
				AND Date_Out__c > :Date.valueOf(endDate))
				OR (Date_In__c >= :Date.valueOf(startDate)
				AND Date_Out__c = NULL))
				AND City__c = :cityId
			ORDER BY Date_In__c
		]) {
			system.debug('cityId::: ' + cityId);
			system.debug('housingStay::: ' + housingStay);

			itinerary = new Itinerary(housingStay);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					housingStay.Date_In__c != null &&
					((housingStay.Date_Out__c != null && itineraryDate >= housingStay.Date_In__c && itineraryDate <= housingStay.Date_Out__c) ||
					(housingStay.Date_In__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			housingStay.Date_In_Text__c = housingStay.Date_In__c != null
				? Datetime.newInstance(housingStay.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			housingStay.Date_Out_Text__c = housingStay.Date_Out__c != null
				? Datetime.newInstance(housingStay.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Housing__c roomType : housingStay.Housing__r) {
				roomType.Date_In_Text__c = roomType.Date_In__c != null
					? Datetime.newInstance(roomType.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				roomType.Date_Out_Text__c = roomType.Date_Out__c != null
					? Datetime.newInstance(roomType.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
			}
		}
		for (Ground__c groundSubtrip : [
			SELECT
				id,
				GT_Trip_Details__c,
				(
					SELECT
						id,
						GT_Sub_Trip_Details__c,
						Vehicle_Ref__c,
						Start_Date__c,
						Start_Date_Time__c,
						End_Date__c,
						End_Date_Time__c,
						Travel_Type__c,
						Group_Type__c,
						Location_Pick_up__c,
						Location_Drop_off__c,
						Location_Details__c,
						Location_Details_Drop_Off__c,
						Airline_Info_Special_Notes__c
					FROM GTTravels__r
					WHERE RecordType.DeveloperName = 'GT_Travel_Details'
					ORDER BY Line__c
				)
			FROM Ground__c
			WHERE
				Production_Ground__c = :opportunityId
				AND RecordType.DeveloperName = 'GT_Sub_Trip_Details'
				AND ((GT_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND GT_Trip_Details__r.Start_Date__c <= :Date.valueOf(endDate))
				OR (GT_Trip_Details__r.End_Date__c >= :Date.valueOf(startDate)
				AND GT_Trip_Details__r.End_Date__c <= :Date.valueOf(endDate))
				OR (GT_Trip_Details__r.Start_Date__c < :Date.valueOf(startDate)
				AND GT_Trip_Details__r.End_Date__c > :Date.valueOf(endDate))
				OR (GT_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND GT_Trip_Details__r.End_Date__c = NULL))
			ORDER BY Trip_Order__c
		]) {
			if (!groundSubtripDetailsMap.containsKey(groundSubtrip.GT_Trip_Details__c))
				groundSubtripDetailsMap.put(groundSubtrip.GT_Trip_Details__c, new List<Ground__c>());
			groundSubtripDetailsMap.get(groundSubtrip.GT_Trip_Details__c).add(groundSubtrip);
			for (Ground__c groundTravel : groundSubtrip.GTTravels__r) {
				groundTravel.Start_Date_Text__c = groundTravel.Start_Date__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.End_Date_Text__c = groundTravel.End_Date__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.Start_Date_Time_Text__c = groundTravel.Start_Date__c != null &&
					groundTravel.Start_Date_Time__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, groundTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				groundTravel.End_Date_Time_Text__c = groundTravel.End_Date__c != null &&
					groundTravel.End_Date_Time__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, groundTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.GT__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.GT__c = :groundSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Ground_Rate_Travel_Commission'
		])
			revenuesMap.put(rate.Bid__r.GT__c, rate);
		for (Ground__c groundTrip : [
			SELECT
				id,
				Name,
				Start_Date__c,
				End_Date__c,
				Status_Ground__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.ShippingStreet,
				Vendor_lookup__r.BillingCity,
				Vendor_lookup__r.BillingState,
				Vendor_lookup__r.BillingCountryCode,
				Vendor_lookup__r.Phone,
				Start_city__r.City__c,
				Start_city__r.State__c,
				(
					SELECT id, Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make_Model__c, Year__c, Amenities__c
					FROM Ground__r
					WHERE RecordType.DeveloperName = 'Vehicle_Type'
					ORDER BY Vehicle_Ref__c
				)
			FROM Ground__c
			WHERE
				Production_Ground__c = :opportunityId
				AND RecordType.DeveloperName = 'GT_Trip_Details'
				AND ((Start_Date__c >= :Date.valueOf(startDate)
				AND Start_Date__c <= :Date.valueOf(endDate))
				OR (End_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c <= :Date.valueOf(endDate))
				OR (Start_Date__c < :Date.valueOf(startDate)
				AND End_Date__c > :Date.valueOf(endDate))
				OR (Start_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c = NULL))
				AND (Arriving_city__c = :cityId
				OR Start_City__c = :cityId)
			ORDER BY Start_Date__c
		]) {
			itinerary = new Itinerary(groundTrip);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					groundTrip.Start_Date__c != null &&
					((groundTrip.End_Date__c != null && itineraryDate >= groundTrip.Start_Date__c && itineraryDate <= groundTrip.End_Date__c) ||
					(groundTrip.Start_Date__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			groundTrip.Start_Date_Text__c = groundTrip.Start_Date__c != null
				? Datetime.newInstance(groundTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			groundTrip.End_Date_Text__c = groundTrip.End_Date__c != null
				? Datetime.newInstance(groundTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (groundSubtripDetailsMap.containsKey(groundTrip.id))
				itinerary.relatedRecords = groundSubtripDetailsMap.get(groundTrip.id);
			if (revenuesMap.containsKey(groundTrip.id))
				groundTrip.Total_Price__c = revenuesMap.get(groundTrip.id).Total_Price__c;
		}
		for (Freight__c freightSubtrip : [
			SELECT
				id,
				Freight_Trip_Details__c,
				(
					SELECT
						id,
						Freight_Sub_Trip_Details__c,
						Vehicle_Ref__c,
						Start_Date__c,
						Start_Date_Time__c,
						End_Date__c,
						End_Date_Time__c,
						Travel_Type__c,
						Group_Type__c,
						Location_Pick_up__c,
						Location_Drop_off__c,
						Location_Details__c,
						Location_Details_Drop_Off__c,
						Airline_Info_Special_Notes__c,
						Freight_Truck_Sq_Ft__c
					FROM FreightEquipments__r
					WHERE RecordType.DeveloperName = 'Equipment_Details'
					ORDER BY Line__c
				)
			FROM Freight__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Freight_Sub_Trip_Details'
				AND ((Freight_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.Start_Date__c <= :Date.valueOf(endDate))
				OR (Freight_Trip_Details__r.End_Date__c >= :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.End_Date__c <= :Date.valueOf(endDate))
				OR (Freight_Trip_Details__r.Start_Date__c < :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.End_Date__c > :Date.valueOf(endDate))
				OR (Freight_Trip_Details__r.Start_Date__c >= :Date.valueOf(startDate)
				AND Freight_Trip_Details__r.End_Date__c = NULL))
				AND (End_city__c = :cityId
				OR Start_City__c = :cityId)
			ORDER BY Trip_Order__c
		]) {
			if (!freightSubtripDetailsMap.containsKey(freightSubtrip.Freight_Trip_Details__c))
				freightSubtripDetailsMap.put(freightSubtrip.Freight_Trip_Details__c, new List<Freight__c>());
			freightSubtripDetailsMap.get(freightSubtrip.Freight_Trip_Details__c).add(freightSubtrip);
			for (Freight__c freightTravel : freightSubtrip.FreightEquipments__r) {
				freightTravel.Start_Date_Text__c = freightTravel.Start_Date__c != null
					? Datetime.newInstance(freightTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				freightTravel.End_Date_Text__c = freightTravel.End_Date__c != null
					? Datetime.newInstance(freightTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				freightTravel.Start_Date_Time_Text__c = freightTravel.Start_Date__c != null &&
					freightTravel.Start_Date_Time__c != null
					? Datetime.newInstance(freightTravel.Start_Date__c, freightTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				freightTravel.End_Date_Time_Text__c = freightTravel.End_Date__c != null &&
					freightTravel.End_Date_Time__c != null
					? Datetime.newInstance(freightTravel.End_Date__c, freightTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.Freight__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.Freight__c = :freightSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Freight_Rate_Commission'
		])
			revenuesMap.put(rate.Bid__r.Freight__c, rate);
		for (Freight__c freightTrip : [
			SELECT
				id,
				Name,
				Start_Date__c,
				End_Date__c,
				Status__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.BillingStreet,
				Vendor_lookup__r.BillingCity,
				Vendor_lookup__r.BillingState,
				Vendor_lookup__r.BillingCountryCode,
				Vendor_lookup__r.Phone,
				Start_city__r.City__c,
				Start_city__r.State__c,
				(
					SELECT
						id,
						Equipment__c,
						Vehicle_Ref__c,
						Vehicle_Type__c,
						Capacity__c,
						Make_Model__c,
						Year__c,
						Freight_Truck_Sq_Ft__c,
						Amenities__c
					FROM FreightSubTrips__r
					WHERE RecordType.DeveloperName = 'Vehicle_Type'
					ORDER BY Equipment__c
				)
			FROM Freight__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Freight_Trip_Details'
				AND ((Start_Date__c >= :Date.valueOf(startDate)
				AND Start_Date__c <= :Date.valueOf(endDate))
				OR (End_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c <= :Date.valueOf(endDate))
				OR (Start_Date__c < :Date.valueOf(startDate)
				AND End_Date__c > :Date.valueOf(endDate))
				OR (Start_Date__c >= :Date.valueOf(startDate)
				AND End_Date__c = NULL))
				AND (End_city__c = :cityId
				OR Start_City__c = :cityId)
			ORDER BY Start_Date__c
		]) {
			itinerary = new Itinerary(freightTrip);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					freightTrip.Start_Date__c != null &&
					((freightTrip.End_Date__c != null && itineraryDate >= freightTrip.Start_Date__c && itineraryDate <= freightTrip.End_Date__c) ||
					(freightTrip.Start_Date__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			freightTrip.Start_Date_Text__c = freightTrip.Start_Date__c != null
				? Datetime.newInstance(freightTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			freightTrip.End_Date_Text__c = freightTrip.End_Date__c != null
				? Datetime.newInstance(freightTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (freightSubtripDetailsMap.containsKey(freightTrip.id))
				itinerary.relatedRecords = freightSubtripDetailsMap.get(freightTrip.id);
			if (revenuesMap.containsKey(freightTrip.id))
				freightTrip.Total_Price__c = revenuesMap.get(freightTrip.id).Total_Price__c;
		}
		for (Revenue__c rate : [
			SELECT id, Bid__r.Air__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Air_Rate_Commission'
				AND ((Bid__r.Air__r.Departure_Date__c >= :Date.valueOf(startDate)
				AND Bid__r.Air__r.Departure_Date__c <= :Date.valueOf(endDate))
				OR (Bid__r.Air__r.Return_Date__c >= :Date.valueOf(startDate)
				AND Bid__r.Air__r.Return_Date__c <= :Date.valueOf(endDate))
				OR (Bid__r.Air__r.Departure_Date__c < :Date.valueOf(startDate)
				AND Bid__r.Air__r.Return_Date__c > :Date.valueOf(endDate))
				OR (Bid__r.Air__r.Departure_Date__c >= :Date.valueOf(startDate)
				AND Bid__r.Air__r.Return_Date__c = NULL))
				AND Deviation__c = NULL
		])
			revenuesMap.put(rate.Bid__r.Air__c, rate);
		System.debug(searchItinerariesMap);
		for (Air__c airTrip : [
			SELECT
				id,
				Name,
				Status__c,
				Departure_Date__c,
				Departure_City__r.Name,
				Departure_City__r.City__r.Name,
				Departure_City__r.City__r.City__c,
				Departure_City__r.City__r.State__c,
				Return_Date__c,
				Return_Departure_City__r.Name,
				Return_Departure_City__r.City__r.Name,
				Return_Arrival_City__r.Name,
				Return_Arrival_City__r.City__r.Name,
				Vendor__r.Name,
				Vendor__r.BillingStreet,
				Vendor__r.BillingCity,
				Vendor__r.BillingState,
				Vendor__r.BillingCountryCode,
				Vendor__r.Phone,
				(
					SELECT
						id,
						Departure_Date__c,
						Dep_Time__c,
						Departure_City__r.Name,
						Departure_City__r.City__r.City__c,
						Departure_City__r.City__r.State__c,
						Arrival_Date__c,
						Arr_Time__c,
						Arrival_City__r.Name,
						Arrival_City__r.City__r.City__c,
						Arrival_City__r.City__r.State__c,
						Flight_Duration_hrs__c,
						Flight_Duration_Mins__c,
						Number_of_Seats__c,
						Equip_Type__c
					FROM Air_Segments__r
					WHERE RecordType.DeveloperName = 'Air_Segments'
				)
			FROM Air__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Air_Trip_Details'
				AND ((Departure_Date__c >= :Date.valueOf(startDate)
				AND Departure_Date__c <= :Date.valueOf(endDate))
				OR (Return_Date__c >= :Date.valueOf(startDate)
				AND Return_Date__c <= :Date.valueOf(endDate))
				OR (Departure_Date__c < :Date.valueOf(startDate)
				AND Return_Date__c > :Date.valueOf(endDate))
				OR (Departure_Date__c >= :Date.valueOf(startDate)
				AND Return_Date__c = NULL))
				AND (Arrival_City__r.City__c = :cityId
				OR Return_Departure_City__r.City__c = :cityId)
			ORDER BY Departure_Date__c
		]) {
			itinerary = new Itinerary(airTrip);
			for (Date itineraryDate : searchItinerariesMap.keySet())
				if (
					airTrip.Departure_Date__c != null &&
					((airTrip.Return_Date__c != null && itineraryDate >= airTrip.Departure_Date__c && itineraryDate <= airTrip.Return_Date__c) ||
					(airTrip.Departure_Date__c == itineraryDate))
				)
					searchItinerariesMap.get(itineraryDate).add(itinerary);
			airTrip.Departure_Date_Text__c = airTrip.Departure_Date__c != null
				? Datetime.newInstance(airTrip.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			airTrip.Return_Date_Text__c = airTrip.Return_Date__c != null
				? Datetime.newInstance(airTrip.Return_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Air__c airSegment : airTrip.Air_Segments__r) {
				airSegment.Departure_Date_Text__c = airSegment.Departure_Date__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Arrival_Date_Text__c = airSegment.Arrival_Date__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Dep_Time_Text__c = airSegment.Departure_Date__c != null &&
					airSegment.Dep_Time__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, airSegment.Dep_Time__c).format('h:mm a')
					: '';
				airSegment.Arr_Time_Text__c = airSegment.Arrival_Date__c != null &&
					airSegment.Arr_Time__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, airSegment.Arr_Time__c).format('h:mm a')
					: '';
			}
			if (revenuesMap.containsKey(airTrip.id))
				airTrip.Total_Price__c = revenuesMap.get(airTrip.id).Total_Price__c;
			System.debug(airTrip);
		}
		//System.debug(JSON.serialize(searchItinerariesMap));
		return JSON.serialize(searchItinerariesMap);
	}
	*/

	/*
	@AuraEnabled
	public static String searchItinerariesUsingCity(String opportunityId, String cityId) {
		Map<Date, List<Itinerary>> searchItinerariesMap = new Map<Date, List<Itinerary>>();
		Map<Id, List<Ground__c>> groundSubtripDetailsMap = new Map<Id, List<Ground__c>>();
		Map<Id, List<Freight__c>> freightSubtripDetailsMap = new Map<Id, List<Freight__c>>();
		Map<Id, Revenue__c> revenuesMap = new Map<Id, Revenue__c>();
		Itinerary itinerary;

		for (Housing__c housingStay : [
			SELECT
				id,
				Name,
				Date_In__c,
				Date_Out__c,
				Status_CC__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.ShippingStreet,
				Vendor_lookup__r.ShippingCity,
				Vendor_lookup__r.ShippingState,
				Vendor_lookup__r.ShippingCountryCode,
				Vendor_lookup__r.Phone,
				Venue__r.Name,
				City__r.City__c,
				City__r.State__c,
				(
					SELECT
						Id,
						Units__c,
						Unit_Type__c,
						Special_Notes__c,
						Date_In__c,
						Date_Out__c,
						Rate__c,
						Nights_CC__c,
						Sales_Housing__c,
						Room_Type__c
					FROM Housing__r
					WHERE RecordType.DeveloperName = 'Room_Types_Ops' AND Bid__c = NULL
					ORDER BY CreatedDate DESC
				)
			FROM Housing__c
			WHERE
				Production_CC__c = :opportunityId
				AND (RecordType.DeveloperName = 'Hotel_Housing'
				OR RecordType.DeveloperName = 'Corporate_Housing'
				OR RecordType.DeveloperName = 'Individual_Reservation')
				AND City__c = :cityId
			ORDER BY Date_In__c
		]) {
			itinerary = new Itinerary(housingStay);
			if (housingStay.Date_In__c != null) {
				if (searchItinerariesMap.containsKey(housingStay.Date_In__c)) {
					searchItinerariesMap.get(housingStay.Date_In__c).add(itinerary);
				} else {
					searchItinerariesMap.put(housingStay.Date_In__c, new List<Itinerary>{ itinerary });
				}
			}

			housingStay.Date_In_Text__c = housingStay.Date_In__c != null
				? Datetime.newInstance(housingStay.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			housingStay.Date_Out_Text__c = housingStay.Date_Out__c != null
				? Datetime.newInstance(housingStay.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Housing__c roomType : housingStay.Housing__r) {
				roomType.Date_In_Text__c = roomType.Date_In__c != null
					? Datetime.newInstance(roomType.Date_In__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				roomType.Date_Out_Text__c = roomType.Date_Out__c != null
					? Datetime.newInstance(roomType.Date_Out__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
			}
		}

		for (Ground__c groundSubtrip : [
			SELECT
				id,
				GT_Trip_Details__c,
				(
					SELECT
						id,
						GT_Sub_Trip_Details__c,
						Vehicle_Ref__c,
						Start_Date__c,
						Start_Date_Time__c,
						End_Date__c,
						End_Date_Time__c,
						Travel_Type__c,
						Group_Type__c,
						Location_Pick_up__c,
						Location_Drop_off__c,
						Location_Details__c,
						Location_Details_Drop_Off__c,
						Airline_Info_Special_Notes__c
					FROM GTTravels__r
					WHERE RecordType.DeveloperName = 'GT_Travel_Details'
					ORDER BY Line__c
				)
			FROM Ground__c
			WHERE
				Production_Ground__c = :opportunityId
				AND RecordType.DeveloperName = 'GT_Sub_Trip_Details'
				AND (Arriving_city__c = :cityId
				OR Start_City__c = :cityId)
			ORDER BY Trip_Order__c
		]) {
			if (!groundSubtripDetailsMap.containsKey(groundSubtrip.GT_Trip_Details__c))
				groundSubtripDetailsMap.put(groundSubtrip.GT_Trip_Details__c, new List<Ground__c>());
			groundSubtripDetailsMap.get(groundSubtrip.GT_Trip_Details__c).add(groundSubtrip);
			for (Ground__c groundTravel : groundSubtrip.GTTravels__r) {
				groundTravel.Start_Date_Text__c = groundTravel.Start_Date__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.End_Date_Text__c = groundTravel.End_Date__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				groundTravel.Start_Date_Time_Text__c = groundTravel.Start_Date__c != null &&
					groundTravel.Start_Date_Time__c != null
					? Datetime.newInstance(groundTravel.Start_Date__c, groundTravel.Start_Date_Time__c).format('h:mm a')
					: '';
				groundTravel.End_Date_Time_Text__c = groundTravel.End_Date__c != null &&
					groundTravel.End_Date_Time__c != null
					? Datetime.newInstance(groundTravel.End_Date__c, groundTravel.End_Date_Time__c).format('h:mm a')
					: '';
			}
		}

		for (Revenue__c rate : [
			SELECT id, Bid__r.GT__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.GT__c = :groundSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Ground_Rate_Travel_Commission'
		])
			revenuesMap.put(rate.Bid__r.GT__c, rate);

		for (Ground__c groundTrip : [
			SELECT
				id,
				Name,
				Start_Date__c,
				End_Date__c,
				Status_Ground__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.ShippingStreet,
				Vendor_lookup__r.BillingCity,
				Vendor_lookup__r.BillingState,
				Vendor_lookup__r.BillingCountryCode,
				Vendor_lookup__r.Phone,
				Start_city__r.City__c,
				Start_city__r.State__c,
				(
					SELECT id, Name, Vehicle_Ref__c, Vehicle_Type__c, Capacity__c, Make_Model__c, Year__c, Amenities__c
					FROM Ground__r
					WHERE RecordType.DeveloperName = 'Vehicle_Type'
					ORDER BY Vehicle_Ref__c
				)
			FROM Ground__c
			WHERE
				Production_Ground__c = :opportunityId
				AND RecordType.DeveloperName = 'GT_Trip_Details'
				AND (Arriving_city__c = :cityId
				OR Start_City__c = :cityId)
			ORDER BY Start_Date__c
		]) {
			itinerary = new Itinerary(groundTrip);
			if (groundTrip.Start_Date__c != null) {
				if (searchItinerariesMap.containsKey(groundTrip.Start_Date__c)) {
					searchItinerariesMap.get(groundTrip.Start_Date__c).add(itinerary);
				} else {
					searchItinerariesMap.put(groundTrip.Start_Date__c, new List<Itinerary>{ itinerary });
				}
			}
			groundTrip.Start_Date_Text__c = groundTrip.Start_Date__c != null
				? Datetime.newInstance(groundTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			groundTrip.End_Date_Text__c = groundTrip.End_Date__c != null
				? Datetime.newInstance(groundTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (groundSubtripDetailsMap.containsKey(groundTrip.id))
				itinerary.relatedRecords = groundSubtripDetailsMap.get(groundTrip.id);
			if (revenuesMap.containsKey(groundTrip.id))
				groundTrip.Total_Price__c = revenuesMap.get(groundTrip.id).Total_Price__c;
		}

		for (Revenue__c rate : [
			SELECT id, Bid__r.Freight__c, Total_Price__c
			FROM Revenue__c
			WHERE
				Bid__r.Freight__c = :freightSubtripDetailsMap.keySet()
				AND Bid__r.Status__c = 'Contracted'
				AND RecordType.DeveloperName = 'Freight_Rate_Commission'
		])
			revenuesMap.put(rate.Bid__r.Freight__c, rate);
		for (Freight__c freightTrip : [
			SELECT
				id,
				Name,
				Start_Date__c,
				End_Date__c,
				Status__c,
				Vendor_lookup__r.Name,
				Vendor_lookup__r.BillingStreet,
				Vendor_lookup__r.BillingCity,
				Vendor_lookup__r.BillingState,
				Vendor_lookup__r.BillingCountryCode,
				Vendor_lookup__r.Phone,
				Start_city__r.City__c,
				Start_city__r.State__c,
				(
					SELECT
						id,
						Equipment__c,
						Vehicle_Ref__c,
						Vehicle_Type__c,
						Capacity__c,
						Make_Model__c,
						Year__c,
						Freight_Truck_Sq_Ft__c,
						Amenities__c
					FROM FreightSubTrips__r
					WHERE RecordType.DeveloperName = 'Vehicle_Type'
					ORDER BY Equipment__c
				)
			FROM Freight__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Freight_Trip_Details'
				AND (End_city__c = :cityId
				OR Start_City__c = :cityId)
			ORDER BY Start_Date__c
		]) {
			itinerary = new Itinerary(freightTrip);
			if (freightTrip.Start_Date__c != null) {
				if (searchItinerariesMap.containsKey(freightTrip.Start_Date__c)) {
					searchItinerariesMap.get(freightTrip.Start_Date__c).add(itinerary);
				} else {
					searchItinerariesMap.put(freightTrip.Start_Date__c, new List<Itinerary>{ itinerary });
				}
			}
			freightTrip.Start_Date_Text__c = freightTrip.Start_Date__c != null
				? Datetime.newInstance(freightTrip.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			freightTrip.End_Date_Text__c = freightTrip.End_Date__c != null
				? Datetime.newInstance(freightTrip.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			if (freightSubtripDetailsMap.containsKey(freightTrip.id))
				itinerary.relatedRecords = freightSubtripDetailsMap.get(freightTrip.id);
			if (revenuesMap.containsKey(freightTrip.id))
				freightTrip.Total_Price__c = revenuesMap.get(freightTrip.id).Total_Price__c;
		}

		for (Revenue__c rate : [
			SELECT id, Bid__r.Air__c, Total_Price__c
			FROM Revenue__c
			WHERE Bid__r.Production__c = :opportunityId AND RecordType.DeveloperName = 'Air_Rate_Commission' AND Deviation__c = NULL
		])
			revenuesMap.put(rate.Bid__r.Air__c, rate);
		System.debug(searchItinerariesMap);
		for (Air__c airTrip : [
			SELECT
				id,
				Name,
				Status__c,
				Departure_Date__c,
				Departure_City__r.Name,
				Departure_City__r.City__r.Name,
				Departure_City__r.City__r.City__c,
				Departure_City__r.City__r.State__c,
				Return_Date__c,
				Return_Departure_City__r.Name,
				Return_Departure_City__r.City__r.Name,
				Return_Arrival_City__r.Name,
				Return_Arrival_City__r.City__r.Name,
				Vendor__r.Name,
				Vendor__r.BillingStreet,
				Vendor__r.BillingCity,
				Vendor__r.BillingState,
				Vendor__r.BillingCountryCode,
				Vendor__r.Phone,
				(
					SELECT
						id,
						Departure_Date__c,
						Dep_Time__c,
						Departure_City__r.Name,
						Departure_City__r.City__r.City__c,
						Departure_City__r.City__r.State__c,
						Arrival_Date__c,
						Arr_Time__c,
						Arrival_City__r.Name,
						Arrival_City__r.City__r.City__c,
						Arrival_City__r.City__r.State__c,
						Flight_Duration_hrs__c,
						Flight_Duration_Mins__c,
						Number_of_Seats__c,
						Equip_Type__c
					FROM Air_Segments__r
					WHERE RecordType.DeveloperName = 'Air_Segments'
				)
			FROM Air__c
			WHERE
				Production__c = :opportunityId
				AND RecordType.DeveloperName = 'Air_Trip_Details'
				AND (Arrival_City__r.City__c = :cityId
				OR Return_Departure_City__r.City__c = :cityId)
			ORDER BY Departure_Date__c
		]) {
			itinerary = new Itinerary(airTrip);
			if (airTrip.Departure_Date__c != null) {
				if (searchItinerariesMap.containsKey(airTrip.Departure_Date__c)) {
					searchItinerariesMap.get(airTrip.Departure_Date__c).add(itinerary);
				} else {
					searchItinerariesMap.put(airTrip.Departure_Date__c, new List<Itinerary>{ itinerary });
				}
			}
			airTrip.Departure_Date_Text__c = airTrip.Departure_Date__c != null
				? Datetime.newInstance(airTrip.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			airTrip.Return_Date_Text__c = airTrip.Return_Date__c != null
				? Datetime.newInstance(airTrip.Return_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd MMM yyyy')
				: '';
			for (Air__c airSegment : airTrip.Air_Segments__r) {
				airSegment.Departure_Date_Text__c = airSegment.Departure_Date__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Arrival_Date_Text__c = airSegment.Arrival_Date__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, Time.newInstance(0, 0, 0, 0)).format('EEE, dd MMM yyyy')
					: '';
				airSegment.Dep_Time_Text__c = airSegment.Departure_Date__c != null &&
					airSegment.Dep_Time__c != null
					? Datetime.newInstance(airSegment.Departure_Date__c, airSegment.Dep_Time__c).format('h:mm a')
					: '';
				airSegment.Arr_Time_Text__c = airSegment.Arrival_Date__c != null &&
					airSegment.Arr_Time__c != null
					? Datetime.newInstance(airSegment.Arrival_Date__c, airSegment.Arr_Time__c).format('h:mm a')
					: '';
			}
			if (revenuesMap.containsKey(airTrip.id))
				airTrip.Total_Price__c = revenuesMap.get(airTrip.id).Total_Price__c;
			System.debug(airTrip);
		}
		//System.debug(JSON.serialize(searchItinerariesMap));
		return JSON.serialize(searchItinerariesMap);
	}
	*/

	public class Itinerary {
		@AuraEnabled
		public SObject record { get; set; }
		@AuraEnabled
		public List<SObject> relatedRecords { get; set; }
		public Itinerary(SObject record, List<SObject> relatedRecords) {
			this.record = record;
			this.relatedRecords = relatedRecords;
		}
		public Itinerary(SObject record) {
			this.record = record;
			this.relatedRecords = new List<SObject>();
		}
	}

	public static String getFilteredItineraryRecordByCity(Map<Date, List<Itinerary>> searchItinerariesMap, String city){
		// takes a list of sobjects and checks the list of api names passed in
		List<SObject> filteredRecordsByCity = new List<SObject>();

		// get the related records from the Itinerary
		//Map<Date, List<Itinerary>> searchItinerariesMap = new Map<Date, List<Itinerary>>();
		//searchItinerariesMap = (Map<Date, List<Itinerary>>)JSON.deserialize(itinMap, Map<Date, List<Itinerary>>.class);
		Map<Date, List<Itinerary>> newItinMap = new Map<Date, List<Itinerary>>();
		for(Date d : searchItinerariesMap.keySet()){
			newItinMap.put(d,searchItinerariesMap.get(d));
			List<Itinerary> theItins = new List<Itinerary>();

			for(Itinerary itin : searchItinerariesMap.get(d)) {
				/*
				filteredRecordsByCity = new List<SObject>();

				List<String> theFields = new List<String>{'City__c'};
				
				SObject record = itin.record;
				Boolean keepme = false;
				Map<String, Object> fieldsToValue = record.getPopulatedFieldsAsMap();
					system.debug('fieldsToValue keyset :: ' + fieldsToValue.keySet());
					for (String field : fieldsToValue.keySet()){
						Object theValue = fieldsToValue.get(field);
						if (field.contains('City')) {
							if (String.valueOf(theValue) == city) {
								system.debug('field :: ' + field);
								system.debug('fieldsToValue.get :: ' + fieldsToValue.get(field));
								keepme = true;
								break;
							} else {
								keepme = false;
							}
						}
					}
					if (keepme = true) {
						theItins.add(itin);
					} else {
						break;
					}
				system.debug('filteredRecordsByCity : ' + searchItinerariesMap.size());
					*/
			
				//itin.relatedRecords = filteredRecordsByCity;
				system.debug('here it is ::: ' + itin);
				String theItinerary = itin.toString();
				if (theItinerary.contains(city)) {
					theItins.add(itin);
				}
			}
			newItinMap.put(d,theItins);
		}

		return JSON.serialize(newItinMap);
	}

	public static List<SObject> getObjectsFromItinerary(String itinMap, String city){
		// takes a list of sobjects and checks the list of api names passed in
		List<SObject> filteredRecords = new List<SObject>();

		// get the related records from the Itinerary
		Map<Date, List<Itinerary>> searchItinerariesMap = new Map<Date, List<Itinerary>>();
		searchItinerariesMap = (Map<Date, List<Itinerary>>)JSON.deserialize(itinMap, Map<Date, List<Itinerary>>.class);

		for(Date d : searchItinerariesMap.keySet()){
			for(Itinerary itin : searchItinerariesMap.get(d)) {
				SObject record = itin.record;
				filteredRecords.add(record);
				if (itin.relatedRecords != null) {
					filteredRecords.addAll(itin.relatedRecords);
				}
			}
		}

		return filteredRecords;
	}
}
```


# Last Modified


# Usage

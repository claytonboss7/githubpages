---
layout: default
title: VoyajerItinerary
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerItinerary
## Fields
### VoyajerItineraryController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        component.set('v.today', today);
        var userId = $A.get("$SObjectType.CurrentUser.Id");
        component.set("v.userId",userId);
        component.set("v.menuSelected","");
        component.set("v.itineraryData",{services:""});
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadProductionServices");
        callToParent.fire();
	},
    
    loadItineraryData : function(component, event, helper) {
        function isEmpty(obj) {
            for(var key in obj) if(obj.hasOwnProperty(key)) return false;
            return true;
        }
        var menuSelected = component.get("v.menuSelected");
        var itineraryData = component.get("v.itineraryData");
        console.log(JSON.parse(JSON.stringify(itineraryData)));
        if(!!menuSelected) {
            var servicesSaved = itineraryData.services;
            switch (menuSelected) {
                case "services":
                    if(servicesSaved.includes("Housing")) component.set("v.isLodgingSelected",true);
                    component.set("v.isLodgingLocked",itineraryData.isLodgingLocked);
                    if(servicesSaved.includes("Ground Travel")) component.set("v.isGroundSelected",true);
                    component.set("v.isGroundLocked",itineraryData.isGroundLocked);
                    if(servicesSaved.includes("Air")) component.set("v.isAirSelected",true);
                    component.set("v.isAirLocked",itineraryData.isAirLocked);
                    if(servicesSaved.includes("Freight")) component.set("v.isFreightSelected",true);
                    component.set("v.isFreightLocked",itineraryData.isFreightLocked);
                    break;
                case "housing":
                    if(!itineraryData.hasOwnProperty("lodgingRecords")) {
                        console.log("loadItineraryData->loadLodgingPage");
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadLodgingPage");
                        callToParent.fire();
                    }
                    else {
                        console.log("loadItineraryData->setLodgingPage");
                        var lodgingRecords = JSON.parse(JSON.stringify(itineraryData.lodgingRecords));
                        if(itineraryData.hasOwnProperty("salesForHousing")) {
                            component.set("v.salesForHousing",itineraryData.salesForHousing);
                            component.set("v.salesHousingRoomTypes",itineraryData.salesHousingRoomTypes);
                            component.set("v.salesHousingConcessions",itineraryData.salesHousingConcessions);
                        } else if(isEmpty(component.get("v.salesForHousing"))) {
                            component.set("v.salesForHousing",{});
                            component.set("v.salesHousingRoomTypes",[]);
                            component.set("v.salesHousingConcessions",[]);
                        }
                        component.set("v.lodgingRecords",lodgingRecords);
                        component.set("v.distanceFromEventOptions",itineraryData.distanceFromEventOptions);
                        component.set("v.hotelStars",itineraryData.hotelStars);
                        component.set("v.hotelTypes",itineraryData.hotelTypes);
                        component.set("v.preferredBrands",itineraryData.preferredBrands);
                        component.set("v.roomTypes",itineraryData.roomTypes);
                        component.set("v.concessionHousingTypes",itineraryData.concessionHousingTypes);
                        component.set("v.concessionCorporateTypes",itineraryData.concessionCorporateTypes);
                    }
                    break;
                case "ground":
                    if(!itineraryData.hasOwnProperty("groundRecords")) {
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadGroundPage");
                        callToParent.fire();
                    }
                    else {
                        var groundRecords = JSON.parse(JSON.stringify(itineraryData.groundRecords));
                        if(itineraryData.hasOwnProperty("salesForGround")) component.set("v.salesForGround",itineraryData.salesForGround);
                        else if(isEmpty(component.get("v.salesForGround"))) component.set("v.salesForGround",{});
                        component.set("v.groundRecords",groundRecords);
                        component.set("v.tripTypesGround",itineraryData.tripTypesGround);
                        component.set("v.locationPickUpTypes",itineraryData.locationPickUpTypes);
                        component.set("v.locationDropOffTypes",itineraryData.locationDropOffTypes);
                        component.set("v.vehicleTypesGround",itineraryData.vehicleTypesGround);
                        component.set("v.groupTypesGround",itineraryData.groupTypesGround);
                        component.set("v.amenitiesGround",itineraryData.amenitiesGround);
                    }
                    break;
                case "air":
                    if(!itineraryData.hasOwnProperty("flightRecords")) {
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadAirPage");
                        callToParent.fire();
                    }
                    else {
                        var flightRecords = JSON.parse(JSON.stringify(itineraryData.flightRecords));
                        if(itineraryData.hasOwnProperty("salesForAir")) component.set("v.salesForAir",itineraryData.salesForAir);
                        else if(isEmpty(component.get("v.salesForAir"))) component.set("v.salesForAir",{});
                        component.set("v.classServicesAir",itineraryData.classServicesAir);
                        component.set("v.preferredAirlinesAir",itineraryData.preferredAirlinesAir);
                        component.set("v.flightRecords",flightRecords);
                    }
                    break;
                case "freight":
                    if(!itineraryData.hasOwnProperty("freightRecords")) {
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadFreightPage");
                        callToParent.fire();
                    }
                    else {
                        var freightRecords = JSON.parse(JSON.stringify(itineraryData.freightRecords));
                        if(itineraryData.hasOwnProperty("salesForFreight")) component.set("v.salesForFreight",itineraryData.salesForFreight);
                        else if(isEmpty(component.get("v.salesForFreight"))) component.set("v.salesForFreight",{});
                        component.set("v.groupTypesFreight",itineraryData.groupTypesFreight);
                        component.set("v.freightRecords",freightRecords);
                    }
                    break;
                default:
                    break;
            }
            var menuOptions = component.get("v.menuOptions");
            var menuOptionsSelected = [{ label: "Select Services", value: "services", icon: "fa-hand-pointer", checked: true }];
            if(menuOptions.length < 2) {
                var checked = true;
                if(menuSelected == "services") checked = false;
                if(servicesSaved.includes("Housing")) menuOptionsSelected.push({ label: "Lodging", value: "housing", icon: "fa-home", checked: checked });
                if(menuSelected == "housing") checked = false;
                if(servicesSaved.includes("Ground Travel")) menuOptionsSelected.push({ label: "Ground Travel", value: "ground", icon: "fa-car", checked: checked });
                if(menuSelected == "ground") checked = false;
                if(servicesSaved.includes("Air")) menuOptionsSelected.push({ label: "Air Travel", value: "air", icon: "fa-plane", checked: checked });
                if(menuSelected == "air") checked = false;
                if(servicesSaved.includes("Freight")) menuOptionsSelected.push({ label: "Freight", value: "freight", icon: "fa-truck", checked: checked });
                if(menuSelected == "freight") checked = false;
                if(menuOptionsSelected.length>1) menuOptionsSelected.push({ label: "Review & Submit", value: "review", icon: "fa-paper-plane", checked: checked });
                menuOptions = menuOptionsSelected.slice(0);
            } else {
                menuOptions.forEach(item => { if(item.value == menuSelected) item.checked = true; })
            }
            component.set("v.menuOptions",menuOptions);
        }
    },
    
    toggleItineraryService : function(component, event, helper) {
        var service = event.getSource().get("v.alternativeText");
        var servicesSaved = component.get("v.itineraryData").services;
        var toastEvent = $A.get("e.force:showToast");
        toastEvent.setParams({ type: "error", title: "", message: "You are not able to unselect services that have itineraries created for them. Please contact your Road Rebel Coordinator." });
        if(service.toLowerCase() == "lodging") { if(component.get("v.isLodgingSelected") && component.get("v.isLodgingLocked")) toastEvent.fire(); else  component.set("v.isLodgingSelected",!component.get("v.isLodgingSelected")); }
        if(service.toLowerCase() == "ground travel") { if(component.get("v.isGroundSelected") && component.get("v.isGroundLocked")) toastEvent.fire(); else component.set("v.isGroundSelected",!component.get("v.isGroundSelected")); }
        if(service.toLowerCase() == "air travel") { if(component.get("v.isAirSelected") && component.get("v.isAirLocked")) toastEvent.fire(); else component.set("v.isAirSelected",!component.get("v.isAirSelected")); }
        if(service.toLowerCase() == "freight") { if(component.get("v.isFreightSelected") && component.get("v.isFreightLocked")) toastEvent.fire(); else component.set("v.isFreightSelected",!component.get("v.isFreightSelected")); }
    },
    
    saveServices : function(component, event, helper) {
        var servicesSelected = "";
        if(component.get("v.isLodgingSelected")) servicesSelected += "Housing;";
        if(component.get("v.isGroundSelected")) servicesSelected += "Ground Travel;";
        if(component.get("v.isAirSelected")) servicesSelected += "Air;";
        if(component.get("v.isFreightSelected")) servicesSelected += "Freight;";
        if(servicesSelected.length==0) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "You need to select at least one service"
            });
            toastEvent.fire();
        } else {
            var callToParent = component.getEvent("callToParent");
            component.set("v.menuOptions",[]);
            callToParent.setParam("action","saveServices");
            callToParent.setParam("data",{ productionId: component.get("v.productionSelected"), services: servicesSelected});
            callToParent.fire();
        }
    },
    
    handleNewDates : function(component, event, helper) {
        function isEmpty(obj) {
            for(var key in obj) if(obj.hasOwnProperty(key)) return false;
            return true;
        }
        var itineraryData = component.get("v.itineraryData");
        var menuSelected = component.get("v.menuSelected");
        var index = -1;
        switch (menuSelected) {
            case "housing":
                var lodgingRecords = component.get("v.lodgingRecords");
                index = lodgingRecords.length;
                var salesForHousing = component.get("v.salesForHousing");
                if(!isEmpty(salesForHousing)) {
                    lodgingRecords.push({
                        itineraryId: "",
                        startDate: component.get("v.today"),
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        cityId: "",
                        cityTitle: "",
                        lodgingId: "",
                        lodgingType: "",
                        budgetTarget: salesForHousing.hasOwnProperty("Budget__c")? salesForHousing.Budget__c : 0.00,
                        hotelStars: salesForHousing.hasOwnProperty("Star_Preference__c")? salesForHousing.Star_Preference__c : component.get("v.hotelStars")[0],
                        hotelType: salesForHousing.hasOwnProperty("Hotel_Class__c")? salesForHousing.Hotel_Class__c : component.get("v.hotelTypes")[0],
                        distanceFromEvent: salesForHousing.hasOwnProperty("Distance_to_Venue__c")? salesForHousing.Distance_to_Venue__c : component.get("v.distanceFromEventOptions")[0],
                        preferredBrands: salesForHousing.hasOwnProperty("Brand_Preference__c")? salesForHousing.Brand_Preference__c : "",
                        preferredBrandsList: salesForHousing.hasOwnProperty("Brand_Preference__c")? salesForHousing.Brand_Preference__c.split(";") : [],
                        additionalNotes: "",
                        roomTypeRecords: component.get("v.salesHousingRoomTypes"),
                        concessionRecords: [],
                        otherRoomTypeRecords: [],
                        otherConcessionRecords: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                else {
                    lodgingRecords.push({
                        itineraryId: "",
                        startDate: component.get("v.today"),
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        cityId: "",
                        cityTitle: "",
                        lodgingId: "",
                        lodgingType: "",
                        budgetTarget: 0,
                        hotelStars: component.get("v.hotelStars")[0],
                        hotelType: component.get("v.hotelTypes")[0],
                        distanceFromEvent: component.get("v.distanceFromEventOptions")[0],
                        preferredBrands: "",
                        preferredBrandsList: [],
                        additionalNotes: "",
                        roomTypeRecords: [],
                        concessionRecords: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                component.set("v.lodgingRecords",lodgingRecords);
                break;
            case "ground":
                var groundRecords = component.get("v.groundRecords");
                index = groundRecords.length;
                var salesForGround = component.get("v.salesForGround");
                if(!isEmpty(salesForGround)) {
                    groundRecords.push({
                        itineraryId: "",
                        cityTitle: "",
                        startDate: "",
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        tripDetailsId: "",
                        additionalNotes: "",
                        busType: salesForGround.hasOwnProperty("busType")? salesForGround.busType : "",
                        qtyOfBuses: salesForGround.hasOwnProperty("qtyOfBuses")? salesForGround.qtyOfBuses : 1,
                        passengers: salesForGround.hasOwnProperty("passengers")? salesForGround.passengers : 1,
                        gearLuggage: salesForGround.hasOwnProperty("gearLuggage")? salesForGround.gearLuggage : "",
                        groupType: "",
                        amenities: salesForGround.hasOwnProperty("amenities")? salesForGround.amenities : "",
                        amenitiesList: salesForGround.hasOwnProperty("amenities")? salesForGround.amenities.split(";") : [],
                        notes: salesForGround.hasOwnProperty("notes")? salesForGround.notes : "",
                        legs: [{
                            subTripDetailsId: "",
                            subTripType: component.get("v.tripTypesGround")[0],
                            legId: "",
                            locationPickUp: component.get("v.locationPickUpTypes")[0],
                            locationDropOff: component.get("v.locationDropOffTypes")[0],
                            locationDetailsPickUp: "",
                            locationDetailsDropOff: "",
                            datePickUp: component.get("v.today"),
                            timePickUp: "",
                            dateDropOff: "",
                            timeDropOff: ""
                        }],
                        otherLegs: [],
                        otherVehicles: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                else {
                    groundRecords.push({
                        itineraryId: "",
                        cityTitle: "",
                        startDate: "",
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        tripDetailsId: "",
                        additionalNotes: "",
                        busType: "",
                        qtyOfBuses: 1,
                        passengers: 1,
                        gearLuggage: "",
                        groupType: "",
                        amenities: "",
                        amenitiesList: [],
                        notes: "",
                        legs: [{
                            subTripDetailsId: "",
                            subTripType: component.get("v.tripTypesGround")[0],
                            legId: "",
                            locationPickUp: component.get("v.locationPickUpTypes")[0],
                            locationDropOff: component.get("v.locationDropOffTypes")[0],
                            locationDetailsPickUp: "",
                            locationDetailsDropOff: "",
                            datePickUp: component.get("v.today"),
                            timePickUp: "",
                            dateDropOff: "",
                            timeDropOff: ""
                        }],
                        otherLegs: [],
                        otherVehicles: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                component.set("v.groundRecords",groundRecords);
                break;
            case "air":
                var flightRecords = component.get("v.flightRecords");
                index = flightRecords.length;
                flightRecords.push({
                    itineraryId: "",
                    cityTitle: "",
                    startDate: "",
                    startDateTitle: "",
                    endDate: "",
                    endDateTitle: "",
                    airDetailsId: "",
                    additionalNotes: "",
                    tripType: "One Way",
                    classService: component.get("v.classServicesAir")[0],
                    pax: 0,
                    preferredAirline: component.get("v.preferredAirlinesAir")[0],
                    segments: [{
                        segmentId: "",
                        departureCity: "",
                        departureDate: component.get("v.today"),
                        departureTimeStart: "",
                        departureTimeEnd: "",
                        arrivalCity: "",
                        arrivalDate: ""
                    }],
                    isLocked: false,
                    isEdited: true
                });
                component.set("v.flightRecords",flightRecords);
                break;
            case "freight":
                var freightRecords = component.get("v.freightRecords");
                index = freightRecords.length;
                freightRecords.push({
                    itineraryId: "",
                    cityTitle: "",
                    startDate: "",
                    startDateTitle: "",
                    endDate: "",
                    endDateTitle: "",
                    tripDetailsId: "",
                    subTripDetailsId: "",
                    additionalNotes: "",
                    groupType: component.get("v.groupTypesFreight")[0],
                    notes: "",
                    legs: [{
                        subTripDetailsId: "",
                        legId: "",
                        locationDetailsPickUp: "",
                        locationDetailsDropOff: "",
                        datePickUp: component.get("v.today"),
                        timePickUp: "",
                        dateDropOff: "",
                        timeDropOff: ""
                    }],
                    otherLegs: [],
                    manifestId: "",
                    manifestName: "",
                    isLocked: false,
                    isEdited: true
                });
                component.set("v.freightRecords",freightRecords);
                break;
            default:
                break;
        }
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened",index);
    },
    
    handleShowRecord : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        var recordOpened = component.get("v.recordOpened");
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        if(recordOpened !== index) component.set("v.recordOpened",index);
        else component.set("v.recordOpened","-1");
    },
    
    handleInputChange : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var input = event.getSource();
        if(!input.checkValidity) input.reportValidity();
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        records[index].isEdited = true;
        var fieldName = input.get("v.fieldName");
        var name = input.get("v.name");
        /*
        if(fieldName != undefined && menuSelected == "air") {
            var tripType = records[index].tripType;
            if(tripType == "Round Trip") {
                switch (fieldName) {
                    case "Departure_City__c":
                        console.log("Departure_City__c");
                        records[index].segments[1].arrivalCityId = input.get("v.value")[0];
                        break;
                    case "Arrival_City__c":
                        console.log("Arrival_City__c");
                        records[index].segments[1].departureCityId = input.get("v.value")[0];
                        break;
                    default:
                        break;
                }
            }
        }
        */
        if(name != undefined && menuSelected == "air") {
            var tripType = records[index].tripType;
            if(tripType != "One Way" && name == "Departure_Date__c") {
                var segmentIndex = parseInt(input.get("v.label"));
                if(segmentIndex < records[index].segments.length-1) records[index].segments[segmentIndex+1].arrivalDate = records[index].segments[segmentIndex].departureDate;
            }
        }
        if(menuSelected == "housing") component.set("v.lodgingRecords",records);
        if(menuSelected == "ground") component.set("v.groundRecords",records);
        if(menuSelected == "air") component.set("v.flightRecords",records);
        if(menuSelected == "freight") component.set("v.freightRecords",records);
    },
    
    onLodgingVenueCity : function(component, event, helper) {
        var index = component.get("v.recordOpened");
        var records = component.get("v.lodgingRecords");
        var record = records[index];
        record.otherVenue = "";
        component.set("v.lodgingRecords",records);
        component.set("v.loadVenueCityLookup",true);
    },
    
    onLodgingVenue : function(component, event, helper) {
        var index = component.get("v.recordOpened");
        var records = component.get("v.lodgingRecords");
        var record = records[index];
        record.otherVenue = "";
        component.set("v.lodgingRecords",records);
        component.set("v.loadVenueLookup",true);
    },
    
    onLodgingCity : function(component, event, helper) {
        var index = component.get("v.recordOpened");
        var records = component.get("v.lodgingRecords");
        var record = records[index];
        record.otherVenue = "";
        component.set("v.lodgingRecords",records);
        component.set("v.loadCityLookup",true);
    },
    
    onAirportRound : function(component, event, helper) {
        console.log("onAirportRound");
        var index = component.get("v.recordOpened");
        var records = component.get("v.flightRecords");
        var tripType = records[index].tripType;
        if(tripType == "Round Trip") {
            records[index].segments[1].departureCityId = records[index].segments[0].arrivalCityId;
            records[index].segments[1].arrivalCityId = records[index].segments[0].departureCityId;
            component.set("v.triggerLookupValidation",!component.get("v.triggerLookupValidation"));
        }
        component.set("v.flightRecords",records);
        //console.log(JSON.parse(JSON.stringify( records[index] )));
    },
    
    handleShowRecordDetails : function(component, event, helper) {
        component.set("v.showRecordDetails",!component.get("v.showRecordDetails"));
        component.set("v.showOtherDetails",false);
    },
    
    handleShowOtherDetails : function(component, event, helper) {
        component.set("v.showOtherDetails",!component.get("v.showOtherDetails"));
        component.set("v.showRecordDetails",false);
    },
    
    handleAddRoomType : function(component, event, helper) {
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var roomTypeRecords = [];
        if(lodging.hasOwnProperty("roomTypeRecords")) roomTypeRecords = lodging.roomTypeRecords;
        roomTypeRecords.push({
            Id: "",
            Unit_Type__c: component.get("v.roomTypes")[0],
            Units__c: ""
        });
        lodging.roomTypeRecords = roomTypeRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleRemoveRoomType : function(component, event, helper) {
        var indexRoom = parseInt(event.getSource().get("v.value"));
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var roomTypeRecords = lodging.roomTypeRecords;
        roomTypeRecords.splice(indexRoom,1);
        lodging.roomTypeRecords = roomTypeRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleAddConcession : function(component, event, helper) {
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var concessionRecords = [];
        if(lodging.hasOwnProperty("concessionRecords")) concessionRecords = lodging.concessionRecords;
        if(lodging.lodgingType != "housingCorp") {
            concessionRecords.push({
                Id: "",
                Concessions_Requested__c: component.get("v.concessionHousingTypes")[0],
                Notes__c: ""
            });
        } else {
            concessionRecords.push({
                Id: "",
                Concessions_Requested__c: component.get("v.concessionCorporateTypes")[0],
                Notes__c: ""
            });
        }
        lodging.concessionRecords = concessionRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleRemoveConcession : function(component, event, helper) {
        var indexConcession = parseInt(event.getSource().get("v.value"));
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var concessionRecords = lodging.concessionRecords;
        concessionRecords.splice(indexConcession,1);
        lodging.concessionRecords = concessionRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleAddGroundLeg : function(component, event, helper) {
        var groundIndex = component.get("v.recordOpened");
        var groundRecords = component.get("v.groundRecords");
        var ground = groundRecords[groundIndex];
        var legs = [];
        if(ground.hasOwnProperty("legs")) legs = ground.legs;
        legs.push({
            subTripDetailsId: "",
            subTripType: component.get("v.tripTypesGround")[0],
            legId: "",
            locationPickUp: component.get("v.locationPickUpTypes")[0],
            locationDropOff: component.get("v.locationDropOffTypes")[0],
            locationDetailsPickUp: "",
            locationDetailsDropOff: "",
            datePickUp: component.get("v.today"),
            timePickUp: "",
            dateDropOff: "",
            timeDropOff: ""
        });
        ground.legs = legs;
        ground.isEdited = true;
        groundRecords[groundIndex] = ground;
        component.set("v.groundRecords",groundRecords);
    },
    
    handleRemoveGroundLeg : function(component, event, helper) {
        var indexLeg = parseInt(event.getSource().get("v.value"));
        var groundIndex = component.get("v.recordOpened");
        var groundRecords = component.get("v.groundRecords");
        var ground = groundRecords[groundIndex];
        var legs = ground.legs;
        legs.splice(indexLeg,1);
        ground.legs = legs;
        ground.isEdited = true;
        groundRecords[groundIndex] = ground;
        component.set("v.groundRecords",groundRecords);
    },
    
    handleAddSegment : function(component, event, helper) {
        var flightIndex = component.get("v.recordOpened");
        var flightRecords = component.get("v.flightRecords");
        var flight = flightRecords[flightIndex];
        var segments = [];
        if(flight.hasOwnProperty("segments")) segments = flight.segments;
        var departureDate = component.get("v.today");
        var arrivalDate = component.get("v.today");
        if(!!segments[segments.length-1].departureDate) {
            departureDate = segments[segments.length-1].departureDate;
            arrivalDate = segments[segments.length-1].departureDate;
        }
        segments.push({
            segmentId: "",
            departureCity: "",
            departureDate: departureDate,
            departureTimeStart: "",
            departureTimeEnd: "",
            arrivalCity: "",
            arrivalDate: arrivalDate
        });
        flight.segments = segments;
        flight.isEdited = true;
        flightRecords[flightIndex] = flight;
        component.set("v.flightRecords",flightRecords);
    },
    
    handleRemoveSegment : function(component, event, helper) {
        var indexSegment = parseInt(event.getSource().get("v.value"));
        var flightIndex = component.get("v.recordOpened");
        var flightRecords = component.get("v.flightRecords");
        var flight = flightRecords[flightIndex];
        var segments = flight.segments;
        segments.splice(indexSegment,1);
        if(indexSegment != segments.length) segments[indexSegment].arrivalDate = !!segments[indexSegment-1].departureDate? segments[indexSegment-1].departureDate : component.get("v.today");
        flight.segments = segments;
        flight.isEdited = true;
        flightRecords[flightRecords] = flight;
        component.set("v.flightRecords",flightRecords);
    },
    
    handleAddFreightLeg : function(component, event, helper) {
        var freightIndex = component.get("v.recordOpened");
        var freightRecords = component.get("v.freightRecords");
        var freight = freightRecords[freightIndex];
        var legs = [];
        if(freight.hasOwnProperty("legs")) legs = freight.legs;
        legs.push({
            subTripDetailsId: "",
            legId: "",
            tripType: "",
            locationDetailsPickUp: "",
            locationDetailsDropOff: "",
            datePickUp: component.get("v.today"),
            timePickUp: "",
            dateDropOff: "",
            timeDropOff: ""
        });
        freight.legs = legs;
        freight.isEdited = true;
        freightRecords[freightIndex] = freight;
        component.set("v.freightRecords",freightRecords);
    },
    
    handleRemoveFreightLeg : function(component, event, helper) {
        var indexLeg = parseInt(event.getSource().get("v.value"));
        var freightIndex = component.get("v.recordOpened");
        var freightRecords = component.get("v.freightRecords");
        var freight = freightRecords[freightIndex];
        var legs = freight.legs;
        legs.splice(indexLeg,1);
        freight.legs = legs;
        freight.isEdited = true;
        freightRecords[freightIndex] = freight;
        component.set("v.freightRecords",freightRecords);
    },
    
    handleChangeLodgingStay : function(component, event, helper) {
        var lodgingType = event.getParam("value");
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var salesHousingConcessions = component.get("v.salesHousingConcessions");
        var concessionsToCompare = lodgingType != "housingCorp"? component.get("v.concessionHousingTypes") : component.get("v.concessionCorporateTypes");
        var concessionsToAdd = [];
        /**Fix By Clay Dev 4 Feb, 2021 #176599208
        salesHousingConcessions.forEach(concession => { if(concessionsToCompare.indexOf(concession.Concessions_Requested__c) > 0) concessionsToAdd.push(concession); });
        lodging.concessionRecords.push.apply(lodging.concessionRecords,concessionsToAdd);
        **/
        salesHousingConcessions.forEach(concession => { 
            if(concessionsToCompare.indexOf(concession.Concessions_Requested__c)  < 0) { 
            	concessionsToCompare.push(concession.Concessions_Requested__c);                                
            }
        });
        if(lodgingType != "housingCorp") {
            component.set("v.concessionHousingTypes", concessionsToCompare);
        } else {
            component.set("v.concessionCorporateTypes", concessionsToCompare);
        }
        lodging.concessionRecords.push.apply(lodging.concessionRecords,salesHousingConcessions);
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleChangeAirTrip : function(component, event, helper) {
        var tripType = event.getParam("value");
        var flightIndex = component.get("v.recordOpened");
        var flightRecords = component.get("v.flightRecords");
        var flight = flightRecords[flightIndex];
        var segments = [];
        switch (tripType) {
            case "One Way":
                segments.push({
                    segmentId: "",
                    departureCityId: "",
                    departureCityName: "",
                    departureDate: component.get("v.today"),
                    departureTimeStart: "",
                    departureTimeEnd: "",
                    arrivalCityId: "",
                    arrivalCityName: "",
                    arrivalDate: ""
                });
                break;
            case "Round Trip":
            case "Multi-City":
                segments.push({
                    segmentId: "",
                    departureCityId: "",
                    departureCityName: "",
                    departureDate: component.get("v.today"),
                    departureTimeStart: "",
                    departureTimeEnd: "",
                    arrivalCityId: "",
                    arrivalCityName: "",
                    arrivalDate: ""
                });
                segments.push({
                    segmentId: "",
                    departureCityId: "",
                    departureCityName: "",
                    departureDate: "",
                    departureTimeStart: "",
                    departureTimeEnd: "",
                    arrivalCityId: "",
                    arrivalCityName: "",
                    arrivalDate: component.get("v.today")
                });
                break;
            default:
                break;
        }
        flight.segments = segments;
        flight.isEdited = true;
        flightRecords[flightIndex] = flight;
        component.set("v.flightRecords",flightRecords);
    },
    
    handleAttachManifestMessage: function(component, event, helper) {
        var freightIndex = component.get("v.recordOpened");
        var freightRecords = component.get("v.freightRecords");
        var freight = freightRecords[freightIndex];
        if(freight.isEdited) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please save this record first before uploading a file."
            });
            toastEvent.fire();
        } else {
            var menuSelected = component.get("v.menuSelected");
            var index = component.get("v.recordOpened");
            var records = [];
            if(menuSelected == "housing") records = component.get("v.lodgingRecords");
            if(menuSelected == "ground") records = component.get("v.groundRecords");
            if(menuSelected == "air") records = component.get("v.flightRecords");
            if(menuSelected == "freight") records = component.get("v.freightRecords");
            var record = records[index];
            component.set("v.openAttachment",true);
            component.set("v.fileName",record.manifestName);
            component.set("v.fileId",record.manifestId);
        }
    },
    
    handleUploadFinished : function(component, event, helper) {
        var uploadedFiles = event.getParam("files");
        component.set("v.fileId",uploadedFiles[0].documentId);
        component.set("v.fileName",uploadedFiles[0].name);
    },
    
    handleConfirmFile : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        var record = records[index];
        record.manifestId = component.get("v.fileId");
        record.manifestName = component.get("v.fileName");
        record.isEdited = true;
        records[index] = record;
        if(menuSelected == "housing") component.set("v.lodgingRecords",records);
        if(menuSelected == "ground") component.set("v.groundRecords",records);
        if(menuSelected == "air") component.set("v.flightRecords",records);
        if(menuSelected == "freight") component.set("v.freightRecords",records);
        console.log(record);
        component.set("v.openAttachment",false);
        component.set("v.fileName","");
        component.set("v.fileId","");
    },
    
    handleCommunicationEvent : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var tabSelected = component.get("v.tabSelected");
        var action = event.getParam("action");
        var data = JSON.parse(JSON.stringify(event.getParam("data")));
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") records = component.get("v.lodgingRecords");
            if(tabSelected == "Ground Travel") records = component.get("v.groundRecords");
            if(tabSelected == "Air") records = component.get("v.flightRecords");
            if(tabSelected == "Freight") records = component.get("v.freightRecords");
        }
        var recordType = "record";
        if(menuSelected == "housing") recordType = "Stay";
        if(menuSelected == "ground") recordType = "Trip";
        if(menuSelected == "air") recordType = "Flight";
        if(menuSelected == "freight") recordType = "Trip";
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") recordType = "Stay";
            if(tabSelected == "Ground Travel") recordType = "Trip";
            if(tabSelected == "Air") recordType = "Flight";
            if(tabSelected == "Freight") recordType = "Trip";
        }
        console.log(data);
        switch (action) {
            case "insert":
                data.record.isEdited = false;
                records[index] = data.record;
                if(menuSelected == "housing") component.set("v.isLodgingLocked",true);
                if(menuSelected == "ground") component.set("v.isGroundLocked",true);
                if(menuSelected == "air") component.set("v.isAirLocked",true);
                if(menuSelected == "freight") component.set("v.isFreightLocked",true);
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "success",
                    title: "",
                    message: recordType + " saved."
                });
                toastEvent.fire();
                break;
            case "update":
                data.record.isEdited = false;
                records[index] = data.record;
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "success",
                    title: "",
                    message: recordType + " updated."
                });
                toastEvent.fire();
                break;
            case "delete":
                records.splice(index,1);
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "success",
                    title: "",
                    message: recordType + " deleted."
                });
                toastEvent.fire();
                component.set("v.showRecordDetails",false);
                component.set("v.showOtherDetails",false);
                component.set("v.recordOpened","-1");
                break;
            default:
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "error",
                    title: "",
                    message: action
                });
                toastEvent.fire();
                return;
                break;
        }
        if(data.hasOwnProperty("salesForHousing")) component.set("v.salesForHousing",data.salesForHousing);
        if(data.hasOwnProperty("salesHousingRoomTypes")) component.set("v.salesHousingRoomTypes",data.salesHousingRoomTypes);
        if(data.hasOwnProperty("salesHousingConcessions")) component.set("v.salesHousingConcessions",data.salesHousingConcessions);
        if(data.hasOwnProperty("salesForGround")) component.set("v.salesForGround",data.salesForGround);
        if(menuSelected == "housing") component.set("v.lodgingRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "ground") component.set("v.groundRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "air") component.set("v.flightRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "freight") component.set("v.freightRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") component.set("v.lodgingRecords",JSON.parse(JSON.stringify(records)));
            if(tabSelected == "Ground Travel") component.set("v.groundRecords",JSON.parse(JSON.stringify(records)));
            if(tabSelected == "Air") component.set("v.flightRecords",JSON.parse(JSON.stringify(records)));
            if(tabSelected == "Freight") component.set("v.freightRecords",JSON.parse(JSON.stringify(records)));
        }
    },
    
    handleSaveRecord : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        var record = records[index];
        if(!record.isEdited) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "Nothing to update."
            });
            toastEvent.fire();
        } else {
            var lodgingTypeEmpty = false;
            var allValid = false;
            if(menuSelected == "housing" && !record.lodgingType) lodgingTypeEmpty = true;
            else allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
                inputCmp.reportValidity();
                return validSoFar && inputCmp.checkValidity();
            }, true);
            //console.log("triggerLookupValidation: "+component.get("v.triggerLookupValidation"));
            component.set("v.triggerLookupValidation",!component.get("v.triggerLookupValidation"));
            if(menuSelected == "housing" && !record.cityId) allValid = false;
            if(menuSelected == "air") for(var i = 0; i < record.segments.length; i++) if(!record.segments[i].departureCityId || !record.segments[i].arrivalCityId) allValid = false;
            if (allValid) {
                if(menuSelected == "housing") {
                    if(record.preferredBrandsList.length > 0) record.preferredBrands = record.preferredBrandsList.join(";");
                    else record.preferredBrands = "";
                }
                if(menuSelected == "ground") {
                    if(record.amenitiesList.length > 0) record.amenities = record.amenitiesList.join(";");
                    else record.amenities = "";
                }
                console.log("ready to send");
                var callToParent = component.getEvent("callToParent");
                callToParent.setParam("action","saveItineraryRecord");
                callToParent.setParam("data",{
                    recordType: menuSelected,
                    record: record
                });
                callToParent.fire();
            } else {
                component.set("v.showRecordDetails",true);
                var toastEvent = $A.get("e.force:showToast");
                var message = "Please update the invalid form entries and try again.";
                if(lodgingTypeEmpty) message = "You need to select a lodging type first.";
                toastEvent.setParams({
                    type: "error",
                    title: "",
                    message: message
                });
                toastEvent.fire();
            }
        }
    },
    
    handleDeleteRecord : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var tabSelected = component.get("v.tabSelected");
        var index = component.get("v.recordOpened");
        var record = {};
        var records = [];
        var isDeleteDenied = false;
        if(menuSelected == "housing") {
            records = component.get("v.lodgingRecords");
            record = records[index];
            if(record.otherRoomTypeRecords.length > 0 || record.otherConcessionRecords.length > 0) isDeleteDenied = true;
        }
        if(menuSelected == "ground") {
            records = component.get("v.groundRecords");
            record = records[index];
            if(record.otherLegs.length > 0 || record.otherVehicles.length > 0) isDeleteDenied = true;
        }
        if(menuSelected == "air") {
            records = component.get("v.flightRecords");
            record = records[index];
        }
        if(menuSelected == "freight") {
            records = component.get("v.freightRecords");
            record = records[index];
            if(record.otherLegs.length > 0) isDeleteDenied = true;
        }
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") {
                records = component.get("v.lodgingRecords");
                record = records[index];
                if(record.otherRoomTypeRecords.length > 0 || record.otherConcessionRecords.length > 0) isDeleteDenied = true;
            }
            if(tabSelected == "Ground Travel") {
                records = component.get("v.groundRecords");
                record = records[index];
                if(record.otherLegs.length > 0 || record.otherVehicles.length > 0) isDeleteDenied = true;
            }
            if(tabSelected == "Air") {
                records = component.get("v.flightRecords");
                record = records[index];
            }
            if(tabSelected == "Freight") {
                records = component.get("v.freightRecords");
                record = records[index];
                if(record.otherLegs.length > 0) isDeleteDenied = true;
            }
        }
        if(isDeleteDenied) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "You cannot delete a itinerary with records managed by Road Rebel. Please contact Road Rebel team for support."
            });
            toastEvent.fire();
            return;
        }
        if(records.length == 1) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "You need at least one record on this service."
            });
            toastEvent.fire();
        } else if(record.itineraryId == "") {
            records.splice(index,1);
            var recordType = "record";
            if(menuSelected == "housing") recordType = "Stay";
            if(menuSelected == "ground") recordType = "Trip";
            if(menuSelected == "air") recordType = "Flight";
            if(menuSelected == "freight") recordType = "Trip";
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "success",
                title: "",
                message: recordType + " deleted."
            });
            toastEvent.fire();
            component.set("v.showRecordDetails",false);
            component.set("v.showOtherDetails",false);
            component.set("v.recordOpened","-1");
            if(menuSelected == "housing") records = component.set("v.lodgingRecords",records);
            if(menuSelected == "ground") records = component.set("v.groundRecords",records);
            if(menuSelected == "air") records = component.set("v.flightRecords",records);
            if(menuSelected == "freight") records = component.set("v.freightRecords",records);
        } else {
            var recordType = "";
            if(menuSelected == "review") {
                if(tabSelected == "Lodging") recordType = "housing";
                if(tabSelected == "Ground Travel") recordType = "ground";
                if(tabSelected == "Air") recordType = "air";
                if(tabSelected == "Freight") recordType = "freight";
            } else recordType = menuSelected;
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","removeItineraryRecord");
            callToParent.setParam("data",{
                recordType: recordType,
                recordId: record.itineraryId
            });
            callToParent.fire();
        }
    },
    
    handleEditRecord : function(component, event, helper) {
        var tabSelected = component.get("v.tabSelected");
        if(tabSelected == "Lodging") component.set("v.menuSelected","housing");
        if(tabSelected == "Ground Travel") component.set("v.menuSelected","ground");
        if(tabSelected == "Air") component.set("v.menuSelected","air");
        if(tabSelected == "Freight") component.set("v.menuSelected","freight");
    },
    
    handleBack : function(component, event, helper) {
        var menuOptions = component.get("v.menuOptions");
        var menuSelected = component.get("v.menuSelected");
        var openBackConfirmation = component.get("v.openBackConfirmation");
        component.set("v.openBackConfirmation",false);
        var recordsPending = false;
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        records.forEach(record => { if(record.isEdited) recordsPending = true; });
        if(recordsPending && !openBackConfirmation) component.set("v.openBackConfirmation",true);
        else {
            for(var i = 0; i<menuOptions.length; i++) if(menuOptions[i].value == menuSelected) {
                menuSelected = menuOptions[i-1].value;
                i = menuOptions.length;
            }
            component.set("v.showRecordDetails",false);
            component.set("v.showOtherDetails",false);
            component.set("v.recordOpened","-1");
            component.set("v.menuSelected",menuSelected);
            var itineraryData = component.get("v.itineraryData");
            switch (menuSelected) {
                case "services":
                    component.set("v.lodgingRecords",[]);
                    component.set("v.groundRecords",[]);
                    component.set("v.flightRecords",[]);
                    component.set("v.freightRecords",[]);
                    delete itineraryData.lodgingRecords;
                    delete itineraryData.groundRecords;
                    delete itineraryData.flightRecords;
                    delete itineraryData.freightRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "housing":
                    component.set("v.lodgingRecords",[]);
                    delete itineraryData.lodgingRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "ground":
                    component.set("v.groundRecords",[]);
                    delete itineraryData.groundRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "air":
                    component.set("v.flightRecords",[]);
                    delete itineraryData.flightRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "freight":
                    component.set("v.freightRecords",[]);
                    delete itineraryData.freightRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                default:
                    break;
            }
        }
    },
    
    handleNext : function(component, event, helper) {
        var menuOptions = component.get("v.menuOptions");
        var menuSelected = component.get("v.menuSelected");
        var openNextConfirmation = component.get("v.openNextConfirmation");
        component.set("v.openNextConfirmation",false);
        var recordsPending = false;
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        records.forEach(record => { if(record.isEdited) recordsPending = true; });
        if(recordsPending && !openNextConfirmation) {
            if(records.length == 1) {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "warning",
                    title: "",
                    message: "You need to save at least one record before continuing."
                });
                toastEvent.fire();
            } else component.set("v.openNextConfirmation",true);
        } else {
            var itineraryData = component.get("v.itineraryData");
            var recordsSaved = [];
            if(menuSelected == "housing") recordsSaved = itineraryData.lodgingRecords;
            if(menuSelected == "ground") recordsSaved = itineraryData.groundRecords;
            if(menuSelected == "air") recordsSaved = itineraryData.flightRecords;
            if(menuSelected == "freight") recordsSaved = itineraryData.freightRecords;
            for(var i = records.length-1; i>=0; --i) {
                if(records[i].isEdited && !!records[i].itineraryId) recordsSaved.forEach(record => { if(record.itineraryId == records[i].itineraryId) records[i] = record; });
                else if (records[i].isEdited) records.splice(i,1);
            }
            if(menuSelected == "housing") records = component.set("v.lodgingRecords",records);
            if(menuSelected == "ground") records = component.set("v.groundRecords",records);
            if(menuSelected == "air") records = component.set("v.flightRecords",records);
            if(menuSelected == "freight") records = component.set("v.freightRecords",records);
            for(var i = 0; i<menuOptions.length; i++) if(menuOptions[i].value == menuSelected) {
                menuSelected = menuOptions[i+1].value;
                i = menuOptions.length
            }
            component.set("v.showRecordDetails",false);
            component.set("v.showOtherDetails",false);
            component.set("v.recordOpened","-1");
            component.set("v.menuSelected",menuSelected);
            switch (menuSelected) {
                case "ground":
                    var callToParent = component.getEvent("callToParent");
                    callToParent.setParam("action","loadGroundPage");
                    callToParent.fire();
                    break;
                case "air":
                    var callToParent = component.getEvent("callToParent");
                    callToParent.setParam("action","loadAirPage");
                    callToParent.fire();
                    break;
                case "freight":
                    var callToParent = component.getEvent("callToParent");
                    callToParent.setParam("action","loadFreightPage");
                    callToParent.fire();
                    break;
                case "review":
                    var tabSelected = "";
                    if(component.get("v.isFreightSelected")) tabSelected = "Freight";
                    if(component.get("v.isAirSelected")) tabSelected = "Air";
                    if(component.get("v.isGroundSelected")) tabSelected = "Ground Travel";
                    if(component.get("v.isLodgingSelected")) tabSelected = "Lodging";
                    component.set("v.tabSelected",tabSelected);
                    break;
                default:
                    break;
            }
        }
    },
    
    handleCloseModal : function(component, event, helper) {
        component.set("v.openAttachment",false);
        component.set("v.openBackConfirmation",false);
        component.set("v.openNextConfirmation",false);
        component.set("v.fileName","");
        component.set("v.fileId","");
    },
    
    showLodgingRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Lodging");
    },
    
    showGroundRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Ground Travel");
    },
    
    showAirRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Air");
    },
    
    showFreightRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Freight");
    },
    
    handleSubmit : function(component, event, helper) {
        var recordsPending = false;
        var records = [];
        if(component.get("v.isLodgingSelected")) {
            records = component.get("v.lodgingRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(component.get("v.isGroundSelected")) {
            records = component.get("v.groundRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(component.get("v.isAirSelected")) {
            records = component.get("v.flightRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(component.get("v.isFreightSelected")) {
            records = component.get("v.freightRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(recordsPending) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","submitItineraries");
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "Nothing to submit."
            });
            toastEvent.fire();
        }
    }
})
```
### VoyajerItinerary

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerItinerary

```
.THIS .mainMenuTitle {
    font-size: 1rem;
    padding: 0.5em;
    border-bottom: 1px solid #9f9f9f;
    margin-bottom: 0.5em;
}

.THIS .page-header_services {
    font-size: 1.5rem;
    text-align: center;
    margin-top: 0.25em;
}

.THIS .page-header_services:first-child {
    font-size: 1rem;
    margin-top: 1.5em;
}

.THIS .serviceBox {
    width: 8em;
    margin-bottom: 1em;
    position: relative;
    display: flex;
    flex-direction: column;
}

.THIS .serviceBox > div {
    text-align: center;
}

.THIS .serviceBoxImage {
    width: 100%;
    height: auto;
}

.THIS .serviceBox img {
    background-color: #f7f9fe;
    border-radius: 50%;
}

.THIS .serviceBoxName {
    margin-top: 1em;
    text-transform: uppercase;
    font-weight: 500;
    color: #00b4ff;
}

.THIS .multiSelectPicklist {
    width: 100%;
    border-radius: 0.25rem;
    text-transform: none;
    justify-content: space-between;
    padding-right: 0.5em !important;
}

.THIS .multiSelectPicklist .slds-icon {
    right: 0.25em;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .preferences {
    display: flex;
    flex-direction: column;
    margin-top: 0.75em;
    border-top: 1px solid #dbdbdb;
}

.THIS .additionalFields {
    margin-top: 0.75em;
    border-top: 1px solid #dbdbdb;
}

.THIS .preferences > div {
    display: flex;
    flex: 1;
    margin-bottom: 0.5em;
}

.THIS .preferencesHeader > div,
.THIS .preferencesRow > div {
    flex: 1;
    padding: .25rem;
}

.THIS .preferencesHeader > div {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    font-weight: 500;
    color: rgb(105, 105, 105);
}

.THIS .travels {
    display: flex;
    flex-direction: column;
    margin-top: 0.75em;
}

.THIS .travelRow {
    display: flex;
    flex: 1;
}

.THIS .travelRow > div:first-child {
    flex: 1;
}

.THIS .formInputTextarea textarea {
    margin-top: 0px;
    margin-bottom: 0px;
    height: 2rem;
    padding: 0.25rem 0.75rem;
}

.THIS .travelFields {
    display: flex;
    flex: 1;
    flex-direction: column;
}

.THIS .travelFields > div {
    display: flex;
}

.THIS .fieldSelect label {
    display: none;
}

.THIS .field {
    align-items: center;
    display: flex;
}

.THIS .fieldInput {
    flex: 1;
    padding-right: 0.25em;
}

.THIS .labelTooltip {
    padding-left: 0.25rem;
}

.THIS .labelTooltip .slds-form-element__icon {
    padding-top: 0;
}

.THIS .noRadius .slds-button {
    border-radius: 0;
}

.THIS .noRadius .slds-radio_faux {
    display: block;
}

.THIS .actions {
    display: flex;
    justify-content: flex-end;
    padding-top: 1em;
}

.THIS .reviewNavigator {
    background-color: white;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .slds-dueling-list__column:last-child {
    display: none;
}

@media (max-width: 800px) {
    .THIS .page-header_services:first-child {
        margin-top: 0;
    }
}

@media (max-width: 550px) {
    .THIS .mainMenuTitle {
        height: 8.25em;
        position: relative;
    }
    
    .THIS .mainMenuTitle h3 {
        transform: rotate(270deg);
        position: absolute;
        right: -100%;
        width: 8em;
        top: 40%;
        margin: auto;
        text-align: center;
    }
}
```
### VoyajerItinerary

```
<aura:component>
    <aura:attribute type="String" name="userId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="menuSelected" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="tabSelected" />
    <aura:attribute type="String" name="fileName" />
    <aura:attribute type="String" name="fileId" />
    <aura:attribute type="Object" name="itineraryData" />
    <aura:attribute type="Object" name="salesForHousing" />
    <aura:attribute type="Object" name="salesForGround" />
    <aura:attribute type="Object" name="salesForAir" />
    <aura:attribute type="Object" name="salesForFreight" />
    <aura:attribute type="Object" name="recordTypes" />
    <aura:attribute type="List" name="menuOptions" />
    <aura:attribute type="List" name="lodgingTypes" default="[{'label': 'Group Hotel', 'value': 'housingHotel'},{'label': 'Apartment/Private Home', 'value': 'housingCorp'},{'label': 'Less than 10 rooms', 'value': 'housingIR'}]" />
    <aura:attribute type="List" name="distanceFromEventOptions" />
    <aura:attribute type="List" name="hotelStars" />
    <aura:attribute type="List" name="hotelTypes" />
    <aura:attribute type="List" name="preferredBrands" />
    <aura:attribute type="List" name="roomTypes" />
    <aura:attribute type="List" name="concessionHousingTypes" />
    <aura:attribute type="List" name="concessionCorporateTypes" />
    <aura:attribute type="List" name="salesHousingRoomTypes" />
    <aura:attribute type="List" name="salesHousingConcessions" />
    <aura:attribute type="List" name="tripTypesGround" />
    <aura:attribute type="List" name="locationPickUpTypes" />
    <aura:attribute type="List" name="locationDropOffTypes" />
    <aura:attribute type="List" name="vehicleTypesGround" />
    <aura:attribute type="List" name="groupTypesGround" />
    <aura:attribute type="List" name="amenitiesGround" />
    <aura:attribute type="List" name="classServicesAir" />
    <aura:attribute type="List" name="preferredAirlinesAir" />
    <aura:attribute type="List" name="groupTypesFreight" />
    <aura:attribute type="List" name="tripTypes" default="[{'label': 'One Way', 'value': 'One Way'},{'label': 'Round Trip', 'value': 'Round Trip'},{'label': 'Multi-City', 'value': 'Multi-City'}]" />
    <aura:attribute type="List" name="lodgingRecords" />
    <aura:attribute type="List" name="groundRecords" />
    <aura:attribute type="List" name="flightRecords" />
    <aura:attribute type="List" name="freightRecords" />
    <aura:attribute type="Boolean" name="isLodgingSelected" default="false" />
    <aura:attribute type="Boolean" name="isLodgingLocked" default="false" />
    <aura:attribute type="Boolean" name="isGroundSelected" default="false" />
    <aura:attribute type="Boolean" name="isGroundLocked" default="false" />
    <aura:attribute type="Boolean" name="isAirSelected" default="false" />
    <aura:attribute type="Boolean" name="isAirLocked" default="false" />
    <aura:attribute type="Boolean" name="isFreightSelected" default="false" />
    <aura:attribute type="Boolean" name="isFreightLocked" default="false" />
    <aura:attribute type="Boolean" name="showRecordDetails" default="false" />
    <aura:attribute type="Boolean" name="showOtherDetails" default="false" />
    <aura:attribute type="Boolean" name="triggerLookupValidation" default="false" />
    <aura:attribute type="Boolean" name="loadVenueCityLookup" default="false" />
    <aura:attribute type="Boolean" name="loadVenueLookup" default="false" />
    <aura:attribute type="Boolean" name="loadCityLookup" default="false" />
    <aura:attribute type="Boolean" name="openAttachment" default="false" />
    <aura:attribute type="Boolean" name="openBackConfirmation" default="false" />
    <aura:attribute type="Boolean" name="openNextConfirmation" default="false" />
    <aura:attribute type="Integer" name="recordOpened" default="-1" />
    <aura:attribute type="Date" name="today" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.itineraryData}" action="{!c.loadItineraryData}" />
    <aura:handler action="{!c.handleCommunicationEvent}" event="c:VoyajerCallToChild" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="mainMenu">
            <div class="mainMenuTitle"><h3>Enter Itinerary</h3></div>
            <nav class="slds-nav-vertical sideBarItinerary lightningVerticalNavigation">
                <aura:iteration items="{!v.menuOptions}" var="item">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected==item.value? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action">
                            <i class="{!'fas '+item.icon+' sideBarItineraryIcon'}"></i><span class="hideOnMobile">{!item.label}</span>
                            <aura:if isTrue="{!item.checked}">
                                <div class="checkpoint"><i class="fas fa-check-circle checkpointIcon"></i><div class="checkpointBackground"></div></div>
                            </aura:if>
                        </div>
                    </div>
                </aura:iteration>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <aura:if isTrue="{!v.menuSelected=='services'}">
                    <div class="page-section" style="align-items: center;">
                        <div class="page-header page-header_services">Let's begin...</div>
                        <div class="page-header page-header_services">Select the services you will need</div>
                        <div class="page-section-services_center">
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Lodging" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_housing_icons'+(v.isLodgingSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Lodging</p></div>
                            </div>
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Ground Travel" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_busing_icons'+(v.isGroundSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Ground Travel</p></div>
                            </div>
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Air Travel" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_plane_icons'+(v.isAirSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Air Travel</p></div>
                            </div>
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Freight" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_freight_icons'+(v.isFreightSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Freight</p></div>
                            </div>
                        </div>
                        <div class="page-section"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.saveServices}" /></div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='housing'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-home titleIcon"></i>Lodging</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.lodgingRecords}" var="lodging" indexVar="lodgingIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(lodging.isLocked==true,'background-color: #0065ff; color: white;',if(lodging.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!lodgingIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!empty(lodging.cityTitle)}">
                                                <!-- 177513339 -->
                                                <aura:if isTrue="{!(lodging.stayStatus=='Layoff')}">
                                                    <div class="location" title="Layoff">Layoff</div>
                                                    <aura:set attribute="else">
                                                    	<div class="location" title="{!'Stay '+(lodgingIndex+1)}">{!'Stay '+(lodgingIndex+1)}</div>
                                                    </aura:set>
                                                </aura:if>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!lodging.cityTitle}">{!lodging.cityTitle}</div>
                                                    <div class="dates" style="{!if(empty(lodging.startDateTitle),'display:none;','')}">{!lodging.startDateTitle} - {!lodging.endDateTitle}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==lodgingIndex?'utility:up':'utility:down'}" value="{!lodgingIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==lodgingIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(lodging.isLocked==true,'background-color: #c5dcff;',if(lodging.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!lodging.isLocked!=true}">
                                                <div>
                                                    <lightning:radioGroup aura:id="lodgingForm" name="radioButtonGroup" label="" options="{!v.lodgingTypes}" value="{!lodging.lodgingType}" type="button" class="noRadius" onchange="{!c.handleChangeLodgingStay}" disabled="{!if(empty(lodging.lodgingType),false,true)}" />
                                                </div>
                                                <aura:if isTrue="{!not(empty(lodging.lodgingType))}">
                                                    <br/>
                                                    <div class="formColumnTwoChilds">
                                                        <div class="formField">
                                                            <label for="Start_Date__c">Check-In</label>
                                                            <lightning:input aura:id="recordField" name="Start_Date__c" type="date" label="" value="{!lodging.startDate}" min="{!v.today}" max="{!lodging.endDate}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                        </div>
                                                        <div class="formField">
                                                            <label for="End_Date__c">Check-Out</label>
                                                            <lightning:input aura:id="recordField" name="End_Date__c" type="date" label="" value="{!lodging.endDate}" min="{!lodging.startDate}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                        </div>
                                                    </div>
                                                    <div class="formColumnTwoChilds">
                                                        <div class="formField">
                                                            <c:VoyajerCustomLookup objectAPIName="Account" 
                                                                                   fieldName="Venue_City__c" 
                                                                                   iconName="custom:custom78" 
                                                                                   lookupId="{!lodging.venueCityId}" 
                                                                                   label="Venue City" 
                                                                                   inputPlaceholder="Enter Location" 
                                                                                   isEdited="{!lodging.isEdited}" 
                                                                                   isRequired="false" 
                                                                                   loadVenueCityLookup="{!v.loadVenueCityLookup}" 
                                                                                   venueId="{!lodging.venueId}" 
                                                                                   lodgingVenueAux="{!c.onLodgingVenue}" 
                                                                                   cityId="{!lodging.cityId}" 
                                                                                   lodgingCityAux="{!c.onLodgingCity}" />
                                                        </div>
                                                        <div class="formField">
                                                            <c:VoyajerCustomLookup objectAPIName="Account" 
                                                                                   fieldName="Venue__c" 
                                                                                   iconName="custom:custom85" 
                                                                                   lookupId="{!lodging.venueId}" 
                                                                                   label="Venue" 
                                                                                   inputPlaceholder="Enter Venue" 
                                                                                   isRequired="false" 
                                                                                   isEdited="{!lodging.isEdited}" 
                                                                                   loadVenueLookup="{!v.loadVenueLookup}" 
                                                                                   venueCityId="{!lodging.venueCityId}" 
                                                                                   lodgingVenueCityAux="{!c.onLodgingVenueCity}" 
                                                                                   cityId="{!lodging.cityId}" 
                                                                                   lodgingCityAux="{!c.onLodgingCity}" />
                                                        </div>
                                                    </div>
                                                    <div class="formColumnTwoChilds">
                                                        <div class="formField">
                                                            <c:VoyajerCustomLookup objectAPIName="City__c" 
                                                                                   fieldName="City__c" 
                                                                                   iconName="custom:custom24" 
                                                                                   lookupId="{!lodging.cityId}" 
                                                                                   label="Location" 
                                                                                   inputPlaceholder="Enter Location" 
                                                                                   isRequired="true" 
                                                                                   isEdited="{!lodging.isEdited}" 
                                                                                   loadCityLookup="{!v.loadCityLookup}" 
                                                                                   triggerLookupValidation="{!v.triggerLookupValidation}" />
                                                        </div>
                                                        <div class="formField">
                                                            <label for="Other_Venue__c">
                                                                Other Venue<lightning:helptext class="labelTooltip" content="If you can’t find venue in your city please add your venue name here." />
                                                            </label>
                                                            <lightning:input aura:id="recordField" name="Other_Venue__c" label="" value="{!lodging.otherVenue}" variant="label-hidden" class="fieldInput" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!or(not(empty(lodging.otherRoomTypeRecords)),not(empty(lodging.otherConcessionRecords)))}">
                                                        <div class="recordDetails">
                                                            <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                                                <div class="recordTitleText">
                                                                    <div><i class="fas fa-hotel titleIcon" style="color: white;"></i> Other Rooms and Concessions (managed by RR Team)</div>
                                                                </div>
                                                                <div class="recordTitleButton">
                                                                    <lightning:buttonIcon iconName="{!v.showOtherDetails==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowOtherDetails}" />
                                                                </div>
                                                            </div>
                                                            <div class="recordBodyContent" style="{!v.showOtherDetails!=true?'display: none;':''}">
                                                                <aura:if isTrue="{!not(empty(lodging.otherRoomTypeRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;"><span>Room Type</span></div>
                                                                            <div style="display: flex; min-width: 12em; justify-content: center;"><span>Qty of Rooms</span></div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.allRoomTypeRecords}" var="room" indexVar="roomIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;"><span>{!room.Unit_Type__c}</span></div>
                                                                                <div style="display: flex; min-width: 12em; justify-content: center;"><span>{!room.Units__c}</span></div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                                <aura:if isTrue="{!not(empty(lodging.otherConcessionRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;">Concessions</div>
                                                                            <div style="flex: 1">Notes</div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.otherConcessionRecords}" var="concession" indexVar="concessionIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;">{!concession.Concessions_Requested__c}</div>
                                                                                <div style="flex: 1">{!concession.Notes__c}</div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                    <div class="recordDetails">
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <div><i class="fas fa-map-marked-alt titleIcon"></i> Lodging Details</div>
                                                            </div>
                                                            <div class="recordTitleButton">
                                                                <lightning:buttonIcon iconName="{!v.showRecordDetails==true?'utility:up':'utility:down'}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecordDetails}" />
                                                            </div>
                                                        </div>
                                                        <aura:if isTrue="{!v.showRecordDetails==true}">
                                                            <div class="recordBodyContent">
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField"><label for="Budget__c">Budget Target</label><lightning:input aura:id="recordField" name="Budget__c" type="number" label="" value="{!lodging.budgetTarget}" min="0" variant="label-hidden" formatter="currency" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    <div class="formField">
                                                                        <label for="Distance_to_Venue__c">Distance from Event</label>
                                                                        <div class="fieldSelect">
                                                                            <lightning:select name="Distance_to_Venue__c" label="" value="{!lodging.distanceFromEvent}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                <aura:iteration items="{!v.distanceFromEventOptions}" var="distance">
                                                                                    <option value="{!distance}">{!distance}</option>
                                                                                </aura:iteration>
                                                                            </lightning:select>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField">
                                                                        <label for="Star_Preference__c">Hotel Stars</label>
                                                                        <div class="fieldSelect">
                                                                            <lightning:select name="Star_Preference__c" label="" value="{!lodging.hotelStars}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                <aura:iteration items="{!v.hotelStars}" var="hotelStar">
                                                                                    <option value="{!hotelStar}">{!hotelStar}</option>
                                                                                </aura:iteration>
                                                                            </lightning:select>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formField">
                                                                        <label for="Hotel_Class__c">Hotel Type</label>
                                                                        <div class="fieldSelect">
                                                                            <lightning:select name="Hotel_Class__c" label="" value="{!lodging.hotelType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                <aura:iteration items="{!v.hotelTypes}" var="hotelType">
                                                                                    <option value="{!hotelType}">{!hotelType}</option>
                                                                                </aura:iteration>
                                                                            </lightning:select>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="formField">
                                                                    <label for="Brand_Preference__c">Preferred Brands</label>
                                                                    <lightning:dualListbox name="Brand_Preference__c"
                                                                                           label= ""
                                                                                           sourceLabel="Available"
                                                                                           selectedLabel="Chosen"
                                                                                           options="{!v.preferredBrands}"
                                                                                           value="{!lodging.preferredBrandsList}"
                                                                                           onchange="{!c.handleInputChange}"
                                                                                           variant="label-hidden" />
                                                                </div>
                                                                <div class="preferences">
                                                                    <aura:if isTrue="{!not(empty(lodging.roomTypeRecords))}">
                                                                        <div class="preferencesHeader">
                                                                            <div>Room Type</div>
                                                                            <div>Qty of Rooms</div>
                                                                        </div>
                                                                    </aura:if>
                                                                    <aura:iteration items="{!lodging.roomTypeRecords}" var="room" indexVar="roomIndex">
                                                                        <div class="preferencesRow">
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Unit_Type__c" label="" value="{!room.Unit_Type__c}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.roomTypes}" var="roomType">
                                                                                        <option value="{!roomType}">{!roomType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                            <div class="field">
                                                                                <lightning:input aura:id="recordField" name="Units__c" type="number" label="" value="{!room.Units__c}" variant="label-hidden" min="1" required="true" class="fieldInput" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                <lightning:buttonIcon iconName="utility:clear" value="{!roomIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveRoomType}" />
                                                                            </div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                    <div class="actions">
                                                                        <lightning:button label="Add Room Type" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddRoomType}" />
                                                                    </div>
                                                                </div>
                                                                <div class="preferences">
                                                                    <aura:if isTrue="{!not(empty(lodging.concessionRecords))}">
                                                                        <div class="preferencesHeader">
                                                                            <div>Concessions</div>
                                                                            <div>Notes</div>
                                                                        </div>
                                                                    </aura:if>
                                                                    <aura:iteration items="{!lodging.concessionRecords}" var="concession" indexVar="concessionIndex">
                                                                        <div class="preferencesRow">
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Concessions_Requested__c" label="" value="{!concession.Concessions_Requested__c}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:if isTrue="{!lodging.lodgingType!='housingCorp'}">
                                                                                        <aura:iteration items="{!v.concessionHousingTypes}" var="concessionType">
                                                                                            <option value="{!concessionType}">{!concessionType}</option>
                                                                                        </aura:iteration>
                                                                                        <aura:set attribute="else">
                                                                                            <aura:iteration items="{!v.concessionCorporateTypes}" var="concessionType">
                                                                                                <option value="{!concessionType}">{!concessionType}</option>
                                                                                            </aura:iteration>
                                                                                        </aura:set>
                                                                                    </aura:if>
                                                                                </lightning:select>
                                                                            </div>
                                                                            <div class="field">
                                                                                <lightning:input aura:id="recordField" name="Notes__c" label="" value="{!concession.Notes__c}" variant="label-hidden" class="fieldInput" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                <lightning:buttonIcon iconName="utility:clear" value="{!concessionIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveConcession}" />
                                                                            </div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                    <div class="actions">
                                                                        <lightning:button label="Add Concession" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddConcession}" />
                                                                    </div>
                                                                </div>
                                                                <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                                    <label for="Client_Notes__c">Additional Notes</label>
                                                                    <lightning:textarea name="Client_Notes__c" label="" value="{!lodging.additionalNotes}" variant="label-hidden" onchange="{!c.handleInputChange}" />
                                                                </div>
                                                            </div>
                                                        </aura:if>
                                                    </div>
                                                </aura:if>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <div class="recordTable tripTable">
                                                        <div class="tableTripRow">
                                                            <div class="tripList">
                                                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                    <div class="tableHeader"><span>Lodging Type</span></div>
                                                                    <div class="tripInfo">
                                                                        <aura:if isTrue="{!lodging.lodgingType == 'housingHotel'}"><span>Group hotel</span></aura:if>
                                                                        <aura:if isTrue="{!lodging.lodgingType == 'housingCorp'}"><span>Long term housing</span></aura:if>
                                                                        <aura:if isTrue="{!lodging.lodgingType == 'housingIR'}"><span>Less than 10 rooms</span></aura:if>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="tripList">
                                                                <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Check-In</span></div>
                                                            <div style="flex: 1;"><span>Check-Out</span></div>
                                                            <div class="tableLocation"><span>Location</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.startDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                            <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.endDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                            <div class="tableLocation"><span>{!lodging.cityTitle}</span></div>
                                                        </div>
                                                    </div>
                                                    <div class="recordTable tripTable">
                                                        <div class="tableTripRow">
                                                            <div class="tripList">
                                                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                    <div class="tableHeader"><span>Venue City</span></div>
                                                                    <div class="tripInfo">
                                                                        <span>{!not(empty(lodging.venueId))? lodging.venueName : lodging.otherVenue}</span>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="tripList">
                                                                <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Budget Target</span></div>
                                                            <div style="flex: 1;"><span>Hotel Stars</span></div>
                                                            <div style="flex: 1;"><span>Hotel Type</span></div>
                                                            <div style="flex: 1;"><span>Distance to Event</span></div>
                                                            <div style="flex: 2;"><span>Preferred Brands</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.budgetTarget}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelStars}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelType}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.distanceFromEvent}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 2;">
                                                                <aura:if isTrue="{!not(empty(lodging.preferredBrandsList))}">
                                                                    <span>
                                                                        <aura:iteration items="{!lodging.preferredBrandsList}" var="brand" indexVar="indexBrand">
                                                                            {!brand+if(lodging.preferredBrandsList.length-1>indexBrand,', ','')}
                                                                        </aura:iteration>
                                                                    </span>
                                                                    <!--<ul class="slds-list_dotted"><aura:iteration items="{!lodging.preferredBrandsList}" var="brand"><li style="white-space: pre-wrap;">{!brand}</li></aura:iteration></ul>-->
                                                                    <aura:set attribute="else">-</aura:set>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!not(empty(lodging.allRoomTypeRecords))}">
                                                        <div class="recordTable tableList">
                                                            <div class="tableHeader">
                                                                <div style="flex: 1;"><span>Room Type</span></div>
                                                                <div style="display: flex; min-width: 12em; justify-content: center;"><span>Qty of Rooms</span></div>
                                                            </div>
                                                            <aura:iteration items="{!lodging.allRoomTypeRecords}" var="room" indexVar="roomIndex">
                                                                <div class="tableRow">
                                                                    <div style="flex: 1;"><span>{!room.Unit_Type__c}</span></div>
                                                                    <div style="display: flex; min-width: 12em; justify-content: center;"><span>{!room.Units__c}</span></div>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </aura:if>
                                                    <aura:if isTrue="{!not(empty(lodging.allConcessionRecords))}">
                                                        <div class="recordTable tableList">
                                                            <div class="tableHeader">
                                                                <div style="flex: 1;"><span>Concessions</span></div>
                                                                <div style="flex: 1"><span>Notes</span></div>
                                                            </div>
                                                            <aura:iteration items="{!lodging.allConcessionRecords}" var="concession" indexVar="concessionIndex">
                                                                <div class="tableRow">
                                                                    <div style="flex: 1;"><span>{!concession.Concessions_Requested__c}</span></div>
                                                                    <div style="flex: 1"><span>{!concession.Notes__c}</span></div>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </aura:if>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;"><span>Additional Notes</span></span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!lodging.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.lodgingRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='ground'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-car titleIcon"></i>Ground Travel</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.groundRecords}" var="ground" indexVar="groundIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(ground.isLocked==true,'background-color: #0065ff; color: white;',if(ground.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!groundIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!and(empty(ground.cityTitleStart),empty(ground.cityTitleEnd))}">
                                                <div class="location" title="{!'Trip '+(groundIndex+1)}">{!'Trip '+(groundIndex+1)}</div>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!ground.cityTitleStart+ground.cityTitleEnd}">{!ground.cityTitleStart+ground.cityTitleEnd}</div>
                                                    <div class="dates" style="{!if(empty(ground.startDateTitle),'display:none;','')}">{!ground.startDateTitle} - {!ground.endDateTitle}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==groundIndex?'utility:up':'utility:down'}" value="{!groundIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==groundIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(ground.isLocked==true,'background-color: #c5dcff;',if(ground.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!ground.isLocked!=true}">
                                                <div class="travels">
                                                    <aura:iteration items="{!ground.legs}" var="leg" indexVar="legIndex">
                                                        <div class="travelRow" style="{!if(legIndex>0,'border-top: 1px solid #dbdbdb; margin-top: 0.5em;','')}">
                                                            <div>
                                                                <div class="formColumnThreeChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField">
                                                                            <label for="Sub_Trip_Type__c">Trip Type</label>
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Sub_Trip_Type__c" label="" value="{!leg.subTripType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.tripTypesGround}" var="tripType">
                                                                                        <option value="{!tripType}">{!tripType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                        </div>
                                                                        <div class="formField">
                                                                            <label for="Location_Type__c">Location Pick Up Type</label>
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Location_Type__c" label="" value="{!leg.locationPickUp}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.locationPickUpTypes}" var="pickUpType">
                                                                                        <option value="{!pickUpType}">{!pickUpType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formField">
                                                                        <label for="Location_Details__c">Location Pick Up Details</label>
                                                                        <lightning:input type="text" aura:id="recordField" placeholder="Enter Location" name="Location_Details__c" value="{!leg.locationDetailsPickUp}" variant="label-hidden" required="true" class="formInputTextarea" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="Start_Date__c">Date</label><lightning:input aura:id="recordField" name="Start_Date__c" type="date" dateStyle="short" value="{!leg.datePickUp}" variant="label-hidden" required="true" min="{!v.today}" max="{!leg.dateDropOff}" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="Start_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="Start_Date_Time__c" type="time" value="{!leg.timePickUp}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnThreeChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formColumnBlank"></div>
                                                                        <div class="formField">
                                                                            <label for="Location_Drop_Off_Type__c">Location Drop Off Type</label>
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Location_Drop_Off_Type__c" label="" value="{!leg.locationDropOff}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.locationDropOffTypes}" var="dropOffType">
                                                                                        <option value="{!dropOffType}">{!dropOffType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formField">
                                                                        <label for="Location_Details__c">Location Drop Off Details</label>
                                                                        <lightning:input type="text" aura:id="recordField" placeholder="Enter Location" name="Location_Details_Drop_Off__c" value="{!leg.locationDetailsDropOff}" variant="label-hidden" required="true" class="formInputTextarea" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="End_Date__c">Date</label><lightning:input aura:id="recordField" name="End_Date__c" type="date" dateStyle="short" value="{!leg.dateDropOff}" min="{!leg.datePickUp}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="End_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="End_Date_Time__c" type="time" value="{!leg.timeDropOff}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="buttonColumn">
                                                                <aura:if isTrue="{!legIndex>0}">
                                                                    <lightning:buttonIcon iconName="utility:clear" value="{!legIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveGroundLeg}" />
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="actions">
                                                        <lightning:button label="Add Leg" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddGroundLeg}" />
                                                    </div>
                                                </div>
                                                <aura:if isTrue="{!not(empty(ground.otherLegs)) || not(empty(ground.otherVehicles))}">
                                                    <div class="recordDetails">
                                                        <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                                            <div class="recordTitleText">
                                                                <div><i class="fas fa-route titleIcon" style="color: white;"></i> Other Legs and Vehicles (managed by RR Team)</div>
                                                            </div>
                                                            <div class="recordTitleButton">
                                                                <lightning:buttonIcon iconName="{!v.showOtherDetails==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowOtherDetails}" />
                                                            </div>
                                                        </div>
                                                        <div class="recordBodyContent" style="{!v.showOtherDetails!=true?'display: none;':''}">
                                                            <aura:iteration items="{!ground.otherLegs}" var="leg">
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;"><div class="tableHeader"><span>Trip Type</span></div><div class="tripInfo"><span>{!leg.subTripType}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Pick Up Type</div><div class="tripInfo"><span>{!leg.locationPickUp}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Pick Up Details</div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Drop Off Type</div><div class="tripInfo"><span>{!leg.locationDropOff}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Drop Off Details</div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </aura:iteration>
                                                            <aura:if isTrue="{!not(empty(ground.otherVehicles))}">
                                                                <div class="recordTable tableList">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Bus Type</span></div>
                                                                        <div style="flex: 1;"><span>Qty of Buses</span></div>
                                                                        <div style="flex: 1;"><span># of Passengers</span></div>
                                                                        <div style="flex: 2;"><span>Gear / Luggage Space Needed</span></div>
                                                                        <div style="flex: 1;"><span>Trip Type</span></div>
                                                                    </div>
                                                                    <aura:iteration items="{!ground.otherVehicles}" var="vehicle">
                                                                        <div class="tableRow">
                                                                            <div style="flex: 1;"><span>{!vehicle.busType}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.qtyOfBuses}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.passengers}</span></div>
                                                                            <div style="flex: 2;"><span>{!vehicle.gearLuggage}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.groupType}</span></div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                </div>
                                                            </aura:if>
                                                        </div>
                                                    </div>
                                                </aura:if>
                                                <div class="recordDetails">
                                                    <div class="recordTitle">
                                                        <div class="recordTitleText">
                                                            <div><i class="fas fa-map-marked-alt titleIcon"></i> Ground Details</div>
                                                        </div>
                                                        <div class="recordTitleButton">
                                                            <lightning:buttonIcon iconName="{!v.showRecordDetails==true?'utility:up':'utility:down'}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecordDetails}" />
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.showRecordDetails==true}">
                                                        <div class="recordBodyContent">
                                                            <div class="formColumnTwoChilds">
                                                                <div class="formField">
                                                                    <label for="Vehicle_Type__c">Bus Type</label>
                                                                    <div class="fieldSelect">
                                                                        <lightning:select name="Vehicle_Type__c" label="" value="{!ground.busType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                            <aura:iteration items="{!v.vehicleTypesGround}" var="vehicleType">
                                                                                <option value="{!vehicleType}">{!vehicleType}</option>
                                                                            </aura:iteration>
                                                                        </lightning:select>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField"><label for="Qty_of_Buses__c">Qty of Buses</label><lightning:input aura:id="recordField" name="Qty_of_Buses__c" type="number" value="{!ground.qtyOfBuses}" label="" min="1" step="1" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="Capacity__c"># of Passengers</label><lightning:input aura:id="recordField" name="Capacity__c" type="number" value="{!ground.passengers}" label="" min="1" step="1" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="formColumnTwoChilds">
                                                                <div class="formField">
                                                                    <label for="Gear_Luggage_Space__c">Gear / Luggage Space Needed</label>
                                                                    <lightning:input type="text" aura:id="recordField" name="Gear_Luggage_Space__c" value="{!ground.gearLuggage}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                </div>
                                                                <div class="formField">
                                                                    <label for="Group_Type__c">Group Type</label>
                                                                    <div class="fieldSelect">
                                                                        <lightning:select name="Group_Type__c" label="" value="{!ground.groupType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                            <option value="">--None--</option>
                                                                            <aura:iteration items="{!v.groupTypesGround}" var="groupType">
                                                                                <option value="{!groupType}">{!groupType}</option>
                                                                            </aura:iteration>
                                                                        </lightning:select>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="formField">
                                                                <label for="Amenities__c">Amenities</label>
                                                                <lightning:dualListbox name="Amenities__c"
                                                                                       label= ""
                                                                                       sourceLabel="Available"
                                                                                       selectedLabel="Chosen"
                                                                                       options="{!v.amenitiesGround}"
                                                                                       value="{!ground.amenitiesList}"
                                                                                       onchange="{!c.handleInputChange}"
                                                                                       variant="label-hidden" />
                                                            </div>
                                                            <div class="formField">
                                                                <label for="Other_Amenities__c">Other Amenities</label>
                                                                <lightning:input type="text" aura:id="recordField" name="Other_Amenities__c" value="{!ground.notes}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                            </div>
                                                            <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                                <label for="Client_Notes__c">Additional Notes</label>
                                                                <lightning:textarea aura:id="recordField" name="Client_Notes__c" label="" value="{!ground.additionalNotes}" variant="label-hidden" min="1" onchange="{!c.handleInputChange}" />
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <aura:iteration items="{!ground.allLegs}" var="leg">
                                                        <div class="recordTable tripTable">
                                                            <div class="tableTripRow">
                                                                <div class="tripList">
                                                                    <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;"><div class="tableHeader"><span>Trip Type</span></div><div class="tripInfo"><span>{!leg.subTripType}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Pick Up Type</div><div class="tripInfo"><span>{!leg.locationPickUp}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Pick Up Details</div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                </div>
                                                                <div class="tripList">
                                                                    <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Drop Off Type</div><div class="tripInfo"><span>{!leg.locationDropOff}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Drop Off Details</div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Bus Type</span></div>
                                                            <div style="flex: 1;"><span>Qty of Buses</span></div>
                                                            <div style="flex: 1;"><span># of Passengers</span></div>
                                                            <div style="flex: 2;"><span>Gear / Luggage Space Needed</span></div>
                                                            <div style="flex: 1;"><span>Trip Type</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;"><span>{!ground.busType}</span></div>
                                                            <div style="flex: 1;"><span>{!ground.qtyOfBuses}</span></div>
                                                            <div style="flex: 1;"><span>{!ground.passengers}</span></div>
                                                            <div style="flex: 2;"><span>{!ground.gearLuggage}</span></div>
                                                            <div style="flex: 1;"><span>{!ground.groupType}</span></div>
                                                        </div>
                                                        <aura:iteration items="{!ground.otherVehicles}" var="vehicle">
                                                            <div class="tableRow">
                                                                <div style="flex: 1;"><span>{!vehicle.busType}</span></div>
                                                                <div style="flex: 1;"><span>{!vehicle.qtyOfBuses}</span></div>
                                                                <div style="flex: 1;"><span>{!vehicle.passengers}</span></div>
                                                                <div style="flex: 2;"><span>{!vehicle.gearLuggage}</span></div>
                                                                <div style="flex: 1;"><span>{!vehicle.groupType}</span></div>
                                                            </div>
                                                        </aura:iteration>
                                                    </div>
                                                    <div class="recordTable tableList">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;">Amenities</div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;">
                                                                <aura:if isTrue="{!not(empty(ground.amenitiesList))}">
                                                                    <aura:iteration items="{!ground.amenitiesList}" var="amenitie" indexVar="indexAmenitie">
                                                                        {!amenitie+if(ground.amenitiesList.length-1>indexAmenitie,', ','')}
                                                                    </aura:iteration>
                                                                    {!if(not(empty(ground.notes)),', '+ground.notes,'')}
                                                                    <aura:set attribute="else">
                                                                        {!if(not(empty(ground.notes)),ground.notes,'-')}
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em; "><span style="font-weight: 500;">Additional Notes</span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!ground.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.groundRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='air'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-plane titleIcon"></i>Air Travel</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.flightRecords}" var="flight" indexVar="flightIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(flight.isLocked==true,'background-color: #0065ff; color: white;',if(flight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!flightIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!and(empty(flight.cityTitleStart),empty(flight.cityTitleEnd))}">
                                                <div class="location" title="{!'Trip '+(flightIndex+1)}">{!'Flight '+(flightIndex+1)}</div>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!flight.cityTitleStart+flight.cityTitleEnd}">{!flight.cityTitleStart+flight.cityTitleEnd}</div>
                                                    <div class="dates" style="{!if(empty(flight.startDateTitle),'display:none;','')}">{!flight.startDateTitle+(empty(flight.endDateTitle)? '' : ' - '+flight.endDateTitle)}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==flightIndex?'utility:up':'utility:down'}" value="{!flightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==flightIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(flight.isLocked==true,'background-color: #c5dcff;',if(flight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!flight.isLocked!=true}">
                                                <div>
                                                    <lightning:radioGroup aura:id="airForm" name="radioButtonGroup" label="" options="{!v.tripTypes}" value="{!flight.tripType}" type="button" class="noRadius" onchange="{!c.handleChangeAirTrip}" />
                                                </div>
                                                <div class="travels">
                                                    <aura:iteration items="{!flight.segments}" var="segment" indexVar="segmentIndex">
                                                        <div class="travelRow" style="margin-top: 0.5em;">
                                                            <div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField">
                                                                            <label for="Departure_Date__c">{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Return Date','Departure Date')}</label>
                                                                            <lightning:input aura:id="recordField" name="Departure_Date__c" type="date" dateStyle="short" value="{!segment.departureDate}" variant="label-hidden" required="true" label="{!segmentIndex}" min="{!if(segmentIndex>0,segment.arrivalDate,v.today)}" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                        </div>
                                                                        <div style="display: flex; width: 100%;">
                                                                            <div class="formField">
                                                                                <label for="Start_Date_Time__c">{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Return Time','Estimated Times')}</label>
                                                                                <div style="display: flex; width: 100%;">
                                                                                    <lightning:input aura:id="recordField" name="Dep_Time__c" type="time" value="{!segment.departureTimeStart}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                    <div style="display: flex; padding: 0 0.25em; justify-content: center; align-content: center; flex-direction: column;">TO</div>
                                                                                    <lightning:input aura:id="recordField" name="Arr_Time__c" type="time" value="{!segment.departureTimeEnd}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField">
                                                                            <c:VoyajerCustomLookup objectAPIName="Airport__c" 
                                                                                                   fieldName="Departure_City__c" 
                                                                                                   iconName="custom:custom20" 
                                                                                                   lookupId="{!segment.departureCityId}" 
                                                                                                   label="Departure City" 
                                                                                                   inputPlaceholder="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Enter Location Above','Enter Location')}" 
                                                                                                   isRequired="true" 
                                                                                                   isEdited="{!flight.isEdited}" 
                                                                                                   triggerLookupValidation="{!v.triggerLookupValidation}" 
                                                                                                   isDisabled="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),true,false)}" 
                                                                                                   airportRoundAux="{!c.onAirportRound}" />
                                                                        </div>
                                                                        <div class="formField">
                                                                            <c:VoyajerCustomLookup objectAPIName="Airport__c" 
                                                                                                   fieldName="Arrival_City__c" 
                                                                                                   iconName="custom:custom20" 
                                                                                                   lookupId="{!segment.arrivalCityId}" 
                                                                                                   label="Arrival City" 
                                                                                                   inputPlaceholder="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Enter Location Above','Enter Location')}" 
                                                                                                   isRequired="true" 
                                                                                                   isEdited="{!flight.isEdited}" 
                                                                                                   triggerLookupValidation="{!v.triggerLookupValidation}" 
                                                                                                   isDisabled="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),true,false)}" 
                                                                                                   airportRoundAux="{!c.onAirportRound}" />
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="buttonColumn">
                                                                <aura:if isTrue="{!segmentIndex>1}">
                                                                    <lightning:buttonIcon iconName="utility:clear" value="{!segmentIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveSegment}" />
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="actions">
                                                        <aura:if isTrue="{!flight.tripType=='Multi-City'}"><lightning:button label="Add Segment" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddSegment}" /></aura:if>
                                                    </div>
                                                </div>
                                                <div class="formColumnThreeChilds" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                    <div class="formField">
                                                        <label for="Class__c">Class of Service</label>
                                                        <div class="fieldSelect">
                                                            <lightning:select name="Class__c" label="" value="{!flight.classService}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                <aura:iteration items="{!v.classServicesAir}" var="classService">
                                                                    <option value="{!classService}">{!classService}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </div>
                                                    </div>
                                                    <div class="formField"><label for="PAX__c"># of Passengers</label><lightning:input aura:id="recordField" name="PAX__c" type="number" value="{!flight.pax}" label="" min="1" step="1" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                    <div class="formField">
                                                        <label for="Preferred_Airline__c">Preferred Airline</label>
                                                        <div class="fieldSelect">
                                                            <lightning:select name="Preferred_Airline__c" label="" value="{!flight.preferredAirline}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                <option value="">--None--</option>
                                                                <aura:iteration items="{!v.preferredAirlinesAir}" var="preferredAirline">
                                                                    <option value="{!preferredAirline}">{!preferredAirline}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                    <label for="Client_Notes__c">Additional Notes</label>
                                                    <lightning:textarea aura:id="recordField" name="Client_Notes__c" label="" value="{!flight.additionalNotes}" variant="label-hidden" min="1" onchange="{!c.handleInputChange}" />
                                                </div>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <aura:iteration items="{!flight.segments}" var="segment">
                                                        <div class="recordTable tableFields">
                                                            <div class="tableHeader">
                                                                <div style="flex: 2;"><span>Departure Date</span></div>
                                                                <div style="flex: 2;"><span>Estimated Times</span></div>
                                                                <div style="flex: 3;"><span>Departure City</span></div>
                                                                <div style="flex: 3;"><span>Arrival City</span></div>
                                                            </div>
                                                            <div class="tableRow">
                                                                <div style="flex: 2;"><span>{!segment.departureDate}</span></div>
                                                                <div style="flex: 2;"><span><lightning:formattedTime value="{!segment.departureTimeStart}" /> - <lightning:formattedTime value="{!segment.departureTimeEnd}" /></span></div>
                                                                <div style="flex: 3;"><span>{!segment.departureCityName}</span></div>
                                                                <div style="flex: 3;"><span>{!segment.arrivalCityName}</span></div>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 2;"><span>Type of Flight</span></div>
                                                            <div style="flex: 2;"><span>Class of Service</span></div>
                                                            <div style="flex: 3;"><span># of Passengers</span></div>
                                                            <div style="flex: 3;"><span>Preferred Airlines</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 2;"><span>{!flight.tripType}</span></div>
                                                            <div style="flex: 2;"><span>{!flight.classService}</span></div>
                                                            <div style="flex: 3;"><span>{!flight.pax}</span></div>
                                                            <div style="flex: 3;"><span>{!flight.preferredAirline}</span></div>
                                                        </div>
                                                    </div>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!flight.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.flightRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='freight'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-truck titleIcon"></i>Freight</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.freightRecords}" var="freight" indexVar="freightIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(freight.isLocked==true,'background-color: #0065ff; color: white;',if(freight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!freightIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!and(empty(freight.cityTitleStart),empty(freight.cityTitleEnd))}">
                                                <div class="location" title="{!'Trip '+(freightIndex+1)}">{!'Trip '+(freightIndex+1)}</div>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!freight.cityTitleStart+freight.cityTitleEnd}">{!freight.cityTitleStart+freight.cityTitleEnd}</div>
                                                    <div class="dates" style="{!if(empty(freight.startDateTitle),'display:none;','')}">{!freight.startDateTitle} - {!freight.endDateTitle}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==freightIndex?'utility:up':'utility:down'}" value="{!freightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==freightIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(freight.isLocked==true,'background-color: #c5dcff;',if(freight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!freight.isLocked!=true}">
                                                <div class="travels">
                                                    <aura:iteration items="{!freight.legs}" var="leg" indexVar="legIndex">
                                                        <div class="travelRow" style="{!if(legIndex>0,'border-top: 1px solid #dbdbdb; margin-top: 0.5em;','')}">
                                                            <div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField">
                                                                        <label for="Location_Details__c">Pick Up Location</label>
                                                                        <lightning:input type="text" aura:id="recordField" name="Location_Details__c" value="{!leg.locationDetailsPickUp}" placeholder="Enter Location" variant="label-hidden" required="true" class="formInputTextarea" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="Start_Date__c">Date</label><lightning:input aura:id="recordField" name="Start_Date__c" type="date" dateStyle="short" value="{!leg.datePickUp}" variant="label-hidden" required="true" min="{!v.today}" max="{!leg.dateDropOff}" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="Start_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="Start_Date_Time__c" type="time" value="{!leg.timePickUp}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField">
                                                                        <label for="Location_Details_Drop_Off__c">Drop Off Location</label>
                                                                        <lightning:input type="text" aura:id="recordField" name="Location_Details_Drop_Off__c" value="{!leg.locationDetailsDropOff}" placeholder="Enter Location" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="End_Date__c">Date</label><lightning:input aura:id="recordField" name="End_Date__c" type="date" dateStyle="short" value="{!leg.dateDropOff}" min="{!leg.datePickUp}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="End_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="End_Date_Time__c" type="time" value="{!leg.timeDropOff}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="buttonColumn">
                                                                <aura:if isTrue="{!legIndex>0}">
                                                                    <lightning:buttonIcon iconName="utility:clear" value="{!legIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveFreightLeg}" />
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="actions">
                                                        <lightning:button label="Add Leg" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddFreightLeg}" />
                                                    </div>
                                                </div>
                                                <aura:if isTrue="{!not(empty(freight.otherLegs))}">
                                                    <div class="recordDetails">
                                                        <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                                            <div class="recordTitleText">
                                                                <div><i class="fas fa-luggage-cart titleIcon" style="color: white;"></i> Other Legs (managed by RR Team)</div>
                                                            </div>
                                                            <div class="recordTitleButton">
                                                                <lightning:buttonIcon iconName="{!v.showOtherDetails==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowOtherDetails}" />
                                                            </div>
                                                        </div>
                                                        <div class="recordBodyContent" style="{!v.showOtherDetails!=true?'display: none;':''}">
                                                            <aura:iteration items="{!freight.otherLegs}" var="leg">
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow"><div class="tableHeader"><span>Pick Up Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow"><div class="tableHeader">Drop Off Location</div><div class="tripInfo">{!leg.locationDetailsDropOff}</div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Date of Drop Off</div><div class="tripInfo"><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Time of Drop Off</div><div class="tripInfo"><lightning:formattedTime value="{!leg.timeDropOff}" /></div></div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                </aura:if>
                                                <div class="recordDetails">
                                                    <div class="recordTitle">
                                                        <div class="recordTitleText">
                                                            <div><i class="fas fa-map-marked-alt titleIcon"></i> Freight Details</div>
                                                        </div>
                                                        <div class="recordTitleButton">
                                                            <lightning:buttonIcon iconName="{!v.showRecordDetails==true?'utility:up':'utility:down'}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecordDetails}" />
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.showRecordDetails==true}">
                                                        <div class="recordBodyContent">
                                                            <div class="formColumnTwoChilds">
                                                                <div class="formField">
                                                                    <label for="Service_Type__c">Freight Type</label>
                                                                    <div class="fieldSelect">
                                                                        <lightning:select name="Service_Type__c" label="" value="{!freight.groupType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                            <aura:iteration items="{!v.groupTypesFreight}" var="groupType">
                                                                                <option value="{!groupType}">{!groupType}</option>
                                                                            </aura:iteration>
                                                                        </lightning:select>
                                                                    </div>
                                                                </div>
                                                                <div class="formField">
                                                                    <label for="Freight_Trip_Contents__c">Contents</label>
                                                                    <lightning:input type="text" aura:id="recordField" name="Freight_Trip_Contents__c" value="{!freight.notes}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                </div>
                                                            </div>
                                                            <div style="text-align: end; padding: 0.5em 0;">
                                                                <aura:if isTrue="{!not(empty(freight.manifestName))}">
                                                                    <div style="display: inline-flex; padding: 0.5em; white-space: nowrap; text-overflow: ellipsis; overflow: hidden; width: 16em;">
                                                                        <span style="padding-right: 0.5em;">Manifest:</span>
                                                                        <span style="font-style: italic;">{!freight.manifestName}</span>
                                                                    </div>
                                                                </aura:if>
                                                                <lightning:button label="Attach Manifest" iconName="utility:note" variant="brand" class="formButtonBrand" onclick="{!c.handleAttachManifestMessage}" />
                                                            </div>
                                                            <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                                <label for="Client_Notes__c">Additional Notes</label>
                                                                <lightning:textarea aura:id="recordField" name="Client_Notes__c" label="" value="{!freight.additionalNotes}" variant="label-hidden" onchange="{!c.handleInputChange}" />
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <aura:iteration items="{!freight.allLegs}" var="leg">
                                                        <div class="recordTable tripTable">
                                                            <div class="tableTripRow">
                                                                <div class="tripList">
                                                                    <div class="tableRow"><div class="tableHeader"><span>Pick Up Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                </div>
                                                                <div class="tripList">
                                                                    <div class="tableRow"><div class="tableHeader"><span>Drop Off Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Freight Type</span></div>
                                                            <div style="flex: 1;"><span>Contents</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;"><span>{!freight.groupType}</span></div>
                                                            <div style="flex: 1;"><span>{!freight.notes}</span></div>
                                                        </div>
                                                        <div class="tableRow" style="border-top: 1px solid #dbdbdb;">
                                                            <div class="tableHeader"><span>Manifest File Attached</span></div>
                                                            <div class="tripInfo"><span>{!freight.manifestName}</span></div>
                                                        </div>
                                                    </div>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!freight.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.freightRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='review'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-paper-plane titleIcon"></i>Review &amp; Submit</h1>
                        </div>
                    </div>
                    <div class="page-section" style="align-items: flex-end; justify-content: flex-end; width: 100%;">
                        <div class="topNavigator" style="border-bottom: 0; ">
                            <div class="buttonsNavigator">
                                <aura:if isTrue="{!v.isLodgingSelected}">
                                    <div class="centerDiv" onclick="{!c.showLodgingRecords}" style="{!v.tabSelected=='Lodging'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Lodging</div>
                                        <div class="showOnTablet"><i class="fas fa-home tabIcon"></i></div>
                                    </div>
                                </aura:if>
                                <aura:if isTrue="{!v.isGroundSelected}">
                                    <div class="centerDiv" onclick="{!c.showGroundRecords}" style="{!v.tabSelected=='Ground Travel'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Ground Travel</div>
                                        <div class="showOnTablet"><i class="fas fa-car tabIcon"></i></div>
                                    </div>
                                </aura:if>
                                <aura:if isTrue="{!v.isAirSelected}">
                                    <div class="centerDiv" onclick="{!c.showAirRecords}" style="{!v.tabSelected=='Air'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Air</div>
                                        <div class="showOnTablet"><i class="fas fa-plane tabIcon"></i></div>
                                    </div>
                                </aura:if>
                                <aura:if isTrue="{!v.isFreightSelected}">
                                    <div class="centerDiv" onclick="{!c.showFreightRecords}" style="{!v.tabSelected=='Freight'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Freight</div>
                                        <div class="showOnTablet"><i class="fas fa-truck tabIcon"></i></div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </div>
                    <div class="page-section" style="align-items: center; width: 100%;">
                        <div class="page-section_record" style="margin-top: 0;">
                            <div class="recordHeader">
                                <div class="recordTitle">
                                    <div class="recordTitleText">
                                        <div><i class="fas fa-map-marked-alt titleIcon"></i> {!v.tabSelected} Review</div>
                                    </div>
                                </div>
                            </div>
                            <div class="recordBody">
                                <div class="recordBodyContent">
                                    <aura:if isTrue="{!v.tabSelected=='Lodging'}">
                                        <aura:iteration items="{!v.lodgingRecords}" var="lodging" indexVar="lodgingIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(lodging.isLocked==true,'background-color: #0065ff; color: white;',if(lodging.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!lodgingIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!empty(lodging.cityTitle)}">
                                                                    <div class="location" title="{!'Stay '+(lodgingIndex+1)}">{!'Stay '+(lodgingIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!lodging.cityTitle}">{!lodging.cityTitle}</div>
                                                                        <div class="dates" style="{!if(empty(lodging.startDateTitle),'display:none;','')}">{!lodging.startDateTitle} - {!lodging.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==lodgingIndex?'utility:up':'utility:down'}" value="{!lodgingIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==lodgingIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(lodging.isLocked==true,'background-color: #c5dcff;',if(lodging.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                                <div class="tableHeader"><span>Lodging Type</span></div>
                                                                                <div class="tripInfo">
                                                                                    <aura:if isTrue="{!lodging.lodgingType == 'housingHotel'}"><span>Group hotel</span></aura:if>
                                                                                    <aura:if isTrue="{!lodging.lodgingType == 'housingCorp'}"><span>Apartment/Private Home</span></aura:if>
                                                                                    <aura:if isTrue="{!lodging.lodgingType == 'housingIR'}"><span>Less than 10 rooms</span></aura:if>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Check-In</span></div>
                                                                        <div style="flex: 1;"><span>Check-Out</span></div>
                                                                        <div class="tableLocation"><span>Location</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.startDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                                        <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.endDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                                        <div class="tableLocation"><span>{!lodging.cityTitle}</span></div>
                                                                    </div>
                                                                </div>
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                                <div class="tableHeader"><span>Venue City</span></div>
                                                                                <div class="tripInfo">
                                                                                    <span>{!not(empty(lodging.venueId))? lodging.venueName : lodging.otherVenue}</span>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Budget Target</span></div>
                                                                        <div style="flex: 1;"><span>Hotel Stars</span></div>
                                                                        <div style="flex: 1;"><span>Hotel Type</span></div>
                                                                        <div style="flex: 1;"><span>Distance to Event</span></div>
                                                                        <div style="flex: 2;"><span>Preferred Brands</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.budgetTarget}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelStars}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelType}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.distanceFromEvent}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 2;">
                                                                            <aura:if isTrue="{!not(empty(lodging.preferredBrandsList))}">
                                                                                <span>
                                                                                    <aura:iteration items="{!lodging.preferredBrandsList}" var="brand" indexVar="indexBrand">
                                                                                        {!brand+if(lodging.preferredBrandsList.length-1>indexBrand,', ','')}
                                                                                    </aura:iteration>
                                                                                </span>
                                                                                <!--<ul class="slds-list_dotted"><aura:iteration items="{!lodging.preferredBrandsList}" var="brand"><li style="white-space: pre-wrap;">{!brand}</li></aura:iteration></ul>-->
                                                                                <aura:set attribute="else">-</aura:set>
                                                                            </aura:if>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!not(empty(lodging.allRoomTypeRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;"><span>Room Type</span></div>
                                                                            <div style="display: flex; min-width: 12em; justify-content: center;"><span>Qty of Rooms</span></div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.allRoomTypeRecords}" var="room" indexVar="roomIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;"><span>{!room.Unit_Type__c}</span></div>
                                                                                <div style="display: flex; min-width: 12em; justify-content: center;"><span>{!room.Units__c}</span></div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                                <aura:if isTrue="{!not(empty(lodging.allConcessionRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;"><span>Concessions</span></div>
                                                                            <div style="flex: 1"><span>Notes</span></div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.allConcessionRecords}" var="concession" indexVar="concessionIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;"><span>{!concession.Concessions_Requested__c}</span></div>
                                                                                <div style="flex: 1"><span>{!concession.Notes__c}</span></div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!lodging.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!lodging.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                    <aura:if isTrue="{!v.tabSelected=='Ground Travel'}">
                                        <aura:iteration items="{!v.groundRecords}" var="ground" indexVar="groundIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(ground.isLocked==true,'background-color: #0065ff; color: white;',if(ground.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!groundIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!and(empty(ground.cityTitleStart),empty(ground.cityTitleEnd))}">
                                                                    <div class="location" title="{!'Trip '+(groundIndex+1)}">{!'Trip '+(groundIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!ground.cityTitleStart+ground.cityTitleEnd}">{!ground.cityTitleStart+ground.cityTitleEnd}</div>
                                                                        <div class="dates" style="{!if(empty(ground.startDateTitle),'display:none;','')}">{!ground.startDateTitle} - {!ground.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==groundIndex?'utility:up':'utility:down'}" value="{!groundIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==groundIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(ground.isLocked==true,'background-color: #c5dcff;',if(ground.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <aura:iteration items="{!ground.allLegs}" var="leg">
                                                                    <div class="recordTable tripTable">
                                                                        <div class="tableTripRow">
                                                                            <div class="tripList">
                                                                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;"><div class="tableHeader"><span>Trip Type</span></div><div class="tripInfo"><span>{!leg.subTripType}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Pick Up Type</div><div class="tripInfo"><span>{!leg.locationPickUp}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Pick Up Details</div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                            </div>
                                                                            <div class="tripList">
                                                                                <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Drop Off Type</div><div class="tripInfo"><span>{!leg.locationDropOff}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Drop Off Details</div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </aura:iteration>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Bus Type</span></div>
                                                                        <div style="flex: 1;"><span>Qty of Buses</span></div>
                                                                        <div style="flex: 1;"><span># of Passengers</span></div>
                                                                        <div style="flex: 2;"><span>Gear / Luggage Space Needed</span></div>
                                                                        <div style="flex: 1;"><span>Trip Type</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;"><span>{!ground.busType}</span></div>
                                                                        <div style="flex: 1;"><span>{!ground.qtyOfBuses}</span></div>
                                                                        <div style="flex: 1;"><span>{!ground.passengers}</span></div>
                                                                        <div style="flex: 2;"><span>{!ground.gearLuggage}</span></div>
                                                                        <div style="flex: 1;"><span>{!ground.groupType}</span></div>
                                                                    </div>
                                                                    <aura:iteration items="{!ground.otherVehicles}" var="vehicle">
                                                                        <div class="tableRow">
                                                                            <div style="flex: 1;"><span>{!vehicle.busType}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.qtyOfBuses}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.passengers}</span></div>
                                                                            <div style="flex: 2;"><span>{!vehicle.gearLuggage}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.groupType}</span></div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                </div>
                                                                <div class="recordTable tableList">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;">Amenities</div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;">
                                                                            <aura:if isTrue="{!not(empty(ground.amenitiesList))}">
                                                                                <aura:iteration items="{!ground.amenitiesList}" var="amenitie" indexVar="indexAmenitie">
                                                                                    {!amenitie+if(ground.amenitiesList.length-1>indexAmenitie,', ','')}
                                                                                </aura:iteration>
                                                                                {!if(not(empty(ground.notes)),', '+ground.notes,'')}
                                                                                <aura:set attribute="else">
                                                                                    {!if(not(empty(ground.notes)),ground.notes,'-')}
                                                                                </aura:set>
                                                                            </aura:if>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em; "><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!ground.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!ground.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                    <aura:if isTrue="{!v.tabSelected=='Air'}">
                                        <aura:iteration items="{!v.flightRecords}" var="flight" indexVar="flightIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(flight.isLocked==true,'background-color: #0065ff; color: white;',if(flight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!flightIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!and(empty(flight.cityTitleStart),empty(flight.cityTitleEnd))}">
                                                                    <div class="location" title="{!'Trip '+(flightIndex+1)}">{!'Flight '+(flightIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!flight.cityTitleStart+flight.cityTitleEnd}">{!flight.cityTitleStart+flight.cityTitleEnd}</div>
                                                                        <div class="dates" style="{!if(empty(flight.startDateTitle),'display:none;','')}">{!flight.startDateTitle} - {!flight.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==flightIndex?'utility:up':'utility:down'}" value="{!flightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==flightIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(flight.isLocked==true,'background-color: #c5dcff;',if(flight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <aura:iteration items="{!flight.segments}" var="segment">
                                                                    <div class="recordTable tableFields">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 2;"><span>Departure Date</span></div>
                                                                            <div style="flex: 2;"><span>Estimated Times</span></div>
                                                                            <div style="flex: 3;"><span>Departure City</span></div>
                                                                            <div style="flex: 3;"><span>Arrival City</span></div>
                                                                        </div>
                                                                        <div class="tableRow">
                                                                            <div style="flex: 2;"><span>{!segment.departureDate}</span></div>
                                                                            <div style="flex: 2;"><span><lightning:formattedTime value="{!segment.departureTimeStart}" /> - <lightning:formattedTime value="{!segment.departureTimeEnd}" /></span></div>
                                                                            <div style="flex: 3;"><span>{!segment.departureCityName}</span></div>
                                                                            <div style="flex: 3;"><span>{!segment.arrivalCityName}</span></div>
                                                                        </div>
                                                                    </div>
                                                                </aura:iteration>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 2;"><span>Type of Flight</span></div>
                                                                        <div style="flex: 2;"><span>Class of Service</span></div>
                                                                        <div style="flex: 3;"><span># of Passengers</span></div>
                                                                        <div style="flex: 3;"><span>Preferred Airlines</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 2;"><span>{!flight.tripType}</span></div>
                                                                        <div style="flex: 2;"><span>{!flight.classService}</span></div>
                                                                        <div style="flex: 3;"><span>{!flight.pax}</span></div>
                                                                        <div style="flex: 3;"><span>{!flight.preferredAirline}</span></div>
                                                                    </div>
                                                                </div>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!flight.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!flight.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                    <aura:if isTrue="{!v.tabSelected=='Freight'}">
                                        <aura:iteration items="{!v.freightRecords}" var="freight" indexVar="freightIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(freight.isLocked==true,'background-color: #0065ff; color: white;',if(freight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!freightIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!and(empty(freight.cityTitleStart),empty(freight.cityTitleEnd))}">
                                                                    <div class="location" title="{!'Trip '+(freightIndex+1)}">{!'Trip '+(freightIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!freight.cityTitleStart+freight.cityTitleEnd}">{!freight.cityTitleStart+freight.cityTitleEnd}</div>
                                                                        <div class="dates" style="{!if(empty(freight.startDateTitle),'display:none;','')}">{!freight.startDateTitle} - {!freight.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==freightIndex?'utility:up':'utility:down'}" value="{!freightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==freightIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(freight.isLocked==true,'background-color: #c5dcff;',if(freight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <aura:iteration items="{!freight.allLegs}" var="leg">
                                                                    <div class="recordTable tripTable">
                                                                        <div class="tableTripRow">
                                                                            <div class="tripList">
                                                                                <div class="tableRow"><div class="tableHeader"><span>Pick Up Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                            </div>
                                                                            <div class="tripList">
                                                                                <div class="tableRow"><div class="tableHeader"><span>Drop Off Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </aura:iteration>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Freight Type</span></div>
                                                                        <div style="flex: 1;"><span>Contents</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;"><span>{!freight.groupType}</span></div>
                                                                        <div style="flex: 1;"><span>{!freight.notes}</span></div>
                                                                    </div>
                                                                    <div class="tableRow" style="border-top: 1px solid #dbdbdb;">
                                                                        <div class="tableHeader"><span>Manifest File Attached</span></div>
                                                                        <div class="tripInfo"><span>{!freight.manifestName}</span></div>
                                                                    </div>
                                                                </div>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!freight.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!freight.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <lightning:button label="Submit" variant="brand" class="formButtonBrand" onclick="{!c.handleSubmit}" />
                    </div>
                </aura:if>
            </div>
            <aura:if isTrue="{!v.openAttachment}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container" style="max-width: 24em;">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Attach your manifest</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <div style="text-align: center;"><lightning:fileUpload label="" recordId="{!v.userId}" onuploadfinished="{!c.handleUploadFinished}" /></div>
                            <div style="display: flex; justify-content: center; margin-top: 1em;"><lightning:fileCard fileId="{!v.fileId}" description="{!v.fileName}"/></div>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="Cancel" title="Cancel" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Confirm" title="Confirm" variant="brand" class="formButtonBrandLight" onclick="{!c.handleConfirmFile}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openBackConfirmation}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">We need a confirmation!</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You have records pending to be saved. All your changes will be lost.</p>
                            <br/>
                            <p>Do you want to go back?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="Not yet" title="Not yet" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Go back" title="Go back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openNextConfirmation}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">We need a confirmation!</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You have records pending to be saved. All your changes will be lost.</p>
                            <br/>
                            <p>Do you want to continue?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="Not yet" title="Not yet" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Continue" title="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
        </div>
    </div>
</aura:component>
```
### VoyajerItineraryController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        component.set('v.today', today);
        var userId = $A.get("$SObjectType.CurrentUser.Id");
        component.set("v.userId",userId);
        component.set("v.menuSelected","");
        component.set("v.itineraryData",{services:""});
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadProductionServices");
        callToParent.fire();
	},
    
    loadItineraryData : function(component, event, helper) {
        function isEmpty(obj) {
            for(var key in obj) if(obj.hasOwnProperty(key)) return false;
            return true;
        }
        var menuSelected = component.get("v.menuSelected");
        var itineraryData = component.get("v.itineraryData");
        console.log(JSON.parse(JSON.stringify(itineraryData)));
        if(!!menuSelected) {
            var servicesSaved = itineraryData.services;
            switch (menuSelected) {
                case "services":
                    if(servicesSaved.includes("Housing")) component.set("v.isLodgingSelected",true);
                    component.set("v.isLodgingLocked",itineraryData.isLodgingLocked);
                    if(servicesSaved.includes("Ground Travel")) component.set("v.isGroundSelected",true);
                    component.set("v.isGroundLocked",itineraryData.isGroundLocked);
                    if(servicesSaved.includes("Air")) component.set("v.isAirSelected",true);
                    component.set("v.isAirLocked",itineraryData.isAirLocked);
                    if(servicesSaved.includes("Freight")) component.set("v.isFreightSelected",true);
                    component.set("v.isFreightLocked",itineraryData.isFreightLocked);
                    break;
                case "housing":
                    if(!itineraryData.hasOwnProperty("lodgingRecords")) {
                        console.log("loadItineraryData->loadLodgingPage");
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadLodgingPage");
                        callToParent.fire();
                    }
                    else {
                        console.log("loadItineraryData->setLodgingPage");
                        var lodgingRecords = JSON.parse(JSON.stringify(itineraryData.lodgingRecords));
                        if(itineraryData.hasOwnProperty("salesForHousing")) {
                            component.set("v.salesForHousing",itineraryData.salesForHousing);
                            component.set("v.salesHousingRoomTypes",itineraryData.salesHousingRoomTypes);
                            component.set("v.salesHousingConcessions",itineraryData.salesHousingConcessions);
                        } else if(isEmpty(component.get("v.salesForHousing"))) {
                            component.set("v.salesForHousing",{});
                            component.set("v.salesHousingRoomTypes",[]);
                            component.set("v.salesHousingConcessions",[]);
                        }
                        component.set("v.lodgingRecords",lodgingRecords);
                        component.set("v.distanceFromEventOptions",itineraryData.distanceFromEventOptions);
                        component.set("v.hotelStars",itineraryData.hotelStars);
                        component.set("v.hotelTypes",itineraryData.hotelTypes);
                        component.set("v.preferredBrands",itineraryData.preferredBrands);
                        component.set("v.roomTypes",itineraryData.roomTypes);
                        component.set("v.concessionHousingTypes",itineraryData.concessionHousingTypes);
                        component.set("v.concessionCorporateTypes",itineraryData.concessionCorporateTypes);
                    }
                    break;
                case "ground":
                    if(!itineraryData.hasOwnProperty("groundRecords")) {
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadGroundPage");
                        callToParent.fire();
                    }
                    else {
                        var groundRecords = JSON.parse(JSON.stringify(itineraryData.groundRecords));
                        if(itineraryData.hasOwnProperty("salesForGround")) component.set("v.salesForGround",itineraryData.salesForGround);
                        else if(isEmpty(component.get("v.salesForGround"))) component.set("v.salesForGround",{});
                        component.set("v.groundRecords",groundRecords);
                        component.set("v.tripTypesGround",itineraryData.tripTypesGround);
                        component.set("v.locationPickUpTypes",itineraryData.locationPickUpTypes);
                        component.set("v.locationDropOffTypes",itineraryData.locationDropOffTypes);
                        component.set("v.vehicleTypesGround",itineraryData.vehicleTypesGround);
                        component.set("v.groupTypesGround",itineraryData.groupTypesGround);
                        component.set("v.amenitiesGround",itineraryData.amenitiesGround);
                    }
                    break;
                case "air":
                    if(!itineraryData.hasOwnProperty("flightRecords")) {
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadAirPage");
                        callToParent.fire();
                    }
                    else {
                        var flightRecords = JSON.parse(JSON.stringify(itineraryData.flightRecords));
                        if(itineraryData.hasOwnProperty("salesForAir")) component.set("v.salesForAir",itineraryData.salesForAir);
                        else if(isEmpty(component.get("v.salesForAir"))) component.set("v.salesForAir",{});
                        component.set("v.classServicesAir",itineraryData.classServicesAir);
                        component.set("v.preferredAirlinesAir",itineraryData.preferredAirlinesAir);
                        component.set("v.flightRecords",flightRecords);
                    }
                    break;
                case "freight":
                    if(!itineraryData.hasOwnProperty("freightRecords")) {
                        var callToParent = component.getEvent("callToParent");
                        callToParent.setParam("action","loadFreightPage");
                        callToParent.fire();
                    }
                    else {
                        var freightRecords = JSON.parse(JSON.stringify(itineraryData.freightRecords));
                        if(itineraryData.hasOwnProperty("salesForFreight")) component.set("v.salesForFreight",itineraryData.salesForFreight);
                        else if(isEmpty(component.get("v.salesForFreight"))) component.set("v.salesForFreight",{});
                        component.set("v.groupTypesFreight",itineraryData.groupTypesFreight);
                        component.set("v.freightRecords",freightRecords);
                    }
                    break;
                default:
                    break;
            }
            var menuOptions = component.get("v.menuOptions");
            var menuOptionsSelected = [{ label: "Select Services", value: "services", icon: "fa-hand-pointer", checked: true }];
            if(menuOptions.length < 2) {
                var checked = true;
                if(menuSelected == "services") checked = false;
                if(servicesSaved.includes("Housing")) menuOptionsSelected.push({ label: "Lodging", value: "housing", icon: "fa-home", checked: checked });
                if(menuSelected == "housing") checked = false;
                if(servicesSaved.includes("Ground Travel")) menuOptionsSelected.push({ label: "Ground Travel", value: "ground", icon: "fa-car", checked: checked });
                if(menuSelected == "ground") checked = false;
                if(servicesSaved.includes("Air")) menuOptionsSelected.push({ label: "Air Travel", value: "air", icon: "fa-plane", checked: checked });
                if(menuSelected == "air") checked = false;
                if(servicesSaved.includes("Freight")) menuOptionsSelected.push({ label: "Freight", value: "freight", icon: "fa-truck", checked: checked });
                if(menuSelected == "freight") checked = false;
                if(menuOptionsSelected.length>1) menuOptionsSelected.push({ label: "Review & Submit", value: "review", icon: "fa-paper-plane", checked: checked });
                menuOptions = menuOptionsSelected.slice(0);
            } else {
                menuOptions.forEach(item => { if(item.value == menuSelected) item.checked = true; })
            }
            component.set("v.menuOptions",menuOptions);
        }
    },
    
    toggleItineraryService : function(component, event, helper) {
        var service = event.getSource().get("v.alternativeText");
        var servicesSaved = component.get("v.itineraryData").services;
        var toastEvent = $A.get("e.force:showToast");
        toastEvent.setParams({ type: "error", title: "", message: "You are not able to unselect services that have itineraries created for them. Please contact your Road Rebel Coordinator." });
        if(service.toLowerCase() == "lodging") { if(component.get("v.isLodgingSelected") && component.get("v.isLodgingLocked")) toastEvent.fire(); else  component.set("v.isLodgingSelected",!component.get("v.isLodgingSelected")); }
        if(service.toLowerCase() == "ground travel") { if(component.get("v.isGroundSelected") && component.get("v.isGroundLocked")) toastEvent.fire(); else component.set("v.isGroundSelected",!component.get("v.isGroundSelected")); }
        if(service.toLowerCase() == "air travel") { if(component.get("v.isAirSelected") && component.get("v.isAirLocked")) toastEvent.fire(); else component.set("v.isAirSelected",!component.get("v.isAirSelected")); }
        if(service.toLowerCase() == "freight") { if(component.get("v.isFreightSelected") && component.get("v.isFreightLocked")) toastEvent.fire(); else component.set("v.isFreightSelected",!component.get("v.isFreightSelected")); }
    },
    
    saveServices : function(component, event, helper) {
        var servicesSelected = "";
        if(component.get("v.isLodgingSelected")) servicesSelected += "Housing;";
        if(component.get("v.isGroundSelected")) servicesSelected += "Ground Travel;";
        if(component.get("v.isAirSelected")) servicesSelected += "Air;";
        if(component.get("v.isFreightSelected")) servicesSelected += "Freight;";
        if(servicesSelected.length==0) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "You need to select at least one service"
            });
            toastEvent.fire();
        } else {
            var callToParent = component.getEvent("callToParent");
            component.set("v.menuOptions",[]);
            callToParent.setParam("action","saveServices");
            callToParent.setParam("data",{ productionId: component.get("v.productionSelected"), services: servicesSelected});
            callToParent.fire();
        }
    },
    
    handleNewDates : function(component, event, helper) {
        function isEmpty(obj) {
            for(var key in obj) if(obj.hasOwnProperty(key)) return false;
            return true;
        }
        var itineraryData = component.get("v.itineraryData");
        var menuSelected = component.get("v.menuSelected");
        var index = -1;
        switch (menuSelected) {
            case "housing":
                var lodgingRecords = component.get("v.lodgingRecords");
                index = lodgingRecords.length;
                var salesForHousing = component.get("v.salesForHousing");
                if(!isEmpty(salesForHousing)) {
                    lodgingRecords.push({
                        itineraryId: "",
                        startDate: component.get("v.today"),
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        cityId: "",
                        cityTitle: "",
                        lodgingId: "",
                        lodgingType: "",
                        budgetTarget: salesForHousing.hasOwnProperty("Budget__c")? salesForHousing.Budget__c : 0.00,
                        hotelStars: salesForHousing.hasOwnProperty("Star_Preference__c")? salesForHousing.Star_Preference__c : component.get("v.hotelStars")[0],
                        hotelType: salesForHousing.hasOwnProperty("Hotel_Class__c")? salesForHousing.Hotel_Class__c : component.get("v.hotelTypes")[0],
                        distanceFromEvent: salesForHousing.hasOwnProperty("Distance_to_Venue__c")? salesForHousing.Distance_to_Venue__c : component.get("v.distanceFromEventOptions")[0],
                        preferredBrands: salesForHousing.hasOwnProperty("Brand_Preference__c")? salesForHousing.Brand_Preference__c : "",
                        preferredBrandsList: salesForHousing.hasOwnProperty("Brand_Preference__c")? salesForHousing.Brand_Preference__c.split(";") : [],
                        additionalNotes: "",
                        roomTypeRecords: component.get("v.salesHousingRoomTypes"),
                        concessionRecords: [],
                        otherRoomTypeRecords: [],
                        otherConcessionRecords: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                else {
                    lodgingRecords.push({
                        itineraryId: "",
                        startDate: component.get("v.today"),
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        cityId: "",
                        cityTitle: "",
                        lodgingId: "",
                        lodgingType: "",
                        budgetTarget: 0,
                        hotelStars: component.get("v.hotelStars")[0],
                        hotelType: component.get("v.hotelTypes")[0],
                        distanceFromEvent: component.get("v.distanceFromEventOptions")[0],
                        preferredBrands: "",
                        preferredBrandsList: [],
                        additionalNotes: "",
                        roomTypeRecords: [],
                        concessionRecords: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                component.set("v.lodgingRecords",lodgingRecords);
                break;
            case "ground":
                var groundRecords = component.get("v.groundRecords");
                index = groundRecords.length;
                var salesForGround = component.get("v.salesForGround");
                if(!isEmpty(salesForGround)) {
                    groundRecords.push({
                        itineraryId: "",
                        cityTitle: "",
                        startDate: "",
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        tripDetailsId: "",
                        additionalNotes: "",
                        busType: salesForGround.hasOwnProperty("busType")? salesForGround.busType : "",
                        qtyOfBuses: salesForGround.hasOwnProperty("qtyOfBuses")? salesForGround.qtyOfBuses : 1,
                        passengers: salesForGround.hasOwnProperty("passengers")? salesForGround.passengers : 1,
                        gearLuggage: salesForGround.hasOwnProperty("gearLuggage")? salesForGround.gearLuggage : "",
                        groupType: "",
                        amenities: salesForGround.hasOwnProperty("amenities")? salesForGround.amenities : "",
                        amenitiesList: salesForGround.hasOwnProperty("amenities")? salesForGround.amenities.split(";") : [],
                        notes: salesForGround.hasOwnProperty("notes")? salesForGround.notes : "",
                        legs: [{
                            subTripDetailsId: "",
                            subTripType: component.get("v.tripTypesGround")[0],
                            legId: "",
                            locationPickUp: component.get("v.locationPickUpTypes")[0],
                            locationDropOff: component.get("v.locationDropOffTypes")[0],
                            locationDetailsPickUp: "",
                            locationDetailsDropOff: "",
                            datePickUp: component.get("v.today"),
                            timePickUp: "",
                            dateDropOff: "",
                            timeDropOff: ""
                        }],
                        otherLegs: [],
                        otherVehicles: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                else {
                    groundRecords.push({
                        itineraryId: "",
                        cityTitle: "",
                        startDate: "",
                        startDateTitle: "",
                        endDate: "",
                        endDateTitle: "",
                        tripDetailsId: "",
                        additionalNotes: "",
                        busType: "",
                        qtyOfBuses: 1,
                        passengers: 1,
                        gearLuggage: "",
                        groupType: "",
                        amenities: "",
                        amenitiesList: [],
                        notes: "",
                        legs: [{
                            subTripDetailsId: "",
                            subTripType: component.get("v.tripTypesGround")[0],
                            legId: "",
                            locationPickUp: component.get("v.locationPickUpTypes")[0],
                            locationDropOff: component.get("v.locationDropOffTypes")[0],
                            locationDetailsPickUp: "",
                            locationDetailsDropOff: "",
                            datePickUp: component.get("v.today"),
                            timePickUp: "",
                            dateDropOff: "",
                            timeDropOff: ""
                        }],
                        otherLegs: [],
                        otherVehicles: [],
                        isLocked: false,
                        isEdited: true
                    });
                }
                component.set("v.groundRecords",groundRecords);
                break;
            case "air":
                var flightRecords = component.get("v.flightRecords");
                index = flightRecords.length;
                flightRecords.push({
                    itineraryId: "",
                    cityTitle: "",
                    startDate: "",
                    startDateTitle: "",
                    endDate: "",
                    endDateTitle: "",
                    airDetailsId: "",
                    additionalNotes: "",
                    tripType: "One Way",
                    classService: component.get("v.classServicesAir")[0],
                    pax: 0,
                    preferredAirline: component.get("v.preferredAirlinesAir")[0],
                    segments: [{
                        segmentId: "",
                        departureCity: "",
                        departureDate: component.get("v.today"),
                        departureTimeStart: "",
                        departureTimeEnd: "",
                        arrivalCity: "",
                        arrivalDate: ""
                    }],
                    isLocked: false,
                    isEdited: true
                });
                component.set("v.flightRecords",flightRecords);
                break;
            case "freight":
                var freightRecords = component.get("v.freightRecords");
                index = freightRecords.length;
                freightRecords.push({
                    itineraryId: "",
                    cityTitle: "",
                    startDate: "",
                    startDateTitle: "",
                    endDate: "",
                    endDateTitle: "",
                    tripDetailsId: "",
                    subTripDetailsId: "",
                    additionalNotes: "",
                    groupType: component.get("v.groupTypesFreight")[0],
                    notes: "",
                    legs: [{
                        subTripDetailsId: "",
                        legId: "",
                        locationDetailsPickUp: "",
                        locationDetailsDropOff: "",
                        datePickUp: component.get("v.today"),
                        timePickUp: "",
                        dateDropOff: "",
                        timeDropOff: ""
                    }],
                    otherLegs: [],
                    manifestId: "",
                    manifestName: "",
                    isLocked: false,
                    isEdited: true
                });
                component.set("v.freightRecords",freightRecords);
                break;
            default:
                break;
        }
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened",index);
    },
    
    handleShowRecord : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        var recordOpened = component.get("v.recordOpened");
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        if(recordOpened !== index) component.set("v.recordOpened",index);
        else component.set("v.recordOpened","-1");
    },
    
    handleInputChange : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var input = event.getSource();
        if(!input.checkValidity) input.reportValidity();
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        records[index].isEdited = true;
        var fieldName = input.get("v.fieldName");
        var name = input.get("v.name");
        /*
        if(fieldName != undefined && menuSelected == "air") {
            var tripType = records[index].tripType;
            if(tripType == "Round Trip") {
                switch (fieldName) {
                    case "Departure_City__c":
                        console.log("Departure_City__c");
                        records[index].segments[1].arrivalCityId = input.get("v.value")[0];
                        break;
                    case "Arrival_City__c":
                        console.log("Arrival_City__c");
                        records[index].segments[1].departureCityId = input.get("v.value")[0];
                        break;
                    default:
                        break;
                }
            }
        }
        */
        if(name != undefined && menuSelected == "air") {
            var tripType = records[index].tripType;
            if(tripType != "One Way" && name == "Departure_Date__c") {
                var segmentIndex = parseInt(input.get("v.label"));
                if(segmentIndex < records[index].segments.length-1) records[index].segments[segmentIndex+1].arrivalDate = records[index].segments[segmentIndex].departureDate;
            }
        }
        if(menuSelected == "housing") component.set("v.lodgingRecords",records);
        if(menuSelected == "ground") component.set("v.groundRecords",records);
        if(menuSelected == "air") component.set("v.flightRecords",records);
        if(menuSelected == "freight") component.set("v.freightRecords",records);
    },
    
    onLodgingVenueCity : function(component, event, helper) {
        var index = component.get("v.recordOpened");
        var records = component.get("v.lodgingRecords");
        var record = records[index];
        record.otherVenue = "";
        component.set("v.lodgingRecords",records);
        component.set("v.loadVenueCityLookup",true);
    },
    
    onLodgingVenue : function(component, event, helper) {
        var index = component.get("v.recordOpened");
        var records = component.get("v.lodgingRecords");
        var record = records[index];
        record.otherVenue = "";
        component.set("v.lodgingRecords",records);
        component.set("v.loadVenueLookup",true);
    },
    
    onLodgingCity : function(component, event, helper) {
        var index = component.get("v.recordOpened");
        var records = component.get("v.lodgingRecords");
        var record = records[index];
        record.otherVenue = "";
        component.set("v.lodgingRecords",records);
        component.set("v.loadCityLookup",true);
    },
    
    onAirportRound : function(component, event, helper) {
        console.log("onAirportRound");
        var index = component.get("v.recordOpened");
        var records = component.get("v.flightRecords");
        var tripType = records[index].tripType;
        if(tripType == "Round Trip") {
            records[index].segments[1].departureCityId = records[index].segments[0].arrivalCityId;
            records[index].segments[1].arrivalCityId = records[index].segments[0].departureCityId;
            component.set("v.triggerLookupValidation",!component.get("v.triggerLookupValidation"));
        }
        component.set("v.flightRecords",records);
        //console.log(JSON.parse(JSON.stringify( records[index] )));
    },
    
    handleShowRecordDetails : function(component, event, helper) {
        component.set("v.showRecordDetails",!component.get("v.showRecordDetails"));
        component.set("v.showOtherDetails",false);
    },
    
    handleShowOtherDetails : function(component, event, helper) {
        component.set("v.showOtherDetails",!component.get("v.showOtherDetails"));
        component.set("v.showRecordDetails",false);
    },
    
    handleAddRoomType : function(component, event, helper) {
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var roomTypeRecords = [];
        if(lodging.hasOwnProperty("roomTypeRecords")) roomTypeRecords = lodging.roomTypeRecords;
        roomTypeRecords.push({
            Id: "",
            Unit_Type__c: component.get("v.roomTypes")[0],
            Units__c: ""
        });
        lodging.roomTypeRecords = roomTypeRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleRemoveRoomType : function(component, event, helper) {
        var indexRoom = parseInt(event.getSource().get("v.value"));
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var roomTypeRecords = lodging.roomTypeRecords;
        roomTypeRecords.splice(indexRoom,1);
        lodging.roomTypeRecords = roomTypeRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleAddConcession : function(component, event, helper) {
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var concessionRecords = [];
        if(lodging.hasOwnProperty("concessionRecords")) concessionRecords = lodging.concessionRecords;
        if(lodging.lodgingType != "housingCorp") {
            concessionRecords.push({
                Id: "",
                Concessions_Requested__c: component.get("v.concessionHousingTypes")[0],
                Notes__c: ""
            });
        } else {
            concessionRecords.push({
                Id: "",
                Concessions_Requested__c: component.get("v.concessionCorporateTypes")[0],
                Notes__c: ""
            });
        }
        lodging.concessionRecords = concessionRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleRemoveConcession : function(component, event, helper) {
        var indexConcession = parseInt(event.getSource().get("v.value"));
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var concessionRecords = lodging.concessionRecords;
        concessionRecords.splice(indexConcession,1);
        lodging.concessionRecords = concessionRecords;
        lodging.isEdited = true;
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleAddGroundLeg : function(component, event, helper) {
        var groundIndex = component.get("v.recordOpened");
        var groundRecords = component.get("v.groundRecords");
        var ground = groundRecords[groundIndex];
        var legs = [];
        if(ground.hasOwnProperty("legs")) legs = ground.legs;
        legs.push({
            subTripDetailsId: "",
            subTripType: component.get("v.tripTypesGround")[0],
            legId: "",
            locationPickUp: component.get("v.locationPickUpTypes")[0],
            locationDropOff: component.get("v.locationDropOffTypes")[0],
            locationDetailsPickUp: "",
            locationDetailsDropOff: "",
            datePickUp: component.get("v.today"),
            timePickUp: "",
            dateDropOff: "",
            timeDropOff: ""
        });
        ground.legs = legs;
        ground.isEdited = true;
        groundRecords[groundIndex] = ground;
        component.set("v.groundRecords",groundRecords);
    },
    
    handleRemoveGroundLeg : function(component, event, helper) {
        var indexLeg = parseInt(event.getSource().get("v.value"));
        var groundIndex = component.get("v.recordOpened");
        var groundRecords = component.get("v.groundRecords");
        var ground = groundRecords[groundIndex];
        var legs = ground.legs;
        legs.splice(indexLeg,1);
        ground.legs = legs;
        ground.isEdited = true;
        groundRecords[groundIndex] = ground;
        component.set("v.groundRecords",groundRecords);
    },
    
    handleAddSegment : function(component, event, helper) {
        var flightIndex = component.get("v.recordOpened");
        var flightRecords = component.get("v.flightRecords");
        var flight = flightRecords[flightIndex];
        var segments = [];
        if(flight.hasOwnProperty("segments")) segments = flight.segments;
        var departureDate = component.get("v.today");
        var arrivalDate = component.get("v.today");
        if(!!segments[segments.length-1].departureDate) {
            departureDate = segments[segments.length-1].departureDate;
            arrivalDate = segments[segments.length-1].departureDate;
        }
        segments.push({
            segmentId: "",
            departureCity: "",
            departureDate: departureDate,
            departureTimeStart: "",
            departureTimeEnd: "",
            arrivalCity: "",
            arrivalDate: arrivalDate
        });
        flight.segments = segments;
        flight.isEdited = true;
        flightRecords[flightIndex] = flight;
        component.set("v.flightRecords",flightRecords);
    },
    
    handleRemoveSegment : function(component, event, helper) {
        var indexSegment = parseInt(event.getSource().get("v.value"));
        var flightIndex = component.get("v.recordOpened");
        var flightRecords = component.get("v.flightRecords");
        var flight = flightRecords[flightIndex];
        var segments = flight.segments;
        segments.splice(indexSegment,1);
        if(indexSegment != segments.length) segments[indexSegment].arrivalDate = !!segments[indexSegment-1].departureDate? segments[indexSegment-1].departureDate : component.get("v.today");
        flight.segments = segments;
        flight.isEdited = true;
        flightRecords[flightRecords] = flight;
        component.set("v.flightRecords",flightRecords);
    },
    
    handleAddFreightLeg : function(component, event, helper) {
        var freightIndex = component.get("v.recordOpened");
        var freightRecords = component.get("v.freightRecords");
        var freight = freightRecords[freightIndex];
        var legs = [];
        if(freight.hasOwnProperty("legs")) legs = freight.legs;
        legs.push({
            subTripDetailsId: "",
            legId: "",
            tripType: "",
            locationDetailsPickUp: "",
            locationDetailsDropOff: "",
            datePickUp: component.get("v.today"),
            timePickUp: "",
            dateDropOff: "",
            timeDropOff: ""
        });
        freight.legs = legs;
        freight.isEdited = true;
        freightRecords[freightIndex] = freight;
        component.set("v.freightRecords",freightRecords);
    },
    
    handleRemoveFreightLeg : function(component, event, helper) {
        var indexLeg = parseInt(event.getSource().get("v.value"));
        var freightIndex = component.get("v.recordOpened");
        var freightRecords = component.get("v.freightRecords");
        var freight = freightRecords[freightIndex];
        var legs = freight.legs;
        legs.splice(indexLeg,1);
        freight.legs = legs;
        freight.isEdited = true;
        freightRecords[freightIndex] = freight;
        component.set("v.freightRecords",freightRecords);
    },
    
    handleChangeLodgingStay : function(component, event, helper) {
        var lodgingType = event.getParam("value");
        var lodgingIndex = component.get("v.recordOpened");
        var lodgingRecords = component.get("v.lodgingRecords");
        var lodging = lodgingRecords[lodgingIndex];
        var salesHousingConcessions = component.get("v.salesHousingConcessions");
        var concessionsToCompare = lodgingType != "housingCorp"? component.get("v.concessionHousingTypes") : component.get("v.concessionCorporateTypes");
        var concessionsToAdd = [];
        /**Fix By Clay Dev 4 Feb, 2021 #176599208
        salesHousingConcessions.forEach(concession => { if(concessionsToCompare.indexOf(concession.Concessions_Requested__c) > 0) concessionsToAdd.push(concession); });
        lodging.concessionRecords.push.apply(lodging.concessionRecords,concessionsToAdd);
        **/
        salesHousingConcessions.forEach(concession => { 
            if(concessionsToCompare.indexOf(concession.Concessions_Requested__c)  < 0) { 
            	concessionsToCompare.push(concession.Concessions_Requested__c);                                
            }
        });
        if(lodgingType != "housingCorp") {
            component.set("v.concessionHousingTypes", concessionsToCompare);
        } else {
            component.set("v.concessionCorporateTypes", concessionsToCompare);
        }
        lodging.concessionRecords.push.apply(lodging.concessionRecords,salesHousingConcessions);
        lodgingRecords[lodgingIndex] = lodging;
        component.set("v.lodgingRecords",lodgingRecords);
    },
    
    handleChangeAirTrip : function(component, event, helper) {
        var tripType = event.getParam("value");
        var flightIndex = component.get("v.recordOpened");
        var flightRecords = component.get("v.flightRecords");
        var flight = flightRecords[flightIndex];
        var segments = [];
        switch (tripType) {
            case "One Way":
                segments.push({
                    segmentId: "",
                    departureCityId: "",
                    departureCityName: "",
                    departureDate: component.get("v.today"),
                    departureTimeStart: "",
                    departureTimeEnd: "",
                    arrivalCityId: "",
                    arrivalCityName: "",
                    arrivalDate: ""
                });
                break;
            case "Round Trip":
            case "Multi-City":
                segments.push({
                    segmentId: "",
                    departureCityId: "",
                    departureCityName: "",
                    departureDate: component.get("v.today"),
                    departureTimeStart: "",
                    departureTimeEnd: "",
                    arrivalCityId: "",
                    arrivalCityName: "",
                    arrivalDate: ""
                });
                segments.push({
                    segmentId: "",
                    departureCityId: "",
                    departureCityName: "",
                    departureDate: "",
                    departureTimeStart: "",
                    departureTimeEnd: "",
                    arrivalCityId: "",
                    arrivalCityName: "",
                    arrivalDate: component.get("v.today")
                });
                break;
            default:
                break;
        }
        flight.segments = segments;
        flight.isEdited = true;
        flightRecords[flightIndex] = flight;
        component.set("v.flightRecords",flightRecords);
    },
    
    handleAttachManifestMessage: function(component, event, helper) {
        var freightIndex = component.get("v.recordOpened");
        var freightRecords = component.get("v.freightRecords");
        var freight = freightRecords[freightIndex];
        if(freight.isEdited) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please save this record first before uploading a file."
            });
            toastEvent.fire();
        } else {
            var menuSelected = component.get("v.menuSelected");
            var index = component.get("v.recordOpened");
            var records = [];
            if(menuSelected == "housing") records = component.get("v.lodgingRecords");
            if(menuSelected == "ground") records = component.get("v.groundRecords");
            if(menuSelected == "air") records = component.get("v.flightRecords");
            if(menuSelected == "freight") records = component.get("v.freightRecords");
            var record = records[index];
            component.set("v.openAttachment",true);
            component.set("v.fileName",record.manifestName);
            component.set("v.fileId",record.manifestId);
        }
    },
    
    handleUploadFinished : function(component, event, helper) {
        var uploadedFiles = event.getParam("files");
        component.set("v.fileId",uploadedFiles[0].documentId);
        component.set("v.fileName",uploadedFiles[0].name);
    },
    
    handleConfirmFile : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        var record = records[index];
        record.manifestId = component.get("v.fileId");
        record.manifestName = component.get("v.fileName");
        record.isEdited = true;
        records[index] = record;
        if(menuSelected == "housing") component.set("v.lodgingRecords",records);
        if(menuSelected == "ground") component.set("v.groundRecords",records);
        if(menuSelected == "air") component.set("v.flightRecords",records);
        if(menuSelected == "freight") component.set("v.freightRecords",records);
        console.log(record);
        component.set("v.openAttachment",false);
        component.set("v.fileName","");
        component.set("v.fileId","");
    },
    
    handleCommunicationEvent : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var tabSelected = component.get("v.tabSelected");
        var action = event.getParam("action");
        var data = JSON.parse(JSON.stringify(event.getParam("data")));
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") records = component.get("v.lodgingRecords");
            if(tabSelected == "Ground Travel") records = component.get("v.groundRecords");
            if(tabSelected == "Air") records = component.get("v.flightRecords");
            if(tabSelected == "Freight") records = component.get("v.freightRecords");
        }
        var recordType = "record";
        if(menuSelected == "housing") recordType = "Stay";
        if(menuSelected == "ground") recordType = "Trip";
        if(menuSelected == "air") recordType = "Flight";
        if(menuSelected == "freight") recordType = "Trip";
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") recordType = "Stay";
            if(tabSelected == "Ground Travel") recordType = "Trip";
            if(tabSelected == "Air") recordType = "Flight";
            if(tabSelected == "Freight") recordType = "Trip";
        }
        console.log(data);
        switch (action) {
            case "insert":
                data.record.isEdited = false;
                records[index] = data.record;
                if(menuSelected == "housing") component.set("v.isLodgingLocked",true);
                if(menuSelected == "ground") component.set("v.isGroundLocked",true);
                if(menuSelected == "air") component.set("v.isAirLocked",true);
                if(menuSelected == "freight") component.set("v.isFreightLocked",true);
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "success",
                    title: "",
                    message: recordType + " saved."
                });
                toastEvent.fire();
                break;
            case "update":
                data.record.isEdited = false;
                records[index] = data.record;
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "success",
                    title: "",
                    message: recordType + " updated."
                });
                toastEvent.fire();
                break;
            case "delete":
                records.splice(index,1);
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "success",
                    title: "",
                    message: recordType + " deleted."
                });
                toastEvent.fire();
                component.set("v.showRecordDetails",false);
                component.set("v.showOtherDetails",false);
                component.set("v.recordOpened","-1");
                break;
            default:
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "error",
                    title: "",
                    message: action
                });
                toastEvent.fire();
                return;
                break;
        }
        if(data.hasOwnProperty("salesForHousing")) component.set("v.salesForHousing",data.salesForHousing);
        if(data.hasOwnProperty("salesHousingRoomTypes")) component.set("v.salesHousingRoomTypes",data.salesHousingRoomTypes);
        if(data.hasOwnProperty("salesHousingConcessions")) component.set("v.salesHousingConcessions",data.salesHousingConcessions);
        if(data.hasOwnProperty("salesForGround")) component.set("v.salesForGround",data.salesForGround);
        if(menuSelected == "housing") component.set("v.lodgingRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "ground") component.set("v.groundRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "air") component.set("v.flightRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "freight") component.set("v.freightRecords",JSON.parse(JSON.stringify(records)));
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") component.set("v.lodgingRecords",JSON.parse(JSON.stringify(records)));
            if(tabSelected == "Ground Travel") component.set("v.groundRecords",JSON.parse(JSON.stringify(records)));
            if(tabSelected == "Air") component.set("v.flightRecords",JSON.parse(JSON.stringify(records)));
            if(tabSelected == "Freight") component.set("v.freightRecords",JSON.parse(JSON.stringify(records)));
        }
    },
    
    handleSaveRecord : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var index = component.get("v.recordOpened");
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        var record = records[index];
        if(!record.isEdited) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "Nothing to update."
            });
            toastEvent.fire();
        } else {
            var lodgingTypeEmpty = false;
            var allValid = false;
            if(menuSelected == "housing" && !record.lodgingType) lodgingTypeEmpty = true;
            else allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
                inputCmp.reportValidity();
                return validSoFar && inputCmp.checkValidity();
            }, true);
            //console.log("triggerLookupValidation: "+component.get("v.triggerLookupValidation"));
            component.set("v.triggerLookupValidation",!component.get("v.triggerLookupValidation"));
            if(menuSelected == "housing" && !record.cityId) allValid = false;
            if(menuSelected == "air") for(var i = 0; i < record.segments.length; i++) if(!record.segments[i].departureCityId || !record.segments[i].arrivalCityId) allValid = false;
            if (allValid) {
                if(menuSelected == "housing") {
                    if(record.preferredBrandsList.length > 0) record.preferredBrands = record.preferredBrandsList.join(";");
                    else record.preferredBrands = "";
                }
                if(menuSelected == "ground") {
                    if(record.amenitiesList.length > 0) record.amenities = record.amenitiesList.join(";");
                    else record.amenities = "";
                }
                console.log("ready to send");
                var callToParent = component.getEvent("callToParent");
                callToParent.setParam("action","saveItineraryRecord");
                callToParent.setParam("data",{
                    recordType: menuSelected,
                    record: record
                });
                callToParent.fire();
            } else {
                component.set("v.showRecordDetails",true);
                var toastEvent = $A.get("e.force:showToast");
                var message = "Please update the invalid form entries and try again.";
                if(lodgingTypeEmpty) message = "You need to select a lodging type first.";
                toastEvent.setParams({
                    type: "error",
                    title: "",
                    message: message
                });
                toastEvent.fire();
            }
        }
    },
    
    handleDeleteRecord : function(component, event, helper) {
        var menuSelected = component.get("v.menuSelected");
        var tabSelected = component.get("v.tabSelected");
        var index = component.get("v.recordOpened");
        var record = {};
        var records = [];
        var isDeleteDenied = false;
        if(menuSelected == "housing") {
            records = component.get("v.lodgingRecords");
            record = records[index];
            if(record.otherRoomTypeRecords.length > 0 || record.otherConcessionRecords.length > 0) isDeleteDenied = true;
        }
        if(menuSelected == "ground") {
            records = component.get("v.groundRecords");
            record = records[index];
            if(record.otherLegs.length > 0 || record.otherVehicles.length > 0) isDeleteDenied = true;
        }
        if(menuSelected == "air") {
            records = component.get("v.flightRecords");
            record = records[index];
        }
        if(menuSelected == "freight") {
            records = component.get("v.freightRecords");
            record = records[index];
            if(record.otherLegs.length > 0) isDeleteDenied = true;
        }
        if(menuSelected == "review") {
            if(tabSelected == "Lodging") {
                records = component.get("v.lodgingRecords");
                record = records[index];
                if(record.otherRoomTypeRecords.length > 0 || record.otherConcessionRecords.length > 0) isDeleteDenied = true;
            }
            if(tabSelected == "Ground Travel") {
                records = component.get("v.groundRecords");
                record = records[index];
                if(record.otherLegs.length > 0 || record.otherVehicles.length > 0) isDeleteDenied = true;
            }
            if(tabSelected == "Air") {
                records = component.get("v.flightRecords");
                record = records[index];
            }
            if(tabSelected == "Freight") {
                records = component.get("v.freightRecords");
                record = records[index];
                if(record.otherLegs.length > 0) isDeleteDenied = true;
            }
        }
        if(isDeleteDenied) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "You cannot delete a itinerary with records managed by Road Rebel. Please contact Road Rebel team for support."
            });
            toastEvent.fire();
            return;
        }
        if(records.length == 1) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "You need at least one record on this service."
            });
            toastEvent.fire();
        } else if(record.itineraryId == "") {
            records.splice(index,1);
            var recordType = "record";
            if(menuSelected == "housing") recordType = "Stay";
            if(menuSelected == "ground") recordType = "Trip";
            if(menuSelected == "air") recordType = "Flight";
            if(menuSelected == "freight") recordType = "Trip";
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "success",
                title: "",
                message: recordType + " deleted."
            });
            toastEvent.fire();
            component.set("v.showRecordDetails",false);
            component.set("v.showOtherDetails",false);
            component.set("v.recordOpened","-1");
            if(menuSelected == "housing") records = component.set("v.lodgingRecords",records);
            if(menuSelected == "ground") records = component.set("v.groundRecords",records);
            if(menuSelected == "air") records = component.set("v.flightRecords",records);
            if(menuSelected == "freight") records = component.set("v.freightRecords",records);
        } else {
            var recordType = "";
            if(menuSelected == "review") {
                if(tabSelected == "Lodging") recordType = "housing";
                if(tabSelected == "Ground Travel") recordType = "ground";
                if(tabSelected == "Air") recordType = "air";
                if(tabSelected == "Freight") recordType = "freight";
            } else recordType = menuSelected;
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","removeItineraryRecord");
            callToParent.setParam("data",{
                recordType: recordType,
                recordId: record.itineraryId
            });
            callToParent.fire();
        }
    },
    
    handleEditRecord : function(component, event, helper) {
        var tabSelected = component.get("v.tabSelected");
        if(tabSelected == "Lodging") component.set("v.menuSelected","housing");
        if(tabSelected == "Ground Travel") component.set("v.menuSelected","ground");
        if(tabSelected == "Air") component.set("v.menuSelected","air");
        if(tabSelected == "Freight") component.set("v.menuSelected","freight");
    },
    
    handleBack : function(component, event, helper) {
        var menuOptions = component.get("v.menuOptions");
        var menuSelected = component.get("v.menuSelected");
        var openBackConfirmation = component.get("v.openBackConfirmation");
        component.set("v.openBackConfirmation",false);
        var recordsPending = false;
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        records.forEach(record => { if(record.isEdited) recordsPending = true; });
        if(recordsPending && !openBackConfirmation) component.set("v.openBackConfirmation",true);
        else {
            for(var i = 0; i<menuOptions.length; i++) if(menuOptions[i].value == menuSelected) {
                menuSelected = menuOptions[i-1].value;
                i = menuOptions.length;
            }
            component.set("v.showRecordDetails",false);
            component.set("v.showOtherDetails",false);
            component.set("v.recordOpened","-1");
            component.set("v.menuSelected",menuSelected);
            var itineraryData = component.get("v.itineraryData");
            switch (menuSelected) {
                case "services":
                    component.set("v.lodgingRecords",[]);
                    component.set("v.groundRecords",[]);
                    component.set("v.flightRecords",[]);
                    component.set("v.freightRecords",[]);
                    delete itineraryData.lodgingRecords;
                    delete itineraryData.groundRecords;
                    delete itineraryData.flightRecords;
                    delete itineraryData.freightRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "housing":
                    component.set("v.lodgingRecords",[]);
                    delete itineraryData.lodgingRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "ground":
                    component.set("v.groundRecords",[]);
                    delete itineraryData.groundRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "air":
                    component.set("v.flightRecords",[]);
                    delete itineraryData.flightRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                case "freight":
                    component.set("v.freightRecords",[]);
                    delete itineraryData.freightRecords;
                    component.set("v.itineraryData",itineraryData);
                    break;
                default:
                    break;
            }
        }
    },
    
    handleNext : function(component, event, helper) {
        var menuOptions = component.get("v.menuOptions");
        var menuSelected = component.get("v.menuSelected");
        var openNextConfirmation = component.get("v.openNextConfirmation");
        component.set("v.openNextConfirmation",false);
        var recordsPending = false;
        var records = [];
        if(menuSelected == "housing") records = component.get("v.lodgingRecords");
        if(menuSelected == "ground") records = component.get("v.groundRecords");
        if(menuSelected == "air") records = component.get("v.flightRecords");
        if(menuSelected == "freight") records = component.get("v.freightRecords");
        records.forEach(record => { if(record.isEdited) recordsPending = true; });
        if(recordsPending && !openNextConfirmation) {
            if(records.length == 1) {
                var toastEvent = $A.get("e.force:showToast");
                toastEvent.setParams({
                    type: "warning",
                    title: "",
                    message: "You need to save at least one record before continuing."
                });
                toastEvent.fire();
            } else component.set("v.openNextConfirmation",true);
        } else {
            var itineraryData = component.get("v.itineraryData");
            var recordsSaved = [];
            if(menuSelected == "housing") recordsSaved = itineraryData.lodgingRecords;
            if(menuSelected == "ground") recordsSaved = itineraryData.groundRecords;
            if(menuSelected == "air") recordsSaved = itineraryData.flightRecords;
            if(menuSelected == "freight") recordsSaved = itineraryData.freightRecords;
            for(var i = records.length-1; i>=0; --i) {
                if(records[i].isEdited && !!records[i].itineraryId) recordsSaved.forEach(record => { if(record.itineraryId == records[i].itineraryId) records[i] = record; });
                else if (records[i].isEdited) records.splice(i,1);
            }
            if(menuSelected == "housing") records = component.set("v.lodgingRecords",records);
            if(menuSelected == "ground") records = component.set("v.groundRecords",records);
            if(menuSelected == "air") records = component.set("v.flightRecords",records);
            if(menuSelected == "freight") records = component.set("v.freightRecords",records);
            for(var i = 0; i<menuOptions.length; i++) if(menuOptions[i].value == menuSelected) {
                menuSelected = menuOptions[i+1].value;
                i = menuOptions.length
            }
            component.set("v.showRecordDetails",false);
            component.set("v.showOtherDetails",false);
            component.set("v.recordOpened","-1");
            component.set("v.menuSelected",menuSelected);
            switch (menuSelected) {
                case "ground":
                    var callToParent = component.getEvent("callToParent");
                    callToParent.setParam("action","loadGroundPage");
                    callToParent.fire();
                    break;
                case "air":
                    var callToParent = component.getEvent("callToParent");
                    callToParent.setParam("action","loadAirPage");
                    callToParent.fire();
                    break;
                case "freight":
                    var callToParent = component.getEvent("callToParent");
                    callToParent.setParam("action","loadFreightPage");
                    callToParent.fire();
                    break;
                case "review":
                    var tabSelected = "";
                    if(component.get("v.isFreightSelected")) tabSelected = "Freight";
                    if(component.get("v.isAirSelected")) tabSelected = "Air";
                    if(component.get("v.isGroundSelected")) tabSelected = "Ground Travel";
                    if(component.get("v.isLodgingSelected")) tabSelected = "Lodging";
                    component.set("v.tabSelected",tabSelected);
                    break;
                default:
                    break;
            }
        }
    },
    
    handleCloseModal : function(component, event, helper) {
        component.set("v.openAttachment",false);
        component.set("v.openBackConfirmation",false);
        component.set("v.openNextConfirmation",false);
        component.set("v.fileName","");
        component.set("v.fileId","");
    },
    
    showLodgingRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Lodging");
    },
    
    showGroundRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Ground Travel");
    },
    
    showAirRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Air");
    },
    
    showFreightRecords : function(component, event, helper) {
        component.set("v.showRecordDetails",false);
        component.set("v.showOtherDetails",false);
        component.set("v.recordOpened","-1");
        component.set("v.tabSelected","Freight");
    },
    
    handleSubmit : function(component, event, helper) {
        var recordsPending = false;
        var records = [];
        if(component.get("v.isLodgingSelected")) {
            records = component.get("v.lodgingRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(component.get("v.isGroundSelected")) {
            records = component.get("v.groundRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(component.get("v.isAirSelected")) {
            records = component.get("v.flightRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(component.get("v.isFreightSelected")) {
            records = component.get("v.freightRecords");
            records.forEach(record => { if(!record.isLocked) recordsPending = true; });
        }
        if(recordsPending) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","submitItineraries");
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "warning",
                title: "",
                message: "Nothing to submit."
            });
            toastEvent.fire();
        }
    }
})
```
### VoyajerItinerary

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerItinerary

```
.THIS .mainMenuTitle {
    font-size: 1rem;
    padding: 0.5em;
    border-bottom: 1px solid #9f9f9f;
    margin-bottom: 0.5em;
}

.THIS .page-header_services {
    font-size: 1.5rem;
    text-align: center;
    margin-top: 0.25em;
}

.THIS .page-header_services:first-child {
    font-size: 1rem;
    margin-top: 1.5em;
}

.THIS .serviceBox {
    width: 8em;
    margin-bottom: 1em;
    position: relative;
    display: flex;
    flex-direction: column;
}

.THIS .serviceBox > div {
    text-align: center;
}

.THIS .serviceBoxImage {
    width: 100%;
    height: auto;
}

.THIS .serviceBox img {
    background-color: #f7f9fe;
    border-radius: 50%;
}

.THIS .serviceBoxName {
    margin-top: 1em;
    text-transform: uppercase;
    font-weight: 500;
    color: #00b4ff;
}

.THIS .multiSelectPicklist {
    width: 100%;
    border-radius: 0.25rem;
    text-transform: none;
    justify-content: space-between;
    padding-right: 0.5em !important;
}

.THIS .multiSelectPicklist .slds-icon {
    right: 0.25em;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .preferences {
    display: flex;
    flex-direction: column;
    margin-top: 0.75em;
    border-top: 1px solid #dbdbdb;
}

.THIS .additionalFields {
    margin-top: 0.75em;
    border-top: 1px solid #dbdbdb;
}

.THIS .preferences > div {
    display: flex;
    flex: 1;
    margin-bottom: 0.5em;
}

.THIS .preferencesHeader > div,
.THIS .preferencesRow > div {
    flex: 1;
    padding: .25rem;
}

.THIS .preferencesHeader > div {
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
    font-weight: 500;
    color: rgb(105, 105, 105);
}

.THIS .travels {
    display: flex;
    flex-direction: column;
    margin-top: 0.75em;
}

.THIS .travelRow {
    display: flex;
    flex: 1;
}

.THIS .travelRow > div:first-child {
    flex: 1;
}

.THIS .formInputTextarea textarea {
    margin-top: 0px;
    margin-bottom: 0px;
    height: 2rem;
    padding: 0.25rem 0.75rem;
}

.THIS .travelFields {
    display: flex;
    flex: 1;
    flex-direction: column;
}

.THIS .travelFields > div {
    display: flex;
}

.THIS .fieldSelect label {
    display: none;
}

.THIS .field {
    align-items: center;
    display: flex;
}

.THIS .fieldInput {
    flex: 1;
    padding-right: 0.25em;
}

.THIS .labelTooltip {
    padding-left: 0.25rem;
}

.THIS .labelTooltip .slds-form-element__icon {
    padding-top: 0;
}

.THIS .noRadius .slds-button {
    border-radius: 0;
}

.THIS .noRadius .slds-radio_faux {
    display: block;
}

.THIS .actions {
    display: flex;
    justify-content: flex-end;
    padding-top: 1em;
}

.THIS .reviewNavigator {
    background-color: white;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .slds-dueling-list__column:last-child {
    display: none;
}

@media (max-width: 800px) {
    .THIS .page-header_services:first-child {
        margin-top: 0;
    }
}

@media (max-width: 550px) {
    .THIS .mainMenuTitle {
        height: 8.25em;
        position: relative;
    }
    
    .THIS .mainMenuTitle h3 {
        transform: rotate(270deg);
        position: absolute;
        right: -100%;
        width: 8em;
        top: 40%;
        margin: auto;
        text-align: center;
    }
}
```
### VoyajerItinerary

```
<aura:component>
    <aura:attribute type="String" name="userId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="menuSelected" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="tabSelected" />
    <aura:attribute type="String" name="fileName" />
    <aura:attribute type="String" name="fileId" />
    <aura:attribute type="Object" name="itineraryData" />
    <aura:attribute type="Object" name="salesForHousing" />
    <aura:attribute type="Object" name="salesForGround" />
    <aura:attribute type="Object" name="salesForAir" />
    <aura:attribute type="Object" name="salesForFreight" />
    <aura:attribute type="Object" name="recordTypes" />
    <aura:attribute type="List" name="menuOptions" />
    <aura:attribute type="List" name="lodgingTypes" default="[{'label': 'Group Hotel', 'value': 'housingHotel'},{'label': 'Apartment/Private Home', 'value': 'housingCorp'},{'label': 'Less than 10 rooms', 'value': 'housingIR'}]" />
    <aura:attribute type="List" name="distanceFromEventOptions" />
    <aura:attribute type="List" name="hotelStars" />
    <aura:attribute type="List" name="hotelTypes" />
    <aura:attribute type="List" name="preferredBrands" />
    <aura:attribute type="List" name="roomTypes" />
    <aura:attribute type="List" name="concessionHousingTypes" />
    <aura:attribute type="List" name="concessionCorporateTypes" />
    <aura:attribute type="List" name="salesHousingRoomTypes" />
    <aura:attribute type="List" name="salesHousingConcessions" />
    <aura:attribute type="List" name="tripTypesGround" />
    <aura:attribute type="List" name="locationPickUpTypes" />
    <aura:attribute type="List" name="locationDropOffTypes" />
    <aura:attribute type="List" name="vehicleTypesGround" />
    <aura:attribute type="List" name="groupTypesGround" />
    <aura:attribute type="List" name="amenitiesGround" />
    <aura:attribute type="List" name="classServicesAir" />
    <aura:attribute type="List" name="preferredAirlinesAir" />
    <aura:attribute type="List" name="groupTypesFreight" />
    <aura:attribute type="List" name="tripTypes" default="[{'label': 'One Way', 'value': 'One Way'},{'label': 'Round Trip', 'value': 'Round Trip'},{'label': 'Multi-City', 'value': 'Multi-City'}]" />
    <aura:attribute type="List" name="lodgingRecords" />
    <aura:attribute type="List" name="groundRecords" />
    <aura:attribute type="List" name="flightRecords" />
    <aura:attribute type="List" name="freightRecords" />
    <aura:attribute type="Boolean" name="isLodgingSelected" default="false" />
    <aura:attribute type="Boolean" name="isLodgingLocked" default="false" />
    <aura:attribute type="Boolean" name="isGroundSelected" default="false" />
    <aura:attribute type="Boolean" name="isGroundLocked" default="false" />
    <aura:attribute type="Boolean" name="isAirSelected" default="false" />
    <aura:attribute type="Boolean" name="isAirLocked" default="false" />
    <aura:attribute type="Boolean" name="isFreightSelected" default="false" />
    <aura:attribute type="Boolean" name="isFreightLocked" default="false" />
    <aura:attribute type="Boolean" name="showRecordDetails" default="false" />
    <aura:attribute type="Boolean" name="showOtherDetails" default="false" />
    <aura:attribute type="Boolean" name="triggerLookupValidation" default="false" />
    <aura:attribute type="Boolean" name="loadVenueCityLookup" default="false" />
    <aura:attribute type="Boolean" name="loadVenueLookup" default="false" />
    <aura:attribute type="Boolean" name="loadCityLookup" default="false" />
    <aura:attribute type="Boolean" name="openAttachment" default="false" />
    <aura:attribute type="Boolean" name="openBackConfirmation" default="false" />
    <aura:attribute type="Boolean" name="openNextConfirmation" default="false" />
    <aura:attribute type="Integer" name="recordOpened" default="-1" />
    <aura:attribute type="Date" name="today" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.itineraryData}" action="{!c.loadItineraryData}" />
    <aura:handler action="{!c.handleCommunicationEvent}" event="c:VoyajerCallToChild" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="mainMenu">
            <div class="mainMenuTitle"><h3>Enter Itinerary</h3></div>
            <nav class="slds-nav-vertical sideBarItinerary lightningVerticalNavigation">
                <aura:iteration items="{!v.menuOptions}" var="item">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected==item.value? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action">
                            <i class="{!'fas '+item.icon+' sideBarItineraryIcon'}"></i><span class="hideOnMobile">{!item.label}</span>
                            <aura:if isTrue="{!item.checked}">
                                <div class="checkpoint"><i class="fas fa-check-circle checkpointIcon"></i><div class="checkpointBackground"></div></div>
                            </aura:if>
                        </div>
                    </div>
                </aura:iteration>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <aura:if isTrue="{!v.menuSelected=='services'}">
                    <div class="page-section" style="align-items: center;">
                        <div class="page-header page-header_services">Let's begin...</div>
                        <div class="page-header page-header_services">Select the services you will need</div>
                        <div class="page-section-services_center">
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Lodging" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_housing_icons'+(v.isLodgingSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Lodging</p></div>
                            </div>
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Ground Travel" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_busing_icons'+(v.isGroundSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Ground Travel</p></div>
                            </div>
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Air Travel" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_plane_icons'+(v.isAirSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Air Travel</p></div>
                            </div>
                            <div class="serviceBox">
                                <lightning:avatar onclick="{!c.toggleItineraryService}" variant="circle" alternativeText="Freight" size="large" class="serviceBoxImage" 
                                                  src="{!$Resource.CommunityImages+'/SelectServiceIcons/service_freight_icons'+(v.isFreightSelected? '' : '_not')+'_selected.png'}" />
                                <div class="serviceBoxName"><p>Freight</p></div>
                            </div>
                        </div>
                        <div class="page-section"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.saveServices}" /></div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='housing'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-home titleIcon"></i>Lodging</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.lodgingRecords}" var="lodging" indexVar="lodgingIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(lodging.isLocked==true,'background-color: #0065ff; color: white;',if(lodging.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!lodgingIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!empty(lodging.cityTitle)}">
                                                <!-- 177513339 -->
                                                <aura:if isTrue="{!(lodging.stayStatus=='Layoff')}">
                                                    <div class="location" title="Layoff">Layoff</div>
                                                    <aura:set attribute="else">
                                                    	<div class="location" title="{!'Stay '+(lodgingIndex+1)}">{!'Stay '+(lodgingIndex+1)}</div>
                                                    </aura:set>
                                                </aura:if>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!lodging.cityTitle}">{!lodging.cityTitle}</div>
                                                    <div class="dates" style="{!if(empty(lodging.startDateTitle),'display:none;','')}">{!lodging.startDateTitle} - {!lodging.endDateTitle}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==lodgingIndex?'utility:up':'utility:down'}" value="{!lodgingIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==lodgingIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(lodging.isLocked==true,'background-color: #c5dcff;',if(lodging.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!lodging.isLocked!=true}">
                                                <div>
                                                    <lightning:radioGroup aura:id="lodgingForm" name="radioButtonGroup" label="" options="{!v.lodgingTypes}" value="{!lodging.lodgingType}" type="button" class="noRadius" onchange="{!c.handleChangeLodgingStay}" disabled="{!if(empty(lodging.lodgingType),false,true)}" />
                                                </div>
                                                <aura:if isTrue="{!not(empty(lodging.lodgingType))}">
                                                    <br/>
                                                    <div class="formColumnTwoChilds">
                                                        <div class="formField">
                                                            <label for="Start_Date__c">Check-In</label>
                                                            <lightning:input aura:id="recordField" name="Start_Date__c" type="date" label="" value="{!lodging.startDate}" min="{!v.today}" max="{!lodging.endDate}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                        </div>
                                                        <div class="formField">
                                                            <label for="End_Date__c">Check-Out</label>
                                                            <lightning:input aura:id="recordField" name="End_Date__c" type="date" label="" value="{!lodging.endDate}" min="{!lodging.startDate}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                        </div>
                                                    </div>
                                                    <div class="formColumnTwoChilds">
                                                        <div class="formField">
                                                            <c:VoyajerCustomLookup objectAPIName="Account" 
                                                                                   fieldName="Venue_City__c" 
                                                                                   iconName="custom:custom78" 
                                                                                   lookupId="{!lodging.venueCityId}" 
                                                                                   label="Venue City" 
                                                                                   inputPlaceholder="Enter Location" 
                                                                                   isEdited="{!lodging.isEdited}" 
                                                                                   isRequired="false" 
                                                                                   loadVenueCityLookup="{!v.loadVenueCityLookup}" 
                                                                                   venueId="{!lodging.venueId}" 
                                                                                   lodgingVenueAux="{!c.onLodgingVenue}" 
                                                                                   cityId="{!lodging.cityId}" 
                                                                                   lodgingCityAux="{!c.onLodgingCity}" />
                                                        </div>
                                                        <div class="formField">
                                                            <c:VoyajerCustomLookup objectAPIName="Account" 
                                                                                   fieldName="Venue__c" 
                                                                                   iconName="custom:custom85" 
                                                                                   lookupId="{!lodging.venueId}" 
                                                                                   label="Venue" 
                                                                                   inputPlaceholder="Enter Venue" 
                                                                                   isRequired="false" 
                                                                                   isEdited="{!lodging.isEdited}" 
                                                                                   loadVenueLookup="{!v.loadVenueLookup}" 
                                                                                   venueCityId="{!lodging.venueCityId}" 
                                                                                   lodgingVenueCityAux="{!c.onLodgingVenueCity}" 
                                                                                   cityId="{!lodging.cityId}" 
                                                                                   lodgingCityAux="{!c.onLodgingCity}" />
                                                        </div>
                                                    </div>
                                                    <div class="formColumnTwoChilds">
                                                        <div class="formField">
                                                            <c:VoyajerCustomLookup objectAPIName="City__c" 
                                                                                   fieldName="City__c" 
                                                                                   iconName="custom:custom24" 
                                                                                   lookupId="{!lodging.cityId}" 
                                                                                   label="Location" 
                                                                                   inputPlaceholder="Enter Location" 
                                                                                   isRequired="true" 
                                                                                   isEdited="{!lodging.isEdited}" 
                                                                                   loadCityLookup="{!v.loadCityLookup}" 
                                                                                   triggerLookupValidation="{!v.triggerLookupValidation}" />
                                                        </div>
                                                        <div class="formField">
                                                            <label for="Other_Venue__c">
                                                                Other Venue<lightning:helptext class="labelTooltip" content="If you can’t find venue in your city please add your venue name here." />
                                                            </label>
                                                            <lightning:input aura:id="recordField" name="Other_Venue__c" label="" value="{!lodging.otherVenue}" variant="label-hidden" class="fieldInput" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!or(not(empty(lodging.otherRoomTypeRecords)),not(empty(lodging.otherConcessionRecords)))}">
                                                        <div class="recordDetails">
                                                            <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                                                <div class="recordTitleText">
                                                                    <div><i class="fas fa-hotel titleIcon" style="color: white;"></i> Other Rooms and Concessions (managed by RR Team)</div>
                                                                </div>
                                                                <div class="recordTitleButton">
                                                                    <lightning:buttonIcon iconName="{!v.showOtherDetails==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowOtherDetails}" />
                                                                </div>
                                                            </div>
                                                            <div class="recordBodyContent" style="{!v.showOtherDetails!=true?'display: none;':''}">
                                                                <aura:if isTrue="{!not(empty(lodging.otherRoomTypeRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;"><span>Room Type</span></div>
                                                                            <div style="display: flex; min-width: 12em; justify-content: center;"><span>Qty of Rooms</span></div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.allRoomTypeRecords}" var="room" indexVar="roomIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;"><span>{!room.Unit_Type__c}</span></div>
                                                                                <div style="display: flex; min-width: 12em; justify-content: center;"><span>{!room.Units__c}</span></div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                                <aura:if isTrue="{!not(empty(lodging.otherConcessionRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;">Concessions</div>
                                                                            <div style="flex: 1">Notes</div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.otherConcessionRecords}" var="concession" indexVar="concessionIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;">{!concession.Concessions_Requested__c}</div>
                                                                                <div style="flex: 1">{!concession.Notes__c}</div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                    <div class="recordDetails">
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <div><i class="fas fa-map-marked-alt titleIcon"></i> Lodging Details</div>
                                                            </div>
                                                            <div class="recordTitleButton">
                                                                <lightning:buttonIcon iconName="{!v.showRecordDetails==true?'utility:up':'utility:down'}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecordDetails}" />
                                                            </div>
                                                        </div>
                                                        <aura:if isTrue="{!v.showRecordDetails==true}">
                                                            <div class="recordBodyContent">
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField"><label for="Budget__c">Budget Target</label><lightning:input aura:id="recordField" name="Budget__c" type="number" label="" value="{!lodging.budgetTarget}" min="0" variant="label-hidden" formatter="currency" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    <div class="formField">
                                                                        <label for="Distance_to_Venue__c">Distance from Event</label>
                                                                        <div class="fieldSelect">
                                                                            <lightning:select name="Distance_to_Venue__c" label="" value="{!lodging.distanceFromEvent}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                <aura:iteration items="{!v.distanceFromEventOptions}" var="distance">
                                                                                    <option value="{!distance}">{!distance}</option>
                                                                                </aura:iteration>
                                                                            </lightning:select>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField">
                                                                        <label for="Star_Preference__c">Hotel Stars</label>
                                                                        <div class="fieldSelect">
                                                                            <lightning:select name="Star_Preference__c" label="" value="{!lodging.hotelStars}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                <aura:iteration items="{!v.hotelStars}" var="hotelStar">
                                                                                    <option value="{!hotelStar}">{!hotelStar}</option>
                                                                                </aura:iteration>
                                                                            </lightning:select>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formField">
                                                                        <label for="Hotel_Class__c">Hotel Type</label>
                                                                        <div class="fieldSelect">
                                                                            <lightning:select name="Hotel_Class__c" label="" value="{!lodging.hotelType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                <aura:iteration items="{!v.hotelTypes}" var="hotelType">
                                                                                    <option value="{!hotelType}">{!hotelType}</option>
                                                                                </aura:iteration>
                                                                            </lightning:select>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="formField">
                                                                    <label for="Brand_Preference__c">Preferred Brands</label>
                                                                    <lightning:dualListbox name="Brand_Preference__c"
                                                                                           label= ""
                                                                                           sourceLabel="Available"
                                                                                           selectedLabel="Chosen"
                                                                                           options="{!v.preferredBrands}"
                                                                                           value="{!lodging.preferredBrandsList}"
                                                                                           onchange="{!c.handleInputChange}"
                                                                                           variant="label-hidden" />
                                                                </div>
                                                                <div class="preferences">
                                                                    <aura:if isTrue="{!not(empty(lodging.roomTypeRecords))}">
                                                                        <div class="preferencesHeader">
                                                                            <div>Room Type</div>
                                                                            <div>Qty of Rooms</div>
                                                                        </div>
                                                                    </aura:if>
                                                                    <aura:iteration items="{!lodging.roomTypeRecords}" var="room" indexVar="roomIndex">
                                                                        <div class="preferencesRow">
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Unit_Type__c" label="" value="{!room.Unit_Type__c}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.roomTypes}" var="roomType">
                                                                                        <option value="{!roomType}">{!roomType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                            <div class="field">
                                                                                <lightning:input aura:id="recordField" name="Units__c" type="number" label="" value="{!room.Units__c}" variant="label-hidden" min="1" required="true" class="fieldInput" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                <lightning:buttonIcon iconName="utility:clear" value="{!roomIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveRoomType}" />
                                                                            </div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                    <div class="actions">
                                                                        <lightning:button label="Add Room Type" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddRoomType}" />
                                                                    </div>
                                                                </div>
                                                                <div class="preferences">
                                                                    <aura:if isTrue="{!not(empty(lodging.concessionRecords))}">
                                                                        <div class="preferencesHeader">
                                                                            <div>Concessions</div>
                                                                            <div>Notes</div>
                                                                        </div>
                                                                    </aura:if>
                                                                    <aura:iteration items="{!lodging.concessionRecords}" var="concession" indexVar="concessionIndex">
                                                                        <div class="preferencesRow">
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Concessions_Requested__c" label="" value="{!concession.Concessions_Requested__c}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:if isTrue="{!lodging.lodgingType!='housingCorp'}">
                                                                                        <aura:iteration items="{!v.concessionHousingTypes}" var="concessionType">
                                                                                            <option value="{!concessionType}">{!concessionType}</option>
                                                                                        </aura:iteration>
                                                                                        <aura:set attribute="else">
                                                                                            <aura:iteration items="{!v.concessionCorporateTypes}" var="concessionType">
                                                                                                <option value="{!concessionType}">{!concessionType}</option>
                                                                                            </aura:iteration>
                                                                                        </aura:set>
                                                                                    </aura:if>
                                                                                </lightning:select>
                                                                            </div>
                                                                            <div class="field">
                                                                                <lightning:input aura:id="recordField" name="Notes__c" label="" value="{!concession.Notes__c}" variant="label-hidden" class="fieldInput" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                <lightning:buttonIcon iconName="utility:clear" value="{!concessionIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveConcession}" />
                                                                            </div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                    <div class="actions">
                                                                        <lightning:button label="Add Concession" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddConcession}" />
                                                                    </div>
                                                                </div>
                                                                <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                                    <label for="Client_Notes__c">Additional Notes</label>
                                                                    <lightning:textarea name="Client_Notes__c" label="" value="{!lodging.additionalNotes}" variant="label-hidden" onchange="{!c.handleInputChange}" />
                                                                </div>
                                                            </div>
                                                        </aura:if>
                                                    </div>
                                                </aura:if>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <div class="recordTable tripTable">
                                                        <div class="tableTripRow">
                                                            <div class="tripList">
                                                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                    <div class="tableHeader"><span>Lodging Type</span></div>
                                                                    <div class="tripInfo">
                                                                        <aura:if isTrue="{!lodging.lodgingType == 'housingHotel'}"><span>Group hotel</span></aura:if>
                                                                        <aura:if isTrue="{!lodging.lodgingType == 'housingCorp'}"><span>Long term housing</span></aura:if>
                                                                        <aura:if isTrue="{!lodging.lodgingType == 'housingIR'}"><span>Less than 10 rooms</span></aura:if>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="tripList">
                                                                <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Check-In</span></div>
                                                            <div style="flex: 1;"><span>Check-Out</span></div>
                                                            <div class="tableLocation"><span>Location</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.startDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                            <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.endDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                            <div class="tableLocation"><span>{!lodging.cityTitle}</span></div>
                                                        </div>
                                                    </div>
                                                    <div class="recordTable tripTable">
                                                        <div class="tableTripRow">
                                                            <div class="tripList">
                                                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                    <div class="tableHeader"><span>Venue City</span></div>
                                                                    <div class="tripInfo">
                                                                        <span>{!not(empty(lodging.venueId))? lodging.venueName : lodging.otherVenue}</span>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="tripList">
                                                                <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Budget Target</span></div>
                                                            <div style="flex: 1;"><span>Hotel Stars</span></div>
                                                            <div style="flex: 1;"><span>Hotel Type</span></div>
                                                            <div style="flex: 1;"><span>Distance to Event</span></div>
                                                            <div style="flex: 2;"><span>Preferred Brands</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.budgetTarget}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelStars}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelType}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.distanceFromEvent}</span></div>
                                                            <div style="display: flex; align-items: center; flex: 2;">
                                                                <aura:if isTrue="{!not(empty(lodging.preferredBrandsList))}">
                                                                    <span>
                                                                        <aura:iteration items="{!lodging.preferredBrandsList}" var="brand" indexVar="indexBrand">
                                                                            {!brand+if(lodging.preferredBrandsList.length-1>indexBrand,', ','')}
                                                                        </aura:iteration>
                                                                    </span>
                                                                    <!--<ul class="slds-list_dotted"><aura:iteration items="{!lodging.preferredBrandsList}" var="brand"><li style="white-space: pre-wrap;">{!brand}</li></aura:iteration></ul>-->
                                                                    <aura:set attribute="else">-</aura:set>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!not(empty(lodging.allRoomTypeRecords))}">
                                                        <div class="recordTable tableList">
                                                            <div class="tableHeader">
                                                                <div style="flex: 1;"><span>Room Type</span></div>
                                                                <div style="display: flex; min-width: 12em; justify-content: center;"><span>Qty of Rooms</span></div>
                                                            </div>
                                                            <aura:iteration items="{!lodging.allRoomTypeRecords}" var="room" indexVar="roomIndex">
                                                                <div class="tableRow">
                                                                    <div style="flex: 1;"><span>{!room.Unit_Type__c}</span></div>
                                                                    <div style="display: flex; min-width: 12em; justify-content: center;"><span>{!room.Units__c}</span></div>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </aura:if>
                                                    <aura:if isTrue="{!not(empty(lodging.allConcessionRecords))}">
                                                        <div class="recordTable tableList">
                                                            <div class="tableHeader">
                                                                <div style="flex: 1;"><span>Concessions</span></div>
                                                                <div style="flex: 1"><span>Notes</span></div>
                                                            </div>
                                                            <aura:iteration items="{!lodging.allConcessionRecords}" var="concession" indexVar="concessionIndex">
                                                                <div class="tableRow">
                                                                    <div style="flex: 1;"><span>{!concession.Concessions_Requested__c}</span></div>
                                                                    <div style="flex: 1"><span>{!concession.Notes__c}</span></div>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </aura:if>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;"><span>Additional Notes</span></span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!lodging.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.lodgingRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='ground'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-car titleIcon"></i>Ground Travel</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.groundRecords}" var="ground" indexVar="groundIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(ground.isLocked==true,'background-color: #0065ff; color: white;',if(ground.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!groundIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!and(empty(ground.cityTitleStart),empty(ground.cityTitleEnd))}">
                                                <div class="location" title="{!'Trip '+(groundIndex+1)}">{!'Trip '+(groundIndex+1)}</div>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!ground.cityTitleStart+ground.cityTitleEnd}">{!ground.cityTitleStart+ground.cityTitleEnd}</div>
                                                    <div class="dates" style="{!if(empty(ground.startDateTitle),'display:none;','')}">{!ground.startDateTitle} - {!ground.endDateTitle}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==groundIndex?'utility:up':'utility:down'}" value="{!groundIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==groundIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(ground.isLocked==true,'background-color: #c5dcff;',if(ground.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!ground.isLocked!=true}">
                                                <div class="travels">
                                                    <aura:iteration items="{!ground.legs}" var="leg" indexVar="legIndex">
                                                        <div class="travelRow" style="{!if(legIndex>0,'border-top: 1px solid #dbdbdb; margin-top: 0.5em;','')}">
                                                            <div>
                                                                <div class="formColumnThreeChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField">
                                                                            <label for="Sub_Trip_Type__c">Trip Type</label>
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Sub_Trip_Type__c" label="" value="{!leg.subTripType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.tripTypesGround}" var="tripType">
                                                                                        <option value="{!tripType}">{!tripType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                        </div>
                                                                        <div class="formField">
                                                                            <label for="Location_Type__c">Location Pick Up Type</label>
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Location_Type__c" label="" value="{!leg.locationPickUp}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.locationPickUpTypes}" var="pickUpType">
                                                                                        <option value="{!pickUpType}">{!pickUpType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formField">
                                                                        <label for="Location_Details__c">Location Pick Up Details</label>
                                                                        <lightning:input type="text" aura:id="recordField" placeholder="Enter Location" name="Location_Details__c" value="{!leg.locationDetailsPickUp}" variant="label-hidden" required="true" class="formInputTextarea" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="Start_Date__c">Date</label><lightning:input aura:id="recordField" name="Start_Date__c" type="date" dateStyle="short" value="{!leg.datePickUp}" variant="label-hidden" required="true" min="{!v.today}" max="{!leg.dateDropOff}" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="Start_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="Start_Date_Time__c" type="time" value="{!leg.timePickUp}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnThreeChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formColumnBlank"></div>
                                                                        <div class="formField">
                                                                            <label for="Location_Drop_Off_Type__c">Location Drop Off Type</label>
                                                                            <div class="fieldSelect">
                                                                                <lightning:select name="Location_Drop_Off_Type__c" label="" value="{!leg.locationDropOff}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                                    <aura:iteration items="{!v.locationDropOffTypes}" var="dropOffType">
                                                                                        <option value="{!dropOffType}">{!dropOffType}</option>
                                                                                    </aura:iteration>
                                                                                </lightning:select>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formField">
                                                                        <label for="Location_Details__c">Location Drop Off Details</label>
                                                                        <lightning:input type="text" aura:id="recordField" placeholder="Enter Location" name="Location_Details_Drop_Off__c" value="{!leg.locationDetailsDropOff}" variant="label-hidden" required="true" class="formInputTextarea" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="End_Date__c">Date</label><lightning:input aura:id="recordField" name="End_Date__c" type="date" dateStyle="short" value="{!leg.dateDropOff}" min="{!leg.datePickUp}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="End_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="End_Date_Time__c" type="time" value="{!leg.timeDropOff}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="buttonColumn">
                                                                <aura:if isTrue="{!legIndex>0}">
                                                                    <lightning:buttonIcon iconName="utility:clear" value="{!legIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveGroundLeg}" />
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="actions">
                                                        <lightning:button label="Add Leg" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddGroundLeg}" />
                                                    </div>
                                                </div>
                                                <aura:if isTrue="{!not(empty(ground.otherLegs)) || not(empty(ground.otherVehicles))}">
                                                    <div class="recordDetails">
                                                        <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                                            <div class="recordTitleText">
                                                                <div><i class="fas fa-route titleIcon" style="color: white;"></i> Other Legs and Vehicles (managed by RR Team)</div>
                                                            </div>
                                                            <div class="recordTitleButton">
                                                                <lightning:buttonIcon iconName="{!v.showOtherDetails==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowOtherDetails}" />
                                                            </div>
                                                        </div>
                                                        <div class="recordBodyContent" style="{!v.showOtherDetails!=true?'display: none;':''}">
                                                            <aura:iteration items="{!ground.otherLegs}" var="leg">
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;"><div class="tableHeader"><span>Trip Type</span></div><div class="tripInfo"><span>{!leg.subTripType}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Pick Up Type</div><div class="tripInfo"><span>{!leg.locationPickUp}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Pick Up Details</div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Drop Off Type</div><div class="tripInfo"><span>{!leg.locationDropOff}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Location Drop Off Details</div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </aura:iteration>
                                                            <aura:if isTrue="{!not(empty(ground.otherVehicles))}">
                                                                <div class="recordTable tableList">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Bus Type</span></div>
                                                                        <div style="flex: 1;"><span>Qty of Buses</span></div>
                                                                        <div style="flex: 1;"><span># of Passengers</span></div>
                                                                        <div style="flex: 2;"><span>Gear / Luggage Space Needed</span></div>
                                                                        <div style="flex: 1;"><span>Trip Type</span></div>
                                                                    </div>
                                                                    <aura:iteration items="{!ground.otherVehicles}" var="vehicle">
                                                                        <div class="tableRow">
                                                                            <div style="flex: 1;"><span>{!vehicle.busType}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.qtyOfBuses}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.passengers}</span></div>
                                                                            <div style="flex: 2;"><span>{!vehicle.gearLuggage}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.groupType}</span></div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                </div>
                                                            </aura:if>
                                                        </div>
                                                    </div>
                                                </aura:if>
                                                <div class="recordDetails">
                                                    <div class="recordTitle">
                                                        <div class="recordTitleText">
                                                            <div><i class="fas fa-map-marked-alt titleIcon"></i> Ground Details</div>
                                                        </div>
                                                        <div class="recordTitleButton">
                                                            <lightning:buttonIcon iconName="{!v.showRecordDetails==true?'utility:up':'utility:down'}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecordDetails}" />
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.showRecordDetails==true}">
                                                        <div class="recordBodyContent">
                                                            <div class="formColumnTwoChilds">
                                                                <div class="formField">
                                                                    <label for="Vehicle_Type__c">Bus Type</label>
                                                                    <div class="fieldSelect">
                                                                        <lightning:select name="Vehicle_Type__c" label="" value="{!ground.busType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                            <aura:iteration items="{!v.vehicleTypesGround}" var="vehicleType">
                                                                                <option value="{!vehicleType}">{!vehicleType}</option>
                                                                            </aura:iteration>
                                                                        </lightning:select>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField"><label for="Qty_of_Buses__c">Qty of Buses</label><lightning:input aura:id="recordField" name="Qty_of_Buses__c" type="number" value="{!ground.qtyOfBuses}" label="" min="1" step="1" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="Capacity__c"># of Passengers</label><lightning:input aura:id="recordField" name="Capacity__c" type="number" value="{!ground.passengers}" label="" min="1" step="1" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="formColumnTwoChilds">
                                                                <div class="formField">
                                                                    <label for="Gear_Luggage_Space__c">Gear / Luggage Space Needed</label>
                                                                    <lightning:input type="text" aura:id="recordField" name="Gear_Luggage_Space__c" value="{!ground.gearLuggage}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                </div>
                                                                <div class="formField">
                                                                    <label for="Group_Type__c">Group Type</label>
                                                                    <div class="fieldSelect">
                                                                        <lightning:select name="Group_Type__c" label="" value="{!ground.groupType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                            <option value="">--None--</option>
                                                                            <aura:iteration items="{!v.groupTypesGround}" var="groupType">
                                                                                <option value="{!groupType}">{!groupType}</option>
                                                                            </aura:iteration>
                                                                        </lightning:select>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="formField">
                                                                <label for="Amenities__c">Amenities</label>
                                                                <lightning:dualListbox name="Amenities__c"
                                                                                       label= ""
                                                                                       sourceLabel="Available"
                                                                                       selectedLabel="Chosen"
                                                                                       options="{!v.amenitiesGround}"
                                                                                       value="{!ground.amenitiesList}"
                                                                                       onchange="{!c.handleInputChange}"
                                                                                       variant="label-hidden" />
                                                            </div>
                                                            <div class="formField">
                                                                <label for="Other_Amenities__c">Other Amenities</label>
                                                                <lightning:input type="text" aura:id="recordField" name="Other_Amenities__c" value="{!ground.notes}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                            </div>
                                                            <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                                <label for="Client_Notes__c">Additional Notes</label>
                                                                <lightning:textarea aura:id="recordField" name="Client_Notes__c" label="" value="{!ground.additionalNotes}" variant="label-hidden" min="1" onchange="{!c.handleInputChange}" />
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <aura:iteration items="{!ground.allLegs}" var="leg">
                                                        <div class="recordTable tripTable">
                                                            <div class="tableTripRow">
                                                                <div class="tripList">
                                                                    <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;"><div class="tableHeader"><span>Trip Type</span></div><div class="tripInfo"><span>{!leg.subTripType}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Pick Up Type</div><div class="tripInfo"><span>{!leg.locationPickUp}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Pick Up Details</div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                </div>
                                                                <div class="tripList">
                                                                    <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Drop Off Type</div><div class="tripInfo"><span>{!leg.locationDropOff}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader">Location Drop Off Details</div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Bus Type</span></div>
                                                            <div style="flex: 1;"><span>Qty of Buses</span></div>
                                                            <div style="flex: 1;"><span># of Passengers</span></div>
                                                            <div style="flex: 2;"><span>Gear / Luggage Space Needed</span></div>
                                                            <div style="flex: 1;"><span>Trip Type</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;"><span>{!ground.busType}</span></div>
                                                            <div style="flex: 1;"><span>{!ground.qtyOfBuses}</span></div>
                                                            <div style="flex: 1;"><span>{!ground.passengers}</span></div>
                                                            <div style="flex: 2;"><span>{!ground.gearLuggage}</span></div>
                                                            <div style="flex: 1;"><span>{!ground.groupType}</span></div>
                                                        </div>
                                                        <aura:iteration items="{!ground.otherVehicles}" var="vehicle">
                                                            <div class="tableRow">
                                                                <div style="flex: 1;"><span>{!vehicle.busType}</span></div>
                                                                <div style="flex: 1;"><span>{!vehicle.qtyOfBuses}</span></div>
                                                                <div style="flex: 1;"><span>{!vehicle.passengers}</span></div>
                                                                <div style="flex: 2;"><span>{!vehicle.gearLuggage}</span></div>
                                                                <div style="flex: 1;"><span>{!vehicle.groupType}</span></div>
                                                            </div>
                                                        </aura:iteration>
                                                    </div>
                                                    <div class="recordTable tableList">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;">Amenities</div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;">
                                                                <aura:if isTrue="{!not(empty(ground.amenitiesList))}">
                                                                    <aura:iteration items="{!ground.amenitiesList}" var="amenitie" indexVar="indexAmenitie">
                                                                        {!amenitie+if(ground.amenitiesList.length-1>indexAmenitie,', ','')}
                                                                    </aura:iteration>
                                                                    {!if(not(empty(ground.notes)),', '+ground.notes,'')}
                                                                    <aura:set attribute="else">
                                                                        {!if(not(empty(ground.notes)),ground.notes,'-')}
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </div>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em; "><span style="font-weight: 500;">Additional Notes</span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!ground.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.groundRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='air'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-plane titleIcon"></i>Air Travel</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.flightRecords}" var="flight" indexVar="flightIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(flight.isLocked==true,'background-color: #0065ff; color: white;',if(flight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!flightIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!and(empty(flight.cityTitleStart),empty(flight.cityTitleEnd))}">
                                                <div class="location" title="{!'Trip '+(flightIndex+1)}">{!'Flight '+(flightIndex+1)}</div>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!flight.cityTitleStart+flight.cityTitleEnd}">{!flight.cityTitleStart+flight.cityTitleEnd}</div>
                                                    <div class="dates" style="{!if(empty(flight.startDateTitle),'display:none;','')}">{!flight.startDateTitle+(empty(flight.endDateTitle)? '' : ' - '+flight.endDateTitle)}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==flightIndex?'utility:up':'utility:down'}" value="{!flightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==flightIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(flight.isLocked==true,'background-color: #c5dcff;',if(flight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!flight.isLocked!=true}">
                                                <div>
                                                    <lightning:radioGroup aura:id="airForm" name="radioButtonGroup" label="" options="{!v.tripTypes}" value="{!flight.tripType}" type="button" class="noRadius" onchange="{!c.handleChangeAirTrip}" />
                                                </div>
                                                <div class="travels">
                                                    <aura:iteration items="{!flight.segments}" var="segment" indexVar="segmentIndex">
                                                        <div class="travelRow" style="margin-top: 0.5em;">
                                                            <div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField">
                                                                            <label for="Departure_Date__c">{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Return Date','Departure Date')}</label>
                                                                            <lightning:input aura:id="recordField" name="Departure_Date__c" type="date" dateStyle="short" value="{!segment.departureDate}" variant="label-hidden" required="true" label="{!segmentIndex}" min="{!if(segmentIndex>0,segment.arrivalDate,v.today)}" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                        </div>
                                                                        <div style="display: flex; width: 100%;">
                                                                            <div class="formField">
                                                                                <label for="Start_Date_Time__c">{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Return Time','Estimated Times')}</label>
                                                                                <div style="display: flex; width: 100%;">
                                                                                    <lightning:input aura:id="recordField" name="Dep_Time__c" type="time" value="{!segment.departureTimeStart}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                    <div style="display: flex; padding: 0 0.25em; justify-content: center; align-content: center; flex-direction: column;">TO</div>
                                                                                    <lightning:input aura:id="recordField" name="Arr_Time__c" type="time" value="{!segment.departureTimeEnd}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                    <div class="formColumnTwoChilds">
                                                                        <div class="formField">
                                                                            <c:VoyajerCustomLookup objectAPIName="Airport__c" 
                                                                                                   fieldName="Departure_City__c" 
                                                                                                   iconName="custom:custom20" 
                                                                                                   lookupId="{!segment.departureCityId}" 
                                                                                                   label="Departure City" 
                                                                                                   inputPlaceholder="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Enter Location Above','Enter Location')}" 
                                                                                                   isRequired="true" 
                                                                                                   isEdited="{!flight.isEdited}" 
                                                                                                   triggerLookupValidation="{!v.triggerLookupValidation}" 
                                                                                                   isDisabled="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),true,false)}" 
                                                                                                   airportRoundAux="{!c.onAirportRound}" />
                                                                        </div>
                                                                        <div class="formField">
                                                                            <c:VoyajerCustomLookup objectAPIName="Airport__c" 
                                                                                                   fieldName="Arrival_City__c" 
                                                                                                   iconName="custom:custom20" 
                                                                                                   lookupId="{!segment.arrivalCityId}" 
                                                                                                   label="Arrival City" 
                                                                                                   inputPlaceholder="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),'Enter Location Above','Enter Location')}" 
                                                                                                   isRequired="true" 
                                                                                                   isEdited="{!flight.isEdited}" 
                                                                                                   triggerLookupValidation="{!v.triggerLookupValidation}" 
                                                                                                   isDisabled="{!if(and(flight.tripType=='Round Trip',segmentIndex>0),true,false)}" 
                                                                                                   airportRoundAux="{!c.onAirportRound}" />
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="buttonColumn">
                                                                <aura:if isTrue="{!segmentIndex>1}">
                                                                    <lightning:buttonIcon iconName="utility:clear" value="{!segmentIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveSegment}" />
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="actions">
                                                        <aura:if isTrue="{!flight.tripType=='Multi-City'}"><lightning:button label="Add Segment" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddSegment}" /></aura:if>
                                                    </div>
                                                </div>
                                                <div class="formColumnThreeChilds" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                    <div class="formField">
                                                        <label for="Class__c">Class of Service</label>
                                                        <div class="fieldSelect">
                                                            <lightning:select name="Class__c" label="" value="{!flight.classService}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                <aura:iteration items="{!v.classServicesAir}" var="classService">
                                                                    <option value="{!classService}">{!classService}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </div>
                                                    </div>
                                                    <div class="formField"><label for="PAX__c"># of Passengers</label><lightning:input aura:id="recordField" name="PAX__c" type="number" value="{!flight.pax}" label="" min="1" step="1" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                    <div class="formField">
                                                        <label for="Preferred_Airline__c">Preferred Airline</label>
                                                        <div class="fieldSelect">
                                                            <lightning:select name="Preferred_Airline__c" label="" value="{!flight.preferredAirline}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                <option value="">--None--</option>
                                                                <aura:iteration items="{!v.preferredAirlinesAir}" var="preferredAirline">
                                                                    <option value="{!preferredAirline}">{!preferredAirline}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </div>
                                                    </div>
                                                </div>
                                                <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                    <label for="Client_Notes__c">Additional Notes</label>
                                                    <lightning:textarea aura:id="recordField" name="Client_Notes__c" label="" value="{!flight.additionalNotes}" variant="label-hidden" min="1" onchange="{!c.handleInputChange}" />
                                                </div>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <aura:iteration items="{!flight.segments}" var="segment">
                                                        <div class="recordTable tableFields">
                                                            <div class="tableHeader">
                                                                <div style="flex: 2;"><span>Departure Date</span></div>
                                                                <div style="flex: 2;"><span>Estimated Times</span></div>
                                                                <div style="flex: 3;"><span>Departure City</span></div>
                                                                <div style="flex: 3;"><span>Arrival City</span></div>
                                                            </div>
                                                            <div class="tableRow">
                                                                <div style="flex: 2;"><span>{!segment.departureDate}</span></div>
                                                                <div style="flex: 2;"><span><lightning:formattedTime value="{!segment.departureTimeStart}" /> - <lightning:formattedTime value="{!segment.departureTimeEnd}" /></span></div>
                                                                <div style="flex: 3;"><span>{!segment.departureCityName}</span></div>
                                                                <div style="flex: 3;"><span>{!segment.arrivalCityName}</span></div>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 2;"><span>Type of Flight</span></div>
                                                            <div style="flex: 2;"><span>Class of Service</span></div>
                                                            <div style="flex: 3;"><span># of Passengers</span></div>
                                                            <div style="flex: 3;"><span>Preferred Airlines</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 2;"><span>{!flight.tripType}</span></div>
                                                            <div style="flex: 2;"><span>{!flight.classService}</span></div>
                                                            <div style="flex: 3;"><span>{!flight.pax}</span></div>
                                                            <div style="flex: 3;"><span>{!flight.preferredAirline}</span></div>
                                                        </div>
                                                    </div>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!flight.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.flightRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='freight'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-truck titleIcon"></i>Freight</h1>
                            <lightning:button label="New Dates" iconName="utility:add" class="formButtonAction" onclick="{!c.handleNewDates}" />
                        </div>
                    </div>
                    <aura:iteration items="{!v.freightRecords}" var="freight" indexVar="freightIndex">
                        <div class="page-section" style="align-items: center; width: 100%;">
                            <div class="page-section_record">
                                <div class="recordHeader">
                                    <div class="recordBodySideColumn" style="{!if(freight.isLocked==true,'background-color: #0065ff; color: white;',if(freight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                        <span>{!freightIndex+1}</span>
                                    </div>
                                    <div class="recordTitle">
                                        <div class="recordTitleText">
                                            <aura:if isTrue="{!and(empty(freight.cityTitleStart),empty(freight.cityTitleEnd))}">
                                                <div class="location" title="{!'Trip '+(freightIndex+1)}">{!'Trip '+(freightIndex+1)}</div>
                                                <aura:set attribute="else">
                                                    <div class="location" title="{!freight.cityTitleStart+freight.cityTitleEnd}">{!freight.cityTitleStart+freight.cityTitleEnd}</div>
                                                    <div class="dates" style="{!if(empty(freight.startDateTitle),'display:none;','')}">{!freight.startDateTitle} - {!freight.endDateTitle}</div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==freightIndex?'utility:up':'utility:down'}" value="{!freightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==freightIndex?true:false}">
                                    <div class="recordBody">
                                        <div class="recordBodySideColumn hideOnMobile" style="{!if(freight.isLocked==true,'background-color: #c5dcff;',if(freight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                        <div class="recordBodyContent">
                                            <aura:if isTrue="{!freight.isLocked!=true}">
                                                <div class="travels">
                                                    <aura:iteration items="{!freight.legs}" var="leg" indexVar="legIndex">
                                                        <div class="travelRow" style="{!if(legIndex>0,'border-top: 1px solid #dbdbdb; margin-top: 0.5em;','')}">
                                                            <div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField">
                                                                        <label for="Location_Details__c">Pick Up Location</label>
                                                                        <lightning:input type="text" aura:id="recordField" name="Location_Details__c" value="{!leg.locationDetailsPickUp}" placeholder="Enter Location" variant="label-hidden" required="true" class="formInputTextarea" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="Start_Date__c">Date</label><lightning:input aura:id="recordField" name="Start_Date__c" type="date" dateStyle="short" value="{!leg.datePickUp}" variant="label-hidden" required="true" min="{!v.today}" max="{!leg.dateDropOff}" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="Start_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="Start_Date_Time__c" type="time" value="{!leg.timePickUp}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                                <div class="formColumnTwoChilds">
                                                                    <div class="formField">
                                                                        <label for="Location_Details_Drop_Off__c">Drop Off Location</label>
                                                                        <lightning:input type="text" aura:id="recordField" name="Location_Details_Drop_Off__c" value="{!leg.locationDetailsDropOff}" placeholder="Enter Location" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                    </div>
                                                                    <div style="display: flex; width: 100%;">
                                                                        <div class="formField"><label for="End_Date__c">Date</label><lightning:input aura:id="recordField" name="End_Date__c" type="date" dateStyle="short" value="{!leg.dateDropOff}" min="{!leg.datePickUp}" variant="label-hidden" required="true" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                        <div class="formField"><label for="End_Date_Time__c">Time</label><lightning:input aura:id="recordField" name="End_Date_Time__c" type="time" value="{!leg.timeDropOff}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" /></div>
                                                                    </div>
                                                                </div>
                                                            </div>
                                                            <div class="buttonColumn">
                                                                <aura:if isTrue="{!legIndex>0}">
                                                                    <lightning:buttonIcon iconName="utility:clear" value="{!legIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveFreightLeg}" />
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="actions">
                                                        <lightning:button label="Add Leg" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddFreightLeg}" />
                                                    </div>
                                                </div>
                                                <aura:if isTrue="{!not(empty(freight.otherLegs))}">
                                                    <div class="recordDetails">
                                                        <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                                            <div class="recordTitleText">
                                                                <div><i class="fas fa-luggage-cart titleIcon" style="color: white;"></i> Other Legs (managed by RR Team)</div>
                                                            </div>
                                                            <div class="recordTitleButton">
                                                                <lightning:buttonIcon iconName="{!v.showOtherDetails==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowOtherDetails}" />
                                                            </div>
                                                        </div>
                                                        <div class="recordBodyContent" style="{!v.showOtherDetails!=true?'display: none;':''}">
                                                            <aura:iteration items="{!freight.otherLegs}" var="leg">
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow"><div class="tableHeader"><span>Pick Up Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                            <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow"><div class="tableHeader">Drop Off Location</div><div class="tripInfo">{!leg.locationDetailsDropOff}</div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Date of Drop Off</div><div class="tripInfo"><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></div></div>
                                                                            <div class="tableRow"><div class="tableHeader">Time of Drop Off</div><div class="tripInfo"><lightning:formattedTime value="{!leg.timeDropOff}" /></div></div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                            </aura:iteration>
                                                        </div>
                                                    </div>
                                                </aura:if>
                                                <div class="recordDetails">
                                                    <div class="recordTitle">
                                                        <div class="recordTitleText">
                                                            <div><i class="fas fa-map-marked-alt titleIcon"></i> Freight Details</div>
                                                        </div>
                                                        <div class="recordTitleButton">
                                                            <lightning:buttonIcon iconName="{!v.showRecordDetails==true?'utility:up':'utility:down'}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecordDetails}" />
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.showRecordDetails==true}">
                                                        <div class="recordBodyContent">
                                                            <div class="formColumnTwoChilds">
                                                                <div class="formField">
                                                                    <label for="Service_Type__c">Freight Type</label>
                                                                    <div class="fieldSelect">
                                                                        <lightning:select name="Service_Type__c" label="" value="{!freight.groupType}" variant="label-hidden" onchange="{!c.handleInputChange}">
                                                                            <aura:iteration items="{!v.groupTypesFreight}" var="groupType">
                                                                                <option value="{!groupType}">{!groupType}</option>
                                                                            </aura:iteration>
                                                                        </lightning:select>
                                                                    </div>
                                                                </div>
                                                                <div class="formField">
                                                                    <label for="Freight_Trip_Contents__c">Contents</label>
                                                                    <lightning:input type="text" aura:id="recordField" name="Freight_Trip_Contents__c" value="{!freight.notes}" variant="label-hidden" onchange="{!c.handleInputChange}" autocomplete="off" />
                                                                </div>
                                                            </div>
                                                            <div style="text-align: end; padding: 0.5em 0;">
                                                                <aura:if isTrue="{!not(empty(freight.manifestName))}">
                                                                    <div style="display: inline-flex; padding: 0.5em; white-space: nowrap; text-overflow: ellipsis; overflow: hidden; width: 16em;">
                                                                        <span style="padding-right: 0.5em;">Manifest:</span>
                                                                        <span style="font-style: italic;">{!freight.manifestName}</span>
                                                                    </div>
                                                                </aura:if>
                                                                <lightning:button label="Attach Manifest" iconName="utility:note" variant="brand" class="formButtonBrand" onclick="{!c.handleAttachManifestMessage}" />
                                                            </div>
                                                            <div class="formField" style="border-top: 1px solid #dbdbdb; margin-top: 0.5em;">
                                                                <label for="Client_Notes__c">Additional Notes</label>
                                                                <lightning:textarea aura:id="recordField" name="Client_Notes__c" label="" value="{!freight.additionalNotes}" variant="label-hidden" onchange="{!c.handleInputChange}" />
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                                <div class="recordActions">
                                                    <lightning:button label="Save" variant="brand" class="formButtonBrandLight" onclick="{!c.handleSaveRecord}" />
                                                    <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                </div>
                                                <!-- Record Submited -->
                                                <aura:set attribute="else">
                                                    <aura:iteration items="{!freight.allLegs}" var="leg">
                                                        <div class="recordTable tripTable">
                                                            <div class="tableTripRow">
                                                                <div class="tripList">
                                                                    <div class="tableRow"><div class="tableHeader"><span>Pick Up Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                </div>
                                                                <div class="tripList">
                                                                    <div class="tableRow"><div class="tableHeader"><span>Drop Off Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                    <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                </div>
                                                            </div>
                                                        </div>
                                                    </aura:iteration>
                                                    <div class="recordTable tableFields">
                                                        <div class="tableHeader">
                                                            <div style="flex: 1;"><span>Freight Type</span></div>
                                                            <div style="flex: 1;"><span>Contents</span></div>
                                                        </div>
                                                        <div class="tableRow">
                                                            <div style="flex: 1;"><span>{!freight.groupType}</span></div>
                                                            <div style="flex: 1;"><span>{!freight.notes}</span></div>
                                                        </div>
                                                        <div class="tableRow" style="border-top: 1px solid #dbdbdb;">
                                                            <div class="tableHeader"><span>Manifest File Attached</span></div>
                                                            <div class="tripInfo"><span>{!freight.manifestName}</span></div>
                                                        </div>
                                                    </div>
                                                    <div>
                                                        <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                        <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                            <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!freight.additionalNotes}</div>
                                                        </div>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </aura:iteration>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <aura:if isTrue="{!not(empty(v.freightRecords))}"><lightning:button label="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" /></aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='review'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1><i class="fas fa-paper-plane titleIcon"></i>Review &amp; Submit</h1>
                        </div>
                    </div>
                    <div class="page-section" style="align-items: flex-end; justify-content: flex-end; width: 100%;">
                        <div class="topNavigator" style="border-bottom: 0; ">
                            <div class="buttonsNavigator">
                                <aura:if isTrue="{!v.isLodgingSelected}">
                                    <div class="centerDiv" onclick="{!c.showLodgingRecords}" style="{!v.tabSelected=='Lodging'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Lodging</div>
                                        <div class="showOnTablet"><i class="fas fa-home tabIcon"></i></div>
                                    </div>
                                </aura:if>
                                <aura:if isTrue="{!v.isGroundSelected}">
                                    <div class="centerDiv" onclick="{!c.showGroundRecords}" style="{!v.tabSelected=='Ground Travel'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Ground Travel</div>
                                        <div class="showOnTablet"><i class="fas fa-car tabIcon"></i></div>
                                    </div>
                                </aura:if>
                                <aura:if isTrue="{!v.isAirSelected}">
                                    <div class="centerDiv" onclick="{!c.showAirRecords}" style="{!v.tabSelected=='Air'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Air</div>
                                        <div class="showOnTablet"><i class="fas fa-plane tabIcon"></i></div>
                                    </div>
                                </aura:if>
                                <aura:if isTrue="{!v.isFreightSelected}">
                                    <div class="centerDiv" onclick="{!c.showFreightRecords}" style="{!v.tabSelected=='Freight'? 'border-bottom: 0.25em solid #0065ff;':''}">
                                        <div class="hideOnTablet">Freight</div>
                                        <div class="showOnTablet"><i class="fas fa-truck tabIcon"></i></div>
                                    </div>
                                </aura:if>
                            </div>
                        </div>
                    </div>
                    <div class="page-section" style="align-items: center; width: 100%;">
                        <div class="page-section_record" style="margin-top: 0;">
                            <div class="recordHeader">
                                <div class="recordTitle">
                                    <div class="recordTitleText">
                                        <div><i class="fas fa-map-marked-alt titleIcon"></i> {!v.tabSelected} Review</div>
                                    </div>
                                </div>
                            </div>
                            <div class="recordBody">
                                <div class="recordBodyContent">
                                    <aura:if isTrue="{!v.tabSelected=='Lodging'}">
                                        <aura:iteration items="{!v.lodgingRecords}" var="lodging" indexVar="lodgingIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(lodging.isLocked==true,'background-color: #0065ff; color: white;',if(lodging.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!lodgingIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!empty(lodging.cityTitle)}">
                                                                    <div class="location" title="{!'Stay '+(lodgingIndex+1)}">{!'Stay '+(lodgingIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!lodging.cityTitle}">{!lodging.cityTitle}</div>
                                                                        <div class="dates" style="{!if(empty(lodging.startDateTitle),'display:none;','')}">{!lodging.startDateTitle} - {!lodging.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==lodgingIndex?'utility:up':'utility:down'}" value="{!lodgingIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==lodgingIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(lodging.isLocked==true,'background-color: #c5dcff;',if(lodging.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                                <div class="tableHeader"><span>Lodging Type</span></div>
                                                                                <div class="tripInfo">
                                                                                    <aura:if isTrue="{!lodging.lodgingType == 'housingHotel'}"><span>Group hotel</span></aura:if>
                                                                                    <aura:if isTrue="{!lodging.lodgingType == 'housingCorp'}"><span>Apartment/Private Home</span></aura:if>
                                                                                    <aura:if isTrue="{!lodging.lodgingType == 'housingIR'}"><span>Less than 10 rooms</span></aura:if>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Check-In</span></div>
                                                                        <div style="flex: 1;"><span>Check-Out</span></div>
                                                                        <div class="tableLocation"><span>Location</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.startDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                                        <div style="flex: 1;"><span><lightning:formattedDateTime value="{!lodging.endDate}" year="2-digit" month="numeric" day="numeric" /></span></div>
                                                                        <div class="tableLocation"><span>{!lodging.cityTitle}</span></div>
                                                                    </div>
                                                                </div>
                                                                <div class="recordTable tripTable">
                                                                    <div class="tableTripRow">
                                                                        <div class="tripList">
                                                                            <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;">
                                                                                <div class="tableHeader"><span>Venue City</span></div>
                                                                                <div class="tripInfo">
                                                                                    <span>{!not(empty(lodging.venueId))? lodging.venueName : lodging.otherVenue}</span>
                                                                                </div>
                                                                            </div>
                                                                        </div>
                                                                        <div class="tripList">
                                                                            <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Budget Target</span></div>
                                                                        <div style="flex: 1;"><span>Hotel Stars</span></div>
                                                                        <div style="flex: 1;"><span>Hotel Type</span></div>
                                                                        <div style="flex: 1;"><span>Distance to Event</span></div>
                                                                        <div style="flex: 2;"><span>Preferred Brands</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.budgetTarget}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelStars}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.hotelType}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 1;"><span>{!lodging.distanceFromEvent}</span></div>
                                                                        <div style="display: flex; align-items: center; flex: 2;">
                                                                            <aura:if isTrue="{!not(empty(lodging.preferredBrandsList))}">
                                                                                <span>
                                                                                    <aura:iteration items="{!lodging.preferredBrandsList}" var="brand" indexVar="indexBrand">
                                                                                        {!brand+if(lodging.preferredBrandsList.length-1>indexBrand,', ','')}
                                                                                    </aura:iteration>
                                                                                </span>
                                                                                <!--<ul class="slds-list_dotted"><aura:iteration items="{!lodging.preferredBrandsList}" var="brand"><li style="white-space: pre-wrap;">{!brand}</li></aura:iteration></ul>-->
                                                                                <aura:set attribute="else">-</aura:set>
                                                                            </aura:if>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!not(empty(lodging.allRoomTypeRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;"><span>Room Type</span></div>
                                                                            <div style="display: flex; min-width: 12em; justify-content: center;"><span>Qty of Rooms</span></div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.allRoomTypeRecords}" var="room" indexVar="roomIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;"><span>{!room.Unit_Type__c}</span></div>
                                                                                <div style="display: flex; min-width: 12em; justify-content: center;"><span>{!room.Units__c}</span></div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                                <aura:if isTrue="{!not(empty(lodging.allConcessionRecords))}">
                                                                    <div class="recordTable tableList">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 1;"><span>Concessions</span></div>
                                                                            <div style="flex: 1"><span>Notes</span></div>
                                                                        </div>
                                                                        <aura:iteration items="{!lodging.allConcessionRecords}" var="concession" indexVar="concessionIndex">
                                                                            <div class="tableRow">
                                                                                <div style="flex: 1;"><span>{!concession.Concessions_Requested__c}</span></div>
                                                                                <div style="flex: 1"><span>{!concession.Notes__c}</span></div>
                                                                            </div>
                                                                        </aura:iteration>
                                                                    </div>
                                                                </aura:if>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!lodging.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!lodging.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                    <aura:if isTrue="{!v.tabSelected=='Ground Travel'}">
                                        <aura:iteration items="{!v.groundRecords}" var="ground" indexVar="groundIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(ground.isLocked==true,'background-color: #0065ff; color: white;',if(ground.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!groundIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!and(empty(ground.cityTitleStart),empty(ground.cityTitleEnd))}">
                                                                    <div class="location" title="{!'Trip '+(groundIndex+1)}">{!'Trip '+(groundIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!ground.cityTitleStart+ground.cityTitleEnd}">{!ground.cityTitleStart+ground.cityTitleEnd}</div>
                                                                        <div class="dates" style="{!if(empty(ground.startDateTitle),'display:none;','')}">{!ground.startDateTitle} - {!ground.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==groundIndex?'utility:up':'utility:down'}" value="{!groundIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==groundIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(ground.isLocked==true,'background-color: #c5dcff;',if(ground.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <aura:iteration items="{!ground.allLegs}" var="leg">
                                                                    <div class="recordTable tripTable">
                                                                        <div class="tableTripRow">
                                                                            <div class="tripList">
                                                                                <div class="tableRow" style="border-bottom: 1px solid #dbdbdb;"><div class="tableHeader"><span>Trip Type</span></div><div class="tripInfo"><span>{!leg.subTripType}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Pick Up Type</div><div class="tripInfo"><span>{!leg.locationPickUp}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Pick Up Details</div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                            </div>
                                                                            <div class="tripList">
                                                                                <div class="tableRow formColumnBlank" style="padding: 0.5em 1em; color: white; border-bottom: 1px solid #dbdbdb;">.</div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Drop Off Type</div><div class="tripInfo"><span>{!leg.locationDropOff}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader">Location Drop Off Details</div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </aura:iteration>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Bus Type</span></div>
                                                                        <div style="flex: 1;"><span>Qty of Buses</span></div>
                                                                        <div style="flex: 1;"><span># of Passengers</span></div>
                                                                        <div style="flex: 2;"><span>Gear / Luggage Space Needed</span></div>
                                                                        <div style="flex: 1;"><span>Trip Type</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;"><span>{!ground.busType}</span></div>
                                                                        <div style="flex: 1;"><span>{!ground.qtyOfBuses}</span></div>
                                                                        <div style="flex: 1;"><span>{!ground.passengers}</span></div>
                                                                        <div style="flex: 2;"><span>{!ground.gearLuggage}</span></div>
                                                                        <div style="flex: 1;"><span>{!ground.groupType}</span></div>
                                                                    </div>
                                                                    <aura:iteration items="{!ground.otherVehicles}" var="vehicle">
                                                                        <div class="tableRow">
                                                                            <div style="flex: 1;"><span>{!vehicle.busType}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.qtyOfBuses}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.passengers}</span></div>
                                                                            <div style="flex: 2;"><span>{!vehicle.gearLuggage}</span></div>
                                                                            <div style="flex: 1;"><span>{!vehicle.groupType}</span></div>
                                                                        </div>
                                                                    </aura:iteration>
                                                                </div>
                                                                <div class="recordTable tableList">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;">Amenities</div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;">
                                                                            <aura:if isTrue="{!not(empty(ground.amenitiesList))}">
                                                                                <aura:iteration items="{!ground.amenitiesList}" var="amenitie" indexVar="indexAmenitie">
                                                                                    {!amenitie+if(ground.amenitiesList.length-1>indexAmenitie,', ','')}
                                                                                </aura:iteration>
                                                                                {!if(not(empty(ground.notes)),', '+ground.notes,'')}
                                                                                <aura:set attribute="else">
                                                                                    {!if(not(empty(ground.notes)),ground.notes,'-')}
                                                                                </aura:set>
                                                                            </aura:if>
                                                                        </div>
                                                                    </div>
                                                                </div>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em; "><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!ground.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!ground.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                    <aura:if isTrue="{!v.tabSelected=='Air'}">
                                        <aura:iteration items="{!v.flightRecords}" var="flight" indexVar="flightIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(flight.isLocked==true,'background-color: #0065ff; color: white;',if(flight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!flightIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!and(empty(flight.cityTitleStart),empty(flight.cityTitleEnd))}">
                                                                    <div class="location" title="{!'Trip '+(flightIndex+1)}">{!'Flight '+(flightIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!flight.cityTitleStart+flight.cityTitleEnd}">{!flight.cityTitleStart+flight.cityTitleEnd}</div>
                                                                        <div class="dates" style="{!if(empty(flight.startDateTitle),'display:none;','')}">{!flight.startDateTitle} - {!flight.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==flightIndex?'utility:up':'utility:down'}" value="{!flightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==flightIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(flight.isLocked==true,'background-color: #c5dcff;',if(flight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <aura:iteration items="{!flight.segments}" var="segment">
                                                                    <div class="recordTable tableFields">
                                                                        <div class="tableHeader">
                                                                            <div style="flex: 2;"><span>Departure Date</span></div>
                                                                            <div style="flex: 2;"><span>Estimated Times</span></div>
                                                                            <div style="flex: 3;"><span>Departure City</span></div>
                                                                            <div style="flex: 3;"><span>Arrival City</span></div>
                                                                        </div>
                                                                        <div class="tableRow">
                                                                            <div style="flex: 2;"><span>{!segment.departureDate}</span></div>
                                                                            <div style="flex: 2;"><span><lightning:formattedTime value="{!segment.departureTimeStart}" /> - <lightning:formattedTime value="{!segment.departureTimeEnd}" /></span></div>
                                                                            <div style="flex: 3;"><span>{!segment.departureCityName}</span></div>
                                                                            <div style="flex: 3;"><span>{!segment.arrivalCityName}</span></div>
                                                                        </div>
                                                                    </div>
                                                                </aura:iteration>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 2;"><span>Type of Flight</span></div>
                                                                        <div style="flex: 2;"><span>Class of Service</span></div>
                                                                        <div style="flex: 3;"><span># of Passengers</span></div>
                                                                        <div style="flex: 3;"><span>Preferred Airlines</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 2;"><span>{!flight.tripType}</span></div>
                                                                        <div style="flex: 2;"><span>{!flight.classService}</span></div>
                                                                        <div style="flex: 3;"><span>{!flight.pax}</span></div>
                                                                        <div style="flex: 3;"><span>{!flight.preferredAirline}</span></div>
                                                                    </div>
                                                                </div>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!flight.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!flight.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                    <aura:if isTrue="{!v.tabSelected=='Freight'}">
                                        <aura:iteration items="{!v.freightRecords}" var="freight" indexVar="freightIndex">
                                            <div class="page-section" style="align-items: center; width: 100%;">
                                                <div class="page-section_record">
                                                    <div class="recordHeader">
                                                        <div class="recordBodySideColumn" style="{!if(freight.isLocked==true,'background-color: #0065ff; color: white;',if(freight.isEdited==true,'background-color: #ff0000; color: white;',''))}">
                                                            <span>{!freightIndex+1}</span>
                                                        </div>
                                                        <div class="recordTitle">
                                                            <div class="recordTitleText">
                                                                <aura:if isTrue="{!and(empty(freight.cityTitleStart),empty(freight.cityTitleEnd))}">
                                                                    <div class="location" title="{!'Trip '+(freightIndex+1)}">{!'Trip '+(freightIndex+1)}</div>
                                                                    <aura:set attribute="else">
                                                                        <div class="location" title="{!freight.cityTitleStart+freight.cityTitleEnd}">{!freight.cityTitleStart+freight.cityTitleEnd}</div>
                                                                        <div class="dates" style="{!if(empty(freight.startDateTitle),'display:none;','')}">{!freight.startDateTitle} - {!freight.endDateTitle}</div>
                                                                    </aura:set>
                                                                </aura:if>
                                                            </div>
                                                            <div class="recordTitleButton"><lightning:buttonIcon iconName="{!v.recordOpened==freightIndex?'utility:up':'utility:down'}" value="{!freightIndex}" variant="bare" alternativeText="Open" onclick="{!c.handleShowRecord}" /></div>
                                                        </div>
                                                    </div>
                                                    <aura:if isTrue="{!v.recordOpened==freightIndex?true:false}">
                                                        <div class="recordBody">
                                                            <div class="recordBodySideColumn hideOnMobile" style="{!if(freight.isLocked==true,'background-color: #c5dcff;',if(freight.isEdited==true,'background-color: #ffe9e9;',''))}"></div>
                                                            <div class="recordBodyContent">
                                                                <aura:iteration items="{!freight.allLegs}" var="leg">
                                                                    <div class="recordTable tripTable">
                                                                        <div class="tableTripRow">
                                                                            <div class="tripList">
                                                                                <div class="tableRow"><div class="tableHeader"><span>Pick Up Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsPickUp}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.datePickUp}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Pick Up</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timePickUp}" /></span></div></div>
                                                                            </div>
                                                                            <div class="tripList">
                                                                                <div class="tableRow"><div class="tableHeader"><span>Drop Off Location</span></div><div class="tripInfo"><span>{!leg.locationDetailsDropOff}</span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Date of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedDateTime value="{!leg.dateDropOff}" year="2-digit" month="numeric" day="numeric" timeZone="UTC" /></span></div></div>
                                                                                <div class="tableRow"><div class="tableHeader"><span>Time of Drop Off</span></div><div class="tripInfo"><span><lightning:formattedTime value="{!leg.timeDropOff}" /></span></div></div>
                                                                            </div>
                                                                        </div>
                                                                    </div>
                                                                </aura:iteration>
                                                                <div class="recordTable tableFields">
                                                                    <div class="tableHeader">
                                                                        <div style="flex: 1;"><span>Freight Type</span></div>
                                                                        <div style="flex: 1;"><span>Contents</span></div>
                                                                    </div>
                                                                    <div class="tableRow">
                                                                        <div style="flex: 1;"><span>{!freight.groupType}</span></div>
                                                                        <div style="flex: 1;"><span>{!freight.notes}</span></div>
                                                                    </div>
                                                                    <div class="tableRow" style="border-top: 1px solid #dbdbdb;">
                                                                        <div class="tableHeader"><span>Manifest File Attached</span></div>
                                                                        <div class="tripInfo"><span>{!freight.manifestName}</span></div>
                                                                    </div>
                                                                </div>
                                                                <div>
                                                                    <div style="margin-top: 1em; padding: 0 0.25em;"><span style="font-weight: 500;">Additional Notes</span></div>
                                                                    <div class="recordTable" style="padding: 0.5em 1em; min-height: 4em;">
                                                                        <div style="text-align: justify; display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; text-overflow: ellipsis;">{!freight.additionalNotes}</div>
                                                                    </div>
                                                                </div>
                                                                <aura:if isTrue="{!freight.isLocked!=true}">
                                                                    <div class="recordActions" style="text-align: end;">
                                                                        <lightning:button label="Delete" onclick="{!c.handleDeleteRecord}" />
                                                                        <lightning:button label="Edit" variant="brand" class="formButtonBrandLight" onclick="{!c.handleEditRecord}" />
                                                                    </div>
                                                                </aura:if>
                                                            </div>
                                                        </div>
                                                    </aura:if>
                                                </div>
                                            </div>
                                        </aura:iteration>
                                    </aura:if>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div style="display: flex; justify-content: flex-end;">
                        <lightning:button label="Back" onclick="{!c.handleBack}" />
                        <lightning:button label="Submit" variant="brand" class="formButtonBrand" onclick="{!c.handleSubmit}" />
                    </div>
                </aura:if>
            </div>
            <aura:if isTrue="{!v.openAttachment}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container" style="max-width: 24em;">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Attach your manifest</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <div style="text-align: center;"><lightning:fileUpload label="" recordId="{!v.userId}" onuploadfinished="{!c.handleUploadFinished}" /></div>
                            <div style="display: flex; justify-content: center; margin-top: 1em;"><lightning:fileCard fileId="{!v.fileId}" description="{!v.fileName}"/></div>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="Cancel" title="Cancel" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Confirm" title="Confirm" variant="brand" class="formButtonBrandLight" onclick="{!c.handleConfirmFile}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openBackConfirmation}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">We need a confirmation!</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You have records pending to be saved. All your changes will be lost.</p>
                            <br/>
                            <p>Do you want to go back?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="Not yet" title="Not yet" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Go back" title="Go back" variant="brand" class="formButtonBrandLight" onclick="{!c.handleBack}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openNextConfirmation}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">We need a confirmation!</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You have records pending to be saved. All your changes will be lost.</p>
                            <br/>
                            <p>Do you want to continue?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="Not yet" title="Not yet" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Continue" title="Continue" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNext}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
        </div>
    </div>
</aura:component>
```

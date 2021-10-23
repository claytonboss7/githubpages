---
layout: default
title: VoyajerVendor
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerVendor
## Fields
### VoyajerVendorController

```
({
	doInit : function(component, event, helper) {
        var userProfile = component.get("v.userProfile");
        component.set("v.vendorProfile",{
            accountId: "",
            RecordTypeId: "",
            Name: "",
            Vendor_Type__c: "",
            ParentId: "",
            Management_Company_lookup__c: "",
            ShippingStreet: "",
            City__c: "",
            ShippingState: "",
            ShippingPostalCode: "",
            ShippingCountry: "",
            Metro_Area__c: "",
            Phone: "",
            X24_hr_Emergency_Phone__c: "",
            Fax: "",
            Website: "",
            GT_Vendor_Type__c: "",
            Service_Areas_Cities_and_notes__c: "",
            DOT__c: "",
            IFTA__c: "",
            Insurance__c: "",
            Associations__c: ""
        });
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorProfile");
        callToParent.fire();
	},
    
    handleCountryChange : function(component, event, helper) {
        var country = event.getSource().get("v.value");
        var countryAndStates = component.get("v.countryAndStates");
        component.set("v.disableState",true);
        var states = [];
        for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
        if(states.length>0) {
            component.set("v.disableState",false);
            component.set("v.states",states);
        } else component.set("v.states",["--- None ---"]);
    },
    
    loadVendorData : function(component, event, helper) {
        var vendorData = component.get("v.vendorData");
        var menuSelected = component.get("v.menuSelected");
        var currentAction = component.get("v.currentAction");
        var message = "";
        console.log(vendorData);
        switch (menuSelected) {
            case "profile":
                var country = vendorData.ShippingCountry;
                var countryAndStates = component.get("v.countryAndStates");
                component.set("v.disableState",true);
                var states = [];
                for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
                if(states.length>0) {
                    component.set("v.disableState",false);
                    component.set("v.states",states);
                } else component.set("v.states",["--- None ---"]);
                component.set("v.vendorProfile",vendorData);
                if(currentAction == "profileOnEdit")message = "Basic Info updated!";
                break;
            case "contacts":
                component.set("v.vendorContacts",vendorData);
                if(currentAction == "contactNew") message = "Contact created!";
                if(currentAction == "contactOnEdit") message = "Contact updated!";
                if(currentAction == "contactRemoved") message = "Contact deleted!";
                break;
            case "payment":
                component.set("v.vendorGT",vendorData);
                if(currentAction == "paymentOnEdit") message = "Payments updated!";
                break;
            case "propertyProfile":
            case "propertyInRoom":
            case "propertyOnSite":
                component.set("v.vendorProperty",vendorData);
                if(currentAction == "propertyOnEdit") message = "Property Profile updated!";
                if(currentAction == "inRoomOnEdit") message = "Property In-Room Amenities updated!";
                if(currentAction == "onSiteOnEdit") message = "Property On-Site Amenities updated!";
                break;
            case "groundCoach":
                if(currentAction == "vehicleNew" || currentAction == "vehicleOnEdit" || currentAction == "vehicleRemoved") {
                    component.set("v.vendorVehicles",vendorData);
                    if(currentAction == "vehicleNew") message = "Vehicle created!";
                    if(currentAction == "vehicleOnEdit") message = "Vehicle updated!";
                    if(currentAction == "vehicleRemoved") message = "Vehicle deleted!";
                }
                if(currentAction == "availableAmenitiesEdit") {
                    component.set("v.vendorGT",vendorData);
                    message = "Amenities updated!";
                }
                if(!currentAction) {
                    component.set("v.vendorVehicles",vendorData.vehicles);
                    component.set("v.vendorGT",vendorData.coach);
                }
                break;
            case "groundChauffeured":
            case "groundRental":
                component.set("v.vendorGT",vendorData);
                if(currentAction == "chauffeuredOnEdit") message = "Fleet Details - Chauffeured updated!";
                break;
            default:
                break;
        }
        if(!!currentAction) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({ type: "success", title: "", message: message });
            toastEvent.fire();
        }
        component.set("v.recordOpened",-1);
        component.set("v.currentAction","");
        component.set("v.openNewContact",false);
        component.set("v.openRemoveContact",false);
        component.set("v.openNewVehicle",false);
        component.set("v.openRemoveVehicle",false); 
    },
    
    formLoaded : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","contentLoaded");
        callToParent.fire();
	},
    
    loadMenuContent : function(component, event, helper) {
        var menuSelected = event.target.id;
        component.set("v.recordOpened",-1);
        component.set("v.currentAction","");
        if(menuSelected == "profile") component.set("v.showSubMenu",false);
        if(menuSelected == "contacts") component.set("v.showSubMenu",false);
        if(menuSelected == "privacy") component.set("v.showSubMenu",false);
        if(menuSelected == "propertyProfile") component.set("v.showSubMenu",true);
        if(menuSelected == "groundCoach") component.set("v.showSubMenu",true);
        if(menuSelected == "groundPayment") component.set("v.showSubMenu",false);
        component.set("v.menuSelected",menuSelected);
        var callToParent = component.getEvent("callToParent");
        switch (menuSelected) {
            case "profile": callToParent.setParam("action","loadVendorProfile"); break;
            case "contacts": callToParent.setParam("action","loadVendorContacts"); break;
            case "payment": callToParent.setParam("action","loadPayment"); break;
            case "propertyProfile": callToParent.setParam("action","loadPropertyProfile"); break;
            case "propertyInRoom": callToParent.setParam("action","loadPropertyInRoom"); break;
            case "propertyOnSite": callToParent.setParam("action","loadPropertyOnSite"); break;
            case "groundCoach": callToParent.setParam("action","loadFleetCoach"); break;
            case "groundChauffeured": callToParent.setParam("action","loadFleetChauffeured"); break;
            case "groundRental": callToParent.setParam("action","loadFleetRental"); break;
            default: break;
        }
        if(!!callToParent.getParam("action")) callToParent.fire();
    },
    
    saveVendorProfile : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else {
                switch (fieldName) {
                    case "Management_Company_lookup__c":
                    case "City__c":
                        return validSoFar && reportValidity;
                        break;
                    default:
                        return validSoFar;
                        break;
                }
                return validSoFar;
            }
        }, true);
        if(allValid) {
            component.set("v.currentAction","profileOnEdit");
            var userProfile = component.get("v.userProfile");
            var vendorProfile = component.get("v.vendorProfile");
            var callToParent = component.getEvent("callToParent");
            var data = {
                accountId: vendorProfile.accountId,
                ShippingStreet: vendorProfile.ShippingStreet,
                City__c: Array.isArray(vendorProfile.City__c)? '' : vendorProfile.City__c,
                ShippingState: vendorProfile.ShippingState,
                ShippingPostalCode: vendorProfile.ShippingPostalCode,
                ShippingCountry: vendorProfile.ShippingCountry,
                Phone: vendorProfile.Phone,
                Fax: vendorProfile.Fax,
                Website: vendorProfile.Website,
                userProfile: userProfile
            };
            switch (userProfile) {
                case "HousingVendor":
                    data.Vendor_Type__c = vendorProfile.Vendor_Type__c;
                    data.Management_Company_lookup__c = Array.isArray(vendorProfile.Management_Company_lookup__c)? '' : vendorProfile.Management_Company_lookup__c;
                    data.Metro_Area__c = vendorProfile.Metro_Area__c;
                    break;
                case "GroundVendor":
                    data.X24_hr_Emergency_Phone__c = vendorProfile.X24_hr_Emergency_Phone__c;
                    data.GT_Vendor_Type__c = vendorProfile.GT_Vendor_Type__c;
                    data.Service_Areas_Cities_and_notes__c = vendorProfile.Service_Areas_Cities_and_notes__c;
                    data.DOT__c = vendorProfile.DOT__c;
                    data.IFTA__c = vendorProfile.IFTA__c;
                    data.Insurance__c = vendorProfile.Insurance__c;
                    data.Associations__c = vendorProfile.Associations__c;
                    break;
                default:
                    break;
            }
            callToParent.setParam("action","saveVendorProfile");
            callToParent.setParam("data",data);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleShowRecord : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        var recordOpened = component.get("v.recordOpened");
        var records = [];
        var menuSelected = component.get("v.menuSelected");
        if(menuSelected == "contacts") records = component.get("v.vendorContacts");
        if(menuSelected == "groundCoach") records = component.get("v.vendorVehicles");
        var vendorEditRecord = {};
        if(recordOpened !== index) {
            component.set("v.recordOpened",index);
            vendorEditRecord = records[index];
            if(menuSelected == "contacts") component.set("v.currentAction","contactOnEdit");
            if(menuSelected == "groundCoach") component.set("v.currentAction","vehicleOnEdit");
        } else {
            component.set("v.recordOpened",-1);
            component.set("v.currentAction","");
        }
        component.set("v.vendorEditRecord",vendorEditRecord);
    },
    
    handleCloseModal : function(component, event, helper) {
        component.set("v.recordOpened",-1);
        component.set("v.recordToDelete",-1); 
        component.set("v.vendorEditRecord",{});
        component.set("v.currentAction","");
        component.set("v.openNewContact",false);
        component.set("v.openRemoveContact",false);
        component.set("v.openNewVehicle",false);
        component.set("v.openRemoveVehicle",false); 
    },
    
    handleNewVendorContact : function(component, event, helper) {
        component.set("v.openNewContact",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{
            contactId: "",
            firstName: "",
            lastName: "",
            title: "",
            phone: "",
            ext: "",
            mobile: "",
            email: ""
        });
        component.set("v.currentAction","contactNew");
    },
    
    saveVendorContact : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveVendorContact");
            callToParent.setParam("data",component.get("v.vendorEditRecord"));
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleShowRemoveContact : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        component.set("v.recordToDelete",index);
        component.set("v.currentAction","contactRemoved");
        component.set("v.openRemoveContact",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{});
    },
    
    removeContact : function(component, event, helper) {
        var contactId = component.get("v.vendorContacts")[component.get("v.recordToDelete")].contactId;
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","removeContact");
        callToParent.setParam("data",contactId);
        callToParent.fire();
    },
    
    savePropertyProfile : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else {
                switch (fieldName) {
                    default:
                        return validSoFar;
                        break;
                }
                return validSoFar;
            }
        }, true);
        if(allValid) {
            var vendorProperty = JSON.parse(JSON.stringify(component.get("v.vendorProperty")));
            if(vendorProperty.Extended_Stay__c != 'Yes') {
                vendorProperty.Studios__c = 0;
                vendorProperty.Studios_Bed_Size__c = "";
                vendorProperty.Studio_Area__c = "";
                vendorProperty.X1_bedrooms__c = 0;
                vendorProperty.X1_bedroom_bed_size__c = "";
                vendorProperty.X1_bedrooms_Area__c = "";
                vendorProperty.X1_bedrooms_w_Den__c = 0;
                vendorProperty.X1_bedroom_w_Den_bed_size__c = "";
                vendorProperty.X1_bedrooms_w_Den_Area__c = "";
                vendorProperty.X2_bedroom_1_bath__c = 0;
                vendorProperty.X2_bedroom_1_bath_bed_size__c = "";
                vendorProperty.X2_bedroom_1_bath_Area__c = "";
                vendorProperty.X2_bedroom_2_bath__c = 0;
                vendorProperty.X2_bedroom_2_bath_bed_size__c = "";
                vendorProperty.X2_bedroom_2_bath_Area__c = "";
            }
            if(vendorProperty.Porterage_add_l_Info__c.length>0) vendorProperty.Porterage_add_l_Info__c = vendorProperty.Porterage_add_l_Info__c.join(";");
            else vendorProperty.Porterage_add_l_Info__c = "";
            component.set("v.currentAction","propertyOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","savePropertyProfile");
            callToParent.setParam("data",vendorProperty);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    savePropertyInRoom : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        if(allValid) {
            var vendorProperty = JSON.parse(JSON.stringify(component.get("v.vendorProperty")));
            if(vendorProperty.High_Speed_Internet__c != 'Yes') {
                vendorProperty.Connection__c = "";
                vendorProperty.Internet_Charge__c = 0.00;
                vendorProperty.Internet_Charge_Type__c = "";
            }
            if(vendorProperty.Pets_Allowed__c != 'Yes') {
                vendorProperty.Pets_max_LBS__c = 0;
                vendorProperty.Pets_charge__c = 0.00;
                vendorProperty.Pets_charge_type__c = "";
            }
            if(vendorProperty.Refrigerator__c != 'Yes') {
                vendorProperty.Refrigerator_Size__c = "";
                vendorProperty.Refrigerator_charge__c = 0.00;
                vendorProperty.Refrigerator_charge_type__c = "";
                vendorProperty.Refrigerator_Location__c = "";
                vendorProperty.Avail_refrigerators__c = 0;
            }
            if(vendorProperty.Microwave__c != 'Yes') {
                vendorProperty.Microwave_charge__c = 0.00;
                vendorProperty.Microwave_charge_type__c = "";
                vendorProperty.Microwave_Location__c = "";
                vendorProperty.Avail_Microwave__c = 0;
            }
            if(vendorProperty.Oven__c != 'Yes') {
                vendorProperty.Oven_Location__c = "";
            }
            if(vendorProperty.Burners__c != 'Yes') {
                vendorProperty.of_burners__c = "";
                vendorProperty.Burners_location__c = "";
            }
            if(vendorProperty.BathtubOption != 'Yes') {
                vendorProperty.Bathtub__c = "";
            }
            if(vendorProperty.Washer_Dryer__c != 'Yes') {
                vendorProperty.Washer_Dryer_Type__c = "";
            }
            component.set("v.currentAction","inRoomOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","savePropertyInRoom");
            callToParent.setParam("data",vendorProperty);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    savePropertyOnSite : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        if(allValid) {
            var vendorProperty = JSON.parse(JSON.stringify(component.get("v.vendorProperty")));
            if(vendorProperty.Pool__c != 'Yes') vendorProperty.Pool_Seasonal__c = "";
            if(vendorProperty.Hot_Tub__c != 'Yes') vendorProperty.Hot_tub_seasonal__c = "";
            if(vendorProperty.Hotel_Bars__c != 'Yes') {
                vendorProperty.hotel_bars_2__c = 0;
                vendorProperty.Hotel_bar_hours__c = "";
            }
            if(vendorProperty.Restaurants__c != 'Yes') {
                vendorProperty.Restaurants_2__c = 0;
                vendorProperty.Restaurants_hours__c = "";
            }
            if(vendorProperty.Breakfast__c != 'Yes') vendorProperty.Breakfast_type__c = "";
            if(vendorProperty.Room_Service__c != 'Yes') vendorProperty.Room_Service_hours__c = "";
            if(vendorProperty.Managers_Reception__c != 'Yes') vendorProperty.Managers_Reception_Hours__c = "";
            if(vendorProperty.Self_Parking__c != 'Yes') {
                vendorProperty.Self_Parking_Charge__c = 0.00;
                vendorProperty.Self_Parking_Charge_Type__c = "";
                vendorProperty.Self_Parking_Add_l_info__c = "";
            }
            if(vendorProperty.Valet_Parking__c != 'Yes') {
                vendorProperty.Valet_Parking_Charge__c = 0.00;
                vendorProperty.Valet_Parking_Charge_Type__c = "";
                vendorProperty.Valet_Parking_Add_l_info__c = "";
            }
            if(vendorProperty.Coach_Bus_Parking__c != 'Yes') {
                vendorProperty.Coach_Bus_Charge__c = 0.00;
                vendorProperty.Coach_Bus_Charge_Type__c = "";
                vendorProperty.Coach_Bus_Add_l_info__c = "";
                vendorProperty.Coach_Bus_parking_spots__c = 0;
            }
            component.set("v.currentAction","onSiteOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","savePropertyOnSite");
            callToParent.setParam("data",vendorProperty);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleNewVehicle : function(component, event, helper) {
        component.set("v.openNewVehicle",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{
            vehicleId: "",
            vehicleType: "",
            quantity: 0,
            capacity: 0,
            make: "",
            otherMake: "",
            model: "",
            year: ""
        });
        component.set("v.currentAction","vehicleNew");
    },
    
    saveVendorVehicle : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            var value = inputCmp.get("v.value");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else {
                var validate = true;
                switch (fieldName) {
                    case "Vehicle_Type__c":
                    case "Make__c":
                        if(!!value) validate =  true;
                        else validate = false;
                        break;
                    default:
                        break;
                }
                return validSoFar && validate;
            }
        }, true);
        if(allValid) {
            var vendorEditRecord = JSON.parse(JSON.stringify(component.get("v.vendorEditRecord")));
            if(vendorEditRecord.make != "Other") vendorEditRecord.otherMake = "";
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveVendorVehicle");
            callToParent.setParam("data",vendorEditRecord);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleShowRemoveVehicle : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        component.set("v.recordToDelete",index);
        component.set("v.currentAction","vehicleRemoved");
        component.set("v.openRemoveVehicle",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{});
    },
    
    removeVehicle : function(component, event, helper) {
        var vehicleId = component.get("v.vendorVehicles")[component.get("v.recordToDelete")].vehicleId;
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","removeVehicle");
        callToParent.setParam("data",vehicleId);
        callToParent.fire();
    },
    
    saveFleetCoach : function(component, event, helper) {
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{});
        component.set("v.currentAction","");
        component.set("v.openNewVehicle",false);
        var allValid = component.find("recordFieldAmenitie").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.WiFi_coach__c != 'Yes') vendorGT.WiFi_Qty__c = 0;
            if(vendorGT.DVD__c != 'Yes') vendorGT.DVD_Qty__c = 0;
            if(vendorGT.Satellite_TV__c != 'Yes') vendorGT.Satellite_TV_Qty__c = 0;
            if(vendorGT.Table__c != 'Yes') vendorGT.Table_Qty__c = 0;
            if(vendorGT.Trailer_Hitch__c != 'Yes') vendorGT.Trailer_Hitch_Qty__c = 0;
            if(vendorGT.Trailer__c != 'Yes') vendorGT.Trailer_Qty__c = 0;
            if(vendorGT.Restroom__c != 'Yes') vendorGT.Restroom_Qty__c = 0;
            if(vendorGT.Outlets_in_Rows__c != 'Yes') {
                vendorGT.Outlets_in_Rows_Qty__c = 0;
                vendorGT.Outlets_position__c = "";
            }
            if(vendorGT.Executive_Coach__c != 'Yes') {
                vendorGT.Executive_Coach_Qty__c = 0;
                vendorGT.Kitchenettes__c = false;
            }
            if(vendorGT.Sleepers__c != 'Yes') vendorGT.Sleepers_Qty__c = 0;
            if(vendorGT.Sleepers__c == 'Yes' && Array.isArray(vendorGT.Sleepers_Amenities__c) && vendorGT.Sleepers_Amenities__c.length>0) vendorGT.Sleepers_Amenities__c = vendorGT.Sleepers_Amenities__c.join(";");
            else vendorGT.Sleepers_Amenities__c = "";
            component.set("v.currentAction","availableAmenitiesEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveFleetCoach");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    saveFleetChauffeured : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.Sedan__c != 'Yes') vendorGT.Sedan_Notes__c = "";
            if(vendorGT.Executive_Sedan__c != 'Yes') vendorGT.Executive_Sedan_Notes__c = "";
            if(vendorGT.Luxury_Sedan__c != 'Yes') vendorGT.Luxury_Sedan_Notes__c = "";
            if(vendorGT.X12_PAX_Van__c != 'Yes') vendorGT.X12_PAX_Van_Notes__c = "";
            if(vendorGT.X15_PAX_Van__c != 'Yes') vendorGT.X15_PAX_Van_Notes__c = "";
            if(vendorGT.Luggage_Van__c != 'Yes') vendorGT.Luggage_Van_Notes__c = "";
            if(vendorGT.SUV__c != 'Yes') vendorGT.SUV_Notes__c = "";
            if(vendorGT.Limo__c != 'Yes') vendorGT.Limo_notes__c = "";
            if(vendorGT.Mini_Coach__c != 'Yes') vendorGT.Mini_Coach_notes__c = "";
            component.set("v.currentAction","chauffeuredOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveFleetChauffeured");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    saveFleetRental : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.Compact__c != 'Yes') vendorGT.Compact_notes__c = "";
            if(vendorGT.Intermediate__c != 'Yes') vendorGT.Intermediate_notes__c = "";
            if(vendorGT.Standard__c != 'Yes') vendorGT.Standard_notes__c = "";
            if(vendorGT.Full_Size__c != 'Yes') vendorGT.Full_Size_notes__c = "";
            if(vendorGT.Luxury__c != 'Yes') vendorGT.Luxury_notes__c = "";
            if(vendorGT.Standard_SUV__c != 'Yes') vendorGT.Standard_SUV_notes__c = "";
            if(vendorGT.Luxury_SUV__c != 'Yes') vendorGT.Luxury_SUV_notes__c = "";
            if(vendorGT.Mini_Van__c != 'Yes') vendorGT.Mini_Van_notes__c = "";
            if(vendorGT.X12_PAX_Van_Rental__c != 'Yes') vendorGT.X12_PAX_Van_Notes_Rental__c = "";
            if(vendorGT.X15_PAX_Van_Rental__c != 'Yes') vendorGT.X15_PAX_Van_Notes_Rental__c = "";
            if(vendorGT.Hybrid_Car__c != 'Yes') vendorGT.Hybrid_Car_notes__c = "";
            if(vendorGT.Hybrid_SUV__c != 'Yes') vendorGT.Hybrid_SUV_notes__c = "";
            component.set("v.currentAction","chauffeuredOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveFleetRental");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    saveVendorPayment : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.Visa_Accepted__c != 'Yes') vendorGT.Visa_Surcharge__c = 0.00;
            if(vendorGT.Master_Card_Accepted__c != 'Yes') vendorGT.Master_Card_Surcharge__c = 0.00;
            if(vendorGT.American_Express_Accepted__c != 'Yes') vendorGT.American_Express_Surcharge__c = 0.00;
            if(vendorGT.Discover_Accepted__c != 'Yes') vendorGT.Discover_Surcharge__c = 0.00;
            if(vendorGT.Other_Payment__c != 'Yes') vendorGT.Other_payment_notes__c = "";
            console.log(vendorGT);
            component.set("v.currentAction","paymentOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveVendorPayment");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    }
})
```
### VoyajerVendorHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerVendor

```
<aura:component >
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="Boolean" name="disableState" default="true" />
    <aura:attribute type="Boolean" name="showSubMenu" default="false" />
    <aura:attribute type="Boolean" name="openNewContact" default="false" />
    <aura:attribute type="Boolean" name="openNewVehicle" default="false" />
    <aura:attribute type="Boolean" name="openRemoveContact" default="false" />
    <aura:attribute type="Boolean" name="openRemoveVehicle" default="false" />
    <aura:attribute type="String" name="menuSelected" default="profile" />
    <aura:attribute type="String" name="userProfile" />
    <aura:attribute type="String" name="currentAction" default="" />
    <aura:attribute type="List" name="vendorContacts" />
    <aura:attribute type="List" name="vendorVehicles" />
    <aura:attribute type="List" name="countries" />
    <aura:attribute type="List" name="states" />
    <aura:attribute type="List" name="optionsYesNo" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'No', 'value': 'No'}]" />
    <aura:attribute type="List" name="optionsYesContactNo" default="[{'label': 'Yes', 'value': 'Yes, contact property for details'},{'label': 'No', 'value': 'No'}]" />
    <aura:attribute type="List" name="optionsYesNoComplimentary" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'Yes/Complimentary', 'value': 'Yes/Complimentary'},{'label': 'No', 'value': 'No'}]" />
    <aura:attribute type="List" name="optionsYesNoContract" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'No', 'value': 'No'},{'label': 'Yes, Contract property for details', 'value': 'Yes, Contract property for details'}]" />
    <aura:attribute type="List" name="optionsEntry" default="[{'label': 'Both', 'value': 'Both'},{'label': 'Exterior', 'value': 'Exterior'},{'label': 'Interior', 'value': 'Interior'}]" />
    <aura:attribute type="List" name="optionsPorterage" default="[{'label': 'Mandatory', 'value': 'Mandatory'},{'label': 'Available', 'value': 'Available'},{'label': 'Not available', 'value': 'Not available'}]" />
    <aura:attribute type="List" name="optionsPorterageAddInfo" default="[{'label': 'Per bag', 'value': 'Per bag'},{'label': 'Per person', 'value': 'Per person'},{'label': 'RoundTrip', 'value': 'RoundTrip'}]" />
    <aura:attribute type="List" name="optionsOutlets" default="[{'label': 'Every Row', 'value': 'Every Row'},{'label': 'Every Other Row', 'value': 'Every Other Row'}]" />
    <aura:attribute type="List" name="optionsSleepersAmenities" default="[{'label': 'Shower', 'value': 'Shower'},{'label': 'Kitchenettes', 'value': 'Kitchenettes'},{'label': 'Slideout', 'value': 'Slideout'},{'label': 'Restrooms', 'value': 'Restrooms'}]" />
    <aura:attribute type="Object" name="vendorData" />
    <aura:attribute type="Object" name="vendorProfile" />
    <aura:attribute type="Object" name="vendorEditRecord" />
    <aura:attribute type="Object" name="vendorProperty" />
    <aura:attribute type="Object" name="vendorGT" />
    <aura:attribute type="Object" name="countryAndStates" />
    <aura:attribute type="Integer" name="recordOpened" default="-1" />
    <aura:attribute type="Integer" name="recordToDelete" default="-1" />
    <!-- docs -->
    <aura:attribute type="String" name="serviceId" default="a0156000001xchaAAA" />
    <aura:attribute type="List" name="lsDocuments" default="[]" />
	<aura:attribute type="List" name="lsDocumentsAux" default="[]" />
    <!-- end docs -->
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:handler name="change" value="{!v.vendorData}" action="{!c.loadVendorData}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="mainMenu">
            <div class="profilePicName">
                <div class="profilePictureContainer">
                    <lightning:avatar src="{!v.userLogged.FullPhotoUrl}"
                                      onclick="{!c.loadUserContent}"
                                      variant="circle"
                                      initials="{!v.userLogged.Initials__c}"
                                      size="large"
                                      class="profilePicture"
                                      alternativeText="{!v.userLogged.Name}" />
                </div>
                <div class="profileName">
                    <span><b>{!v.userLogged.Name}</b></span>
                </div>
            </div>
            <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page">
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='profile'? ' slds-is-active' : '')}">
                    <a href="javascript:void(0);" id="profile" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Basic Info</a>
                </div>
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='contacts'? ' slds-is-active' : '')}">
                    <a href="javascript:void(0);" id="contacts" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Contacts</a>
                </div>
                <aura:if isTrue="{!or(v.userProfile=='HousingVendor',v.userProfile=='CorporateVendor')}">
                    <div style="{!v.showSubMenu==true?'background: rgba(21, 137, 238, 0.25);':''}">
                        <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='propertyProfile'? ' slds-is-active' : '')}">
                            <a href="javascript:void(0);" id="propertyProfile" class="slds-nav-vertical__action" style="justify-content: space-between;" onclick="{!c.loadMenuContent}">
                                Property Profile <i class="fas fa-chevron-down"></i>
                            </a>
                        </div>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='propertyInRoom'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="propertyInRoom" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">In-Room Amenities</a>
                            </div>
                        </aura:if>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='propertyOnSite'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="propertyOnSite" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">On-Site Amenities</a>
                            </div>
                        </aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.userProfile=='GroundVendor'}">
                    <div style="{!v.showSubMenu==true?'background: rgba(21, 137, 238, 0.25);':''}">
                        <div class="slds-nav-vertical__item">
                            <a href="javascript:void(0);" id="groundCoach" class="slds-nav-vertical__action" style="justify-content: space-between;" onclick="{!c.loadMenuContent}">
                                Fleet Details <i class="fas fa-chevron-down"  onclick="{!c.loadMenuContent}"></i>
                            </a>
                        </div>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='groundCoach'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="groundCoach" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Coach</a>
                            </div>
                        </aura:if>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='groundChauffeured'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="groundChauffeured" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Chauffeured</a>
                            </div>
                        </aura:if>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='groundRental'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="groundRental" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Rental</a>
                            </div>
                        </aura:if>
                    </div>
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='payment'? ' slds-is-active' : '')}">
                        <a href="javascript:void(0);" id="payment" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Payment &amp; Cancellation</a>
                    </div>
                </aura:if>
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='privacy'? ' slds-is-active' : '')}">
                    <a href="javascript:void(0);" id="privacy" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Privacy</a>
                </div>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <!-- HOUSING PAGES -->
                <aura:if isTrue="{!and(v.menuSelected=='profile',or(v.userProfile=='HousingVendor',v.userProfile=='CorporateVendor'))}">
                    <div class="page-section">
                        <div class="page-header"><h1>Basic Info</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="profileForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Name">Property Name<sub class="subLabel"> Call Road Rebel if changes are needed</sub></label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Name}" disabled="true" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Vendor_Type__c">Property Type</label>
                                    <lightning:inputField aura:id="recordField" fieldName="Vendor_Type__c" value="{!v.vendorProfile.Vendor_Type__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="ParentId">Property Chain<sub class="subLabel"> Call Road Rebel if changes are needed</sub></label>
                                    <lightning:inputField aura:id="recordField" fieldName="ParentId" value="{!v.vendorProfile.ParentId}" disabled="true" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="LastName">Management Company</label>
                                    <lightning:inputField aura:id="recordField" fieldName="Management_Company_lookup__c" value="{!v.vendorProfile.Management_Company_lookup__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formField">
                                <label for="ShippingStreet">Street Address</label>
                                <lightning:input aura:id="recordField" type="text" placeholder="Enter Address" value="{!v.vendorProfile.ShippingStreet}" variant="label-hidden" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="City__c">City</label>
                                    <lightning:inputField aura:id="recordField" fieldName="City__c" value="{!v.vendorProfile.City__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnTwoChilds" style="padding: 0 0.75em;">
                                    <div class="formField" style="padding-left: 0;">
                                        <lightning:select aura:id="stateField"
                                                          name="State"
                                                          value="{!v.vendorProfile.ShippingState}"
                                                          label="{!v.countryAndStates.childFieldLabel}"
                                                          disabled="{!v.disableState}">
                                            <aura:iteration items="{!v.states}" var="state">
                                                <option value="{!state}" selected="{!state==v.vendorProfile.ShippingState}">{!state}</option>
                                            </aura:iteration>
                                        </lightning:select>
                                    </div>
                                    <div class="formField" style="padding-right: 0;">
                                        <label for="ShippingPostalCode">Zip</label>
                                        <lightning:inputField aura:id="recordField" fieldName="ShippingPostalCode" value="{!v.vendorProfile.ShippingPostalCode}" variant="label-hidden" />
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <lightning:select aura:id="countryField"
                                                      name="Country"
                                                      value="{!v.vendorProfile.ShippingCountry}"
                                                      label="{!v.countryAndStates.parentFieldLabel}"
                                                      onchange="{!c.handleCountryChange}">
                                        <aura:iteration items="{!v.countries}" var="country">
                                            <option value="{!country}" selected="{!state==v.vendorProfile.ShippingCountry}">{!country}</option>
                                        </aura:iteration>
                                    </lightning:select>
                                </div>
                                <div class="formField">
                                    <label for="Metro_Area__c">Metro Area</label>
                                    <lightning:inputField aura:id="recordField" fieldName="Metro_Area__c" value="{!v.vendorProfile.Metro_Area__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Phone}" required="true" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Fax">Fax Number</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Fax}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Website">Website</label>
                                    <lightning:input aura:id="recordField" type="url" value="{!v.vendorProfile.Website}" variant="label-hidden" required="true" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorProfile}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='propertyProfile'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Property Profile</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Star_Rating__c">Star Rating</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Star_Rating__c}" disabled="true" variant="label-hidden" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnBlank"></div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Check_In_Time__c">Check-In Time</label>
                                    <lightning:input aura:id="recordField" type="time" value="{!v.vendorProperty.Check_In_Time__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Check_out_time__c">Check-Out Time</label>
                                    <lightning:input aura:id="recordField" type="time" value="{!v.vendorProperty.Check_out_time__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <br/>
                            <div class="formField">
                                <label for="X100_Non_Smoking__c">100% Non-Smoking</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.X100_Non_Smoking__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Lift_Elevator__c">Lift/Elevator</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Lift_Elevator__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Property_Entry__c">Property Entry</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsEntry}" value="{!v.vendorProperty.Property_Entry__c}" type="radio" />
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Porterage__c">Porterage</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsPorterage}" value="{!v.vendorProperty.Porterage__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Porterage__c=='Mandatory'}">
                                        <label for="Porterage_Charge__c">Charge</label>
                                        <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Porterage_Charge__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Porterage__c=='Mandatory'}">
                                        <label for="Porterage_add_l_Info__c">Charge Type</label>
                                        <lightning:checkboxGroup label="" options="{!v.optionsPorterageAddInfo}" value="{!v.vendorProperty.Porterage_add_l_Info__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                            </div>
                            <br/>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Number_of_rooms__c">Total Rooms</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Number_of_rooms__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Number_of_suites__c">Total Suites</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Number_of_suites__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Single_Rooms__c">Number of Singles</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Single_Rooms__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Single_Room_Bed_Size__c">Single Room Bed Size</label>
                                    <lightning:inputField fieldName="Single_Room_Bed_Size__c" value="{!v.vendorProperty.Single_Room_Bed_Size__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Single_Room_Area__c">Single Room Size</label>
                                    <lightning:input type="text" value="{!v.vendorProperty.Single_Room_Area__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Double_Rooms__c">Number of Doubles</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Double_Rooms__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Double_Room_Bed_Size__c">Double Room Bed Size</label>
                                    <lightning:inputField fieldName="Double_Room_Bed_Size__c" value="{!v.vendorProperty.Double_Room_Bed_Size__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Double_Room_Area__c">Double Room Size</label>
                                    <lightning:input type="text" value="{!v.vendorProperty.Double_Room_Area__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <br/>
                            <div class="formField">
                                <label for="Extended_Stay__c">Do you offer extended stays?</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Extended_Stay__c}" type="radio" />
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Extended_Stay__c=='Yes'}">
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="Studios__c">Number of Studios</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Studios__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="Studios_Bed_Size__c">Studio Room Bed Size</label>
                                        <lightning:inputField fieldName="Studios_Bed_Size__c" value="{!v.vendorProperty.Studios_Bed_Size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="Studio_Area__c">Studio Room Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Studio_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X1_bedrooms__c">Number of 1-Bedrooms</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X1_bedrooms__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedroom_bed_size__c">1-Bedroom Bed Size</label>
                                        <lightning:inputField fieldName="X1_bedroom_bed_size__c" value="{!v.vendorProperty.X1_bedroom_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedrooms_Area__c">1-Bedroom Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X1_bedrooms_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X1_bedrooms_w_Den__c">Number of 1-Bedrooms w/Den</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X1_bedrooms_w_Den__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedroom_w_Den_bed_size__c">1-Bedroom w/Den Bed Size</label>
                                        <lightning:inputField fieldName="X1_bedroom_w_Den_bed_size__c" value="{!v.vendorProperty.X1_bedroom_w_Den_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedrooms_w_Den_Area__c">1-Bedroom w/Den Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X1_bedrooms_w_Den_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X2_bedroom_1_bath__c">Number of 2-Bedrooms w/ 1-Bath</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X2_bedroom_1_bath__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_1_bath_bed_size__c">2-Bedroom w/ 1-Bath Bed Size</label>
                                        <lightning:inputField fieldName="X2_bedroom_1_bath_bed_size__c" value="{!v.vendorProperty.X2_bedroom_1_bath_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_1_bath_Area__c">2-Bedroom w/ 1-Bath Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X2_bedroom_1_bath_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X2_bedroom_2_bath__c">Number of 2-Bedrooms w/ 2-Bath</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X2_bedroom_2_bath__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_2_bath_bed_size__c">2-Bedroom w/ 2-Bath Bed Size</label>
                                        <lightning:inputField fieldName="X2_bedroom_2_bath_bed_size__c" value="{!v.vendorProperty.X2_bedroom_2_bath_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_2_bath_Area__c">2-Bedroom w/ 2-Bath Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X2_bedroom_2_bath_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                            </aura:if>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.savePropertyProfile}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='propertyInRoom'}">
                    <div class="page-section">
                        <div class="page-header"><h1>In-Room Amenities</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formField">
                                <label for="Windows_Open__c">Windows Open</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Windows_Open__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Air_conditioning__c">Air Conditioning</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Air_conditioning__c}" type="radio" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="High_Speed_Internet__c">High Speed Internet</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.High_Speed_Internet__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.High_Speed_Internet__c=='Yes'}">
                                            <label for="Connection__c">Type</label>
                                            <lightning:inputField fieldName="Connection__c" value="{!v.vendorProperty.Connection__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.High_Speed_Internet__c=='Yes'}">
                                            <label for="Internet_Charge__c">Charge</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Internet_Charge__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.High_Speed_Internet__c=='Yes'}">
                                            <label for="Internet_Charge_Type__c">Charge Type</label>
                                            <lightning:inputField fieldName="Internet_Charge_Type__c" value="{!v.vendorProperty.Internet_Charge_Type__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField" style="min-width: 0;">
                                        <label for="Pets_Allowed__c">Pets Allowed</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoContract}" value="{!v.vendorProperty.Pets_Allowed__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Pets_Allowed__c=='Yes'}">
                                            <label for="Pets_max_LBS__c">Weight Limit</label>
                                            <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Pets_max_LBS__c}" step="1" class="formWeight" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Pets_Allowed__c=='Yes'}">
                                            <label for="Pets_charge__c">Charge</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Pets_charge__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Pets_Allowed__c=='Yes'}">
                                            <label for="Pets_charge_type__c">Charge Type</label>
                                            <lightning:inputField fieldName="Pets_charge_type__c" value="{!v.vendorProperty.Pets_charge_type__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnFourChildsDependant">
                                <div class="formField">
                                    <label for="Refrigerator__c">Refrigerator</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Refrigerator__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Refrigerator__c=='Yes'}">
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Refrigerator_Size__c">Size</label>
                                                <lightning:inputField fieldName="Refrigerator_Size__c" value="{!v.vendorProperty.Refrigerator_Size__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Refrigerator_charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Refrigerator_charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Refrigerator_charge_type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Refrigerator_charge_type__c" value="{!v.vendorProperty.Refrigerator_charge_type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Refrigerator_Location__c">Location</label>
                                                <lightning:inputField fieldName="Refrigerator_Location__c" value="{!v.vendorProperty.Refrigerator_Location__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Avail_refrigerators__c">Quantity Available</label>
                                                <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Avail_refrigerators__c}" step="1" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Refrigerator__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnFourChildsDependant">
                                <div class="formField">
                                    <label for="Microwave__c">Microwave</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Microwave__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Microwave__c=='Yes'}">
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Microwave_charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Microwave_charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Microwave_charge_type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Microwave_charge_type__c" value="{!v.vendorProperty.Microwave_charge_type__c}" variant="label-hidden" />
                                            </div>
                                             <div class="formColumnBlank"></div>
                                        </div>
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Microwave_Location__c">Location</label>
                                                <lightning:inputField fieldName="Microwave_Location__c" value="{!v.vendorProperty.Microwave_Location__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Avail_Microwave__c">Quantity Available</label>
                                                <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Avail_Microwave__c}" step="1" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Microwave__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Oven__c">Oven</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Oven__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Oven__c=='Yes'}">
                                            <label for="Oven_Location__c">Location</label>
                                            <lightning:inputField fieldName="Oven_Location__c" value="{!v.vendorProperty.Oven_Location__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Burners__c">Burners</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Burners__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Burners__c=='Yes'}">
                                            <label for="of_burners__c"># of Burners</label>
                                            <lightning:inputField fieldName="of_burners__c" value="{!v.vendorProperty.of_burners__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Burners__c=='Yes'}">
                                            <label for="Burners_location__c">Location</label>
                                            <lightning:inputField fieldName="Burners_location__c" value="{!v.vendorProperty.Burners_location__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </div>
                            <div class="formField">
                                <label for="Coffee_Maker__c">Coffee Maker</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Coffee_Maker__c}" type="radio" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="BathtubOption">Bathtub</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.BathtubOption}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.BathtubOption=='Yes'}">
                                            <label for="Bathtub__c">Location <abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="Bathtub__c" value="{!v.vendorProperty.Bathtub__c}" variant="label-hidden" required="true" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Washer_Dryer__c">Washer / Dryer</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Washer_Dryer__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Washer_Dryer__c=='Yes'}">
                                            <label for="Washer_Dryer_Type__c">Type</label>
                                            <lightning:inputField fieldName="Washer_Dryer_Type__c" value="{!v.vendorProperty.Washer_Dryer_Type__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Hairdryers__c">Hair Dryerr</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hairdryers__c}" type="radio" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnFourChildsDependant">
                                <div class="formField">
                                    <label for="Safe__c">Safe</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Safe__c}" type="radio" />
                                </div>
                                <div>
                                    <div class="formField">
                                        <label for="Safe_Comments__c">Comments</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Safe_Comments__c}" variant="label-hidden" />
                                    </div>
                                </div>
                            </div>
                            <div class="formField">
                                <label for="Other_Resources_Amenities__c">Other Resources / Amenities</label>
                                <lightning:textarea value="{!v.vendorProperty.Other_Resources_Amenities__c}" class="formTextarea" variant="label-hidden" />
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.savePropertyInRoom}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='propertyOnSite'}">
                    <div class="page-section">
                        <div class="page-header"><h1>On-Site Amenities</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Pool__c">Pool</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Pool__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Pool__c=='Yes'}">
                                        <label for="Pool_Seasonal__c">Seasonal</label>
                                        <lightning:inputField fieldName="Pool_Seasonal__c" value="{!v.vendorProperty.Pool_Seasonal__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Hot_Tub__c">Hot Tub</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hot_Tub__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Hot_Tub__c=='Yes'}">
                                        <label for="Hot_tub_seasonal__c">Seasonal</label>
                                        <lightning:inputField fieldName="Hot_tub_seasonal__c" value="{!v.vendorProperty.Hot_tub_seasonal__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formField">
                                <label for="Fitness_room__c">Fitness Room</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Fitness_room__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Hotel_Shuttle__c">Hotel Shuttle</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hotel_Shuttle__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Airport_Shuttle__c">Airport Shuttle</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesContactNo}" value="{!v.vendorProperty.Airport_Shuttle__c}" type="radio" />
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Hotel_Bars__c">Hotel Bar(s)</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hotel_Bars__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Hotel_Bars__c=='Yes'}">
                                        <label for="hotel_bars_2__c">How Many?</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.hotel_bars_2__c}" step="1" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Hotel_Bars__c=='Yes'}">
                                        <label for="Hotel_bar_hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Hotel_bar_hours__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Restaurants__c">Hotel Restaurant(s)</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Restaurants__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Restaurants__c=='Yes'}">
                                        <label for="Restaurants_2__c">How Many?</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Restaurants_2__c}" step="1" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Restaurants__c=='Yes'}">
                                        <label for="Restaurants_hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Restaurants_hours__c}" maxlength="100" variant="label-hidden" />
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Breakfast__c">Comp Breakfast</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Breakfast__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Breakfast__c=='Yes'}">
                                        <label for="Breakfast_type__c">Type</label>
                                        <lightning:inputField fieldName="Breakfast_type__c" value="{!v.vendorProperty.Breakfast_type__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Room_Service__c">Room Service</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Room_Service__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Room_Service__c=='Yes'}">
                                        <label for="Room_Service_hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Room_Service_hours__c}" maxlength="100" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Managers_Reception__c">Managers Reception</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Managers_Reception__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Managers_Reception__c=='Yes'}">
                                        <label for="Managers_Reception_Hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Managers_Reception_Hours__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formField">
                                    <label for="Self_Parking__c">Self Parking</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.Self_Parking__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Self_Parking__c=='Yes'}">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Self_Parking_Charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Self_Parking_Charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Self_Parking_Charge_Type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Self_Parking_Charge_Type__c" value="{!v.vendorProperty.Self_Parking_Charge_Type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Self_Parking_Add_l_info__c">Additional Info</label>
                                                <lightning:inputField fieldName="Self_Parking_Add_l_info__c" value="{!v.vendorProperty.Self_Parking_Add_l_info__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Self_Parking__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formField">
                                    <label for="Valet_Parking__c">Valet Parking</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.Valet_Parking__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Valet_Parking__c=='Yes'}">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Valet_Parking_Charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Valet_Parking_Charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Valet_Parking_Charge_Type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Valet_Parking_Charge_Type__c" value="{!v.vendorProperty.Valet_Parking_Charge_Type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Valet_Parking_Add_l_info__c">Additional Info</label>
                                                <lightning:inputField fieldName="Valet_Parking_Add_l_info__c" value="{!v.vendorProperty.Valet_Parking_Add_l_info__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Valet_Parking__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formField">
                                    <label for="Coach_Bus_Parking__c">Bus Parking</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.Coach_Bus_Parking__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Coach_Bus_Parking__c=='Yes'}">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Coach_Bus_Charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Coach_Bus_Charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Coach_Bus_Charge_Type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Coach_Bus_Charge_Type__c" value="{!v.vendorProperty.Coach_Bus_Charge_Type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Coach_Bus_Add_l_info__c">Additional Info</label>
                                                <lightning:inputField fieldName="Coach_Bus_Add_l_info__c" value="{!v.vendorProperty.Coach_Bus_Add_l_info__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Coach_Bus_parking_spots__c">Number of parking spots</label>
                                                <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Coach_Bus_parking_spots__c}" step="1" variant="label-hidden" />
                                            </div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Coach_Bus_Parking__c=='Yes'}"><br/></aura:if>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.savePropertyOnSite}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <!-- GROUND PAGES -->
                <aura:if isTrue="{!and(v.menuSelected=='profile',v.userProfile=='GroundVendor')}">
                    <div class="page-section">
                        <div class="page-header"><h1>Basic Info</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="profileForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProfile.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formField">
                                <label for="Name">Company Name<sub class="subLabel"> Call Road Rebel if changes are needed</sub></label>
                                <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Name}" disabled="true" variant="label-hidden" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="ShippingStreet">Address</label>
                                    <lightning:input aura:id="recordField" type="text" placeholder="Enter Address" value="{!v.vendorProfile.ShippingStreet}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <lightning:select aura:id="countryField"
                                                      name="Country"
                                                      value="{!v.vendorProfile.ShippingCountry}"
                                                      label="{!v.countryAndStates.parentFieldLabel}"
                                                      onchange="{!c.handleCountryChange}">
                                        <aura:iteration items="{!v.countries}" var="country">
                                            <option value="{!country}" selected="{!state==v.vendorProfile.ShippingCountry}">{!country}</option>
                                        </aura:iteration>
                                    </lightning:select>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="City__c">City</label>
                                    <lightning:inputField aura:id="recordField" fieldName="City__c" value="{!v.vendorProfile.City__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnTwoChilds" style="padding: 0 0.75em;">
                                    <div class="formField" style="padding-left: 0;">
                                        <lightning:select aura:id="stateField"
                                                          name="State"
                                                          value="{!v.vendorProfile.ShippingState}"
                                                          label="{!v.countryAndStates.childFieldLabel}"
                                                          disabled="{!v.disableState}">
                                            <aura:iteration items="{!v.states}" var="state">
                                                <option value="{!state}" selected="{!state==v.vendorProfile.ShippingState}">{!state}</option>
                                            </aura:iteration>
                                        </lightning:select>
                                    </div>
                                    <div class="formField" style="padding-right: 0;">
                                        <label for="ShippingPostalCode">Zip</label>
                                        <lightning:inputField aura:id="recordField" fieldName="ShippingPostalCode" value="{!v.vendorProfile.ShippingPostalCode}" variant="label-hidden" />
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Phone">Phone</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Phone}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="X24_hr_Emergency_Phone__c">24 Hour Phone</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.X24_hr_Emergency_Phone__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Fax">Fax Number</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Fax}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Website">Website</label>
                                    <lightning:input aura:id="recordField" type="url" value="{!v.vendorProfile.Website}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="website">Service Type</label>
                                    <lightning:inputField aura:id="recordField" fieldName="GT_Vendor_Type__c" value="{!v.vendorProfile.GT_Vendor_Type__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Service_Areas_Cities_and_notes__c">Service Areas - City, State , Country</label>
                                    <lightning:textarea value="{!v.vendorProperty.Service_Areas_Cities_and_notes__c}" class="formTextarea" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div style="padding: 1em;"><b>Credentials</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="DOT__c">DOT #</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.DOT__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="IFTA__c">IFTA #</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.IFTA__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Insurance__c">Insurance</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Insurance__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Associations__c">Associations</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Associations__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorProfile}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='groundCoach'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Fleet Details - Coach</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <div class="tableHeader">
                            <div style="display: flex; flex: 1; padding: 0 !important;">
                                <div style="flex: 1;">Type</div>
                                <div style="width: 4em; text-align: center;">Qty</div>
                                <div style="flex: 1; text-align: center;">Capacity</div>
                            </div>
                            <div style="display: flex; flex: 1; padding: 0 !important;">
                                <div style="flex: 2;">Make / Model</div>
                                <div style="flex: 1;">Year</div>
                                <div style="width: 5em;"></div>
                            </div>
                        </div>
                        <aura:iteration items="{!v.vendorVehicles}" var="vehicle" indexVar="vehicleIndex">
                            <div class="tableRow" style="margin-bottom: 1em;">
                                <div class="tableTitle">
                                    <div style="display: flex; flex: 1;">
                                        <div class="tableCell" style="flex: 1; font-weight: 500;">{!vehicle.vehicleType}</div>
                                        <div class="tableCell" style="flex: none; width: 4em; padding-right: 0; text-align: center;">{!vehicle.quantity}</div>
                                        <div class="tableCell" style="flex: 1; text-align: center; padding-right: 0.75em;">{!vehicle.capacity}</div>
                                    </div>
                                    <div style="display: flex; flex: 1;">
                                        <div class="tableCell" style="flex: 2;">{!if(not(empty(vehicle.otherMake)),vehicle.otherMake+' / '+vehicle.model,vehicle.make+' / '+vehicle.model)}</div>
                                        <div class="tableCell" style="flex: 1;">{!vehicle.year}</div>
                                        <div class="tableButton">
                                            <lightning:buttonIcon iconName="utility:edit" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Edit" value="{!vehicleIndex}" onclick="{!c.handleShowRecord}" />
                                            <lightning:buttonIcon iconName="utility:delete" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Delete" value="{!vehicleIndex}" onclick="{!c.handleShowRemoveVehicle}" />
                                        </div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==vehicleIndex}">
                                    <div style="border-top: 1px solid #dbdbdb; padding: 0.75em; overflow: initial;">
                                        <lightning:recordEditForm aura:id="vehicleForm"
                                                                  objectApiName="Fleet__c"
                                                                  density="comfy">
                                            <lightning:messages />
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Vehicle_Type__c">Type<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:inputField aura:id="recordField" fieldName="Vehicle_Type__c" value="{!v.vendorEditRecord.vehicleType}" variant="label-hidden" required="true" />
                                                </div>
                                                <div class="formColumnTwoChilds">
                                                    <div class="formField">
                                                        <label for="Quantity__c">Qty<abbr class="slds-required" title="required"> *</abbr></label>
                                                        <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.quantity}" variant="label-hidden" required="true" />
                                                    </div>
                                                    <div class="formField">
                                                        <label for="Capacity__c">Capacity<abbr class="slds-required" title="required"> *</abbr></label>
                                                        <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.capacity}" variant="label-hidden" required="true" />
                                                    </div>
                                                </div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formColumnTwoChilds">
                                                    <div class="formField">
                                                        <label for="Make__c">Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                        <lightning:inputField aura:id="recordField" fieldName="Make__c" value="{!v.vendorEditRecord.make}" variant="label-hidden" required="true" />
                                                    </div>
                                                    <div class="formField">
                                                        <aura:if isTrue="{!v.vendorEditRecord.make=='Other'}">
                                                            <label for="Other_make__c">Other Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                            <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.otherMake}" variant="label-hidden" required="true" />
                                                            <aura:set attribute="else">
                                                                <div class="formColumnBlank"></div>
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </div>
                                                <div class="formColumnTwoChilds">
                                                    <div class="formField">
                                                        <label for="Model__c">Model</label>
                                                        <lightning:inputField aura:id="recordField" fieldName="Model__c" value="{!v.vendorEditRecord.model}" variant="label-hidden" />
                                                    </div>
                                                    <div class="formField">
                                                        <label for="Year__c">Year</label>
                                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.year}" variant="label-hidden" />
                                                    </div>
                                                </div>
                                            </div>
                                            <div style="text-align: left;">
                                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorVehicle}" />
                                                <lightning:button type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                                            </div>
                                        </lightning:recordEditForm>
                                    </div>
                                </aura:if>
                            </div>
                        </aura:iteration>
                        <div style="text-align: right;">
                            <lightning:button label="Add Vehicle" variant="brand" class="formButtonBrand" onclick="{!c.handleNewVehicle}" />
                        </div>
                        <br/>
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Available Amenities</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="WiFi_coach__c" class="radioLabel">WiFi</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.WiFi_coach__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.WiFi_coach__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.WiFi_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="DVD__c" class="radioLabel">DVD</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.DVD__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.DVD__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.DVD_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Satellite_TV__c" class="radioLabel">Satelite TV</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Satellite_TV__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Satellite_TV__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Satellite_TV_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Table__c" class="radioLabel">Table</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Table__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Table__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Table_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Trailer_Hitch__c" class="radioLabel">Trailer Hitch</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Trailer_Hitch__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Trailer_Hitch__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Trailer_Hitch_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Trailer__c" class="radioLabel">Trailer</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Trailer__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Trailer__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Trailer_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Restroom__c" class="radioLabel">Restroom</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Restroom__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Restroom__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Restroom_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Outlets_in_Rows__c" class="radioLabel">Outlets in rows</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Outlets_in_Rows__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Outlets_in_Rows__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Outlets_in_Rows_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Outlets_in_Rows__c=='Yes'}">
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsOutlets}" value="{!v.vendorGT.Outlets_position__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Executive_Coach__c" class="radioLabel">Executive Coach</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Executive_Coach__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Executive_Coach__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Executive_Coach_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Executive_Coach__c=='Yes'}">
                                    <div class="formFieldRadio">
                                        <lightning:input type="checkbox" value="{!v.vendorGT.Outlets_position__c}" label="Kitchenette" name="Kitchenettes__c" class="checkboxField" />
                                    </div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Sleepers__c" class="radioLabel">Sleepers</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Sleepers__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Sleepers__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Sleepers_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Sleepers__c=='Yes'}">
                                    <div class="formFieldRadio">
                                        <lightning:checkboxGroup label="" options="{!v.optionsSleepersAmenities}" value="{!v.vendorGT.Sleepers_Amenities__c}" variant="label-hidden" class="checkboxHorizontal" />
                                    </div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveFleetCoach}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='groundChauffeured'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Fleet Details - Chauffeured</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Available Vehicles</b></div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Sedan__c" class="radioLabel">Sedan</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Sedan__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Sedan__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Sedan_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Executive_Sedan__c" class="radioLabel">Executive Sedan</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Executive_Sedan__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Executive_Sedan__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Executive_Sedan_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luxury_Sedan__c" class="radioLabel">Luxury Sedan</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luxury_Sedan__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luxury_Sedan__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luxury_Sedan_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X12_PAX_Van__c" class="radioLabel">12 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X12_PAX_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X12_PAX_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X12_PAX_Van_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X15_PAX_Van__c" class="radioLabel">15 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X15_PAX_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X15_PAX_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X15_PAX_Van_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luggage_Van__c" class="radioLabel">Luggage Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luggage_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luggage_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luggage_Van_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="SUV__c" class="radioLabel">SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.SUV_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Limo__c" class="radioLabel">Limo</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Limo__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Limo__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Limo_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Mini_Coach__c" class="radioLabel">Mini Coach</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Mini_Coach__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Mini_Coach__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Mini_Coach_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <br/>
                            <div style="padding: 1em;"><b>Available Amenities</b></div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Leather_Seats__c" class="radioLabel">Leather seats</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Leather_Seats__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="WiFi_CV__c" class="radioLabel">WiFi</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.WiFi_CV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Meet_Greet_Service__c" class="radioLabel">Meet &amp; Greet services</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Meet_Greet_Service__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="DVD_CV__c" class="radioLabel">DVD</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.DVD_CV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Mini_Bar_CV__c" class="radioLabel">Mini Bar</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Mini_Bar_CV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Airport_Services__c" class="radioLabel">Airport service</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Airport_Services__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveFleetChauffeured}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='groundRental'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Fleet Details - Rental</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Available Vehicles</b></div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Compact__c" class="radioLabel">Compact</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Compact__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Compact__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Compact_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Intermediate__c" class="radioLabel">Intermediate</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Intermediate__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Intermediate__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Intermediate_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Standard__c" class="radioLabel">Standard</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Standard__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Standard__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Standard_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Full_Size__c" class="radioLabel">Full size</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Full_Size__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Full_Size__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Full_Size_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luxury__c" class="radioLabel">Luxury</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luxury__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luxury__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luxury_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Standard_SUV__c" class="radioLabel">Standard SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Standard_SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Standard_SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Standard_SUV_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luxury_SUV__c" class="radioLabel">Luxury SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luxury_SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luxury_SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luxury_SUV_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Mini_Van__c" class="radioLabel">Mini Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Mini_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Mini_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Mini_Van_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X12_PAX_Van_Rental__c" class="radioLabel">12 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X12_PAX_Van_Rental__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X12_PAX_Van_Rental__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X12_PAX_Van_Notes_Rental__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X15_PAX_Van_Rental__c" class="radioLabel">15 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X15_PAX_Van_Rental__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X15_PAX_Van_Rental__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X15_PAX_Van_Notes_Rental__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Hybrid_Car__c" class="radioLabel">Hybrid car</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Hybrid_Car__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Hybrid_Car__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Hybrid_Car_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Hybrid_SUV__c" class="radioLabel">Hybrid SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Hybrid_SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Hybrid_SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Hybrid_SUV_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <br/>
                            <div style="padding: 1em;"><b>Available Options</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Delivery__c" class="radioLabel">Delivery</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Delivery__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Pick_up__c" class="radioLabel">Pick up</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Pick_up__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Direct_Bill__c" class="radioLabel">Direct billing</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Direct_Bill__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Master_Bill_Account_w_Credit_Card__c" class="radioLabel">Master bill account with credit card</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Master_Bill_Account_w_Credit_Card__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <br/>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Age_Requirement_yrs__c">Driver age requirement</label>
                                    <lightning:input aura:id="recordField" type="number" step="1" min="0" max="100" value="{!v.vendorProperty.Age_Requirement_yrs__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formField">
                                <label for="Rental_Insurance_Options__c">Rental insurance options</label>
                                <lightning:input aura:id="recordField" type="text" value="{!v.vendorProperty.Rental_Insurance_Options__c}" variant="label-hidden" />
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveFleetRental}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <!-- GENERAL PAGES -->
                <aura:if isTrue="{!v.menuSelected=='contacts'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Contacts</h1>
                            <lightning:button label="Add New Contact" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNewVendorContact}" />
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <div class="tableHeader" style="padding:0;">
                            <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                <div style="flex: 1; min-width: 0;">Contact</div>
                                <div style="flex: 1; min-width: 0;">Title</div>
                                <div style="flex: 1; min-width: 0;">Phone</div>
                            </div>
                            <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                <div style="flex: 1; min-width: 0;">Mobile</div>
                                <div style="flex: 2; min-width: 0;">Email</div>
                                <div style="width: 4.5rem; text-align: center;"></div>
                            </div>
                        </div>
                        <aura:iteration items="{!v.vendorContacts}" var="contact" indexVar="contactIndex">
                            <div class="tableRow" style="{!contactIndex>0?'margin-top: 1em;':''}">
                                <div class="tableTitle" style="display: flex; flex-direction: row; padding: .25em .75rem!important;">
                                    <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                        <div class="tableCell" style="font-weight: 500;">{!contact.firstName+' '+contact.lastName}</div>
                                        <div class="tableCell">{!contact.title}</div>
                                        <div class="tableCell">{!contact.ext!=''?contact.phone+', ext. '+contact.ext:contact.phone}</div>
                                    </div>
                                    <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                        <div class="tableCell">{!contact.mobile}</div>
                                        <div class="tableCell" style="flex: 2;">{!contact.email}</div>
                                        <div class="tableButton" style="width: 4.5rem; text-align: center;">
                                            <lightning:buttonIcon iconName="utility:edit" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Edit" value="{!contactIndex}" onclick="{!c.handleShowRecord}" />
                                            <lightning:buttonIcon iconName="utility:delete" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Delete" value="{!contactIndex}" onclick="{!c.handleShowRemoveContact}" />
                                        </div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==contactIndex}">
                                    <div style="border-top: 1px solid #dbdbdb; padding: 0.75em;">
                                        <lightning:recordEditForm aura:id="contactForm"
                                                                  objectApiName="Contact"
                                                                  density="comfy">
                                            <lightning:messages />
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="FirstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.firstName}" variant="label-hidden" required="true" />
                                                </div>
                                                <div class="formField">
                                                    <label for="LastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.lastName}" variant="label-hidden" required="true" />
                                                </div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Title">Title</label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.title}" variant="label-hidden" />
                                                </div>
                                                <div class="formColumnBlank"></div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Phone">Phone</label>
                                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.phone}" variant="label-hidden" />
                                                </div>
                                                <div class="formField">
                                                    <label for="Ext">Ext</label>
                                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.ext}" variant="label-hidden" class="extField" />
                                                </div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="MobilePhone">Mobile</label>
                                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.mobile}" variant="label-hidden" />
                                                </div>
                                                <div class="formColumnBlank"></div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="email" value="{!v.vendorEditRecord.email}" variant="label-hidden" required="true" />
                                                </div>
                                                <div class="formColumnBlank"></div>
                                            </div>
                                            <div style="text-align: left;">
                                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorContact}" />
                                                <lightning:button type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                                            </div>
                                        </lightning:recordEditForm>
                                    </div>
                                </aura:if>
                            </div>
                        </aura:iteration>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='payment'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Payment &amp; Cancellation Policy</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Credit Cards Accepted</b></div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="Visa_Accepted__c" class="radioLabel">Visa</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Visa_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Visa_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.Visa_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="Master_Card_Accepted__c" class="radioLabel">Mastercard</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Master_Card_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Master_Card_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.Master_Card_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="American_Express_Accepted__c" class="radioLabel">American Express</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.American_Express_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.American_Express_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.American_Express_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="Discover_Accepted__c" class="radioLabel">Discover Card</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Discover_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Discover_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.Discover_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <br/>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Name">Surcharge negotiable?</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Surcharge_Negotiable__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds"></div>
                            </div>
                            <div style="padding: 1em;"><b>Check Payments</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Check_Payment__c" class="radioLabel">Checks accepted</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Check_Payment__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Wire_Transfer_Bank_Draft__c" class="radioLabel">Wire transfers / Bank drafts</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Wire_Transfer_Bank_Draft__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Bank_Name__c">Bank Name</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorGT.Bank_Name__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="IBAN__c">IBAN #</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorGT.IBAN__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Swift__c">Swift / BIC</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorGT.Swift__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <br/>
                            <div style="padding: 1em;"><b>Check Payments</b></div>
                             <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Other_Payment__c" class="radioLabel">Ohter payments accepted</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Other_Payment__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <aura:if isTrue="{!v.vendorGT.Other_Payment__c=='Yes'}">
                                <div class="formField">
                                    <label for="Other_payment_notes__c">List other payment methods accepted</label>
                                    <lightning:input aura:id="recordField" type="text" maxlength="250" value="{!v.vendorGT.Other_payment_notes__c}" variant="label-hidden" />
                                </div>
                            </aura:if>
                            <br/>
                            <div class="formField">
                                <label for="Payment_policy__c">Payment Policy</label>
                                <lightning:textarea value="{!v.vendorGT.Payment_policy__c}" class="formTextarea" variant="label-hidden" />
                            </div>
                            <div class="formField">
                                <label for="Cancellation_Policy__c">Cancellation Policy</label>
                                <lightning:textarea value="{!v.vendorGT.Cancellation_Policy__c}" class="formTextarea" variant="label-hidden" />
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorPayment}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='privacy'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Privacy</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <c:VoyajerPrivacy />
                    </div>
                </aura:if>
            </div>
            <aura:if isTrue="{!v.openNewContact}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">New Contact</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <lightning:recordEditForm aura:id="contactForm"
                                                      objectApiName="Contact"
                                                      density="comfy">
                                <lightning:messages />
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="FirstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.firstName}" variant="label-hidden" required="true" />
                                    </div>
                                    <div class="formField">
                                        <label for="LastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.lastName}" variant="label-hidden" required="true" />
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Title">Title</label>
                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.title}" variant="label-hidden" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Phone">Phone</label>
                                        <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.phone}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="Ext">Ext</label>
                                        <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.ext}" variant="label-hidden" class="extField" />
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="MobilePhone">Mobile</label>
                                        <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.mobile}" variant="label-hidden" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:input aura:id="recordField" type="email" value="{!v.vendorEditRecord.email}" variant="label-hidden" required="true" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </lightning:recordEditForm>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button aura:id="submitContact" type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorContact}" />
                            <lightning:button aura:id="cancelContact" type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openRemoveContact}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-02" aria-modal="true" aria-describedby="modal-content-id-2" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Delete Contact</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You are about to delete a contact. Are you sure?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="No, Cancel" title="No, Cancel" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Yes, Delete" title="Yes, Delete" variant="brand" class="formButtonBrandLight" onclick="{!c.removeContact}"  />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openNewVehicle}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">New Vehicle</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1" style="overflow: initial;">
                            <lightning:recordEditForm aura:id="vehicleForm"
                                                      objectApiName="Fleet__c"
                                                      density="comfy">
                                <lightning:messages />
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Vehicle_Type__c">Type<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:inputField aura:id="recordField" fieldName="Vehicle_Type__c" value="{!v.vendorEditRecord.vehicleType}" variant="label-hidden" required="true" />
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Quantity__c">Qty<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.quantity}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <label for="Capacity__c">Capacity<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.capacity}" variant="label-hidden" required="true" />
                                        </div>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Make__c">Make<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="Make__c" value="{!v.vendorEditRecord.make}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <aura:if isTrue="{!v.vendorEditRecord.make=='Other'}">
                                                <label for="Other_make__c">Other Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.otherMake}" variant="label-hidden" required="true" />
                                                <aura:set attribute="else">
                                                    <div class="formColumnBlank"></div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Model__c">Model</label>
                                            <lightning:inputField aura:id="recordField" fieldName="Model__c" value="{!v.vendorEditRecord.model}" variant="label-hidden" />
                                        </div>
                                        <div class="formField">
                                            <label for="Year__c">Year</label>
                                            <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.year}" variant="label-hidden" />
                                        </div>
                                    </div>
                                </div>
                            </lightning:recordEditForm>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button aura:id="submitContact" type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorVehicle}" />
                            <lightning:button aura:id="cancelContact" type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openRemoveVehicle}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-02" aria-modal="true" aria-describedby="modal-content-id-2" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Delete Vehicle</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You are about to delete a vehicle. Are you sure?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="No, Cancel" title="No, Cancel" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Yes, Delete" title="Yes, Delete" variant="brand" class="formButtonBrandLight" onclick="{!c.removeVehicle}"  />
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
### VoyajerVendor

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendor

```
.THIS {
}

.THIS .profilePictureContainer {
    text-align: center;
    padding-top: 1em;
}

.THIS .profilePicture {
    width: 5em;
    height: 5em;
    border: 0.25em solid #606060;
}

.THIS .profileName {
    text-align: center;
    padding: 1em 0.5em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .slds-textarea {
    height: 2.75em;
}

.THIS .slds-form-password {
    width: 40%;
    margin: 0 auto;
    min-width: 20em;
}

.THIS .slds-form-password .slds-form-element__label {
    margin-bottom: 0.5em;
    font-weight: 500;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-select_container::before {
    border-bottom: none;
}

.THIS .slds-select_container::after {
    border-top: none;
}

.THIS .slds-select_container .slds-select {
    -webkit-appearance : menuList
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .subLabel {
    font-weight: 400;
    bottom: 0;
}

.THIS .tableHeader {
    display: flex;
    font-weight: 500;
    font-size: 0.75rem;
    padding: 0.25em 0.75rem !important;
    border: 1px solid transparent;
    background-color: transparent;
}

.THIS .tableRow {
    display: flex;
    border: 1px solid #dbdbdb;
    flex-direction: column;
}

.THIS .tableTitle {
    padding: 0.75rem !important;
    display: flex;
    width: 100%;
}

.THIS .tableTitleButton {
    margin: 0 0.25em;
}

.THIS .tableCell {
    flex: 1;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: 0 0.5em;
    min-width: 0;
}

.THIS .tableTitleIcon {
    width: 1.25em;
    height: 1.25em;
}

.THIS .formField,
.THIS .formColumnBlank {
    padding: 0 0.75em;
}

.THIS .extField {
    width: 6em;
}

.THIS .formButtonPadding {
    margin: 0.75em;
}

.THIS .formTextarea textarea {
    min-height: 6em;
}

.THIS .formWeight .slds-form-element__control::after {
    right: 0.2rem;
    content: "LBS";
    position: absolute;
    padding: 0.4rem;
}

.THIS .formWeight .slds-form-element__control input {
    padding-right: 2.25rem;
}

.THIS .formFieldRadio {
    display: flex;
    margin-bottom: .5rem;
    min-width: 0;
    padding: 0 .75em;
}

.THIS .radioLabel {
    align-items: center;
    display:flex;
    flex: 3;
    min-height: 2rem;
}

.THIS .radioHorizontal {
    align-items: center;
    display: flex;
    flex: 2;
}

.THIS .radioHorizontal .slds-form-element__control {
    display: flex;
}

.THIS .checkboxField {
    display: flex;
    align-items: center;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux {
    background-color: black;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux:after {
    border-bottom: 2px solid white;
    border-left: 2px solid white;
}

.THIS .checkboxHorizontal {
    align-items: center;
    display: flex;
    flex: 1;
}

.THIS .checkboxHorizontal > * {
    width: 100%;
}

.THIS .checkboxHorizontal .slds-form-element__control {
    display: flex;
    justify-content: space-between;
}

@media (max-width: 800px) {
    .THIS .profilePicture {
        width: 3.8em;
        height: 3.8em;
        border: 0.175em solid #606060;
    }
}

@media (max-width: 550px) {
    .THIS .profilePicture {
        width: 2em;
        height: 2em;
        border: 0.1em solid #606060;
    }
}
```
### VoyajerVendorController

```
({
	doInit : function(component, event, helper) {
        var userProfile = component.get("v.userProfile");
        component.set("v.vendorProfile",{
            accountId: "",
            RecordTypeId: "",
            Name: "",
            Vendor_Type__c: "",
            ParentId: "",
            Management_Company_lookup__c: "",
            ShippingStreet: "",
            City__c: "",
            ShippingState: "",
            ShippingPostalCode: "",
            ShippingCountry: "",
            Metro_Area__c: "",
            Phone: "",
            X24_hr_Emergency_Phone__c: "",
            Fax: "",
            Website: "",
            GT_Vendor_Type__c: "",
            Service_Areas_Cities_and_notes__c: "",
            DOT__c: "",
            IFTA__c: "",
            Insurance__c: "",
            Associations__c: ""
        });
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorProfile");
        callToParent.fire();
	},
    
    handleCountryChange : function(component, event, helper) {
        var country = event.getSource().get("v.value");
        var countryAndStates = component.get("v.countryAndStates");
        component.set("v.disableState",true);
        var states = [];
        for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
        if(states.length>0) {
            component.set("v.disableState",false);
            component.set("v.states",states);
        } else component.set("v.states",["--- None ---"]);
    },
    
    loadVendorData : function(component, event, helper) {
        var vendorData = component.get("v.vendorData");
        var menuSelected = component.get("v.menuSelected");
        var currentAction = component.get("v.currentAction");
        var message = "";
        console.log(vendorData);
        switch (menuSelected) {
            case "profile":
                var country = vendorData.ShippingCountry;
                var countryAndStates = component.get("v.countryAndStates");
                component.set("v.disableState",true);
                var states = [];
                for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
                if(states.length>0) {
                    component.set("v.disableState",false);
                    component.set("v.states",states);
                } else component.set("v.states",["--- None ---"]);
                component.set("v.vendorProfile",vendorData);
                if(currentAction == "profileOnEdit")message = "Basic Info updated!";
                break;
            case "contacts":
                component.set("v.vendorContacts",vendorData);
                if(currentAction == "contactNew") message = "Contact created!";
                if(currentAction == "contactOnEdit") message = "Contact updated!";
                if(currentAction == "contactRemoved") message = "Contact deleted!";
                break;
            case "payment":
                component.set("v.vendorGT",vendorData);
                if(currentAction == "paymentOnEdit") message = "Payments updated!";
                break;
            case "propertyProfile":
            case "propertyInRoom":
            case "propertyOnSite":
                component.set("v.vendorProperty",vendorData);
                if(currentAction == "propertyOnEdit") message = "Property Profile updated!";
                if(currentAction == "inRoomOnEdit") message = "Property In-Room Amenities updated!";
                if(currentAction == "onSiteOnEdit") message = "Property On-Site Amenities updated!";
                break;
            case "groundCoach":
                if(currentAction == "vehicleNew" || currentAction == "vehicleOnEdit" || currentAction == "vehicleRemoved") {
                    component.set("v.vendorVehicles",vendorData);
                    if(currentAction == "vehicleNew") message = "Vehicle created!";
                    if(currentAction == "vehicleOnEdit") message = "Vehicle updated!";
                    if(currentAction == "vehicleRemoved") message = "Vehicle deleted!";
                }
                if(currentAction == "availableAmenitiesEdit") {
                    component.set("v.vendorGT",vendorData);
                    message = "Amenities updated!";
                }
                if(!currentAction) {
                    component.set("v.vendorVehicles",vendorData.vehicles);
                    component.set("v.vendorGT",vendorData.coach);
                }
                break;
            case "groundChauffeured":
            case "groundRental":
                component.set("v.vendorGT",vendorData);
                if(currentAction == "chauffeuredOnEdit") message = "Fleet Details - Chauffeured updated!";
                break;
            default:
                break;
        }
        if(!!currentAction) {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({ type: "success", title: "", message: message });
            toastEvent.fire();
        }
        component.set("v.recordOpened",-1);
        component.set("v.currentAction","");
        component.set("v.openNewContact",false);
        component.set("v.openRemoveContact",false);
        component.set("v.openNewVehicle",false);
        component.set("v.openRemoveVehicle",false); 
    },
    
    formLoaded : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","contentLoaded");
        callToParent.fire();
	},
    
    loadMenuContent : function(component, event, helper) {
        var menuSelected = event.target.id;
        component.set("v.recordOpened",-1);
        component.set("v.currentAction","");
        if(menuSelected == "profile") component.set("v.showSubMenu",false);
        if(menuSelected == "contacts") component.set("v.showSubMenu",false);
        if(menuSelected == "privacy") component.set("v.showSubMenu",false);
        if(menuSelected == "propertyProfile") component.set("v.showSubMenu",true);
        if(menuSelected == "groundCoach") component.set("v.showSubMenu",true);
        if(menuSelected == "groundPayment") component.set("v.showSubMenu",false);
        component.set("v.menuSelected",menuSelected);
        var callToParent = component.getEvent("callToParent");
        switch (menuSelected) {
            case "profile": callToParent.setParam("action","loadVendorProfile"); break;
            case "contacts": callToParent.setParam("action","loadVendorContacts"); break;
            case "payment": callToParent.setParam("action","loadPayment"); break;
            case "propertyProfile": callToParent.setParam("action","loadPropertyProfile"); break;
            case "propertyInRoom": callToParent.setParam("action","loadPropertyInRoom"); break;
            case "propertyOnSite": callToParent.setParam("action","loadPropertyOnSite"); break;
            case "groundCoach": callToParent.setParam("action","loadFleetCoach"); break;
            case "groundChauffeured": callToParent.setParam("action","loadFleetChauffeured"); break;
            case "groundRental": callToParent.setParam("action","loadFleetRental"); break;
            default: break;
        }
        if(!!callToParent.getParam("action")) callToParent.fire();
    },
    
    saveVendorProfile : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else {
                switch (fieldName) {
                    case "Management_Company_lookup__c":
                    case "City__c":
                        return validSoFar && reportValidity;
                        break;
                    default:
                        return validSoFar;
                        break;
                }
                return validSoFar;
            }
        }, true);
        if(allValid) {
            component.set("v.currentAction","profileOnEdit");
            var userProfile = component.get("v.userProfile");
            var vendorProfile = component.get("v.vendorProfile");
            var callToParent = component.getEvent("callToParent");
            var data = {
                accountId: vendorProfile.accountId,
                ShippingStreet: vendorProfile.ShippingStreet,
                City__c: Array.isArray(vendorProfile.City__c)? '' : vendorProfile.City__c,
                ShippingState: vendorProfile.ShippingState,
                ShippingPostalCode: vendorProfile.ShippingPostalCode,
                ShippingCountry: vendorProfile.ShippingCountry,
                Phone: vendorProfile.Phone,
                Fax: vendorProfile.Fax,
                Website: vendorProfile.Website,
                userProfile: userProfile
            };
            switch (userProfile) {
                case "HousingVendor":
                    data.Vendor_Type__c = vendorProfile.Vendor_Type__c;
                    data.Management_Company_lookup__c = Array.isArray(vendorProfile.Management_Company_lookup__c)? '' : vendorProfile.Management_Company_lookup__c;
                    data.Metro_Area__c = vendorProfile.Metro_Area__c;
                    break;
                case "GroundVendor":
                    data.X24_hr_Emergency_Phone__c = vendorProfile.X24_hr_Emergency_Phone__c;
                    data.GT_Vendor_Type__c = vendorProfile.GT_Vendor_Type__c;
                    data.Service_Areas_Cities_and_notes__c = vendorProfile.Service_Areas_Cities_and_notes__c;
                    data.DOT__c = vendorProfile.DOT__c;
                    data.IFTA__c = vendorProfile.IFTA__c;
                    data.Insurance__c = vendorProfile.Insurance__c;
                    data.Associations__c = vendorProfile.Associations__c;
                    break;
                default:
                    break;
            }
            callToParent.setParam("action","saveVendorProfile");
            callToParent.setParam("data",data);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleShowRecord : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        var recordOpened = component.get("v.recordOpened");
        var records = [];
        var menuSelected = component.get("v.menuSelected");
        if(menuSelected == "contacts") records = component.get("v.vendorContacts");
        if(menuSelected == "groundCoach") records = component.get("v.vendorVehicles");
        var vendorEditRecord = {};
        if(recordOpened !== index) {
            component.set("v.recordOpened",index);
            vendorEditRecord = records[index];
            if(menuSelected == "contacts") component.set("v.currentAction","contactOnEdit");
            if(menuSelected == "groundCoach") component.set("v.currentAction","vehicleOnEdit");
        } else {
            component.set("v.recordOpened",-1);
            component.set("v.currentAction","");
        }
        component.set("v.vendorEditRecord",vendorEditRecord);
    },
    
    handleCloseModal : function(component, event, helper) {
        component.set("v.recordOpened",-1);
        component.set("v.recordToDelete",-1); 
        component.set("v.vendorEditRecord",{});
        component.set("v.currentAction","");
        component.set("v.openNewContact",false);
        component.set("v.openRemoveContact",false);
        component.set("v.openNewVehicle",false);
        component.set("v.openRemoveVehicle",false); 
    },
    
    handleNewVendorContact : function(component, event, helper) {
        component.set("v.openNewContact",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{
            contactId: "",
            firstName: "",
            lastName: "",
            title: "",
            phone: "",
            ext: "",
            mobile: "",
            email: ""
        });
        component.set("v.currentAction","contactNew");
    },
    
    saveVendorContact : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveVendorContact");
            callToParent.setParam("data",component.get("v.vendorEditRecord"));
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleShowRemoveContact : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        component.set("v.recordToDelete",index);
        component.set("v.currentAction","contactRemoved");
        component.set("v.openRemoveContact",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{});
    },
    
    removeContact : function(component, event, helper) {
        var contactId = component.get("v.vendorContacts")[component.get("v.recordToDelete")].contactId;
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","removeContact");
        callToParent.setParam("data",contactId);
        callToParent.fire();
    },
    
    savePropertyProfile : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else {
                switch (fieldName) {
                    default:
                        return validSoFar;
                        break;
                }
                return validSoFar;
            }
        }, true);
        if(allValid) {
            var vendorProperty = JSON.parse(JSON.stringify(component.get("v.vendorProperty")));
            if(vendorProperty.Extended_Stay__c != 'Yes') {
                vendorProperty.Studios__c = 0;
                vendorProperty.Studios_Bed_Size__c = "";
                vendorProperty.Studio_Area__c = "";
                vendorProperty.X1_bedrooms__c = 0;
                vendorProperty.X1_bedroom_bed_size__c = "";
                vendorProperty.X1_bedrooms_Area__c = "";
                vendorProperty.X1_bedrooms_w_Den__c = 0;
                vendorProperty.X1_bedroom_w_Den_bed_size__c = "";
                vendorProperty.X1_bedrooms_w_Den_Area__c = "";
                vendorProperty.X2_bedroom_1_bath__c = 0;
                vendorProperty.X2_bedroom_1_bath_bed_size__c = "";
                vendorProperty.X2_bedroom_1_bath_Area__c = "";
                vendorProperty.X2_bedroom_2_bath__c = 0;
                vendorProperty.X2_bedroom_2_bath_bed_size__c = "";
                vendorProperty.X2_bedroom_2_bath_Area__c = "";
            }
            if(vendorProperty.Porterage_add_l_Info__c.length>0) vendorProperty.Porterage_add_l_Info__c = vendorProperty.Porterage_add_l_Info__c.join(";");
            else vendorProperty.Porterage_add_l_Info__c = "";
            component.set("v.currentAction","propertyOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","savePropertyProfile");
            callToParent.setParam("data",vendorProperty);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    savePropertyInRoom : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        if(allValid) {
            var vendorProperty = JSON.parse(JSON.stringify(component.get("v.vendorProperty")));
            if(vendorProperty.High_Speed_Internet__c != 'Yes') {
                vendorProperty.Connection__c = "";
                vendorProperty.Internet_Charge__c = 0.00;
                vendorProperty.Internet_Charge_Type__c = "";
            }
            if(vendorProperty.Pets_Allowed__c != 'Yes') {
                vendorProperty.Pets_max_LBS__c = 0;
                vendorProperty.Pets_charge__c = 0.00;
                vendorProperty.Pets_charge_type__c = "";
            }
            if(vendorProperty.Refrigerator__c != 'Yes') {
                vendorProperty.Refrigerator_Size__c = "";
                vendorProperty.Refrigerator_charge__c = 0.00;
                vendorProperty.Refrigerator_charge_type__c = "";
                vendorProperty.Refrigerator_Location__c = "";
                vendorProperty.Avail_refrigerators__c = 0;
            }
            if(vendorProperty.Microwave__c != 'Yes') {
                vendorProperty.Microwave_charge__c = 0.00;
                vendorProperty.Microwave_charge_type__c = "";
                vendorProperty.Microwave_Location__c = "";
                vendorProperty.Avail_Microwave__c = 0;
            }
            if(vendorProperty.Oven__c != 'Yes') {
                vendorProperty.Oven_Location__c = "";
            }
            if(vendorProperty.Burners__c != 'Yes') {
                vendorProperty.of_burners__c = "";
                vendorProperty.Burners_location__c = "";
            }
            if(vendorProperty.BathtubOption != 'Yes') {
                vendorProperty.Bathtub__c = "";
            }
            if(vendorProperty.Washer_Dryer__c != 'Yes') {
                vendorProperty.Washer_Dryer_Type__c = "";
            }
            component.set("v.currentAction","inRoomOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","savePropertyInRoom");
            callToParent.setParam("data",vendorProperty);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    savePropertyOnSite : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        if(allValid) {
            var vendorProperty = JSON.parse(JSON.stringify(component.get("v.vendorProperty")));
            if(vendorProperty.Pool__c != 'Yes') vendorProperty.Pool_Seasonal__c = "";
            if(vendorProperty.Hot_Tub__c != 'Yes') vendorProperty.Hot_tub_seasonal__c = "";
            if(vendorProperty.Hotel_Bars__c != 'Yes') {
                vendorProperty.hotel_bars_2__c = 0;
                vendorProperty.Hotel_bar_hours__c = "";
            }
            if(vendorProperty.Restaurants__c != 'Yes') {
                vendorProperty.Restaurants_2__c = 0;
                vendorProperty.Restaurants_hours__c = "";
            }
            if(vendorProperty.Breakfast__c != 'Yes') vendorProperty.Breakfast_type__c = "";
            if(vendorProperty.Room_Service__c != 'Yes') vendorProperty.Room_Service_hours__c = "";
            if(vendorProperty.Managers_Reception__c != 'Yes') vendorProperty.Managers_Reception_Hours__c = "";
            if(vendorProperty.Self_Parking__c != 'Yes') {
                vendorProperty.Self_Parking_Charge__c = 0.00;
                vendorProperty.Self_Parking_Charge_Type__c = "";
                vendorProperty.Self_Parking_Add_l_info__c = "";
            }
            if(vendorProperty.Valet_Parking__c != 'Yes') {
                vendorProperty.Valet_Parking_Charge__c = 0.00;
                vendorProperty.Valet_Parking_Charge_Type__c = "";
                vendorProperty.Valet_Parking_Add_l_info__c = "";
            }
            if(vendorProperty.Coach_Bus_Parking__c != 'Yes') {
                vendorProperty.Coach_Bus_Charge__c = 0.00;
                vendorProperty.Coach_Bus_Charge_Type__c = "";
                vendorProperty.Coach_Bus_Add_l_info__c = "";
                vendorProperty.Coach_Bus_parking_spots__c = 0;
            }
            component.set("v.currentAction","onSiteOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","savePropertyOnSite");
            callToParent.setParam("data",vendorProperty);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleNewVehicle : function(component, event, helper) {
        component.set("v.openNewVehicle",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{
            vehicleId: "",
            vehicleType: "",
            quantity: 0,
            capacity: 0,
            make: "",
            otherMake: "",
            model: "",
            year: ""
        });
        component.set("v.currentAction","vehicleNew");
    },
    
    saveVendorVehicle : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            var value = inputCmp.get("v.value");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else {
                var validate = true;
                switch (fieldName) {
                    case "Vehicle_Type__c":
                    case "Make__c":
                        if(!!value) validate =  true;
                        else validate = false;
                        break;
                    default:
                        break;
                }
                return validSoFar && validate;
            }
        }, true);
        if(allValid) {
            var vendorEditRecord = JSON.parse(JSON.stringify(component.get("v.vendorEditRecord")));
            if(vendorEditRecord.make != "Other") vendorEditRecord.otherMake = "";
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveVendorVehicle");
            callToParent.setParam("data",vendorEditRecord);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleShowRemoveVehicle : function(component, event, helper) {
        var index = parseInt(event.getSource().get("v.value"));
        component.set("v.recordToDelete",index);
        component.set("v.currentAction","vehicleRemoved");
        component.set("v.openRemoveVehicle",true);
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{});
    },
    
    removeVehicle : function(component, event, helper) {
        var vehicleId = component.get("v.vendorVehicles")[component.get("v.recordToDelete")].vehicleId;
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","removeVehicle");
        callToParent.setParam("data",vehicleId);
        callToParent.fire();
    },
    
    saveFleetCoach : function(component, event, helper) {
        component.set("v.recordOpened",-1);
        component.set("v.vendorEditRecord",{});
        component.set("v.currentAction","");
        component.set("v.openNewVehicle",false);
        var allValid = component.find("recordFieldAmenitie").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.WiFi_coach__c != 'Yes') vendorGT.WiFi_Qty__c = 0;
            if(vendorGT.DVD__c != 'Yes') vendorGT.DVD_Qty__c = 0;
            if(vendorGT.Satellite_TV__c != 'Yes') vendorGT.Satellite_TV_Qty__c = 0;
            if(vendorGT.Table__c != 'Yes') vendorGT.Table_Qty__c = 0;
            if(vendorGT.Trailer_Hitch__c != 'Yes') vendorGT.Trailer_Hitch_Qty__c = 0;
            if(vendorGT.Trailer__c != 'Yes') vendorGT.Trailer_Qty__c = 0;
            if(vendorGT.Restroom__c != 'Yes') vendorGT.Restroom_Qty__c = 0;
            if(vendorGT.Outlets_in_Rows__c != 'Yes') {
                vendorGT.Outlets_in_Rows_Qty__c = 0;
                vendorGT.Outlets_position__c = "";
            }
            if(vendorGT.Executive_Coach__c != 'Yes') {
                vendorGT.Executive_Coach_Qty__c = 0;
                vendorGT.Kitchenettes__c = false;
            }
            if(vendorGT.Sleepers__c != 'Yes') vendorGT.Sleepers_Qty__c = 0;
            if(vendorGT.Sleepers__c == 'Yes' && Array.isArray(vendorGT.Sleepers_Amenities__c) && vendorGT.Sleepers_Amenities__c.length>0) vendorGT.Sleepers_Amenities__c = vendorGT.Sleepers_Amenities__c.join(";");
            else vendorGT.Sleepers_Amenities__c = "";
            component.set("v.currentAction","availableAmenitiesEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveFleetCoach");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    saveFleetChauffeured : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.Sedan__c != 'Yes') vendorGT.Sedan_Notes__c = "";
            if(vendorGT.Executive_Sedan__c != 'Yes') vendorGT.Executive_Sedan_Notes__c = "";
            if(vendorGT.Luxury_Sedan__c != 'Yes') vendorGT.Luxury_Sedan_Notes__c = "";
            if(vendorGT.X12_PAX_Van__c != 'Yes') vendorGT.X12_PAX_Van_Notes__c = "";
            if(vendorGT.X15_PAX_Van__c != 'Yes') vendorGT.X15_PAX_Van_Notes__c = "";
            if(vendorGT.Luggage_Van__c != 'Yes') vendorGT.Luggage_Van_Notes__c = "";
            if(vendorGT.SUV__c != 'Yes') vendorGT.SUV_Notes__c = "";
            if(vendorGT.Limo__c != 'Yes') vendorGT.Limo_notes__c = "";
            if(vendorGT.Mini_Coach__c != 'Yes') vendorGT.Mini_Coach_notes__c = "";
            component.set("v.currentAction","chauffeuredOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveFleetChauffeured");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    saveFleetRental : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.Compact__c != 'Yes') vendorGT.Compact_notes__c = "";
            if(vendorGT.Intermediate__c != 'Yes') vendorGT.Intermediate_notes__c = "";
            if(vendorGT.Standard__c != 'Yes') vendorGT.Standard_notes__c = "";
            if(vendorGT.Full_Size__c != 'Yes') vendorGT.Full_Size_notes__c = "";
            if(vendorGT.Luxury__c != 'Yes') vendorGT.Luxury_notes__c = "";
            if(vendorGT.Standard_SUV__c != 'Yes') vendorGT.Standard_SUV_notes__c = "";
            if(vendorGT.Luxury_SUV__c != 'Yes') vendorGT.Luxury_SUV_notes__c = "";
            if(vendorGT.Mini_Van__c != 'Yes') vendorGT.Mini_Van_notes__c = "";
            if(vendorGT.X12_PAX_Van_Rental__c != 'Yes') vendorGT.X12_PAX_Van_Notes_Rental__c = "";
            if(vendorGT.X15_PAX_Van_Rental__c != 'Yes') vendorGT.X15_PAX_Van_Notes_Rental__c = "";
            if(vendorGT.Hybrid_Car__c != 'Yes') vendorGT.Hybrid_Car_notes__c = "";
            if(vendorGT.Hybrid_SUV__c != 'Yes') vendorGT.Hybrid_SUV_notes__c = "";
            component.set("v.currentAction","chauffeuredOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveFleetRental");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    saveVendorPayment : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var vendorGT = JSON.parse(JSON.stringify(component.get("v.vendorGT")));
            if(vendorGT.Visa_Accepted__c != 'Yes') vendorGT.Visa_Surcharge__c = 0.00;
            if(vendorGT.Master_Card_Accepted__c != 'Yes') vendorGT.Master_Card_Surcharge__c = 0.00;
            if(vendorGT.American_Express_Accepted__c != 'Yes') vendorGT.American_Express_Surcharge__c = 0.00;
            if(vendorGT.Discover_Accepted__c != 'Yes') vendorGT.Discover_Surcharge__c = 0.00;
            if(vendorGT.Other_Payment__c != 'Yes') vendorGT.Other_payment_notes__c = "";
            console.log(vendorGT);
            component.set("v.currentAction","paymentOnEdit");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveVendorPayment");
            callToParent.setParam("data",vendorGT);
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    }
})
```
### VoyajerVendorHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerVendor

```
<aura:component >
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="Boolean" name="disableState" default="true" />
    <aura:attribute type="Boolean" name="showSubMenu" default="false" />
    <aura:attribute type="Boolean" name="openNewContact" default="false" />
    <aura:attribute type="Boolean" name="openNewVehicle" default="false" />
    <aura:attribute type="Boolean" name="openRemoveContact" default="false" />
    <aura:attribute type="Boolean" name="openRemoveVehicle" default="false" />
    <aura:attribute type="String" name="menuSelected" default="profile" />
    <aura:attribute type="String" name="userProfile" />
    <aura:attribute type="String" name="currentAction" default="" />
    <aura:attribute type="List" name="vendorContacts" />
    <aura:attribute type="List" name="vendorVehicles" />
    <aura:attribute type="List" name="countries" />
    <aura:attribute type="List" name="states" />
    <aura:attribute type="List" name="optionsYesNo" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'No', 'value': 'No'}]" />
    <aura:attribute type="List" name="optionsYesContactNo" default="[{'label': 'Yes', 'value': 'Yes, contact property for details'},{'label': 'No', 'value': 'No'}]" />
    <aura:attribute type="List" name="optionsYesNoComplimentary" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'Yes/Complimentary', 'value': 'Yes/Complimentary'},{'label': 'No', 'value': 'No'}]" />
    <aura:attribute type="List" name="optionsYesNoContract" default="[{'label': 'Yes', 'value': 'Yes'},{'label': 'No', 'value': 'No'},{'label': 'Yes, Contract property for details', 'value': 'Yes, Contract property for details'}]" />
    <aura:attribute type="List" name="optionsEntry" default="[{'label': 'Both', 'value': 'Both'},{'label': 'Exterior', 'value': 'Exterior'},{'label': 'Interior', 'value': 'Interior'}]" />
    <aura:attribute type="List" name="optionsPorterage" default="[{'label': 'Mandatory', 'value': 'Mandatory'},{'label': 'Available', 'value': 'Available'},{'label': 'Not available', 'value': 'Not available'}]" />
    <aura:attribute type="List" name="optionsPorterageAddInfo" default="[{'label': 'Per bag', 'value': 'Per bag'},{'label': 'Per person', 'value': 'Per person'},{'label': 'RoundTrip', 'value': 'RoundTrip'}]" />
    <aura:attribute type="List" name="optionsOutlets" default="[{'label': 'Every Row', 'value': 'Every Row'},{'label': 'Every Other Row', 'value': 'Every Other Row'}]" />
    <aura:attribute type="List" name="optionsSleepersAmenities" default="[{'label': 'Shower', 'value': 'Shower'},{'label': 'Kitchenettes', 'value': 'Kitchenettes'},{'label': 'Slideout', 'value': 'Slideout'},{'label': 'Restrooms', 'value': 'Restrooms'}]" />
    <aura:attribute type="Object" name="vendorData" />
    <aura:attribute type="Object" name="vendorProfile" />
    <aura:attribute type="Object" name="vendorEditRecord" />
    <aura:attribute type="Object" name="vendorProperty" />
    <aura:attribute type="Object" name="vendorGT" />
    <aura:attribute type="Object" name="countryAndStates" />
    <aura:attribute type="Integer" name="recordOpened" default="-1" />
    <aura:attribute type="Integer" name="recordToDelete" default="-1" />
    <!-- docs -->
    <aura:attribute type="String" name="serviceId" default="a0156000001xchaAAA" />
    <aura:attribute type="List" name="lsDocuments" default="[]" />
	<aura:attribute type="List" name="lsDocumentsAux" default="[]" />
    <!-- end docs -->
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:handler name="change" value="{!v.vendorData}" action="{!c.loadVendorData}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="mainMenu">
            <div class="profilePicName">
                <div class="profilePictureContainer">
                    <lightning:avatar src="{!v.userLogged.FullPhotoUrl}"
                                      onclick="{!c.loadUserContent}"
                                      variant="circle"
                                      initials="{!v.userLogged.Initials__c}"
                                      size="large"
                                      class="profilePicture"
                                      alternativeText="{!v.userLogged.Name}" />
                </div>
                <div class="profileName">
                    <span><b>{!v.userLogged.Name}</b></span>
                </div>
            </div>
            <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page">
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='profile'? ' slds-is-active' : '')}">
                    <a href="javascript:void(0);" id="profile" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Basic Info</a>
                </div>
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='contacts'? ' slds-is-active' : '')}">
                    <a href="javascript:void(0);" id="contacts" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Contacts</a>
                </div>
                <aura:if isTrue="{!or(v.userProfile=='HousingVendor',v.userProfile=='CorporateVendor')}">
                    <div style="{!v.showSubMenu==true?'background: rgba(21, 137, 238, 0.25);':''}">
                        <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='propertyProfile'? ' slds-is-active' : '')}">
                            <a href="javascript:void(0);" id="propertyProfile" class="slds-nav-vertical__action" style="justify-content: space-between;" onclick="{!c.loadMenuContent}">
                                Property Profile <i class="fas fa-chevron-down"></i>
                            </a>
                        </div>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='propertyInRoom'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="propertyInRoom" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">In-Room Amenities</a>
                            </div>
                        </aura:if>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='propertyOnSite'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="propertyOnSite" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">On-Site Amenities</a>
                            </div>
                        </aura:if>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.userProfile=='GroundVendor'}">
                    <div style="{!v.showSubMenu==true?'background: rgba(21, 137, 238, 0.25);':''}">
                        <div class="slds-nav-vertical__item">
                            <a href="javascript:void(0);" id="groundCoach" class="slds-nav-vertical__action" style="justify-content: space-between;" onclick="{!c.loadMenuContent}">
                                Fleet Details <i class="fas fa-chevron-down"  onclick="{!c.loadMenuContent}"></i>
                            </a>
                        </div>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='groundCoach'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="groundCoach" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Coach</a>
                            </div>
                        </aura:if>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='groundChauffeured'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="groundChauffeured" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Chauffeured</a>
                            </div>
                        </aura:if>
                        <aura:if isTrue="{!v.showSubMenu==true}">
                            <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='groundRental'? ' slds-is-active' : '')}">
                                <a href="javascript:void(0);" id="groundRental" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Rental</a>
                            </div>
                        </aura:if>
                    </div>
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='payment'? ' slds-is-active' : '')}">
                        <a href="javascript:void(0);" id="payment" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Payment &amp; Cancellation</a>
                    </div>
                </aura:if>
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='privacy'? ' slds-is-active' : '')}">
                    <a href="javascript:void(0);" id="privacy" class="slds-nav-vertical__action" onclick="{!c.loadMenuContent}">Privacy</a>
                </div>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <!-- HOUSING PAGES -->
                <aura:if isTrue="{!and(v.menuSelected=='profile',or(v.userProfile=='HousingVendor',v.userProfile=='CorporateVendor'))}">
                    <div class="page-section">
                        <div class="page-header"><h1>Basic Info</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="profileForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Name">Property Name<sub class="subLabel"> Call Road Rebel if changes are needed</sub></label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Name}" disabled="true" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Vendor_Type__c">Property Type</label>
                                    <lightning:inputField aura:id="recordField" fieldName="Vendor_Type__c" value="{!v.vendorProfile.Vendor_Type__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="ParentId">Property Chain<sub class="subLabel"> Call Road Rebel if changes are needed</sub></label>
                                    <lightning:inputField aura:id="recordField" fieldName="ParentId" value="{!v.vendorProfile.ParentId}" disabled="true" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="LastName">Management Company</label>
                                    <lightning:inputField aura:id="recordField" fieldName="Management_Company_lookup__c" value="{!v.vendorProfile.Management_Company_lookup__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formField">
                                <label for="ShippingStreet">Street Address</label>
                                <lightning:input aura:id="recordField" type="text" placeholder="Enter Address" value="{!v.vendorProfile.ShippingStreet}" variant="label-hidden" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="City__c">City</label>
                                    <lightning:inputField aura:id="recordField" fieldName="City__c" value="{!v.vendorProfile.City__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnTwoChilds" style="padding: 0 0.75em;">
                                    <div class="formField" style="padding-left: 0;">
                                        <lightning:select aura:id="stateField"
                                                          name="State"
                                                          value="{!v.vendorProfile.ShippingState}"
                                                          label="{!v.countryAndStates.childFieldLabel}"
                                                          disabled="{!v.disableState}">
                                            <aura:iteration items="{!v.states}" var="state">
                                                <option value="{!state}" selected="{!state==v.vendorProfile.ShippingState}">{!state}</option>
                                            </aura:iteration>
                                        </lightning:select>
                                    </div>
                                    <div class="formField" style="padding-right: 0;">
                                        <label for="ShippingPostalCode">Zip</label>
                                        <lightning:inputField aura:id="recordField" fieldName="ShippingPostalCode" value="{!v.vendorProfile.ShippingPostalCode}" variant="label-hidden" />
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <lightning:select aura:id="countryField"
                                                      name="Country"
                                                      value="{!v.vendorProfile.ShippingCountry}"
                                                      label="{!v.countryAndStates.parentFieldLabel}"
                                                      onchange="{!c.handleCountryChange}">
                                        <aura:iteration items="{!v.countries}" var="country">
                                            <option value="{!country}" selected="{!state==v.vendorProfile.ShippingCountry}">{!country}</option>
                                        </aura:iteration>
                                    </lightning:select>
                                </div>
                                <div class="formField">
                                    <label for="Metro_Area__c">Metro Area</label>
                                    <lightning:inputField aura:id="recordField" fieldName="Metro_Area__c" value="{!v.vendorProfile.Metro_Area__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Phone}" required="true" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Fax">Fax Number</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Fax}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Website">Website</label>
                                    <lightning:input aura:id="recordField" type="url" value="{!v.vendorProfile.Website}" variant="label-hidden" required="true" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorProfile}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='propertyProfile'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Property Profile</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Star_Rating__c">Star Rating</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Star_Rating__c}" disabled="true" variant="label-hidden" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnBlank"></div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Check_In_Time__c">Check-In Time</label>
                                    <lightning:input aura:id="recordField" type="time" value="{!v.vendorProperty.Check_In_Time__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Check_out_time__c">Check-Out Time</label>
                                    <lightning:input aura:id="recordField" type="time" value="{!v.vendorProperty.Check_out_time__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <br/>
                            <div class="formField">
                                <label for="X100_Non_Smoking__c">100% Non-Smoking</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.X100_Non_Smoking__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Lift_Elevator__c">Lift/Elevator</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Lift_Elevator__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Property_Entry__c">Property Entry</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsEntry}" value="{!v.vendorProperty.Property_Entry__c}" type="radio" />
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Porterage__c">Porterage</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsPorterage}" value="{!v.vendorProperty.Porterage__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Porterage__c=='Mandatory'}">
                                        <label for="Porterage_Charge__c">Charge</label>
                                        <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Porterage_Charge__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Porterage__c=='Mandatory'}">
                                        <label for="Porterage_add_l_Info__c">Charge Type</label>
                                        <lightning:checkboxGroup label="" options="{!v.optionsPorterageAddInfo}" value="{!v.vendorProperty.Porterage_add_l_Info__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                            </div>
                            <br/>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Number_of_rooms__c">Total Rooms</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Number_of_rooms__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Number_of_suites__c">Total Suites</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Number_of_suites__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Single_Rooms__c">Number of Singles</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Single_Rooms__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Single_Room_Bed_Size__c">Single Room Bed Size</label>
                                    <lightning:inputField fieldName="Single_Room_Bed_Size__c" value="{!v.vendorProperty.Single_Room_Bed_Size__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Single_Room_Area__c">Single Room Size</label>
                                    <lightning:input type="text" value="{!v.vendorProperty.Single_Room_Area__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Double_Rooms__c">Number of Doubles</label>
                                    <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Double_Rooms__c}" step="1" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Double_Room_Bed_Size__c">Double Room Bed Size</label>
                                    <lightning:inputField fieldName="Double_Room_Bed_Size__c" value="{!v.vendorProperty.Double_Room_Bed_Size__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Double_Room_Area__c">Double Room Size</label>
                                    <lightning:input type="text" value="{!v.vendorProperty.Double_Room_Area__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <br/>
                            <div class="formField">
                                <label for="Extended_Stay__c">Do you offer extended stays?</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Extended_Stay__c}" type="radio" />
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Extended_Stay__c=='Yes'}">
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="Studios__c">Number of Studios</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Studios__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="Studios_Bed_Size__c">Studio Room Bed Size</label>
                                        <lightning:inputField fieldName="Studios_Bed_Size__c" value="{!v.vendorProperty.Studios_Bed_Size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="Studio_Area__c">Studio Room Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Studio_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X1_bedrooms__c">Number of 1-Bedrooms</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X1_bedrooms__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedroom_bed_size__c">1-Bedroom Bed Size</label>
                                        <lightning:inputField fieldName="X1_bedroom_bed_size__c" value="{!v.vendorProperty.X1_bedroom_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedrooms_Area__c">1-Bedroom Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X1_bedrooms_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X1_bedrooms_w_Den__c">Number of 1-Bedrooms w/Den</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X1_bedrooms_w_Den__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedroom_w_Den_bed_size__c">1-Bedroom w/Den Bed Size</label>
                                        <lightning:inputField fieldName="X1_bedroom_w_Den_bed_size__c" value="{!v.vendorProperty.X1_bedroom_w_Den_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X1_bedrooms_w_Den_Area__c">1-Bedroom w/Den Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X1_bedrooms_w_Den_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X2_bedroom_1_bath__c">Number of 2-Bedrooms w/ 1-Bath</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X2_bedroom_1_bath__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_1_bath_bed_size__c">2-Bedroom w/ 1-Bath Bed Size</label>
                                        <lightning:inputField fieldName="X2_bedroom_1_bath_bed_size__c" value="{!v.vendorProperty.X2_bedroom_1_bath_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_1_bath_Area__c">2-Bedroom w/ 1-Bath Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X2_bedroom_1_bath_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                                <div class="formColumnThreeChilds">
                                    <div class="formField">
                                        <label for="X2_bedroom_2_bath__c">Number of 2-Bedrooms w/ 2-Bath</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.X2_bedroom_2_bath__c}" step="1" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_2_bath_bed_size__c">2-Bedroom w/ 2-Bath Bed Size</label>
                                        <lightning:inputField fieldName="X2_bedroom_2_bath_bed_size__c" value="{!v.vendorProperty.X2_bedroom_2_bath_bed_size__c}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="X2_bedroom_2_bath_Area__c">2-Bedroom w/ 2-Bath Size</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.X2_bedroom_2_bath_Area__c}" variant="label-hidden" />
                                    </div>
                                </div>
                            </aura:if>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.savePropertyProfile}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='propertyInRoom'}">
                    <div class="page-section">
                        <div class="page-header"><h1>In-Room Amenities</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formField">
                                <label for="Windows_Open__c">Windows Open</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Windows_Open__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Air_conditioning__c">Air Conditioning</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Air_conditioning__c}" type="radio" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="High_Speed_Internet__c">High Speed Internet</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.High_Speed_Internet__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.High_Speed_Internet__c=='Yes'}">
                                            <label for="Connection__c">Type</label>
                                            <lightning:inputField fieldName="Connection__c" value="{!v.vendorProperty.Connection__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.High_Speed_Internet__c=='Yes'}">
                                            <label for="Internet_Charge__c">Charge</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Internet_Charge__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.High_Speed_Internet__c=='Yes'}">
                                            <label for="Internet_Charge_Type__c">Charge Type</label>
                                            <lightning:inputField fieldName="Internet_Charge_Type__c" value="{!v.vendorProperty.Internet_Charge_Type__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField" style="min-width: 0;">
                                        <label for="Pets_Allowed__c">Pets Allowed</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoContract}" value="{!v.vendorProperty.Pets_Allowed__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Pets_Allowed__c=='Yes'}">
                                            <label for="Pets_max_LBS__c">Weight Limit</label>
                                            <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Pets_max_LBS__c}" step="1" class="formWeight" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Pets_Allowed__c=='Yes'}">
                                            <label for="Pets_charge__c">Charge</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Pets_charge__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Pets_Allowed__c=='Yes'}">
                                            <label for="Pets_charge_type__c">Charge Type</label>
                                            <lightning:inputField fieldName="Pets_charge_type__c" value="{!v.vendorProperty.Pets_charge_type__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnFourChildsDependant">
                                <div class="formField">
                                    <label for="Refrigerator__c">Refrigerator</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Refrigerator__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Refrigerator__c=='Yes'}">
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Refrigerator_Size__c">Size</label>
                                                <lightning:inputField fieldName="Refrigerator_Size__c" value="{!v.vendorProperty.Refrigerator_Size__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Refrigerator_charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Refrigerator_charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Refrigerator_charge_type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Refrigerator_charge_type__c" value="{!v.vendorProperty.Refrigerator_charge_type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Refrigerator_Location__c">Location</label>
                                                <lightning:inputField fieldName="Refrigerator_Location__c" value="{!v.vendorProperty.Refrigerator_Location__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Avail_refrigerators__c">Quantity Available</label>
                                                <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Avail_refrigerators__c}" step="1" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Refrigerator__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnFourChildsDependant">
                                <div class="formField">
                                    <label for="Microwave__c">Microwave</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Microwave__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Microwave__c=='Yes'}">
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Microwave_charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Microwave_charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Microwave_charge_type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Microwave_charge_type__c" value="{!v.vendorProperty.Microwave_charge_type__c}" variant="label-hidden" />
                                            </div>
                                             <div class="formColumnBlank"></div>
                                        </div>
                                        <div class="formColumnThreeChilds">
                                            <div class="formField">
                                                <label for="Microwave_Location__c">Location</label>
                                                <lightning:inputField fieldName="Microwave_Location__c" value="{!v.vendorProperty.Microwave_Location__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Avail_Microwave__c">Quantity Available</label>
                                                <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Avail_Microwave__c}" step="1" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Microwave__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Oven__c">Oven</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Oven__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Oven__c=='Yes'}">
                                            <label for="Oven_Location__c">Location</label>
                                            <lightning:inputField fieldName="Oven_Location__c" value="{!v.vendorProperty.Oven_Location__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Burners__c">Burners</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Burners__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Burners__c=='Yes'}">
                                            <label for="of_burners__c"># of Burners</label>
                                            <lightning:inputField fieldName="of_burners__c" value="{!v.vendorProperty.of_burners__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Burners__c=='Yes'}">
                                            <label for="Burners_location__c">Location</label>
                                            <lightning:inputField fieldName="Burners_location__c" value="{!v.vendorProperty.Burners_location__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </div>
                            <div class="formField">
                                <label for="Coffee_Maker__c">Coffee Maker</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Coffee_Maker__c}" type="radio" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="BathtubOption">Bathtub</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.BathtubOption}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.BathtubOption=='Yes'}">
                                            <label for="Bathtub__c">Location <abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="Bathtub__c" value="{!v.vendorProperty.Bathtub__c}" variant="label-hidden" required="true" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Washer_Dryer__c">Washer / Dryer</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Washer_Dryer__c}" type="radio" />
                                    </div>
                                    <div class="formField">
                                        <aura:if isTrue="{!v.vendorProperty.Washer_Dryer__c=='Yes'}">
                                            <label for="Washer_Dryer_Type__c">Type</label>
                                            <lightning:inputField fieldName="Washer_Dryer_Type__c" value="{!v.vendorProperty.Washer_Dryer_Type__c}" variant="label-hidden" />
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Hairdryers__c">Hair Dryerr</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hairdryers__c}" type="radio" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnFourChildsDependant">
                                <div class="formField">
                                    <label for="Safe__c">Safe</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Safe__c}" type="radio" />
                                </div>
                                <div>
                                    <div class="formField">
                                        <label for="Safe_Comments__c">Comments</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Safe_Comments__c}" variant="label-hidden" />
                                    </div>
                                </div>
                            </div>
                            <div class="formField">
                                <label for="Other_Resources_Amenities__c">Other Resources / Amenities</label>
                                <lightning:textarea value="{!v.vendorProperty.Other_Resources_Amenities__c}" class="formTextarea" variant="label-hidden" />
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.savePropertyInRoom}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='propertyOnSite'}">
                    <div class="page-section">
                        <div class="page-header"><h1>On-Site Amenities</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProperty.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Pool__c">Pool</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Pool__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Pool__c=='Yes'}">
                                        <label for="Pool_Seasonal__c">Seasonal</label>
                                        <lightning:inputField fieldName="Pool_Seasonal__c" value="{!v.vendorProperty.Pool_Seasonal__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Hot_Tub__c">Hot Tub</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hot_Tub__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Hot_Tub__c=='Yes'}">
                                        <label for="Hot_tub_seasonal__c">Seasonal</label>
                                        <lightning:inputField fieldName="Hot_tub_seasonal__c" value="{!v.vendorProperty.Hot_tub_seasonal__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formField">
                                <label for="Fitness_room__c">Fitness Room</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Fitness_room__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Hotel_Shuttle__c">Hotel Shuttle</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hotel_Shuttle__c}" type="radio" />
                            </div>
                            <div class="formField">
                                <label for="Airport_Shuttle__c">Airport Shuttle</label>
                                <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesContactNo}" value="{!v.vendorProperty.Airport_Shuttle__c}" type="radio" />
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Hotel_Bars__c">Hotel Bar(s)</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Hotel_Bars__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Hotel_Bars__c=='Yes'}">
                                        <label for="hotel_bars_2__c">How Many?</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.hotel_bars_2__c}" step="1" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Hotel_Bars__c=='Yes'}">
                                        <label for="Hotel_bar_hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Hotel_bar_hours__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Restaurants__c">Hotel Restaurant(s)</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Restaurants__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Restaurants__c=='Yes'}">
                                        <label for="Restaurants_2__c">How Many?</label>
                                        <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Restaurants_2__c}" step="1" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Restaurants__c=='Yes'}">
                                        <label for="Restaurants_hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Restaurants_hours__c}" maxlength="100" variant="label-hidden" />
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Breakfast__c">Comp Breakfast</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Breakfast__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Breakfast__c=='Yes'}">
                                        <label for="Breakfast_type__c">Type</label>
                                        <lightning:inputField fieldName="Breakfast_type__c" value="{!v.vendorProperty.Breakfast_type__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Room_Service__c">Room Service</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Room_Service__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Room_Service__c=='Yes'}">
                                        <label for="Room_Service_hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Room_Service_hours__c}" maxlength="100" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Managers_Reception__c">Managers Reception</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorProperty.Managers_Reception__c}" type="radio" />
                                </div>
                                <div class="formField">
                                    <aura:if isTrue="{!v.vendorProperty.Managers_Reception__c=='Yes'}">
                                        <label for="Managers_Reception_Hours__c">Hours</label>
                                        <lightning:input type="text" value="{!v.vendorProperty.Managers_Reception_Hours__c}" variant="label-hidden" />
                                    </aura:if>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formField">
                                    <label for="Self_Parking__c">Self Parking</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.Self_Parking__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Self_Parking__c=='Yes'}">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Self_Parking_Charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Self_Parking_Charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Self_Parking_Charge_Type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Self_Parking_Charge_Type__c" value="{!v.vendorProperty.Self_Parking_Charge_Type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Self_Parking_Add_l_info__c">Additional Info</label>
                                                <lightning:inputField fieldName="Self_Parking_Add_l_info__c" value="{!v.vendorProperty.Self_Parking_Add_l_info__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Self_Parking__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formField">
                                    <label for="Valet_Parking__c">Valet Parking</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.Valet_Parking__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Valet_Parking__c=='Yes'}">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Valet_Parking_Charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Valet_Parking_Charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Valet_Parking_Charge_Type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Valet_Parking_Charge_Type__c" value="{!v.vendorProperty.Valet_Parking_Charge_Type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Valet_Parking_Add_l_info__c">Additional Info</label>
                                                <lightning:inputField fieldName="Valet_Parking_Add_l_info__c" value="{!v.vendorProperty.Valet_Parking_Add_l_info__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formColumnBlank"></div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Valet_Parking__c=='Yes'}"><br/></aura:if>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formField">
                                    <label for="Coach_Bus_Parking__c">Bus Parking</label>
                                    <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNoComplimentary}" value="{!v.vendorProperty.Coach_Bus_Parking__c}" type="radio" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorProperty.Coach_Bus_Parking__c=='Yes'}">
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Coach_Bus_Charge__c">Charge</label>
                                                <lightning:input aura:id="recordField" type="number" formatter="currency" step="0.01" value="{!v.vendorProperty.Coach_Bus_Charge__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Coach_Bus_Charge_Type__c">Charge Type</label>
                                                <lightning:inputField fieldName="Coach_Bus_Charge_Type__c" value="{!v.vendorProperty.Coach_Bus_Charge_Type__c}" variant="label-hidden" />
                                            </div>
                                        </div>
                                        <div class="formColumnTwoChilds">
                                            <div class="formField">
                                                <label for="Coach_Bus_Add_l_info__c">Additional Info</label>
                                                <lightning:inputField fieldName="Coach_Bus_Add_l_info__c" value="{!v.vendorProperty.Coach_Bus_Add_l_info__c}" variant="label-hidden" />
                                            </div>
                                            <div class="formField">
                                                <label for="Coach_Bus_parking_spots__c">Number of parking spots</label>
                                                <lightning:input aura:id="recordField" type="number" value="{!v.vendorProperty.Coach_Bus_parking_spots__c}" step="1" variant="label-hidden" />
                                            </div>
                                        </div>
                                    </aura:if>
                                </div>
                            </div>
                            <aura:if isTrue="{!v.vendorProperty.Coach_Bus_Parking__c=='Yes'}"><br/></aura:if>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.savePropertyOnSite}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <!-- GROUND PAGES -->
                <aura:if isTrue="{!and(v.menuSelected=='profile',v.userProfile=='GroundVendor')}">
                    <div class="page-section">
                        <div class="page-header"><h1>Basic Info</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="profileForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorProfile.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formField">
                                <label for="Name">Company Name<sub class="subLabel"> Call Road Rebel if changes are needed</sub></label>
                                <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Name}" disabled="true" variant="label-hidden" />
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="ShippingStreet">Address</label>
                                    <lightning:input aura:id="recordField" type="text" placeholder="Enter Address" value="{!v.vendorProfile.ShippingStreet}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <lightning:select aura:id="countryField"
                                                      name="Country"
                                                      value="{!v.vendorProfile.ShippingCountry}"
                                                      label="{!v.countryAndStates.parentFieldLabel}"
                                                      onchange="{!c.handleCountryChange}">
                                        <aura:iteration items="{!v.countries}" var="country">
                                            <option value="{!country}" selected="{!state==v.vendorProfile.ShippingCountry}">{!country}</option>
                                        </aura:iteration>
                                    </lightning:select>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="City__c">City</label>
                                    <lightning:inputField aura:id="recordField" fieldName="City__c" value="{!v.vendorProfile.City__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnTwoChilds" style="padding: 0 0.75em;">
                                    <div class="formField" style="padding-left: 0;">
                                        <lightning:select aura:id="stateField"
                                                          name="State"
                                                          value="{!v.vendorProfile.ShippingState}"
                                                          label="{!v.countryAndStates.childFieldLabel}"
                                                          disabled="{!v.disableState}">
                                            <aura:iteration items="{!v.states}" var="state">
                                                <option value="{!state}" selected="{!state==v.vendorProfile.ShippingState}">{!state}</option>
                                            </aura:iteration>
                                        </lightning:select>
                                    </div>
                                    <div class="formField" style="padding-right: 0;">
                                        <label for="ShippingPostalCode">Zip</label>
                                        <lightning:inputField aura:id="recordField" fieldName="ShippingPostalCode" value="{!v.vendorProfile.ShippingPostalCode}" variant="label-hidden" />
                                    </div>
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Phone">Phone</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Phone}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="X24_hr_Emergency_Phone__c">24 Hour Phone</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.X24_hr_Emergency_Phone__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Fax">Fax Number</label>
                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorProfile.Fax}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Website">Website</label>
                                    <lightning:input aura:id="recordField" type="url" value="{!v.vendorProfile.Website}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="website">Service Type</label>
                                    <lightning:inputField aura:id="recordField" fieldName="GT_Vendor_Type__c" value="{!v.vendorProfile.GT_Vendor_Type__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Service_Areas_Cities_and_notes__c">Service Areas - City, State , Country</label>
                                    <lightning:textarea value="{!v.vendorProperty.Service_Areas_Cities_and_notes__c}" class="formTextarea" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div style="padding: 1em;"><b>Credentials</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="DOT__c">DOT #</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.DOT__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="IFTA__c">IFTA #</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.IFTA__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Insurance__c">Insurance</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Insurance__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Associations__c">Associations</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorProfile.Associations__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorProfile}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='groundCoach'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Fleet Details - Coach</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <div class="tableHeader">
                            <div style="display: flex; flex: 1; padding: 0 !important;">
                                <div style="flex: 1;">Type</div>
                                <div style="width: 4em; text-align: center;">Qty</div>
                                <div style="flex: 1; text-align: center;">Capacity</div>
                            </div>
                            <div style="display: flex; flex: 1; padding: 0 !important;">
                                <div style="flex: 2;">Make / Model</div>
                                <div style="flex: 1;">Year</div>
                                <div style="width: 5em;"></div>
                            </div>
                        </div>
                        <aura:iteration items="{!v.vendorVehicles}" var="vehicle" indexVar="vehicleIndex">
                            <div class="tableRow" style="margin-bottom: 1em;">
                                <div class="tableTitle">
                                    <div style="display: flex; flex: 1;">
                                        <div class="tableCell" style="flex: 1; font-weight: 500;">{!vehicle.vehicleType}</div>
                                        <div class="tableCell" style="flex: none; width: 4em; padding-right: 0; text-align: center;">{!vehicle.quantity}</div>
                                        <div class="tableCell" style="flex: 1; text-align: center; padding-right: 0.75em;">{!vehicle.capacity}</div>
                                    </div>
                                    <div style="display: flex; flex: 1;">
                                        <div class="tableCell" style="flex: 2;">{!if(not(empty(vehicle.otherMake)),vehicle.otherMake+' / '+vehicle.model,vehicle.make+' / '+vehicle.model)}</div>
                                        <div class="tableCell" style="flex: 1;">{!vehicle.year}</div>
                                        <div class="tableButton">
                                            <lightning:buttonIcon iconName="utility:edit" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Edit" value="{!vehicleIndex}" onclick="{!c.handleShowRecord}" />
                                            <lightning:buttonIcon iconName="utility:delete" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Delete" value="{!vehicleIndex}" onclick="{!c.handleShowRemoveVehicle}" />
                                        </div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==vehicleIndex}">
                                    <div style="border-top: 1px solid #dbdbdb; padding: 0.75em; overflow: initial;">
                                        <lightning:recordEditForm aura:id="vehicleForm"
                                                                  objectApiName="Fleet__c"
                                                                  density="comfy">
                                            <lightning:messages />
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Vehicle_Type__c">Type<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:inputField aura:id="recordField" fieldName="Vehicle_Type__c" value="{!v.vendorEditRecord.vehicleType}" variant="label-hidden" required="true" />
                                                </div>
                                                <div class="formColumnTwoChilds">
                                                    <div class="formField">
                                                        <label for="Quantity__c">Qty<abbr class="slds-required" title="required"> *</abbr></label>
                                                        <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.quantity}" variant="label-hidden" required="true" />
                                                    </div>
                                                    <div class="formField">
                                                        <label for="Capacity__c">Capacity<abbr class="slds-required" title="required"> *</abbr></label>
                                                        <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.capacity}" variant="label-hidden" required="true" />
                                                    </div>
                                                </div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formColumnTwoChilds">
                                                    <div class="formField">
                                                        <label for="Make__c">Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                        <lightning:inputField aura:id="recordField" fieldName="Make__c" value="{!v.vendorEditRecord.make}" variant="label-hidden" required="true" />
                                                    </div>
                                                    <div class="formField">
                                                        <aura:if isTrue="{!v.vendorEditRecord.make=='Other'}">
                                                            <label for="Other_make__c">Other Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                            <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.otherMake}" variant="label-hidden" required="true" />
                                                            <aura:set attribute="else">
                                                                <div class="formColumnBlank"></div>
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </div>
                                                <div class="formColumnTwoChilds">
                                                    <div class="formField">
                                                        <label for="Model__c">Model</label>
                                                        <lightning:inputField aura:id="recordField" fieldName="Model__c" value="{!v.vendorEditRecord.model}" variant="label-hidden" />
                                                    </div>
                                                    <div class="formField">
                                                        <label for="Year__c">Year</label>
                                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.year}" variant="label-hidden" />
                                                    </div>
                                                </div>
                                            </div>
                                            <div style="text-align: left;">
                                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorVehicle}" />
                                                <lightning:button type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                                            </div>
                                        </lightning:recordEditForm>
                                    </div>
                                </aura:if>
                            </div>
                        </aura:iteration>
                        <div style="text-align: right;">
                            <lightning:button label="Add Vehicle" variant="brand" class="formButtonBrand" onclick="{!c.handleNewVehicle}" />
                        </div>
                        <br/>
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Available Amenities</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="WiFi_coach__c" class="radioLabel">WiFi</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.WiFi_coach__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.WiFi_coach__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.WiFi_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="DVD__c" class="radioLabel">DVD</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.DVD__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.DVD__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.DVD_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Satellite_TV__c" class="radioLabel">Satelite TV</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Satellite_TV__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Satellite_TV__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Satellite_TV_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Table__c" class="radioLabel">Table</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Table__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Table__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Table_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Trailer_Hitch__c" class="radioLabel">Trailer Hitch</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Trailer_Hitch__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Trailer_Hitch__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Trailer_Hitch_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Trailer__c" class="radioLabel">Trailer</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Trailer__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Trailer__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Trailer_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Restroom__c" class="radioLabel">Restroom</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Restroom__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Restroom__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Restroom_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Outlets_in_Rows__c" class="radioLabel">Outlets in rows</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Outlets_in_Rows__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Outlets_in_Rows__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Outlets_in_Rows_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Outlets_in_Rows__c=='Yes'}">
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsOutlets}" value="{!v.vendorGT.Outlets_position__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Executive_Coach__c" class="radioLabel">Executive Coach</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Executive_Coach__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Executive_Coach__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Executive_Coach_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Executive_Coach__c=='Yes'}">
                                    <div class="formFieldRadio">
                                        <lightning:input type="checkbox" value="{!v.vendorGT.Outlets_position__c}" label="Kitchenette" name="Kitchenettes__c" class="checkboxField" />
                                    </div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnThreeChilds">
                                    <div class="formFieldRadio">
                                        <label for="Sleepers__c" class="radioLabel">Sleepers</label>
                                    </div>
                                    <div class="formFieldRadio">
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Sleepers__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.vendorGT.Sleepers__c=='Yes'}">
                                            <div class="formField"><lightning:input aura:id="recordFieldAmenitie" type="number" min="1" placeholder="Enter Qty" value="{!v.vendorGT.Sleepers_Qty__c}" variant="label-hidden" /></div>
                                            <aura:set attribute="else">
                                                <div class="formColumnBlank"></div>
                                            </aura:set>
                                        </aura:if>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Sleepers__c=='Yes'}">
                                    <div class="formFieldRadio">
                                        <lightning:checkboxGroup label="" options="{!v.optionsSleepersAmenities}" value="{!v.vendorGT.Sleepers_Amenities__c}" variant="label-hidden" class="checkboxHorizontal" />
                                    </div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveFleetCoach}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='groundChauffeured'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Fleet Details - Chauffeured</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Available Vehicles</b></div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Sedan__c" class="radioLabel">Sedan</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Sedan__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Sedan__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Sedan_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Executive_Sedan__c" class="radioLabel">Executive Sedan</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Executive_Sedan__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Executive_Sedan__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Executive_Sedan_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luxury_Sedan__c" class="radioLabel">Luxury Sedan</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luxury_Sedan__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luxury_Sedan__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luxury_Sedan_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X12_PAX_Van__c" class="radioLabel">12 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X12_PAX_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X12_PAX_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X12_PAX_Van_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X15_PAX_Van__c" class="radioLabel">15 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X15_PAX_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X15_PAX_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X15_PAX_Van_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luggage_Van__c" class="radioLabel">Luggage Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luggage_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luggage_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luggage_Van_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="SUV__c" class="radioLabel">SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.SUV_Notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Limo__c" class="radioLabel">Limo</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Limo__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Limo__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Limo_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Mini_Coach__c" class="radioLabel">Mini Coach</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Mini_Coach__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Mini_Coach__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Mini_Coach_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <br/>
                            <div style="padding: 1em;"><b>Available Amenities</b></div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Leather_Seats__c" class="radioLabel">Leather seats</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Leather_Seats__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="WiFi_CV__c" class="radioLabel">WiFi</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.WiFi_CV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Meet_Greet_Service__c" class="radioLabel">Meet &amp; Greet services</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Meet_Greet_Service__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="DVD_CV__c" class="radioLabel">DVD</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.DVD_CV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Mini_Bar_CV__c" class="radioLabel">Mini Bar</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Mini_Bar_CV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Airport_Services__c" class="radioLabel">Airport service</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Airport_Services__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveFleetChauffeured}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='groundRental'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Fleet Details - Rental</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Available Vehicles</b></div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Compact__c" class="radioLabel">Compact</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Compact__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Compact__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Compact_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Intermediate__c" class="radioLabel">Intermediate</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Intermediate__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Intermediate__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Intermediate_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Standard__c" class="radioLabel">Standard</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Standard__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Standard__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Standard_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Full_Size__c" class="radioLabel">Full size</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Full_Size__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Full_Size__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Full_Size_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luxury__c" class="radioLabel">Luxury</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luxury__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luxury__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luxury_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Standard_SUV__c" class="radioLabel">Standard SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Standard_SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Standard_SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Standard_SUV_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Luxury_SUV__c" class="radioLabel">Luxury SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Luxury_SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Luxury_SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Luxury_SUV_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Mini_Van__c" class="radioLabel">Mini Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Mini_Van__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Mini_Van__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Mini_Van_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X12_PAX_Van_Rental__c" class="radioLabel">12 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X12_PAX_Van_Rental__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X12_PAX_Van_Rental__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X12_PAX_Van_Notes_Rental__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="X15_PAX_Van_Rental__c" class="radioLabel">15 PAX Van</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.X15_PAX_Van_Rental__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.X15_PAX_Van_Rental__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.X15_PAX_Van_Notes_Rental__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Hybrid_Car__c" class="radioLabel">Hybrid car</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Hybrid_Car__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Hybrid_Car__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Hybrid_Car_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="formColumnThreeChildsDependant">
                                <div class="formFieldRadio">
                                    <label for="Hybrid_SUV__c" class="radioLabel">Hybrid SUV</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Hybrid_SUV__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div>
                                    <aura:if isTrue="{!v.vendorGT.Hybrid_SUV__c=='Yes'}">
                                        <div class="formField"><lightning:input aura:id="recordField" type="text" maxlength="250" placeholder="Make / Model" value="{!v.vendorGT.Hybrid_SUV_notes__c}" variant="label-hidden" /></div>
                                    </aura:if>
                                </div>
                            </div>
                            <br/>
                            <div style="padding: 1em;"><b>Available Options</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Delivery__c" class="radioLabel">Delivery</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Delivery__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Pick_up__c" class="radioLabel">Pick up</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Pick_up__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Direct_Bill__c" class="radioLabel">Direct billing</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Direct_Bill__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Master_Bill_Account_w_Credit_Card__c" class="radioLabel">Master bill account with credit card</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Master_Bill_Account_w_Credit_Card__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div><div class="formColumnBlank"></div></div>
                            </div>
                            <br/>
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="Age_Requirement_yrs__c">Driver age requirement</label>
                                    <lightning:input aura:id="recordField" type="number" step="1" min="0" max="100" value="{!v.vendorProperty.Age_Requirement_yrs__c}" variant="label-hidden" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formField">
                                <label for="Rental_Insurance_Options__c">Rental insurance options</label>
                                <lightning:input aura:id="recordField" type="text" value="{!v.vendorProperty.Rental_Insurance_Options__c}" variant="label-hidden" />
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveFleetRental}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <!-- GENERAL PAGES -->
                <aura:if isTrue="{!v.menuSelected=='contacts'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Contacts</h1>
                            <lightning:button label="Add New Contact" variant="brand" class="formButtonBrandLight" onclick="{!c.handleNewVendorContact}" />
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <div class="tableHeader" style="padding:0;">
                            <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                <div style="flex: 1; min-width: 0;">Contact</div>
                                <div style="flex: 1; min-width: 0;">Title</div>
                                <div style="flex: 1; min-width: 0;">Phone</div>
                            </div>
                            <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                <div style="flex: 1; min-width: 0;">Mobile</div>
                                <div style="flex: 2; min-width: 0;">Email</div>
                                <div style="width: 4.5rem; text-align: center;"></div>
                            </div>
                        </div>
                        <aura:iteration items="{!v.vendorContacts}" var="contact" indexVar="contactIndex">
                            <div class="tableRow" style="{!contactIndex>0?'margin-top: 1em;':''}">
                                <div class="tableTitle" style="display: flex; flex-direction: row; padding: .25em .75rem!important;">
                                    <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                        <div class="tableCell" style="font-weight: 500;">{!contact.firstName+' '+contact.lastName}</div>
                                        <div class="tableCell">{!contact.title}</div>
                                        <div class="tableCell">{!contact.ext!=''?contact.phone+', ext. '+contact.ext:contact.phone}</div>
                                    </div>
                                    <div class="tableRow" style="border: 0; flex-direction: row; display: flex; padding: 0;">
                                        <div class="tableCell">{!contact.mobile}</div>
                                        <div class="tableCell" style="flex: 2;">{!contact.email}</div>
                                        <div class="tableButton" style="width: 4.5rem; text-align: center;">
                                            <lightning:buttonIcon iconName="utility:edit" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Edit" value="{!contactIndex}" onclick="{!c.handleShowRecord}" />
                                            <lightning:buttonIcon iconName="utility:delete" size="medium" class="tableTitleButton" iconClass="tableTitleIcon" variant="bare" alternativeText="Delete" value="{!contactIndex}" onclick="{!c.handleShowRemoveContact}" />
                                        </div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.recordOpened==contactIndex}">
                                    <div style="border-top: 1px solid #dbdbdb; padding: 0.75em;">
                                        <lightning:recordEditForm aura:id="contactForm"
                                                                  objectApiName="Contact"
                                                                  density="comfy">
                                            <lightning:messages />
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="FirstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.firstName}" variant="label-hidden" required="true" />
                                                </div>
                                                <div class="formField">
                                                    <label for="LastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.lastName}" variant="label-hidden" required="true" />
                                                </div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Title">Title</label>
                                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.title}" variant="label-hidden" />
                                                </div>
                                                <div class="formColumnBlank"></div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Phone">Phone</label>
                                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.phone}" variant="label-hidden" />
                                                </div>
                                                <div class="formField">
                                                    <label for="Ext">Ext</label>
                                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.ext}" variant="label-hidden" class="extField" />
                                                </div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="MobilePhone">Mobile</label>
                                                    <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.mobile}" variant="label-hidden" />
                                                </div>
                                                <div class="formColumnBlank"></div>
                                            </div>
                                            <div class="formColumnTwoChilds">
                                                <div class="formField">
                                                    <label for="Email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                                    <lightning:input aura:id="recordField" type="email" value="{!v.vendorEditRecord.email}" variant="label-hidden" required="true" />
                                                </div>
                                                <div class="formColumnBlank"></div>
                                            </div>
                                            <div style="text-align: left;">
                                                <lightning:button type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorContact}" />
                                                <lightning:button type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                                            </div>
                                        </lightning:recordEditForm>
                                    </div>
                                </aura:if>
                            </div>
                        </aura:iteration>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='payment'}">
                    <div class="page-section">
                        <div class="page-header">
                            <h1>Payment &amp; Cancellation Policy</h1>
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <lightning:recordEditForm aura:id="propertyForm"
                                                  objectApiName="Account"
                                                  recordTypeId="{!v.vendorGT.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div style="padding: 1em;"><b>Credit Cards Accepted</b></div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="Visa_Accepted__c" class="radioLabel">Visa</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Visa_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Visa_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.Visa_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="Master_Card_Accepted__c" class="radioLabel">Mastercard</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Master_Card_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Master_Card_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.Master_Card_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="American_Express_Accepted__c" class="radioLabel">American Express</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.American_Express_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.American_Express_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.American_Express_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formFieldRadio">
                                    <label for="Discover_Accepted__c" class="radioLabel">Discover Card</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Discover_Accepted__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <aura:if isTrue="{!v.vendorGT.Discover_Accepted__c=='Yes'}">
                                    <div class="formField"><lightning:input aura:id="recordField" type="number" formatter="percent-fixed" min="0.01" step="0.01" placeholder="Surcharge (%)" value="{!v.vendorGT.Discover_Surcharge__c}" variant="label-hidden" /></div>
                                    <aura:set attribute="else">
                                        <div class="formColumnBlank"></div>
                                    </aura:set>
                                </aura:if>
                                <div class="formColumnBlank"></div>
                            </div>
                            <br/>
                            <div class="formColumnTwoChilds">
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Name">Surcharge negotiable?</label>
                                        <lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Surcharge_Negotiable__c}" type="radio" class="radioHorizontal" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds"></div>
                            </div>
                            <div style="padding: 1em;"><b>Check Payments</b></div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Check_Payment__c" class="radioLabel">Checks accepted</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Check_Payment__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Wire_Transfer_Bank_Draft__c" class="radioLabel">Wire transfers / Bank drafts</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Wire_Transfer_Bank_Draft__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="Bank_Name__c">Bank Name</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorGT.Bank_Name__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="IBAN__c">IBAN #</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorGT.IBAN__c}" variant="label-hidden" />
                                </div>
                                <div class="formField">
                                    <label for="Swift__c">Swift / BIC</label>
                                    <lightning:input aura:id="recordField" type="text" value="{!v.vendorGT.Swift__c}" variant="label-hidden" />
                                </div>
                            </div>
                            <br/>
                            <div style="padding: 1em;"><b>Check Payments</b></div>
                             <div class="formColumnTwoChilds">
                                <div class="formFieldRadio">
                                    <label for="Other_Payment__c" class="radioLabel">Ohter payments accepted</label><lightning:radioGroup label="" variant="label-hidden" options="{!v.optionsYesNo}" value="{!v.vendorGT.Other_Payment__c}" type="radio" class="radioHorizontal" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <aura:if isTrue="{!v.vendorGT.Other_Payment__c=='Yes'}">
                                <div class="formField">
                                    <label for="Other_payment_notes__c">List other payment methods accepted</label>
                                    <lightning:input aura:id="recordField" type="text" maxlength="250" value="{!v.vendorGT.Other_payment_notes__c}" variant="label-hidden" />
                                </div>
                            </aura:if>
                            <br/>
                            <div class="formField">
                                <label for="Payment_policy__c">Payment Policy</label>
                                <lightning:textarea value="{!v.vendorGT.Payment_policy__c}" class="formTextarea" variant="label-hidden" />
                            </div>
                            <div class="formField">
                                <label for="Cancellation_Policy__c">Cancellation Policy</label>
                                <lightning:textarea value="{!v.vendorGT.Cancellation_Policy__c}" class="formTextarea" variant="label-hidden" />
                            </div>
                            <div style="text-align: right;">
                                <lightning:button type="button" variant="brand" label="Update" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorPayment}" />
                            </div>
                        </lightning:recordEditForm>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='privacy'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Privacy</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <c:VoyajerPrivacy />
                    </div>
                </aura:if>
            </div>
            <aura:if isTrue="{!v.openNewContact}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">New Contact</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <lightning:recordEditForm aura:id="contactForm"
                                                      objectApiName="Contact"
                                                      density="comfy">
                                <lightning:messages />
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="FirstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.firstName}" variant="label-hidden" required="true" />
                                    </div>
                                    <div class="formField">
                                        <label for="LastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.lastName}" variant="label-hidden" required="true" />
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Title">Title</label>
                                        <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.title}" variant="label-hidden" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Phone">Phone</label>
                                        <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.phone}" variant="label-hidden" />
                                    </div>
                                    <div class="formField">
                                        <label for="Ext">Ext</label>
                                        <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.ext}" variant="label-hidden" class="extField" />
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="MobilePhone">Mobile</label>
                                        <lightning:input aura:id="recordField" type="tel" value="{!v.vendorEditRecord.mobile}" variant="label-hidden" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:input aura:id="recordField" type="email" value="{!v.vendorEditRecord.email}" variant="label-hidden" required="true" />
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </lightning:recordEditForm>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button aura:id="submitContact" type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorContact}" />
                            <lightning:button aura:id="cancelContact" type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openRemoveContact}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-02" aria-modal="true" aria-describedby="modal-content-id-2" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Delete Contact</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You are about to delete a contact. Are you sure?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="No, Cancel" title="No, Cancel" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Yes, Delete" title="Yes, Delete" variant="brand" class="formButtonBrandLight" onclick="{!c.removeContact}"  />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openNewVehicle}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">New Vehicle</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1" style="overflow: initial;">
                            <lightning:recordEditForm aura:id="vehicleForm"
                                                      objectApiName="Fleet__c"
                                                      density="comfy">
                                <lightning:messages />
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <label for="Vehicle_Type__c">Type<abbr class="slds-required" title="required"> *</abbr></label>
                                        <lightning:inputField aura:id="recordField" fieldName="Vehicle_Type__c" value="{!v.vendorEditRecord.vehicleType}" variant="label-hidden" required="true" />
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Quantity__c">Qty<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.quantity}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <label for="Capacity__c">Capacity<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" step="1" min="0" value="{!v.vendorEditRecord.capacity}" variant="label-hidden" required="true" />
                                        </div>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Make__c">Make<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="Make__c" value="{!v.vendorEditRecord.make}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <aura:if isTrue="{!v.vendorEditRecord.make=='Other'}">
                                                <label for="Other_make__c">Other Make<abbr class="slds-required" title="required"> *</abbr></label>
                                                <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.otherMake}" variant="label-hidden" required="true" />
                                                <aura:set attribute="else">
                                                    <div class="formColumnBlank"></div>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Model__c">Model</label>
                                            <lightning:inputField aura:id="recordField" fieldName="Model__c" value="{!v.vendorEditRecord.model}" variant="label-hidden" />
                                        </div>
                                        <div class="formField">
                                            <label for="Year__c">Year</label>
                                            <lightning:input aura:id="recordField" type="text" value="{!v.vendorEditRecord.year}" variant="label-hidden" />
                                        </div>
                                    </div>
                                </div>
                            </lightning:recordEditForm>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button aura:id="submitContact" type="button" variant="brand" label="Save" class="formButtonBrand formButtonPadding" onclick="{!c.saveVendorVehicle}" />
                            <lightning:button aura:id="cancelContact" type="button" label="Cancel" class="formButtonPadding" onclick="{!c.handleCloseModal}" />
                        </footer>
                    </div>
                </section>
                <div class="slds-backdrop slds-backdrop_open"></div>
                <!--###### MODAL BOX Part END Here ######-->
            </aura:if>
            <aura:if isTrue="{!v.openRemoveVehicle}">
                <!--###### MODAL BOX Start######--> 
                <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-02" aria-modal="true" aria-describedby="modal-content-id-2" class="slds-modal slds-fade-in-open">
                    <div class="slds-modal__container">
                        <!-- ###### MODAL BOX HEADER Start ######-->
                        <header class="slds-modal__header">
                            <!--<lightning:buttonIcon iconName="utility:close" alternativeText="close" variant="bare-inverse" class="slds-modal__close" onclick="{!c.handleCloseModal}" />-->
                            <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Delete Vehicle</h2>
                        </header>
                        <!--###### MODAL BOX BODY Part Start######-->
                        <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                            <p>You are about to delete a vehicle. Are you sure?</p>
                        </div>
                        <!--###### MODAL BOX FOOTER Part Start ######-->
                        <footer class="slds-modal__footer">
                            <lightning:button label="No, Cancel" title="No, Cancel" variant="neutral" onclick="{!c.handleCloseModal}" />
                            <lightning:button label="Yes, Delete" title="Yes, Delete" variant="brand" class="formButtonBrandLight" onclick="{!c.removeVehicle}"  />
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
### VoyajerVendor

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendor

```
.THIS {
}

.THIS .profilePictureContainer {
    text-align: center;
    padding-top: 1em;
}

.THIS .profilePicture {
    width: 5em;
    height: 5em;
    border: 0.25em solid #606060;
}

.THIS .profileName {
    text-align: center;
    padding: 1em 0.5em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .slds-textarea {
    height: 2.75em;
}

.THIS .slds-form-password {
    width: 40%;
    margin: 0 auto;
    min-width: 20em;
}

.THIS .slds-form-password .slds-form-element__label {
    margin-bottom: 0.5em;
    font-weight: 500;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-select_container::before {
    border-bottom: none;
}

.THIS .slds-select_container::after {
    border-top: none;
}

.THIS .slds-select_container .slds-select {
    -webkit-appearance : menuList
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .subLabel {
    font-weight: 400;
    bottom: 0;
}

.THIS .tableHeader {
    display: flex;
    font-weight: 500;
    font-size: 0.75rem;
    padding: 0.25em 0.75rem !important;
    border: 1px solid transparent;
    background-color: transparent;
}

.THIS .tableRow {
    display: flex;
    border: 1px solid #dbdbdb;
    flex-direction: column;
}

.THIS .tableTitle {
    padding: 0.75rem !important;
    display: flex;
    width: 100%;
}

.THIS .tableTitleButton {
    margin: 0 0.25em;
}

.THIS .tableCell {
    flex: 1;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
    padding: 0 0.5em;
    min-width: 0;
}

.THIS .tableTitleIcon {
    width: 1.25em;
    height: 1.25em;
}

.THIS .formField,
.THIS .formColumnBlank {
    padding: 0 0.75em;
}

.THIS .extField {
    width: 6em;
}

.THIS .formButtonPadding {
    margin: 0.75em;
}

.THIS .formTextarea textarea {
    min-height: 6em;
}

.THIS .formWeight .slds-form-element__control::after {
    right: 0.2rem;
    content: "LBS";
    position: absolute;
    padding: 0.4rem;
}

.THIS .formWeight .slds-form-element__control input {
    padding-right: 2.25rem;
}

.THIS .formFieldRadio {
    display: flex;
    margin-bottom: .5rem;
    min-width: 0;
    padding: 0 .75em;
}

.THIS .radioLabel {
    align-items: center;
    display:flex;
    flex: 3;
    min-height: 2rem;
}

.THIS .radioHorizontal {
    align-items: center;
    display: flex;
    flex: 2;
}

.THIS .radioHorizontal .slds-form-element__control {
    display: flex;
}

.THIS .checkboxField {
    display: flex;
    align-items: center;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux {
    background-color: black;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux:after {
    border-bottom: 2px solid white;
    border-left: 2px solid white;
}

.THIS .checkboxHorizontal {
    align-items: center;
    display: flex;
    flex: 1;
}

.THIS .checkboxHorizontal > * {
    width: 100%;
}

.THIS .checkboxHorizontal .slds-form-element__control {
    display: flex;
    justify-content: space-between;
}

@media (max-width: 800px) {
    .THIS .profilePicture {
        width: 3.8em;
        height: 3.8em;
        border: 0.175em solid #606060;
    }
}

@media (max-width: 550px) {
    .THIS .profilePicture {
        width: 2em;
        height: 2em;
        border: 0.1em solid #606060;
    }
}
```

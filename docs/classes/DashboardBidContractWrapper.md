---
layout: default
title: DashboardBidContractWrapper
parent: classes
---

```global class DashboardBidContractWrapper implements Comparable {
    public static String orderFieldBidContract {get;set;}
    public static String orderOrientationBidContract {get;set;}
    public Air__c airTrip {get;set;}
    public Ground__c gtTrip {get;set;}
    public Freight__c freightTrip {get;set;}
    public Id bidId {get;set;}
    public String bidName {get;set;}
    public Id parentId {get;set;}
    public Date startDate {get;set;}
    public Date endDate {get;set;}
    public String vendor {get;set;}
    public Id vendorId {get;set;}
    public String groupName {get;set;}
    public String status {get;set;}
    //Housing fields
    public String venue {get;set;}
    public Id venueId {get;set;}
    public String city {get;set;}
    public Id cityId {get;set;}
    //GT fields
    public String description {get;set;}
    public String serviceType {get;set;}
    //Air fields
    public String dep_arr {get;set;}
    public String rt_dep_arr {get;set;}
    public String trip_type {get;set;}
    public String pax {get;set;}
    
    public DashboardBidContractWrapper(Id bidId, String bidName, String vendor, Id vendorId, String status){
        this.bidId = bidId;
        this.bidName = bidName;
        this.vendor = vendor;
        this.vendorId = vendorId;
        this.status = status;
    }

    public DashboardBidContractWrapper(Ground__c gtTrip, Id bidId, String bidName, String vendor, Id vendorId, String status){
        this.gtTrip = gtTrip;
        this.bidId = bidId;
        this.bidName = bidName;
        this.vendor = vendor;
        this.vendorId = vendorId;
        this.status = status;
    }

    public DashboardBidContractWrapper(Freight__c freightTrip, Id bidId, String bidName, String vendor, Id vendorId, String status){
        this.freightTrip = freightTrip;
        this.bidId = bidId;
        this.bidName = bidName;
        this.vendor = vendor;
        this.vendorId = vendorId;
        this.status = status;
    }

    public DashboardBidContractWrapper(Air__c airTrip, Id bidId, String bidName, String vendor, Id vendorId, String status){
        this.airTrip = airTrip;
        this.bidId = bidId;
        this.bidName = bidName;
        this.vendor = vendor;
        this.vendorId = vendorId;
        this.status = status;
    }

    public void setHousingFields(Id parentId, Date startDate, Date endDate, String venue, String city, String groupName) {
        this.parentId = parentId;
        this.startDate = startDate;
        this.endDate = endDate;
        this.venue = venue;
        this.city = city;
        this.groupName = groupName;
    }
    
    public void setGroundFields(Id parentId, Date startDate, Date endDate, String groupName, String description, String serviceType) {
        this.parentId = parentId;
        this.startDate = startDate;
        this.endDate = endDate;
        this.groupName = groupName;
        this.description = description;
        this.serviceType = serviceType;
    }
    
    public void setFreightFields(Id parentId, Date startDate, Date endDate, String groupName, String description, String serviceType) {
        this.parentId = parentId;
        this.startDate = startDate;
        this.endDate = endDate;
        this.groupName = groupName;
        this.description = description;
        this.serviceType = serviceType;
    }
    
    public void setAirFields(Id parentId, Date startDate, String dep_arr, Date endDate, String rt_dep_arr, String trip_type, String pax) {
        this.parentId = parentId;
        this.startDate = startDate;
        this.dep_arr = dep_arr;
        this.endDate = endDate;
        this.rt_dep_arr = rt_dep_arr;
        this.trip_type = trip_type;
        this.pax = pax;
    }
    
    public Integer compareTo(Object obj) {
        DashboardBidContractWrapper data = (DashboardBidContractWrapper) obj;
        switch on orderFieldBidContract {
            when 'startDate' { return sortByStartDate(data); }
            when 'dep_arr' { return sortByDepArr(data); }
            when 'endDate' { return sortByEndDate(data); }
            when 'rt_dep_arr' { return sortByRtDepArr(data); }
            when 'vendor' { return sortByVendor(data); }
            when 'groupName' { return sortByGroupName(data); }
            when 'status' { return sortByStatus(data); }
            when 'venue' { return sortByVenue(data);}
            when 'city' { return sortByCity(data); }
            when 'serviceType' { return sortByService(data); }
            when 'trip_type' { return sortByTripType(data); }
            when 'pax' { return sortByPax(data); }
            when else { return 0; }
        }
    }
    
    private Integer sortByStartDate(DashboardBidContractWrapper data) {
        if (this.startDate == data.startDate) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.startDate > data.startDate) || (orderOrientationBidContract == 'DESC' && this.startDate < data.startDate)) return 1;
        else return -1;
    }
    private Integer sortByDepArr(DashboardBidContractWrapper data) {
        if(orderOrientationBidContract == 'ASC'){
            if (this.dep_arr > data.dep_arr) return 1;
        }else{
            if (this.dep_arr < data.dep_arr) return 1;
        }
        if (this.dep_arr == data.dep_arr) return 0;
        
        return -1;
    }
    private Integer sortByEndDate(DashboardBidContractWrapper data) {
        if (this.endDate == data.endDate) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.endDate > data.endDate) || (orderOrientationBidContract == 'DESC' && this.endDate < data.endDate)) return 1;
        else return -1;
    }
    private Integer sortByRtDepArr(DashboardBidContractWrapper data) {
        if(orderOrientationBidContract == 'ASC'){
            if (this.rt_dep_arr > data.rt_dep_arr) return 1;
        }else{
            if (this.rt_dep_arr < data.rt_dep_arr) return 1;
        }
        if (this.rt_dep_arr == data.rt_dep_arr) return 0;
        
        return -1;
    }
    private Integer sortByVendor(DashboardBidContractWrapper data) {
        if (this.vendor == data.vendor) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.vendor > data.vendor) || (orderOrientationBidContract == 'DESC' && this.vendor < data.vendor)) return 1;
        else return -1;
    }
    private Integer sortByGroupName(DashboardBidContractWrapper data) {
        if (this.groupName == data.groupName) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.groupName > data.groupName) || (orderOrientationBidContract == 'DESC' && this.groupName < data.groupName)) return 1;
        else return -1;
    }
    private Integer sortByStatus(DashboardBidContractWrapper data) {
        if (this.status == data.status) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.status > data.status) || (orderOrientationBidContract == 'DESC' && this.status < data.status)) return 1;
        else return -1;
    }
    private Integer sortByVenue(DashboardBidContractWrapper data) {
        if (this.venue == data.venue) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.venue > data.venue) || (orderOrientationBidContract == 'DESC' && this.venue < data.venue)) return 1;
        else return -1;
    }
    private Integer sortByCity(DashboardBidContractWrapper data) {
        if (this.city == data.city) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.city > data.city) || (orderOrientationBidContract == 'DESC' && this.city < data.city)) return 1;
        else return -1;
    }
    private Integer sortByService(DashboardBidContractWrapper data) {
        if (this.serviceType == data.serviceType) return 0;
        else if((orderOrientationBidContract == 'ASC' && this.serviceType > data.serviceType) || (orderOrientationBidContract == 'DESC' && this.serviceType < data.serviceType)) return 1;
        else return -1;
    }
    private Integer sortByTripType(DashboardBidContractWrapper data) {
        if(orderOrientationBidContract == 'ASC'){
            if (this.trip_type > data.trip_type) return 1;
        }else{
            if (this.trip_type < data.trip_type) return 1;
        }
        if (this.trip_type == data.trip_type) return 0;
        
        return -1;
    }
    private Integer sortByPax(DashboardBidContractWrapper data) {
        if(orderOrientationBidContract == 'ASC'){
            if (this.pax > data.pax) return 1;
        }else{
            if (this.pax < data.pax) return 1;
        }
        if (this.pax == data.pax) return 0;
        
        return -1;
    }
}```

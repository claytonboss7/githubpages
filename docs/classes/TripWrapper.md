---
layout: default
title: TripWrapper
parent: classes
---

```global class TripWrapper implements Comparable{
    public static String orderFieldTrip {get;set;}
    public static String orderOrientationTrip {get;set;}
    public Ground__c g {get;set;}
    public Freight__c f {get;set;}
    public Air__c a {get;set;}
    public Date start_date {get;set;}
    public Date end_date {get;set;}
    public String description {get;set;}
    public String service_type {get;set;}
    public String vendor {get;set;}
    public String groupz {get;set;}
    public String status {get;set;}
    public Date deadline_date {get;set;}
    public Date departure_date {get;set;}
    public String dep_arr {get;set;}
    public Date return_date {get;set;}
    public String rt_dep_arr {get;set;}
    public String trip_type {get;set;}
    public String pax {get;set;}
    public Date decision_due_date {get;set;}
    public String baggage {get;set;}
    
    public TripWrapper(Ground__c vg, Date vstart_date, Date vend_date, String vdescription, String vservice_type, String vvendor, String vgroupz, String vstatus, Date vdeadline_date){
        g = vg;
        start_date = vstart_date;
        end_date = vend_date;
        description = vdescription;
        service_type = vservice_type;
        vendor = vvendor;
        groupz = vgroupz;
        status = vstatus;
        deadline_date = vdeadline_date;
    }
    public TripWrapper(Freight__c vf, Date vstart_date, Date vend_date, String vdescription, String vservice_type, String vvendor, String vgroupz, String vstatus, Date vdeadline_date){
        f = vf;
        start_date = vstart_date;
        end_date = vend_date;
        description = vdescription;
        service_type = vservice_type;
        vendor = vvendor;
        groupz = vgroupz;
        status = vstatus;
        deadline_date = vdeadline_date;
    }
    public TripWrapper(Air__c va, Date vdeparture_date, String vdep_arr, Date vreturn_date, String vrt_dep_arr, String vtrip_type, String vvendor, String vpax, Date vdecision_due_date, String vstatus, String vbaggage){
        a = va;
        departure_date = vdeparture_date;
        dep_arr = vdep_arr;
        return_date = vreturn_date;
        rt_dep_arr = vrt_dep_arr;
        trip_type = vtrip_type;
        vendor = vvendor;
        pax = vpax;
        decision_due_date = vdecision_due_date;
        status = vstatus;
        baggage = vbaggage;
    }
    
    public Integer compareTo(Object obj) {
        TripWrapper data = (TripWrapper)obj;
        if (orderFieldTrip == 'start_date') return sortByStartDate(data);
        if (orderFieldTrip == 'end_date') return sortByEndDate(data);
        if (orderFieldTrip == 'description') return sortByDescription(data);
        if (orderFieldTrip == 'service_type') return sortByServiceType(data);
        if (orderFieldTrip == 'vendor') return sortByVendor(data);
        if (orderFieldTrip == 'group') return sortByGroup(data);
        if (orderFieldTrip == 'status') return sortByStatus(data);
        if (orderFieldTrip == 'deadline_date') return sortByDeadlineDate(data);
        if (orderFieldTrip == 'departure_date') return sortByDepartureDate(data);
        if (orderFieldTrip == 'dep_arr') return sortByDepArr(data);
        if (orderFieldTrip == 'return_date') return sortByReturnDate(data);
        if (orderFieldTrip == 'rt_dep_arr') return sortByRtDepArr(data);
        if (orderFieldTrip == 'trip_type') return sortByTripType(data);
        if (orderFieldTrip == 'pax') return sortByPax(data);
        if (orderFieldTrip == 'decision_due_date') return sortByDecisionDueDate(data);
        if (orderFieldTrip == 'baggage') return sortByBaggage(data);
        return 0;
    }
    private Integer sortByBaggage(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.baggage > data.baggage) return 1;
        }else{
            if (this.baggage < data.baggage) return 1;
        }
        if (this.baggage == data.baggage) return 0;
        
        return -1;
    }
    private Integer sortByDecisionDueDate(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.decision_due_date > data.decision_due_date) return 1;
        }else{
            if (this.decision_due_date < data.decision_due_date) return 1;
        }
        if (this.decision_due_date == data.decision_due_date) return 0;
        
        return -1;
    }
    private Integer sortByPax(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.pax > data.pax) return 1;
        }else{
            if (this.pax < data.pax) return 1;
        }
        if (this.pax == data.pax) return 0;
        
        return -1;
    }
    private Integer sortByTripType(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.trip_type > data.trip_type) return 1;
        }else{
            if (this.trip_type < data.trip_type) return 1;
        }
        if (this.trip_type == data.trip_type) return 0;
        
        return -1;
    }
    private Integer sortByRtDepArr(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.rt_dep_arr > data.rt_dep_arr) return 1;
        }else{
            if (this.rt_dep_arr < data.rt_dep_arr) return 1;
        }
        if (this.rt_dep_arr == data.rt_dep_arr) return 0;
        
        return -1;
    }
    private Integer sortByReturnDate(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.return_date > data.return_date) return 1;
        }else{
            if (this.return_date < data.return_date) return 1;
        }
        if (this.return_date == data.return_date) return 0;
        if (this.return_date == null) return 1;
        if (data.return_date == null) return -1;
        return -1;
    }
    private Integer sortByDepArr(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.dep_arr > data.dep_arr) return 1;
        }else{
            if (this.dep_arr < data.dep_arr) return 1;
        }
        if (this.dep_arr == data.dep_arr) return 0;
        
        return -1;
    }
    private Integer sortByDepartureDate(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.departure_date > data.departure_date) return 1;
        }else{
            if (this.departure_date < data.departure_date) return 1;
        }
        if (this.departure_date == data.departure_date) return 0;
        if (this.departure_date == null) return 1;
        if (data.departure_date == null) return -1;
        return -1;
    }
    private Integer sortByStartDate(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.start_date > data.start_date) return 1;
        }else{
            if (this.start_date < data.start_date) return 1;
        }
        if (this.start_date == data.start_date) return 0;
        
        return -1;
    }
    private Integer sortByEndDate(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.end_date > data.end_date) return 1;
        }else{
            if (this.end_date < data.end_date) return 1;
        }
        if (this.end_date == data.end_date) return 0;
        
        return -1;
    }
    private Integer sortByDescription(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.description > data.description) return 1;
        }else{
            if (this.description < data.description) return 1;
        }
        if (this.description == data.description) return 0;
        
        return -1;
    }
    private Integer sortByServiceType(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.service_type > data.service_type) return 1;
        }else{
            if (this.service_type < data.service_type) return 1;
        }
        if (this.service_type == data.service_type) return 0;
        
        return -1;
    }
    private Integer sortByVendor(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.vendor > data.vendor) return 1;
        }else{
            if (this.vendor < data.vendor) return 1;
        }
        if (this.vendor == data.vendor) return 0;
        
        return -1;
    }
    private Integer sortByGroup(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.groupz > data.groupz) return 1;
        }else{
            if (this.groupz < data.groupz) return 1;
        }
        if (this.groupz == data.groupz) return 0;
        
        return -1;
    }
    private Integer sortByStatus(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.status > data.status) return 1;
        }else{
            if (this.status < data.status) return 1;
        }
        if (this.status == data.status) return 0;
        
        return -1;
    }
    private Integer sortByDeadlineDate(TripWrapper data) {
        if(orderOrientationTrip == 'ASC'){ if (this.deadline_date > data.deadline_date) return 1;
        }else{
            if (this.deadline_date < data.deadline_date) return 1;
        }
        if (this.deadline_date == data.deadline_date) return 0;
        
        return -1;
    }
}```

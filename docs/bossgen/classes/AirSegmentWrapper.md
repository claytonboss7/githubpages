---
layout: default
title: AirSegmentWrapper
parent: classes
---
# Metadata Type
classes


# Filename 
AirSegmentWrapper


# Raw XML
```
global class AirSegmentWrapper implements Comparable{
    public static String orderField {get;set;}
    public static String orderOrientation {get;set;}
    public Air__c air {get;set;}
    public String departure_cityid {get;set;}
    public String departure_city {get;set;}
    public String arrival_cityid {get;set;}
    public String arrival_city {get;set;}
    public Date departure_date {get;set;}
    
    public AirSegmentWrapper(Air__c vair, Date vdeparture_date){
        air = vair;
        departure_date = vdeparture_date;
    }
    
    public AirSegmentWrapper(Air__c vair, String vdeparture_cityid, String vdeparture_city, String varrival_cityid, String varrival_city){
        air = vair;
        departure_cityid = vdeparture_cityid;
        departure_city = vdeparture_city;
        arrival_cityid = varrival_cityid;
        arrival_city = varrival_city;
    }
    
    public Integer compareTo(Object obj) {
        AirSegmentWrapper data = (AirSegmentWrapper)obj;
        if (orderField == 'date') return sortByDate(data);
        return 0;
    }
    
    private Integer sortByDate(AirSegmentWrapper data) {
        if(orderOrientation == 'ASC'){
            if (this.departure_date > data.departure_date) return 1;
        }else{
            if (this.departure_date < data.departure_date) return 1;
        }
        if (this.departure_date == data.departure_date) return 0;
        
        return -1;
    }
}
```


# Last Modified


# Usage

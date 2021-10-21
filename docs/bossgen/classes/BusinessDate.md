---
layout: default
title: BusinessDate
parent: classes
---
# Metadata Type
classes


# Filename 
BusinessDate


# Raw XML
```
public class BusinessDate {
    
    public static Date AddBusinessDays(Date startDate, Integer BusinessDaysToAdd) {
        Date finalDate = startDate;
        Integer direction = BusinessDaysToAdd < 0? -1 : 1;
        String locale = UserInfo.getLocale();
        System.debug(locale);
        while(BusinessDaysToAdd != 0) {
            finalDate = finalDate.addDays(direction);
            if(!IsWeekendDay(finalDate,locale)) BusinessDaysToAdd -= direction;
        }
        if(finalDate < Date.today()) finalDate = Date.today();
        if(IsWeekendDay(finalDate,locale)) finalDate = AddBusinessDays(finalDate,1);
        System.debug(finalDate);
        return finalDate;
    }
    
    private static Boolean IsWeekendDay(Date datePropose, String locale) {
        Date startOfWeek = datePropose.toStartOfWeek();
        if(Datetime.newInstance(startOfWeek, Time.newInstance(0,0,0,0)).format('u').equals('1')) startOfWeek = startOfWeek.addDays(-1);
        else if(Datetime.newInstance(startOfWeek, Time.newInstance(0,0,0,0)).format('u').equals('6')) startOfWeek = startOfWeek.addDays(-6);
        System.debug(startOfWeek);
        Integer dayOfWeek = startOfWeek.daysBetween(datePropose);
        return ((dayOfWeek == 0 || dayOfWeek == 6 || dayOfWeek == 7)? true : false);
    }
}
```


# Last Modified


# Usage

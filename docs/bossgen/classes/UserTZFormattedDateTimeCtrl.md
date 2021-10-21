---
layout: default
title: UserTZFormattedDateTimeCtrl
parent: classes
---
# Metadata Type
classes


# Filename 
UserTZFormattedDateTimeCtrl


# Raw XML
```
public class UserTZFormattedDateTimeCtrl {
    public DateTime dateTimeValue { get; set; }
    public String dateTimeformat { get; set; }

    public String getTimeZoneValue() {
        if(dateTimeValue != null) {
            dateTimeformat = String.isNotBlank(dateTimeformat) ? dateTimeformat : 'dd-MMMM-yyyy hh:mm a';
            return dateTimeValue.format(dateTimeformat);
        }
        return null;
    }
}
```


# Last Modified


# Usage

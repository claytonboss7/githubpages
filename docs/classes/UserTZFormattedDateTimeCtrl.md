---
layout: default
title: UserTZFormattedDateTimeCtrl
parent: classes
---

```public class UserTZFormattedDateTimeCtrl {
    public DateTime dateTimeValue { get; set; }
    public String dateTimeformat { get; set; }

    public String getTimeZoneValue() {
        if(dateTimeValue != null) {
            dateTimeformat = String.isNotBlank(dateTimeformat) ? dateTimeformat : 'dd-MMMM-yyyy hh:mm a';
            return dateTimeValue.format(dateTimeformat);
        }
        return null;
    }
}```

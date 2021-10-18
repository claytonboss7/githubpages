---
layout: default
title: UserTZFormattedDateTime
parent: components
---

```<apex:component access="global" controller="UserTZFormattedDateTimeCtrl">
     <apex:attribute assignTo="{!dateTimeformat}" description="format for datetime field" 
                     name="date_Timeformat" type="String"></apex:attribute>
       <apex:attribute assignTo="{!dateTimeValue}" description="The DateTime value to be rendered based upon the user's
               locale" name="date_Timevalue" type="DateTime"></apex:attribute>
       {!TimeZoneValue}
</apex:component>```

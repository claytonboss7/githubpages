---
layout: default
title: CommSubscriptionTiming
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
CommSubscriptionTiming
## Fields
### Unit

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Unit</fullName>
    <inlineHelpText>The unit of time that works with Offset to determine the communication timing.</inlineHelpText>
    <trackHistory>false</trackHistory>
</CustomField>
```
### PreferredTimeZone

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PreferredTimeZone</fullName>
    <inlineHelpText>Time zone of the preferred time span.</inlineHelpText>
    <trackHistory>false</trackHistory>
</CustomField>
```
### Offset

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Offset</fullName>
    <inlineHelpText>The amount of time before or after an event or the specific day of the week that you should communicate with the contact point. Set the unit of time in Unit. For example, if you set Unit as &quot;Week&quot; and Offset as &quot;-4&quot; communicate with the contact point four weeks before the event. If you set Offset as &quot;4&quot; communicate with the contact point four weeks after the event. If you set Unit as &quot;Day of Week&quot; and Offset as &quot;1,&quot; communicate with the contact point on Monday. If you set Offset as &quot;7&quot; communicate with the contact point on Sunday.</inlineHelpText>
    <trackHistory>false</trackHistory>
</CustomField>
```
### CommSubscriptionConsentId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>CommSubscriptionConsentId</fullName>
    <inlineHelpText>The communication subscription consent record associated with the communication subscription timing.</inlineHelpText>
    <trackHistory>false</trackHistory>
    <type>MasterDetail</type>
</CustomField>
```
### PreferredTimeStart

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PreferredTimeStart</fullName>
    <inlineHelpText>Start of the preferred time span in which to reach the contact point.</inlineHelpText>
    <trackHistory>false</trackHistory>
</CustomField>
```
### PreferredTimeEnd

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>PreferredTimeEnd</fullName>
    <inlineHelpText>End of the preferred time span in which to reach the contact point.</inlineHelpText>
    <trackHistory>false</trackHistory>
</CustomField>
```

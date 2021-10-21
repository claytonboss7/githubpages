---
layout: default
title: Concessions__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Concessions__c
## Fields
### Included_Excluded__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Included_Excluded__c</fullName>
    <externalId>false</externalId>
    <label>Included/Excluded</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Included</fullName>
                <default>false</default>
                <label>Included</label>
            </value>
            <value>
                <fullName>Excluded</fullName>
                <default>false</default>
                <label>Excluded</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### isFromCommunity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>isFromCommunity__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>isFromCommunity</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Notes_NAV__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Notes_NAV__c</fullName>
    <externalId>false</externalId>
    <label>Notes_NAV</label>
    <length>1000</length>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Concessions_Requested__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Concessions_Requested__c</fullName>
    <externalId>false</externalId>
    <label>Concessions Requested</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <controllingField>Concession_Type__c</controllingField>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>1 comp apartment per 20 picked up:</fullName>
                <default>false</default>
                <label>1 comp apartment per 20 picked up.</label>
            </value>
            <value>
                <fullName>Tax Terms &amp; conditions:</fullName>
                <default>false</default>
                <label>Tax Terms &amp; conditions.</label>
            </value>
            <value>
                <fullName>Minimum lease terms:</fullName>
                <default>false</default>
                <label>Minimum lease terms.</label>
            </value>
            <value>
                <fullName>Deposit and security info:</fullName>
                <default>false</default>
                <label>Deposit and security info.</label>
            </value>
            <value>
                <fullName>Housekeeping rate &amp; frequency:</fullName>
                <default>false</default>
                <label>Housekeeping rate &amp; frequency.</label>
            </value>
            <value>
                <fullName>Wireless High Speed internet included in rate:</fullName>
                <default>false</default>
                <label>Wireless High Speed internet included in rate.</label>
            </value>
            <value>
                <fullName>Utilities included in the rate:</fullName>
                <default>false</default>
                <label>Utilities included in the rate.</label>
            </value>
            <value>
                <fullName>Date you can confirm availability (if more than 30 days out):</fullName>
                <default>false</default>
                <label>Date you can confirm availability (if more than 30 days out).</label>
            </value>
            <value>
                <fullName>Additional Fees:</fullName>
                <default>false</default>
                <label>Additional Fees.</label>
            </value>
            <value>
                <fullName>Rent paid weekly/monthly/other</fullName>
                <default>false</default>
                <label>Rent paid weekly/monthly/other.</label>
            </value>
            <value>
                <fullName>Rate based on ____ minimum number of days</fullName>
                <default>false</default>
                <label>Rate based on ____ minimum number of days.</label>
            </value>
            <value>
                <fullName>Anticipated availability is listed above. Unit availability will be discussed starting DATE</fullName>
                <default>false</default>
                <label>Anticipated availability is listed above. Unit availability will be discussed starting DATE.</label>
            </value>
            <value>
                <fullName>Driver Lodging</fullName>
                <default>false</default>
                <label>Driver Lodging.</label>
            </value>
            <value>
                <fullName>Gratuity</fullName>
                <default>false</default>
                <label>Gratuity.</label>
            </value>
            <value>
                <fullName>Tolls</fullName>
                <default>false</default>
                <label>Tolls.</label>
            </value>
            <value>
                <fullName>Parking</fullName>
                <default>false</default>
                <label>Parking.</label>
            </value>
            <value>
                <fullName>Fuel</fullName>
                <default>false</default>
                <label>Fuel.</label>
            </value>
            <value>
                <fullName>Over Drive</fullName>
                <default>false</default>
                <label>Over Drive.</label>
            </value>
            <value>
                <fullName>Dead Head</fullName>
                <default>false</default>
                <label>Dead Head.</label>
            </value>
            <value>
                <fullName>Live Days</fullName>
                <default>false</default>
                <label>Live Days.</label>
            </value>
            <value>
                <fullName>Permit</fullName>
                <default>false</default>
                <label>Permit.</label>
            </value>
            <value>
                <fullName>Total miles</fullName>
                <default>false</default>
                <label>Total miles.</label>
            </value>
            <value>
                <fullName>Wait time</fullName>
                <default>false</default>
                <label>Wait time.</label>
            </value>
            <value>
                <fullName>Loading Unloading</fullName>
                <default>false</default>
                <label>Loading Unloading.</label>
            </value>
            <value>
                <fullName>Driving permits</fullName>
                <default>false</default>
                <label>Driving permits.</label>
            </value>
            <value>
                <fullName>Import and export charges</fullName>
                <default>false</default>
                <label>Import and export charges.</label>
            </value>
            <value>
                <fullName>Loading</fullName>
                <default>false</default>
                <label>Loading.</label>
            </value>
            <value>
                <fullName>Unloading</fullName>
                <default>false</default>
                <label>Unloading.</label>
            </value>
            <value>
                <fullName>Duties</fullName>
                <default>false</default>
                <label>Duties.</label>
            </value>
            <value>
                <fullName>Taxes</fullName>
                <default>false</default>
                <label>Taxes.</label>
            </value>
            <value>
                <fullName>Customs exam charges</fullName>
                <default>false</default>
                <label>Customs exam charges.</label>
            </value>
            <value>
                <fullName>Demurrage, storage and detention charges</fullName>
                <default>false</default>
                <label>Demurrage, storage and detention charges.</label>
            </value>
            <value>
                <fullName>ATA carnet expenses</fullName>
                <default>false</default>
                <label>ATA carnet expenses.</label>
            </value>
            <value>
                <fullName>Airport handling</fullName>
                <default>false</default>
                <label>Airport handling.</label>
            </value>
            <value>
                <fullName>Airline collection</fullName>
                <default>false</default>
                <label>Airline collection.</label>
            </value>
            <value>
                <fullName>Customs</fullName>
                <default>false</default>
                <label>Customs.</label>
            </value>
            <value>
                <fullName>Customs clearance</fullName>
                <default>false</default>
                <label>Customs clearance.</label>
            </value>
            <value>
                <fullName>Local transport</fullName>
                <default>false</default>
                <label>Local transport.</label>
            </value>
            <value>
                <fullName>Storage</fullName>
                <default>false</default>
                <label>Storage.</label>
            </value>
            <value>
                <fullName>Documentation</fullName>
                <default>false</default>
                <label>Documentation.</label>
            </value>
            <value>
                <fullName>ATA Carnet raising and processing</fullName>
                <default>false</default>
                <label>ATA Carnet raising and processing.</label>
            </value>
            <value>
                <fullName>Transport Insurance</fullName>
                <default>false</default>
                <label>Transport Insurance.</label>
            </value>
            <value>
                <fullName>Duties and taxes</fullName>
                <default>false</default>
                <label>Duties and taxes.</label>
            </value>
            <value>
                <fullName>Custom exam charges</fullName>
                <default>false</default>
                <label>Custom exam charges.</label>
            </value>
            <value>
                <fullName>Demurrage</fullName>
                <default>false</default>
                <label>Demurrage.</label>
            </value>
            <value>
                <fullName>Insurance</fullName>
                <default>false</default>
                <label>Insurance.</label>
            </value>
            <value>
                <fullName>All single rooms must have king beds.</fullName>
                <default>false</default>
                <label>All single rooms must have king beds.</label>
            </value>
            <value>
                <fullName>Bathtubs in all group rooms.</fullName>
                <default>false</default>
                <label>Bathtubs in all group rooms.</label>
            </value>
            <value>
                <fullName>Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment</fullName>
                <default>false</default>
                <label>Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment.</label>
            </value>
            <value>
                <fullName>Check-out at 00:00 for the whole group guaranteed.</fullName>
                <default>false</default>
                <label>Check-out at 00:00 for the whole group guaranteed.</label>
            </value>
            <value>
                <fullName>Comp hospitality room with microwave and fridge for group use, if not already in all guest rooms</fullName>
                <default>false</default>
                <label>Comp hospitality room with microwave and fridge for group use, if not already in all guest rooms.</label>
            </value>
            <value>
                <fullName>Complimentary High Speed internet in the rooms.</fullName>
                <default>false</default>
                <label>Complimentary High Speed internet in the rooms.</label>
            </value>
            <value>
                <fullName>Complimentary local &amp; 800 calls.</fullName>
                <default>false</default>
                <label>Complimentary local &amp; 800 calls.</label>
            </value>
            <value>
                <fullName>Complimentary microwave and fridges in all rooms.</fullName>
                <default>false</default>
                <label>Complimentary microwave and fridges in all rooms.</label>
            </value>
            <value>
                <fullName>Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.</fullName>
                <default>false</default>
                <label>Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.</label>
            </value>
            <value>
                <fullName>Complimentary parking. If not complimentary, please indicate discounted parking.</fullName>
                <default>false</default>
                <label>Complimentary parking. If not complimentary, please indicate discounted parking.</label>
            </value>
            <value>
                <fullName>CONTRACTED CALL IN RATE FOR A TV SHOW. No room night guarantee, rate for individuals coming in and out. Rate must be guaranteed regardless of pick-up.</fullName>
                <default>false</default>
                <label>CONTRACTED CALL IN RATE FOR A TV SHOW. No room night guarantee, rate for individuals coming in and out. Rate must be guaranteed regardless of pick-up.</label>
            </value>
            <value>
                <fullName>F&amp;B discount.</fullName>
                <default>false</default>
                <label>F&amp;B discount.</label>
            </value>
            <value>
                <fullName>Hotel contact to sign a location agreement (agreeing to shoot an interview in the room; no hotel photograph logos or signage)</fullName>
                <default>false</default>
                <label>Hotel contact to sign a location agreement (agreeing to shoot an interview in the room; no hotel photograph logos or signage).</label>
            </value>
            <value>
                <fullName>If you can not take all the rooms, please note how many you can take if you are interested in a partial block.</fullName>
                <default>false</default>
                <label>If you can not take all the rooms, please note how many you can take if you are interested in a partial block.</label>
            </value>
            <value>
                <fullName>Include rates for all suite types.</fullName>
                <default>false</default>
                <label>Include rates for all suite types.</label>
            </value>
            <value>
                <fullName>Laundry discount.</fullName>
                <default>false</default>
                <label>Laundry discount.</label>
            </value>
            <value>
                <fullName>Micro&apos;s &amp; Fridges very important- how many can you accommodate? Is there an additional charge?</fullName>
                <default>false</default>
                <label>Micro&apos;s &amp; Fridges very important- how many can you accommodate? Is there an additional charge.</label>
            </value>
            <value>
                <fullName>Complimentary meeting room on GROUND FLOOR for tech gear.</fullName>
                <default>false</default>
                <label>Complimentary meeting room on GROUND FLOOR for tech gear.</label>
            </value>
            <value>
                <fullName>Option date to be no earlier than</fullName>
                <default>false</default>
                <label>Option date to be no earlier than.</label>
            </value>
            <value>
                <fullName>Please provide a weekly/monthly parking rate for group (if not complimentary).</fullName>
                <default>false</default>
                <label>Please provide a weekly/monthly parking rate for group (if not complimentary).</label>
            </value>
            <value>
                <fullName>Please see attached rooming list and quote based on that. The hotel acknowledges offer is based on the attached rooming list.</fullName>
                <default>false</default>
                <label>Please see attached rooming list and quote based on that. The hotel acknowledges offer is based on the attached rooming list.</label>
            </value>
            <value>
                <fullName>Discounted breakfast price</fullName>
                <default>false</default>
                <label>Discounted breakfast price.</label>
            </value>
            <value>
                <fullName>Room counts and dates are soft and may change.</fullName>
                <default>false</default>
                <label>Room counts and dates are soft and may change.</label>
            </value>
            <value>
                <fullName>Rooms may or may not be continuous throughout the length of stay. May need rooms pre and post stay.</fullName>
                <default>false</default>
                <label>Rooms may or may not be continuous throughout the length of stay. May need rooms pre and post stay.</label>
            </value>
            <value>
                <fullName>Suite upgrade for company manager, if available.</fullName>
                <default>false</default>
                <label>Suite upgrade for company manager, if available.</label>
            </value>
            <value>
                <fullName>This group is a SPECIAL EQUITY tour. Individuals will have 1 official hotel option. Rate and all terms of contract are guaranteed</fullName>
                <default>false</default>
                <label>This group is a SPECIAL EQUITY tour. Individuals will have 1 official hotel option. Rate and all terms of contract are guaranteed.</label>
            </value>
            <value>
                <fullName>This group is a UNION TOUR. Individuals will have 2 official hotel options to select from. No pick up is a guaranteed. Rate and all terms of contract are guaranteed regardless of pick up.</fullName>
                <default>false</default>
                <label>This group is a UNION TOUR. Individuals will have 2 official hotel options to select from. No pick up is a guaranteed. Rate and all terms of contract are guaranteed regardless of pick up.</label>
            </value>
            <value>
                <fullName>Hotel bar will stay open late for group use.</fullName>
                <default>false</default>
                <label>Hotel bar will stay open late for group use.</label>
            </value>
            <value>
                <fullName>X suite upgrades.</fullName>
                <default>false</default>
                <label>X suite upgrades.</label>
            </value>
            <value>
                <fullName>XX room night(s) of every XX room nights picked up cumulative per stay is complimentary</fullName>
                <default>false</default>
                <label>XX room night(s) of every XX room nights picked up cumulative per stay is complimentary.</label>
            </value>
            <value>
                <fullName>Deadhead Driver Lodging</fullName>
                <default>false</default>
                <label>Deadhead Driver Lodging.</label>
            </value>
            <value>
                <fullName>Manned 24 hour flight watch service</fullName>
                <default>false</default>
                <label>Manned 24 hour flight watch service.</label>
            </value>
            <value>
                <fullName>Dedicated Flight Support Team</fullName>
                <default>false</default>
                <label>Dedicated Flight Support Team.</label>
            </value>
            <value>
                <fullName>Passenger Charges and taxes</fullName>
                <default>false</default>
                <label>Passenger Charges and taxes.</label>
            </value>
            <value>
                <fullName>War Risk Insurance or any similar or other insurance premium surcharge required</fullName>
                <default>false</default>
                <label>War Risk Insurance or any similar or other insurance premium surcharge required.</label>
            </value>
            <value>
                <fullName>Non-standard airport fees and taxes</fullName>
                <default>false</default>
                <label>Non-standard airport fees and taxes.</label>
            </value>
            <value>
                <fullName>De-icing and ground transportation</fullName>
                <default>false</default>
                <label>De-icing and ground transportation.</label>
            </value>
            <value>
                <fullName>Additional fuel costs over USD 4.00 per gallon and surcharges (if applicable)</fullName>
                <default>false</default>
                <label>Additional fuel costs over USD 4.00 per gallon and surcharges (if applicable).</label>
            </value>
            <value>
                <fullName>In-Flight Representative</fullName>
                <default>false</default>
                <label>In-Flight Representative.</label>
            </value>
            <value>
                <fullName>Use of internet, WIFI, in-flight satellite telephone or other communication charges</fullName>
                <default>false</default>
                <label>Use of internet, WIFI, in-flight satellite telephone or other communication charges.</label>
            </value>
            <value>
                <fullName>Stamp Duty (if applicable)</fullName>
                <default>false</default>
                <label>Stamp Duty (if applicable).</label>
            </value>
            <value>
                <fullName>Other</fullName>
                <default>false</default>
                <label>Other.</label>
            </value>
            <value>
                <fullName>Check-in at 00:00 for the whole group guaranteed.</fullName>
                <default>false</default>
                <label>Check-in at 00:00 for the whole group guaranteed.</label>
            </value>
            <value>
                <fullName>COVID</fullName>
                <default>false</default>
                <label>COVID.</label>
            </value>
            <value>
                <fullName>Breakfast included in rate – Please specify cost of breakfast if not included.</fullName>
                <default>false</default>
                <label>Breakfast included in rate – Please specify cost of breakfast if not included.</label>
            </value>
            <value>
                <fullName>Rewards points available.</fullName>
                <default>false</default>
                <label>Rewards points available.</label>
            </value>
            <value>
                <fullName>Mini bars must be emptied for the group, free of charge.</fullName>
                <default>false</default>
                <label>Mini bars must be emptied for the group, free of charge.</label>
            </value>
            <value>
                <fullName>Hotel is WAIVING all cancellation and attrition penalties. Group will prioritize properties that can accommodate this request.</fullName>
                <default>false</default>
                <label>Hotel is WAIVING all cancellation and attrition penalties. Group will prioritize properties that can accommodate this request.</label>
            </value>
        </valueSetDefinition>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>All single rooms must have king beds.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Bathtubs in all group rooms.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Breakfast included in rate. If not included, please specify type and cost per person per day (inclusive of tax and gratuity) in comment</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Check-out at 00:00 for the whole group guaranteed.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Comp hospitality room with microwave and fridge for group use, if not already in all guest rooms</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Complimentary High Speed internet in the rooms.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Complimentary local &amp; 800 calls.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Complimentary microwave and fridges in all rooms.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Complimentary parking for X buses, if there is a fee please specify how much per bus and note how many buses you can accommodate.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Complimentary parking. If not complimentary, please indicate discounted parking.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>CONTRACTED CALL IN RATE FOR A TV SHOW. No room night guarantee, rate for individuals coming in and out. Rate must be guaranteed regardless of pick-up.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>F&amp;B discount.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Hotel contact to sign a location agreement (agreeing to shoot an interview in the room; no hotel photograph logos or signage)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>If you can not take all the rooms, please note how many you can take if you are interested in a partial block.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Include rates for all suite types.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Laundry discount.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Micro&apos;s &amp; Fridges very important- how many can you accommodate? Is there an additional charge?</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Complimentary meeting room on GROUND FLOOR for tech gear.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Option date to be no earlier than</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Please provide a weekly/monthly parking rate for group (if not complimentary).</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Please see attached rooming list and quote based on that. The hotel acknowledges offer is based on the attached rooming list.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Discounted breakfast price</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Room counts and dates are soft and may change.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Rooms may or may not be continuous throughout the length of stay. May need rooms pre and post stay.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Suite upgrade for company manager, if available.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>This group is a SPECIAL EQUITY tour. Individuals will have 1 official hotel option. Rate and all terms of contract are guaranteed</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>This group is a UNION TOUR. Individuals will have 2 official hotel options to select from. No pick up is a guaranteed. Rate and all terms of contract are guaranteed regardless of pick up.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Hotel bar will stay open late for group use.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>X suite upgrades.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>XX room night(s) of every XX room nights picked up cumulative per stay is complimentary</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Other</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Breakfast included in rate – Please specify cost of breakfast if not included.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housing</controllingFieldValue>
            <valueName>Hotel is WAIVING all cancellation and attrition penalties. Group will prioritize properties that can accommodate this request.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>1 comp apartment per 20 picked up:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Tax Terms &amp; conditions:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Minimum lease terms:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Deposit and security info:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Housekeeping rate &amp; frequency:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Wireless High Speed internet included in rate:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Utilities included in the rate:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Date you can confirm availability (if more than 30 days out):</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Additional Fees:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Rent paid weekly/monthly/other</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Rate based on ____ minimum number of days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Corporate Housing</controllingFieldValue>
            <valueName>Anticipated availability is listed above. Unit availability will be discussed starting DATE</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Driver Lodging</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Gratuity</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Tolls</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Parking</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Fuel</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Over Drive</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Dead Head</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Live Days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Permit</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Total miles</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Wait time</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Taxes</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>GT</controllingFieldValue>
            <valueName>Deadhead Driver Lodging</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Loading Unloading</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Driving permits</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Import and export charges</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Loading</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Unloading</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Duties</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Customs exam charges</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Demurrage, storage and detention charges</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>ATA carnet expenses</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Airport handling</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Airline collection</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Customs</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Customs clearance</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Local transport</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Storage</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Documentation</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>ATA Carnet raising and processing</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Transport Insurance</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Duties and taxes</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Custom exam charges</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Demurrage</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Freight</controllingFieldValue>
            <valueName>Insurance</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Manned 24 hour flight watch service</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Dedicated Flight Support Team</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Passenger Charges and taxes</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>War Risk Insurance or any similar or other insurance premium surcharge required</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Non-standard airport fees and taxes</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>De-icing and ground transportation</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Additional fuel costs over USD 4.00 per gallon and surcharges (if applicable)</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>In-Flight Representative</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Use of internet, WIFI, in-flight satellite telephone or other communication charges</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Air</controllingFieldValue>
            <valueName>Stamp Duty (if applicable)</valueName>
        </valueSettings>
    </valueSet>
</CustomField>
```
### Concession_Provided__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Concession_Provided__c</fullName>
    <externalId>false</externalId>
    <label>Concession Provided</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <controllingField>Concessions_Requested__c</controllingField>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Yes</fullName>
                <default>false</default>
                <label>Yes</label>
            </value>
            <value>
                <fullName>No Comp</fullName>
                <default>false</default>
                <label>No Comp</label>
            </value>
            <value>
                <fullName>Other _____________</fullName>
                <default>false</default>
                <label>Other _____________</label>
            </value>
            <value>
                <fullName>Tax exempt after 30 days</fullName>
                <default>false</default>
                <label>Tax exempt after 30 days</label>
            </value>
            <value>
                <fullName>Tax exempt after 30 days, however, tax is collected and will be refunded after 30 days</fullName>
                <default>false</default>
                <label>Tax exempt after 30 days, however, tax is collected and will be refunded after 30 days</label>
            </value>
            <value>
                <fullName>Stays under 30 days pay tax rate of: _____% tax per night</fullName>
                <default>false</default>
                <label>Stays under 30 days pay tax rate of: _____% tax per night</label>
            </value>
            <value>
                <fullName>30 nights/days</fullName>
                <default>false</default>
                <label>30 nights/days</label>
            </value>
            <value>
                <fullName>7 nights/days</fullName>
                <default>false</default>
                <label>7 nights/days</label>
            </value>
            <value>
                <fullName>14 nights/days</fullName>
                <default>false</default>
                <label>14 nights/days</label>
            </value>
            <value>
                <fullName>No deposit</fullName>
                <default>false</default>
                <label>No deposit</label>
            </value>
            <value>
                <fullName>Deposit of ____________, due ____________</fullName>
                <default>false</default>
                <label>Deposit of ____________, due ____________</label>
            </value>
            <value>
                <fullName>Deposit to be used as first month&apos;s rent</fullName>
                <default>false</default>
                <label>Deposit to be used as first month&apos;s rent</label>
            </value>
            <value>
                <fullName>Deposit to be refunded upon check out</fullName>
                <default>false</default>
                <label>Deposit to be refunded upon check out</label>
            </value>
            <value>
                <fullName>Deposit to be used as final cleaning fee</fullName>
                <default>false</default>
                <label>Deposit to be used as final cleaning fee</label>
            </value>
            <value>
                <fullName>Bi Weekly included in rate</fullName>
                <default>false</default>
                <label>Bi Weekly included in rate</label>
            </value>
            <value>
                <fullName>HK not included in rate, one-time fee is:</fullName>
                <default>false</default>
                <label>HK not included in rate, one-time fee is:</label>
            </value>
            <value>
                <fullName>If not, how much? ______ per day/24 hours/week/month</fullName>
                <default>false</default>
                <label>If not, how much? ______ per day/24 hours/week/month</label>
            </value>
            <value>
                <fullName>Yes, cap amount ______</fullName>
                <default>false</default>
                <label>Yes, cap amount ______</label>
            </value>
            <value>
                <fullName>No</fullName>
                <default>false</default>
                <label>No</label>
            </value>
            <value>
                <fullName>Date:_______</fullName>
                <default>false</default>
                <label>Date:_______</label>
            </value>
            <value>
                <fullName>None</fullName>
                <default>false</default>
                <label>None</label>
            </value>
            <value>
                <fullName>Weekly</fullName>
                <default>false</default>
                <label>Weekly</label>
            </value>
            <value>
                <fullName>Monthly</fullName>
                <default>false</default>
                <label>Monthly</label>
            </value>
            <value>
                <fullName>Minimum number of days _____</fullName>
                <default>false</default>
                <label>Minimum number of days _____</label>
            </value>
            <value>
                <fullName>Is Driver Lodging included in the rate?</fullName>
                <default>false</default>
                <label>Is Driver Lodging included in the rate?</label>
            </value>
            <value>
                <fullName>If not included, please list dates group is responsible for: Check In ____ Check Out ____</fullName>
                <default>false</default>
                <label>If not included, please list dates group is responsible for: Check In ____ Check Out ____</label>
            </value>
            <value>
                <fullName>Please include gratuity in rate</fullName>
                <default>false</default>
                <label>Please include gratuity in rate</label>
            </value>
            <value>
                <fullName>Gratuity will be paid directly to driver</fullName>
                <default>false</default>
                <label>Gratuity will be paid directly to driver</label>
            </value>
            <value>
                <fullName>Tolls included up to ____________</fullName>
                <default>false</default>
                <label>Tolls included up to ____________</label>
            </value>
            <value>
                <fullName>Tolls will be an additional charge</fullName>
                <default>false</default>
                <label>Tolls will be an additional charge</label>
            </value>
            <value>
                <fullName>Tolls included</fullName>
                <default>false</default>
                <label>Tolls included</label>
            </value>
            <value>
                <fullName>Parking is an additional cost.</fullName>
                <default>false</default>
                <label>Parking is an additional cost.</label>
            </value>
            <value>
                <fullName>Fuel is based on ______ miles at $____/mile</fullName>
                <default>false</default>
                <label>Fuel is based on ______ miles at $____/mile</label>
            </value>
            <value>
                <fullName>Number of overdrives included ____________</fullName>
                <default>false</default>
                <label>Number of overdrives included ____________</label>
            </value>
            <value>
                <fullName>Additional overdrives at rate of ____________</fullName>
                <default>false</default>
                <label>Additional overdrives at rate of ____________</label>
            </value>
            <value>
                <fullName>Deadhead Days _________</fullName>
                <default>false</default>
                <label>Deadhead Days _________</label>
            </value>
            <value>
                <fullName>Live Days _________</fullName>
                <default>false</default>
                <label>Live Days _________</label>
            </value>
            <value>
                <fullName>Total Days _________</fullName>
                <default>false</default>
                <label>Total Days _________</label>
            </value>
            <value>
                <fullName>Permit fees included up to _________</fullName>
                <default>false</default>
                <label>Permit fees included up to _________</label>
            </value>
            <value>
                <fullName>Permit fees included</fullName>
                <default>false</default>
                <label>Permit fees included</label>
            </value>
            <value>
                <fullName>Permit fees will be and additional charge</fullName>
                <default>false</default>
                <label>Permit fees will be and additional charge</label>
            </value>
            <value>
                <fullName>Wait time billed at $_____</fullName>
                <default>false</default>
                <label>Wait time billed at $_____</label>
            </value>
            <value>
                <fullName>Wait time billed at _____</fullName>
                <default>false</default>
                <label>Wait time billed at _____</label>
            </value>
        </valueSetDefinition>
        <valueSettings>
            <controllingFieldValue>Rent paid weekly/monthly/other</controllingFieldValue>
            <controllingFieldValue>1 comp apartment per 20 picked up:</controllingFieldValue>
            <controllingFieldValue>Minimum lease terms:</controllingFieldValue>
            <controllingFieldValue>Housekeeping rate &amp; frequency:</controllingFieldValue>
            <controllingFieldValue>Additional Fees:</controllingFieldValue>
            <valueName>Other _____________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Rent paid weekly/monthly/other</controllingFieldValue>
            <valueName>Weekly</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Rent paid weekly/monthly/other</controllingFieldValue>
            <valueName>Monthly</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Rate based on ____ minimum number of days</controllingFieldValue>
            <valueName>Minimum number of days _____</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Anticipated availability is listed above. Unit availability will be discussed starting DATE</controllingFieldValue>
            <controllingFieldValue>Date you can confirm availability (if more than 30 days out):</controllingFieldValue>
            <valueName>Date:_______</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Driver Lodging</controllingFieldValue>
            <controllingFieldValue>Total miles</controllingFieldValue>
            <valueName>Is Driver Lodging included in the rate?</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Driver Lodging</controllingFieldValue>
            <controllingFieldValue>Total miles</controllingFieldValue>
            <valueName>If not included, please list dates group is responsible for: Check In ____ Check Out ____</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Gratuity</controllingFieldValue>
            <valueName>Please include gratuity in rate</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Gratuity</controllingFieldValue>
            <valueName>Gratuity will be paid directly to driver</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Tolls</controllingFieldValue>
            <valueName>Tolls included up to ____________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Tolls</controllingFieldValue>
            <valueName>Tolls will be an additional charge</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Tolls</controllingFieldValue>
            <valueName>Tolls included</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Parking</controllingFieldValue>
            <valueName>Parking is an additional cost.</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Fuel</controllingFieldValue>
            <valueName>Fuel is based on ______ miles at $____/mile</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Over Drive</controllingFieldValue>
            <valueName>Number of overdrives included ____________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Over Drive</controllingFieldValue>
            <valueName>Additional overdrives at rate of ____________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Dead Head</controllingFieldValue>
            <valueName>Deadhead Days _________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>1 comp apartment per 20 picked up:</controllingFieldValue>
            <controllingFieldValue>Wireless High Speed internet included in rate:</controllingFieldValue>
            <controllingFieldValue>Utilities included in the rate:</controllingFieldValue>
            <valueName>Yes</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>1 comp apartment per 20 picked up:</controllingFieldValue>
            <valueName>No Comp</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Tax Terms &amp; conditions:</controllingFieldValue>
            <valueName>Tax exempt after 30 days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Tax Terms &amp; conditions:</controllingFieldValue>
            <valueName>Tax exempt after 30 days, however, tax is collected and will be refunded after 30 days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Tax Terms &amp; conditions:</controllingFieldValue>
            <valueName>Stays under 30 days pay tax rate of: _____% tax per night</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Minimum lease terms:</controllingFieldValue>
            <valueName>30 nights/days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Minimum lease terms:</controllingFieldValue>
            <valueName>7 nights/days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Minimum lease terms:</controllingFieldValue>
            <valueName>14 nights/days</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Deposit and security info:</controllingFieldValue>
            <valueName>No deposit</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Deposit and security info:</controllingFieldValue>
            <valueName>Deposit of ____________, due ____________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Deposit and security info:</controllingFieldValue>
            <valueName>Deposit to be used as first month&apos;s rent</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Deposit and security info:</controllingFieldValue>
            <valueName>Deposit to be refunded upon check out</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Deposit and security info:</controllingFieldValue>
            <valueName>Deposit to be used as final cleaning fee</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housekeeping rate &amp; frequency:</controllingFieldValue>
            <valueName>Bi Weekly included in rate</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Housekeeping rate &amp; frequency:</controllingFieldValue>
            <valueName>HK not included in rate, one-time fee is:</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Wireless High Speed internet included in rate:</controllingFieldValue>
            <valueName>If not, how much? ______ per day/24 hours/week/month</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Utilities included in the rate:</controllingFieldValue>
            <valueName>Yes, cap amount ______</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Utilities included in the rate:</controllingFieldValue>
            <valueName>No</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Additional Fees:</controllingFieldValue>
            <valueName>None</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Live Days</controllingFieldValue>
            <valueName>Live Days _________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Live Days</controllingFieldValue>
            <valueName>Total Days _________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Permit</controllingFieldValue>
            <valueName>Permit fees included up to _________</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Permit</controllingFieldValue>
            <valueName>Permit fees included</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Permit</controllingFieldValue>
            <valueName>Permit fees will be and additional charge</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Wait time</controllingFieldValue>
            <valueName>Wait time billed at $_____</valueName>
        </valueSettings>
        <valueSettings>
            <controllingFieldValue>Wait time</controllingFieldValue>
            <valueName>Wait time billed at _____</valueName>
        </valueSettings>
    </valueSet>
</CustomField>
```
### Concession_Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Concession_Type__c</fullName>
    <externalId>false</externalId>
    <label>Concession Type</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Housing</fullName>
                <default>false</default>
                <label>Housing</label>
            </value>
            <value>
                <fullName>Corporate Housing</fullName>
                <default>false</default>
                <label>Corporate Housing</label>
            </value>
            <value>
                <fullName>GT</fullName>
                <default>false</default>
                <label>GT</label>
            </value>
            <value>
                <fullName>Freight</fullName>
                <default>false</default>
                <label>Freight</label>
            </value>
            <value>
                <fullName>Air</fullName>
                <default>false</default>
                <label>Air</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### Concessions_Requested_Index__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Concessions_Requested_Index__c</fullName>
    <externalId>true</externalId>
    <label>Concessions Requested Index</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### IsDetailNotFees__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsDetailNotFees__c</fullName>
    <externalId>false</externalId>
    <formula>IF( ISPICKVAL(Concessions_Requested__c, &apos;Vendor guarantees they are following CDC guidelines and Motorcoach (ABA or UMA) industry cleanliness protocols&apos;),true,false)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>IsDetailNotFees</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Air__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Air__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Air</label>
    <referenceTo>Air__c</referenceTo>
    <relationshipLabel>Concessions</relationshipLabel>
    <relationshipName>Concessions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Create_in_Bid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Create_in_Bid__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Create in Bid</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Agreed__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Agreed__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>Agreed</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### IsFromVendor__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsFromVendor__c</fullName>
    <defaultValue>false</defaultValue>
    <externalId>false</externalId>
    <label>IsFromVendor</label>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Checkbox</type>
</CustomField>
```
### Production__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Production</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Concessions</relationshipLabel>
    <relationshipName>Concessions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Bid__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Bid__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Bid</label>
    <referenceTo>Bid__c</referenceTo>
    <relationshipLabel>Concessions</relationshipLabel>
    <relationshipName>Concessions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Freight__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Freight__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Freight</label>
    <referenceTo>Freight__c</referenceTo>
    <relationshipLabel>Concessions</relationshipLabel>
    <relationshipName>Concessions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Order__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Order__c</fullName>
    <externalId>false</externalId>
    <label>Order</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Housing__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Housing__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Housing</label>
    <referenceTo>Housing__c</referenceTo>
    <relationshipLabel>Concessions</relationshipLabel>
    <relationshipName>Concessions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Rate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Rate__c</fullName>
    <externalId>false</externalId>
    <label>Rate</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Notes__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Notes__c</fullName>
    <externalId>true</externalId>
    <label>Notes</label>
    <length>255</length>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### GT__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>GT__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>GT</label>
    <referenceTo>Ground__c</referenceTo>
    <relationshipLabel>Concessions</relationshipLabel>
    <relationshipName>Concessions</relationshipName>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

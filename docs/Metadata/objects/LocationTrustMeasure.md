---
layout: default
title: LocationTrustMeasure
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
LocationTrustMeasure
## Fields
### Description

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Description</fullName>
    <inlineHelpText>Explain how you’ll carry out the trust measure. Be concise. Prioritize clarity over complete sentences — you have only 250 characters.</inlineHelpText>
</CustomField>
```
### SortOrder

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>SortOrder</fullName>
    <inlineHelpText>Indicates where this trust measure is positioned in your layout. For example, in a banner layout, a display order of 1 places the trust card to the left. A display order of 2 places the trust measure to the right of 1.</inlineHelpText>
</CustomField>
```
### IsVisibleInPublic

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IsVisibleInPublic</fullName>
    <inlineHelpText>Publishes this trust measure to the location you select.</inlineHelpText>
</CustomField>
```
### OwnerId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>OwnerId</fullName>
    <type>Lookup</type>
</CustomField>
```
### IconUrl

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>IconUrl</fullName>
    <inlineHelpText>The URL where your icon is hosted. You create and host the icon for each trust measure.</inlineHelpText>
</CustomField>
```
### LocationId

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>LocationId</fullName>
    <inlineHelpText>The store, hotel, or other physical space that your business occupies. Each trust measure lives at a single location. If no external reference exists on the location, the trust card won’t display. If you get an error, edit the location to add an external reference.</inlineHelpText>
    <type>Lookup</type>
</CustomField>
```
### Title

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Title</fullName>
    <inlineHelpText>The header for your trust measure that’s displayed to viewers. Keep it short and sweet! You can use up to 40 characters, but 20 is best to keep your title on one line.</inlineHelpText>
</CustomField>
```

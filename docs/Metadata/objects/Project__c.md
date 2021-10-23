---
layout: default
title: Project__c
parent: objects
grand_parent: Metadata
---
# Metadata Type
CustomObject

# Name
Project__c
## Fields
### Last_Project_Update__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Last_Project_Update__c</fullName>
    <externalId>false</externalId>
    <label>Last Project Update</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Project_Health__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project_Health__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(&apos;Good&apos;, &apos;Good&apos;, IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/tangodesktopproject/16/theme/dialog-error.png&apos;, &apos;Red&apos;), 

&apos;Ok&apos;, IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/tangodesktopproject/16/theme/emblem-important.png&apos;, &apos;Orange&apos;), 

IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/fatcow/farmfresh/16/tick.png&apos;, &apos;Green&apos;))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Project Health</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Budget__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Budget__c</fullName>
    <externalId>false</externalId>
    <label>Budget</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Currency</type>
</CustomField>
```
### Story_Template__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Story_Template__c</fullName>
    <externalId>false</externalId>
    <label>Story Template</label>
    <length>131072</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### JSON__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>JSON__c</fullName>
    <externalId>false</externalId>
    <label>JSON</label>
    <length>131072</length>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Shadow_Project__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Shadow_Project__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Shadow Project</label>
    <referenceTo>Shadow_Project__c</referenceTo>
    <relationshipLabel>Projects</relationshipLabel>
    <relationshipName>Projects</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Production_Org__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Production_Org__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Production Org</label>
    <referenceTo>Org__c</referenceTo>
    <relationshipLabel>Projects (Production Org)</relationshipLabel>
    <relationshipName>Projects1</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Project__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Project</label>
    <referenceTo>Project__c</referenceTo>
    <relationshipLabel>Projects</relationshipLabel>
    <relationshipName>Projects</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Amount_of_Stories__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Amount_of_Stories__c</fullName>
    <externalId>false</externalId>
    <label>Amount of Stories</label>
    <summaryForeignKey>Project_Item__c.Project__c</summaryForeignKey>
    <summaryOperation>count</summaryOperation>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Summary</type>
</CustomField>
```
### Integration_Org__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Integration_Org__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Integration Org</label>
    <referenceTo>Org__c</referenceTo>
    <relationshipLabel>Projects</relationshipLabel>
    <relationshipName>Projects</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Opportunity__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Opportunity__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Opportunity</label>
    <referenceTo>Opportunity</referenceTo>
    <relationshipLabel>Projects</relationshipLabel>
    <relationshipName>Projects</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Project_Version__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project_Version__c</fullName>
    <externalId>false</externalId>
    <label>Project Version</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Project_Start_Date__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project_Start_Date__c</fullName>
    <externalId>false</externalId>
    <label>Project Start Date</label>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Date</type>
</CustomField>
```
### Project_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project_URL__c</fullName>
    <externalId>false</externalId>
    <formula>HYPERLINK(&apos;https://www.pivotaltracker.com/n/projects/&apos; +  Project_Id__c ,&apos;https://www.pivotaltracker.com/n/projects/&apos; +  Project_Id__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Project URL</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Project_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project_Id__c</fullName>
    <externalId>true</externalId>
    <label>Project Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Tracker_Integration__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Tracker_Integration__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(Project_Id__c, null, IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/tangodesktopproject/16/theme/dialog-error.png&apos;, &apos;Red&apos;),

IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/fatcow/farmfresh/16/tick.png&apos;, &apos;Green&apos;))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Tracker Integration</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Account__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Account__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Account</label>
    <referenceTo>Account</referenceTo>
    <relationshipLabel>Projects</relationshipLabel>
    <relationshipName>Projects</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```

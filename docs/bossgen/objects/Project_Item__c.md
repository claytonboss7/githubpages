---
layout: default
title: Project_Item__c
parent: objects
---
# Metadata Type
CustomObject

# Name
Project_Item__c
## Fields
### pt_kind__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_kind__c</fullName>
    <externalId>false</externalId>
    <label>pt_kind</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Git_PR_Full_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Git_PR_Full_Name__c</fullName>
    <externalId>false</externalId>
    <label>Git PR Full Name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Data__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Data__c</fullName>
    <externalId>false</externalId>
    <label>Data</label>
    <length>131072</length>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>LongTextArea</type>
    <visibleLines>3</visibleLines>
</CustomField>
```
### Days_since_Update__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Days_since_Update__c</fullName>
    <externalId>false</externalId>
    <formula>Today() -  DATEVALUE(Age_Since_Update__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Days since Update</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Deployment_Item__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Deployment_Item__c</fullName>
    <deleteConstraint>SetNull</deleteConstraint>
    <externalId>false</externalId>
    <label>Deployment Item</label>
    <referenceTo>Deployment_Items__c</referenceTo>
    <relationshipLabel>Project Items</relationshipLabel>
    <relationshipName>Project_Items</relationshipName>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Lookup</type>
</CustomField>
```
### Git_Branch__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Git_Branch__c</fullName>
    <externalId>false</externalId>
    <label>Git Branch</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### pt_description__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_description__c</fullName>
    <externalId>false</externalId>
    <label>pt_description</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Planned_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Planned_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Planned Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Git_Pull_Request__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Git_Pull_Request__c</fullName>
    <externalId>false</externalId>
    <label>Git Pull Request</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Project__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Project__c</fullName>
    <externalId>false</externalId>
    <label>Project</label>
    <referenceTo>Project__c</referenceTo>
    <relationshipLabel>Latest Story Edits</relationshipLabel>
    <relationshipName>Project_Items</relationshipName>
    <relationshipOrder>0</relationshipOrder>
    <reparentableMasterDetail>true</reparentableMasterDetail>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>MasterDetail</type>
    <writeRequiresMasterRead>false</writeRequiresMasterRead>
</CustomField>
```
### pt_name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_name__c</fullName>
    <externalId>false</externalId>
    <label>pt_name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Started_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Started_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Started Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Story_Name__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Story_Name__c</fullName>
    <externalId>false</externalId>
    <label>Story Name</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Quip_Pre_Development_URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Quip_Pre_Development_URL__c</fullName>
    <externalId>false</externalId>
    <label>Quip Pre Development URL</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Url</type>
</CustomField>
```
### Kind__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Kind__c</fullName>
    <externalId>false</externalId>
    <label>Kind</label>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>story</fullName>
                <default>false</default>
                <label>story</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### pt_owned_by_id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_owned_by_id__c</fullName>
    <externalId>false</externalId>
    <label>pt_owned_by_id</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### pt_current_state__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_current_state__c</fullName>
    <externalId>false</externalId>
    <label>pt_current_state</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Story_Id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Story_Id__c</fullName>
    <externalId>false</externalId>
    <label>Story Id</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### pt_updated_at__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_updated_at__c</fullName>
    <externalId>false</externalId>
    <label>pt_updated_at</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Boss_Story__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Boss_Story__c</fullName>
    <externalId>false</externalId>
    <formula>CASE(&apos;Good&apos;, &apos;Good&apos;, IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/tangodesktopproject/16/theme/dialog-error.png&apos;, &apos;Red&apos;),

&apos;Ok&apos;, IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/tangodesktopproject/16/theme/emblem-important.png&apos;, &apos;Orange&apos;),

IMAGE(&apos;/resource/1523798147000/GraphicsPackNew/fatcow/farmfresh/16/tick.png&apos;, &apos;Green&apos;))</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Boss Story</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### pt_project_id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_project_id__c</fullName>
    <externalId>false</externalId>
    <label>pt_project_id</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Story_Status__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Story_Status__c</fullName>
    <defaultValue>&quot;planned&quot;</defaultValue>
    <externalId>false</externalId>
    <label>Story Status</label>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>planned</fullName>
                <default>false</default>
                <label>planned</label>
            </value>
            <value>
                <fullName>started</fullName>
                <default>false</default>
                <label>started</label>
            </value>
            <value>
                <fullName>finished</fullName>
                <default>false</default>
                <label>finished</label>
            </value>
            <value>
                <fullName>delivered</fullName>
                <default>false</default>
                <label>delivered</label>
            </value>
            <value>
                <fullName>accepted uat</fullName>
                <default>false</default>
                <label>accepted uat</label>
            </value>
            <value>
                <fullName>accepted in prod</fullName>
                <default>false</default>
                <label>accepted in prod</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### URL__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>URL__c</fullName>
    <externalId>false</externalId>
    <label>URL</label>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Url</type>
</CustomField>
```
### Finished_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Finished_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Finished Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Age_Since_Update__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Age_Since_Update__c</fullName>
    <externalId>false</externalId>
    <formula>DATETIMEVALUE(pt_updated_at__c)</formula>
    <formulaTreatBlanksAs>BlankAsZero</formulaTreatBlanksAs>
    <label>Age Since Update</label>
    <required>false</required>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### pt_story_type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_story_type__c</fullName>
    <externalId>false</externalId>
    <label>pt_story_type</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### Type__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Type__c</fullName>
    <externalId>false</externalId>
    <label>Type</label>
    <required>false</required>
    <trackFeedHistory>true</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Picklist</type>
    <valueSet>
        <restricted>true</restricted>
        <valueSetDefinition>
            <sorted>false</sorted>
            <value>
                <fullName>Feature</fullName>
                <default>false</default>
                <label>Feature</label>
            </value>
            <value>
                <fullName>Bug</fullName>
                <default>false</default>
                <label>Bug</label>
            </value>
            <value>
                <fullName>Release</fullName>
                <default>false</default>
                <label>Release</label>
            </value>
            <value>
                <fullName>Chore</fullName>
                <default>false</default>
                <label>Chore</label>
            </value>
        </valueSetDefinition>
    </valueSet>
</CustomField>
```
### pt_created_at__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_created_at__c</fullName>
    <externalId>false</externalId>
    <label>pt_created_at</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### pt_accepted_at__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_accepted_at__c</fullName>
    <externalId>false</externalId>
    <label>pt_accepted_at</label>
    <length>255</length>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Text</type>
    <unique>false</unique>
</CustomField>
```
### pt_requested_by_id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_requested_by_id__c</fullName>
    <externalId>false</externalId>
    <label>pt_requested_by_id</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### pt_url__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_url__c</fullName>
    <externalId>false</externalId>
    <label>pt_url</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Url</type>
</CustomField>
```
### Delivered_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Delivered_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Delivered Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### Unstarted_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Unstarted_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Unstarted Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```
### pt_id__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_id__c</fullName>
    <externalId>true</externalId>
    <label>pt_id</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### pt_estimate__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>pt_estimate__c</fullName>
    <externalId>false</externalId>
    <label>pt_estimate</label>
    <precision>18</precision>
    <required>false</required>
    <scale>0</scale>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>Number</type>
    <unique>false</unique>
</CustomField>
```
### Accepted_Timestamp__c

```
<?xml version="1.0" encoding="UTF-8"?>
<CustomField xmlns="http://soap.sforce.com/2006/04/metadata">
    <fullName>Accepted_Timestamp__c</fullName>
    <externalId>false</externalId>
    <label>Accepted Timestamp</label>
    <required>false</required>
    <trackFeedHistory>false</trackFeedHistory>
    <trackHistory>false</trackHistory>
    <trackTrending>false</trackTrending>
    <type>DateTime</type>
</CustomField>
```

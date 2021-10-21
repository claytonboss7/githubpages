---
layout: default
title: GroundTriggerHandler
parent: classes
---
# Metadata Type
classes


# Filename 
GroundTriggerHandler


# Raw XML
```
public class GroundTriggerHandler{
    //--------------------Handler Methods----------------------
    public static void populateFields(Map<Id, Ground__c> oldGroundMap, List<Ground__c> grounds){
        Map<Id, Ground__c> subTripsMap = new Map<Id, Ground__c>();
        for(Ground__c ground : grounds){
            if(ground.Service_Type__c != null){
                ground.Service_Type_Text__c = '';
                for(String service : ground.Service_Type__c.split(';')) if(service.trim() != '') ground.Service_Type_Text__c = ground.Service_Type_Text__c + service.trim() + ';';
            }
            if(String.isNotEmpty(ground.Status_Ground__c) && (oldGroundMap == null || ground.Status_Ground__c != oldGroundMap.get(ground.Id).Status_Ground__c)) ground.Status_Change_Date__c = Date.Today();
            else if(oldGroundMap != null && String.isEmpty(ground.Status_Ground__c) && ground.Status_Ground__c != oldGroundMap.get(ground.Id).Status_Ground__c) ground.Status_Change_Date__c = null;
        } 
    }
    public static void populateCongaFields(Map<Id, Ground__c> oldGroundMap, List<Ground__c> grounds){
        Map<Id, Ground__c> subTripsMap = new Map<Id, Ground__c>();
        for(Ground__c ground : grounds) if(Schema.SObjectType.Ground__c.getRecordTypeInfosByName().get('GT Travel Details') != null && ground.recordtypeId.equals(Schema.SObjectType.Ground__c.getRecordTypeInfosByName().get('GT Travel Details').getRecordTypeId()) && ground.GT_Sub_Trip_Details__c != null && (oldGroundMap == null || (ground.recordtypeId != oldGroundMap.get(ground.Id).recordtypeId || ground.GT_Sub_Trip_Details__c != oldGroundMap.get(ground.Id).GT_Sub_Trip_Details__c || ground.Line__c != oldGroundMap.get(ground.Id).Line__c || ground.Vehicle_Ref__c != oldGroundMap.get(ground.Id).Vehicle_Ref__c || ground.Start_Date__c != oldGroundMap.get(ground.Id).Start_Date__c || ground.Start_Date_Time__c != oldGroundMap.get(ground.Id).Start_Date_Time__c || ground.End_Date__c != oldGroundMap.get(ground.Id).End_Date__c || ground.End_Date_Time__c != oldGroundMap.get(ground.Id).End_Date_Time__c || ground.End_Date_Time__c != oldGroundMap.get(ground.Id).End_Date_Time__c || ground.Travel_Type__c != oldGroundMap.get(ground.Id).Travel_Type__c || ground.Group_Type__c != oldGroundMap.get(ground.Id).Group_Type__c || ground.Location_Pick_up__c != oldGroundMap.get(ground.Id).Location_Pick_up__c || ground.Location_Drop_off__c != oldGroundMap.get(ground.Id).Location_Drop_off__c || ground.Location_Details__c != oldGroundMap.get(ground.Id).Location_Details__c || ground.Airline_Info_Special_Notes__c != oldGroundMap.get(ground.Id).Airline_Info_Special_Notes__c))) subTripsMap.put(ground.GT_Sub_Trip_Details__c, new Ground__c(id = ground.GT_Sub_Trip_Details__c, Travel_Information_Conga__c = ''));
        if(!subTripsMap.values().isEmpty()){
            for(Ground__c ground : [Select id, GT_Sub_Trip_Details__c, Vehicle_Ref__c, Start_Date__c, Start_Date_Time__c, End_Date__c, End_Date_Time__c, Travel_Type__c, Group_Type__c, Location_Pick_up__c, Location_Drop_off__c, Location_Details__c, Airline_Info_Special_Notes__c from Ground__c where GT_Sub_Trip_Details__c in:subTripsMap.keySet() and RecordType.DeveloperName = 'GT_Travel_Details' order by Line__c]) subTripsMap.get(ground.GT_Sub_Trip_Details__c).Travel_Information_Conga__c += '<tr><td width="55" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + ground.Vehicle_Ref__c + '</td><td width="80" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (ground.Start_Date__c != null ? Datetime.newInstance(ground.Start_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd-MMM-yyyy') : '') + '</td><td width="55" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (ground.Start_Date__c != null && ground.Start_Date_Time__c != null ? Datetime.newInstance(ground.Start_Date__c, ground.Start_Date_Time__c).format('h:mm a') : '') + '</td><td width="70" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (ground.End_Date__c != null ? Datetime.newInstance(ground.End_Date__c, Time.newInstance(0, 0, 0, 0)).format('dd-MMM-yyyy') : '') + '</td><td width="55" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (ground.End_Date__c != null && ground.End_Date_Time__c != null ? Datetime.newInstance(ground.End_Date__c, ground.End_Date_Time__c).format('h:mm a') : '') + '</td><td width="50" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (String.isNotEmpty(ground.Travel_Type__c) ? ground.Travel_Type__c : '') + '</td><td width="50" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (String.isNotEmpty(ground.Group_Type__c) ? ground.Group_Type__c : '') + '</td><td width="85" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (String.isNotEmpty(ground.Location_Pick_up__c) ? ground.Location_Pick_up__c : '') + '</td><td width="85" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (String.isNotEmpty(ground.Location_Drop_off__c) ? ground.Location_Drop_off__c : '') + '</td><td width="85" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (String.isNotEmpty(ground.Location_Details__c) ? ground.Location_Details__c : '') + '</td><td width="100" height="20" align="left" style="padding:3px 4px;border-bottom:1px dashed black">' + (String.isNotEmpty(ground.Airline_Info_Special_Notes__c) ? ground.Airline_Info_Special_Notes__c : '') + '</td></tr>';
            for(Ground__c ground:subTripsMap.values()) ground.Travel_Information_Conga__c = '<table width="100%" cellspacing="0" cellpadding="0" border="0" align="left" valign="middle"><thead><tr><th width="55" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">VEHICLE</th><th width="80" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">START DATE</th><th width="55" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">TIME</th><th width="70" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">END DATE</th><th width="55" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">TIME</th><th width="50" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">TYPE</th><th width="50" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">GROUP</th><th width="85" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">LOCATION <br/>PICK UP</th><th width="85" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">LOCATION DROP OFF</th><th width="85" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">LOCATION DETAILS</th><th width="100" height="20" align="left" style="padding:3px 4px;border-top:2px solid black;border-bottom:1px solid black">AIRLINE INFO/<br/>SPECIAL NOTES</th></tr></thead><tbody>' + ground.Travel_Information_Conga__c + '</tbody></table>';
            try{
                update subTripsMap.values();
            }
            catch(DmlException e){
                System.debug('GroundTriggerHandler - DmlException: ' + e.getMessage());
            }
        }
    }
    public static void createJournals(Map<Id, Ground__c> oldGroundMap, List<Ground__c> grounds){
        List<JournalCreation.JournalEntry> journalEntries = new List<JournalCreation.JournalEntry>();
        for(Ground__c ground : grounds){
            if(ground.Status_Ground__c != oldGroundMap.get(ground.Id).Status_Ground__c) 
                journalEntries.add(new JournalCreation.JournalEntry('ground',ground.Id,Schema.SObjectType.Journal__c.getRecordTypeInfosByDeveloperName().get('Trip_Journal').getRecordTypeId(),'GT status is changed to ' + ground.Status_Ground__c));
        }
        if(!journalEntries.isEmpty()) JournalCreation.insertJournal(journalEntries);
    }
    public static void createTraces(Map<Id, Ground__c> oldGroundMap, Map<Id, Ground__c> groundMap){
        Set<Id> productions = new Set<Id>();
        Map<Id,Id> coordinators = new Map<Id,Id>();
        List<Task> traces = new List<Task>();
        Id recordTypeTT = Schema.SObjectType.Task.getRecordTypeInfosByDeveloperName().get('Trace_Task').getRecordTypeId();
        Map<Id,Id> tracesForStayOrTrip = new Map<Id,Id>();
    
        for(Ground__c ground : groundMap.values()) productions.add(ground.Production_Ground__c);
        for(Production_Associations__c pa : [SELECT Production_Opp__c, User__c FROM Production_Associations__c WHERE Production_Opp__c = :productions AND Team_Roles__c INCLUDES ('Primary GT Coordinator')]) coordinators.put(pa.Production_Opp__c, pa.User__c);
        for(Task t : [SELECT Id, WhatId FROM Task WHERE WhatId =: groundMap.keySet() AND IsForStayOrTrip__c = true AND RecordType.Name = 'Trace Task' ORDER BY createddate]) tracesForStayOrTrip.put(t.WhatId, t.Id);
    
        for(Ground__c ground : groundMap.values()){
            if(ground.RecordTypeId == Schema.SObjectType.Ground__c.getRecordTypeInfosByDeveloperName().get('GT_Trip_Details').getRecordTypeId()
            && ground.Trace_Date__c != null && String.isNotEmpty(ground.Status_Ground__c) && (oldGroundMap == null || ground.Trace_Date__c != oldGroundMap.get(ground.Id).Trace_Date__c || ground.Status_Ground__c != oldGroundMap.get(ground.Id).Status_Ground__c) && coordinators.containsKey(ground.Production_Ground__c)){
                //system.debug('# createTraces() - add trace...');
                traces.add(new Task(
                    Id = tracesForStayOrTrip.containsKey(ground.Id) ? tracesForStayOrTrip.get(ground.Id) : null,
                    IsForStayOrTrip__c = true,
                    recordTypeId = recordTypeTT,
                    WhatId=ground.Id,
                    ActivityDate=ground.Trace_Date__c,
                    Deadline_Date__c=ground.Deadline_Date__c != null ? ground.Deadline_Date__c : null,
                    OwnerId=coordinators.get(ground.Production_Ground__c),
                    Subject=ground.Status_Ground__c,
                    Task_Type__c='Ground Status Trace'
                ));
            }
        }
        if(!traces.isEmpty()) upsert traces;
    }
}
```


# Last Modified


# Usage

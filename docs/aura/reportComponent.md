---
layout: default
title: reportComponent
parent: aura
---
# Metadata Type
CustomObject

# Name
reportComponent
## Fields
### reportComponentHelper

```
({
    getReportResponse : function(component, event, helper) {
        var action = component.get("c.getReportResponse");
		var report = component.get('v.reportId');
        action.setParams({
            reportId:component.get('v.selectedReport'),
            accountId:component.get('v.recordId')
        });
        action.setCallback(this, function(a){
			var reportResponseObj = JSON.parse(a.getReturnValue());

            component.set("v.tabResp", reportResponseObj.tabResp);
            component.set("v.sumResp", reportResponseObj.sumResp);
            component.set("v.reportResponse", reportResponseObj);
            component.set('v.loaded', !component.get('v.loaded'));

            // Display toast message to indicate load status
            var toastEvent = $A.get("e.force:showToast");
            if(action.getState() ==='SUCCESS'){
                toastEvent.setParams({
                    "title": "Report Loaded.",
                    "duration": 500
                });
            }else{
                toastEvent.setParams({
                    "title": "Error!",
                    "message": " Something has gone wrong."
                });
            }
            toastEvent.fire();
        });
         $A.enqueueAction(action);
    }   
})
```
### reportComponentController

```
({
    doInit : function(component, event, helper) {
        component.set('v.loaded', !component.get('v.loaded'));
        helper.getReportResponse(component, event, helper);   
    },
    loadReport : function(component, event, helper) {

    },
    showSpinner : function (component, event, helper) {

    },
    hideSpinner : function (component, event, helper) {

    },
    handleRefresh : function (component, event, helper) {
        component.set('v.loaded', !component.get('v.loaded'));
        helper.getReportResponse(component, event, helper);   
    }
})
```
### reportComponent

```
.THIS {

}
.THIS.exampleHolder{
    position: relative;
    display: inline-block;
    margin-left: 15px;
    width: 95%;
    height: 95%;
    vertical-align: middle;
    white-space: nowrap;
}
```
### reportComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportComponent

```
<aura:component controller="LightningReportsController" implements="force:appHostable,flexipage:availableForAllPageTypes,force:hasRecordId">

    <!-- Handle component initialization in a client-side controller -->
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>

    <!-- Handle loading events by displaying a spinner -->
    <aura:attribute name="loaded" type="Boolean" default="true" />
    <aura:attribute name="reportId" type="String" default="" />
    <aura:attribute name="selectedReport" type="String" default="" />
    <!-- Handle loading a report which was clicked on -->
	<aura:handler event="c:reportLoadEvent" action="{!c.loadReport}"/>    

    <!-- load all the reports for search -->
    <aura:attribute name="reportList" type="Report[]"/>
    
    <!-- Dynamically load the report rows -->
    <aura:attribute name="reportResponse" type="Object"/>    

    <div class="slds-scope">

        <div class="exampleHolder">
            <lightning:card title="Vendor Bid History"> 
                <aura:set attribute="actions">
                    <lightning:icon iconName="standard:lightning_component" size="x-small" alternativeText="Success!" onclick="{!c.handleRefresh}"/>
                </aura:set>
                <aura:if isTrue="{! v.loaded }">
                    <div class="slds-scrollable">

                        <div data-role="page" data-theme="d" id="reportPage">   
                            <div role="main" class="">    
                                
                                <ul data-role="listview" data-filter="true" data-filter-reveal="true" data-filter-placeholder="Search reports..." data-inset="true">
                                    <aura:iteration var="report" items="{!v.reportList}">
                                        <c:reportSearchComponent report="{!report}" />
                                    </aura:iteration>
                                </ul>
                                
                                <!-- this is how tabular and matrix reports are displayed -->
                                <!-- Iterate over the list of report rows and display them -->
                                <!-- special case for the header row -->
                                <lightning:layout>
                                    <lightning:layoutItem>

                                        <article class="slds-card_boundary">

                                            <div style="border: 1px solid rgb(101, 153, 205);" class="slds box">
                                                <table class="slds-table slds-table_cell-buffer slds-table_bordered slds-table_col-bordered">
                                            
                                                    <aura:renderIf isTrue="{!v.reportResponse.reportType == 'summary' ? false : true}">
                                                        <thead>
                                                            <c:reportRowComponent row="{!v.reportResponse.tabResp.reportFields}" isHeader="true"/>
                                                        </thead>
                                                        <tbody>
                                                            <aura:iteration var="row" items="{!v.reportResponse.tabResp.fieldDataList}">
                                                                <c:reportRowComponent row="{!row}" isHeader="false"/>
                                                            </aura:iteration>
                                                        </tbody>
                                                        <aura:set attribute="else">
                                                            <!-- this is how summary reports are displayed -->
                                                            <thead>
                                                                <c:reportRowComponent row="{!v.reportResponse.sumResp.reportFields}" isHeader="true"/>
                                                            </thead>
                                                            <tbody>
                                                                <aura:iteration var="group" items="{!v.reportResponse.sumResp.groupList}">
                                                                    <c:reportGroupComponent group="{!group}"/>
                                                                </aura:iteration>
                                                            </tbody>
                                                            
                                                        </aura:set>
                                                    </aura:renderIf>   
                                                    
                                                </table>
                                            </div>
                                        </article>
                                    </lightning:layoutItem>
                                </lightning:layout>
                    
                                    
                    
                            </div>
                        </div>     
                    </div>            
                    <aura:set attribute="else">
                        <lightning:spinner alternativeText="alternativeText" size="small" variant="base" />
                    </aura:set>
                </aura:if>
            </lightning:card>

        </div>
    </div>
</aura:component>
```
### reportComponent

```
<design:component>
  <design:attribute
    name="selectedReport"
    datasource="apex://ReportPickListValues"
  />
</design:component>
```
### reportComponentHelper

```
({
    getReportResponse : function(component, event, helper) {
        var action = component.get("c.getReportResponse");
		var report = component.get('v.reportId');
        action.setParams({
            reportId:component.get('v.selectedReport'),
            accountId:component.get('v.recordId')
        });
        action.setCallback(this, function(a){
			var reportResponseObj = JSON.parse(a.getReturnValue());

            component.set("v.tabResp", reportResponseObj.tabResp);
            component.set("v.sumResp", reportResponseObj.sumResp);
            component.set("v.reportResponse", reportResponseObj);
            component.set('v.loaded', !component.get('v.loaded'));

            // Display toast message to indicate load status
            var toastEvent = $A.get("e.force:showToast");
            if(action.getState() ==='SUCCESS'){
                toastEvent.setParams({
                    "title": "Report Loaded.",
                    "duration": 500
                });
            }else{
                toastEvent.setParams({
                    "title": "Error!",
                    "message": " Something has gone wrong."
                });
            }
            toastEvent.fire();
        });
         $A.enqueueAction(action);
    }   
})
```
### reportComponentController

```
({
    doInit : function(component, event, helper) {
        component.set('v.loaded', !component.get('v.loaded'));
        helper.getReportResponse(component, event, helper);   
    },
    loadReport : function(component, event, helper) {

    },
    showSpinner : function (component, event, helper) {

    },
    hideSpinner : function (component, event, helper) {

    },
    handleRefresh : function (component, event, helper) {
        component.set('v.loaded', !component.get('v.loaded'));
        helper.getReportResponse(component, event, helper);   
    }
})
```
### reportComponent

```
.THIS {

}
.THIS.exampleHolder{
    position: relative;
    display: inline-block;
    margin-left: 15px;
    width: 95%;
    height: 95%;
    vertical-align: middle;
    white-space: nowrap;
}
```
### reportComponent

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>52.0</apiVersion>
    <description>DESCRIPTION</description>
</AuraDefinitionBundle>
```
### reportComponent

```
<aura:component controller="LightningReportsController" implements="force:appHostable,flexipage:availableForAllPageTypes,force:hasRecordId">

    <!-- Handle component initialization in a client-side controller -->
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>

    <!-- Handle loading events by displaying a spinner -->
    <aura:attribute name="loaded" type="Boolean" default="true" />
    <aura:attribute name="reportId" type="String" default="" />
    <aura:attribute name="selectedReport" type="String" default="" />
    <!-- Handle loading a report which was clicked on -->
	<aura:handler event="c:reportLoadEvent" action="{!c.loadReport}"/>    

    <!-- load all the reports for search -->
    <aura:attribute name="reportList" type="Report[]"/>
    
    <!-- Dynamically load the report rows -->
    <aura:attribute name="reportResponse" type="Object"/>    

    <div class="slds-scope">

        <div class="exampleHolder">
            <lightning:card title="Vendor Bid History"> 
                <aura:set attribute="actions">
                    <lightning:icon iconName="standard:lightning_component" size="x-small" alternativeText="Success!" onclick="{!c.handleRefresh}"/>
                </aura:set>
                <aura:if isTrue="{! v.loaded }">
                    <div class="slds-scrollable">

                        <div data-role="page" data-theme="d" id="reportPage">   
                            <div role="main" class="">    
                                
                                <ul data-role="listview" data-filter="true" data-filter-reveal="true" data-filter-placeholder="Search reports..." data-inset="true">
                                    <aura:iteration var="report" items="{!v.reportList}">
                                        <c:reportSearchComponent report="{!report}" />
                                    </aura:iteration>
                                </ul>
                                
                                <!-- this is how tabular and matrix reports are displayed -->
                                <!-- Iterate over the list of report rows and display them -->
                                <!-- special case for the header row -->
                                <lightning:layout>
                                    <lightning:layoutItem>

                                        <article class="slds-card_boundary">

                                            <div style="border: 1px solid rgb(101, 153, 205);" class="slds box">
                                                <table class="slds-table slds-table_cell-buffer slds-table_bordered slds-table_col-bordered">
                                            
                                                    <aura:renderIf isTrue="{!v.reportResponse.reportType == 'summary' ? false : true}">
                                                        <thead>
                                                            <c:reportRowComponent row="{!v.reportResponse.tabResp.reportFields}" isHeader="true"/>
                                                        </thead>
                                                        <tbody>
                                                            <aura:iteration var="row" items="{!v.reportResponse.tabResp.fieldDataList}">
                                                                <c:reportRowComponent row="{!row}" isHeader="false"/>
                                                            </aura:iteration>
                                                        </tbody>
                                                        <aura:set attribute="else">
                                                            <!-- this is how summary reports are displayed -->
                                                            <thead>
                                                                <c:reportRowComponent row="{!v.reportResponse.sumResp.reportFields}" isHeader="true"/>
                                                            </thead>
                                                            <tbody>
                                                                <aura:iteration var="group" items="{!v.reportResponse.sumResp.groupList}">
                                                                    <c:reportGroupComponent group="{!group}"/>
                                                                </aura:iteration>
                                                            </tbody>
                                                            
                                                        </aura:set>
                                                    </aura:renderIf>   
                                                    
                                                </table>
                                            </div>
                                        </article>
                                    </lightning:layoutItem>
                                </lightning:layout>
                    
                                    
                    
                            </div>
                        </div>     
                    </div>            
                    <aura:set attribute="else">
                        <lightning:spinner alternativeText="alternativeText" size="small" variant="base" />
                    </aura:set>
                </aura:if>
            </lightning:card>

        </div>
    </div>
</aura:component>
```
### reportComponent

```
<design:component>
  <design:attribute
    name="selectedReport"
    datasource="apex://ReportPickListValues"
  />
</design:component>
```

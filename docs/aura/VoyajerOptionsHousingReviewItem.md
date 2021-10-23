---
layout: default
title: VoyajerOptionsHousingReviewItem
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsHousingReviewItem
## Fields
### VoyajerOptionsHousingReviewItem

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerOptionsHousingReviewItem

```
<aura:component>
    <aura:attribute type="String" name="housingId" />
    <aura:attribute type="Integer" name="optionIndex" />
    <aura:attribute type="String" name="comments" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:registerEvent name='callToParent' type='c:VoyajerCallToParent'/>
    <aura:handler name="change" value="{!v.comments}" action="{!c.changeComments}" />


    <div class="pageContentForm header">
        <div class="slds-grid slds-wrap">
            <div class="slds-col slds-size_1-of-1 optionBox">
                <div class="slds-grid slds-wrap" style="padding-bottom: 1em;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                        <div class="optionBoxName">
                            <p title="Report Name">{!v.optionDetailRecord.vendor}</p>
                        </div>
                        <div class="optionBoxDescription">
                            <p>
                                <aura:iteration items="{!v.optionDetailRecord.stars}" var="star">
                                    <i class="fas fa-star" style="color: #ffa000"></i>
                                </aura:iteration>
                            </p>
                            <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_venue}</p>
                            <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.optionDetailRecord.physical}</p>
                            <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">
                                <aura:if isTrue="{!and(v.optionDetailRecord.website != null, v.optionDetailRecord.website != '')}">
                                    <lightning:formattedText linkify="true" value="{!v.optionDetailRecord.website}" />
                                </aura:if>
                            </p>
                            <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_onevenue}</p>
                            <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                            <!--<p>
                            <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                            <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                            <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                            <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                        </p>-->
                            <p>
                                <a href="javascript:void(0)" data-bidindex="{!v.optionDetailRecordId}" onclick="{!c.openOptionDetail}" style="font-size: 12px;font-weight: bold;">
                                    VIEW DETAILS
                                </a>
                            </p>
                        </div>
                    </div>
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right;">
                        <div class="slds-grid slds-wrap">
                            <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;">
                                <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName}</span> | <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.dateIn} - {!v.serviceData.dateOut}</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;margin-bottom: 1em;">
                                <div class="slds-grid slds-wrap">
                                    <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_4-of-5">
                                            <span class="room-type" style="padding-right: 0.5em;">{!roomtype.Units__c}</span> - 
                                            <span class="room-type" style="padding-left: 0.5em;">{!roomtype.Unit_Type__c}</span>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5" style="text-align: right;">
                                            <span class="room-type" style="font-weight:bold;">
                                                <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                           style="currency" 
                                                                           currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                           currencyDisplayAs="symbol" />
                                                <!--${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}-->
                                            </span>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div style="margin-top: 1em;">
                                    <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                        Weighted Avg Rate
                                        <span style="margin-left: 1em;">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.avgrate}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            <!--${!v.optionDetailRecord.avgrate}-->
                                        </span>
                                    </span>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div style="margin-top: 1em;">
                                    <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                        Est. Total Cost
                                        <span style="margin-left: 1em;">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            <!--${!v.optionDetailRecord.avgrate}-->
                                        </span>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                        <span style="font-size: 12px;font-weight: bold;">Add Comments</span>
                    </div>
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                        <div class="formField">
                            <!-- Fix By Clay Dev 15 April, 2021 #177420809
                            <lightning:textarea aura:id="recordField" onchange="{!c.handleCommentsChange}" name="" label="" value="{!v.optionDetailRecord.optionComments}" variant="label-hidden" />
                            -->
        					<lightning:textarea rows="4" cols="50" maxlength="255" aura:id="recordField" onchange="{!c.handleCommentsChange}" name="" label="" value="{!v.optionDetailRecord.optionComments}" variant="label-hidden" />
                        	<div style="float:right;">{!((!v.optionDetailRecord.optionComments || v.optionDetailRecord.optionComments == null) ? 0 : v.optionDetailRecord.optionComments.length)} of 255</div>
                        </div>
                    </div>
                </div>
            </div>  
        </div>
    </div>
</aura:component>
```
### VoyajerOptionsHousingReviewItem

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>50.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingReviewItem

```
.THIS {
}
```
### VoyajerOptionsHousingReviewItemRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerOptionsHousingReviewItemHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerOptionsHousingReviewItem

```
<design:component >

</design:component>
```
### VoyajerOptionsHousingReviewItem

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerOptionsHousingReviewItemController

```
({
    handleCommentsChange : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","changeMultipleOptions");
        callToParent.setParam("data",{
            optionIndex: component.get('v.optionIndex'),
            optionData: component.get('v.optionDetailRecord'),
            optionComment: component.get('v.optionDetailRecord.optionComments')
        });
        callToParent.fire();
        console.log('fired event');
        console.log('optionIndex :: ' + component.get('v.optionIndex'));
    },
    changeComments : function(component, event, helper) {
        console.log('comments has changed ::: ' + component.get('v.comments'));
    }
})
```
### VoyajerOptionsHousingReviewItem

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerOptionsHousingReviewItem

```
<aura:component>
    <aura:attribute type="String" name="housingId" />
    <aura:attribute type="Integer" name="optionIndex" />
    <aura:attribute type="String" name="comments" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:registerEvent name='callToParent' type='c:VoyajerCallToParent'/>
    <aura:handler name="change" value="{!v.comments}" action="{!c.changeComments}" />


    <div class="pageContentForm header">
        <div class="slds-grid slds-wrap">
            <div class="slds-col slds-size_1-of-1 optionBox">
                <div class="slds-grid slds-wrap" style="padding-bottom: 1em;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                        <div class="optionBoxName">
                            <p title="Report Name">{!v.optionDetailRecord.vendor}</p>
                        </div>
                        <div class="optionBoxDescription">
                            <p>
                                <aura:iteration items="{!v.optionDetailRecord.stars}" var="star">
                                    <i class="fas fa-star" style="color: #ffa000"></i>
                                </aura:iteration>
                            </p>
                            <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_venue}</p>
                            <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.optionDetailRecord.physical}</p>
                            <p style="font-size: 12px;margin-right: 0.5em;font-weight:bold;color:#00b4ff;">
                                <aura:if isTrue="{!and(v.optionDetailRecord.website != null, v.optionDetailRecord.website != '')}">
                                    <lightning:formattedText linkify="true" value="{!v.optionDetailRecord.website}" />
                                </aura:if>
                            </p>
                            <p style="font-size: 12px;">{!v.optionDetailRecord.dx_to_onevenue}</p>
                            <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                            <!--<p>
                            <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                            <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                            <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                            <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                        </p>-->
                            <p>
                                <a href="javascript:void(0)" data-bidindex="{!v.optionDetailRecordId}" onclick="{!c.openOptionDetail}" style="font-size: 12px;font-weight: bold;">
                                    VIEW DETAILS
                                </a>
                            </p>
                        </div>
                    </div>
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align: right;">
                        <div class="slds-grid slds-wrap">
                            <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;">
                                <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName}</span> | <span style="font-weight:bold;color:#00b4ff;">{!v.serviceData.dateIn} - {!v.serviceData.dateOut}</span>
                            </div>
                            <div class="slds-col slds-size_1-of-1" style="margin-top: 1em;margin-bottom: 1em;">
                                <div class="slds-grid slds-wrap">
                                    <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_4-of-5">
                                            <span class="room-type" style="padding-right: 0.5em;">{!roomtype.Units__c}</span> - 
                                            <span class="room-type" style="padding-left: 0.5em;">{!roomtype.Unit_Type__c}</span>
                                        </div>
                                        <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-5" style="text-align: right;">
                                            <span class="room-type" style="font-weight:bold;">
                                                <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                           style="currency" 
                                                                           currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                           currencyDisplayAs="symbol" />
                                                <!--${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}-->
                                            </span>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div style="margin-top: 1em;">
                                    <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                        Weighted Avg Rate
                                        <span style="margin-left: 1em;">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.avgrate}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            <!--${!v.optionDetailRecord.avgrate}-->
                                        </span>
                                    </span>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div style="margin-top: 1em;">
                                    <span style="padding: 1em 0 0 3em;font-weight:bold;color:#00b4ff;font-style:italic;border-top: 1px solid #dbdbdb;">
                                        Est. Total Cost
                                        <span style="margin-left: 1em;">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            <!--${!v.optionDetailRecord.avgrate}-->
                                        </span>
                                    </span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="slds-grid slds-wrap" style="margin-top: 1em;">
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                        <span style="font-size: 12px;font-weight: bold;">Add Comments</span>
                    </div>
                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1">
                        <div class="formField">
                            <!-- Fix By Clay Dev 15 April, 2021 #177420809
                            <lightning:textarea aura:id="recordField" onchange="{!c.handleCommentsChange}" name="" label="" value="{!v.optionDetailRecord.optionComments}" variant="label-hidden" />
                            -->
        					<lightning:textarea rows="4" cols="50" maxlength="255" aura:id="recordField" onchange="{!c.handleCommentsChange}" name="" label="" value="{!v.optionDetailRecord.optionComments}" variant="label-hidden" />
                        	<div style="float:right;">{!((!v.optionDetailRecord.optionComments || v.optionDetailRecord.optionComments == null) ? 0 : v.optionDetailRecord.optionComments.length)} of 255</div>
                        </div>
                    </div>
                </div>
            </div>  
        </div>
    </div>
</aura:component>
```
### VoyajerOptionsHousingReviewItem

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>50.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingReviewItem

```
.THIS {
}
```
### VoyajerOptionsHousingReviewItemRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerOptionsHousingReviewItemHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerOptionsHousingReviewItem

```
<design:component >

</design:component>
```
### VoyajerOptionsHousingReviewItem

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerOptionsHousingReviewItemController

```
({
    handleCommentsChange : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","changeMultipleOptions");
        callToParent.setParam("data",{
            optionIndex: component.get('v.optionIndex'),
            optionData: component.get('v.optionDetailRecord'),
            optionComment: component.get('v.optionDetailRecord.optionComments')
        });
        callToParent.fire();
        console.log('fired event');
        console.log('optionIndex :: ' + component.get('v.optionIndex'));
    },
    changeComments : function(component, event, helper) {
        console.log('comments has changed ::: ' + component.get('v.comments'));
    }
})
```

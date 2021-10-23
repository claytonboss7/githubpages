---
layout: default
title: VoyajerHousingCloseOut
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerHousingCloseOut
## Fields
### VoyajerHousingCloseOutHelper

```
({
	calCommissionDue : function(component) {
        //productionRooms
		//productionRoom.roomNights
		//productionRoom.roomRate
        //productionRoom.roomCommission
        
        //lodgingRooms
        //lodgingRoom.roomNights
        //lodgingRoom.roomRate
        //lodgingRoom.roomCommission
        
        //roomRevenue.commissionType == 'Percentage'
        //roomRevenue.commissionType == 'Amount'
        //roomRevenue.commissionValue
        //roomRevenue.commissionDue
        console.log("# calCommissionDue() ");
        
        var productionRooms = component.get("v.productionRooms");
        var lodgingRooms = component.get("v.lodgingRooms");
        var roomRevenue = component.get("v.roomRevenue");
        
        console.log("# productionRooms = " + JSON.stringify(productionRooms));
        console.log("# lodgingRooms = " + JSON.stringify(lodgingRooms));
        console.log("# roomRevenue = " + JSON.stringify(roomRevenue));
        
        var result = 0;
        var s1 = 0;
        var s2 = 0;
        
        productionRooms.forEach(r => {
            if(parseFloat(r.roomNights) > 0 && parseFloat(r.roomRate) > 0){
            	result = 0;
            	if(roomRevenue.commissionType == 'Amount'){
            		console.log('# Amount');
            		result = parseFloat(r.roomNights * roomRevenue.commissionValue);
                }else if(roomRevenue.commissionType == 'Percentage'){
            		console.log('# Percentage');
            		result = parseFloat( r.roomNights * r.roomRate * (roomRevenue.commissionValue/100) );
        		}
        		console.log('# result = ' + result);
                s1 += result;
        		if(result>0) r.roomCommission = result;
        	}
        });

        lodgingRooms.forEach(r => {
            if(parseFloat(r.roomNights) > 0 && parseFloat(r.roomRate) > 0){
            	result = 0;
            	if(roomRevenue.commissionType == 'Amount'){
            		console.log('# Amount');
            		result = parseFloat(r.roomNights * roomRevenue.commissionValue);
                }else if(roomRevenue.commissionType == 'Percentage'){
            		console.log('# Percentage');
            		result = parseFloat( r.roomNights * r.roomRate * (roomRevenue.commissionValue/100) );
        		}
        		console.log('# result = ' + result);
                s2 += result;
                if(result>0) r.roomCommission = result;
        	}
        });
        
		console.log("# s1 = " + s1);
		console.log("# s2 = " + s2);

        if(s1>0 || s2>0){
            var with2Decimals = s1.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0];
            s1 = parseFloat(with2Decimals);
            
            var with2Decimals = s2.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0];
            s2 = parseFloat(with2Decimals);
            
            console.log("# s1 new = " + s1);
            console.log("# s2 new = " + s2);
            roomRevenue.commissionDue = s1+s2;
            //update
            component.set("v.productionRooms",productionRooms);
            component.set("v.lodgingRooms",lodgingRooms);
        	component.set("v.roomRevenue",roomRevenue);
        }

        return 0;
	}
})
```
### VoyajerHousingCloseOutController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadCloseOut");
        callToParent.fire();
	},
    
    loadCloseOutData : function(component, event, helper) {
        var closeOutData = component.get("v.closeOutData");
        console.log(closeOutData);
        component.set("v.isAccessible",closeOutData.isAccessible);
        component.set("v.roomTypes",closeOutData.roomTypes);
        component.set("v.revenueTypes",closeOutData.revenueTypes);
        component.set("v.chargeTypes",closeOutData.chargeTypes);
        component.set("v.rebates",closeOutData.rebates);
        component.set("v.productionRooms",closeOutData.productionRooms);
        component.set("v.lodgingRooms",closeOutData.lodgingRooms);
        component.set("v.revenues",closeOutData.revenues);
        component.set("v.roomRevenue",closeOutData.roomRevenue);
    },
    
    handleShowRooms : function(component, event, helper) {
        component.set("v.showRooms",!component.get("v.showRooms"));
    },
    
    handleShowRevenues : function(component, event, helper) {
        component.set("v.showRevenues",!component.get("v.showRevenues"));
    },
    
    handleAddLodgingRoom : function(component, event, helper) {
        var lodgingRecords = component.get("v.lodgingRooms");
        lodgingRecords.push({
            recordId: "",
            roomNights: 0,
            roomRate: 0,
            roomType: ""
        });
        component.set("v.lodgingRooms",lodgingRecords);
    },
    
    handleRemoveLodgingRoom : function(component, event, helper) {
        var indexRoom = parseInt(event.getSource().get("v.value"));
        var lodgingRecords = component.get("v.lodgingRooms");
        lodgingRecords.splice(indexRoom,1);
        component.set("v.lodgingRooms",lodgingRecords);
        var c = helper.calCommissionDue(component);
    },
    
    handleAddRevenue : function(component, event, helper) {
        var revenues = component.get("v.revenues");
        revenues.push({
            recordId: "",
            revenueType: "",
            revenueCharge: "",
            revenueValue: 0,
            revenuePer: "",
            revenueTotal: 0,
            revenueInvoice: 0
        });
        component.set("v.revenues",revenues);
    },
    
    handleRemoveRevenue : function(component, event, helper) {
        var indexRevenue = parseInt(event.getSource().get("v.value"));
        var revenues = component.get("v.revenues");
        revenues.splice(indexRevenue,1);
        component.set("v.revenues",revenues);
    },
    
    handleSaveCloseOut : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if (allValid) {
            var closeOut = {
                productionRooms: component.get("v.productionRooms"),
                lodgingRooms: component.get("v.lodgingRooms"),
                roomRevenue: component.get("v.roomRevenue"),
                revenues: component.get("v.revenues")
            }
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveCloseOut");
            callToParent.setParam("data",closeOut);
            callToParent.fire();
        } else {
            component.set("v.showRooms",true);
            component.set("v.showRevenues",true);
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleCalCommissionDue: function(component, event, helper) {
        console.log("# handleCalCommissionDue()");
        var c = helper.calCommissionDue(component);
    }
})
```
### VoyajerHousingCloseOut

```
<aura:component >
	<aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="Object" name="closeOutData" />
    <aura:attribute type="Object" name="roomRevenue" />
    <aura:attribute type="Boolean" name="showRooms" default="true" />
    <aura:attribute type="Boolean" name="showRevenues" default="true" />
    <aura:attribute type="Boolean" name="isAccessible" default="false" />
    <aura:attribute type="List" name="roomTypes" />
    <aura:attribute type="List" name="revenueTypes" />
    <aura:attribute type="List" name="chargeTypes" />
    <aura:attribute type="List" name="rebates" />
    <aura:attribute type="List" name="productionRooms" />
    <aura:attribute type="List" name="lodgingRooms" />
    <aura:attribute type="List" name="revenues" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.closeOutData}" action="{!c.loadCloseOutData}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <aura:if isTrue="{!v.isAccessible==true}">
            <div class="pageContent">
                <div class="pageContentSpaces">
                    <div class="page-section">
                        <div class="page-header">
                            <h1 style="display: flex; align-items: center;">
                                <lightning:icon iconName="utility:screen" alternativeText="Contact" size="small" />
                                <span style="padding-left: 0.25em;">Lodging Close Out</span>
                            </h1>
                            <lightning:button iconName="utility:copy" label="Save" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" />
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <div class="twoColumns">
                            <div class="recordDetailsCloseOut" style="{!v.showRooms!=true?'height: 3.75em;':''}">
                                <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                    <div class="recordTitleText">
                                        <div><i class="fas fa-bed titleIcon" style="color: white;"></i> Room Details</div>
                                    </div>
                                    <div class="recordTitleButton">
                                        <lightning:buttonIcon iconName="{!v.showRooms==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowRooms}" />
                                    </div>
                                </div>
                                <div class="recordBodyContent" style="{!v.showRooms!=true?'display: none;':''}">
                                    <div class="recordTable tableList" style="margin: 0;">
                                        <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;"></div>
                                            <div style="width: 7rem; text-align: center;">Room Nights</div>
                                            <div style="width: 7rem; text-align: center;">Room Rate</div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <aura:iteration items="{!v.productionRooms}" var="productionRoom">
                                            <div class="tableRow" style="border-top: 0;">
                                                <div class="addButtonColumn"></div>
                                                <div style="flex: 1;">
                                                    <lightning:formattedText value="{!productionRoom.roomType}" class="outputText" />
                                                </div>
                                                <div style="width: 7rem; justify-content: center;">
                                                    <lightning:input aura:id="recordField" type="number" value="{!productionRoom.roomNights}" label="" variant="label-hidden" step="1" class="closeOutInput" onchange="{!c.handleCalCommissionDue}"/>
                                                </div>
                                                <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                    <lightning:formattedNumber value="{!productionRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                </div>
                                                <div class="buttonColumn"></div>
                                            </div>
                                        </aura:iteration>
                                        <div class="tableRow">
                                            <div class="addButtonColumn" style="align-items: flex-start;">
                                                <lightning:button iconName="utility:add" label="Other" class="formButtonAction" onclick="{!c.handleAddLodgingRoom}" />
                                            </div>
                                            <div style="display: flex; flex: 1; flex-direction: column; padding: 0;">
                                                <aura:iteration items="{!v.lodgingRooms}" var="lodgingRoom" indexVar="roomIndex">
                                                    <div class="tableRow" style="border-top: 0;">
                                                        <div class="fieldSelect" style="flex: 1;">
                                                            <lightning:select name="Unit_Type__c" label="" variant="label-hidden" value="{!lodgingRoom.roomType}">
                                                                <option value="">-- None --</option>
                                                                <aura:iteration items="{!v.roomTypes}" var="roomType">
                                                                    <option value="{!roomType}">{!roomType}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </div>
                                                        <div style="width: 7rem; justify-content: center;">
                                                            <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomNights}" label="" variant="label-hidden" step="1" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" />
                                                        </div>
                                                        <div style="width: 7rem; justify-content: center;">
                                                            <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomRate}" label="Room rate" variant="label-hidden" step="0.01" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" />
                                                        </div>
                                                        <div class="buttonColumn">
                                                            <lightning:buttonIcon iconName="utility:clear" value="{!roomIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveLodgingRoom}" />
                                                        </div>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                        <div class="tableRow">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Comps:</div>
                                            <div style="width: 7rem; justify-content: center;">
                                                <lightning:input aura:id="recordField" value="{!v.roomRevenue.compsValue}" type="number" label="Comps" variant="label-hidden" step="1" class="closeOutInput" />
                                            </div>
                                            <div style="width: 7rem; justify-content: center;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Currency:</div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                <lightning:formattedText value="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}" class="outputText" />
                                            </div>
                                            <div style="width: 7rem; justify-content: center;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Commission:</div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                <!--<lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="percent" minimumFractionDigits="2"/>-->
                                                <aura:if isTrue="{!v.roomRevenue.commissionType == 'Percentage'}">
                                                    <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="decimal" maximumFractionDigits="2" minimumFractionDigits="2"/> %
                                                </aura:if>
                                                <aura:if isTrue="{!v.roomRevenue.commissionType == 'Amount'}">
                                                    <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                </aura:if>
                                            </div>
                                            <div style="width: 7rem; justify-content: center;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Commission Due:</div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                <lightning:formattedNumber value="{!v.roomRevenue.commissionDue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <div style="width: 7rem; justify-content: flex-end;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1; align-items: flex-start;">Notes:</div>
                                            <div style="width: 15.75rem; justify-content: center;">
                                                <lightning:textarea aura:id="recordField" name="Client_Notes__c" value="" label="" variant="label-hidden" onchange="{!c.handleInputChange}" class="notes" />
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="closeOutQuestions">
                                <div class="tableRow">
                                    <div style="flex: 1;">Do you need an invoice sent?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isInvoiceSent}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: 1;">Is this a monthly Pick Up?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isMonthlyPickUp}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>
                                <!--<div class="tableRow">
                                    <div style="flex: 1;">Does this match amount on pick up report?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isMatchingAmount}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>-->
                            </div>
                        </div>
                        <div class="recordDetails">
                            <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                <div class="recordTitleText">
                                    <div><i class="fas fa-dollar-sign titleIcon" style="color: white;"></i> Revenue Details</div>
                                </div>
                                <div class="recordTitleButton">
                                    <lightning:buttonIcon iconName="{!v.showRevenues==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowRevenues}" />
                                </div>
                            </div>
                            <div class="recordBodyContent" style="{!v.showRevenues!=true?'display: none;':''}">
                                <div class="recordTable tableList" style="margin: 0;">
                                    <div class="tableHeader">
                                        <div style="flex: 1; text-align: center;">Revenue Type</div>
                                        <div style="flex: 1; text-align: center;">Charge Type</div>
                                        <div style="flex: 1; text-align: center;">Amount/Percentage</div>
                                        <div style="flex: 1; text-align: center;">Rebate Per</div>
                                        <div style="flex: 1; text-align: center;">Total #</div>
                                        <div style="flex: 1; text-align: center;">Invoiced Amount</div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <aura:iteration items="{!v.revenues}" var="revenue" indexVar="revenueIndex">
                                        <div class="tableRow">
                                            <div style="flex: 1;" class="fieldSelect">
                                                <lightning:select name="Revenue_Type__c" value="{!revenue.revenueType}" label="" variant="label-hidden" class="revenueSelect">
                                                    <option value="">-- None --</option>
                                                    <aura:iteration items="{!v.revenueTypes}" var="revenueType">
                                                        <option value="{!revenueType}">{!revenueType}</option>
                                                    </aura:iteration>
                                                </lightning:select>
                                            </div>
                                            <div style="flex: 1;" class="fieldSelect">
                                                <lightning:select name="Charge_Type__c" value="{!revenue.revenueCharge}" label="" variant="label-hidden" class="revenueSelect">
                                                    <option value="">-- None --</option>
                                                    <aura:iteration items="{!v.chargeTypes}" var="chargeType">
                                                        <option value="{!chargeType}">{!chargeType}</option>
                                                    </aura:iteration>
                                                </lightning:select>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueValue}" name="RevenueValue" label="" variant="label-hidden" min="0.01" step="0.01" class="closeOutInput" />
                                            </div>
                                            <div style="flex: 1;" class="fieldSelect">
                                                <aura:if isTrue="{!revenue.revenueType=='Rebate'}">
                                                    <lightning:select name="Rebate_Per__c" value="{!revenue.revenuePer}" label="" variant="label-hidden" class="revenueSelect" onchange="{!c.handleInputChange}">
                                                        <option value="">-- None --</option>
                                                        <aura:iteration items="{!v.rebates}" var="rebate">
                                                            <option value="{!rebate}">{!rebate}</option>
                                                        </aura:iteration>
                                                    </lightning:select>
                                                </aura:if>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueTotal}" name="Total__c" label="" variant="label-hidden" min="1" step="1" class="closeOutInput" />
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueInvoice}" name="Invoice_Amount__c" label="" variant="label-hidden" min="0.01" step="0.01" class="closeOutInput" />
                                            </div>
                                            <div class="buttonColumn">
                                                <lightning:buttonIcon iconName="utility:clear" value="{!revenueIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveRevenue}" />
                                            </div>
                                        </div> 
                                    </aura:iteration>
                                </div>
                                <div class="actions">
                                    <lightning:button label="Add Revenue" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddRevenue}" />
                                </div>
                            </div>
                        </div>
                    </div>
                    <div style="display: flex; justify-content: flex-end; margin-top: 1em;">
                        <lightning:button iconName="utility:copy" label="Save" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" />
                    </div>
                </div>
            </div>
        </aura:if>
    </div>
</aura:component>
```
### VoyajerHousingCloseOut

```
.THIS {
}

.THIS .twoColumns {
    display: flex;
}

.THIS .recordDetailsCloseOut {
    border: 1px solid #dbdbdb;
    display: flex;
    flex-direction: column;
    background-color: white;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
    max-width: 45em;
    margin-right: 1em;
    flex: 2;
}

.THIS .recordDetailsCloseOut > div {
    display: flex;
}

.THIS .recordDetailsCloseOut .recordTitle {
    background-color: #f0f0f0;
    height: 3.75em;
}

.THIS .recordDetailsCloseOut .recordBodyContent {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableRow > div {
    display: flex;
    align-items: center;
}

.THIS .outputText {
    max-width: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.THIS .closeOutInput input {
    text-align: end;
}

.THIS .addButtonColumn {
    width: 7rem;
}

.THIS .fieldSelect label {
    display: none;
}

.THIS .revenueSelect {
    width: 100%;
}

.THIS .notes {
    width: 100%;
}

.THIS .closeOutQuestions {
    flex: 1;
}

.THIS .actions {
    display: flex;
    justify-content: flex-end;
    padding-top: 1em;
}
```
### VoyajerHousingCloseOut

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerHousingCloseOutHelper

```
({
	calCommissionDue : function(component) {
        //productionRooms
		//productionRoom.roomNights
		//productionRoom.roomRate
        //productionRoom.roomCommission
        
        //lodgingRooms
        //lodgingRoom.roomNights
        //lodgingRoom.roomRate
        //lodgingRoom.roomCommission
        
        //roomRevenue.commissionType == 'Percentage'
        //roomRevenue.commissionType == 'Amount'
        //roomRevenue.commissionValue
        //roomRevenue.commissionDue
        console.log("# calCommissionDue() ");
        
        var productionRooms = component.get("v.productionRooms");
        var lodgingRooms = component.get("v.lodgingRooms");
        var roomRevenue = component.get("v.roomRevenue");
        
        console.log("# productionRooms = " + JSON.stringify(productionRooms));
        console.log("# lodgingRooms = " + JSON.stringify(lodgingRooms));
        console.log("# roomRevenue = " + JSON.stringify(roomRevenue));
        
        var result = 0;
        var s1 = 0;
        var s2 = 0;
        
        productionRooms.forEach(r => {
            if(parseFloat(r.roomNights) > 0 && parseFloat(r.roomRate) > 0){
            	result = 0;
            	if(roomRevenue.commissionType == 'Amount'){
            		console.log('# Amount');
            		result = parseFloat(r.roomNights * roomRevenue.commissionValue);
                }else if(roomRevenue.commissionType == 'Percentage'){
            		console.log('# Percentage');
            		result = parseFloat( r.roomNights * r.roomRate * (roomRevenue.commissionValue/100) );
        		}
        		console.log('# result = ' + result);
                s1 += result;
        		if(result>0) r.roomCommission = result;
        	}
        });

        lodgingRooms.forEach(r => {
            if(parseFloat(r.roomNights) > 0 && parseFloat(r.roomRate) > 0){
            	result = 0;
            	if(roomRevenue.commissionType == 'Amount'){
            		console.log('# Amount');
            		result = parseFloat(r.roomNights * roomRevenue.commissionValue);
                }else if(roomRevenue.commissionType == 'Percentage'){
            		console.log('# Percentage');
            		result = parseFloat( r.roomNights * r.roomRate * (roomRevenue.commissionValue/100) );
        		}
        		console.log('# result = ' + result);
                s2 += result;
                if(result>0) r.roomCommission = result;
        	}
        });
        
		console.log("# s1 = " + s1);
		console.log("# s2 = " + s2);

        if(s1>0 || s2>0){
            var with2Decimals = s1.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0];
            s1 = parseFloat(with2Decimals);
            
            var with2Decimals = s2.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0];
            s2 = parseFloat(with2Decimals);
            
            console.log("# s1 new = " + s1);
            console.log("# s2 new = " + s2);
            roomRevenue.commissionDue = s1+s2;
            //update
            component.set("v.productionRooms",productionRooms);
            component.set("v.lodgingRooms",lodgingRooms);
        	component.set("v.roomRevenue",roomRevenue);
        }

        return 0;
	}
})
```
### VoyajerHousingCloseOutController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadCloseOut");
        callToParent.fire();
	},
    
    loadCloseOutData : function(component, event, helper) {
        var closeOutData = component.get("v.closeOutData");
        console.log(closeOutData);
        component.set("v.isAccessible",closeOutData.isAccessible);
        component.set("v.roomTypes",closeOutData.roomTypes);
        component.set("v.revenueTypes",closeOutData.revenueTypes);
        component.set("v.chargeTypes",closeOutData.chargeTypes);
        component.set("v.rebates",closeOutData.rebates);
        component.set("v.productionRooms",closeOutData.productionRooms);
        component.set("v.lodgingRooms",closeOutData.lodgingRooms);
        component.set("v.revenues",closeOutData.revenues);
        component.set("v.roomRevenue",closeOutData.roomRevenue);
    },
    
    handleShowRooms : function(component, event, helper) {
        component.set("v.showRooms",!component.get("v.showRooms"));
    },
    
    handleShowRevenues : function(component, event, helper) {
        component.set("v.showRevenues",!component.get("v.showRevenues"));
    },
    
    handleAddLodgingRoom : function(component, event, helper) {
        var lodgingRecords = component.get("v.lodgingRooms");
        lodgingRecords.push({
            recordId: "",
            roomNights: 0,
            roomRate: 0,
            roomType: ""
        });
        component.set("v.lodgingRooms",lodgingRecords);
    },
    
    handleRemoveLodgingRoom : function(component, event, helper) {
        var indexRoom = parseInt(event.getSource().get("v.value"));
        var lodgingRecords = component.get("v.lodgingRooms");
        lodgingRecords.splice(indexRoom,1);
        component.set("v.lodgingRooms",lodgingRecords);
        var c = helper.calCommissionDue(component);
    },
    
    handleAddRevenue : function(component, event, helper) {
        var revenues = component.get("v.revenues");
        revenues.push({
            recordId: "",
            revenueType: "",
            revenueCharge: "",
            revenueValue: 0,
            revenuePer: "",
            revenueTotal: 0,
            revenueInvoice: 0
        });
        component.set("v.revenues",revenues);
    },
    
    handleRemoveRevenue : function(component, event, helper) {
        var indexRevenue = parseInt(event.getSource().get("v.value"));
        var revenues = component.get("v.revenues");
        revenues.splice(indexRevenue,1);
        component.set("v.revenues",revenues);
    },
    
    handleSaveCloseOut : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if (allValid) {
            var closeOut = {
                productionRooms: component.get("v.productionRooms"),
                lodgingRooms: component.get("v.lodgingRooms"),
                roomRevenue: component.get("v.roomRevenue"),
                revenues: component.get("v.revenues")
            }
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","saveCloseOut");
            callToParent.setParam("data",closeOut);
            callToParent.fire();
        } else {
            component.set("v.showRooms",true);
            component.set("v.showRevenues",true);
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({
                type: "error",
                title: "",
                message: "Please update the invalid form entries and try again."
            });
            toastEvent.fire();
        }
    },
    
    handleCalCommissionDue: function(component, event, helper) {
        console.log("# handleCalCommissionDue()");
        var c = helper.calCommissionDue(component);
    }
})
```
### VoyajerHousingCloseOut

```
<aura:component >
	<aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="Object" name="closeOutData" />
    <aura:attribute type="Object" name="roomRevenue" />
    <aura:attribute type="Boolean" name="showRooms" default="true" />
    <aura:attribute type="Boolean" name="showRevenues" default="true" />
    <aura:attribute type="Boolean" name="isAccessible" default="false" />
    <aura:attribute type="List" name="roomTypes" />
    <aura:attribute type="List" name="revenueTypes" />
    <aura:attribute type="List" name="chargeTypes" />
    <aura:attribute type="List" name="rebates" />
    <aura:attribute type="List" name="productionRooms" />
    <aura:attribute type="List" name="lodgingRooms" />
    <aura:attribute type="List" name="revenues" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.closeOutData}" action="{!c.loadCloseOutData}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <aura:if isTrue="{!v.isAccessible==true}">
            <div class="pageContent">
                <div class="pageContentSpaces">
                    <div class="page-section">
                        <div class="page-header">
                            <h1 style="display: flex; align-items: center;">
                                <lightning:icon iconName="utility:screen" alternativeText="Contact" size="small" />
                                <span style="padding-left: 0.25em;">Lodging Close Out</span>
                            </h1>
                            <lightning:button iconName="utility:copy" label="Save" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" />
                        </div>
                    </div>
                    <div class="pageContentForm">
                        <div class="twoColumns">
                            <div class="recordDetailsCloseOut" style="{!v.showRooms!=true?'height: 3.75em;':''}">
                                <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                    <div class="recordTitleText">
                                        <div><i class="fas fa-bed titleIcon" style="color: white;"></i> Room Details</div>
                                    </div>
                                    <div class="recordTitleButton">
                                        <lightning:buttonIcon iconName="{!v.showRooms==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowRooms}" />
                                    </div>
                                </div>
                                <div class="recordBodyContent" style="{!v.showRooms!=true?'display: none;':''}">
                                    <div class="recordTable tableList" style="margin: 0;">
                                        <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;"></div>
                                            <div style="width: 7rem; text-align: center;">Room Nights</div>
                                            <div style="width: 7rem; text-align: center;">Room Rate</div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <aura:iteration items="{!v.productionRooms}" var="productionRoom">
                                            <div class="tableRow" style="border-top: 0;">
                                                <div class="addButtonColumn"></div>
                                                <div style="flex: 1;">
                                                    <lightning:formattedText value="{!productionRoom.roomType}" class="outputText" />
                                                </div>
                                                <div style="width: 7rem; justify-content: center;">
                                                    <lightning:input aura:id="recordField" type="number" value="{!productionRoom.roomNights}" label="" variant="label-hidden" step="1" class="closeOutInput" onchange="{!c.handleCalCommissionDue}"/>
                                                </div>
                                                <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                    <lightning:formattedNumber value="{!productionRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                </div>
                                                <div class="buttonColumn"></div>
                                            </div>
                                        </aura:iteration>
                                        <div class="tableRow">
                                            <div class="addButtonColumn" style="align-items: flex-start;">
                                                <lightning:button iconName="utility:add" label="Other" class="formButtonAction" onclick="{!c.handleAddLodgingRoom}" />
                                            </div>
                                            <div style="display: flex; flex: 1; flex-direction: column; padding: 0;">
                                                <aura:iteration items="{!v.lodgingRooms}" var="lodgingRoom" indexVar="roomIndex">
                                                    <div class="tableRow" style="border-top: 0;">
                                                        <div class="fieldSelect" style="flex: 1;">
                                                            <lightning:select name="Unit_Type__c" label="" variant="label-hidden" value="{!lodgingRoom.roomType}">
                                                                <option value="">-- None --</option>
                                                                <aura:iteration items="{!v.roomTypes}" var="roomType">
                                                                    <option value="{!roomType}">{!roomType}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </div>
                                                        <div style="width: 7rem; justify-content: center;">
                                                            <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomNights}" label="" variant="label-hidden" step="1" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" />
                                                        </div>
                                                        <div style="width: 7rem; justify-content: center;">
                                                            <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomRate}" label="Room rate" variant="label-hidden" step="0.01" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" />
                                                        </div>
                                                        <div class="buttonColumn">
                                                            <lightning:buttonIcon iconName="utility:clear" value="{!roomIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveLodgingRoom}" />
                                                        </div>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                        <div class="tableRow">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Comps:</div>
                                            <div style="width: 7rem; justify-content: center;">
                                                <lightning:input aura:id="recordField" value="{!v.roomRevenue.compsValue}" type="number" label="Comps" variant="label-hidden" step="1" class="closeOutInput" />
                                            </div>
                                            <div style="width: 7rem; justify-content: center;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Currency:</div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                <lightning:formattedText value="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}" class="outputText" />
                                            </div>
                                            <div style="width: 7rem; justify-content: center;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Commission:</div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                <!--<lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="percent" minimumFractionDigits="2"/>-->
                                                <aura:if isTrue="{!v.roomRevenue.commissionType == 'Percentage'}">
                                                    <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="decimal" maximumFractionDigits="2" minimumFractionDigits="2"/> %
                                                </aura:if>
                                                <aura:if isTrue="{!v.roomRevenue.commissionType == 'Amount'}">
                                                    <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                </aura:if>
                                            </div>
                                            <div style="width: 7rem; justify-content: center;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1;">Commission Due:</div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5em;">
                                                <lightning:formattedNumber value="{!v.roomRevenue.commissionDue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <div style="width: 7rem; justify-content: flex-end;"></div>
                                            <div class="buttonColumn"></div>
                                        </div>
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1; align-items: flex-start;">Notes:</div>
                                            <div style="width: 15.75rem; justify-content: center;">
                                                <lightning:textarea aura:id="recordField" name="Client_Notes__c" value="" label="" variant="label-hidden" onchange="{!c.handleInputChange}" class="notes" />
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="closeOutQuestions">
                                <div class="tableRow">
                                    <div style="flex: 1;">Do you need an invoice sent?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isInvoiceSent}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: 1;">Is this a monthly Pick Up?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isMonthlyPickUp}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>
                                <!--<div class="tableRow">
                                    <div style="flex: 1;">Does this match amount on pick up report?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isMatchingAmount}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>-->
                            </div>
                        </div>
                        <div class="recordDetails">
                            <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                <div class="recordTitleText">
                                    <div><i class="fas fa-dollar-sign titleIcon" style="color: white;"></i> Revenue Details</div>
                                </div>
                                <div class="recordTitleButton">
                                    <lightning:buttonIcon iconName="{!v.showRevenues==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowRevenues}" />
                                </div>
                            </div>
                            <div class="recordBodyContent" style="{!v.showRevenues!=true?'display: none;':''}">
                                <div class="recordTable tableList" style="margin: 0;">
                                    <div class="tableHeader">
                                        <div style="flex: 1; text-align: center;">Revenue Type</div>
                                        <div style="flex: 1; text-align: center;">Charge Type</div>
                                        <div style="flex: 1; text-align: center;">Amount/Percentage</div>
                                        <div style="flex: 1; text-align: center;">Rebate Per</div>
                                        <div style="flex: 1; text-align: center;">Total #</div>
                                        <div style="flex: 1; text-align: center;">Invoiced Amount</div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <aura:iteration items="{!v.revenues}" var="revenue" indexVar="revenueIndex">
                                        <div class="tableRow">
                                            <div style="flex: 1;" class="fieldSelect">
                                                <lightning:select name="Revenue_Type__c" value="{!revenue.revenueType}" label="" variant="label-hidden" class="revenueSelect">
                                                    <option value="">-- None --</option>
                                                    <aura:iteration items="{!v.revenueTypes}" var="revenueType">
                                                        <option value="{!revenueType}">{!revenueType}</option>
                                                    </aura:iteration>
                                                </lightning:select>
                                            </div>
                                            <div style="flex: 1;" class="fieldSelect">
                                                <lightning:select name="Charge_Type__c" value="{!revenue.revenueCharge}" label="" variant="label-hidden" class="revenueSelect">
                                                    <option value="">-- None --</option>
                                                    <aura:iteration items="{!v.chargeTypes}" var="chargeType">
                                                        <option value="{!chargeType}">{!chargeType}</option>
                                                    </aura:iteration>
                                                </lightning:select>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueValue}" name="RevenueValue" label="" variant="label-hidden" min="0.01" step="0.01" class="closeOutInput" />
                                            </div>
                                            <div style="flex: 1;" class="fieldSelect">
                                                <aura:if isTrue="{!revenue.revenueType=='Rebate'}">
                                                    <lightning:select name="Rebate_Per__c" value="{!revenue.revenuePer}" label="" variant="label-hidden" class="revenueSelect" onchange="{!c.handleInputChange}">
                                                        <option value="">-- None --</option>
                                                        <aura:iteration items="{!v.rebates}" var="rebate">
                                                            <option value="{!rebate}">{!rebate}</option>
                                                        </aura:iteration>
                                                    </lightning:select>
                                                </aura:if>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueTotal}" name="Total__c" label="" variant="label-hidden" min="1" step="1" class="closeOutInput" />
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueInvoice}" name="Invoice_Amount__c" label="" variant="label-hidden" min="0.01" step="0.01" class="closeOutInput" />
                                            </div>
                                            <div class="buttonColumn">
                                                <lightning:buttonIcon iconName="utility:clear" value="{!revenueIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveRevenue}" />
                                            </div>
                                        </div> 
                                    </aura:iteration>
                                </div>
                                <div class="actions">
                                    <lightning:button label="Add Revenue" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddRevenue}" />
                                </div>
                            </div>
                        </div>
                    </div>
                    <div style="display: flex; justify-content: flex-end; margin-top: 1em;">
                        <lightning:button iconName="utility:copy" label="Save" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" />
                    </div>
                </div>
            </div>
        </aura:if>
    </div>
</aura:component>
```
### VoyajerHousingCloseOut

```
.THIS {
}

.THIS .twoColumns {
    display: flex;
}

.THIS .recordDetailsCloseOut {
    border: 1px solid #dbdbdb;
    display: flex;
    flex-direction: column;
    background-color: white;
    box-shadow: 4px 4px 4px 0px #dbdbdb;
    max-width: 45em;
    margin-right: 1em;
    flex: 2;
}

.THIS .recordDetailsCloseOut > div {
    display: flex;
}

.THIS .recordDetailsCloseOut .recordTitle {
    background-color: #f0f0f0;
    height: 3.75em;
}

.THIS .recordDetailsCloseOut .recordBodyContent {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableRow > div {
    display: flex;
    align-items: center;
}

.THIS .outputText {
    max-width: 100%;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}

.THIS .closeOutInput input {
    text-align: end;
}

.THIS .addButtonColumn {
    width: 7rem;
}

.THIS .fieldSelect label {
    display: none;
}

.THIS .revenueSelect {
    width: 100%;
}

.THIS .notes {
    width: 100%;
}

.THIS .closeOutQuestions {
    flex: 1;
}

.THIS .actions {
    display: flex;
    justify-content: flex-end;
    padding-top: 1em;
}
```
### VoyajerHousingCloseOut

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

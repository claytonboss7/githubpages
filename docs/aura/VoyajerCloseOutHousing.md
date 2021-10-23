---
layout: default
title: VoyajerCloseOutHousing
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerCloseOutHousing
## Fields
### VoyajerCloseOutHousingHelper

```
({
	calCommissionDue : function(component) {
        var productionRooms = component.get("v.productionRooms");
        var lodgingRooms = component.get("v.lodgingRooms");
        var roomRevenue = component.get("v.roomRevenue");
        
        var result = 0;
        var s1 = 0;
        var s2 = 0;
        var compsValue = 0;
        
        productionRooms.forEach(function(r) {
            if(roomRevenue.commissionType == 'Amount') result = parseFloat( (r.roomNights - r.roomComps) * roomRevenue.commissionValue);
            else result = parseFloat( (r.roomNights - r.roomComps) * r.roomRate * (roomRevenue.commissionValue/100) );
            s1 += result;
            compsValue += parseFloat(r.roomComps);
            r.roomCommission = result;
        });
        
        lodgingRooms.forEach(function(r) {
            result = 0;
            if(roomRevenue.commissionType == 'Amount') result = parseFloat( (r.roomNights - r.roomComps) * roomRevenue.commissionValue);
            else result = parseFloat( (r.roomNights - r.roomComps) * r.roomRate * (roomRevenue.commissionValue/100) );
            s2 += result;
            compsValue += parseFloat(r.roomComps);
            r.roomCommission = result;
        });
        
        s1 = parseFloat(s1.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0]);
        s2 = parseFloat(s2.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0]);
        roomRevenue.commissionDue = s1+s2;
        roomRevenue.compsValue = parseFloat(compsValue.toString().match(/^\d+$/)[0]);
        //update
        component.set("v.productionRooms",productionRooms);
        component.set("v.lodgingRooms",lodgingRooms);
        component.set("v.roomRevenue",roomRevenue);
    },
    
    calRevenueDetails : function(component) {
        var revenues = component.get("v.revenues");
        revenues.forEach(function(r) {
            r.revenueInvoice = r.revenueValue * r.revenueTotal;
        });
        component.set("v.revenues",revenues);
    }
})
```
### VoyajerCloseOutHousing

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCloseOutHousing

```
<aura:component >
	<aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="serviceId" />
    <aura:attribute type="String" name="lodgingType" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="String" name="reviewName" default="" />
    <aura:attribute type="String" name="reviewTitle" default="" />
    <aura:attribute type="String" name="reviewEmail" default="" />
    <aura:attribute type="String" name="reviewPhone" default="" />
    <aura:attribute type="String" name="agreementText" default="Property agrees to negotiate with Road Rebel ONLY moving forward and not offer client lower rates directly. If either is breached, 
                                                                you agree to pay Road Rebel commission on any room pick-up at your property(s). This also serves as the commission agreement in the event we go to contract. 
                                                                By selecting Submit, you are signing this agreement electronically.*" />
    <aura:attribute type="String" name="isVatChanged" default="No" />
    <aura:attribute type="Object" name="closeOutRevenue" default=""/>
    <aura:attribute type="Object" name="closeOutData" />
    <aura:attribute type="Object" name="roomRevenue" />
    <aura:attribute type="Object" name="communitySign" />
    <aura:attribute type="Boolean" name="showRooms" default="true" />
    <aura:attribute type="Boolean" name="showRevenues" default="true" />
    <aura:attribute type="Boolean" name="showMonthlyPickUps" default="true" />
    <aura:attribute type="Boolean" name="isAccessible" default="false" />
    <aura:attribute type="Boolean" name="isReadOnly" default="false" />
    <aura:attribute type="Boolean" name="isSent" default="false" />
    <aura:attribute type="Boolean" name="isSync" default="false" />
    <aura:attribute type="List" name="roomTypes" />
    <aura:attribute type="List" name="revenueTypes" />
    <aura:attribute type="List" name="chargeTypes" />
    <aura:attribute type="List" name="rebates" />
    <aura:attribute type="List" name="productionRooms" />
    <aura:attribute type="List" name="lodgingRooms" />
    <aura:attribute type="List" name="revenues" />
    <aura:attribute type="List" name="monthlyPickUps" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.closeOutData}" action="{!c.loadCloseOutData}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    <aura:registerEvent type="c:VoyajerCallToParentGetRevenue" name="callToParentGetRevenue" />
    <aura:registerEvent type="c:VoyajerCallToParentUpdateVAT" name="callToParentUpdateVAT" />
    
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
                            <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button iconName="utility:copy" label="Submit" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" /></aura:if>
                        </div>
                    </div>
                    <div class="pageContentForm">
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
                                        <div style="flex: 1; min-width: 0; padding-left: 1.25rem;"></div>
                                        <div style="width: 7rem; text-align: center;">Room Nights</div>
                                        <div style="width: 4.5rem; text-align: center;">Comps</div>
                                        <div style="width: 6rem; text-align: center;">Room Rate</div>
                                        <div style="width: 8rem; text-align: center;">Room Revenue</div>
                                        <div style="width: 7rem; text-align: center;">Commission</div>
                                        <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                            <div style="width: 9.5rem; text-align: center;">Confirmation #(s)</div>
                                        </aura:if>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <aura:iteration items="{!v.productionRooms}" var="productionRoom">
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1; min-width: 0; padding-left: 1.25rem;">
                                                <lightning:formattedText value="{!productionRoom.roomType}" class="outputText" />
                                            </div>
                                            <div style="width: 7rem; justify-content: center;">
                                                <lightning:input aura:id="recordField" type="number" value="{!productionRoom.roomNights}" label="" variant="label-hidden" step="1" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                            </div>
                                            <div style="width: 4.5rem; justify-content: center;">
                                                <lightning:input aura:id="recordField" type="number" value="{!productionRoom.roomComps}" label="" variant="label-hidden" step="1" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                            </div>
                                            <div style="width: 6rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                <lightning:formattedNumber value="{!productionRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <div style="width: 8rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                <lightning:formattedNumber value="{!(productionRoom.roomNights-productionRoom.roomComps)*productionRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                <lightning:formattedNumber value="{!productionRoom.roomCommission}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                                <div style="width: 9.5rem; justify-content: center;">
                                                    <lightning:input aura:id="recordField" type="text" value="{!productionRoom.roomConfirmation}" label="" variant="label-hidden" class="closeOutInput" readonly="{!v.isReadOnly}" />
                                                </div>
                                            </aura:if>
                                            <div class="buttonColumn"></div>
                                        </div>
                                    </aura:iteration>
                                    <div class="tableRow">
                                        <div class="addButtonColumn" style="align-items: flex-start;">
                                            <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button iconName="utility:add" label="Other" class="formButtonAction" onclick="{!c.handleAddLodgingRoom}" /></aura:if>
                                        </div>
                                        <div style="display: flex; flex: 1; flex-direction: column; padding: 0;">
                                            <aura:iteration items="{!v.lodgingRooms}" var="lodgingRoom" indexVar="roomIndex">
                                                <div class="tableRow" style="border-top: 0;">
                                                    <div class="fieldSelect" style="{!'flex: 1; min-width: 0;' + (v.isReadOnly? ' padding-left: 1.25rem;' : '')}">
                                                        <aura:if isTrue="{!v.isReadOnly}">
                                                            <lightning:formattedText value="{!lodgingRoom.roomType}" class="outputText" />
                                                            <aura:set attribute="else">
                                                                <lightning:select name="Unit_Type__c" label="" variant="label-hidden" value="{!lodgingRoom.roomType}">
                                                                    <aura:iteration items="{!v.roomTypes}" var="roomType">
                                                                        <option value="{!roomType}">{!roomType}</option>
                                                                    </aura:iteration>
                                                                </lightning:select>
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                    <div style="width: 7rem; justify-content: center;">
                                                        <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomNights}" label="" variant="label-hidden" step="1" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                                    </div>
                                                    <div style="width: 4.5rem; justify-content: center;">
                                                        <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomComps}" label="" variant="label-hidden" step="1" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                                    </div>
                                                    <div style="{!'width: 6rem; justify-content: center;' + (v.isReadOnly? ' padding-left: 1.25rem;' : '')}">
                                                        <aura:if isTrue="{!v.isReadOnly}">
                                                            <lightning:formattedNumber value="{!lodgingRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                            <aura:set attribute="else">
                                                                <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomRate}" label="" variant="label-hidden" step="0.01" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                    <div style="width: 8rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                        <lightning:formattedNumber value="{!(lodgingRoom.roomNights-lodgingRoom.roomComps)*lodgingRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                    </div>
                                                    <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                        <lightning:formattedNumber value="{!lodgingRoom.roomCommission}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                    </div>
                                                    <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                                        <div style="width: 9.5rem; justify-content: center;">
                                                            <lightning:input aura:id="recordField" type="text" value="{!lodgingRoom.roomConfirmation}" label="" variant="label-hidden" class="closeOutInput" readonly="{!v.isReadOnly}" />
                                                        </div>
                                                    </aura:if>
                                                    <div class="buttonColumn">
                                                        <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:buttonIcon iconName="utility:clear" value="{!roomIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveLodgingRoom}" /></aura:if>
                                                    </div>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                    <div class="tableRow">
                                        <div class="addButtonColumn"></div>
                                        <div style="flex: 1; min-width: 0;">Comps:</div>
                                        <div style="width: 7rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <lightning:input aura:id="recordField" value="{!v.roomRevenue.compsValue}" type="number" label="Comps" variant="label-hidden" step="1" class="closeOutInput" readonly="{!v.isReadOnly}" />
                                        </div>
                                         <div style="{!'width: 6rem; justify-content: center;' + (v.isReadOnly? ' padding-left: 1.25rem;' : '')}"></div>
                                        <div style="width: 8rem; justify-content: flex-end; padding-right: 1.5rem;"></div>
                                        <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5rem;"></div>
                                        <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                            <div style="width: 9.5rem; justify-content: center;"></div>
                                        </aura:if>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem;">Currency:</div>
                                        <div style="width: 6.5rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <lightning:formattedText value="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}" class="outputText" />
                                        </div>
                                        <div style="flex: 1;"></div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem;">Commission:</div>
                                        <div style="width: 6.5rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <!--<lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="percent" minimumFractionDigits="2"/>-->
                                            <aura:if isTrue="{!v.roomRevenue.commissionType == 'Percentage'}">
                                                <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="decimal" maximumFractionDigits="2" minimumFractionDigits="2"/> %
                                            </aura:if>
                                            <aura:if isTrue="{!v.roomRevenue.commissionType == 'Amount'}">
                                                <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </aura:if>
                                        </div>
                                        <div style="flex: 1;"></div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem;">Commission Due:</div>
                                        <div style="width: 6.5rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <lightning:formattedNumber value="{!v.roomRevenue.commissionDue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                        </div>
                                        <div style="flex: 1;"></div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem; align-items: flex-start;">Notes:</div>
                                        <div style="flex: 1; justify-content: center;">
                                            <lightning:textarea aura:id="recordField" name="Notes__c" value="{!v.roomRevenue.commissionNotes}" label="" variant="label-hidden" onchange="{!c.handleInputChange}" class="notes" readonly="{!v.isReadOnly}" />
                                        </div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="closeOutQuestions" style="display: flex; margin-top: 1em; min-height: 3rem;">
                            <div class="tableRow">
                                <div>Do you need an invoice sent?</div>
                                <div><lightning:input type="toggle" checked="{!v.roomRevenue.isInvoiceSent}" label="option" variant="label-hidden" messageToggleActive="" messageToggleInactive="" disabled="{!v.isReadOnly}" /></div>
                            </div>
                            <div class="tableRow">
                                    <div>Indicate Dates</div>
                                    <div><lightning:input type="text" aura:id="recordField" label="option" variant="label-hidden" value="{!v.roomRevenue.indicateDates}" required="true" readonly="{!v.isReadOnly}" /></div>
                            </div>
                            <!--<div class="tableRow">
                                    <div style="flex: 1;">Does this match amount on pick up report?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isMatchingAmount}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>-->
                        </div>
                        <div class="recordDetails" style="margin-top: 1em;">
                            <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                <div class="recordTitleText">
                                    <div><i class="fas fa-dollar-sign titleIcon" style="color: white;"></i> Update VAT Details</div>
                                </div>
                            </div>
                            <div class="slds-grid">
                            	<div class="slds-col" style="padding: 5px;">
                                    <lightning:input disabled="{!v.isVatChanged == 'No'}" name="VATNumber" label="VAT Number" value="{!v.closeOutData.vatnumber}"/>
                                </div>
                                <div class="slds-col" style="padding: 5px;">
                                    <lightning:input disabled="{!v.isVatChanged == 'No'}" name="Address" label="Address" value="{!v.closeOutData.address}" />
                                </div>
                                <div class="slds-col" style="padding: 5px;">
                                    <lightning:Select name="isChanged" label="VAT Changed?" value="{!v.isVatChanged}">
                                        <option value="No">No</option>
                                        <option value="Yes">Yes</option>
                                    </lightning:Select>
                                </div>
                            </div>
                            <br/>
                            <aura:if isTrue="{!v.isVatChanged == 'Yes'}">
                            	<div class="slds-grid">
                                <div class="slds-col" style="padding: 5px;">
                                    <lightning:button label="Update VAT" class="formButtonAction" onclick="{!c.updateVAT}"/>
                                </div>
                            </div>
                            </aura:if>
                        </div>
                        <div class="recordDetails" style="margin-top: 1em;">
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
                                            <div class="fieldSelect" style="{!'flex: 1;' + (v.isReadOnly? ' justify-content: center;' : '')}">
                                                <aura:if isTrue="{!v.isReadOnly}">
                                                    <lightning:formattedText value="{!revenue.revenueType}" class="outputText" />
                                                    <aura:set attribute="else">
                                                        <lightning:select name="Revenue_Type__c" value="{!revenue.revenueType}" label="" variant="label-hidden" class="revenueSelect">
                                                            <option value="">-- None --</option>
                                                            <aura:iteration items="{!v.revenueTypes}" var="revenueType">
                                                                <option value="{!revenueType}">{!revenueType}</option>
                                                            </aura:iteration>
                                                        </lightning:select>
                                                    </aura:set>
                                                </aura:if>
                                            </div>
                                            <div class="fieldSelect" style="{!'flex: 1;' + (v.isReadOnly? ' justify-content: center;' : '')}">
                                                <aura:if isTrue="{!v.isReadOnly}">
                                                    <lightning:formattedText value="{!revenue.revenueCharge}" class="outputText" />
                                                    <aura:set attribute="else">
                                                        <lightning:select name="Charge_Type__c" value="{!revenue.revenueCharge}" label="" variant="label-hidden" class="revenueSelect">
                                                            <option value="">-- None --</option>
                                                            <aura:iteration items="{!v.chargeTypes}" var="chargeType">
                                                                <option value="{!chargeType}">{!chargeType}</option>
                                                            </aura:iteration>
                                                        </lightning:select>
                                                    </aura:set>
                                                </aura:if>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueValue}" name="RevenueValue" label="" variant="label-hidden" min="0.01" step="0.01" class="closeOutInput" onchange="{!c.handleCalRevenueDetails}" readonly="{!v.isReadOnly}" />
                                            </div>
                                            <div class="fieldSelect" style="{!'flex: 1;' + (v.isReadOnly? ' justify-content: center;' : '')}">
                                                <aura:if isTrue="{!revenue.revenueType=='Rebate'}">
                                                    <aura:if isTrue="{!v.isReadOnly}">
                                                        <lightning:formattedText value="{!revenue.revenuePer}" class="outputText" />
                                                        <aura:set attribute="else">
                                                            <lightning:select name="Rebate_Per__c" value="{!revenue.revenuePer}" label="" variant="label-hidden" class="revenueSelect" onchange="{!c.handleInputChange}">
                                                                <option value="">-- None --</option>
                                                                <aura:iteration items="{!v.rebates}" var="rebate">
                                                                    <option value="{!rebate}">{!rebate}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </aura:set>
                                                    </aura:if>
                                                </aura:if>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueTotal}" name="Total__c" label="" variant="label-hidden" min="1" step="1" class="closeOutInput" readonly="{!v.isReadOnly}" onchange="{!c.handleCalRevenueDetails}" />
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueInvoice}" name="Invoice_Amount__c" label="" variant="label-hidden" min="0.01" step="0.01" readonly="{!v.isReadOnly}" class="closeOutInput" />
                                            </div>
                                            <div class="buttonColumn">
                                                <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:buttonIcon iconName="utility:clear" value="{!revenueIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveRevenue}" /></aura:if>
                                            </div>
                                        </div> 
                                    </aura:iteration>
                                </div>
                                <div class="actions">
                                    <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button label="Add Revenue" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddRevenue}" /></aura:if>
                                </div>
                            </div>
                        </div>
                        <aura:if isTrue="{!v.roomRevenue.isMonthlyPickUp}">
                            <div class="recordDetails" style="margin-top: 1em;">
                                <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                    <div class="recordTitleText">
                                        <div><i class="fas fa-dollar-sign titleIcon" style="color: white;"></i> Monthly Pick Up Details</div>
                                    </div>
                                    <div class="recordTitleButton">
                                        <lightning:buttonIcon iconName="{!v.showMonthlyPickUps==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowMonthlyPickUps}" />
                                    </div>
                                </div>
                                <div class="recordBodyContent" style="{!v.showMonthlyPickUps!=true?'display: none;':''}">
                                    <div class="recordTable tableList" style="margin: 0;">
                                        <div class="tableHeader">
                                            <div style="flex: 1;">Indicate Dates</div>
                                            <div style="flex: 2;">Room Type</div>
                                            <div style="flex: 1;">Room Nights</div>
                                            <div style="flex: 1;">Room Rate</div>
                                            <div style="flex: 1;">Commission</div>
                                            <div style="flex: 1;">Invoiced Date</div>
                                        </div>
                                        <aura:iteration items="{!v.monthlyPickUps}" var="monthlyPickUp" indexVar="monthlyPickUpIndex">
                                            <div class="tableRow">
                                                <div style="flex: 1;">{!monthlyPickUp.indicateDates}</div>
                                                <div style="flex: 2;">{!monthlyPickUp.roomType}</div>
                                                <div style="flex: 1;">{!monthlyPickUp.roomNights}</div>
                                                <div style="flex: 1;"><lightning:formattedNumber value="{!monthlyPickUp.rateCurrency}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/></div>
                                                <div style="flex: 1;"><lightning:formattedNumber value="{!monthlyPickUp.commissionPerRoom}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/></div>
                                                <div style="flex: 1;">{!monthlyPickUp.invoiceDate}</div>
                                            </div>
                                        </aura:iteration>
                                    </div>
                                </div>
                            </div>
                        </aura:if>
                    </div>
                    <div class="pageContentForm" style="margin-top: 1em;">
                        <div class="formFieldRadio">
                            <lightning:input aura:id="recordField" type="checkbox" label="{!v.agreementText}" required="{!not(or(v.isSent,v.isReadOnly))}" checked="{!not(or(v.isSent,v.isReadOnly))}" disabled="{!v.isReadOnly}" class="checkboxField checkboxList checkboxAgreement checkboxRequired" />
                        </div>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="name">Full Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewName" value="{!v.communitySign.reviewName}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewTitle" value="{!v.communitySign.reviewTitle}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="reviewEmail" value="{!v.communitySign.reviewEmail}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewPhone" value="{!v.communitySign.reviewPhone}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                    </div>
                    <div style="display: flex; justify-content: flex-end; margin-top: 1em;">
                        <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button iconName="utility:copy" label="Submit" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" /></aura:if>
                    </div>
                </div>
            </div>
        </aura:if>
    </div>
</aura:component>
```
### VoyajerCloseOutHousing

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
    /*max-width: 45em;*/
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

.THIS .checkboxField {
    padding-left: 0.75em;
}

.THIS .checkboxList .slds-form-element__label {
    font-size: 1rem;
    padding-left: 0.25em;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux {
    background-color: black;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux:after {
    border-bottom: 2px solid white;
    border-left: 2px solid white;
}

.THIS .checkboxRequired .slds-required {
    display: none;
}

.THIS .checkboxAgreement .slds-checkbox__label {
    display: flex;
}

.THIS .checkboxAgreement .slds-checkbox_faux {
    height: 1.25em;
    width: 2.75em;
    margin-top: 0.5em;
}

.THIS .buttonColumn {
    margin-right: 0.25em;
}
```
### VoyajerCloseOutHousingController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadCloseOut");
        callToParent.fire();
        /*
        var callToParentGetRevenue = component.getEvent("callToParentGetRevenue");
        console.log('call to parent ' + callToParentGetRevenue);
        callToParentGetRevenue.fire();
        console.log('after call to parent ');
        */
	},
    updateVAT : function(component, event, helper) {

        var theData = component.get('v.closeOutData');
        var theAddressVATData = new Object();
        theAddressVATData.vatnumber = theData.vatnumber;
        theAddressVATData.address = theData.address;
        theAddressVATData.revenue = theData.revenue;
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","updateVATAddressData");
        callToParent.setParam("data", theAddressVATData);
        callToParent.fire();
    },
    loadCloseOutData : function(component, event, helper) {
        var closeOutData = component.get("v.closeOutData");
        console.log(closeOutData);
        component.set("v.isAccessible",closeOutData.isAccessible);
        component.set("v.isReadOnly",closeOutData.isReadOnly);
        component.set("v.isSent",closeOutData.isSent);
        component.set("v.isSync",closeOutData.isSync);
        component.set("v.optionRecordId",closeOutData.bidId);
        component.set("v.lodgingType",closeOutData.lodgingType);
        component.set("v.productionSelected",closeOutData.productionId);
        component.set("v.reviewName",closeOutData.reviewName);
        component.set("v.reviewTitle",closeOutData.reviewTitle);
        component.set("v.reviewEmail",closeOutData.reviewEmail);
        component.set("v.reviewPhone",closeOutData.reviewPhone);
        component.set("v.roomTypes",closeOutData.roomTypes);
        component.set("v.revenueTypes",closeOutData.revenueTypes);
        component.set("v.chargeTypes",closeOutData.chargeTypes);
        component.set("v.rebates",closeOutData.rebates);
        component.set("v.productionRooms",closeOutData.productionRooms);
        component.set("v.lodgingRooms",closeOutData.lodgingRooms);
        component.set("v.revenues",closeOutData.revenues);
        component.set("v.monthlyPickUps",closeOutData.monthlyPickUps);
        component.set("v.roomRevenue",closeOutData.roomRevenue);
        component.set("v.communitySign",closeOutData.communitySign);
    },
    
    handleShowRooms : function(component, event, helper) {
        component.set("v.showRooms",!component.get("v.showRooms"));
    },
    
    handleShowRevenues : function(component, event, helper) {
        component.set("v.showRevenues",!component.get("v.showRevenues"));
    },
    
    handleShowMonthlyPickUps : function(component, event, helper) {
        component.set("v.showMonthlyPickUps",!component.get("v.showMonthlyPickUps"));
    },
    
    handleAddLodgingRoom : function(component, event, helper) {
        var lodgingRecords = component.get("v.lodgingRooms");
        lodgingRecords.push({
            recordId: "",
            roomType: component.get("v.roomTypes")[0],
            roomNights: 0,
            roomComps: 0,
            roomRate: 0,
            roomCommission: 0,
            roomConfirmation: ""
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
                bidId: component.get("v.optionRecordId"),
                serviceId: component.get("v.serviceId"),
                productionId: component.get("v.productionSelected"),
                productionRooms: component.get("v.productionRooms"),
                lodgingRooms: component.get("v.lodgingRooms"),
                roomRevenue: component.get("v.roomRevenue"),
                revenues: component.get("v.revenues"),
                communitySign: component.get("v.communitySign"),
                journal: {
                    coVendorName: component.get("v.reviewName"),
                    coVendorTitle: component.get("v.reviewTitle"),
                    coVendorEmail: component.get("v.reviewEmail"),
                    coVendorPhone: component.get("v.reviewPhone")
                }
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
        helper.calCommissionDue(component);
    },
    
    handleCalRevenueDetails: function(component, event, helper) {
        helper.calRevenueDetails(component);
    }
})
```
### VoyajerCloseOutHousingHelper

```
({
	calCommissionDue : function(component) {
        var productionRooms = component.get("v.productionRooms");
        var lodgingRooms = component.get("v.lodgingRooms");
        var roomRevenue = component.get("v.roomRevenue");
        
        var result = 0;
        var s1 = 0;
        var s2 = 0;
        var compsValue = 0;
        
        productionRooms.forEach(function(r) {
            if(roomRevenue.commissionType == 'Amount') result = parseFloat( (r.roomNights - r.roomComps) * roomRevenue.commissionValue);
            else result = parseFloat( (r.roomNights - r.roomComps) * r.roomRate * (roomRevenue.commissionValue/100) );
            s1 += result;
            compsValue += parseFloat(r.roomComps);
            r.roomCommission = result;
        });
        
        lodgingRooms.forEach(function(r) {
            result = 0;
            if(roomRevenue.commissionType == 'Amount') result = parseFloat( (r.roomNights - r.roomComps) * roomRevenue.commissionValue);
            else result = parseFloat( (r.roomNights - r.roomComps) * r.roomRate * (roomRevenue.commissionValue/100) );
            s2 += result;
            compsValue += parseFloat(r.roomComps);
            r.roomCommission = result;
        });
        
        s1 = parseFloat(s1.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0]);
        s2 = parseFloat(s2.toString().match(/^-?\d+(?:\.\d{0,2})?/)[0]);
        roomRevenue.commissionDue = s1+s2;
        roomRevenue.compsValue = parseFloat(compsValue.toString().match(/^\d+$/)[0]);
        //update
        component.set("v.productionRooms",productionRooms);
        component.set("v.lodgingRooms",lodgingRooms);
        component.set("v.roomRevenue",roomRevenue);
    },
    
    calRevenueDetails : function(component) {
        var revenues = component.get("v.revenues");
        revenues.forEach(function(r) {
            r.revenueInvoice = r.revenueValue * r.revenueTotal;
        });
        component.set("v.revenues",revenues);
    }
})
```
### VoyajerCloseOutHousing

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerCloseOutHousing

```
<aura:component >
	<aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="serviceId" />
    <aura:attribute type="String" name="lodgingType" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="String" name="reviewName" default="" />
    <aura:attribute type="String" name="reviewTitle" default="" />
    <aura:attribute type="String" name="reviewEmail" default="" />
    <aura:attribute type="String" name="reviewPhone" default="" />
    <aura:attribute type="String" name="agreementText" default="Property agrees to negotiate with Road Rebel ONLY moving forward and not offer client lower rates directly. If either is breached, 
                                                                you agree to pay Road Rebel commission on any room pick-up at your property(s). This also serves as the commission agreement in the event we go to contract. 
                                                                By selecting Submit, you are signing this agreement electronically.*" />
    <aura:attribute type="String" name="isVatChanged" default="No" />
    <aura:attribute type="Object" name="closeOutRevenue" default=""/>
    <aura:attribute type="Object" name="closeOutData" />
    <aura:attribute type="Object" name="roomRevenue" />
    <aura:attribute type="Object" name="communitySign" />
    <aura:attribute type="Boolean" name="showRooms" default="true" />
    <aura:attribute type="Boolean" name="showRevenues" default="true" />
    <aura:attribute type="Boolean" name="showMonthlyPickUps" default="true" />
    <aura:attribute type="Boolean" name="isAccessible" default="false" />
    <aura:attribute type="Boolean" name="isReadOnly" default="false" />
    <aura:attribute type="Boolean" name="isSent" default="false" />
    <aura:attribute type="Boolean" name="isSync" default="false" />
    <aura:attribute type="List" name="roomTypes" />
    <aura:attribute type="List" name="revenueTypes" />
    <aura:attribute type="List" name="chargeTypes" />
    <aura:attribute type="List" name="rebates" />
    <aura:attribute type="List" name="productionRooms" />
    <aura:attribute type="List" name="lodgingRooms" />
    <aura:attribute type="List" name="revenues" />
    <aura:attribute type="List" name="monthlyPickUps" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.closeOutData}" action="{!c.loadCloseOutData}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    <aura:registerEvent type="c:VoyajerCallToParentGetRevenue" name="callToParentGetRevenue" />
    <aura:registerEvent type="c:VoyajerCallToParentUpdateVAT" name="callToParentUpdateVAT" />
    
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
                            <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button iconName="utility:copy" label="Submit" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" /></aura:if>
                        </div>
                    </div>
                    <div class="pageContentForm">
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
                                        <div style="flex: 1; min-width: 0; padding-left: 1.25rem;"></div>
                                        <div style="width: 7rem; text-align: center;">Room Nights</div>
                                        <div style="width: 4.5rem; text-align: center;">Comps</div>
                                        <div style="width: 6rem; text-align: center;">Room Rate</div>
                                        <div style="width: 8rem; text-align: center;">Room Revenue</div>
                                        <div style="width: 7rem; text-align: center;">Commission</div>
                                        <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                            <div style="width: 9.5rem; text-align: center;">Confirmation #(s)</div>
                                        </aura:if>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <aura:iteration items="{!v.productionRooms}" var="productionRoom">
                                        <div class="tableRow" style="border-top: 0;">
                                            <div class="addButtonColumn"></div>
                                            <div style="flex: 1; min-width: 0; padding-left: 1.25rem;">
                                                <lightning:formattedText value="{!productionRoom.roomType}" class="outputText" />
                                            </div>
                                            <div style="width: 7rem; justify-content: center;">
                                                <lightning:input aura:id="recordField" type="number" value="{!productionRoom.roomNights}" label="" variant="label-hidden" step="1" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                            </div>
                                            <div style="width: 4.5rem; justify-content: center;">
                                                <lightning:input aura:id="recordField" type="number" value="{!productionRoom.roomComps}" label="" variant="label-hidden" step="1" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                            </div>
                                            <div style="width: 6rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                <lightning:formattedNumber value="{!productionRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <div style="width: 8rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                <lightning:formattedNumber value="{!(productionRoom.roomNights-productionRoom.roomComps)*productionRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                <lightning:formattedNumber value="{!productionRoom.roomCommission}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </div>
                                            <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                                <div style="width: 9.5rem; justify-content: center;">
                                                    <lightning:input aura:id="recordField" type="text" value="{!productionRoom.roomConfirmation}" label="" variant="label-hidden" class="closeOutInput" readonly="{!v.isReadOnly}" />
                                                </div>
                                            </aura:if>
                                            <div class="buttonColumn"></div>
                                        </div>
                                    </aura:iteration>
                                    <div class="tableRow">
                                        <div class="addButtonColumn" style="align-items: flex-start;">
                                            <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button iconName="utility:add" label="Other" class="formButtonAction" onclick="{!c.handleAddLodgingRoom}" /></aura:if>
                                        </div>
                                        <div style="display: flex; flex: 1; flex-direction: column; padding: 0;">
                                            <aura:iteration items="{!v.lodgingRooms}" var="lodgingRoom" indexVar="roomIndex">
                                                <div class="tableRow" style="border-top: 0;">
                                                    <div class="fieldSelect" style="{!'flex: 1; min-width: 0;' + (v.isReadOnly? ' padding-left: 1.25rem;' : '')}">
                                                        <aura:if isTrue="{!v.isReadOnly}">
                                                            <lightning:formattedText value="{!lodgingRoom.roomType}" class="outputText" />
                                                            <aura:set attribute="else">
                                                                <lightning:select name="Unit_Type__c" label="" variant="label-hidden" value="{!lodgingRoom.roomType}">
                                                                    <aura:iteration items="{!v.roomTypes}" var="roomType">
                                                                        <option value="{!roomType}">{!roomType}</option>
                                                                    </aura:iteration>
                                                                </lightning:select>
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                    <div style="width: 7rem; justify-content: center;">
                                                        <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomNights}" label="" variant="label-hidden" step="1" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                                    </div>
                                                    <div style="width: 4.5rem; justify-content: center;">
                                                        <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomComps}" label="" variant="label-hidden" step="1" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                                    </div>
                                                    <div style="{!'width: 6rem; justify-content: center;' + (v.isReadOnly? ' padding-left: 1.25rem;' : '')}">
                                                        <aura:if isTrue="{!v.isReadOnly}">
                                                            <lightning:formattedNumber value="{!lodgingRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                            <aura:set attribute="else">
                                                                <lightning:input aura:id="recordField" type="number" value="{!lodgingRoom.roomRate}" label="" variant="label-hidden" step="0.01" min="0" class="closeOutInput" onchange="{!c.handleCalCommissionDue}" readonly="{!v.isReadOnly}" />
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                    <div style="width: 8rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                        <lightning:formattedNumber value="{!(lodgingRoom.roomNights-lodgingRoom.roomComps)*lodgingRoom.roomRate}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                    </div>
                                                    <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5rem;">
                                                        <lightning:formattedNumber value="{!lodgingRoom.roomCommission}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                                    </div>
                                                    <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                                        <div style="width: 9.5rem; justify-content: center;">
                                                            <lightning:input aura:id="recordField" type="text" value="{!lodgingRoom.roomConfirmation}" label="" variant="label-hidden" class="closeOutInput" readonly="{!v.isReadOnly}" />
                                                        </div>
                                                    </aura:if>
                                                    <div class="buttonColumn">
                                                        <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:buttonIcon iconName="utility:clear" value="{!roomIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveLodgingRoom}" /></aura:if>
                                                    </div>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                    <div class="tableRow">
                                        <div class="addButtonColumn"></div>
                                        <div style="flex: 1; min-width: 0;">Comps:</div>
                                        <div style="width: 7rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <lightning:input aura:id="recordField" value="{!v.roomRevenue.compsValue}" type="number" label="Comps" variant="label-hidden" step="1" class="closeOutInput" readonly="{!v.isReadOnly}" />
                                        </div>
                                         <div style="{!'width: 6rem; justify-content: center;' + (v.isReadOnly? ' padding-left: 1.25rem;' : '')}"></div>
                                        <div style="width: 8rem; justify-content: flex-end; padding-right: 1.5rem;"></div>
                                        <div style="width: 7rem; justify-content: flex-end; padding-right: 1.5rem;"></div>
                                        <aura:if isTrue="{!v.lodgingType=='housingIR'}">
                                            <div style="width: 9.5rem; justify-content: center;"></div>
                                        </aura:if>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem;">Currency:</div>
                                        <div style="width: 6.5rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <lightning:formattedText value="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}" class="outputText" />
                                        </div>
                                        <div style="flex: 1;"></div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem;">Commission:</div>
                                        <div style="width: 6.5rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <!--<lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="percent" minimumFractionDigits="2"/>-->
                                            <aura:if isTrue="{!v.roomRevenue.commissionType == 'Percentage'}">
                                                <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="decimal" maximumFractionDigits="2" minimumFractionDigits="2"/> %
                                            </aura:if>
                                            <aura:if isTrue="{!v.roomRevenue.commissionType == 'Amount'}">
                                                <lightning:formattedNumber value="{!v.roomRevenue.commissionValue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                            </aura:if>
                                        </div>
                                        <div style="flex: 1;"></div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem;">Commission Due:</div>
                                        <div style="width: 6.5rem; justify-content: center;"></div>
                                        <div style="width: 4.5rem; justify-content: center;">
                                            <lightning:formattedNumber value="{!v.roomRevenue.commissionDue}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/>
                                        </div>
                                        <div style="flex: 1;"></div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                    <div class="tableRow" style="border-top: 0;">
                                        <div class="addButtonColumn"></div>
                                        <div style="width: 20%; max-width: 11rem; align-items: flex-start;">Notes:</div>
                                        <div style="flex: 1; justify-content: center;">
                                            <lightning:textarea aura:id="recordField" name="Notes__c" value="{!v.roomRevenue.commissionNotes}" label="" variant="label-hidden" onchange="{!c.handleInputChange}" class="notes" readonly="{!v.isReadOnly}" />
                                        </div>
                                        <div class="buttonColumn"></div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="closeOutQuestions" style="display: flex; margin-top: 1em; min-height: 3rem;">
                            <div class="tableRow">
                                <div>Do you need an invoice sent?</div>
                                <div><lightning:input type="toggle" checked="{!v.roomRevenue.isInvoiceSent}" label="option" variant="label-hidden" messageToggleActive="" messageToggleInactive="" disabled="{!v.isReadOnly}" /></div>
                            </div>
                            <div class="tableRow">
                                    <div>Indicate Dates</div>
                                    <div><lightning:input type="text" aura:id="recordField" label="option" variant="label-hidden" value="{!v.roomRevenue.indicateDates}" required="true" readonly="{!v.isReadOnly}" /></div>
                            </div>
                            <!--<div class="tableRow">
                                    <div style="flex: 1;">Does this match amount on pick up report?</div>
                                    <div><lightning:input type="toggle" checked="{!v.roomRevenue.isMatchingAmount}" label="option" variant="label-hidden" messageToggleActive="Yes" messageToggleInactive="No" /></div>
                                </div>-->
                        </div>
                        <div class="recordDetails" style="margin-top: 1em;">
                            <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                <div class="recordTitleText">
                                    <div><i class="fas fa-dollar-sign titleIcon" style="color: white;"></i> Update VAT Details</div>
                                </div>
                            </div>
                            <div class="slds-grid">
                            	<div class="slds-col" style="padding: 5px;">
                                    <lightning:input disabled="{!v.isVatChanged == 'No'}" name="VATNumber" label="VAT Number" value="{!v.closeOutData.vatnumber}"/>
                                </div>
                                <div class="slds-col" style="padding: 5px;">
                                    <lightning:input disabled="{!v.isVatChanged == 'No'}" name="Address" label="Address" value="{!v.closeOutData.address}" />
                                </div>
                                <div class="slds-col" style="padding: 5px;">
                                    <lightning:Select name="isChanged" label="VAT Changed?" value="{!v.isVatChanged}">
                                        <option value="No">No</option>
                                        <option value="Yes">Yes</option>
                                    </lightning:Select>
                                </div>
                            </div>
                            <br/>
                            <aura:if isTrue="{!v.isVatChanged == 'Yes'}">
                            	<div class="slds-grid">
                                <div class="slds-col" style="padding: 5px;">
                                    <lightning:button label="Update VAT" class="formButtonAction" onclick="{!c.updateVAT}"/>
                                </div>
                            </div>
                            </aura:if>
                        </div>
                        <div class="recordDetails" style="margin-top: 1em;">
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
                                            <div class="fieldSelect" style="{!'flex: 1;' + (v.isReadOnly? ' justify-content: center;' : '')}">
                                                <aura:if isTrue="{!v.isReadOnly}">
                                                    <lightning:formattedText value="{!revenue.revenueType}" class="outputText" />
                                                    <aura:set attribute="else">
                                                        <lightning:select name="Revenue_Type__c" value="{!revenue.revenueType}" label="" variant="label-hidden" class="revenueSelect">
                                                            <option value="">-- None --</option>
                                                            <aura:iteration items="{!v.revenueTypes}" var="revenueType">
                                                                <option value="{!revenueType}">{!revenueType}</option>
                                                            </aura:iteration>
                                                        </lightning:select>
                                                    </aura:set>
                                                </aura:if>
                                            </div>
                                            <div class="fieldSelect" style="{!'flex: 1;' + (v.isReadOnly? ' justify-content: center;' : '')}">
                                                <aura:if isTrue="{!v.isReadOnly}">
                                                    <lightning:formattedText value="{!revenue.revenueCharge}" class="outputText" />
                                                    <aura:set attribute="else">
                                                        <lightning:select name="Charge_Type__c" value="{!revenue.revenueCharge}" label="" variant="label-hidden" class="revenueSelect">
                                                            <option value="">-- None --</option>
                                                            <aura:iteration items="{!v.chargeTypes}" var="chargeType">
                                                                <option value="{!chargeType}">{!chargeType}</option>
                                                            </aura:iteration>
                                                        </lightning:select>
                                                    </aura:set>
                                                </aura:if>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueValue}" name="RevenueValue" label="" variant="label-hidden" min="0.01" step="0.01" class="closeOutInput" onchange="{!c.handleCalRevenueDetails}" readonly="{!v.isReadOnly}" />
                                            </div>
                                            <div class="fieldSelect" style="{!'flex: 1;' + (v.isReadOnly? ' justify-content: center;' : '')}">
                                                <aura:if isTrue="{!revenue.revenueType=='Rebate'}">
                                                    <aura:if isTrue="{!v.isReadOnly}">
                                                        <lightning:formattedText value="{!revenue.revenuePer}" class="outputText" />
                                                        <aura:set attribute="else">
                                                            <lightning:select name="Rebate_Per__c" value="{!revenue.revenuePer}" label="" variant="label-hidden" class="revenueSelect" onchange="{!c.handleInputChange}">
                                                                <option value="">-- None --</option>
                                                                <aura:iteration items="{!v.rebates}" var="rebate">
                                                                    <option value="{!rebate}">{!rebate}</option>
                                                                </aura:iteration>
                                                            </lightning:select>
                                                        </aura:set>
                                                    </aura:if>
                                                </aura:if>
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueTotal}" name="Total__c" label="" variant="label-hidden" min="1" step="1" class="closeOutInput" readonly="{!v.isReadOnly}" onchange="{!c.handleCalRevenueDetails}" />
                                            </div>
                                            <div style="flex: 1;">
                                                <lightning:input aura:id="recordField" type="number" value="{!revenue.revenueInvoice}" name="Invoice_Amount__c" label="" variant="label-hidden" min="0.01" step="0.01" readonly="{!v.isReadOnly}" class="closeOutInput" />
                                            </div>
                                            <div class="buttonColumn">
                                                <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:buttonIcon iconName="utility:clear" value="{!revenueIndex}" variant="bare" size="large" iconClass="clear" onclick="{!c.handleRemoveRevenue}" /></aura:if>
                                            </div>
                                        </div> 
                                    </aura:iteration>
                                </div>
                                <div class="actions">
                                    <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button label="Add Revenue" iconName="utility:add" class="formButtonAction" onclick="{!c.handleAddRevenue}" /></aura:if>
                                </div>
                            </div>
                        </div>
                        <aura:if isTrue="{!v.roomRevenue.isMonthlyPickUp}">
                            <div class="recordDetails" style="margin-top: 1em;">
                                <div class="recordTitle" style="background-color: #0065ff; color: white;">
                                    <div class="recordTitleText">
                                        <div><i class="fas fa-dollar-sign titleIcon" style="color: white;"></i> Monthly Pick Up Details</div>
                                    </div>
                                    <div class="recordTitleButton">
                                        <lightning:buttonIcon iconName="{!v.showMonthlyPickUps==true?'utility:up':'utility:down'}" iconClass="titleArrow" variant="bare" alternativeText="Open" onclick="{!c.handleShowMonthlyPickUps}" />
                                    </div>
                                </div>
                                <div class="recordBodyContent" style="{!v.showMonthlyPickUps!=true?'display: none;':''}">
                                    <div class="recordTable tableList" style="margin: 0;">
                                        <div class="tableHeader">
                                            <div style="flex: 1;">Indicate Dates</div>
                                            <div style="flex: 2;">Room Type</div>
                                            <div style="flex: 1;">Room Nights</div>
                                            <div style="flex: 1;">Room Rate</div>
                                            <div style="flex: 1;">Commission</div>
                                            <div style="flex: 1;">Invoiced Date</div>
                                        </div>
                                        <aura:iteration items="{!v.monthlyPickUps}" var="monthlyPickUp" indexVar="monthlyPickUpIndex">
                                            <div class="tableRow">
                                                <div style="flex: 1;">{!monthlyPickUp.indicateDates}</div>
                                                <div style="flex: 2;">{!monthlyPickUp.roomType}</div>
                                                <div style="flex: 1;">{!monthlyPickUp.roomNights}</div>
                                                <div style="flex: 1;"><lightning:formattedNumber value="{!monthlyPickUp.rateCurrency}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/></div>
                                                <div style="flex: 1;"><lightning:formattedNumber value="{!monthlyPickUp.commissionPerRoom}" style="currency" currencyCode="{!if(not(empty(v.closeOutData.currency)),v.closeOutData.currency,if(v.officePreference=='RRE','EUR','USD'))}"/></div>
                                                <div style="flex: 1;">{!monthlyPickUp.invoiceDate}</div>
                                            </div>
                                        </aura:iteration>
                                    </div>
                                </div>
                            </div>
                        </aura:if>
                    </div>
                    <div class="pageContentForm" style="margin-top: 1em;">
                        <div class="formFieldRadio">
                            <lightning:input aura:id="recordField" type="checkbox" label="{!v.agreementText}" required="{!not(or(v.isSent,v.isReadOnly))}" checked="{!not(or(v.isSent,v.isReadOnly))}" disabled="{!v.isReadOnly}" class="checkboxField checkboxList checkboxAgreement checkboxRequired" />
                        </div>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="name">Full Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewName" value="{!v.communitySign.reviewName}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewTitle" value="{!v.communitySign.reviewTitle}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="reviewEmail" value="{!v.communitySign.reviewEmail}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewPhone" value="{!v.communitySign.reviewPhone}" label="" variant="label-hidden" required="{!not(or(v.isSent,v.isReadOnly))}" readonly="{!v.isReadOnly}" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                    </div>
                    <div style="display: flex; justify-content: flex-end; margin-top: 1em;">
                        <aura:if isTrue="{!not(v.isReadOnly)}"><lightning:button iconName="utility:copy" label="Submit" class="formButtonAction" onclick="{!c.handleSaveCloseOut}" /></aura:if>
                    </div>
                </div>
            </div>
        </aura:if>
    </div>
</aura:component>
```
### VoyajerCloseOutHousing

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
    /*max-width: 45em;*/
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

.THIS .checkboxField {
    padding-left: 0.75em;
}

.THIS .checkboxList .slds-form-element__label {
    font-size: 1rem;
    padding-left: 0.25em;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux {
    background-color: black;
}

.THIS .slds-checkbox [type=checkbox]:checked+.slds-checkbox__label .slds-checkbox_faux:after {
    border-bottom: 2px solid white;
    border-left: 2px solid white;
}

.THIS .checkboxRequired .slds-required {
    display: none;
}

.THIS .checkboxAgreement .slds-checkbox__label {
    display: flex;
}

.THIS .checkboxAgreement .slds-checkbox_faux {
    height: 1.25em;
    width: 2.75em;
    margin-top: 0.5em;
}

.THIS .buttonColumn {
    margin-right: 0.25em;
}
```
### VoyajerCloseOutHousingController

```
({
	doInit : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadCloseOut");
        callToParent.fire();
        /*
        var callToParentGetRevenue = component.getEvent("callToParentGetRevenue");
        console.log('call to parent ' + callToParentGetRevenue);
        callToParentGetRevenue.fire();
        console.log('after call to parent ');
        */
	},
    updateVAT : function(component, event, helper) {

        var theData = component.get('v.closeOutData');
        var theAddressVATData = new Object();
        theAddressVATData.vatnumber = theData.vatnumber;
        theAddressVATData.address = theData.address;
        theAddressVATData.revenue = theData.revenue;
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","updateVATAddressData");
        callToParent.setParam("data", theAddressVATData);
        callToParent.fire();
    },
    loadCloseOutData : function(component, event, helper) {
        var closeOutData = component.get("v.closeOutData");
        console.log(closeOutData);
        component.set("v.isAccessible",closeOutData.isAccessible);
        component.set("v.isReadOnly",closeOutData.isReadOnly);
        component.set("v.isSent",closeOutData.isSent);
        component.set("v.isSync",closeOutData.isSync);
        component.set("v.optionRecordId",closeOutData.bidId);
        component.set("v.lodgingType",closeOutData.lodgingType);
        component.set("v.productionSelected",closeOutData.productionId);
        component.set("v.reviewName",closeOutData.reviewName);
        component.set("v.reviewTitle",closeOutData.reviewTitle);
        component.set("v.reviewEmail",closeOutData.reviewEmail);
        component.set("v.reviewPhone",closeOutData.reviewPhone);
        component.set("v.roomTypes",closeOutData.roomTypes);
        component.set("v.revenueTypes",closeOutData.revenueTypes);
        component.set("v.chargeTypes",closeOutData.chargeTypes);
        component.set("v.rebates",closeOutData.rebates);
        component.set("v.productionRooms",closeOutData.productionRooms);
        component.set("v.lodgingRooms",closeOutData.lodgingRooms);
        component.set("v.revenues",closeOutData.revenues);
        component.set("v.monthlyPickUps",closeOutData.monthlyPickUps);
        component.set("v.roomRevenue",closeOutData.roomRevenue);
        component.set("v.communitySign",closeOutData.communitySign);
    },
    
    handleShowRooms : function(component, event, helper) {
        component.set("v.showRooms",!component.get("v.showRooms"));
    },
    
    handleShowRevenues : function(component, event, helper) {
        component.set("v.showRevenues",!component.get("v.showRevenues"));
    },
    
    handleShowMonthlyPickUps : function(component, event, helper) {
        component.set("v.showMonthlyPickUps",!component.get("v.showMonthlyPickUps"));
    },
    
    handleAddLodgingRoom : function(component, event, helper) {
        var lodgingRecords = component.get("v.lodgingRooms");
        lodgingRecords.push({
            recordId: "",
            roomType: component.get("v.roomTypes")[0],
            roomNights: 0,
            roomComps: 0,
            roomRate: 0,
            roomCommission: 0,
            roomConfirmation: ""
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
                bidId: component.get("v.optionRecordId"),
                serviceId: component.get("v.serviceId"),
                productionId: component.get("v.productionSelected"),
                productionRooms: component.get("v.productionRooms"),
                lodgingRooms: component.get("v.lodgingRooms"),
                roomRevenue: component.get("v.roomRevenue"),
                revenues: component.get("v.revenues"),
                communitySign: component.get("v.communitySign"),
                journal: {
                    coVendorName: component.get("v.reviewName"),
                    coVendorTitle: component.get("v.reviewTitle"),
                    coVendorEmail: component.get("v.reviewEmail"),
                    coVendorPhone: component.get("v.reviewPhone")
                }
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
        helper.calCommissionDue(component);
    },
    
    handleCalRevenueDetails: function(component, event, helper) {
        helper.calRevenueDetails(component);
    }
})
```

---
layout: default
title: VoyajerOptionsHousingCompare
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsHousingCompare
## Fields
### VoyajerOptionsHousingCompareHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsHousingCompare

```
<aura:component>
    <aura:attribute type="String" name="housingId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="housingType" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="List" name="bidOptionsFiltered" />
    <aura:attribute type="List" name="compareList" />
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i> Compare Options
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}"/>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                            	<p>{!v.serviceData.venue}</p>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.serviceData.releaseDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:2em;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-carousel__stage section-compare">
                        <div class="slds-grid slds-wrap">
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-grid slds-gutters_x-small slds-wrap section-compare_header">
                                    <div class="slds-col slds-size_1-of-4">
                                    </div>
                                    <aura:iteration items="{!v.compareList}" var="bid">
                                        <div class="slds-col slds-size_1-of-4 section-compare_header_item">
                                            <div class="header">{!bid.vendor}</div>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Information Details">Information Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Distance to Venue</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.dx_to_venue}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Website</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="color: #00b4ff; overflow-wrap: break-word;">
                                                    <aura:if isTrue="{!and(bid.website != null, bid.website != '')}">
                                                        <lightning:formattedText linkify="true" value="{!bid.website}" />
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Address</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingStreet}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>City, State / Postal Code</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingCity + ', ' + bid.record.Vendor__r.ShippingState + ' ' + bid.record.Vendor__r.ShippingPostalCode}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <!-- Fix By Clay Dev 31 Jan, 2021 #176367796-->
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Phone</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.phone}
                                                </div>
                                            </aura:iteration>
                                        </div>
										
                                    </div>
                                </div>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Rate Details">Rate Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Date In - Date Out, <br/> Qty, Bed Type &amp; Rate</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.roomTypes)}">
                                                        <aura:iteration items="{!bid.roomTypes}" var="roomtype">
                                                            <div>{!roomtype.Date_In_Text__c} - {!roomtype.Date_Out_Text__c}</div>
                                                            <div>{!roomtype.Units__c} - {!roomtype.Unit_Type__c}</div>
                                                            <div style="font-weight:bold;">
                                                                <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />
                                                                <span>&nbsp;{!roomtype.Rate_Period__c}</span>
                                                            </div>
                                                        </aura:iteration>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                                            <aura:if isTrue="{!v.officePreference == 'RRE'}">
                                                <div class="slds-grid slds-wrap section-compare_content_row">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                        <strong>VAT</strong>
                                                    </div>
                                                    <aura:iteration items="{!v.compareList}" var="bid">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                            <span>{!if(bid.rateDetails.VAT_Rate__c != null,bid.rateDetails.VAT_Rate__c,0)}%&nbsp;{!if(bid.rateDetails.VAT__c == true,'Included','Not Included')}</span>
                                                            <br/>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <div class="slds-grid slds-wrap section-compare_content_row">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                        <strong>CITY TAX</strong>
                                                    </div>
                                                    <aura:iteration items="{!v.compareList}" var="bid">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                            <span>
                                                                <aura:if isTrue="{!if(and(bid.rateDetails.City_Tax_Rate__c != null, bid.rateDetails.City_Tax_Rate__c > 0),true,false)}">
                                                                    <lightning:formattedNumber value="{!bid.rateDetails.City_Tax_Rate__c}" 
                                                                                               style="currency" 
                                                                                               currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                               currencyDisplayAs="symbol" />
                                                                    <aura:set attribute="else">{!if(bid.rateDetails.City_Tax_Rate_percent__c != null,bid.rateDetails.City_Tax_Rate_percent__c+'%','0%')}</aura:set>
                                                                </aura:if>&nbsp;
                                                                {!if(bid.rateDetails.City_Tax__c == true,'Included','Not Included')}&nbsp;
                                                                {!bid.rateDetails.City_Tax_Type__c}
                                                            </span>
                                                            <br/>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <div class="slds-grid slds-wrap section-compare_content_row">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                        <strong>BREAKFAST</strong>
                                                    </div>
                                                    <aura:iteration items="{!v.compareList}" var="bid">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                            <span>
                                                                <lightning:formattedNumber value="{!if(bid.rateDetails.Breakfast_Rate__c != null,bid.rateDetails.Breakfast_Rate__c,0)}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />
                                                                &nbsp;{!if(bid.rateDetails.Breakfast__c == true,'Included','Not Included')}
                                                            </span>
                                                            <br/>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <aura:set attribute="else">
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                            <strong>Tax / Surcharge</strong>
                                                        </div>
                                                        <aura:iteration items="{!v.compareList}" var="bid">
                                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                                <span>{!if(bid.rateDetails.Tax__c != null, bid.rateDetails.Tax__c, '0')}%&nbsp;{!if(bid.rateDetails.Tax_Included__c == true,'Included','Not Included')}</span>
                                                                <br/>
                                                                <span>
                                                                    <aura:if isTrue="{!bid.rateDetails.Surcharge__c != null}">
                                                                        <lightning:formattedNumber value="{!bid.rateDetails.Surcharge__c}" 
                                                                                                   style="currency" 
                                                                                                   currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                                   currencyDisplayAs="symbol" />
                                                                        <aura:set attribute="else">No Surcharge</aura:set>
                                                                    </aura:if>
                                                                </span>
                                                                <br/>
                                                            </div>
                                                        </aura:iteration>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </aura:if>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong><aura:if isTrue="{!v.housingType=='Corporate_Housing'}">Comps / </aura:if>Concessions</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.concessions)}">
                                                        <ul class="slds-text-align_left">
                                                            <aura:iteration items="{!bid.concessions}" var="concession">
                                                                <li style="list-style: disc;">
                                                                    <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                                                                        {!concession.Concessions_Requested__c+' '+concession.Concession_Provided__c}
                                                                        <aura:set attribute="else">
                                                                            {!concession.Concession_Provided__c}
                                                                        </aura:set>
                                                                    </aura:if>
                                                                    <!--{!concession.Concessions_Requested__c}-->
                                                                </li>
                                                            </aura:iteration>
                                                        </ul>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="Property Details">Property Details</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Check-In / Check-Out</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Check_In_Time_Formatted__c != null,bid.vendorData.Check_In_Time_Formatted__c + ' / ','')}
                                                        {!if(bid.vendorData.Check_out_time_formatted__c != null,bid.vendorData.Check_out_time_formatted__c,'')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Rooms / Suites</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Number_of_rooms__c != null || bid.vendorData.Number_of_suites__c != null, bid.vendorData.Number_of_rooms__c + ' / ' + bid.vendorData.Number_of_suites__c, '')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Star Rates</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Star_Rating__c != null,if(bid.vendorData.Star_Rating__c == '1',bid.vendorData.Star_Rating__c + ' star',bid.vendorData.Star_Rating__c + ' stars'),'')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Year Built / Renovated</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Year_built__c != null || bid.vendorData.Year_renovated__c != null, bid.vendorData.Year_built__c + ' / ' + bid.vendorData.Year_renovated__c, '')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>100% Non Smoking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.X100_Non_Smoking__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Lift / Elevator</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Lift_Elevator__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Property Entry</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Property_Entry__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Porterage</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Porterage__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Windows that open</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Windows_Open__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Air Conditioning</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Air_conditioning__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>High Speed Internet</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.High_Speed_Internet__c == 'Yes/Complimentary','Yes',bid.vendorData.High_Speed_Internet__c)}<br/>
                                                        <aura:if isTrue="{!bid.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <aura:if isTrue="{!bid.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                                    No
                                                                    <aura:set attribute="else">
                                                                        <lightning:formattedNumber value="{!bid.vendorData.Internet_Charge__c}" 
                                                                                                   style="currency" 
                                                                                                   currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                                   currencyDisplayAs="symbol" />
                                                                    </aura:set>
                                                                </aura:if>
                                                            </aura:set>
                                                        </aura:if>
                                                        <br/>
                                                        {!bid.vendorData.Connection__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pet Allowed</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Pets_Allowed__c}<br/>
                                                        <aura:if isTrue="{!bid.vendorData.Pets_charge__c != null}">
                                                            {!'Fee: '}
                                                            <lightning:formattedNumber value="{!bid.vendorData.Pets_charge__c}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                        </aura:if>
                                                        <br/>
                                                        {!bid.vendorData.Pets_charge_type__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="In-Room Amenities">In-Room Amenities</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Microwave</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Microwave__c} <br/>
                                                        {!bid.vendorData.Microwave_charge_type__c} <br/>
                                                        {!bid.vendorData.Avail_Microwave__c} <br/>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Refrigerator</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Refrigerator__c} <br/>
                                                        {!bid.vendorData.Refrigerator_charge_type__c} <br/>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Coffee Maker</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Coffee_Maker__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hairdryer</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Hairdryers__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Bathtubs</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Bathtub__c == 'Shower only','No',if(bid.vendorData.Bathtub__c != null,'Yes',''))} <br/>
                                                        {!bid.vendorData.Bathtub__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Safe</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Safe__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="On-Site Amenities">On-Site Amenities</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pool / Hot tub</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        <aura:if isTrue="{!bid.vendorData.Pool__c != null}">
                                                            {!if(bid.vendorData.Pool_Seasonal__c == 'Yes',bid.vendorData.Pool__c+'. Seasonal',bid.vendorData.Pool__c)}
                                                        </aura:if>{!' / '}
                                                        <aura:if isTrue="{!bid.vendorData.Hot_Tub__c != null}">
                                                            {!if(bid.vendorData.Hot_tub_seasonal__c == 'Yes',bid.vendorData.Hot_Tub__c+'. Seasonal',bid.vendorData.Hot_Tub__c)}
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Fitness Room</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Fitness_room__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hotel Shuttle</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Hotel_Shuttle__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Airport Shuttle</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Airport_Shuttle__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hotel Bar</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Hotel_Bars__c} <br/>
                                                        {!if(bid.vendorData.hotel_bars_2__c != null,bid.vendorData.hotel_bars_2__c + ' on-site','')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hotel Restaurant</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Restaurants__c} <br/>
                                                        {!if(bid.vendorData.Restaurants_2__c != null,bid.vendorData.Restaurants_2__c + ' on-site','')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Comp Breakfast</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Breakfast__c == 'Yes/Complimentary','Yes','No')} <br/>
                                                        {!bid.vendorData.Breakfast_type__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Room Service</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Room_Service__c} <br/>
                                                        {!bid.vendorData.Room_Service_hours__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Managers Reception</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Managers_Reception__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Self Parking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Self_Parking__c == 'Yes/Complimentary','Yes',bid.vendorData.Self_Parking__c)} <br/>
                                                        <aura:if isTrue="{!bid.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <lightning:formattedNumber value="{!bid.vendorData.Self_Parking_Charge__c}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Valet Parking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Valet_Parking__c == 'Yes/Complimentary','Yes',bid.vendorData.Valet_Parking__c)} <br/>
                                                        <aura:if isTrue="{!bid.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <lightning:formattedNumber value="{!bid.vendorData.Valet_Parking_Charge__c}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />{!'/' + bid.vendorData.Valet_Parking_Charge_Type__c}
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Bus Parking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Coach_Bus_Parking__c == 'Yes/Complimentary','Yes',bid.vendorData.Coach_Bus_Parking__c)} <br/>
                                                        <aura:if isTrue="{!bid.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <lightning:formattedNumber value="{!bid.vendorData.Coach_Bus_Charge__c}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />{!'/' + bid.vendorData.Coach_Bus_Charge_Type__c}
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header"></div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="text-align: center;">
                                                        <lightning:button label="SELECT" variant="brand" class="formButtonBrand btn-custom" iconName="utility:check" iconPosition="right" value="{!bid.recordId}" onclick="{!c.openReviewSubmit}"/>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                    <!-- Add off-site amenities -->
                                    
                                </aura:if>
                                <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="Building Details">Building Details</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Lift / Elevator</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Lift_Elevator__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>24 Hour Doorman</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.X24_hour_doorman__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>24 Hour FD</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.X24_Hour_FD__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Air Conditioning</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Air_conditioning__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pet Allowed</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Pets_Allowed__c}<br/>
                                                        <aura:if isTrue="{!bid.vendorData.Pets_charge__c != null}">
                                                            {!'Fee: '}
                                                            <lightning:formattedNumber value="{!bid.vendorData.Pets_charge__c}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                        </aura:if>
                                                        <br/>
                                                        {!bid.vendorData.Pets_charge_type__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Washer / Dryer</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Washer_Dryer__c == 'Yes',bid.vendorData.Washer_dryer_in_unit__c+' '+bid.vendorData.Washer_Dryer_Type__c,'No')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pool / Hot tub</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        <div style="float:left;width:33%;">{!if(bid.vendorData.Pool__c != null,bid.vendorData.Pool__c + '/','')}{!bid.vendorData.vendorData.Hot_Tub__c}</div>
                                                        <div style="float:left;width:33%;">{!if(bid.vendorData.Pool_Seasonal__c != null,bid.vendorData.vendorData.Pool_Seasonal__c + '/','')}{!bid.vendorData.Hot_tub_seasonal__c}</div>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Fitness Room</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Fitness_room__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Parking On-Site</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Parking_on_site__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                </aura:if>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Previous RR Shows">Previous RR Shows</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Show Previously Housed</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.rrShows)}">
                                                        <ul class="slds-text-align_left">
                                                            <aura:iteration items="{!bid.rrShows}" var="show">
                                                                <li style="list-style: disc; white-space: pre-wrap;">
                                                                    {!show}
                                                                </li>
                                                            </aura:iteration>
                                                        </ul>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Airports">Airports</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Airport Distance</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.airports)}">
                                                        <ul class="slds-text-align_left">
                                                            <aura:iteration items="{!bid.airports}" var="airport">
                                                                <li style="list-style: disc; white-space: pre-wrap;">
                                                                    {!airport}
                                                                </li>
                                                            </aura:iteration>
                                                        </ul>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="page-section">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1" style="margin-top: 2em;text-align: right;">
                            <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}"/>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <aura:if isTrue="{!v.openSelectOptionsAlert}">
      <c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}"/>
    </aura:if>
</aura:component>
```
### VoyajerOptionsHousingCompareController

```
({
  doInit: function (component, event, helper) {
    console.log(component.get("v.housingType"));
    console.log(JSON.stringify(component.get("v.compareList")));
  },
  backOptionsHousing: function (component, event, helper) {
    component.set("v.mainContent", "optionsHousing");
  },
  openReviewSubmit: function (component, event, helper) {
    var theURL = window.location.href;
    var isPreview = theURL.includes('VoyajerPreviewApp');
    var okToAdvance = true;

    if (isPreview){
      okToAdvance = false;
    } else {
      var list = component.get("v.bidOptions");
      var recordId = event.getSource().get("v.value");
      var index = 0;
      var indexActual;
      okToAdvance = true;
  
      list.forEach(function (bid) {
        if (bid.recordId == recordId) {
          indexActual = index;
        }
        index++;
        if (!bid.isEvent){
          console.log('inside not multi');
          if (bid.record.Status__c  === 'Decision' || bid.record.Status__c  === 'In Contracting' || bid.record.Status__c  === 'Contracted' || bid.record.Status__c  === 'Pending Client Signature'){
            console.log('inside status contracted');
            okToAdvance = false;
          }
        }
      });
  
      if ((list[indexActual].record.Status__c === "Decision" || list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
        okToAdvance = false;
      }
    }

    if (okToAdvance) {
      component.set("v.optionDetailRecordId", indexActual);
      component.set("v.bidOptionsSize", list.length);
      component.set("v.mainContent", "optionsHousingReviewSubmit");
    } else {
      component.set("v.openSelectOptionsAlert", true);
    }
    
  }
});
```
### VoyajerOptionsHousingCompare

```
.THIS .optionBox {
    padding: 1.5em 2em 1.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: white;
    margin: 1.5em 1em 1.5em 0;
    box-shadow: 4px 4px 4px 0 #dbdbdb;
    border-left: 1px solid #dbdbdb;
    border-top: 1px solid #dbdbdb;
}

.THIS .optionBox.left{
    width: 60%;
}

.THIS .optionBox.right{
    width: 38%;
}

.THIS .optionBoxIcon {
    padding-bottom: 1em;
}

.THIS .optionBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .optionBoxName {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 1.25em;
    display: flex;
    align-items: center;
    justify-content: left;
}

.THIS .optionBoxName p {
    line-height: 1.5;
    margin-bottom: 0.2em !important;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    max-height: 3em;
}

.THIS .optionBoxDescription p {
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    min-height: 1.5em;
}

.THIS .optionBoxDescription .room-type {
    min-width: 1.5em;
}

.THIS .pageContentOptions{
    display: flex;
    flex-flow: wrap;
}

.THIS .pageContentForm p {
    margin-bottom: 0 !important;
}

.THIS .recordTable,
.THIS .tableHeader,
.THIS .tableRow {
    display: flex;
    width: 100%;
}

.THIS .recordTable {
    flex-direction: column;
    border: 1px solid #dbdbdb;
    margin: .5em 0 1em;
}

.THIS .tableHeader {
    flex: 1;
    background-color: #f7f9fe;
    font-weight: 500;
}

.THIS .tableRow {
    flex: 1;
    min-width: 0;
}

.THIS .tableList > .tableRow ~ .tableRow {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em 1em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}

.THIS .box-decisionBy{
    display: inline-block;
    padding: 1rem 1.5rem;
    background-color: #ec4518;
    border: none;
    text-align: center;
    color: white;
    font-weight: bold;
}

.THIS .pageContentDashboard-grey{
    background-color: #f0f0f0 !important;
    box-shadow: none !important;
}

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .slds-card-overview .information-label{
    background-color: #f0f0f0;
    padding: 1.1em;
    color: #00b4ff;
    font-weight:bold;
}

.THIS .slds-card-overview .information-label-other{
    padding: 1.1em;
    font-weight:bold;
    font-size: 12px;
    border-left: 1px solid #f0f0f0;
    border-bottom: 1px solid #f0f0f0
}

.THIS .slds-card-overview .information-label.first{
    margin-top: 4.9em;
}

.THIS .slds-card-overview .information-label-value{
    padding: 1.1em;
    font-size: 12px;
    border-bottom: 1px solid #f0f0f0;
    text-align: center;
}

/*--------------------
-----Compare------
----------------------*/

.THIS .section-compare{
}

.THIS .section-compare .section-compare_header{
}

.THIS .section-compare .section-compare_header > .section-compare_header_space{
    
}

.THIS .section-compare .section-compare_header > .section-compare_header_item .header{
    background-color: #085ee2;
    color: white;
    text-align: center;
    padding: 1.5em;
    font-weight: bold;
    font-size: 1.1em;
}

.THIS .section-compare .section-compare_header > .section-compare_header_item > h3{
    min-height: 5em;
    padding: 1em 2.2em;
    background-color: #0670c8;
    text-align: center;
    font-size: 1.1rem;
    color: white;
}

.THIS .section-compare .section-compare_content{
    margin-top: 0;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header{
    background-color: #eff2f7;
    border-radius: 0;
    font-size:.875rem;
    font-weight: 600;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header > .slds-button-expandable{
    padding: .8em 1.5em;
    text-transform: none;
}

.THIS .section-compare .section-compare_content .section-compare_content_row{
    border: 1px solid #eff2f7;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_header{
    padding: .8em 1.5em;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_content{
    padding: .8em 1.5em;
    text-align: center;
}

/*--------------------
-----Button------
----------------------*/

.THIS .slds-button-expandable{
    background:none;
    justify-content:space-between;
    color:#00b4ff;
}

.THIS .slds-button-expandable:hover,
.THIS .slds-button-expandable:focus,
.THIS .slds-button-expandable:active{
    background: none;
    box-shadow: none;
    color:#00b4ff;
}

.THIS .buttonIcon-bluelight{
    color:#00b4ff;
}

.THIS button.btn-blue{
    padding-left: 3rem;
    padding-right: 3rem;
    background-color: #0065ff;
}

.THIS button.btn-blue:active,
.THIS button.btn-blue:visited,
.THIS button.btn-blue:focus {
    background-color: #0453cc;
}


/*--------------------
-----Medias queries------
----------------------*/

@media (min-width: 768px){
    .THIS .section-compare .section-compare_header > .section-compare_header_space{
        width: 22%;
    }
}
```
### VoyajerOptionsHousingCompare

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingCompareHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsHousingCompare

```
<aura:component>
    <aura:attribute type="String" name="housingId" />
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="housingType" />
    <aura:attribute type="String" name="officePreference" />
    <aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="Integer" name="optionDetailRecordId" />
    <aura:attribute type="List" name="bidOptions" />
    <aura:attribute type="List" name="bidOptionsFiltered" />
    <aura:attribute type="List" name="compareList" />
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i> Compare Options
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}"/>
                    </div>
                </div>
                <div class="pageContentDashboard">
                    <div class="page-section">
                        <div class="slds-grid slds-gutters slds-wrap">
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2">
                                <h3><strong style="color:black;">{!v.productionName}</strong></h3>
                                <p style="margin-right: 0.5em;font-weight:bold;color:#00b4ff;">{!v.serviceData.cityName} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}</p>
                            	<p>{!v.serviceData.venue}</p>
                            </div>
                            <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-2" style="text-align:right;">
                                <div class="box-decisionBy">
                                    DECISION BY <br/>
                                    {!v.serviceData.releaseDate}
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="pageContentDashboard" style="padding-top:2em;border-bottom: 1px solid #dbdbdb;">
                    <div class="slds-carousel__stage section-compare">
                        <div class="slds-grid slds-wrap">
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-grid slds-gutters_x-small slds-wrap section-compare_header">
                                    <div class="slds-col slds-size_1-of-4">
                                    </div>
                                    <aura:iteration items="{!v.compareList}" var="bid">
                                        <div class="slds-col slds-size_1-of-4 section-compare_header_item">
                                            <div class="header">{!bid.vendor}</div>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </div>
                            <div class="slds-col slds-size_1-of-1">
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Information Details">Information Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Distance to Venue</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.dx_to_venue}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Website</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="color: #00b4ff; overflow-wrap: break-word;">
                                                    <aura:if isTrue="{!and(bid.website != null, bid.website != '')}">
                                                        <lightning:formattedText linkify="true" value="{!bid.website}" />
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Address</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingStreet}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>City, State / Postal Code</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.record.Vendor__r.ShippingCity + ', ' + bid.record.Vendor__r.ShippingState + ' ' + bid.record.Vendor__r.ShippingPostalCode}
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <!-- Fix By Clay Dev 31 Jan, 2021 #176367796-->
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Phone</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    {!bid.phone}
                                                </div>
                                            </aura:iteration>
                                        </div>
										
                                    </div>
                                </div>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Rate Details">Rate Details</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Date In - Date Out, <br/> Qty, Bed Type &amp; Rate</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.roomTypes)}">
                                                        <aura:iteration items="{!bid.roomTypes}" var="roomtype">
                                                            <div>{!roomtype.Date_In_Text__c} - {!roomtype.Date_Out_Text__c}</div>
                                                            <div>{!roomtype.Units__c} - {!roomtype.Unit_Type__c}</div>
                                                            <div style="font-weight:bold;">
                                                                <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />
                                                                <span>&nbsp;{!roomtype.Rate_Period__c}</span>
                                                            </div>
                                                        </aura:iteration>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                        <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                                            <aura:if isTrue="{!v.officePreference == 'RRE'}">
                                                <div class="slds-grid slds-wrap section-compare_content_row">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                        <strong>VAT</strong>
                                                    </div>
                                                    <aura:iteration items="{!v.compareList}" var="bid">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                            <span>{!if(bid.rateDetails.VAT_Rate__c != null,bid.rateDetails.VAT_Rate__c,0)}%&nbsp;{!if(bid.rateDetails.VAT__c == true,'Included','Not Included')}</span>
                                                            <br/>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <div class="slds-grid slds-wrap section-compare_content_row">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                        <strong>CITY TAX</strong>
                                                    </div>
                                                    <aura:iteration items="{!v.compareList}" var="bid">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                            <span>
                                                                <aura:if isTrue="{!if(and(bid.rateDetails.City_Tax_Rate__c != null, bid.rateDetails.City_Tax_Rate__c > 0),true,false)}">
                                                                    <lightning:formattedNumber value="{!bid.rateDetails.City_Tax_Rate__c}" 
                                                                                               style="currency" 
                                                                                               currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                               currencyDisplayAs="symbol" />
                                                                    <aura:set attribute="else">{!if(bid.rateDetails.City_Tax_Rate_percent__c != null,bid.rateDetails.City_Tax_Rate_percent__c+'%','0%')}</aura:set>
                                                                </aura:if>&nbsp;
                                                                {!if(bid.rateDetails.City_Tax__c == true,'Included','Not Included')}&nbsp;
                                                                {!bid.rateDetails.City_Tax_Type__c}
                                                            </span>
                                                            <br/>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <div class="slds-grid slds-wrap section-compare_content_row">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                        <strong>BREAKFAST</strong>
                                                    </div>
                                                    <aura:iteration items="{!v.compareList}" var="bid">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                            <span>
                                                                <lightning:formattedNumber value="{!if(bid.rateDetails.Breakfast_Rate__c != null,bid.rateDetails.Breakfast_Rate__c,0)}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />
                                                                &nbsp;{!if(bid.rateDetails.Breakfast__c == true,'Included','Not Included')}
                                                            </span>
                                                            <br/>
                                                        </div>
                                                    </aura:iteration>
                                                </div>
                                                <aura:set attribute="else">
                                                    <div class="slds-grid slds-wrap section-compare_content_row">
                                                        <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                            <strong>Tax / Surcharge</strong>
                                                        </div>
                                                        <aura:iteration items="{!v.compareList}" var="bid">
                                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                                <span>{!if(bid.rateDetails.Tax__c != null, bid.rateDetails.Tax__c, '0')}%&nbsp;{!if(bid.rateDetails.Tax_Included__c == true,'Included','Not Included')}</span>
                                                                <br/>
                                                                <span>
                                                                    <aura:if isTrue="{!bid.rateDetails.Surcharge__c != null}">
                                                                        <lightning:formattedNumber value="{!bid.rateDetails.Surcharge__c}" 
                                                                                                   style="currency" 
                                                                                                   currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                                   currencyDisplayAs="symbol" />
                                                                        <aura:set attribute="else">No Surcharge</aura:set>
                                                                    </aura:if>
                                                                </span>
                                                                <br/>
                                                            </div>
                                                        </aura:iteration>
                                                    </div>
                                                </aura:set>
                                            </aura:if>
                                        </aura:if>
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong><aura:if isTrue="{!v.housingType=='Corporate_Housing'}">Comps / </aura:if>Concessions</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.concessions)}">
                                                        <ul class="slds-text-align_left">
                                                            <aura:iteration items="{!bid.concessions}" var="concession">
                                                                <li style="list-style: disc;">
                                                                    <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                                                                        {!concession.Concessions_Requested__c+' '+concession.Concession_Provided__c}
                                                                        <aura:set attribute="else">
                                                                            {!concession.Concession_Provided__c}
                                                                        </aura:set>
                                                                    </aura:if>
                                                                    <!--{!concession.Concessions_Requested__c}-->
                                                                </li>
                                                            </aura:iteration>
                                                        </ul>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                                <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="Property Details">Property Details</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Check-In / Check-Out</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Check_In_Time_Formatted__c != null,bid.vendorData.Check_In_Time_Formatted__c + ' / ','')}
                                                        {!if(bid.vendorData.Check_out_time_formatted__c != null,bid.vendorData.Check_out_time_formatted__c,'')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Rooms / Suites</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Number_of_rooms__c != null || bid.vendorData.Number_of_suites__c != null, bid.vendorData.Number_of_rooms__c + ' / ' + bid.vendorData.Number_of_suites__c, '')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Star Rates</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Star_Rating__c != null,if(bid.vendorData.Star_Rating__c == '1',bid.vendorData.Star_Rating__c + ' star',bid.vendorData.Star_Rating__c + ' stars'),'')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Year Built / Renovated</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Year_built__c != null || bid.vendorData.Year_renovated__c != null, bid.vendorData.Year_built__c + ' / ' + bid.vendorData.Year_renovated__c, '')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>100% Non Smoking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.X100_Non_Smoking__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Lift / Elevator</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Lift_Elevator__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Property Entry</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Property_Entry__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Porterage</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Porterage__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Windows that open</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Windows_Open__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Air Conditioning</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Air_conditioning__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>High Speed Internet</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.High_Speed_Internet__c == 'Yes/Complimentary','Yes',bid.vendorData.High_Speed_Internet__c)}<br/>
                                                        <aura:if isTrue="{!bid.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <aura:if isTrue="{!bid.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                                    No
                                                                    <aura:set attribute="else">
                                                                        <lightning:formattedNumber value="{!bid.vendorData.Internet_Charge__c}" 
                                                                                                   style="currency" 
                                                                                                   currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                                   currencyDisplayAs="symbol" />
                                                                    </aura:set>
                                                                </aura:if>
                                                            </aura:set>
                                                        </aura:if>
                                                        <br/>
                                                        {!bid.vendorData.Connection__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pet Allowed</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Pets_Allowed__c}<br/>
                                                        <aura:if isTrue="{!bid.vendorData.Pets_charge__c != null}">
                                                            {!'Fee: '}
                                                            <lightning:formattedNumber value="{!bid.vendorData.Pets_charge__c}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                        </aura:if>
                                                        <br/>
                                                        {!bid.vendorData.Pets_charge_type__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="In-Room Amenities">In-Room Amenities</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Microwave</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Microwave__c} <br/>
                                                        {!bid.vendorData.Microwave_charge_type__c} <br/>
                                                        {!bid.vendorData.Avail_Microwave__c} <br/>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Refrigerator</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Refrigerator__c} <br/>
                                                        {!bid.vendorData.Refrigerator_charge_type__c} <br/>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Coffee Maker</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Coffee_Maker__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hairdryer</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Hairdryers__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Bathtubs</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Bathtub__c == 'Shower only','No',if(bid.vendorData.Bathtub__c != null,'Yes',''))} <br/>
                                                        {!bid.vendorData.Bathtub__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Safe</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Safe__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="On-Site Amenities">On-Site Amenities</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pool / Hot tub</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        <aura:if isTrue="{!bid.vendorData.Pool__c != null}">
                                                            {!if(bid.vendorData.Pool_Seasonal__c == 'Yes',bid.vendorData.Pool__c+'. Seasonal',bid.vendorData.Pool__c)}
                                                        </aura:if>{!' / '}
                                                        <aura:if isTrue="{!bid.vendorData.Hot_Tub__c != null}">
                                                            {!if(bid.vendorData.Hot_tub_seasonal__c == 'Yes',bid.vendorData.Hot_Tub__c+'. Seasonal',bid.vendorData.Hot_Tub__c)}
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Fitness Room</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Fitness_room__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hotel Shuttle</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Hotel_Shuttle__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Airport Shuttle</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Airport_Shuttle__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hotel Bar</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Hotel_Bars__c} <br/>
                                                        {!if(bid.vendorData.hotel_bars_2__c != null,bid.vendorData.hotel_bars_2__c + ' on-site','')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Hotel Restaurant</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Restaurants__c} <br/>
                                                        {!if(bid.vendorData.Restaurants_2__c != null,bid.vendorData.Restaurants_2__c + ' on-site','')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Comp Breakfast</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Breakfast__c == 'Yes/Complimentary','Yes','No')} <br/>
                                                        {!bid.vendorData.Breakfast_type__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Room Service</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Room_Service__c} <br/>
                                                        {!bid.vendorData.Room_Service_hours__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Managers Reception</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Managers_Reception__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Self Parking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Self_Parking__c == 'Yes/Complimentary','Yes',bid.vendorData.Self_Parking__c)} <br/>
                                                        <aura:if isTrue="{!bid.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <lightning:formattedNumber value="{!bid.vendorData.Self_Parking_Charge__c}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Valet Parking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Valet_Parking__c == 'Yes/Complimentary','Yes',bid.vendorData.Valet_Parking__c)} <br/>
                                                        <aura:if isTrue="{!bid.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <lightning:formattedNumber value="{!bid.vendorData.Valet_Parking_Charge__c}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />{!'/' + bid.vendorData.Valet_Parking_Charge_Type__c}
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Bus Parking</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Coach_Bus_Parking__c == 'Yes/Complimentary','Yes',bid.vendorData.Coach_Bus_Parking__c)} <br/>
                                                        <aura:if isTrue="{!bid.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                            Complimentary
                                                            <aura:set attribute="else">
                                                                <lightning:formattedNumber value="{!bid.vendorData.Coach_Bus_Charge__c}" 
                                                                                           style="currency" 
                                                                                           currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                           currencyDisplayAs="symbol" />{!'/' + bid.vendorData.Coach_Bus_Charge_Type__c}
                                                            </aura:set>
                                                        </aura:if>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header"></div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content" style="text-align: center;">
                                                        <lightning:button label="SELECT" variant="brand" class="formButtonBrand btn-custom" iconName="utility:check" iconPosition="right" value="{!bid.recordId}" onclick="{!c.openReviewSubmit}"/>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                    <!-- Add off-site amenities -->
                                    
                                </aura:if>
                                <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                                    <div class="slds-section slds-is-open section-compare_content">
                                        <h4 class="slds-section__title section-compare_content_header">
                                            <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                                <span class="slds-truncate" title="Building Details">Building Details</span>
                                                <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                            </button>
                                        </h4>
                                        <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Lift / Elevator</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Lift_Elevator__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>24 Hour Doorman</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.X24_hour_doorman__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>24 Hour FD</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.X24_Hour_FD__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Air Conditioning</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Air_conditioning__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pet Allowed</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Pets_Allowed__c}<br/>
                                                        <aura:if isTrue="{!bid.vendorData.Pets_charge__c != null}">
                                                            {!'Fee: '}
                                                            <lightning:formattedNumber value="{!bid.vendorData.Pets_charge__c}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(bid.rateDetails.CurrencyIsoCode != null,bid.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                        </aura:if>
                                                        <br/>
                                                        {!bid.vendorData.Pets_charge_type__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Washer / Dryer</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!if(bid.vendorData.Washer_Dryer__c == 'Yes',bid.vendorData.Washer_dryer_in_unit__c+' '+bid.vendorData.Washer_Dryer_Type__c,'No')}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Pool / Hot tub</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        <div style="float:left;width:33%;">{!if(bid.vendorData.Pool__c != null,bid.vendorData.Pool__c + '/','')}{!bid.vendorData.vendorData.Hot_Tub__c}</div>
                                                        <div style="float:left;width:33%;">{!if(bid.vendorData.Pool_Seasonal__c != null,bid.vendorData.vendorData.Pool_Seasonal__c + '/','')}{!bid.vendorData.Hot_tub_seasonal__c}</div>
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Fitness Room</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Fitness_room__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                            <div class="slds-grid slds-wrap section-compare_content_row">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                    <strong>Parking On-Site</strong>
                                                </div>
                                                <aura:iteration items="{!v.compareList}" var="bid">
                                                    <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                        {!bid.vendorData.Parking_on_site__c}
                                                    </div>
                                                </aura:iteration>
                                            </div>
                                        </div>
                                    </div>
                                </aura:if>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Previous RR Shows">Previous RR Shows</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Show Previously Housed</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.rrShows)}">
                                                        <ul class="slds-text-align_left">
                                                            <aura:iteration items="{!bid.rrShows}" var="show">
                                                                <li style="list-style: disc; white-space: pre-wrap;">
                                                                    {!show}
                                                                </li>
                                                            </aura:iteration>
                                                        </ul>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                                <div class="slds-section slds-is-open section-compare_content">
                                    <h4 class="slds-section__title section-compare_content_header">
                                        <button aria-controls="expandableSection" aria-expanded="true" class="slds-button slds-section__title-action slds-button-expandable" onclick="{!c.handleExpand}">
                                            <span class="slds-truncate" title="Airports">Airports</span>
                                            <lightning:buttonIcon iconName="utility:down" variant="bare" alternativeText="Open" iconClass="buttonIcon-bluelight"/>
                                        </button>
                                    </h4>
                                    <div aria-hidden="false" class="slds-section__content" id="expandableSection" style="padding-top:0;color:#333;">
                                        <div class="slds-grid slds-wrap section-compare_content_row">
                                            <div class="slds-col slds-size_1-of-4 section-compare_content_row_header">
                                                <strong>Airport Distance</strong>
                                            </div>
                                            <aura:iteration items="{!v.compareList}" var="bid">
                                                <div class="slds-col slds-size_1-of-4 section-compare_content_row_content">
                                                    <aura:if isTrue="{!!empty(bid.airports)}">
                                                        <ul class="slds-text-align_left">
                                                            <aura:iteration items="{!bid.airports}" var="airport">
                                                                <li style="list-style: disc; white-space: pre-wrap;">
                                                                    {!airport}
                                                                </li>
                                                            </aura:iteration>
                                                        </ul>
                                                    </aura:if>
                                                </div>
                                            </aura:iteration>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="page-section">
                    <div class="slds-grid slds-wrap">
                        <div class="slds-col slds-size_1-of-1" style="margin-top: 2em;text-align: right;">
                            <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}"/>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <aura:if isTrue="{!v.openSelectOptionsAlert}">
      <c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}"/>
    </aura:if>
</aura:component>
```
### VoyajerOptionsHousingCompareController

```
({
  doInit: function (component, event, helper) {
    console.log(component.get("v.housingType"));
    console.log(JSON.stringify(component.get("v.compareList")));
  },
  backOptionsHousing: function (component, event, helper) {
    component.set("v.mainContent", "optionsHousing");
  },
  openReviewSubmit: function (component, event, helper) {
    var theURL = window.location.href;
    var isPreview = theURL.includes('VoyajerPreviewApp');
    var okToAdvance = true;

    if (isPreview){
      okToAdvance = false;
    } else {
      var list = component.get("v.bidOptions");
      var recordId = event.getSource().get("v.value");
      var index = 0;
      var indexActual;
      okToAdvance = true;
  
      list.forEach(function (bid) {
        if (bid.recordId == recordId) {
          indexActual = index;
        }
        index++;
        if (!bid.isEvent){
          console.log('inside not multi');
          if (bid.record.Status__c  === 'Decision' || bid.record.Status__c  === 'In Contracting' || bid.record.Status__c  === 'Contracted' || bid.record.Status__c  === 'Pending Client Signature'){
            console.log('inside status contracted');
            okToAdvance = false;
          }
        }
      });
  
      if ((list[indexActual].record.Status__c === "Decision" || list[indexActual].record.Status__c === "In Contracting" || list[indexActual].record.Status__c === "Contracted" || list[indexActual].record.Status__c === "Pending Client Signature")) {
        okToAdvance = false;
      }
    }

    if (okToAdvance) {
      component.set("v.optionDetailRecordId", indexActual);
      component.set("v.bidOptionsSize", list.length);
      component.set("v.mainContent", "optionsHousingReviewSubmit");
    } else {
      component.set("v.openSelectOptionsAlert", true);
    }
    
  }
});
```
### VoyajerOptionsHousingCompare

```
.THIS .optionBox {
    padding: 1.5em 2em 1.5em;
    position: relative;
    display: flex;
    flex-direction: column;
    background-color: white;
    margin: 1.5em 1em 1.5em 0;
    box-shadow: 4px 4px 4px 0 #dbdbdb;
    border-left: 1px solid #dbdbdb;
    border-top: 1px solid #dbdbdb;
}

.THIS .optionBox.left{
    width: 60%;
}

.THIS .optionBox.right{
    width: 38%;
}

.THIS .optionBoxIcon {
    padding-bottom: 1em;
}

.THIS .optionBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .optionBoxName {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 1.25em;
    display: flex;
    align-items: center;
    justify-content: left;
}

.THIS .optionBoxName p {
    line-height: 1.5;
    margin-bottom: 0.2em !important;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    max-height: 3em;
}

.THIS .optionBoxDescription p {
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    min-height: 1.5em;
}

.THIS .optionBoxDescription .room-type {
    min-width: 1.5em;
}

.THIS .pageContentOptions{
    display: flex;
    flex-flow: wrap;
}

.THIS .pageContentForm p {
    margin-bottom: 0 !important;
}

.THIS .recordTable,
.THIS .tableHeader,
.THIS .tableRow {
    display: flex;
    width: 100%;
}

.THIS .recordTable {
    flex-direction: column;
    border: 1px solid #dbdbdb;
    margin: .5em 0 1em;
}

.THIS .tableHeader {
    flex: 1;
    background-color: #f7f9fe;
    font-weight: 500;
}

.THIS .tableRow {
    flex: 1;
    min-width: 0;
}

.THIS .tableList > .tableRow ~ .tableRow {
    border-top: 1px solid #dbdbdb;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em 1em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}

.THIS .box-decisionBy{
    display: inline-block;
    padding: 1rem 1.5rem;
    background-color: #ec4518;
    border: none;
    text-align: center;
    color: white;
    font-weight: bold;
}

.THIS .pageContentDashboard-grey{
    background-color: #f0f0f0 !important;
    box-shadow: none !important;
}

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .slds-card-overview .information-label{
    background-color: #f0f0f0;
    padding: 1.1em;
    color: #00b4ff;
    font-weight:bold;
}

.THIS .slds-card-overview .information-label-other{
    padding: 1.1em;
    font-weight:bold;
    font-size: 12px;
    border-left: 1px solid #f0f0f0;
    border-bottom: 1px solid #f0f0f0
}

.THIS .slds-card-overview .information-label.first{
    margin-top: 4.9em;
}

.THIS .slds-card-overview .information-label-value{
    padding: 1.1em;
    font-size: 12px;
    border-bottom: 1px solid #f0f0f0;
    text-align: center;
}

/*--------------------
-----Compare------
----------------------*/

.THIS .section-compare{
}

.THIS .section-compare .section-compare_header{
}

.THIS .section-compare .section-compare_header > .section-compare_header_space{
    
}

.THIS .section-compare .section-compare_header > .section-compare_header_item .header{
    background-color: #085ee2;
    color: white;
    text-align: center;
    padding: 1.5em;
    font-weight: bold;
    font-size: 1.1em;
}

.THIS .section-compare .section-compare_header > .section-compare_header_item > h3{
    min-height: 5em;
    padding: 1em 2.2em;
    background-color: #0670c8;
    text-align: center;
    font-size: 1.1rem;
    color: white;
}

.THIS .section-compare .section-compare_content{
    margin-top: 0;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header{
    background-color: #eff2f7;
    border-radius: 0;
    font-size:.875rem;
    font-weight: 600;
}

.THIS .section-compare .section-compare_content > .section-compare_content_header > .slds-button-expandable{
    padding: .8em 1.5em;
    text-transform: none;
}

.THIS .section-compare .section-compare_content .section-compare_content_row{
    border: 1px solid #eff2f7;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_header{
    padding: .8em 1.5em;
}

.THIS .section-compare .section-compare_content .section-compare_content_row > .section-compare_content_row_content{
    padding: .8em 1.5em;
    text-align: center;
}

/*--------------------
-----Button------
----------------------*/

.THIS .slds-button-expandable{
    background:none;
    justify-content:space-between;
    color:#00b4ff;
}

.THIS .slds-button-expandable:hover,
.THIS .slds-button-expandable:focus,
.THIS .slds-button-expandable:active{
    background: none;
    box-shadow: none;
    color:#00b4ff;
}

.THIS .buttonIcon-bluelight{
    color:#00b4ff;
}

.THIS button.btn-blue{
    padding-left: 3rem;
    padding-right: 3rem;
    background-color: #0065ff;
}

.THIS button.btn-blue:active,
.THIS button.btn-blue:visited,
.THIS button.btn-blue:focus {
    background-color: #0453cc;
}


/*--------------------
-----Medias queries------
----------------------*/

@media (min-width: 768px){
    .THIS .section-compare .section-compare_header > .section-compare_header_space{
        width: 22%;
    }
}
```
### VoyajerOptionsHousingCompare

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

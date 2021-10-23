---
layout: default
title: VoyajerOptionsHousingDetail
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsHousingDetail
## Fields
### VoyajerOptionsHousingDetail

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
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />
    <aura:attribute type="List" name="preferencesSelected" 
                    default="['Bus Parking','Valet parking','Self-Parking','Room Service','Comp Breakfast','Hotel Restaurant(s)','Hotel Bar(s)','Airport Shuttle','Hotel Shuttle'
                             ,'Fitness Room','Pool/Hot tub','Safe','Bathtub','Hairdryer','Coffee maker','Refrigerator','Microwave','Rooms / Suites #','Star Rating',
                             'Year Built / Renovated','100% Non-Smoking','Lift / Elevator','Property Entry','Porterage','Windows that open','Air conditioning','High Speed Internet','Pets Allowed']" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />

    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i> Option {!v.optionDetailRecordIdReal}
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}"/>
                        <div class="option_pagination">
                            <button class="option_pagination_button-left" data-bidindex="{!v.optionDetailRecordId}" data-actionto="last" title="{!v.index}" onclick="{!c.changeOptionsHousingDetail}">
                                <i class="fas fa-angle-left"></i>
                            </button>
                            <span class="option_pagination_counter">{!v.optionDetailRecordIdReal} of {!v.bidOptionsSize}</span>
                            <button class="option_pagination_button-right" data-bidindex="{!v.optionDetailRecordId}" data-actionto="next"  onclick="{!c.changeOptionsHousingDetail}">
                                <i class="fas fa-angle-right"></i>
                            </button>
                        </div>
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
                <div class="pageContentForm header">
                    <div style="display: flex;">
                        <div class="optionBox left">
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
                                <!-- Fix By Clay Dev 31 Jan, 2021 #176367796-->
                                <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                                <p>
                                    <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                                    <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                    <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                    <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                </p>
                            </div>
                        </div>  
                        <div class="optionBox right">
                            <div class="slds-grid slds-wrap" style="border-bottom: 1px solid #dbdbdb;padding: 1em 0em;">
                                <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_3-of-4" style="width:66%;">
                                        <span class="room-type">{!roomtype.Units__c}</span> - 
                                        <span class="room-type" style="padding-left: 0em;">{!roomtype.Unit_Type__c}</span>
                                    </div>
                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align: right;width:34%;">
                                        <span class="room-type" style="font-weight:bold;">
                                            <lightning:formattedNumber value="{!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                                                       &nbsp;{!roomtype.Rate_Period__c}
                                            <!--${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}-->
                                        </span>
                                    </div>
                                </aura:iteration>
                            </div>
                            <div class="slds-grid slds-wrap">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="padding: 1em;text-align:center;font-weight:bold;color:#00b4ff;font-style:italic;">
                                    <span>
                                        Weighted Avg Rate:
                                        <lightning:formattedNumber value="{!v.optionDetailRecord.avgrate}" 
                                                                   style="currency" 
                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                   currencyDisplayAs="symbol" />
                                    </span>
                                     <!--${!v.optionDetailRecord.avgrate}-->
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="padding: 1em;text-align:center;font-weight:bold;color:#00b4ff;font-style:italic;">
                                    <span>
                                        Total Cost:
                                        <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                   style="currency" 
                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                   currencyDisplayAs="symbol" />
                                    </span>
                                     <!--${!v.optionDetailRecord.avgrate}-->
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="text-align: center;">
                                    <lightning:button label="SELECT" variant="brand" value="{!v.optionDetailRecord.recordId}" class="formButtonBrand btn-custom" iconName="utility:check" iconPosition="right" onclick="{!c.openReviewSubmit}"/>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="recordTable tableList">
                      <div class="tableHeader">
                          <div style="flex: 1;">Rate Details</div>
                        </div>
                        <div class="tableRow">
                          <div style="flex: 1;font-weight:bold;">
                                <div>Date In - Dates Out,</div>
                                <div>Qty, Bed Type &amp; Rate</div>
                            </div>
                            <div style="flex: 3;">
                                <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                    <div style="width:100%">
                                        <div style="float:left;width:33%;">{!roomtype.Date_In_Text__c} - {!roomtype.Date_Out_Text__c}</div>
                                        <div style="float:left;width:33%;">{!roomtype.Units__c} - {!roomtype.Unit_Type__c}</div>
                                        <div style="float:left;width:33%;">
                                            <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            <span>&nbsp;{!roomtype.Rate_Period__c}</span>
                                        </div>
                                    </div>
                                </aura:iteration>
                            </div>
                        </div>
                        <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                            <aura:if isTrue="{!v.officePreference == 'RRE'}">
                                <div class="tableRow">
                                    <div style="flex: 1;font-weight:bold;"><div>VAT</div></div>
                                    <div style="flex: 3;">
                                        <div style="display:inline-block;width:100%">
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.VAT_Rate__c != null,v.optionDetailRecord.rateDetails.VAT_Rate__c,0)}%</div>
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.VAT__c == true,'Included','Not Included')}</div>
                                            <div style="float:left;width:33%;"></div>
                                        </div>
                                    </div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: 1;font-weight:bold;"><div>CITY TAX</div></div>
                                    <div style="flex: 3;">
                                        <div style="display:inline-block;width:100%">
                                            <div style="float:left;width:33%;">
                                                <span>
                                                    <aura:if isTrue="{!if(and(v.optionDetailRecord.rateDetails.City_Tax_Rate__c != null, v.optionDetailRecord.rateDetails.City_Tax_Rate__c > 0),true,false)}">
                                                        <lightning:formattedNumber value="{!v.optionDetailRecord.rateDetails.City_Tax_Rate__c}" 
                                                                                   style="currency" 
                                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                   currencyDisplayAs="symbol" />
                                                        <aura:set attribute="else">
                                                            {!if(v.optionDetailRecord.rateDetails.City_Tax_Rate_percent__c != null,v.optionDetailRecord.rateDetails.City_Tax_Rate_percent__c+'%','0%')}
                                                        </aura:set>
                                                    </aura:if>
                                                </span>
                                            </div>
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.City_Tax__c == true,'Included','Not Included')}</div>
                                            <div style="float:left;width:33%;">{!v.optionDetailRecord.rateDetails.City_Tax_Type__c}</div>
                                        </div>
                                    </div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: 1;font-weight:bold;"><div>BREAKFAST</div></div>
                                    <div style="flex: 3;">
                                        <div style="display:inline-block;width:100%">
                                            <div style="float:left;width:33%;">
                                                <lightning:formattedNumber value="{!if(v.optionDetailRecord.rateDetails.Breakfast_Rate__c != null,v.optionDetailRecord.rateDetails.Breakfast_Rate__c,0)}" 
                                                                           style="currency" 
                                                                           currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                           currencyDisplayAs="symbol" />
                                            </div>
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.Breakfast__c == true,'Included','Not Included')}</div>
                                            <div style="float:left;width:33"></div>
                                        </div>
                                    </div>
                                </div>
                                <aura:set attribute="else">
                                    <div class="tableRow">
                                        <div style="flex: 1;font-weight:bold;"><div>Tax/Surcharge</div></div>
                                        <div style="flex: 3;">
                                            <div style="display:inline-block;width:100%">
                                                <div style="float:left;width:33%;">{!v.optionDetailRecord.rateDetails.Tax__c}%</div>
                                                <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.Tax_Included__c == true,'Included','Not Included')}</div>
                                                <div style="float:left;width:33%;">
                                                    <span>
                                                        <aura:if isTrue="{!v.optionDetailRecord.rateDetails.Surcharge__c != null}">
                                                            <lightning:formattedNumber value="{!v.optionDetailRecord.rateDetails.Surcharge__c}" 
                                                                                       style="currency" 
                                                                                       minimumFractionDigits="2" 
                                                                                       maximumFractionDigits="2" 
                                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                            <aura:set attribute="else">No Surcharge</aura:set>
                                                        </aura:if>
                                                    </span>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </aura:set>
                            </aura:if>
                        </aura:if>
                        <div class="tableRow">
                          <div style="flex: 1;font-weight:bold;">
                                <div>Concessions</div>
                            </div>
                            <div style="flex: 3;">
                                <ul>
                                    <aura:iteration items="{!v.optionDetailRecord.concessions}" var="concession">
                                        <li style="list-style: disc; white-space: pre-wrap;">
                                            <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                                                {!concession.Concessions_Requested__c+' '+concession.Concession_Provided__c}
                                                <aura:set attribute="else">
                                                    {!concession.Concession_Provided__c}
                                                </aura:set>
                                            </aura:if>
                                            <!--{!concession.Concessions_Requested__c}
                                            <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">{!' '+concession.Concession_Provided__c}</aura:if>-->
                                        </li>
                                    </aura:iteration>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Property Details</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Check-In / Check-Out</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Check_In_Time_Formatted__c != null,v.optionDetailRecord.vendorData.Check_In_Time_Formatted__c + ' / ','')}
                                    {!if(v.optionDetailRecord.vendorData.Check_out_time_formatted__c != null,v.optionDetailRecord.vendorData.Check_out_time_formatted__c,'')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Rooms / Suites</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Number_of_rooms__c != null || v.optionDetailRecord.vendorData.Number_of_suites__c != null, v.optionDetailRecord.vendorData.Number_of_rooms__c + ' / ' + v.optionDetailRecord.vendorData.Number_of_suites__c, '')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Star Rating</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Star_Rating__c != null,if(v.optionDetailRecord.vendorData.Star_Rating__c == '1',v.optionDetailRecord.vendorData.Star_Rating__c + ' star',v.optionDetailRecord.vendorData.Star_Rating__c + ' stars'),'')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Last Renovated</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Year_built__c != null || v.optionDetailRecord.vendorData.Year_renovated__c != null, v.optionDetailRecord.vendorData.Year_built__c + ' / ' + v.optionDetailRecord.vendorData.Year_renovated__c, '')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>100% Non Smoking</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.X100_Non_Smoking__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Lift / Elevator</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Lift_Elevator__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Property Entry</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Property_Entry__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Porterage</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Porterage__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Windows that open</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Windows_Open__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Air Conditioning</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Air_conditioning__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>High Speed Internet</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.High_Speed_Internet__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.High_Speed_Internet__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                        No
                                                        <aura:set attribute="else">
                                                            <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Internet_Charge__c}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                        </aura:set>
                                                    </aura:if>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Connection__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pet Allowed</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_Allowed__c}</div>
                                        <div style="float:left;width:33%;">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Pets_charge__c}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                        </div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_charge_type__c}</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">In-Room Amenities</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Microwave</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Microwave__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Microwave_charge_type__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Avail_Microwave__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Refrigerator</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Refrigerator__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Refrigerator_charge_type__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Avail_refrigerators__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Coffee Maker</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Coffee_Maker__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hairdryer</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Hairdryers__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Bathtubs</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Bathtub__c == 'Shower only','No',if(v.optionDetailRecord.vendorData.Bathtub__c != null,'Yes',''))}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Bathtub__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Safe</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Safe__c}
                                </div>
                            </div>
                            <!--</c:auraIfContains>-->
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">On-site Amenities</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pool / Hot tub</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Pool__c != null}">
                                                {!if(v.optionDetailRecord.vendorData.Pool_Seasonal__c == 'Yes',v.optionDetailRecord.vendorData.Pool__c+'. Seasonal',v.optionDetailRecord.vendorData.Pool__c)}
                                            </aura:if>{!' / '}
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Hot_Tub__c != null}">
                                                {!if(v.optionDetailRecord.vendorData.Hot_tub_seasonal__c == 'Yes',v.optionDetailRecord.vendorData.Hot_Tub__c+'. Seasonal',v.optionDetailRecord.vendorData.Hot_Tub__c)}
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Fitness Room</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Fitness_room__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hotel Shuttle</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Hotel_Shuttle__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Airport Shuttle</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Airport_Shuttle__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hotel Bar</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Hotel_Bars__c}</div>
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.hotel_bars_2__c != null,v.optionDetailRecord.vendorData.hotel_bars_2__c + ' on-site','')}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hotel Restaurant</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Restaurants__c}</div>
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Restaurants_2__c != null,v.optionDetailRecord.vendorData.Restaurants_2__c + ' on-site','')}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Comp Breakfast</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Breakfast__c == 'Yes/Complimentary','Yes','No')}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Breakfast_type__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Room Service</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Room_Service__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Room_Service_hours__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Managers Reception</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Managers_Reception__c}
                                    </div>
                                </div>
                            </div>
                            <!--<c:auraIfContains items="{!v.preferencesSelected}" element="{!'Self-Parking'}">-->
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Self Parking</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Self_Parking__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.Self_Parking__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Self_Parking_Charge__c}" 
                                                                               style="currency" 
                                                                               currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                               currencyDisplayAs="symbol" />
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Valet Parking</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Valet_Parking__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.Valet_Parking__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Valet_Parking__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Valet_Parking_Charge__c}" 
                                                                               style="currency" 
                                                                               currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                               currencyDisplayAs="symbol" />{!'/' + v.optionDetailRecord.vendorData.Valet_Parking_Charge_Type__c}
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Bus Parking</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Coach_Bus_Parking__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.Coach_Bus_Parking__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Coach_Bus_Parking__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Coach_Bus_Charge__c}" 
                                                                               style="currency" 
                                                                               currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                               currencyDisplayAs="symbol" />{!'/' + v.optionDetailRecord.vendorData.Coach_Bus_Charge_Type__c}
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Off-site Amenities</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Walk to Dining</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Restaurant_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Restaurant_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Shopping Center</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Shopping_Mall_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Shopping_Mall_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Laundromat Location</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Laundromat_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Laundromat_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Full Service Gym</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Gym_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Gym_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>24HR Restaurant</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.X24HR_Restaurant__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.X24HR_Restaurant__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Grocery Store</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Grocery_store_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Grocery_store_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                            </div>
                        </div>
                    </aura:if>
                    <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Building Details</div>
                            </div>
                            
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Lift / Elevator</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Lift_Elevator__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>24 Hour Doorman</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.X24_hour_doorman__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>24 Hour FD</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.X24_Hour_FD__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Air Conditioning</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Air_conditioning__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pet Allowed</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_Allowed__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_charge__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_charge_type__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Washer / Dryer</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Washer_Dryer__c == 'Yes',v.optionDetailRecord.vendorData.Washer_dryer_in_unit__c+' '+v.optionDetailRecord.vendorData.Washer_Dryer_Type__c,'No')}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pool / Hot tub</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Pool__c != null,v.optionDetailRecord.vendorData.Pool__c + '/','')}{!v.optionDetailRecord.vendorData.Hot_Tub__c}</div>
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Pool_Seasonal__c != null,v.optionDetailRecord.vendorData.Pool_Seasonal__c + '/','')}{!v.optionDetailRecord.vendorData.Hot_tub_seasonal__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Fitness Room</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Fitness_room__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Parking On-Site</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Parking_on_site__c}
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Previous RR Shows</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Shows Previously Housed</div>
                                </div>
                                <div style="flex: 3;">
                                    <ul>
                                        <aura:iteration items="{!v.optionDetailRecord.rrShows}" var="show">
                                            <li style="list-style: disc; white-space: pre-wrap;">
                                                <div>{!show}</div>
                                            </li>
                                        </aura:iteration>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Airports</div>
                            </div>
                            
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Airport Distance</div>
                                </div>
                                <div style="flex: 3;">
                                    <ul>
                                        <aura:iteration items="{!v.optionDetailRecord.airports}" var="airport">
                                            <li style="list-style: disc; white-space: pre-wrap;">
                                                <div>{!airport}</div>
                                            </li>
                                        </aura:iteration>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </aura:if>
                </div>
            </div>
        </div>
    </div>
    <aura:if isTrue="{!v.openSelectOptionsAlert}">
        <c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}"/>
      </aura:if>
</aura:component>
```
### VoyajerOptionsHousingDetail

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

.THIS .option_pagination{
    margin-left: 1em;
    border: 1px solid #09b7ff;
    border-radius: 3em;
    background-color: white;
}

.THIS .option_pagination .option_pagination_button-left{
    padding: .6em .5em;
    border-top-left-radius: 3em;
    border-bottom-left-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_button-right{
    padding: .6em .5em;
    border-top-right-radius: 3em;
    border-bottom-right-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_counter{
    padding: .4em 1em;
}

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em 1.25em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}
```
### VoyajerOptionsHousingDetail

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingDetailController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        console.log(component.get("v.housingType"));
        callToParent.setParam("action","loadOptionsHousingDetail");
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    backOptionsHousing: function(component,event,helper){
        component.set("v.mainContent","optionsHousing");
    },
    openReviewSubmit: function(component,event,helper){

      var theURL = window.location.href;
      var isPreview = theURL.includes('VoyajerPreviewApp');
      var okToAdvance = true;

      if (isPreview){
        okToAdvance = false;
      } else {
        var bidindex = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var recordId = event.getSource().get("v.value");
        var index = 0;
        var indexActual;
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
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.optionDetailRecordId", indexActual);
        component.set("v.bidOptionsSize", list.length);
        component.set("v.mainContent", "optionsHousingReviewSubmit");
      } else {
        component.set("v.openSelectOptionsAlert", true);
      }
    },
    changeOptionsHousingDetail: function(component,event,helper){
        var index = parseInt(event.currentTarget.dataset.bidindex);
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        console.log(list.length);
        
        if(event.currentTarget.dataset.actionto == 'next')
            index = index + 1;
        else
            index = index - 1;

        console.log(index);
        if((event.currentTarget.dataset.actionto == 'next' && index < list.length) || (event.currentTarget.dataset.actionto == 'last' && index >= 0)){
            component.set("v.optionDetailRecordId",index);
            component.set("v.optionDetailRecordIdReal",index + 1);
            component.set("v.bidOptionsSize",list.length);
            callToParent.setParam("action","loadOptionsHousingDetail");
            callToParent.setParam("data",{
                detailRecordId: list[index].recordId
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerOptionsHousingDetailHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerOptionsHousingDetail

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
    <aura:attribute type="Object" name="optionDetailRecord" />
    <aura:attribute type="Integer" name="optionDetailRecordIdReal" />
    <aura:attribute type="Integer" name="bidOptionsSize" />
    <aura:attribute type="List" name="preferencesSelected" 
                    default="['Bus Parking','Valet parking','Self-Parking','Room Service','Comp Breakfast','Hotel Restaurant(s)','Hotel Bar(s)','Airport Shuttle','Hotel Shuttle'
                             ,'Fitness Room','Pool/Hot tub','Safe','Bathtub','Hairdryer','Coffee maker','Refrigerator','Microwave','Rooms / Suites #','Star Rating',
                             'Year Built / Renovated','100% Non-Smoking','Lift / Elevator','Property Entry','Porterage','Windows that open','Air conditioning','High Speed Internet','Pets Allowed']" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />

    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 class="page-header-title">
                            <i class="fas fa-shield-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i> Option {!v.optionDetailRecordIdReal}
                        </h1>
                        <lightning:button label="VIEW ALL OPTIONS" variant="brand" class="formButtonBrandLight btn-custom" onclick="{!c.backOptionsHousing}"/>
                        <div class="option_pagination">
                            <button class="option_pagination_button-left" data-bidindex="{!v.optionDetailRecordId}" data-actionto="last" title="{!v.index}" onclick="{!c.changeOptionsHousingDetail}">
                                <i class="fas fa-angle-left"></i>
                            </button>
                            <span class="option_pagination_counter">{!v.optionDetailRecordIdReal} of {!v.bidOptionsSize}</span>
                            <button class="option_pagination_button-right" data-bidindex="{!v.optionDetailRecordId}" data-actionto="next"  onclick="{!c.changeOptionsHousingDetail}">
                                <i class="fas fa-angle-right"></i>
                            </button>
                        </div>
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
                <div class="pageContentForm header">
                    <div style="display: flex;">
                        <div class="optionBox left">
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
                                <!-- Fix By Clay Dev 31 Jan, 2021 #176367796-->
                                <p style="font-size: 12px;">{!v.optionDetailRecord.phone}</p>
                                <p>
                                    <i class="fas fa-wifi" style="{!if(or(v.optionDetailRecord.connection == 'Wireless',v.optionDetailRecord.connection == 'Wireless and Wired'),'color:#007bff;','display:none;')}"></i>
                                    <i class="fas fa-swimming-pool" style="{!if(v.optionDetailRecord.pool == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                    <i class="fas fa-paw" style="{!if(v.optionDetailRecord.pets_allowed == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                    <i class="fas fa-bus" style="{!if(v.optionDetailRecord.hotel_shuttle == 'Yes','color:#007bff;margin-left: 10px;','display:none;')}"></i>
                                </p>
                            </div>
                        </div>  
                        <div class="optionBox right">
                            <div class="slds-grid slds-wrap" style="border-bottom: 1px solid #dbdbdb;padding: 1em 0em;">
                                <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_3-of-4" style="width:66%;">
                                        <span class="room-type">{!roomtype.Units__c}</span> - 
                                        <span class="room-type" style="padding-left: 0em;">{!roomtype.Unit_Type__c}</span>
                                    </div>
                                    <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-4" style="text-align: right;width:34%;">
                                        <span class="room-type" style="font-weight:bold;">
                                            <lightning:formattedNumber value="{!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                                                       &nbsp;{!roomtype.Rate_Period__c}
                                            <!--${!if(and(roomtype.Rate__c != null,roomtype.Rate__c != ''),roomtype.Rate__c,'0.00')}-->
                                        </span>
                                    </div>
                                </aura:iteration>
                            </div>
                            <div class="slds-grid slds-wrap">
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="padding: 1em;text-align:center;font-weight:bold;color:#00b4ff;font-style:italic;">
                                    <span>
                                        Weighted Avg Rate:
                                        <lightning:formattedNumber value="{!v.optionDetailRecord.avgrate}" 
                                                                   style="currency" 
                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                   currencyDisplayAs="symbol" />
                                    </span>
                                     <!--${!v.optionDetailRecord.avgrate}-->
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="padding: 1em;text-align:center;font-weight:bold;color:#00b4ff;font-style:italic;">
                                    <span>
                                        Total Cost:
                                        <lightning:formattedNumber value="{!v.optionDetailRecord.totalrate}" 
                                                                   style="currency" 
                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                   currencyDisplayAs="symbol" />
                                    </span>
                                     <!--${!v.optionDetailRecord.avgrate}-->
                                </div>
                                <div class="slds-col slds-size_1-of-1 slds-medium-size_1-of-1" style="text-align: center;">
                                    <lightning:button label="SELECT" variant="brand" value="{!v.optionDetailRecord.recordId}" class="formButtonBrand btn-custom" iconName="utility:check" iconPosition="right" onclick="{!c.openReviewSubmit}"/>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="recordTable tableList">
                      <div class="tableHeader">
                          <div style="flex: 1;">Rate Details</div>
                        </div>
                        <div class="tableRow">
                          <div style="flex: 1;font-weight:bold;">
                                <div>Date In - Dates Out,</div>
                                <div>Qty, Bed Type &amp; Rate</div>
                            </div>
                            <div style="flex: 3;">
                                <aura:iteration items="{!v.optionDetailRecord.roomTypes}" var="roomtype">
                                    <div style="width:100%">
                                        <div style="float:left;width:33%;">{!roomtype.Date_In_Text__c} - {!roomtype.Date_Out_Text__c}</div>
                                        <div style="float:left;width:33%;">{!roomtype.Units__c} - {!roomtype.Unit_Type__c}</div>
                                        <div style="float:left;width:33%;">
                                            <lightning:formattedNumber value="{!if(roomtype.Rate__c != null,roomtype.Rate__c,'0.00')}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                            <span>&nbsp;{!roomtype.Rate_Period__c}</span>
                                        </div>
                                    </div>
                                </aura:iteration>
                            </div>
                        </div>
                        <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                            <aura:if isTrue="{!v.officePreference == 'RRE'}">
                                <div class="tableRow">
                                    <div style="flex: 1;font-weight:bold;"><div>VAT</div></div>
                                    <div style="flex: 3;">
                                        <div style="display:inline-block;width:100%">
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.VAT_Rate__c != null,v.optionDetailRecord.rateDetails.VAT_Rate__c,0)}%</div>
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.VAT__c == true,'Included','Not Included')}</div>
                                            <div style="float:left;width:33%;"></div>
                                        </div>
                                    </div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: 1;font-weight:bold;"><div>CITY TAX</div></div>
                                    <div style="flex: 3;">
                                        <div style="display:inline-block;width:100%">
                                            <div style="float:left;width:33%;">
                                                <span>
                                                    <aura:if isTrue="{!if(and(v.optionDetailRecord.rateDetails.City_Tax_Rate__c != null, v.optionDetailRecord.rateDetails.City_Tax_Rate__c > 0),true,false)}">
                                                        <lightning:formattedNumber value="{!v.optionDetailRecord.rateDetails.City_Tax_Rate__c}" 
                                                                                   style="currency" 
                                                                                   currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                   currencyDisplayAs="symbol" />
                                                        <aura:set attribute="else">
                                                            {!if(v.optionDetailRecord.rateDetails.City_Tax_Rate_percent__c != null,v.optionDetailRecord.rateDetails.City_Tax_Rate_percent__c+'%','0%')}
                                                        </aura:set>
                                                    </aura:if>
                                                </span>
                                            </div>
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.City_Tax__c == true,'Included','Not Included')}</div>
                                            <div style="float:left;width:33%;">{!v.optionDetailRecord.rateDetails.City_Tax_Type__c}</div>
                                        </div>
                                    </div>
                                </div>
                                <div class="tableRow">
                                    <div style="flex: 1;font-weight:bold;"><div>BREAKFAST</div></div>
                                    <div style="flex: 3;">
                                        <div style="display:inline-block;width:100%">
                                            <div style="float:left;width:33%;">
                                                <lightning:formattedNumber value="{!if(v.optionDetailRecord.rateDetails.Breakfast_Rate__c != null,v.optionDetailRecord.rateDetails.Breakfast_Rate__c,0)}" 
                                                                           style="currency" 
                                                                           currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                           currencyDisplayAs="symbol" />
                                            </div>
                                            <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.Breakfast__c == true,'Included','Not Included')}</div>
                                            <div style="float:left;width:33"></div>
                                        </div>
                                    </div>
                                </div>
                                <aura:set attribute="else">
                                    <div class="tableRow">
                                        <div style="flex: 1;font-weight:bold;"><div>Tax/Surcharge</div></div>
                                        <div style="flex: 3;">
                                            <div style="display:inline-block;width:100%">
                                                <div style="float:left;width:33%;">{!v.optionDetailRecord.rateDetails.Tax__c}%</div>
                                                <div style="float:left;width:33%;">{!if(v.optionDetailRecord.rateDetails.Tax_Included__c == true,'Included','Not Included')}</div>
                                                <div style="float:left;width:33%;">
                                                    <span>
                                                        <aura:if isTrue="{!v.optionDetailRecord.rateDetails.Surcharge__c != null}">
                                                            <lightning:formattedNumber value="{!v.optionDetailRecord.rateDetails.Surcharge__c}" 
                                                                                       style="currency" 
                                                                                       minimumFractionDigits="2" 
                                                                                       maximumFractionDigits="2" 
                                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                            <aura:set attribute="else">No Surcharge</aura:set>
                                                        </aura:if>
                                                    </span>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                </aura:set>
                            </aura:if>
                        </aura:if>
                        <div class="tableRow">
                          <div style="flex: 1;font-weight:bold;">
                                <div>Concessions</div>
                            </div>
                            <div style="flex: 3;">
                                <ul>
                                    <aura:iteration items="{!v.optionDetailRecord.concessions}" var="concession">
                                        <li style="list-style: disc; white-space: pre-wrap;">
                                            <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                                                {!concession.Concessions_Requested__c+' '+concession.Concession_Provided__c}
                                                <aura:set attribute="else">
                                                    {!concession.Concession_Provided__c}
                                                </aura:set>
                                            </aura:if>
                                            <!--{!concession.Concessions_Requested__c}
                                            <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">{!' '+concession.Concession_Provided__c}</aura:if>-->
                                        </li>
                                    </aura:iteration>
                                </ul>
                            </div>
                        </div>
                    </div>
                    <aura:if isTrue="{!v.housingType!='Corporate_Housing'}">
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Property Details</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Check-In / Check-Out</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Check_In_Time_Formatted__c != null,v.optionDetailRecord.vendorData.Check_In_Time_Formatted__c + ' / ','')}
                                    {!if(v.optionDetailRecord.vendorData.Check_out_time_formatted__c != null,v.optionDetailRecord.vendorData.Check_out_time_formatted__c,'')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Rooms / Suites</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Number_of_rooms__c != null || v.optionDetailRecord.vendorData.Number_of_suites__c != null, v.optionDetailRecord.vendorData.Number_of_rooms__c + ' / ' + v.optionDetailRecord.vendorData.Number_of_suites__c, '')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Star Rating</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Star_Rating__c != null,if(v.optionDetailRecord.vendorData.Star_Rating__c == '1',v.optionDetailRecord.vendorData.Star_Rating__c + ' star',v.optionDetailRecord.vendorData.Star_Rating__c + ' stars'),'')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Last Renovated</div>
                                </div>
                                <div style="flex: 3;">
                                    {!if(v.optionDetailRecord.vendorData.Year_built__c != null || v.optionDetailRecord.vendorData.Year_renovated__c != null, v.optionDetailRecord.vendorData.Year_built__c + ' / ' + v.optionDetailRecord.vendorData.Year_renovated__c, '')}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>100% Non Smoking</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.X100_Non_Smoking__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Lift / Elevator</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Lift_Elevator__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Property Entry</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Property_Entry__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Porterage</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Porterage__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Windows that open</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Windows_Open__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Air Conditioning</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Air_conditioning__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>High Speed Internet</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.High_Speed_Internet__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.High_Speed_Internet__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.High_Speed_Internet__c == 'Yes/Complimentary'}">
                                                        No
                                                        <aura:set attribute="else">
                                                            <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Internet_Charge__c}" 
                                                                                       style="currency" 
                                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                                       currencyDisplayAs="symbol" />
                                                        </aura:set>
                                                    </aura:if>
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Connection__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pet Allowed</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_Allowed__c}</div>
                                        <div style="float:left;width:33%;">
                                            <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Pets_charge__c}" 
                                                                       style="currency" 
                                                                       currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                       currencyDisplayAs="symbol" />
                                        </div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_charge_type__c}</div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">In-Room Amenities</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Microwave</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Microwave__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Microwave_charge_type__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Avail_Microwave__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Refrigerator</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Refrigerator__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Refrigerator_charge_type__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Avail_refrigerators__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Coffee Maker</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Coffee_Maker__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hairdryer</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Hairdryers__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Bathtubs</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Bathtub__c == 'Shower only','No',if(v.optionDetailRecord.vendorData.Bathtub__c != null,'Yes',''))}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Bathtub__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Safe</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Safe__c}
                                </div>
                            </div>
                            <!--</c:auraIfContains>-->
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">On-site Amenities</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pool / Hot tub</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Pool__c != null}">
                                                {!if(v.optionDetailRecord.vendorData.Pool_Seasonal__c == 'Yes',v.optionDetailRecord.vendorData.Pool__c+'. Seasonal',v.optionDetailRecord.vendorData.Pool__c)}
                                            </aura:if>{!' / '}
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Hot_Tub__c != null}">
                                                {!if(v.optionDetailRecord.vendorData.Hot_tub_seasonal__c == 'Yes',v.optionDetailRecord.vendorData.Hot_Tub__c+'. Seasonal',v.optionDetailRecord.vendorData.Hot_Tub__c)}
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Fitness Room</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Fitness_room__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hotel Shuttle</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Hotel_Shuttle__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Airport Shuttle</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Airport_Shuttle__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hotel Bar</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Hotel_Bars__c}</div>
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.hotel_bars_2__c != null,v.optionDetailRecord.vendorData.hotel_bars_2__c + ' on-site','')}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Hotel Restaurant</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Restaurants__c}</div>
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Restaurants_2__c != null,v.optionDetailRecord.vendorData.Restaurants_2__c + ' on-site','')}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Comp Breakfast</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Breakfast__c == 'Yes/Complimentary','Yes','No')}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Breakfast_type__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Room Service</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Room_Service__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Room_Service_hours__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Managers Reception</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Managers_Reception__c}
                                    </div>
                                </div>
                            </div>
                            <!--<c:auraIfContains items="{!v.preferencesSelected}" element="{!'Self-Parking'}">-->
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Self Parking</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Self_Parking__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.Self_Parking__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Self_Parking__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Self_Parking_Charge__c}" 
                                                                               style="currency" 
                                                                               currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                               currencyDisplayAs="symbol" />
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Valet Parking</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Valet_Parking__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.Valet_Parking__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Valet_Parking__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Valet_Parking_Charge__c}" 
                                                                               style="currency" 
                                                                               currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                               currencyDisplayAs="symbol" />{!'/' + v.optionDetailRecord.vendorData.Valet_Parking_Charge_Type__c}
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Bus Parking</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Coach_Bus_Parking__c == 'Yes/Complimentary','Yes',v.optionDetailRecord.vendorData.Coach_Bus_Parking__c)}</div>
                                        <div style="float:left;width:33%;">
                                            <aura:if isTrue="{!v.optionDetailRecord.vendorData.Coach_Bus_Parking__c == 'Yes/Complimentary'}">
                                                Complimentary
                                                <aura:set attribute="else">
                                                    <lightning:formattedNumber value="{!v.optionDetailRecord.vendorData.Coach_Bus_Charge__c}" 
                                                                               style="currency" 
                                                                               currencyCode="{!if(v.optionDetailRecord.rateDetails.CurrencyIsoCode != null,v.optionDetailRecord.rateDetails.CurrencyIsoCode,if(v.officePreference == 'RRE','EUR','USD'))}" 
                                                                               currencyDisplayAs="symbol" />{!'/' + v.optionDetailRecord.vendorData.Coach_Bus_Charge_Type__c}
                                                </aura:set>
                                            </aura:if>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Off-site Amenities</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Walk to Dining</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Restaurant_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Restaurant_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Shopping Center</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Shopping_Mall_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Shopping_Mall_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Laundromat Location</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Laundromat_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Laundromat_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Full Service Gym</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Gym_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Gym_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>24HR Restaurant</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.X24HR_Restaurant__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.X24HR_Restaurant__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Grocery Store</div>
                                </div>
                                <div style="flex: 1;">
                                    <aura:if isTrue="{!v.optionDetailRecord.vendorData.Grocery_store_near_URL__c != null}">
                                        <a href="{!v.optionDetailRecord.vendorData.Grocery_store_near_URL__c}" class="slds-button slds-button_brand formButtonBrandLight btn-custom" target="_blank">VIEW GOOGLE MAPS</a>
                                    </aura:if>
                                </div>
                            </div>
                        </div>
                    </aura:if>
                    <aura:if isTrue="{!v.housingType=='Corporate_Housing'}">
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Building Details</div>
                            </div>
                            
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Lift / Elevator</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Lift_Elevator__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>24 Hour Doorman</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.X24_hour_doorman__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>24 Hour FD</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.X24_Hour_FD__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Air Conditioning</div>
                                </div>
                                <div style="flex: 3;">
                                    {!v.optionDetailRecord.vendorData.Air_conditioning__c}
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pet Allowed</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_Allowed__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_charge__c}</div>
                                        <div style="float:left;width:33%;">{!v.optionDetailRecord.vendorData.Pets_charge_type__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Washer / Dryer</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Washer_Dryer__c == 'Yes',v.optionDetailRecord.vendorData.Washer_dryer_in_unit__c+' '+v.optionDetailRecord.vendorData.Washer_Dryer_Type__c,'No')}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Pool / Hot tub</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Pool__c != null,v.optionDetailRecord.vendorData.Pool__c + '/','')}{!v.optionDetailRecord.vendorData.Hot_Tub__c}</div>
                                        <div style="float:left;width:33%;">{!if(v.optionDetailRecord.vendorData.Pool_Seasonal__c != null,v.optionDetailRecord.vendorData.Pool_Seasonal__c + '/','')}{!v.optionDetailRecord.vendorData.Hot_tub_seasonal__c}</div>
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Fitness Room</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Fitness_room__c}
                                    </div>
                                </div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Parking On-Site</div>
                                </div>
                                <div style="flex: 3;">
                                    <div style="display:inline-block;width:100%">
                                        {!v.optionDetailRecord.vendorData.Parking_on_site__c}
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Previous RR Shows</div>
                            </div>
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Shows Previously Housed</div>
                                </div>
                                <div style="flex: 3;">
                                    <ul>
                                        <aura:iteration items="{!v.optionDetailRecord.rrShows}" var="show">
                                            <li style="list-style: disc; white-space: pre-wrap;">
                                                <div>{!show}</div>
                                            </li>
                                        </aura:iteration>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader">
                                <div style="flex: 1;">Airports</div>
                            </div>
                            
                            <div class="tableRow">
                                <div style="flex: 1;font-weight:bold;">
                                    <div>Airport Distance</div>
                                </div>
                                <div style="flex: 3;">
                                    <ul>
                                        <aura:iteration items="{!v.optionDetailRecord.airports}" var="airport">
                                            <li style="list-style: disc; white-space: pre-wrap;">
                                                <div>{!airport}</div>
                                            </li>
                                        </aura:iteration>
                                    </ul>
                                </div>
                            </div>
                        </div>
                    </aura:if>
                </div>
            </div>
        </div>
    </div>
    <aura:if isTrue="{!v.openSelectOptionsAlert}">
        <c:VoyajerOptionsModalSelectAlert openSelectOptionsAlert="{!v.openSelectOptionsAlert}"/>
      </aura:if>
</aura:component>
```
### VoyajerOptionsHousingDetail

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

.THIS .option_pagination{
    margin-left: 1em;
    border: 1px solid #09b7ff;
    border-radius: 3em;
    background-color: white;
}

.THIS .option_pagination .option_pagination_button-left{
    padding: .6em .5em;
    border-top-left-radius: 3em;
    border-bottom-left-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_button-right{
    padding: .6em .5em;
    border-top-right-radius: 3em;
    border-bottom-right-radius: 3em;
    border: 1px solid #09b7ff;
    background-color: white;
    color: #09b7ff;
}

.THIS .option_pagination .option_pagination_counter{
    padding: .4em 1em;
}

.THIS .formButtonBrandLight.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .formButtonBrand.btn-custom{
    font-size: 12px;
    padding: 0em 3em;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    padding: 0.5em 1.25em;
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
}
```
### VoyajerOptionsHousingDetail

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsHousingDetailController

```
({
	doInit : function(component, event, helper) {
        var index = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        console.log(component.get("v.housingType"));
        callToParent.setParam("action","loadOptionsHousingDetail");
        callToParent.setParam("data",{
            detailRecordId: list[index].recordId
        });
        callToParent.fire();
	},
    backOptionsHousing: function(component,event,helper){
        component.set("v.mainContent","optionsHousing");
    },
    openReviewSubmit: function(component,event,helper){

      var theURL = window.location.href;
      var isPreview = theURL.includes('VoyajerPreviewApp');
      var okToAdvance = true;

      if (isPreview){
        okToAdvance = false;
      } else {
        var bidindex = component.get("v.optionDetailRecordId");
        var list = component.get("v.bidOptions");
        var recordId = event.getSource().get("v.value");
        var index = 0;
        var indexActual;
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
        component.set("v.optionDetailRecordIdReal",parseInt(bidindex) + 1);
        component.set("v.optionDetailRecordId", indexActual);
        component.set("v.bidOptionsSize", list.length);
        component.set("v.mainContent", "optionsHousingReviewSubmit");
      } else {
        component.set("v.openSelectOptionsAlert", true);
      }
    },
    changeOptionsHousingDetail: function(component,event,helper){
        var index = parseInt(event.currentTarget.dataset.bidindex);
        var list = component.get("v.bidOptions");
        var callToParent = component.getEvent("callToParent");
        console.log(list.length);
        
        if(event.currentTarget.dataset.actionto == 'next')
            index = index + 1;
        else
            index = index - 1;

        console.log(index);
        if((event.currentTarget.dataset.actionto == 'next' && index < list.length) || (event.currentTarget.dataset.actionto == 'last' && index >= 0)){
            component.set("v.optionDetailRecordId",index);
            component.set("v.optionDetailRecordIdReal",index + 1);
            component.set("v.bidOptionsSize",list.length);
            callToParent.setParam("action","loadOptionsHousingDetail");
            callToParent.setParam("data",{
                detailRecordId: list[index].recordId
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerOptionsHousingDetailHelper

```
({
	helperMethod : function() {
		
	}
})
```

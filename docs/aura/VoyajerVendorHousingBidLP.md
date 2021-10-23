---
layout: default
title: VoyajerVendorHousingBidLP
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerVendorHousingBidLP
## Fields
### VoyajerVendorHousingBidLP

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorHousingBidLP

```
<aura:component >
    <aura:attribute type="String" name="showAlert"/>

	<aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="userProfile" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="menuSelected" default="edit" />
    <aura:attribute type="String" name="productionOfficePreference" default="" />
    <aura:attribute type="String" name="productionAssocUserName" />
    <aura:attribute type="String" name="productionAssocUserPhone" />
    <aura:attribute type="String" name="productionAssocUserEmail" />
    <aura:attribute type="String" name="productionAssocRole" />
    <aura:attribute type="String" name="noBidReason" default="Sold out" />
    <aura:attribute type="String" name="noBidNotes" default="" />
    <aura:attribute type="String" name="noBidFirstName" default="" />
    <aura:attribute type="String" name="noBidLastName" default="" />
    <aura:attribute type="String" name="noBidTitle" default="" />
    <aura:attribute type="String" name="noBidEmail" default="" />
    <!-- Changes as per 176506748 -->
    <aura:attribute type="String" name="lengthDiv" default="0 of 255" />
    <aura:attribute type="String" name="agreementText" default="Property agrees to negotiate with Road Rebel ONLY moving forward and not offer client lower rates directly. If either is breached,
                                                                you agree to pay Road Rebel commission on any room pick-up at your property(s). This also serves as the commission agreement in the event we go to contract.
                                                                By selecting Submit, you are signing this agreement electronically.*" />
    <aura:attribute type="String" name="iata" default="IATA #05-56078-5" />
    <aura:attribute type="String" name="iataRRE" default="IATA #96-06295-6" />
    <aura:attribute type="String" name="reviewName" default="" />
    <aura:attribute type="String" name="reviewTitle" default="" />
    <aura:attribute type="String" name="reviewEmail" default="" />
    <aura:attribute type="String" name="reviewDate" default="" />
    <aura:attribute type="String" name="reviewPhone" default="" />
    <aura:attribute type="Object" name="bidData" />
    <aura:attribute type="Object" name="info" />
    <aura:attribute type="Object" name="revenue" />
    <aura:attribute type="List" name="lodgings" />
    <aura:attribute type="List" name="concessions" />
    <aura:attribute type="Date" name="today" />
    <aura:attribute name="noBidReasons" type="List" default="[
                                                             {'label': 'Sold out', 'value': 'Sold out'},
                                                             {'label': 'Sold out for a portion of stay', 'value': 'Sold out for a portion of stay'},
                                                             {'label': 'Not enough rooms available', 'value': 'Not enough rooms available'},
                                                             {'label': 'Other', 'value': 'Other'}
                                                             ]"/>

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bidData}" action="{!c.loadBidData}" />
    <aura:handler action="{!c.handleCommunicationEvent}" event="c:VoyajerCallToChild" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

    <div>
        <div class="mainMenu">
            <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page" style="margin-top: 1em;">
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='edit'? ' slds-is-active' : '')}">
                    <div class="slds-nav-vertical__action"><span>Housing Bid</span></div>
                </div>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='noBid'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>No Bid</span></div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='review'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='review'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>Review &amp; Submit</span></div>
                    </div>
                </aura:if>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">

                <div class="page-section">
                    <div class="page-header">
                        <aura:if isTrue="{!v.menuSelected=='edit'}">
                            <h1 style="display: flex; align-items: flex-end;">Housing Bid</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='noBid'}">
                            <h1>Sorry to hear you won't be bidding</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='review'}">
                            <h1>Please review and sign your bid below</h1>
                        </aura:if>
                        <div>
                            <div class="productionCoordinatorInfo" style="color: #fff;background-color: #0065ff;font-weight: 700;">
                                <i class="fas fa-comments" style="margin-right: 0.5em;"></i>Need assistance?
                            </div>
                            <div class="productionCoordinatorInfo" style="font-weight: 700;">
                                <div></div>
                                <div>{!v.productionAssocUserRole}</div>
                                <div><i class="fas fa-phone-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserName}</div>
                                <div><i class="far fa-envelope" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserEmail}</div>
                            </div>
                        </div>
                    </div>
                </div>

                <aura:if isTrue="{!v.menuSelected=='edit'}">
                    <div class="pageContentForm">
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Production</sub></label>
                                <h3>{!v.productionName}</h3>
                            </div>
                            <div class="formField" style="text-align: end;">
                                <span><b>{!v.info.bidName}</b></span>
                            </div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Property</sub></label>
                                <p style="margin-top: -0.5em;">
                                    <b>{!v.info.vendorName}</b>
                                    <br/><lightning:formattedRichText value="{!v.info.vendorAddress}"/>
                                </p>
                            </div>
                            <div class="formField">
                                <label><sub class="subLabel">Venue</sub></label>
                                <p style="margin-top: -0.5em;">{!v.info.location}</p>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb;">
                                <div>Check-In</div>
                                <div>Check-Out</div>
                                <div style="flex: none; width: 6em; justify-content: center;">Qty</div>
                                <div>Unit Type</div>
                                <div style="flex: none; width: 6em; justify-content: center;">Nights</div>
                                <div style="flex: 1;">Special Notes</div>
                                <aura:if isTrue="{!v.info.stayRecordType=='Corporate Housing'}">
                                    <div style="flex: 2.5;">Enter your best rate per month</div>
                                <aura:set attribute="else">
                                    <div style="flex: 2.5;">Enter your best rate per room/night</div>
                                </aura:set>
                                </aura:if>
                            </div>
                            <aura:iteration items="{!v.lodgings}" var="lodging">
                                <div class="tableRow">
                                    <div>{!lodging.dateIn}</div>
                                    <div>{!lodging.dateOut}</div>
                                    <div style="flex: none; width: 6em; justify-content: center;">{!lodging.qty}</div>
                                    <div>{!lodging.unitType}</div>
                                    <div style="flex: none; width: 6em; justify-content: center;">{!lodging.nights}</div>
                                    <div style="flex: 1;">{!lodging.specialNotes}</div>
                                    <div style="flex: 2.5;">
                                        <lightning:input aura:id="recordField" type="number" formatter="decimal" name="lodgingCurrencyISOCode" value="{!lodging.rate}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" />
                                    </div>
                                </div>
                            </aura:iteration>
                        </div>
                        <lightning:recordEditForm aura:id="revenueForm"
                                                  objectApiName="Revenue__c"
                                                  recordTypeId="{!v.revenue.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="CurrencyIsoCode">Currency</label>
                                    <lightning:inputField aura:id="recordField" fieldName="CurrencyIsoCode" value="{!v.revenue.CurrencyIsoCode}" variant="label-hidden" required="true" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <aura:if isTrue="{!v.productionOfficePreference=='RRE'}">
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="VAT_Rate__c">VAT Rate %<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" formatter="percent-fixed" name="VAT_Rate__c" value="{!v.revenue.VAT_Rate__c}" step="0.01" label="" min="0" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.VAT__c}" label="Included in rate" name="VAT__c" class="checkboxField formCheckbox" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Breakfast_Rate__c">Breakfast Rate Per Person<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" name="Breakfast_Rate__c" value="{!v.revenue.Breakfast_Rate__c}" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.Breakfast__c}" label="Included in rate" name="Breakfast__c" class="checkboxField formCheckbox" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="cityTaxValue">City Tax Rate<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" formatter="{!if(v.revenue.cityTaxValueType=='Amount','decimal','percent-fixed')}" name="cityTaxValue" value="{!v.revenue.cityTaxValue}" step="0.01" label="" min="0" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <lightning:select name="cityRateType"
                                                              value="{!v.revenue.cityTaxValueType}"
                                                              label="Type">
                                                <option value="Amount" selected="{!v.revenue.cityTaxValueType=='Amount'}">Amount</option>
                                                <option value="Percentage" selected="{!v.revenue.cityTaxValueType=='Percentage'}">Percentage</option>
                                            </lightning:select>
                                        </div>
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="City_Tax_Type__c">Rate Type<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="City_Tax_Type__c" value="{!v.revenue.City_Tax_Type__c}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.City_Tax__c}" label="Included in rate" name="City_Tax__c" class="checkboxField" />
                                        </div>
                                    </div>
                                </div>
                            </aura:if>
                            <aura:if isTrue="{!and(v.productionOfficePreference != 'RRE', v.userProfile != 'CorporateVendor')}">
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Tax__c">Tax %</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="percent-fixed" name="Tax__c" value="{!v.revenue.Tax__c}" step="0.01" label="" min="0" variant="label-hidden" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.Tax_Included__c}" label="Included in rate" name="Tax_Included__c" class="checkboxField formCheckbox" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Surcharge__c">Surcharge</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="decimal" name="lodgingCurrencyISOCode" value="{!v.revenue.Surcharge__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.Surcharge_included__c}" label="Included in rate" name="Surcharge_included__c" class="checkboxField" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </aura:if>
                        </lightning:recordEditForm>
                        <aura:if isTrue="{!not(empty(v.concessions))}">
                            <br/>
                            <aura:if isTrue="{!v.userProfile != 'CorporateVendor'}">
                                <div style="padding: 0.5em;"><b>Concessions requested (check items you can provide):</b></div>
                                <aura:iteration items="{!v.concessions}" var="concession">
                                    <div class="formFieldRadio">
                                        <lightning:input type="checkbox" checked="{!concession.Agreed__c}" label="{!concession.Concessions_Requested__c}" class="checkboxField checkboxList" />
                                    </div>
                                </aura:iteration>
                            </aura:if>
                            <aura:if isTrue="{!v.userProfile == 'CorporateVendor'}">
                                <div class="recordTable tableList">
                                    <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb;">
                                        <div>Concessions requested</div>
                                        <div><span>Concessions provided</span></div>
                                        <div><span>Additional Notes</span></div>
                                    </div>
                                    <aura:iteration items="{!v.concessions}" var="concession">
                                        <div class="tableRow">
                                            <div style="white-space: pre-wrap; align-items: flex-start;">{!concession.Concessions_Requested__c}</div>
                                            <div style="align-items: flex-start;">
                                                <div class="fieldSelect" style="width: 100%;">
                                                    <lightning:select name="Concession_Provided__c" label="" value="{!concession.Concession_Provided__c}" variant="label-hidden" onchange="{!c.handleConcessionProvidedChange}">
                                                        <aura:iteration items="{!concession.concessionProvidedOptions}" var="option">
                                                            <option value="{!option}">{!option}</option>
                                                        </aura:iteration>
                                                        <option value="-- Other --">-- Other (Use additional notes) --</option>
                                                    </lightning:select>
                                                </div>
                                            </div>
                                            <div style="align-items: flex-start;">
                                                <lightning:input aura:id="concessionField"
                                                                 name="customConcession"
                                                                 value="{!concession.customConcession}"
                                                                 label=""
                                                                 variant="label-hidden"
                                                                 required="{!if(concession.Concession_Provided__c=='-- Other --',true,false)}"
                                                                 class="concessionNoteField" />
                                            </div>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </aura:if>
                        </aura:if>
                        <lightning:input aura:id="concessionField" name="customConcession" value="" label="" variant="label-hidden" class="slds-hide" />
                        <br/>
                        <div style="padding: 0.5em;"><b>Road Rebel Commission</b></div>
                        <div class="formColumnThreeChilds">
                            <div class="formFieldRadio">
                                <lightning:input aura:id="recordField" type="checkbox" name="rrCommission" label="{!v.revenue.roadRebelCommission}" checked="{!v.revenue.Commission_Agreed__c}" class="checkboxField checkboxList checkboxRequired" onchange="{!c.onCheckboxChange}" />
                            </div>
                            <div class="formColumnBlank"></div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <br/>
                        <aura:if isTrue="{!v.userProfile != 'CorporateVendor'}">
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="releaseDate">Bid Release Date</label>
                                    <lightning:input aura:id="recordField" name="releaseDate" type="date" dateStyle="short" value="{!v.info.releaseDate}" variant="label-hidden" min="{!v.today}" required="true" format="{!if(v.productionOfficePreference=='RRE','dd-MM-yyyy','mm-DD-yyyy')}"/>
                                </div>
                                <div class="formColumnBlank"></div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <p style="padding-left: 0.5em;">Rooms, rate and concesions are being held until date above</p>
                            <br/>
                        </aura:if>
						<div class="formField">
                            <!-- Changes as per 176506748 -->
                            <label for="notes">Anything else we should know?</label>
                            <lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" value="{!v.info.notes}" aura:id="notesTxtBox" class="formTextarea" variant="label-hidden" />
                        	<div style="float:right;">{!v.lengthDiv}</div>
                        </div>
                        <br/>
                        <div class="formFieldRadio">
                            <lightning:input aura:id="recordField" type="checkbox" label="{!v.agreementText}" required="true" class="checkboxField checkboxList checkboxAgreement checkboxRequired" />
                        </div>
                        <br/>
                        <p style="padding-left: 2.75em; font-weight: 600;">{!if(v.productionOfficePreference=='RRE',v.iataRRE,v.iata)}</p>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="name">Full Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewName" value="{!v.reviewName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewTitle" value="{!v.reviewTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="reviewEmail" value="{!v.reviewEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="phone" name="reviewPhone" value="{!v.reviewPhone}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Unable to bid" class="formButtonPadding" onclick="{!c.handleUnableToBid}" />
                            <!--<lightning:button type="button" label="Place bid" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.handlePlaceBid}" />-->
                            <lightning:button type="button" label="Submit bid" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.handlePlaceBid}" />
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="pageContentForm">
                        <p>We understand if you are unable to bid at this time. Tell us why.</p>
                        <div class="formField">
                            <lightning:radioGroup name="radioGroupRequired" label="" variant="label-hidden"
                                                  options="{!v.noBidReasons}" value="{!v.noBidReason}"
                                                  type="radio" />
                        </div>
                        <aura:if isTrue="{!v.noBidReason=='Other'}">
                            <div class="formField">
                                <label for="noBidNotes">Describe in more detail reason for No Bid</label>
                                <lightning:textarea aura:id="recordField" value="{!v.noBidNotes}" class="formTextarea" variant="label-hidden" required="true" />
                            </div>
                        </aura:if>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="firstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="firstName" value="{!v.noBidFirstName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="lastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="lastName" value="{!v.noBidLastName}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="title" value="{!v.noBidTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="email" value="{!v.noBidEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Submit" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.sendNoBid}" />
                        </div>
                    </div>
                </aura:if>
            </div>


        </div>
    </div>
</aura:component>
```
### VoyajerVendorHousingBidLP

```
.THIS {
}

.THIS .sideBarProfile .slds-nav-vertical__action {
    cursor: default;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    align-items: center;
    display: flex;
    flex: 1;
    padding: 0.5em 1em;
}

.THIS .lodgingRateField {
    display: flex;
    margin-bottom: 0;
    padding: 0;
}

.THIS .lodgingRateField .condition {
    border-color: rgb(194, 57, 52);
    box-shadow: rgb(194, 57, 52) 0 0 0 1px inset;
    background-clip: padding-box;
    border-right: 0;
}

.THIS .lodgingRateField .slds-form-element__label {
    align-items: center;
    background-color: #f7f9fe;
    border: 1px solid #dbdbdb;
    border-top-left-radius: .5em;
    border-bottom-left-radius: .5em;
    display: flex;
    flex: 1;
    font-size: inherit;
    font-weight: 400;
    margin-bottom: 0;
    min-width: 4em;
    padding: 0;
    padding-left: 1em;
}

.THIS .lodgingRateField .slds-form-element__control {
    margin-left: -0.2em;
    padding: 0;
}

.THIS .formFieldCheckbox {
    align-items: flex-end;
    display: flex;
    max-height: 3.75rem;
}

.THIS .noErrorMessage .slds-form-element__help {
    display: none;
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

.THIS .formFieldValue {
    margin-top: -0.25em;
}

.THIS .productionCoordinatorInfo {
    padding: 10px 20px;
    background-color: #fff;
}

.THIS .fieldSelect label {
    display: none;
}

.THIS .concessionNoteField {
    width: 100%;
}
```
### VoyajerVendorHousingBidLPController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        console.log("housingPreference: "+component.get("v.housingPreference"));
        component.set('v.today', today);
        component.set("v.bidData",{});
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorHousingBid");
        callToParent.fire();
	},
    
    loadBidData : function(component, event, helper) {
        var bidData = component.get("v.bidData");
        console.log(bidData);
        if(bidData.info != undefined) {
            component.set("v.info",bidData.info);
            component.set("v.revenue",bidData.revenue);
            component.set("v.lodgings",bidData.lodgings);
            component.set("v.concessions",bidData.concessions);
            component.set("v.reviewName",bidData.reviewName);
            component.set("v.reviewTitle",bidData.reviewTitle);
            component.set("v.reviewEmail",bidData.reviewEmail);
            component.set("v.reviewPhone",bidData.reviewPhone);
        }
    },
    
    //Changes as per 176506748
    checkLength : function(component, event, helper) {
        component.set('v.lengthDiv', '');
        var notesTxtBoxVal = component.find("notesTxtBox").get("v.value");
        component.set('v.lengthDiv', notesTxtBoxVal.length  + ' of 255');
    },
    
    handleBack : function(component, event, helper) {
        component.set("v.mainContent","vendorActions");
    },
    
    handleUnableToBid : function(component, event, helper) {
        component.set("v.menuSelected","noBid");
    },
    
    onCheckboxChange : function(component, event, helper) {
        var inputCmp = event.getSource();
        if(inputCmp.get("v.checked")) inputCmp.setCustomValidity("");
        else inputCmp.setCustomValidity("Offer cannot be considered without.");
        inputCmp.reportValidity();
    },
    
    handleConcessionProvidedChange : function(component, event, helper) {
        var concessionsValid = component.find("concessionField").reduce(function (validSoFar, inputCmp) {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
    },
    
    handlePlaceBid : function(component, event, helper) {

        var thebidid = component.get("v.info").bidId;
        component.set('v.bidId',thebidid);
        var userProfile = component.get("v.userProfile");
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            if(inputCmp.get("v.name") == 'rrCommission') {
                if(inputCmp.get("v.checked")) inputCmp.setCustomValidity("");
                else inputCmp.setCustomValidity("Offer cannot be considered without.");
            }
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        var concessionsValid = true;
        if(userProfile == "CorporateVendor" && component.get("v.concessions").length > 0) {
            concessionsValid = component.find("concessionField").reduce(function (validSoFar, inputCmp) {
                inputCmp.reportValidity();
                return validSoFar && inputCmp.checkValidity();
            }, true);
        }
        if(allValid && concessionsValid) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","placeHousingBid");
            callToParent.setParam("data",{
                info: component.get("v.info"),
                userProfile: component.get("v.userProfile"),
                revenue: component.get("v.revenue"),
                lodgings: component.get("v.lodgings"),
                concessions: component.get("v.concessions"),
                journal: {
                    name: component.get("v.reviewName"),
                    title: component.get("v.reviewTitle"),
                    email: component.get("v.reviewEmail"),
                    phone: component.get("v.reviewPhone")
                }
            });
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({ type: "error", title: "", message: "Please update the invalid form entries and try again." });
            toastEvent.fire();
        }
    },
    
    handleEditBid : function(component, event, helper) {
        component.set("v.menuSelected","edit");
    },
    
    sendNoBid : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var noBidReason = component.get("v.noBidReason");
            if(noBidReason == "Other") noBidReason = component.get("v.noBidNotes");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","unableToBid");
            callToParent.setParam("data",{
                bidId: component.get("v.info").bidId,
                notes: noBidReason,
                journal: {
                    name: component.get("v.noBidFirstName")+" "+component.get("v.noBidLastName"),
                    title: component.get("v.noBidTitle"),
                    email: component.get("v.noBidEmail")
                }
            });
            callToParent.fire();
        }
    },
    
    submitBid : function(component, event, helpewr) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","submitBid");
            callToParent.setParam("data",{
                bidId: component.get("v.info").bidId,
                name: component.get("v.reviewName"),
                title: component.get("v.reviewTitle"),
                email: component.get("v.reviewEmail"),
                phone: component.get("v.reviewPhone"),
                date: component.get("v.reviewDate")
            });
            callToParent.fire();
        }
    }
})
```
### VoyajerVendorHousingBidLP

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerVendorHousingBidLP

```
<aura:component >
    <aura:attribute type="String" name="showAlert"/>

	<aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="userProfile" />
    <aura:attribute type="String" name="productionSelected" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="menuSelected" default="edit" />
    <aura:attribute type="String" name="productionOfficePreference" default="" />
    <aura:attribute type="String" name="productionAssocUserName" />
    <aura:attribute type="String" name="productionAssocUserPhone" />
    <aura:attribute type="String" name="productionAssocUserEmail" />
    <aura:attribute type="String" name="productionAssocRole" />
    <aura:attribute type="String" name="noBidReason" default="Sold out" />
    <aura:attribute type="String" name="noBidNotes" default="" />
    <aura:attribute type="String" name="noBidFirstName" default="" />
    <aura:attribute type="String" name="noBidLastName" default="" />
    <aura:attribute type="String" name="noBidTitle" default="" />
    <aura:attribute type="String" name="noBidEmail" default="" />
    <!-- Changes as per 176506748 -->
    <aura:attribute type="String" name="lengthDiv" default="0 of 255" />
    <aura:attribute type="String" name="agreementText" default="Property agrees to negotiate with Road Rebel ONLY moving forward and not offer client lower rates directly. If either is breached,
                                                                you agree to pay Road Rebel commission on any room pick-up at your property(s). This also serves as the commission agreement in the event we go to contract.
                                                                By selecting Submit, you are signing this agreement electronically.*" />
    <aura:attribute type="String" name="iata" default="IATA #05-56078-5" />
    <aura:attribute type="String" name="iataRRE" default="IATA #96-06295-6" />
    <aura:attribute type="String" name="reviewName" default="" />
    <aura:attribute type="String" name="reviewTitle" default="" />
    <aura:attribute type="String" name="reviewEmail" default="" />
    <aura:attribute type="String" name="reviewDate" default="" />
    <aura:attribute type="String" name="reviewPhone" default="" />
    <aura:attribute type="Object" name="bidData" />
    <aura:attribute type="Object" name="info" />
    <aura:attribute type="Object" name="revenue" />
    <aura:attribute type="List" name="lodgings" />
    <aura:attribute type="List" name="concessions" />
    <aura:attribute type="Date" name="today" />
    <aura:attribute name="noBidReasons" type="List" default="[
                                                             {'label': 'Sold out', 'value': 'Sold out'},
                                                             {'label': 'Sold out for a portion of stay', 'value': 'Sold out for a portion of stay'},
                                                             {'label': 'Not enough rooms available', 'value': 'Not enough rooms available'},
                                                             {'label': 'Other', 'value': 'Other'}
                                                             ]"/>

    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:handler name="change" value="{!v.bidData}" action="{!c.loadBidData}" />
    <aura:handler action="{!c.handleCommunicationEvent}" event="c:VoyajerCallToChild" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />

    <div>
        <div class="mainMenu">
            <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page" style="margin-top: 1em;">
                <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='edit'? ' slds-is-active' : '')}">
                    <div class="slds-nav-vertical__action"><span>Housing Bid</span></div>
                </div>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='noBid'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>No Bid</span></div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='review'}">
                    <div class="{!'slds-nav-vertical__item'+(v.menuSelected=='review'? ' slds-is-active' : '')}">
                        <div class="slds-nav-vertical__action"><span>Review &amp; Submit</span></div>
                    </div>
                </aura:if>
            </nav>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">

                <div class="page-section">
                    <div class="page-header">
                        <aura:if isTrue="{!v.menuSelected=='edit'}">
                            <h1 style="display: flex; align-items: flex-end;">Housing Bid</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='noBid'}">
                            <h1>Sorry to hear you won't be bidding</h1>
                        </aura:if>
                        <aura:if isTrue="{!v.menuSelected=='review'}">
                            <h1>Please review and sign your bid below</h1>
                        </aura:if>
                        <div>
                            <div class="productionCoordinatorInfo" style="color: #fff;background-color: #0065ff;font-weight: 700;">
                                <i class="fas fa-comments" style="margin-right: 0.5em;"></i>Need assistance?
                            </div>
                            <div class="productionCoordinatorInfo" style="font-weight: 700;">
                                <div></div>
                                <div>{!v.productionAssocUserRole}</div>
                                <div><i class="fas fa-phone-alt" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserName}</div>
                                <div><i class="far fa-envelope" style="color: #9f9f9f; margin-right: 0.5em;"></i>{!v.productionAssocUserEmail}</div>
                            </div>
                        </div>
                    </div>
                </div>

                <aura:if isTrue="{!v.menuSelected=='edit'}">
                    <div class="pageContentForm">
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Production</sub></label>
                                <h3>{!v.productionName}</h3>
                            </div>
                            <div class="formField" style="text-align: end;">
                                <span><b>{!v.info.bidName}</b></span>
                            </div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label><sub class="subLabel">Property</sub></label>
                                <p style="margin-top: -0.5em;">
                                    <b>{!v.info.vendorName}</b>
                                    <br/><lightning:formattedRichText value="{!v.info.vendorAddress}"/>
                                </p>
                            </div>
                            <div class="formField">
                                <label><sub class="subLabel">Venue</sub></label>
                                <p style="margin-top: -0.5em;">{!v.info.location}</p>
                            </div>
                        </div>
                        <div class="recordTable tableList">
                            <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb;">
                                <div>Check-In</div>
                                <div>Check-Out</div>
                                <div style="flex: none; width: 6em; justify-content: center;">Qty</div>
                                <div>Unit Type</div>
                                <div style="flex: none; width: 6em; justify-content: center;">Nights</div>
                                <div style="flex: 1;">Special Notes</div>
                                <aura:if isTrue="{!v.info.stayRecordType=='Corporate Housing'}">
                                    <div style="flex: 2.5;">Enter your best rate per month</div>
                                <aura:set attribute="else">
                                    <div style="flex: 2.5;">Enter your best rate per room/night</div>
                                </aura:set>
                                </aura:if>
                            </div>
                            <aura:iteration items="{!v.lodgings}" var="lodging">
                                <div class="tableRow">
                                    <div>{!lodging.dateIn}</div>
                                    <div>{!lodging.dateOut}</div>
                                    <div style="flex: none; width: 6em; justify-content: center;">{!lodging.qty}</div>
                                    <div>{!lodging.unitType}</div>
                                    <div style="flex: none; width: 6em; justify-content: center;">{!lodging.nights}</div>
                                    <div style="flex: 1;">{!lodging.specialNotes}</div>
                                    <div style="flex: 2.5;">
                                        <lightning:input aura:id="recordField" type="number" formatter="decimal" name="lodgingCurrencyISOCode" value="{!lodging.rate}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" />
                                    </div>
                                </div>
                            </aura:iteration>
                        </div>
                        <lightning:recordEditForm aura:id="revenueForm"
                                                  objectApiName="Revenue__c"
                                                  recordTypeId="{!v.revenue.RecordTypeId}"
                                                  density="comfy">
                            <lightning:messages />
                            <div class="formColumnTwoChilds">
                                <div class="formField">
                                    <label for="CurrencyIsoCode">Currency</label>
                                    <lightning:inputField aura:id="recordField" fieldName="CurrencyIsoCode" value="{!v.revenue.CurrencyIsoCode}" variant="label-hidden" required="true" />
                                </div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <aura:if isTrue="{!v.productionOfficePreference=='RRE'}">
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="VAT_Rate__c">VAT Rate %<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" formatter="percent-fixed" name="VAT_Rate__c" value="{!v.revenue.VAT_Rate__c}" step="0.01" label="" min="0" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.VAT__c}" label="Included in rate" name="VAT__c" class="checkboxField formCheckbox" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Breakfast_Rate__c">Breakfast Rate Per Person<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" name="Breakfast_Rate__c" value="{!v.revenue.Breakfast_Rate__c}" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.Breakfast__c}" label="Included in rate" name="Breakfast__c" class="checkboxField formCheckbox" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="cityTaxValue">City Tax Rate<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:input aura:id="recordField" type="number" formatter="{!if(v.revenue.cityTaxValueType=='Amount','decimal','percent-fixed')}" name="cityTaxValue" value="{!v.revenue.cityTaxValue}" step="0.01" label="" min="0" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formField">
                                            <lightning:select name="cityRateType"
                                                              value="{!v.revenue.cityTaxValueType}"
                                                              label="Type">
                                                <option value="Amount" selected="{!v.revenue.cityTaxValueType=='Amount'}">Amount</option>
                                                <option value="Percentage" selected="{!v.revenue.cityTaxValueType=='Percentage'}">Percentage</option>
                                            </lightning:select>
                                        </div>
                                    </div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="City_Tax_Type__c">Rate Type<abbr class="slds-required" title="required"> *</abbr></label>
                                            <lightning:inputField aura:id="recordField" fieldName="City_Tax_Type__c" value="{!v.revenue.City_Tax_Type__c}" variant="label-hidden" required="true" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.City_Tax__c}" label="Included in rate" name="City_Tax__c" class="checkboxField" />
                                        </div>
                                    </div>
                                </div>
                            </aura:if>
                            <aura:if isTrue="{!and(v.productionOfficePreference != 'RRE', v.userProfile != 'CorporateVendor')}">
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Tax__c">Tax %</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="percent-fixed" name="Tax__c" value="{!v.revenue.Tax__c}" step="0.01" label="" min="0" variant="label-hidden" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.Tax_Included__c}" label="Included in rate" name="Tax_Included__c" class="checkboxField formCheckbox" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <label for="Surcharge__c">Surcharge</label>
                                            <lightning:input aura:id="recordField" type="number" formatter="decimal" name="lodgingCurrencyISOCode" value="{!v.revenue.Surcharge__c}" min="0" step="0.01" label="{!v.revenue.CurrencyIsoCode}" variant="label-inline" class="lodgingRateField noErrorMessage" />
                                        </div>
                                        <div class="formFieldCheckbox">
                                            <lightning:input type="checkbox" checked="{!v.revenue.Surcharge_included__c}" label="Included in rate" name="Surcharge_included__c" class="checkboxField" />
                                        </div>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                            </aura:if>
                        </lightning:recordEditForm>
                        <aura:if isTrue="{!not(empty(v.concessions))}">
                            <br/>
                            <aura:if isTrue="{!v.userProfile != 'CorporateVendor'}">
                                <div style="padding: 0.5em;"><b>Concessions requested (check items you can provide):</b></div>
                                <aura:iteration items="{!v.concessions}" var="concession">
                                    <div class="formFieldRadio">
                                        <lightning:input type="checkbox" checked="{!concession.Agreed__c}" label="{!concession.Concessions_Requested__c}" class="checkboxField checkboxList" />
                                    </div>
                                </aura:iteration>
                            </aura:if>
                            <aura:if isTrue="{!v.userProfile == 'CorporateVendor'}">
                                <div class="recordTable tableList">
                                    <div class="tableHeader" style="border-bottom: 1px solid #dbdbdb;">
                                        <div>Concessions requested</div>
                                        <div><span>Concessions provided</span></div>
                                        <div><span>Additional Notes</span></div>
                                    </div>
                                    <aura:iteration items="{!v.concessions}" var="concession">
                                        <div class="tableRow">
                                            <div style="white-space: pre-wrap; align-items: flex-start;">{!concession.Concessions_Requested__c}</div>
                                            <div style="align-items: flex-start;">
                                                <div class="fieldSelect" style="width: 100%;">
                                                    <lightning:select name="Concession_Provided__c" label="" value="{!concession.Concession_Provided__c}" variant="label-hidden" onchange="{!c.handleConcessionProvidedChange}">
                                                        <aura:iteration items="{!concession.concessionProvidedOptions}" var="option">
                                                            <option value="{!option}">{!option}</option>
                                                        </aura:iteration>
                                                        <option value="-- Other --">-- Other (Use additional notes) --</option>
                                                    </lightning:select>
                                                </div>
                                            </div>
                                            <div style="align-items: flex-start;">
                                                <lightning:input aura:id="concessionField"
                                                                 name="customConcession"
                                                                 value="{!concession.customConcession}"
                                                                 label=""
                                                                 variant="label-hidden"
                                                                 required="{!if(concession.Concession_Provided__c=='-- Other --',true,false)}"
                                                                 class="concessionNoteField" />
                                            </div>
                                        </div>
                                    </aura:iteration>
                                </div>
                            </aura:if>
                        </aura:if>
                        <lightning:input aura:id="concessionField" name="customConcession" value="" label="" variant="label-hidden" class="slds-hide" />
                        <br/>
                        <div style="padding: 0.5em;"><b>Road Rebel Commission</b></div>
                        <div class="formColumnThreeChilds">
                            <div class="formFieldRadio">
                                <lightning:input aura:id="recordField" type="checkbox" name="rrCommission" label="{!v.revenue.roadRebelCommission}" checked="{!v.revenue.Commission_Agreed__c}" class="checkboxField checkboxList checkboxRequired" onchange="{!c.onCheckboxChange}" />
                            </div>
                            <div class="formColumnBlank"></div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <br/>
                        <aura:if isTrue="{!v.userProfile != 'CorporateVendor'}">
                            <div class="formColumnThreeChilds">
                                <div class="formField">
                                    <label for="releaseDate">Bid Release Date</label>
                                    <lightning:input aura:id="recordField" name="releaseDate" type="date" dateStyle="short" value="{!v.info.releaseDate}" variant="label-hidden" min="{!v.today}" required="true" format="{!if(v.productionOfficePreference=='RRE','dd-MM-yyyy','mm-DD-yyyy')}"/>
                                </div>
                                <div class="formColumnBlank"></div>
                                <div class="formColumnBlank"></div>
                            </div>
                            <p style="padding-left: 0.5em;">Rooms, rate and concesions are being held until date above</p>
                            <br/>
                        </aura:if>
						<div class="formField">
                            <!-- Changes as per 176506748 -->
                            <label for="notes">Anything else we should know?</label>
                            <lightning:textarea rows="4" cols="50" maxlength="255" onkeyup="{!c.checkLength}" id="txtarea" value="{!v.info.notes}" aura:id="notesTxtBox" class="formTextarea" variant="label-hidden" />
                        	<div style="float:right;">{!v.lengthDiv}</div>
                        </div>
                        <br/>
                        <div class="formFieldRadio">
                            <lightning:input aura:id="recordField" type="checkbox" label="{!v.agreementText}" required="true" class="checkboxField checkboxList checkboxAgreement checkboxRequired" />
                        </div>
                        <br/>
                        <p style="padding-left: 2.75em; font-weight: 600;">{!if(v.productionOfficePreference=='RRE',v.iataRRE,v.iata)}</p>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="name">Full Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewName" value="{!v.reviewName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="reviewTitle" value="{!v.reviewTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="reviewEmail" value="{!v.reviewEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="phone">Phone<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="phone" name="reviewPhone" value="{!v.reviewPhone}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formColumnBlank"></div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Unable to bid" class="formButtonPadding" onclick="{!c.handleUnableToBid}" />
                            <!--<lightning:button type="button" label="Place bid" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.handlePlaceBid}" />-->
                            <lightning:button type="button" label="Submit bid" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.handlePlaceBid}" />
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='noBid'}">
                    <div class="pageContentForm">
                        <p>We understand if you are unable to bid at this time. Tell us why.</p>
                        <div class="formField">
                            <lightning:radioGroup name="radioGroupRequired" label="" variant="label-hidden"
                                                  options="{!v.noBidReasons}" value="{!v.noBidReason}"
                                                  type="radio" />
                        </div>
                        <aura:if isTrue="{!v.noBidReason=='Other'}">
                            <div class="formField">
                                <label for="noBidNotes">Describe in more detail reason for No Bid</label>
                                <lightning:textarea aura:id="recordField" value="{!v.noBidNotes}" class="formTextarea" variant="label-hidden" required="true" />
                            </div>
                        </aura:if>
                        <br/>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="firstName">First Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="firstName" value="{!v.noBidFirstName}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="lastName">Last Name<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="lastName" value="{!v.noBidLastName}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div class="formColumnTwoChilds">
                            <div class="formField">
                                <label for="title">Title<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" name="title" value="{!v.noBidTitle}" label="" variant="label-hidden" required="true" />
                            </div>
                            <div class="formField">
                                <label for="email">Email<abbr class="slds-required" title="required"> *</abbr></label>
                                <lightning:input aura:id="recordField" type="email" name="email" value="{!v.noBidEmail}" label="" variant="label-hidden" required="true" />
                            </div>
                        </div>
                        <div style="text-align: right;">
                            <lightning:button type="button" label="Submit" variant="brand" class="formButtonBrand formButtonPadding" onclick="{!c.sendNoBid}" />
                        </div>
                    </div>
                </aura:if>
            </div>


        </div>
    </div>
</aura:component>
```
### VoyajerVendorHousingBidLP

```
.THIS {
}

.THIS .sideBarProfile .slds-nav-vertical__action {
    cursor: default;
}

.THIS .tableHeader > div,
.THIS .tableRow > div {
    align-items: center;
    display: flex;
    flex: 1;
    padding: 0.5em 1em;
}

.THIS .lodgingRateField {
    display: flex;
    margin-bottom: 0;
    padding: 0;
}

.THIS .lodgingRateField .condition {
    border-color: rgb(194, 57, 52);
    box-shadow: rgb(194, 57, 52) 0 0 0 1px inset;
    background-clip: padding-box;
    border-right: 0;
}

.THIS .lodgingRateField .slds-form-element__label {
    align-items: center;
    background-color: #f7f9fe;
    border: 1px solid #dbdbdb;
    border-top-left-radius: .5em;
    border-bottom-left-radius: .5em;
    display: flex;
    flex: 1;
    font-size: inherit;
    font-weight: 400;
    margin-bottom: 0;
    min-width: 4em;
    padding: 0;
    padding-left: 1em;
}

.THIS .lodgingRateField .slds-form-element__control {
    margin-left: -0.2em;
    padding: 0;
}

.THIS .formFieldCheckbox {
    align-items: flex-end;
    display: flex;
    max-height: 3.75rem;
}

.THIS .noErrorMessage .slds-form-element__help {
    display: none;
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

.THIS .formFieldValue {
    margin-top: -0.25em;
}

.THIS .productionCoordinatorInfo {
    padding: 10px 20px;
    background-color: #fff;
}

.THIS .fieldSelect label {
    display: none;
}

.THIS .concessionNoteField {
    width: 100%;
}
```
### VoyajerVendorHousingBidLPController

```
({
	doInit : function(component, event, helper) {
        var today = $A.localizationService.formatDate(new Date(), "YYYY-MM-DD");
        console.log("housingPreference: "+component.get("v.housingPreference"));
        component.set('v.today', today);
        component.set("v.bidData",{});
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadVendorHousingBid");
        callToParent.fire();
	},
    
    loadBidData : function(component, event, helper) {
        var bidData = component.get("v.bidData");
        console.log(bidData);
        if(bidData.info != undefined) {
            component.set("v.info",bidData.info);
            component.set("v.revenue",bidData.revenue);
            component.set("v.lodgings",bidData.lodgings);
            component.set("v.concessions",bidData.concessions);
            component.set("v.reviewName",bidData.reviewName);
            component.set("v.reviewTitle",bidData.reviewTitle);
            component.set("v.reviewEmail",bidData.reviewEmail);
            component.set("v.reviewPhone",bidData.reviewPhone);
        }
    },
    
    //Changes as per 176506748
    checkLength : function(component, event, helper) {
        component.set('v.lengthDiv', '');
        var notesTxtBoxVal = component.find("notesTxtBox").get("v.value");
        component.set('v.lengthDiv', notesTxtBoxVal.length  + ' of 255');
    },
    
    handleBack : function(component, event, helper) {
        component.set("v.mainContent","vendorActions");
    },
    
    handleUnableToBid : function(component, event, helper) {
        component.set("v.menuSelected","noBid");
    },
    
    onCheckboxChange : function(component, event, helper) {
        var inputCmp = event.getSource();
        if(inputCmp.get("v.checked")) inputCmp.setCustomValidity("");
        else inputCmp.setCustomValidity("Offer cannot be considered without.");
        inputCmp.reportValidity();
    },
    
    handleConcessionProvidedChange : function(component, event, helper) {
        var concessionsValid = component.find("concessionField").reduce(function (validSoFar, inputCmp) {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
    },
    
    handlePlaceBid : function(component, event, helper) {

        var thebidid = component.get("v.info").bidId;
        component.set('v.bidId',thebidid);
        var userProfile = component.get("v.userProfile");
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            if(inputCmp.get("v.name") == 'rrCommission') {
                if(inputCmp.get("v.checked")) inputCmp.setCustomValidity("");
                else inputCmp.setCustomValidity("Offer cannot be considered without.");
            }
            var reportValidity = inputCmp.reportValidity();
            var fieldName = inputCmp.get("v.fieldName");
            if(fieldName == undefined) return validSoFar && inputCmp.checkValidity();
            else return validSoFar && inputCmp.reportValidity();
        }, true);
        var concessionsValid = true;
        if(userProfile == "CorporateVendor" && component.get("v.concessions").length > 0) {
            concessionsValid = component.find("concessionField").reduce(function (validSoFar, inputCmp) {
                inputCmp.reportValidity();
                return validSoFar && inputCmp.checkValidity();
            }, true);
        }
        if(allValid && concessionsValid) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","placeHousingBid");
            callToParent.setParam("data",{
                info: component.get("v.info"),
                userProfile: component.get("v.userProfile"),
                revenue: component.get("v.revenue"),
                lodgings: component.get("v.lodgings"),
                concessions: component.get("v.concessions"),
                journal: {
                    name: component.get("v.reviewName"),
                    title: component.get("v.reviewTitle"),
                    email: component.get("v.reviewEmail"),
                    phone: component.get("v.reviewPhone")
                }
            });
            callToParent.fire();
        } else {
            var toastEvent = $A.get("e.force:showToast");
            toastEvent.setParams({ type: "error", title: "", message: "Please update the invalid form entries and try again." });
            toastEvent.fire();
        }
    },
    
    handleEditBid : function(component, event, helper) {
        component.set("v.menuSelected","edit");
    },
    
    sendNoBid : function(component, event, helper) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var noBidReason = component.get("v.noBidReason");
            if(noBidReason == "Other") noBidReason = component.get("v.noBidNotes");
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","unableToBid");
            callToParent.setParam("data",{
                bidId: component.get("v.info").bidId,
                notes: noBidReason,
                journal: {
                    name: component.get("v.noBidFirstName")+" "+component.get("v.noBidLastName"),
                    title: component.get("v.noBidTitle"),
                    email: component.get("v.noBidEmail")
                }
            });
            callToParent.fire();
        }
    },
    
    submitBid : function(component, event, helpewr) {
        var allValid = component.find("recordField").reduce(function (validSoFar, inputCmp) {
            var reportValidity = inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        if(allValid) {
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","submitBid");
            callToParent.setParam("data",{
                bidId: component.get("v.info").bidId,
                name: component.get("v.reviewName"),
                title: component.get("v.reviewTitle"),
                email: component.get("v.reviewEmail"),
                phone: component.get("v.reviewPhone"),
                date: component.get("v.reviewDate")
            });
            callToParent.fire();
        }
    }
})
```

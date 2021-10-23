---
layout: default
title: VoyajerPageUnavailable
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerPageUnavailable
## Fields
### VoyajerPageUnavailable

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
### VoyajerPageUnavailableHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerPageUnavailable

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerPageUnavailable

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerPageUnavailable

```
<aura:component>

<!--alertType drives what our messages are out of notFound,submitComplete,closeComplete -->
<aura:attribute name="alertType" type="String" default="notFound" />
<aura:attribute name="alertMessage" type="String" />
<aura:attribute name="alertTitle" type="String" />
<aura:attribute name="alertIsError" type="Boolean" default="true" />
<aura:attribute name="alertLink" type="String" default="" />
<aura:attribute name="bidId" type="String" />

  <!--<lightning:inputField fieldName="Withdrawn_Reason__c" class='slds-hide' />-->
  <br />
  <div>
    <div class="mainMenu">
      <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page" style="margin-top: 1em">
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
              <h1 style="display: flex; align-items: flex-end">Housing Bid</h1>
            </aura:if>
            <aura:if isTrue="{!v.menuSelected=='noBid'}">
              <h1>Sorry to hear you won't be bidding</h1>
            </aura:if>
            <aura:if isTrue="{!v.menuSelected=='review'}">
              <h1>Please review and sign your bid below</h1>
            </aura:if>
 
          </div>
        </div>
        <div class="pageContentForm">
          <lightning:layout horizontalAlign="center">
            <!--- TODO: REFACTOR TO TAKE A SUCCESS/ERROR FLAG AND A MESSAGE-->

            <!--notFound-->
              <lightning:layoutItem size="4">
                <div class="slds-text-align_center">
                  <!-- <img src="https://s3-us-west-2.amazonaws.com/supermoney-reviews/businesses/2/mulligan-funding_thumb.png"/>-->
                </div>
                <lightning:card>
                  <div class="slds-p-around_large">
                    <lightning:layout horizontalAlign="center">


                      <aura:if isTrue="{!v.alertIsError}">
                        <lightning:layout horizontalAlign="center">
                          <lightning:layoutItem>
                            <lightning:icon iconName="action:close" size="large" />
                          </lightning:layoutItem>
                        </lightning:layout>
                        <aura:set attribute="else">
                          <lightning:layout horizontalAlign="center">
                            <lightning:layoutItem>
                              <lightning:icon iconName="action:approval" size="large" />
                            </lightning:layoutItem>
                          </lightning:layout>
                        </aura:set>
                      </aura:if>


                      </lightning:layout>
                    <br />
                    <lightning:layout horizontalAlign="center">
                      <lightning:layoutItem>
                        <div class="slds-text-heading_medium">{!v.alertTitle}</div>
                      </lightning:layoutItem>
                    </lightning:layout>
                    <br />

                    <div class="slds-text-align_center">
                        {!v.alertMessage} <br /><br /> 
                        <aura:if isTrue="{!v.alertType=='submitComplete'}">
                          <a href="{!v.alertLink}">View Bid Details</a>
                        </aura:if>
                        <aura:if isTrue="{!v.alertType=='closeComplete'}">
                          <a href="{!v.alertLink}">View Pick Up Report Details</a>
                        </aura:if>
                    </div>
                  </div>
                </lightning:card>
              </lightning:layoutItem>
            <!--notFound-->
          </lightning:layout>
          <br />
        </div>
      </div>
    </div>
  </div>
</aura:component>
```
### VoyajerPageUnavailableRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerPageUnavailableController

```
({
    myAction : function(component, event, helper) {

    }
})
```
### VoyajerPageUnavailable

```
<design:component >

</design:component>
```
### VoyajerPageUnavailable

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>51.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerPageUnavailable

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
### VoyajerPageUnavailableHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerPageUnavailable

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerPageUnavailable

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerPageUnavailable

```
<aura:component>

<!--alertType drives what our messages are out of notFound,submitComplete,closeComplete -->
<aura:attribute name="alertType" type="String" default="notFound" />
<aura:attribute name="alertMessage" type="String" />
<aura:attribute name="alertTitle" type="String" />
<aura:attribute name="alertIsError" type="Boolean" default="true" />
<aura:attribute name="alertLink" type="String" default="" />
<aura:attribute name="bidId" type="String" />

  <!--<lightning:inputField fieldName="Withdrawn_Reason__c" class='slds-hide' />-->
  <br />
  <div>
    <div class="mainMenu">
      <nav class="slds-nav-vertical sideBarProfile" aria-label="Sub page" style="margin-top: 1em">
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
              <h1 style="display: flex; align-items: flex-end">Housing Bid</h1>
            </aura:if>
            <aura:if isTrue="{!v.menuSelected=='noBid'}">
              <h1>Sorry to hear you won't be bidding</h1>
            </aura:if>
            <aura:if isTrue="{!v.menuSelected=='review'}">
              <h1>Please review and sign your bid below</h1>
            </aura:if>
 
          </div>
        </div>
        <div class="pageContentForm">
          <lightning:layout horizontalAlign="center">
            <!--- TODO: REFACTOR TO TAKE A SUCCESS/ERROR FLAG AND A MESSAGE-->

            <!--notFound-->
              <lightning:layoutItem size="4">
                <div class="slds-text-align_center">
                  <!-- <img src="https://s3-us-west-2.amazonaws.com/supermoney-reviews/businesses/2/mulligan-funding_thumb.png"/>-->
                </div>
                <lightning:card>
                  <div class="slds-p-around_large">
                    <lightning:layout horizontalAlign="center">


                      <aura:if isTrue="{!v.alertIsError}">
                        <lightning:layout horizontalAlign="center">
                          <lightning:layoutItem>
                            <lightning:icon iconName="action:close" size="large" />
                          </lightning:layoutItem>
                        </lightning:layout>
                        <aura:set attribute="else">
                          <lightning:layout horizontalAlign="center">
                            <lightning:layoutItem>
                              <lightning:icon iconName="action:approval" size="large" />
                            </lightning:layoutItem>
                          </lightning:layout>
                        </aura:set>
                      </aura:if>


                      </lightning:layout>
                    <br />
                    <lightning:layout horizontalAlign="center">
                      <lightning:layoutItem>
                        <div class="slds-text-heading_medium">{!v.alertTitle}</div>
                      </lightning:layoutItem>
                    </lightning:layout>
                    <br />

                    <div class="slds-text-align_center">
                        {!v.alertMessage} <br /><br /> 
                        <aura:if isTrue="{!v.alertType=='submitComplete'}">
                          <a href="{!v.alertLink}">View Bid Details</a>
                        </aura:if>
                        <aura:if isTrue="{!v.alertType=='closeComplete'}">
                          <a href="{!v.alertLink}">View Pick Up Report Details</a>
                        </aura:if>
                    </div>
                  </div>
                </lightning:card>
              </lightning:layoutItem>
            <!--notFound-->
          </lightning:layout>
          <br />
        </div>
      </div>
    </div>
  </div>
</aura:component>
```
### VoyajerPageUnavailableRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerPageUnavailableController

```
({
    myAction : function(component, event, helper) {

    }
})
```
### VoyajerPageUnavailable

```
<design:component >

</design:component>
```
### VoyajerPageUnavailable

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>51.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

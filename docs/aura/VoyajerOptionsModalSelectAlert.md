---
layout: default
title: VoyajerOptionsModalSelectAlert
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerOptionsModalSelectAlert
## Fields
### VoyajerOptionsModalSelectAlertRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerOptionsModalSelectAlert

```
<design:component >

</design:component>
```
### VoyajerOptionsModalSelectAlert

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsModalSelectAlertHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerOptionsModalSelectAlertController

```
({
    init: function (cmp, event, helper) {
        var theURL = window.location.href;
        console.log('init of modal and url: :: ' + theURL);
        var isPreview = theURL.includes('VoyajerPreviewApp');
        console.log('is preview :: ' + isPreview);
        console.log('init of modal and url: :: ' + theURL);
        if (isPreview){
            cmp.set('v.modalTitleText', 'Preview Only');
            cmp.set('v.modalDetailText', 'Selection not Allowed in Preview');
        }
    },
    closeModal : function(component, event, helper) {
        component.set('v.openSelectOptionsAlert', false);
    }
})
```
### VoyajerOptionsModalSelectAlert

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerOptionsModalSelectAlert

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerOptionsModalSelectAlert

```
<aura:component>
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
    <aura:attribute type="String" name="modalTitleText" default="Invalid Status"/>
    <aura:attribute type="String" name="modalDetailText" default="Need to make a change? Contact your Rebel!"/>
    <aura:handler name="init" value="{!this}" action="{!c.init}" />
<!--###### MODAL BOX Start######-->

  <section
    role="dialog"
    tabindex="-1"
    aria-labelledby="modal-heading-02"
    aria-modal="true"
    aria-describedby="modal-content-id-2"
    class="slds-modal slds-fade-in-open"
  >
    <div class="slds-modal__container">
      <!-- ###### MODAL BOX HEADER Start ######-->
      <header class="slds-modal__header" style="border-bottom: 0">
        <lightning:buttonIcon
          iconName="utility:close"
          alternativeText="close"
          variant="bare-inverse"
          class="slds-modal__close"
          onclick="{!c.closeModal}"
        />
        <h2
          id="modal-heading-01"
          class="slds-text-heading_medium slds-hyphenate"
          style="color: #00b4ff"
        >
        {!v.modalTitleText}
      </h2>
      </header>
      <!--###### MODAL BOX BODY Part Start######-->
      <div
        class="slds-modal__content slds-var-p-around_large"
        id="modal-content-id-1"
        style="padding-top: 0"
      >
        <p style="text-align: left">
       <lightning:formattedRichText value="{!v.modalDetailText}" />
          <!--Need to make a change? Contact your Rebel!-->
        </p>
      </div>
    </div>
  </section>
  <div class="slds-backdrop slds-backdrop_open"></div>
  <!--###### MODAL BOX Part END Here ######-->
</aura:component>
```
### VoyajerOptionsModalSelectAlert

```
.THIS {}
```
### VoyajerOptionsModalSelectAlertRenderer

```
({

// Your renderer method overrides go here

})
```
### VoyajerOptionsModalSelectAlert

```
<design:component >

</design:component>
```
### VoyajerOptionsModalSelectAlert

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>49.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerOptionsModalSelectAlertHelper

```
({
    helperMethod : function() {

    }
})
```
### VoyajerOptionsModalSelectAlertController

```
({
    init: function (cmp, event, helper) {
        var theURL = window.location.href;
        console.log('init of modal and url: :: ' + theURL);
        var isPreview = theURL.includes('VoyajerPreviewApp');
        console.log('is preview :: ' + isPreview);
        console.log('init of modal and url: :: ' + theURL);
        if (isPreview){
            cmp.set('v.modalTitleText', 'Preview Only');
            cmp.set('v.modalDetailText', 'Selection not Allowed in Preview');
        }
    },
    closeModal : function(component, event, helper) {
        component.set('v.openSelectOptionsAlert', false);
    }
})
```
### VoyajerOptionsModalSelectAlert

```
<?xml version="1.0" encoding="UTF-8" standalone="no" ?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E" />
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF" />
	</g>
</svg>
```
### VoyajerOptionsModalSelectAlert

```
<aura:documentation>
	<aura:description>Documentation</aura:description>
	<aura:example name="ExampleName" ref="exampleComponentName" label="Label">
		Example Description
	</aura:example>
</aura:documentation>
```
### VoyajerOptionsModalSelectAlert

```
<aura:component>
    <aura:attribute type="Boolean" name="openSelectOptionsAlert" default="false" />
    <aura:attribute type="String" name="modalTitleText" default="Invalid Status"/>
    <aura:attribute type="String" name="modalDetailText" default="Need to make a change? Contact your Rebel!"/>
    <aura:handler name="init" value="{!this}" action="{!c.init}" />
<!--###### MODAL BOX Start######-->

  <section
    role="dialog"
    tabindex="-1"
    aria-labelledby="modal-heading-02"
    aria-modal="true"
    aria-describedby="modal-content-id-2"
    class="slds-modal slds-fade-in-open"
  >
    <div class="slds-modal__container">
      <!-- ###### MODAL BOX HEADER Start ######-->
      <header class="slds-modal__header" style="border-bottom: 0">
        <lightning:buttonIcon
          iconName="utility:close"
          alternativeText="close"
          variant="bare-inverse"
          class="slds-modal__close"
          onclick="{!c.closeModal}"
        />
        <h2
          id="modal-heading-01"
          class="slds-text-heading_medium slds-hyphenate"
          style="color: #00b4ff"
        >
        {!v.modalTitleText}
      </h2>
      </header>
      <!--###### MODAL BOX BODY Part Start######-->
      <div
        class="slds-modal__content slds-var-p-around_large"
        id="modal-content-id-1"
        style="padding-top: 0"
      >
        <p style="text-align: left">
       <lightning:formattedRichText value="{!v.modalDetailText}" />
          <!--Need to make a change? Contact your Rebel!-->
        </p>
      </div>
    </div>
  </section>
  <div class="slds-backdrop slds-backdrop_open"></div>
  <!--###### MODAL BOX Part END Here ######-->
</aura:component>
```
### VoyajerOptionsModalSelectAlert

```
.THIS {}
```

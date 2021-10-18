---
layout: default
title: rcsfl__Initialize
parent: pages
---

```<apex:page controller="rcsfl.AdminUIController" sidebar="false">
    <apex:form id="adminForm">
    <h1> {!brandName} for Salesforce </h1>
    <P> Please click "Continue" button below to configure {!brandName} for Salesforce. </p>
    <p> The App works with the default configuration.  </p>
    <p> You can configure how to save call logs and fields that appear on call log when user make or receive calls.
    </p>
        <apex:commandButton action="{!initialize}" value="Continue" id="initialize" />
    </apex:form>
</apex:page>```

---
layout: default
title: rcsfl__OpenCTIIndex999
parent: pages
---

```<apex:page showChat="false"
    sidebar="false"
    showHeader="false"
    standardStylesheets="false"
    docType="html-5.0"
    applyHtmlTag="false"
    applyBodyTag="false"
    contentType="text/html"
    controller="rcsfl.RingCentralController"
>
    <base></base>
    <script type="application/javascript">
        var element = document.getElementsByTagName('base')[0];
        var attrValue = false ? "https://apps.ringcentral.com/integration/salesforce/prod/rc/v6.13.0/" : "{!$Resource.OpenCTIQAResource999}/";
        element.setAttribute('href', attrValue);
    </script>
    <style>
      body{overflow: hidden;}
    </style>
    <apex:includeScript value="/support/console/48.0/integration.js"/>
    <apex:includeScript value="/support/api/48.0/interaction.js"/>
    <apex:includeScript value="/support/api/48.0/lightning/opencti_min.js"/>
    <script>
      window.visualRC = {
        actionController: ("{!namespace}" ? "{!namespace}" + "." : "") + 'RingCentralController.',
      };
      window.organizationType = "{!JSENCODE(organizationType)}";
      window.organizationId = "{!organizationId}";
      window.namespace = "{!namespace}";
    </script>
    <script src="external.js"></script>
</apex:page>```

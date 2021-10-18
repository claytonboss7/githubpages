---
layout: default
title: rcsfl__ScheduleMeetingAction
parent: pages
---

```<apex:page showChat="false"
    sidebar="false"
    showHeader="false"
    showQuickActionVfHeader="false"
    standardStylesheets="false"
    docType="html-5.0"
    applyHtmlTag="false"
    applyBodyTag="false"
    contentType="text/html"
    controller="rcsfl.RCVAtionController"
>
  <base></base>
  <script type="application/javascript">
      var element = document.getElementsByTagName('base')[0];
      var attrValue = false ? "https://apps.ringcentral.com/integration/salesforce/prod/rc/v6.13.0/" : "{!$Resource.OpenCTIQAResource999}/";
      element.setAttribute('href', attrValue);
  </script>
    <apex:includeScript value="/canvas/sdk/js/43.0/publisher.js"/>
    <script>
      window.visualRC = {
        actionController: '{!namespace}RCVAtionController.',
      };
      window.organizationType = "{!JSENCODE(organizationType)}";
      window.organizationId = "{!organizationId}";
      window.namespace = "{!namespace}";
      window.baseURL = "{!baseURL}";
    </script>
    <script src="rcvExternal.js"></script>
</apex:page>```

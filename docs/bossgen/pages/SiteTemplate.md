---
layout: default
title: SiteTemplate
parent: pages
---
# Metadata Type
pages


# Filename 
SiteTemplate


# Raw XML
```
<apex:page showHeader="false" id="SiteTemplate">
  <apex:stylesheet value="{!URLFOR($Resource.SiteSamples, 'SiteStyles.css')}"/>
  <apex:insert name="header">
    <c:SiteHeader />
    <hr/>
  </apex:insert>
  <apex:insert name="body"/>
  <apex:insert name="footer">
    <hr/>
    <c:SiteFooter />
    <site:googleAnalyticsTracking />
  </apex:insert>
</apex:page>
```


# Last Modified


# Usage

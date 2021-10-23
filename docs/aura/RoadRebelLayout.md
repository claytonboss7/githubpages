---
layout: default
title: RoadRebelLayout
parent: aura
---
# Metadata Type
CustomObject

# Name
RoadRebelLayout
## Fields
### RoadRebelLayout

```
<design:component label="Road Rebel Theme Layout">
</design:component>
```
### RoadRebelLayoutRenderer

```
({
	// Your renderer method overrides go here
})
```
### RoadRebelLayout

```
.THIS {
    position: relative;
    z-index: 1;
    height: 100%;
    display: flex;
}

.THIS > div {
    flex: 1;
    max-width: 100%;
    max-height: 100%;
}

.THIS .contentRegion {
    padding: 0 !important;
}

.THIS .contentRegion,
.THIS .contentRegion > div,
.THIS .contentRegion > div > div {
    height: 100%;
}

.THIS .contentRegion:before,
.THIS .contentRegion:after {
    content: " ";
    display: flex;
}

.THIS .comm-page-home .cCenterPanel {
    max-width:100% !important;       
    margin:0
}
```
### RoadRebelLayout

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### RoadRebelLayout

```
<aura:component implements="forceCommunity:themeLayout" access="global" description="Sample Custom Theme Layout">
    <div class="container">
        {!v.body}
    </div>
</aura:component>
```
### RoadRebelLayout

```
<design:component label="Road Rebel Theme Layout">
</design:component>
```
### RoadRebelLayoutRenderer

```
({
	// Your renderer method overrides go here
})
```
### RoadRebelLayout

```
.THIS {
    position: relative;
    z-index: 1;
    height: 100%;
    display: flex;
}

.THIS > div {
    flex: 1;
    max-width: 100%;
    max-height: 100%;
}

.THIS .contentRegion {
    padding: 0 !important;
}

.THIS .contentRegion,
.THIS .contentRegion > div,
.THIS .contentRegion > div > div {
    height: 100%;
}

.THIS .contentRegion:before,
.THIS .contentRegion:after {
    content: " ";
    display: flex;
}

.THIS .comm-page-home .cCenterPanel {
    max-width:100% !important;       
    margin:0
}
```
### RoadRebelLayout

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### RoadRebelLayout

```
<aura:component implements="forceCommunity:themeLayout" access="global" description="Sample Custom Theme Layout">
    <div class="container">
        {!v.body}
    </div>
</aura:component>
```

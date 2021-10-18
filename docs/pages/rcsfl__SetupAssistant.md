---
layout: default
title: rcsfl__SetupAssistant
parent: pages
---

```<apex:page sidebar="false" showHeader="false" controller="rcsfl.LightningOutController" title="RingCentral Setup Assistant">

<apex:includeLightning />

<div id="setupAssistant"></div>

<script>
    $Lightning.use('{!namespace}:SetupAssistantApp', function() {
        $Lightning.createComponent(
            '{!namespace}:setupAssistant',
            {
                step: {!$CurrentPage.parameters.step},
                section: '{!$CurrentPage.parameters.section}'
            },
            'setupAssistant',
            function(component) {
            }
        );
    });
</script>

</apex:page>```

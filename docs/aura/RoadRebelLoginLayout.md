---
layout: default
title: RoadRebelLoginLayout
parent: aura
---
# Metadata Type
CustomObject

# Name
RoadRebelLoginLayout
## Fields
### RoadRebelLoginLayout

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### RoadRebelLoginLayout

```
<aura:component implements="forceCommunity:themeLayout" access="global" description="Sample Custom Theme Layout">
    <div>
        <div class="presentation">
            <img src="/resource/CommunityImages/Voyajer_logo_tagline.svg" class="presentationLogo" />
        </div>
        <div class="login">
            <div>
                <div class="headerAndFooter">
                    <img src="/resource/Powered" />
                </div>
                <div class="container">
                    {!v.body}
                </div>
                <div class="headerAndFooter">
                    <!--<a href="javascript:void(0);">Privacy Policy</a>-->
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### RoadRebelLoginLayout

```
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600&display=swap');

.THIS {
    position: relative;
    z-index: 1;
    height: 100%;
    display: flex;
    font-family: 'Poppins', sans-serif;
}

.THIS > div {
    flex: auto;
    width: 50%;
    position: relative;
}

.THIS .headerAndFooter {
    align-items: flex-end;
    display: flex;
    flex: 1;
    justify-content: center;
    margin-bottom: 1em;
}

.THIS .presentation {
    background-color: black;
}

.THIS .presentation:after {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    background-image: url(/resource/CommunityImages/lines-grey.svg);
    background-repeat: no-repeat;
    background-position: 40% 40%;
    filter: invert(1);
    -webkit-filter: invert(100%);
    transform: scaleX(-1) rotate(180deg);
    filter: FlipH;
    -ms-filter: "FlipH";
}

.THIS .presentationLogo {
    position: absolute;
    width: 65%;
    min-width: 20em;
    filter: invert(1);
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.THIS .login {
    overflow-y: auto;
    padding: 1em 0;
    display: flex;
}

.THIS .login > div {
    display: flex;
    flex: 1;
    flex-direction: column;
    max-width: 50em;
    margin: 0 auto;
    width: 80%;
}

.THIS .salesforceIdentityLoginForm2:before {
    content: 'Log in to access your account';
    font-size: 1.25em;
    color: #606060;
    margin-bottom: 1em;
    text-align: center;
    display: block;
    margin-bottom: 1em;
}

.THIS .container {
    width: 70%;
    min-width: 16em;
    margin: 0 auto;
}

.THIS .inputContainer {
    display: flex;
    align-items: center;
    padding: 0.25em 0.5em !important;
    border-top: 0 !important;
    border-left: 0 !important;
    border-right: 0 !important;
    margin-bottom: 1.75em !important;
}

.THIS .uiInput {
    flex: 1;
}

.THIS input {
    width: 80% !important;
    font-size: 1em !important;
}

.THIS .slds-button {
    width: 40% !important;
    min-width: 10em;
    border-radius: 2em !important;
    left: 50%;
    transform: translate(-50%);
    border: 1px solid black !important;
    background-color: #f7f9fe !important;
    transition: 0.3s !important;
}

.THIS .slds-button:hover {
    background-color: #dbdbdb !important;
}

.THIS .slds-button > span {
    color: black !important;
}

.THIS .salesforceIdentityLoginForm2 > div:last-child {
    text-align: center;
}

.THIS .salesforceIdentityLoginForm2 > div:last-child a::before {
    color: #606060;
    content: "Forgot username or password?";
    display: block;
    font-size: 1em;
    left: 50%;
    margin-top: 1em;
    position: relative;
    transform: translate(-50%);
}

.THIS .contentRegion {
    padding: 0 !important;
}

.THIS .contentRegion,
.THIS .contentRegion > div,
.THIS .contentRegion > div > div {
    height: 100%;
}

.THIS .contentRegion > div > div {
    margin: 1em 0;
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

@media (max-width: 800px) {
    .THIS .salesforceIdentityLoginForm2:before {
        font-size: 0.85em;
    }
}

@media (max-width: 800px) and (min-height: 420px), (max-width: 1024px) and (min-height: 1200px) {
    .THIS  {
        flex-direction: column;
    }
    
    .THIS > div {
        flex: 1;
        width: 100%;
    }
    
    .THIS .login {
        flex: 3;
    }
    
    .THIS .salesforceIdentityLoginForm2:before {
        font-size: 1em;
    }
}
```
### RoadRebelLoginLayout

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### RoadRebelLoginLayout

```
<aura:component implements="forceCommunity:themeLayout" access="global" description="Sample Custom Theme Layout">
    <div>
        <div class="presentation">
            <img src="/resource/CommunityImages/Voyajer_logo_tagline.svg" class="presentationLogo" />
        </div>
        <div class="login">
            <div>
                <div class="headerAndFooter">
                    <img src="/resource/Powered" />
                </div>
                <div class="container">
                    {!v.body}
                </div>
                <div class="headerAndFooter">
                    <!--<a href="javascript:void(0);">Privacy Policy</a>-->
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### RoadRebelLoginLayout

```
@import url('https://fonts.googleapis.com/css?family=Poppins:400,500,600&display=swap');

.THIS {
    position: relative;
    z-index: 1;
    height: 100%;
    display: flex;
    font-family: 'Poppins', sans-serif;
}

.THIS > div {
    flex: auto;
    width: 50%;
    position: relative;
}

.THIS .headerAndFooter {
    align-items: flex-end;
    display: flex;
    flex: 1;
    justify-content: center;
    margin-bottom: 1em;
}

.THIS .presentation {
    background-color: black;
}

.THIS .presentation:after {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    background-image: url(/resource/CommunityImages/lines-grey.svg);
    background-repeat: no-repeat;
    background-position: 40% 40%;
    filter: invert(1);
    -webkit-filter: invert(100%);
    transform: scaleX(-1) rotate(180deg);
    filter: FlipH;
    -ms-filter: "FlipH";
}

.THIS .presentationLogo {
    position: absolute;
    width: 65%;
    min-width: 20em;
    filter: invert(1);
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.THIS .login {
    overflow-y: auto;
    padding: 1em 0;
    display: flex;
}

.THIS .login > div {
    display: flex;
    flex: 1;
    flex-direction: column;
    max-width: 50em;
    margin: 0 auto;
    width: 80%;
}

.THIS .salesforceIdentityLoginForm2:before {
    content: 'Log in to access your account';
    font-size: 1.25em;
    color: #606060;
    margin-bottom: 1em;
    text-align: center;
    display: block;
    margin-bottom: 1em;
}

.THIS .container {
    width: 70%;
    min-width: 16em;
    margin: 0 auto;
}

.THIS .inputContainer {
    display: flex;
    align-items: center;
    padding: 0.25em 0.5em !important;
    border-top: 0 !important;
    border-left: 0 !important;
    border-right: 0 !important;
    margin-bottom: 1.75em !important;
}

.THIS .uiInput {
    flex: 1;
}

.THIS input {
    width: 80% !important;
    font-size: 1em !important;
}

.THIS .slds-button {
    width: 40% !important;
    min-width: 10em;
    border-radius: 2em !important;
    left: 50%;
    transform: translate(-50%);
    border: 1px solid black !important;
    background-color: #f7f9fe !important;
    transition: 0.3s !important;
}

.THIS .slds-button:hover {
    background-color: #dbdbdb !important;
}

.THIS .slds-button > span {
    color: black !important;
}

.THIS .salesforceIdentityLoginForm2 > div:last-child {
    text-align: center;
}

.THIS .salesforceIdentityLoginForm2 > div:last-child a::before {
    color: #606060;
    content: "Forgot username or password?";
    display: block;
    font-size: 1em;
    left: 50%;
    margin-top: 1em;
    position: relative;
    transform: translate(-50%);
}

.THIS .contentRegion {
    padding: 0 !important;
}

.THIS .contentRegion,
.THIS .contentRegion > div,
.THIS .contentRegion > div > div {
    height: 100%;
}

.THIS .contentRegion > div > div {
    margin: 1em 0;
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

@media (max-width: 800px) {
    .THIS .salesforceIdentityLoginForm2:before {
        font-size: 0.85em;
    }
}

@media (max-width: 800px) and (min-height: 420px), (max-width: 1024px) and (min-height: 1200px) {
    .THIS  {
        flex-direction: column;
    }
    
    .THIS > div {
        flex: 1;
        width: 100%;
    }
    
    .THIS .login {
        flex: 3;
    }
    
    .THIS .salesforceIdentityLoginForm2:before {
        font-size: 1em;
    }
}
```

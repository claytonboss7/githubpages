---
layout: default
title: forgotPassword
parent: aura
---
# Metadata Type
CustomObject

# Name
forgotPassword
## Fields
### forgotPasswordController

```
({
    handleForgotPassword: function (component, event, helpler) {
        helpler.handleForgotPassword(component, event, helpler);
    },
    onKeyUp: function(component, event, helpler){
    //checks for "enter" key
        if (event.getParam('keyCode')===13) {
            helpler.handleForgotPassword(component, event, helpler);
        }
    },
    
    setExpId: function (component, event, helper) {
        var expId = event.getParam('expid');
        if (expId) {
            component.set("v.expid", expId);
        }
        helper.setBrandingCookie(component, event, helper);
    },

    initialize: function(component, event, helper) {
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap}).fire();
    }
})
```
### forgotPassword

```
<!-- add implements="forceCommunity:availableForAllPageTypes" to surface the component in community builder -->
<aura:component controller="LightningForgotPasswordController">
    <aura:attribute name="usernameLabel" type="String" required="false" default="Username"/>
    <aura:attribute name="submitButtonLabel" type="String" required="false" default="Reset Password"/>
    <aura:attribute name="showError" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="errorMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="checkEmailUrl" type="String" required="true"/>
    <aura:attribute name="expid" type="String" required="false" description="The branding experience ID" />    
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:handler event="c:setExpId" action="{!c.setExpId}"/>    
    <aura:dependency resource="c:setExpId" type="EVENT"/>  
    
    <div>
            <aura:renderIf isTrue="{!v.showError}">
                <div id="error">
                    <ui:outputRichText value="{!v.errorMessage}"/>
                </div>
            </aura:renderIf>
            <div id="sfdc_username_container" class="sfdc">
                <span id="sfdc_user" class="login-icon" data-icon="a"></span>
                <ui:inputText value="" aura:id="username" placeholder="{!v.usernameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
            </div>
    
            <div class="sfdc">
                <ui:button aura:id="submitButton" label="{!v.submitButtonLabel}" press="{!c.handleForgotPassword}" class="sfdc_button"/>
            </div>
    
    </div>
</aura:component>
```
### forgotPasswordHelper

```
({
    qsToEventMap: {
        'expid'  : 'e.c:setExpId'
    },
    
    handleForgotPassword: function (component, event, helpler) {
        var username = component.find("username").get("v.value");
        var checkEmailUrl = component.get("v.checkEmailUrl");
        var action = component.get("c.forgotPassowrd");
        action.setParams({username:username, checkEmailUrl:checkEmailUrl});
        action.setCallback(this, function(a) {
            var rtnValue = a.getReturnValue();
            if (rtnValue != null) {
               component.set("v.errorMessage",rtnValue);
               component.set("v.showError",true);
            }
       });
        $A.enqueueAction(action);
    },

    setBrandingCookie: function (component, event, helpler) {
        var expId = component.get("v.expid");
        if (expId) {
            var action = component.get("c.setExperienceId");
            action.setParams({expId:expId});
            action.setCallback(this, function(a){ });
            $A.enqueueAction(action);
        }
    }
})
```
### forgotPassword

```
.THIS #sfdc_username_container{
    margin-bottom:10px;
    padding: 12px;
    background-color:white;
    border: 1px solid #CCC;
    -webkit-border-radius: 2px;
    -moz-border-radius: 2px;
    border-radius: 2px;
}

.THIS #sfdc_user{
    float:left;
    width:23px;
    height:25px;
    padding-top:1px;
    padding-left:2px;
    margin:0px;

}

.THIS  .login-icon {
    color:#ccc;font-size:22px;
}

.THIS  button.sfdc_button {
    width: 100%;
    margin-top: 15px;
    margin-bottom: 5px;
    color: #fff;
    background-color: #0070d2;
    border-color: #357ebd;
    display: inline-block;
    text-align: center;
    vertical-align: middle;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    padding: 10px 12px;
    font-size: 16px;
    font-family: 'Open Sans', sans-serif;
    font-weight: 300;
    line-height: 1.42857143;
    border-radius: 2px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
}

.THIS  button:hover {
    background-color:#3276b1;
    border-color:#285e8e;
    cursor:pointer;
}

.THIS  input {
    margin-left:10px;
    margin-top: 3px;
    border: 0px solid transparent;
    width: 70%;
    -webkit-appearance: none;
    font-size: 14px;
}

.THIS  #error {
    text-align: center;
    color:#FF0000;
}

.THIS  a {
    color:white;
    text-decoration: none;
}
.THIS  a:hover {
    color:white;
    text-decoration: none;
}
```
### forgotPassword

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>46.0</apiVersion>
    <description>Sample Component for forgotPassword</description>
</AuraDefinitionBundle>
```
### forgotPassword

```
<design:component label="Custom Forgot Password">
    <design:attribute name="checkEmailUrl" default="./CheckPasswordResetEmail"/>
    <design:attribute name="usernameLabel" default="Username"/>
    <design:attribute name="submitButtonLabel" default="Reset Password"/>
</design:component>
```
### forgotPasswordController

```
({
    handleForgotPassword: function (component, event, helpler) {
        helpler.handleForgotPassword(component, event, helpler);
    },
    onKeyUp: function(component, event, helpler){
    //checks for "enter" key
        if (event.getParam('keyCode')===13) {
            helpler.handleForgotPassword(component, event, helpler);
        }
    },
    
    setExpId: function (component, event, helper) {
        var expId = event.getParam('expid');
        if (expId) {
            component.set("v.expid", expId);
        }
        helper.setBrandingCookie(component, event, helper);
    },

    initialize: function(component, event, helper) {
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap}).fire();
    }
})
```
### forgotPassword

```
<!-- add implements="forceCommunity:availableForAllPageTypes" to surface the component in community builder -->
<aura:component controller="LightningForgotPasswordController">
    <aura:attribute name="usernameLabel" type="String" required="false" default="Username"/>
    <aura:attribute name="submitButtonLabel" type="String" required="false" default="Reset Password"/>
    <aura:attribute name="showError" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="errorMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="checkEmailUrl" type="String" required="true"/>
    <aura:attribute name="expid" type="String" required="false" description="The branding experience ID" />    
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:handler event="c:setExpId" action="{!c.setExpId}"/>    
    <aura:dependency resource="c:setExpId" type="EVENT"/>  
    
    <div>
            <aura:renderIf isTrue="{!v.showError}">
                <div id="error">
                    <ui:outputRichText value="{!v.errorMessage}"/>
                </div>
            </aura:renderIf>
            <div id="sfdc_username_container" class="sfdc">
                <span id="sfdc_user" class="login-icon" data-icon="a"></span>
                <ui:inputText value="" aura:id="username" placeholder="{!v.usernameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
            </div>
    
            <div class="sfdc">
                <ui:button aura:id="submitButton" label="{!v.submitButtonLabel}" press="{!c.handleForgotPassword}" class="sfdc_button"/>
            </div>
    
    </div>
</aura:component>
```
### forgotPasswordHelper

```
({
    qsToEventMap: {
        'expid'  : 'e.c:setExpId'
    },
    
    handleForgotPassword: function (component, event, helpler) {
        var username = component.find("username").get("v.value");
        var checkEmailUrl = component.get("v.checkEmailUrl");
        var action = component.get("c.forgotPassowrd");
        action.setParams({username:username, checkEmailUrl:checkEmailUrl});
        action.setCallback(this, function(a) {
            var rtnValue = a.getReturnValue();
            if (rtnValue != null) {
               component.set("v.errorMessage",rtnValue);
               component.set("v.showError",true);
            }
       });
        $A.enqueueAction(action);
    },

    setBrandingCookie: function (component, event, helpler) {
        var expId = component.get("v.expid");
        if (expId) {
            var action = component.get("c.setExperienceId");
            action.setParams({expId:expId});
            action.setCallback(this, function(a){ });
            $A.enqueueAction(action);
        }
    }
})
```
### forgotPassword

```
.THIS #sfdc_username_container{
    margin-bottom:10px;
    padding: 12px;
    background-color:white;
    border: 1px solid #CCC;
    -webkit-border-radius: 2px;
    -moz-border-radius: 2px;
    border-radius: 2px;
}

.THIS #sfdc_user{
    float:left;
    width:23px;
    height:25px;
    padding-top:1px;
    padding-left:2px;
    margin:0px;

}

.THIS  .login-icon {
    color:#ccc;font-size:22px;
}

.THIS  button.sfdc_button {
    width: 100%;
    margin-top: 15px;
    margin-bottom: 5px;
    color: #fff;
    background-color: #0070d2;
    border-color: #357ebd;
    display: inline-block;
    text-align: center;
    vertical-align: middle;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    padding: 10px 12px;
    font-size: 16px;
    font-family: 'Open Sans', sans-serif;
    font-weight: 300;
    line-height: 1.42857143;
    border-radius: 2px;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
}

.THIS  button:hover {
    background-color:#3276b1;
    border-color:#285e8e;
    cursor:pointer;
}

.THIS  input {
    margin-left:10px;
    margin-top: 3px;
    border: 0px solid transparent;
    width: 70%;
    -webkit-appearance: none;
    font-size: 14px;
}

.THIS  #error {
    text-align: center;
    color:#FF0000;
}

.THIS  a {
    color:white;
    text-decoration: none;
}
.THIS  a:hover {
    color:white;
    text-decoration: none;
}
```
### forgotPassword

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>46.0</apiVersion>
    <description>Sample Component for forgotPassword</description>
</AuraDefinitionBundle>
```
### forgotPassword

```
<design:component label="Custom Forgot Password">
    <design:attribute name="checkEmailUrl" default="./CheckPasswordResetEmail"/>
    <design:attribute name="usernameLabel" default="Username"/>
    <design:attribute name="submitButtonLabel" default="Reset Password"/>
</design:component>
```

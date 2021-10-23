---
layout: default
title: loginForm
parent: aura
---
# Metadata Type
CustomObject

# Name
loginForm
## Fields
### loginForm

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>46.0</apiVersion>
    <description>Sample Component for loginForm</description>
</AuraDefinitionBundle>
```
### loginForm

```
<!-- add implements="forceCommunity:availableForAllPageTypes" to surface the component in community builder -->
<aura:component implements="forceCommunity:availableForAllPageTypes" controller="LightningLoginFormController">
    <aura:attribute name="showError" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="errorMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="startUrl" type="String" required="false" description="The url you go to after a successful login" />
    <aura:attribute name="usernameLabel" type="String" required="false" default="Username"/>
    <aura:attribute name="passwordLabel" type="String" required="false" default="Password"/>
    <aura:attribute name="loginButtonLabel" type="String" required="false" default="Log in1"/>
    <aura:attribute name="expid" type="String" required="false" description="The branding experience ID" /> 
    
    <aura:attribute name="showForm" type="Boolean" default="false"/>
    
    <aura:attribute name="forgotPasswordLabel" type="String" required="false" default="Forgot your password?"/>
    <aura:attribute name="selfRegisterLabel" type="String" required="false" default="Not a member?"/>
    <aura:attribute name="forgotPasswordUrl" type="String" required="false" default="/ForgotPassword"/>
    <aura:attribute name="selfRegisterUrl" type="String" required="false" default="/s/SelfRegister"/>
    
    <aura:attribute name="isUsernamePasswordEnabled" type="Boolean" access="private"/>
    <aura:attribute name="isSelfRegistrationEnabled" type="Boolean" access="private"/>
    <aura:attribute name="communityForgotPasswordUrl" type="String" access="private"/>
    <aura:attribute name="communitySelfRegisterUrl" type="String" access="private" default="/s/SelfRegister"/>
    
    <aura:registerevent name="sitePropagatedStartUrl" type="c:setStartUrl"/>
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:dependency resource="c:setStartUrl" type="EVENT"/>
    <!-- Please uncomment
    <aura:dependency resource="siteforce:registerQueryEventMap" type="EVENT"/>
    -->
    <aura:handler event="c:setStartUrl" action="{!c.setStartUrl}"/>
    <aura:handler event="c:setExpId" action="{!c.setExpId}"/>    
    <aura:dependency resource="c:setExpId" type="EVENT"/>  
    <aura:if isTrue="{!v.showForm}">
    	<div>
        <aura:renderIf isTrue="{!v.isUsernamePasswordEnabled}">
            <span>
                <aura:renderIf isTrue="{!v.showError}">
                    <div id="error">
                        <ui:outputRichText value="{!v.errorMessage}"/>
                    </div>
                </aura:renderIf>
            </span>      
            <span class="header">Log in to access your account</span>
            <div id="sfdc_username_container" class="sfdc">
                <ui:inputText value="" aura:id="username" placeholder="{!v.usernameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc" label="{!v.usernameLabel}" labelClass="assistiveText"/>
            </div>
    
            <div id="sfdc_password_container" class="sfdc">
                <ui:inputSecret value="" aura:id="password" placeholder="{!v.passwordLabel}" keyup="{!c.onKeyUp}" class="input sfdc_passwordinput sfdc" label="{!v.passwordLabel}" labelClass="assistiveText"/>
            </div>
    
            <div class="sfdc">
                <ui:button aura:id="submitButton" label="{!v.loginButtonLabel}" press="{!c.handleLogin}" class="sfdc_button"/>
            </div>
            
            <div id="sfdc_forgot" class="sfdc">
                <br/>
                <span><a href="{!if(v.communityForgotPasswordUrl == null, v.forgotPasswordUrl, v.communityForgotPasswordUrl)}">{!v.forgotPasswordLabel}</a></span><br/>
               <!-- <aura:renderIf isTrue="{!v.isSelfRegistrationEnabled}">
                    <span style="float:middle" ><a href="{!if(v.communitySelfRegisterUrl == null, v.selfRegisterUrl, v.communitySelfRegisterUrl)}">{!v.selfRegisterLabel}</a></span>
                </aura:renderIf>  -->                          
            </div> 
        </aura:renderIf>
    </div>
    </aura:if>
</aura:component>
```
### loginFormHelper

```
({
    
    qsToEventMap: {
        'startURL'  : 'e.c:setStartUrl'
    },

    qsToEventMap2: {
        'expid'  : 'e.c:setExpId'
    },
    
    handleNavigation: function(component,event,helper){
        var params = {};
        var parser = document.createElement('a');
        parser.href = decodeURIComponent(window.location.href);
        console.log('parser.href'+parser.href);
        var query = parser.search.substring(1);
        var vars = query.split('&');
        for (var i = 0; i < vars.length; i++) {
            var pair = vars[i].split('=');
            params[pair[0]] = decodeURIComponent(pair[1]);
        }
        console.log('params'+JSON.stringify(params));
        if((params['userId']==null || params['userId']=='') && params['record']!=null){
            //alert('Seems like you are already registered !!');
            window.location.href = window.location.href.replace('/s/login','/s/login/SelfRegister');
        }else{
            component.set('v.showForm',true);
        }
    },
    
    handleLogin: function (component, event, helpler) {
        var username = component.find("username").get("v.value");
        var password = component.find("password").get("v.value");
        var action = component.get("c.login");
        var startUrl = component.get("v.startUrl");
        
        startUrl = decodeURIComponent(startUrl);
        
        action.setParams({username:username, password:password, startUrl:startUrl});
        action.setCallback(this, function(a){
            var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set("v.errorMessage",rtnValue);
                component.set("v.showError",true);
            }
        });
        $A.enqueueAction(action);
    },
    
    getIsUsernamePasswordEnabled : function (component, event, helpler) {
        var action = component.get("c.getIsUsernamePasswordEnabled");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.isUsernamePasswordEnabled',rtnValue);
            }
        });
        $A.enqueueAction(action);
    },
    
    getIsSelfRegistrationEnabled : function (component, event, helpler) {
        var action = component.get("c.getIsSelfRegistrationEnabled");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.isSelfRegistrationEnabled',rtnValue);
            }
        });
        $A.enqueueAction(action);
    },
    
    getCommunityForgotPasswordUrl : function (component, event, helpler) {
        var action = component.get("c.getForgotPasswordUrl");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.communityForgotPasswordUrl',rtnValue);
            }
        });
        $A.enqueueAction(action);
    },
    
    getCommunitySelfRegisterUrl : function (component, event, helpler) {
        var action = component.get("c.getSelfRegistrationUrl");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.communitySelfRegisterUrl',rtnValue);
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
### loginForm

```
<design:component label="Custom Login Form">
    <design:attribute name="startUrl"/>
    <design:attribute name="usernameLabel" default="Email"/>
    <design:attribute name="passwordLabel" default="Password"/>
    <design:attribute name="loginButtonLabel" default="Log in"/>
    <design:attribute name="forgotPasswordLabel" default="Forgot your password?"/>
    <design:attribute name="forgotPasswordUrl"/>
    <design:attribute name="selfRegisterLabel" default="Not a member?"/>
    <design:attribute name="selfRegisterUrl"/>
</design:component>
```
### loginForm

```
.THIS #sfdc_username_container{
    margin-bottom:10px;
    background-color:white;
}

.THIS .input{
    border-top: 0;
    border-left: 0;
    border-right: 0;
}

.THIS #sfdc_user{
    float:left;
    width:23px;
    height:25px;
    padding-top:1px;
    padding-left:2px;
    margin:0px;

}

.THIS #sfdc_lock{
    float:left;
    width:23px;
    height:25px;
    padding-top:1px;
    padding-left:2px;
    margin:0px;
}

.THIS  #error {
    text-align: center;
    color:#FF0000;
}

.THIS  .login-icon {
    color:#ccc;font-size:22px;
}

.THIS #sfdc_password_container{
    background-color:white;
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
    font-weight: 600;
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

.THIS button .label {
    color: #fff;	
}

.THIS  input {
    margin-left:10px;
    margin-top: 3px;
    border: 0px solid transparent;
    width: 70%;
    -webkit-appearance: none;
    font-size: 14px;
}

.THIS .header{
    font-size: 1.25em;
    color: #606060;
    margin-bottom: 1em;
    text-align: center;
    display: block;
    margin-bottom: 1em;
}
.THIS  a {
    color:black;
    text-decoration: none;
    padding-left:150px;
}
.THIS  a:hover {
    color:black;
    text-decoration: none;
}

.THIS label.uiLabel-hidden {
    display:none;
}
```
### loginFormController

```
({
    initialize: function(component, event, helper) {
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap}).fire();    
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap2}).fire();
        component.set('v.isUsernamePasswordEnabled', helper.getIsUsernamePasswordEnabled(component, event, helper));
        component.set("v.isSelfRegistrationEnabled", helper.getIsSelfRegistrationEnabled(component, event, helper));
        component.set("v.communityForgotPasswordUrl", helper.getCommunityForgotPasswordUrl(component, event, helper));
        component.set("v.communitySelfRegisterUrl", helper.getCommunitySelfRegisterUrl(component, event, helper));
    	helper.handleNavigation(component,event,helper);
        
    },
    
    handleLogin: function (component, event, helpler) {
        helpler.handleLogin(component, event, helpler);
    },
    
    setStartUrl: function (component, event, helpler) {
        var startUrl = event.getParam('startURL');
        if(startUrl) {
            component.set("v.startUrl", startUrl);
        }
    },
    
    setExpId: function (component, event, helper) {
        var expId = event.getParam('expid');
        if (expId) {
            component.set("v.expid", expId);
        }
        helper.setBrandingCookie(component, event, helper);
    },
    
    onKeyUp: function(component, event, helpler){
        //checks for "enter" key
        if (event.getParam('keyCode')===13) {
            helpler.handleLogin(component, event, helpler);
        }
    },
    
    navigateToForgotPassword: function(cmp, event, helper) {
        var forgotPwdUrl = cmp.get("v.communityForgotPasswordUrl");
        if ($A.util.isUndefinedOrNull(forgotPwdUrl)) {
            forgotPwdUrl = cmp.get("v.forgotPasswordUrl");
        }
        var startUrl = cmp.get("v.startUrl");
        if(startUrl){
            if(forgotPwdUrl.indexOf("?") === -1) {
                forgotPwdUrl = forgotPwdUrl + '?startURL=' + decodeURIComponent(startUrl);
            } else {
                forgotPwdUrl = forgotPwdUrl + '&startURL=' + decodeURIComponent(startUrl);
            }
        }
        var attributes = { url: forgotPwdUrl };
        $A.get("e.force:navigateToURL").setParams(attributes).fire();
    },
    
    navigateToSelfRegister: function(cmp, event, helper) {
        var selfRegUrl = cmp.get("v.communitySelfRegisterUrl");
        if (selfRegUrl == null) {
            selfRegUrl = cmp.get("v.selfRegisterUrl");
        }
        var startUrl = cmp.get("v.startUrl");
        if(startUrl){
            if(selfRegUrl.indexOf("?") === -1) {
                selfRegUrl = selfRegUrl + '?startURL=' + decodeURIComponent(startUrl);
            } else {
                selfRegUrl = selfRegUrl + '&startURL=' + decodeURIComponent(startUrl);
            }
        }
        var attributes = { url: selfRegUrl };
        $A.get("e.force:navigateToURL").setParams(attributes).fire();
    } 
})
```
### loginForm

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>46.0</apiVersion>
    <description>Sample Component for loginForm</description>
</AuraDefinitionBundle>
```
### loginForm

```
<!-- add implements="forceCommunity:availableForAllPageTypes" to surface the component in community builder -->
<aura:component implements="forceCommunity:availableForAllPageTypes" controller="LightningLoginFormController">
    <aura:attribute name="showError" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="errorMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="startUrl" type="String" required="false" description="The url you go to after a successful login" />
    <aura:attribute name="usernameLabel" type="String" required="false" default="Username"/>
    <aura:attribute name="passwordLabel" type="String" required="false" default="Password"/>
    <aura:attribute name="loginButtonLabel" type="String" required="false" default="Log in1"/>
    <aura:attribute name="expid" type="String" required="false" description="The branding experience ID" /> 
    
    <aura:attribute name="showForm" type="Boolean" default="false"/>
    
    <aura:attribute name="forgotPasswordLabel" type="String" required="false" default="Forgot your password?"/>
    <aura:attribute name="selfRegisterLabel" type="String" required="false" default="Not a member?"/>
    <aura:attribute name="forgotPasswordUrl" type="String" required="false" default="/ForgotPassword"/>
    <aura:attribute name="selfRegisterUrl" type="String" required="false" default="/s/SelfRegister"/>
    
    <aura:attribute name="isUsernamePasswordEnabled" type="Boolean" access="private"/>
    <aura:attribute name="isSelfRegistrationEnabled" type="Boolean" access="private"/>
    <aura:attribute name="communityForgotPasswordUrl" type="String" access="private"/>
    <aura:attribute name="communitySelfRegisterUrl" type="String" access="private" default="/s/SelfRegister"/>
    
    <aura:registerevent name="sitePropagatedStartUrl" type="c:setStartUrl"/>
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:dependency resource="c:setStartUrl" type="EVENT"/>
    <!-- Please uncomment
    <aura:dependency resource="siteforce:registerQueryEventMap" type="EVENT"/>
    -->
    <aura:handler event="c:setStartUrl" action="{!c.setStartUrl}"/>
    <aura:handler event="c:setExpId" action="{!c.setExpId}"/>    
    <aura:dependency resource="c:setExpId" type="EVENT"/>  
    <aura:if isTrue="{!v.showForm}">
    	<div>
        <aura:renderIf isTrue="{!v.isUsernamePasswordEnabled}">
            <span>
                <aura:renderIf isTrue="{!v.showError}">
                    <div id="error">
                        <ui:outputRichText value="{!v.errorMessage}"/>
                    </div>
                </aura:renderIf>
            </span>      
            <span class="header">Log in to access your account</span>
            <div id="sfdc_username_container" class="sfdc">
                <ui:inputText value="" aura:id="username" placeholder="{!v.usernameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc" label="{!v.usernameLabel}" labelClass="assistiveText"/>
            </div>
    
            <div id="sfdc_password_container" class="sfdc">
                <ui:inputSecret value="" aura:id="password" placeholder="{!v.passwordLabel}" keyup="{!c.onKeyUp}" class="input sfdc_passwordinput sfdc" label="{!v.passwordLabel}" labelClass="assistiveText"/>
            </div>
    
            <div class="sfdc">
                <ui:button aura:id="submitButton" label="{!v.loginButtonLabel}" press="{!c.handleLogin}" class="sfdc_button"/>
            </div>
            
            <div id="sfdc_forgot" class="sfdc">
                <br/>
                <span><a href="{!if(v.communityForgotPasswordUrl == null, v.forgotPasswordUrl, v.communityForgotPasswordUrl)}">{!v.forgotPasswordLabel}</a></span><br/>
               <!-- <aura:renderIf isTrue="{!v.isSelfRegistrationEnabled}">
                    <span style="float:middle" ><a href="{!if(v.communitySelfRegisterUrl == null, v.selfRegisterUrl, v.communitySelfRegisterUrl)}">{!v.selfRegisterLabel}</a></span>
                </aura:renderIf>  -->                          
            </div> 
        </aura:renderIf>
    </div>
    </aura:if>
</aura:component>
```
### loginFormHelper

```
({
    
    qsToEventMap: {
        'startURL'  : 'e.c:setStartUrl'
    },

    qsToEventMap2: {
        'expid'  : 'e.c:setExpId'
    },
    
    handleNavigation: function(component,event,helper){
        var params = {};
        var parser = document.createElement('a');
        parser.href = decodeURIComponent(window.location.href);
        console.log('parser.href'+parser.href);
        var query = parser.search.substring(1);
        var vars = query.split('&');
        for (var i = 0; i < vars.length; i++) {
            var pair = vars[i].split('=');
            params[pair[0]] = decodeURIComponent(pair[1]);
        }
        console.log('params'+JSON.stringify(params));
        if((params['userId']==null || params['userId']=='') && params['record']!=null){
            //alert('Seems like you are already registered !!');
            window.location.href = window.location.href.replace('/s/login','/s/login/SelfRegister');
        }else{
            component.set('v.showForm',true);
        }
    },
    
    handleLogin: function (component, event, helpler) {
        var username = component.find("username").get("v.value");
        var password = component.find("password").get("v.value");
        var action = component.get("c.login");
        var startUrl = component.get("v.startUrl");
        
        startUrl = decodeURIComponent(startUrl);
        
        action.setParams({username:username, password:password, startUrl:startUrl});
        action.setCallback(this, function(a){
            var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set("v.errorMessage",rtnValue);
                component.set("v.showError",true);
            }
        });
        $A.enqueueAction(action);
    },
    
    getIsUsernamePasswordEnabled : function (component, event, helpler) {
        var action = component.get("c.getIsUsernamePasswordEnabled");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.isUsernamePasswordEnabled',rtnValue);
            }
        });
        $A.enqueueAction(action);
    },
    
    getIsSelfRegistrationEnabled : function (component, event, helpler) {
        var action = component.get("c.getIsSelfRegistrationEnabled");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.isSelfRegistrationEnabled',rtnValue);
            }
        });
        $A.enqueueAction(action);
    },
    
    getCommunityForgotPasswordUrl : function (component, event, helpler) {
        var action = component.get("c.getForgotPasswordUrl");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.communityForgotPasswordUrl',rtnValue);
            }
        });
        $A.enqueueAction(action);
    },
    
    getCommunitySelfRegisterUrl : function (component, event, helpler) {
        var action = component.get("c.getSelfRegistrationUrl");
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.communitySelfRegisterUrl',rtnValue);
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
### loginForm

```
<design:component label="Custom Login Form">
    <design:attribute name="startUrl"/>
    <design:attribute name="usernameLabel" default="Email"/>
    <design:attribute name="passwordLabel" default="Password"/>
    <design:attribute name="loginButtonLabel" default="Log in"/>
    <design:attribute name="forgotPasswordLabel" default="Forgot your password?"/>
    <design:attribute name="forgotPasswordUrl"/>
    <design:attribute name="selfRegisterLabel" default="Not a member?"/>
    <design:attribute name="selfRegisterUrl"/>
</design:component>
```
### loginForm

```
.THIS #sfdc_username_container{
    margin-bottom:10px;
    background-color:white;
}

.THIS .input{
    border-top: 0;
    border-left: 0;
    border-right: 0;
}

.THIS #sfdc_user{
    float:left;
    width:23px;
    height:25px;
    padding-top:1px;
    padding-left:2px;
    margin:0px;

}

.THIS #sfdc_lock{
    float:left;
    width:23px;
    height:25px;
    padding-top:1px;
    padding-left:2px;
    margin:0px;
}

.THIS  #error {
    text-align: center;
    color:#FF0000;
}

.THIS  .login-icon {
    color:#ccc;font-size:22px;
}

.THIS #sfdc_password_container{
    background-color:white;
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
    font-weight: 600;
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

.THIS button .label {
    color: #fff;	
}

.THIS  input {
    margin-left:10px;
    margin-top: 3px;
    border: 0px solid transparent;
    width: 70%;
    -webkit-appearance: none;
    font-size: 14px;
}

.THIS .header{
    font-size: 1.25em;
    color: #606060;
    margin-bottom: 1em;
    text-align: center;
    display: block;
    margin-bottom: 1em;
}
.THIS  a {
    color:black;
    text-decoration: none;
    padding-left:150px;
}
.THIS  a:hover {
    color:black;
    text-decoration: none;
}

.THIS label.uiLabel-hidden {
    display:none;
}
```
### loginFormController

```
({
    initialize: function(component, event, helper) {
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap}).fire();    
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap2}).fire();
        component.set('v.isUsernamePasswordEnabled', helper.getIsUsernamePasswordEnabled(component, event, helper));
        component.set("v.isSelfRegistrationEnabled", helper.getIsSelfRegistrationEnabled(component, event, helper));
        component.set("v.communityForgotPasswordUrl", helper.getCommunityForgotPasswordUrl(component, event, helper));
        component.set("v.communitySelfRegisterUrl", helper.getCommunitySelfRegisterUrl(component, event, helper));
    	helper.handleNavigation(component,event,helper);
        
    },
    
    handleLogin: function (component, event, helpler) {
        helpler.handleLogin(component, event, helpler);
    },
    
    setStartUrl: function (component, event, helpler) {
        var startUrl = event.getParam('startURL');
        if(startUrl) {
            component.set("v.startUrl", startUrl);
        }
    },
    
    setExpId: function (component, event, helper) {
        var expId = event.getParam('expid');
        if (expId) {
            component.set("v.expid", expId);
        }
        helper.setBrandingCookie(component, event, helper);
    },
    
    onKeyUp: function(component, event, helpler){
        //checks for "enter" key
        if (event.getParam('keyCode')===13) {
            helpler.handleLogin(component, event, helpler);
        }
    },
    
    navigateToForgotPassword: function(cmp, event, helper) {
        var forgotPwdUrl = cmp.get("v.communityForgotPasswordUrl");
        if ($A.util.isUndefinedOrNull(forgotPwdUrl)) {
            forgotPwdUrl = cmp.get("v.forgotPasswordUrl");
        }
        var startUrl = cmp.get("v.startUrl");
        if(startUrl){
            if(forgotPwdUrl.indexOf("?") === -1) {
                forgotPwdUrl = forgotPwdUrl + '?startURL=' + decodeURIComponent(startUrl);
            } else {
                forgotPwdUrl = forgotPwdUrl + '&startURL=' + decodeURIComponent(startUrl);
            }
        }
        var attributes = { url: forgotPwdUrl };
        $A.get("e.force:navigateToURL").setParams(attributes).fire();
    },
    
    navigateToSelfRegister: function(cmp, event, helper) {
        var selfRegUrl = cmp.get("v.communitySelfRegisterUrl");
        if (selfRegUrl == null) {
            selfRegUrl = cmp.get("v.selfRegisterUrl");
        }
        var startUrl = cmp.get("v.startUrl");
        if(startUrl){
            if(selfRegUrl.indexOf("?") === -1) {
                selfRegUrl = selfRegUrl + '?startURL=' + decodeURIComponent(startUrl);
            } else {
                selfRegUrl = selfRegUrl + '&startURL=' + decodeURIComponent(startUrl);
            }
        }
        var attributes = { url: selfRegUrl };
        $A.get("e.force:navigateToURL").setParams(attributes).fire();
    } 
})
```

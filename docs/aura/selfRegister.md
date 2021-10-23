---
layout: default
title: selfRegister
parent: aura
---
# Metadata Type
CustomObject

# Name
selfRegister
## Fields
### selfRegister

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>46.0</apiVersion>
    <description>Sample Component for selfRegister</description>
</AuraDefinitionBundle>
```
### selfRegisterController

```
({
    initialize: function(component, event, helper) {
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap}).fire();
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap2}).fire();        
        component.set('v.extraFields', helper.getExtraFields(component, event, helper));
        var params = {};
        var parser = document.createElement('a');
        parser.href = decodeURIComponent(window.location.href);
        var query = parser.search.substring(1);
        var vars = query.split('&');
        console.log('vars >>'+JSON.stringify(vars));
        for (var i = 0; i < vars.length; i++) {
            var pair = vars[i].split('=');
            console.log('pair >>'+JSON.stringify(pair));
            console.log('pair[0] >>'+JSON.stringify(pair[0]));
            console.log('pair[1] >>'+JSON.stringify(pair[1]));
            var pairValue = decodeURIComponent(pair[1]);
            if(pairValue.includes('contactId')){
                params['contactId'] = decodeURIComponent(pair[2]);
            }else{
                params[pair[0]] = decodeURIComponent(pair[1]);
            }
            
        }
        console.log('params >>'+JSON.stringify(params));
        console.log('contactId >>'+JSON.stringify(params['contactId']));
        component.set('v.recordId',params['record']);
        var action = component.get("c.getUserId");
        action.setParams({ recordId : params['contactId'] });
        action.setCallback(this, function(response) { 
            var state = response.getState();
            if (state === "SUCCESS") 
            {
                console.log('response val'+response.getReturnValue());
                component.find("firstname").set("v.value",response.getReturnValue()[0].FirstName);
                component.find("lastname").set("v.value",response.getReturnValue()[0].LastName);
                component.find("email").set("v.value",response.getReturnValue()[0].Email);
                component.set("v.contactId", response.getReturnValue()[0].Id);
                component.set("v.accountId", response.getReturnValue()[0].AccountId);
                
            }
        });
        $A.enqueueAction(action);

    },
    
    handleSelfRegister: function (component, event, helpler) {
        helpler.handleSelfRegister(component, event, helpler);
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
            helpler.handleSelfRegister(component, event, helpler);
        }
    },
    closeModel : function(component, event, helpler){
        component.set("v.showError",false);
        component.set("v.showSuccess",false);
    }
})
```
### selfRegister

```
<!-- add implements="forceCommunity:availableForAllPageTypes" to surface the component in community builder -->
<aura:component implements="forceCommunity:availableForAllPageTypes" controller="LightningSelfRegisterController" access="global">
    <aura:attribute name="accountId" type="String" required="false" description="accountId for creating the user. If not specified, it will create a PersonAccount if possible for B2C scenario. Or otherwise if it's in a community, the community's self-registration accountId will be used."/>
    <aura:attribute name="regConfirmUrl" type="String" required="true"/>
    <aura:attribute name="showForm" type="Boolean" default="false"/>
    <aura:attribute name="startUrl" type="String" required="false" description="The url you go to after a successful login" />
    <aura:attribute name="showError" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="errorMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="showSuccess" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="successMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="firstnameLabel" type="String" required="false" default="First Name1"/>
    <aura:attribute name="lastnameLabel" type="String" required="false" default="Last Name"/>
    <aura:attribute name="emailLabel" type="String" required="false" default="Email"/>
    <aura:attribute name="passwordLabel" type="String" required="false" default="Create Password"/>
    <aura:attribute name="confirmPasswordLabel" type="String" required="false" default="Confirm Password"/>    
    <aura:attribute name="submitButtonLabel" type="String" required="false" default="Sign Up1"/>
    <aura:attribute name="includePasswordField" type="Boolean" required="false" default="true" description="Whether to include password"/>    
    <aura:attribute name="extraFieldsFieldSet" type="String" required="false" description="A field set name whose fields are desired for user registration"/>
    <aura:attribute name="extraFields" type="list" required="false" description="A field set name whose fields are desired for user registration"/>
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:attribute name="expid" type="String" required="false" description="The branding experience ID" />    
    <aura:attribute name="recordId" type="string"/>
    <aura:attribute name="contactId" type="string"/>
    <aura:registerevent name="sitePropagatedStartUrl" type="c:setStartUrl"/>
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:dependency resource="c:setStartUrl" type="EVENT"/>
    <!-- Please uncomment
    <aura:dependency resource="siteforce:registerQueryEventMap" type="EVENT"/>
    -->
    <aura:handler event="c:setStartUrl" action="{!c.setStartUrl}"/> 
    <aura:handler event="c:setExpId" action="{!c.setExpId}"/>    
    <aura:dependency resource="c:setExpId" type="EVENT"/>   
        <div>
                	
            <aura:renderIf isTrue="{!v.showError}">
                <div aura:id="toastModel" style="height: 4rem; margin-bottom: 30px;">
                    <div class="slds-notify_container slds-is-relative">
                        <div class="slds-notify slds-notify_toast slds-theme_error" role="status">
                            <span class="slds-assistive-text">Succes</span>
                            <span class="slds-icon_container slds-icon-utility-error slds-icon-utility-error slds-m-right_small slds-no-flex slds-align-top" title="{!v.errorMessage}">
                                <lightning:icon iconName="utility:error" size="small" variant="inverse" styleclass="slds-icon slds-icon_small"/>
                            </span>
                            <div class="slds-notify__content">
                                <h2 class="slds-text-heading_small ">{!v.errorMessage}</h2>
                            </div>
                            <div class="slds-notify__close">
                                <span class="slds-button_icon slds-button_icon-inverse" title="Close" onclick="{!c.closeModel}">
                                    <lightning:icon iconName="utility:close" size="small" variant="inverse"/>
                                    <span class="slds-assistive-text">Close</span>
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </aura:renderIf>
            <aura:renderIf isTrue="{!v.showSuccess}">
                <div aura:id="toastModel" style="height: 4rem; margin-bottom: 30px;">
                    <div class="slds-notify_container slds-is-relative">
                        <div class="slds-notify slds-notify_toast slds-theme_success" role="status">
                            <span class="slds-assistive-text">Succes</span>
                            <span class="slds-icon_container slds-icon-utility-success slds-icon-utility-success slds-m-right_small slds-no-flex slds-align-top" title="{!v.successMessage}">
                                <lightning:icon iconName="utility:success" size="small" variant="inverse" styleclass="slds-icon slds-icon_small"/>
                            </span>
                            <div class="slds-notify__content">
                                <h2 class="slds-text-heading_small ">{!v.successMessage}</h2>
                            </div>
                            <div class="slds-notify__close">
                                <span class="slds-button_icon slds-button_icon-inverse" title="Close" onclick="{!c.closeModel}">
                                    <lightning:icon iconName="utility:close" size="small" variant="inverse"/>
                                    <span class="slds-assistive-text">Close</span>
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
                </aura:renderIf>
                <div id="sfdc_username_container" class="sfdc">
                    <ui:inputText value="" aura:id="firstname" placeholder="{!v.firstnameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
                </div>
    
                <div id="sfdc_nickname_container" class="sfdc">
                    <ui:inputText disabled="true" value="" aura:id="lastname" placeholder="{!v.lastnameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
                </div>
    
                <div id="sfdc_email_container" class="sfdc">
                    <ui:inputText disabled="true" value="" aura:id="email" placeholder="{!v.emailLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
                </div>
                
                <aura:iteration aura:id="extraFields" items="{!v.extraFields}" var="curField" indexVar="index">
                    <div id="sfdc_extrafield_container" class="sfdc">
                        <ui:inputText value="{!curField.value}" aura:id="{!curField.fieldPath}" placeholder="{!curField.label}" keyup="{!c.onKeyUp}" class="input sfdc_extrafieldinput sfdc"/>
                    </div>
                </aura:iteration>
    
                <aura:renderIf isTrue="{!v.includePasswordField}">
                    <div id="sfdc_password_container" class="sfdc">
                        <ui:inputSecret value="" aura:id="password" placeholder="{!v.passwordLabel}" keyup="{!c.onKeyUp}" class="input sfdc_passwordinput sfdc"/>
                    </div>
        
                    <div id="sfdc_confirm_password_container" class="sfdc">
                        <ui:inputSecret value="" aura:id="confirmPassword" placeholder="{!v.confirmPasswordLabel}" keyup="{!c.onKeyUp}" class="input sfdc_passwordinput sfdc"/>
                    </div>
                </aura:renderIf>
                <div class="sfdc">
                    <ui:button aura:id="submitButton" label="{!v.submitButtonLabel}" press="{!c.handleSelfRegister}" class="sfdc_button"/>
                </div>
        </div>
</aura:component>
```
### selfRegister

```
<design:component label="Custom Self Register">
    <design:attribute name="startUrl"/>
    <design:attribute name="regConfirmUrl" default="./CheckPasswordResetEmail"/>
    <design:attribute name="firstnameLabel" default="First Name"/>
    <design:attribute name="lastnameLabel" default="Last Name"/>
    <design:attribute name="emailLabel" default="Email"/>
    <design:attribute name="passwordLabel" default="Create Password"/>
    <design:attribute name="confirmPasswordLabel" default="Confirm Password"/>
    <design:attribute name="submitButtonLabel" default="Sign Up"/>
    <design:attribute name="includePasswordField" default="false"/>
    <design:attribute name="extraFieldsFieldSet"/>
</design:component>
```
### selfRegister

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E"/>
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF"/>
	</g>
</svg>
```
### selfRegisterHelper

```
({
    qsToEventMap: {
        'startURL'  : 'e.c:setStartUrl'
    },
    
    qsToEventMap2: {
        'expid'  : 'e.c:setExpId'
    },
    
    handleSelfRegister: function (component, event, helpler) {
        var accountId = component.get("v.accountId");
        var contactId = component.get("v.contactId");
        var regConfirmUrl = component.get("v.regConfirmUrl");
        var firstname = component.find("firstname").get("v.value");
        var lastname = component.find("lastname").get("v.value");
        var email = component.find("email").get("v.value");
        var includePassword = component.get("v.includePasswordField");
        var password = component.find("password").get("v.value");
        var confirmPassword = component.find("confirmPassword").get("v.value");
        var action = component.get("c.selfRegister");
        var extraFields = JSON.stringify(component.get("v.extraFields"));   // somehow apex controllers refuse to deal with list of maps
        var startUrl = component.get("v.startUrl");
        var recordId = component.get('v.recordId');
        startUrl = decodeURIComponent(startUrl);
        
        action.setParams({firstname:firstname,
                          lastname:lastname,
                          email:email,
                          password:password,
                          confirmPassword:confirmPassword,
                          accountId:accountId,
                          contactId:contactId,
                          regConfirmUrl:regConfirmUrl, extraFields:extraFields, startUrl:startUrl, includePassword:includePassword,recordId:recordId});
          action.setCallback(this, function(a){
          var rtnValue = a.getReturnValue();
          if (rtnValue !== null) {
              console.log('error');
             component.set("v.errorMessage",rtnValue);
             component.set("v.showError",true);
          }else{
              console.log('success');
              component.set("v.successMessage","Sign Up is successful. Please check your email for login instructions.");
              component.set("v.showSuccess",true);
          }
       });
    $A.enqueueAction(action);
    },
    
    getExtraFields : function (component, event, helpler) {
        var action = component.get("c.getExtraFields");
        action.setParam("extraFieldsFieldSet", component.get("v.extraFieldsFieldSet"));
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.extraFields',rtnValue);
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
### selfRegister

```
.THIS #sfdc_username_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_nickname_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_email_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_extrafield_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS .sfdc_usernameinput  {
    border: 0 solid transparent;
}

.THIS .sfdc_passwordinput  {
    border: 0 solid transparent;
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

.THIS  .login-icon {
    color:#ccc;font-size:22px;
}

.THIS #sfdc_password_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_confirm_password_container{
    background-color:white;
    border-bottom: 1px solid #ccc;
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

.THIS #sfdc_forgot{
    font-family: 'Open Sans', 'sans-serif';
    font-weight:300;
    font-size: 14px;
    margin-top: 10px
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

.THIS input[type="checkbox"] {
    appearance: none;
    border: 1px solid white;
    height: 22px;
    width: 22px;
    vertical-align: middle;
}

.THIS input[type="checkbox"]:checked {
    border: 1px solid ;
}

.THIS input[type="checkbox"]:checked:after {
    display: block;
    position: relative;
    content: '';
    left: 3px;
    top: 3px;
    height: 6px;
    width: 10px;
    border-bottom: 4px solid /*#354452*/ white;
    border-left: 4px solid /*#354452*/ white;
    transform:rotate(-45deg);
}

.THIS input[type="checkbox"].disabled {
    opacity: 0.35;
}

.THIS input[type="checkbox"] + label {
    vertical-align: middle;
}
.THIS .slds-notify_toast,.THIS .slds-notify--toast {
    min-width: 100%;
    width: 100% !important;
}
```
### selfRegister

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>46.0</apiVersion>
    <description>Sample Component for selfRegister</description>
</AuraDefinitionBundle>
```
### selfRegisterController

```
({
    initialize: function(component, event, helper) {
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap}).fire();
        $A.get("e.siteforce:registerQueryEventMap").setParams({"qsToEvent" : helper.qsToEventMap2}).fire();        
        component.set('v.extraFields', helper.getExtraFields(component, event, helper));
        var params = {};
        var parser = document.createElement('a');
        parser.href = decodeURIComponent(window.location.href);
        var query = parser.search.substring(1);
        var vars = query.split('&');
        console.log('vars >>'+JSON.stringify(vars));
        for (var i = 0; i < vars.length; i++) {
            var pair = vars[i].split('=');
            console.log('pair >>'+JSON.stringify(pair));
            console.log('pair[0] >>'+JSON.stringify(pair[0]));
            console.log('pair[1] >>'+JSON.stringify(pair[1]));
            var pairValue = decodeURIComponent(pair[1]);
            if(pairValue.includes('contactId')){
                params['contactId'] = decodeURIComponent(pair[2]);
            }else{
                params[pair[0]] = decodeURIComponent(pair[1]);
            }
            
        }
        console.log('params >>'+JSON.stringify(params));
        console.log('contactId >>'+JSON.stringify(params['contactId']));
        component.set('v.recordId',params['record']);
        var action = component.get("c.getUserId");
        action.setParams({ recordId : params['contactId'] });
        action.setCallback(this, function(response) { 
            var state = response.getState();
            if (state === "SUCCESS") 
            {
                console.log('response val'+response.getReturnValue());
                component.find("firstname").set("v.value",response.getReturnValue()[0].FirstName);
                component.find("lastname").set("v.value",response.getReturnValue()[0].LastName);
                component.find("email").set("v.value",response.getReturnValue()[0].Email);
                component.set("v.contactId", response.getReturnValue()[0].Id);
                component.set("v.accountId", response.getReturnValue()[0].AccountId);
                
            }
        });
        $A.enqueueAction(action);

    },
    
    handleSelfRegister: function (component, event, helpler) {
        helpler.handleSelfRegister(component, event, helpler);
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
            helpler.handleSelfRegister(component, event, helpler);
        }
    },
    closeModel : function(component, event, helpler){
        component.set("v.showError",false);
        component.set("v.showSuccess",false);
    }
})
```
### selfRegister

```
<!-- add implements="forceCommunity:availableForAllPageTypes" to surface the component in community builder -->
<aura:component implements="forceCommunity:availableForAllPageTypes" controller="LightningSelfRegisterController" access="global">
    <aura:attribute name="accountId" type="String" required="false" description="accountId for creating the user. If not specified, it will create a PersonAccount if possible for B2C scenario. Or otherwise if it's in a community, the community's self-registration accountId will be used."/>
    <aura:attribute name="regConfirmUrl" type="String" required="true"/>
    <aura:attribute name="showForm" type="Boolean" default="false"/>
    <aura:attribute name="startUrl" type="String" required="false" description="The url you go to after a successful login" />
    <aura:attribute name="showError" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="errorMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="showSuccess" type="Boolean" required="true" description="" default="false" access="private"/>
    <aura:attribute name="successMessage" type="String" required="false" description="" access="private"/>
    <aura:attribute name="firstnameLabel" type="String" required="false" default="First Name1"/>
    <aura:attribute name="lastnameLabel" type="String" required="false" default="Last Name"/>
    <aura:attribute name="emailLabel" type="String" required="false" default="Email"/>
    <aura:attribute name="passwordLabel" type="String" required="false" default="Create Password"/>
    <aura:attribute name="confirmPasswordLabel" type="String" required="false" default="Confirm Password"/>    
    <aura:attribute name="submitButtonLabel" type="String" required="false" default="Sign Up1"/>
    <aura:attribute name="includePasswordField" type="Boolean" required="false" default="true" description="Whether to include password"/>    
    <aura:attribute name="extraFieldsFieldSet" type="String" required="false" description="A field set name whose fields are desired for user registration"/>
    <aura:attribute name="extraFields" type="list" required="false" description="A field set name whose fields are desired for user registration"/>
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:attribute name="expid" type="String" required="false" description="The branding experience ID" />    
    <aura:attribute name="recordId" type="string"/>
    <aura:attribute name="contactId" type="string"/>
    <aura:registerevent name="sitePropagatedStartUrl" type="c:setStartUrl"/>
    <aura:handler name="init" value="{!this}" action="{!c.initialize}"/>
    <aura:dependency resource="c:setStartUrl" type="EVENT"/>
    <!-- Please uncomment
    <aura:dependency resource="siteforce:registerQueryEventMap" type="EVENT"/>
    -->
    <aura:handler event="c:setStartUrl" action="{!c.setStartUrl}"/> 
    <aura:handler event="c:setExpId" action="{!c.setExpId}"/>    
    <aura:dependency resource="c:setExpId" type="EVENT"/>   
        <div>
                	
            <aura:renderIf isTrue="{!v.showError}">
                <div aura:id="toastModel" style="height: 4rem; margin-bottom: 30px;">
                    <div class="slds-notify_container slds-is-relative">
                        <div class="slds-notify slds-notify_toast slds-theme_error" role="status">
                            <span class="slds-assistive-text">Succes</span>
                            <span class="slds-icon_container slds-icon-utility-error slds-icon-utility-error slds-m-right_small slds-no-flex slds-align-top" title="{!v.errorMessage}">
                                <lightning:icon iconName="utility:error" size="small" variant="inverse" styleclass="slds-icon slds-icon_small"/>
                            </span>
                            <div class="slds-notify__content">
                                <h2 class="slds-text-heading_small ">{!v.errorMessage}</h2>
                            </div>
                            <div class="slds-notify__close">
                                <span class="slds-button_icon slds-button_icon-inverse" title="Close" onclick="{!c.closeModel}">
                                    <lightning:icon iconName="utility:close" size="small" variant="inverse"/>
                                    <span class="slds-assistive-text">Close</span>
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </aura:renderIf>
            <aura:renderIf isTrue="{!v.showSuccess}">
                <div aura:id="toastModel" style="height: 4rem; margin-bottom: 30px;">
                    <div class="slds-notify_container slds-is-relative">
                        <div class="slds-notify slds-notify_toast slds-theme_success" role="status">
                            <span class="slds-assistive-text">Succes</span>
                            <span class="slds-icon_container slds-icon-utility-success slds-icon-utility-success slds-m-right_small slds-no-flex slds-align-top" title="{!v.successMessage}">
                                <lightning:icon iconName="utility:success" size="small" variant="inverse" styleclass="slds-icon slds-icon_small"/>
                            </span>
                            <div class="slds-notify__content">
                                <h2 class="slds-text-heading_small ">{!v.successMessage}</h2>
                            </div>
                            <div class="slds-notify__close">
                                <span class="slds-button_icon slds-button_icon-inverse" title="Close" onclick="{!c.closeModel}">
                                    <lightning:icon iconName="utility:close" size="small" variant="inverse"/>
                                    <span class="slds-assistive-text">Close</span>
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
                </aura:renderIf>
                <div id="sfdc_username_container" class="sfdc">
                    <ui:inputText value="" aura:id="firstname" placeholder="{!v.firstnameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
                </div>
    
                <div id="sfdc_nickname_container" class="sfdc">
                    <ui:inputText disabled="true" value="" aura:id="lastname" placeholder="{!v.lastnameLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
                </div>
    
                <div id="sfdc_email_container" class="sfdc">
                    <ui:inputText disabled="true" value="" aura:id="email" placeholder="{!v.emailLabel}" keyup="{!c.onKeyUp}" class="input sfdc_usernameinput sfdc"/>
                </div>
                
                <aura:iteration aura:id="extraFields" items="{!v.extraFields}" var="curField" indexVar="index">
                    <div id="sfdc_extrafield_container" class="sfdc">
                        <ui:inputText value="{!curField.value}" aura:id="{!curField.fieldPath}" placeholder="{!curField.label}" keyup="{!c.onKeyUp}" class="input sfdc_extrafieldinput sfdc"/>
                    </div>
                </aura:iteration>
    
                <aura:renderIf isTrue="{!v.includePasswordField}">
                    <div id="sfdc_password_container" class="sfdc">
                        <ui:inputSecret value="" aura:id="password" placeholder="{!v.passwordLabel}" keyup="{!c.onKeyUp}" class="input sfdc_passwordinput sfdc"/>
                    </div>
        
                    <div id="sfdc_confirm_password_container" class="sfdc">
                        <ui:inputSecret value="" aura:id="confirmPassword" placeholder="{!v.confirmPasswordLabel}" keyup="{!c.onKeyUp}" class="input sfdc_passwordinput sfdc"/>
                    </div>
                </aura:renderIf>
                <div class="sfdc">
                    <ui:button aura:id="submitButton" label="{!v.submitButtonLabel}" press="{!c.handleSelfRegister}" class="sfdc_button"/>
                </div>
        </div>
</aura:component>
```
### selfRegister

```
<design:component label="Custom Self Register">
    <design:attribute name="startUrl"/>
    <design:attribute name="regConfirmUrl" default="./CheckPasswordResetEmail"/>
    <design:attribute name="firstnameLabel" default="First Name"/>
    <design:attribute name="lastnameLabel" default="Last Name"/>
    <design:attribute name="emailLabel" default="Email"/>
    <design:attribute name="passwordLabel" default="Create Password"/>
    <design:attribute name="confirmPasswordLabel" default="Confirm Password"/>
    <design:attribute name="submitButtonLabel" default="Sign Up"/>
    <design:attribute name="includePasswordField" default="false"/>
    <design:attribute name="extraFieldsFieldSet"/>
</design:component>
```
### selfRegister

```
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<svg width="120px" height="120px" viewBox="0 0 120 120" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	<g stroke="none" stroke-width="1" fill="none" fill-rule="evenodd">
		<path d="M120,108 C120,114.6 114.6,120 108,120 L12,120 C5.4,120 0,114.6 0,108 L0,12 C0,5.4 5.4,0 12,0 L108,0 C114.6,0 120,5.4 120,12 L120,108 L120,108 Z" id="Shape" fill="#2A739E"/>
		<path d="M77.7383308,20 L61.1640113,20 L44.7300055,63.2000173 L56.0543288,63.2000173 L40,99.623291 L72.7458388,54.5871812 L60.907727,54.5871812 L77.7383308,20 Z" id="Path-1" fill="#FFFFFF"/>
	</g>
</svg>
```
### selfRegisterHelper

```
({
    qsToEventMap: {
        'startURL'  : 'e.c:setStartUrl'
    },
    
    qsToEventMap2: {
        'expid'  : 'e.c:setExpId'
    },
    
    handleSelfRegister: function (component, event, helpler) {
        var accountId = component.get("v.accountId");
        var contactId = component.get("v.contactId");
        var regConfirmUrl = component.get("v.regConfirmUrl");
        var firstname = component.find("firstname").get("v.value");
        var lastname = component.find("lastname").get("v.value");
        var email = component.find("email").get("v.value");
        var includePassword = component.get("v.includePasswordField");
        var password = component.find("password").get("v.value");
        var confirmPassword = component.find("confirmPassword").get("v.value");
        var action = component.get("c.selfRegister");
        var extraFields = JSON.stringify(component.get("v.extraFields"));   // somehow apex controllers refuse to deal with list of maps
        var startUrl = component.get("v.startUrl");
        var recordId = component.get('v.recordId');
        startUrl = decodeURIComponent(startUrl);
        
        action.setParams({firstname:firstname,
                          lastname:lastname,
                          email:email,
                          password:password,
                          confirmPassword:confirmPassword,
                          accountId:accountId,
                          contactId:contactId,
                          regConfirmUrl:regConfirmUrl, extraFields:extraFields, startUrl:startUrl, includePassword:includePassword,recordId:recordId});
          action.setCallback(this, function(a){
          var rtnValue = a.getReturnValue();
          if (rtnValue !== null) {
              console.log('error');
             component.set("v.errorMessage",rtnValue);
             component.set("v.showError",true);
          }else{
              console.log('success');
              component.set("v.successMessage","Sign Up is successful. Please check your email for login instructions.");
              component.set("v.showSuccess",true);
          }
       });
    $A.enqueueAction(action);
    },
    
    getExtraFields : function (component, event, helpler) {
        var action = component.get("c.getExtraFields");
        action.setParam("extraFieldsFieldSet", component.get("v.extraFieldsFieldSet"));
        action.setCallback(this, function(a){
        var rtnValue = a.getReturnValue();
            if (rtnValue !== null) {
                component.set('v.extraFields',rtnValue);
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
### selfRegister

```
.THIS #sfdc_username_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_nickname_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_email_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_extrafield_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS .sfdc_usernameinput  {
    border: 0 solid transparent;
}

.THIS .sfdc_passwordinput  {
    border: 0 solid transparent;
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

.THIS  .login-icon {
    color:#ccc;font-size:22px;
}

.THIS #sfdc_password_container{
    margin-bottom:10px;
    border-bottom: 1px solid #ccc;
}

.THIS #sfdc_confirm_password_container{
    background-color:white;
    border-bottom: 1px solid #ccc;
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

.THIS #sfdc_forgot{
    font-family: 'Open Sans', 'sans-serif';
    font-weight:300;
    font-size: 14px;
    margin-top: 10px
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

.THIS input[type="checkbox"] {
    appearance: none;
    border: 1px solid white;
    height: 22px;
    width: 22px;
    vertical-align: middle;
}

.THIS input[type="checkbox"]:checked {
    border: 1px solid ;
}

.THIS input[type="checkbox"]:checked:after {
    display: block;
    position: relative;
    content: '';
    left: 3px;
    top: 3px;
    height: 6px;
    width: 10px;
    border-bottom: 4px solid /*#354452*/ white;
    border-left: 4px solid /*#354452*/ white;
    transform:rotate(-45deg);
}

.THIS input[type="checkbox"].disabled {
    opacity: 0.35;
}

.THIS input[type="checkbox"] + label {
    vertical-align: middle;
}
.THIS .slds-notify_toast,.THIS .slds-notify--toast {
    min-width: 100%;
    width: 100% !important;
}
```

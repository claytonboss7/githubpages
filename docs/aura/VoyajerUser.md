---
layout: default
title: VoyajerUser
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerUser
## Fields
### VoyajerUserController

```
({
	doInit : function(component, event, helper) {
        var country = component.get("v.userLogged").Contact.MailingCountry;
        var countryAndStates = component.get("v.countryAndStates");
        component.set("v.disableState",true);
        var states = [];
        for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
        if(states.length>0) {
            component.set("v.disableState",false);
            component.set("v.states",states);
        } else component.set("v.states",["--- None ---"]);
	},
    
    profileLoaded : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","contentLoaded");
        callToParent.fire();
	},
    
    handleCountryChange : function(component, event, helper) {
        var country = event.getSource().get("v.value");
        var countryAndStates = component.get("v.countryAndStates");
        component.set("v.disableState",true);
        var states = [];
        for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
        if(states.length>0) {
            component.set("v.disableState",false);
            component.set("v.states",states);
        } else component.set("v.states",["--- None ---"]);
    },
    
    profileUpdating : function(component, event, helper) {
        event.preventDefault();
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","updatingUser");
        callToParent.fire();
        var fields = event.getParam('fields');
        fields.MailingCountry = component.find("Country").get("v.value");
        var state = component.find
        fields.MailingState = '';
        if(!component.get("v.disableState")) fields.MailingState = component.find("State").get("v.value");
        component.find("profileForm").submit(fields);
	},
    
    profileUpdated : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","refreshUser");
        callToParent.fire();
	},
    
    passwordUpdate : function(component, event, helper) {
        event.preventDefault();
        var currentPassword = "";
        var newPassword = "";
        var confirmPassword = "";
        var validExpense = component.find('passwordForm').reduce(function (validSoFar, inputComponent) {
            // Displays error messages for invalid fields
            if(inputComponent.get("v.name") == "currentPassword") currentPassword = inputComponent.get("v.value");
            if(inputComponent.get("v.name") == "newPassword") newPassword = inputComponent.get("v.value");
            if(inputComponent.get("v.name") == "confirmPassword") confirmPassword = inputComponent.get("v.value");
            inputComponent.showHelpMessageIfInvalid();
            return validSoFar && inputComponent.get('v.validity').valid;
        }, true);
        // If we pass error checking, do some real work
        
        if(validExpense){
            var data = {};
            data.currentPassword = currentPassword;
            data.newPassword = newPassword;
            data.confirmPassword = confirmPassword;
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","updatePassword");
            callToParent.setParam("data",data);
            callToParent.fire();
        }
	},
    
    savePreferences : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","savePreferences");
        callToParent.fire();
	}
})
```
### VoyajerUser

```
.THIS {
}

.THIS .profilePictureContainer {
    text-align: center;
    padding-top: 1em;
}

.THIS .profilePicture {
    width: 5em;
    height: 5em;
    border: 0.25em solid #606060;
}

.THIS .profileName {
    text-align: center;
    padding: 1em 0.5em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .slds-textarea {
    height: 2.75em;
}

.THIS .slds-form-password {
    width: 40%;
    margin: 0 auto;
    min-width: 20em;
}

.THIS .slds-form-password .slds-form-element__label {
    margin-bottom: 0.5em;
    font-weight: 500;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-select_container::before {
    border-bottom: none;
}

.THIS .slds-select_container::after {
    border-top: none;
}

.THIS .slds-select_container .slds-select {
    -webkit-appearance : menuList
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .slds-dueling-list__column:last-child {
    display: none;
}

@media (max-width: 800px) {
    .THIS .profilePicture {
        width: 3.8em;
        height: 3.8em;
        border: 0.175em solid #606060;
    }
}

@media (max-width: 550px) {
    .THIS .profilePicture {
        width: 2em;
        height: 2em;
        border: 0.1em solid #606060;
    }
}
```
### VoyajerUser

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerUser

```
<aura:component>
    <aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="Boolean" name="disableState" default="true" />
    <aura:attribute type="String" name="menuSelected" default="profile" />
    <aura:attribute type="List" name="countries" default="['United States']"/>
    <aura:attribute type="List" name="states" default="['Arizona']"/>
    <aura:attribute type="List" name="lodgingPreferencesAvailable" default="[{ label: 'Oven', value: 'Oven' }]"/>
    <aura:attribute type="List" name="lodgingPreferencesSelected" default="['Oven']"/>
    <aura:attribute type="Object" name="countryAndStates" default="{'','',{}}"/>
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="mainMenu">
            <div class="profilePicName">
                <div class="profilePictureContainer">
                    <lightning:avatar src="{!v.userLogged.FullPhotoUrl}"
                                      onclick="{!c.loadUserContent}"
                                      variant="circle"
                                      initials="{!v.userLogged.Initials__c}"
                                      size="large"
                                      class="profilePicture"
                                      alternativeText="{!v.userLogged.Name}" />
                </div>
                <div class="profileName">
                    <span><b>{!v.userLogged.Name}</b></span>
                </div>
            </div>
            <lightning:verticalNavigation selectedItem="{!v.menuSelected}" class="sideBarProfile hideOnMobile">
                <lightning:verticalNavigationItem label="Profile" name="profile"  />
                <!--<lightning:verticalNavigationItem label="Password" name="password" />-->
                <lightning:verticalNavigationItem label="Logding Preferences" name="preferences" />
                <lightning:verticalNavigationItem label="Privacy" name="privacy" />
            </lightning:verticalNavigation>
            <lightning:verticalNavigation selectedItem="{!v.menuSelected}" class="sideBarProfile showOnMobile">
                <lightning:verticalNavigationItemIcon label="" name="profile" iconName="utility:user" />
                <!--<lightning:verticalNavigationItemIcon label="" name="password" iconName="utility:reset_password" />-->
                <lightning:verticalNavigationItemIcon label="" name="preferences" iconName="utility:custom_apps" />
                <lightning:verticalNavigationItemIcon label="" name="privacy" iconName="utility:note" />
            </lightning:verticalNavigation>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <aura:if isTrue="{!v.menuSelected=='profile'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Profile</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <lightning:recordEditForm aura:id="profileForm"
                                                      recordId="{!v.userLogged.ContactId}"
                                                      objectApiName="Contact"
                                                      onload="{!c.profileLoaded}"
                                                      onsubmit="{!c.profileUpdating}"
                                                      onsuccess="{!c.profileUpdated}"
                                                      density="comfy">
                                <lightning:messages />
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="FirstName">First Name</label><lightning:inputField aura:id="FirstName" fieldName="FirstName" variant="label-hidden" /></div>
                                    <div class="formField"><label for="LastName">Last Name</label><lightning:inputField aura:id="LastName" fieldName="LastName" variant="label-hidden" /></div>
                                </div>
                                <div class="formField"><label for="Title">Job Title</label><lightning:inputField aura:id="Title" fieldName="Title" variant="label-hidden" /></div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="Phone">Phone</label><lightning:inputField aura:id="Phone" fieldName="Phone" variant="label-hidden" /></div>
                                    <div class="formField"><label for="MobilePhone">Mobile</label><lightning:inputField aura:id="MobilePhone" fieldName="MobilePhone" variant="label-hidden" /></div>
                                </div>
                                <div class="formField"><label for="Email">Email</label><lightning:inputField aura:id="Email" fieldName="Email" variant="label-hidden" required="true" /></div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="Birthdate">Birthday</label><lightning:inputField aura:id="Birthdate" fieldName="Birthdate" variant="label-hidden" /></div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formField"><label for="MailingStreet">Address</label><lightning:inputField aura:id="MailingStreet" fieldName="MailingStreet" variant="label-hidden" /></div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="MailingCity">City</label><lightning:inputField aura:id="MailingCity" fieldName="MailingCity" variant="label-hidden" /></div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <lightning:select aura:id="State"
                                                              name="State"
                                                              label="{!v.countryAndStates.childFieldLabel}"
                                                              value="{!v.userLogged.Contact.MailingState}"
                                                              disabled="{!v.disableState}">
                                                <aura:iteration items="{!v.states}" var="state">
                                                    <option value="{!state}">{!state}</option>
                                                </aura:iteration>
                                            </lightning:select>
                                        </div>
                                        <div class="formField"><label for="MailingPostalCode">Zip</label><lightning:inputField aura:id="MailingPostalCode" fieldName="MailingPostalCode" variant="label-hidden" /></div>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <lightning:select aura:id="Country"
                                                          name="Country"
                                                          label="{!v.countryAndStates.parentFieldLabel}"
                                                          value="{!v.userLogged.Contact.MailingCountry}"
                                                          onchange="{!c.handleCountryChange}">
                                            <aura:iteration items="{!v.countries}" var="country">
                                                <option value="{!country}">{!country}</option>
                                            </aura:iteration>
                                        </lightning:select>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <br />
                                <div style="text-align: right;">
                                    <lightning:button aura:id="submitProfile" type="submit" variant="brand" label="Update" class="formButtonBrand" />
                                </div>
                            </lightning:recordEditForm>
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='password'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Password</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <form class="slds-form-password">
                                <lightning:input aura:id="passwordForm"
                                                 name="currentPassword"
                                                 type="password"
                                                 label="Confirm your current password"
                                                 placeholder="Current password"
                                                 minlength="8"
                                                 required="true" />
                                <br />
                                <lightning:input aura:id="passwordForm"
                                                 name="newPassword"
                                                 type="password"
                                                 label="Enter your new password"
                                                 placeholder="New password"
                                                 required="true"
                                                 pattern="^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$"
                                                 messageWhenPatternMismatch="A password must contain at least eight characters, including one alphabetic character and one number." />
                                <br />
                                <lightning:input aura:id="passwordForm"
                                                 name="confirmPassword"
                                                 type="password"
                                                 label="Confirm your new password"
                                                 placeholder="Retype new password"
                                                 required="true"/>
                                <br />
                                <div style="text-align: right;">
                                    <lightning:button aura:id="submitPassword" type="submit" variant="brand" label="Change Password" class="formButtonBrand" onclick="{!c.passwordUpdate}" />
                                </div>
                            </form>
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='preferences'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Lodging Preferences</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <lightning:dualListbox name="languages"
                                                   label= ""
                                                   sourceLabel="Preferences"
                                                   selectedLabel="Added Preferences"
                                                   options="{!v.lodgingPreferencesAvailable}"
                                                   value="{!v.lodgingPreferencesSelected}" />
                            <br />
                            <div style="text-align: right;">
                                <lightning:button aura:id="submit" onclick="{!c.savePreferences}" variant="brand" label="Save" class="formButtonBrand" />
                            </div>
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='privacy'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Privacy</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <c:VoyajerPrivacy />
                        </div>
                    </div>
                </aura:if>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerUserController

```
({
	doInit : function(component, event, helper) {
        var country = component.get("v.userLogged").Contact.MailingCountry;
        var countryAndStates = component.get("v.countryAndStates");
        component.set("v.disableState",true);
        var states = [];
        for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
        if(states.length>0) {
            component.set("v.disableState",false);
            component.set("v.states",states);
        } else component.set("v.states",["--- None ---"]);
	},
    
    profileLoaded : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","contentLoaded");
        callToParent.fire();
	},
    
    handleCountryChange : function(component, event, helper) {
        var country = event.getSource().get("v.value");
        var countryAndStates = component.get("v.countryAndStates");
        component.set("v.disableState",true);
        var states = [];
        for (var countryMap in countryAndStates.pickListMap) if(countryMap == country) states = countryAndStates.pickListMap[countryMap];
        if(states.length>0) {
            component.set("v.disableState",false);
            component.set("v.states",states);
        } else component.set("v.states",["--- None ---"]);
    },
    
    profileUpdating : function(component, event, helper) {
        event.preventDefault();
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","updatingUser");
        callToParent.fire();
        var fields = event.getParam('fields');
        fields.MailingCountry = component.find("Country").get("v.value");
        var state = component.find
        fields.MailingState = '';
        if(!component.get("v.disableState")) fields.MailingState = component.find("State").get("v.value");
        component.find("profileForm").submit(fields);
	},
    
    profileUpdated : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","refreshUser");
        callToParent.fire();
	},
    
    passwordUpdate : function(component, event, helper) {
        event.preventDefault();
        var currentPassword = "";
        var newPassword = "";
        var confirmPassword = "";
        var validExpense = component.find('passwordForm').reduce(function (validSoFar, inputComponent) {
            // Displays error messages for invalid fields
            if(inputComponent.get("v.name") == "currentPassword") currentPassword = inputComponent.get("v.value");
            if(inputComponent.get("v.name") == "newPassword") newPassword = inputComponent.get("v.value");
            if(inputComponent.get("v.name") == "confirmPassword") confirmPassword = inputComponent.get("v.value");
            inputComponent.showHelpMessageIfInvalid();
            return validSoFar && inputComponent.get('v.validity').valid;
        }, true);
        // If we pass error checking, do some real work
        
        if(validExpense){
            var data = {};
            data.currentPassword = currentPassword;
            data.newPassword = newPassword;
            data.confirmPassword = confirmPassword;
            var callToParent = component.getEvent("callToParent");
            callToParent.setParam("action","updatePassword");
            callToParent.setParam("data",data);
            callToParent.fire();
        }
	},
    
    savePreferences : function(component, event, helper) {
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","savePreferences");
        callToParent.fire();
	}
})
```
### VoyajerUser

```
.THIS {
}

.THIS .profilePictureContainer {
    text-align: center;
    padding-top: 1em;
}

.THIS .profilePicture {
    width: 5em;
    height: 5em;
    border: 0.25em solid #606060;
}

.THIS .profileName {
    text-align: center;
    padding: 1em 0.5em;
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
}

.THIS .slds-textarea {
    height: 2.75em;
}

.THIS .slds-form-password {
    width: 40%;
    margin: 0 auto;
    min-width: 20em;
}

.THIS .slds-form-password .slds-form-element__label {
    margin-bottom: 0.5em;
    font-weight: 500;
}

.THIS .slds-dueling-list {
    justify-content: center;
}

.THIS .slds-select_container::before {
    border-bottom: none;
}

.THIS .slds-select_container::after {
    border-top: none;
}

.THIS .slds-select_container .slds-select {
    -webkit-appearance : menuList
}

.THIS .slds-dueling-list__column {
    justify-content: center;
}

.THIS .slds-dueling-list__column_responsive {
    flex: 1;
}

.THIS .slds-dueling-list__column:last-child {
    display: none;
}

@media (max-width: 800px) {
    .THIS .profilePicture {
        width: 3.8em;
        height: 3.8em;
        border: 0.175em solid #606060;
    }
}

@media (max-width: 550px) {
    .THIS .profilePicture {
        width: 2em;
        height: 2em;
        border: 0.1em solid #606060;
    }
}
```
### VoyajerUser

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerUser

```
<aura:component>
    <aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    <aura:attribute type="Boolean" name="disableState" default="true" />
    <aura:attribute type="String" name="menuSelected" default="profile" />
    <aura:attribute type="List" name="countries" default="['United States']"/>
    <aura:attribute type="List" name="states" default="['Arizona']"/>
    <aura:attribute type="List" name="lodgingPreferencesAvailable" default="[{ label: 'Oven', value: 'Oven' }]"/>
    <aura:attribute type="List" name="lodgingPreferencesSelected" default="['Oven']"/>
    <aura:attribute type="Object" name="countryAndStates" default="{'','',{}}"/>
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}"/>
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
	<div>
        <div class="mainMenu">
            <div class="profilePicName">
                <div class="profilePictureContainer">
                    <lightning:avatar src="{!v.userLogged.FullPhotoUrl}"
                                      onclick="{!c.loadUserContent}"
                                      variant="circle"
                                      initials="{!v.userLogged.Initials__c}"
                                      size="large"
                                      class="profilePicture"
                                      alternativeText="{!v.userLogged.Name}" />
                </div>
                <div class="profileName">
                    <span><b>{!v.userLogged.Name}</b></span>
                </div>
            </div>
            <lightning:verticalNavigation selectedItem="{!v.menuSelected}" class="sideBarProfile hideOnMobile">
                <lightning:verticalNavigationItem label="Profile" name="profile"  />
                <!--<lightning:verticalNavigationItem label="Password" name="password" />-->
                <lightning:verticalNavigationItem label="Logding Preferences" name="preferences" />
                <lightning:verticalNavigationItem label="Privacy" name="privacy" />
            </lightning:verticalNavigation>
            <lightning:verticalNavigation selectedItem="{!v.menuSelected}" class="sideBarProfile showOnMobile">
                <lightning:verticalNavigationItemIcon label="" name="profile" iconName="utility:user" />
                <!--<lightning:verticalNavigationItemIcon label="" name="password" iconName="utility:reset_password" />-->
                <lightning:verticalNavigationItemIcon label="" name="preferences" iconName="utility:custom_apps" />
                <lightning:verticalNavigationItemIcon label="" name="privacy" iconName="utility:note" />
            </lightning:verticalNavigation>
        </div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <aura:if isTrue="{!v.menuSelected=='profile'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Profile</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <lightning:recordEditForm aura:id="profileForm"
                                                      recordId="{!v.userLogged.ContactId}"
                                                      objectApiName="Contact"
                                                      onload="{!c.profileLoaded}"
                                                      onsubmit="{!c.profileUpdating}"
                                                      onsuccess="{!c.profileUpdated}"
                                                      density="comfy">
                                <lightning:messages />
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="FirstName">First Name</label><lightning:inputField aura:id="FirstName" fieldName="FirstName" variant="label-hidden" /></div>
                                    <div class="formField"><label for="LastName">Last Name</label><lightning:inputField aura:id="LastName" fieldName="LastName" variant="label-hidden" /></div>
                                </div>
                                <div class="formField"><label for="Title">Job Title</label><lightning:inputField aura:id="Title" fieldName="Title" variant="label-hidden" /></div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="Phone">Phone</label><lightning:inputField aura:id="Phone" fieldName="Phone" variant="label-hidden" /></div>
                                    <div class="formField"><label for="MobilePhone">Mobile</label><lightning:inputField aura:id="MobilePhone" fieldName="MobilePhone" variant="label-hidden" /></div>
                                </div>
                                <div class="formField"><label for="Email">Email</label><lightning:inputField aura:id="Email" fieldName="Email" variant="label-hidden" required="true" /></div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="Birthdate">Birthday</label><lightning:inputField aura:id="Birthdate" fieldName="Birthdate" variant="label-hidden" /></div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <div class="formField"><label for="MailingStreet">Address</label><lightning:inputField aura:id="MailingStreet" fieldName="MailingStreet" variant="label-hidden" /></div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField"><label for="MailingCity">City</label><lightning:inputField aura:id="MailingCity" fieldName="MailingCity" variant="label-hidden" /></div>
                                    <div class="formColumnTwoChilds">
                                        <div class="formField">
                                            <lightning:select aura:id="State"
                                                              name="State"
                                                              label="{!v.countryAndStates.childFieldLabel}"
                                                              value="{!v.userLogged.Contact.MailingState}"
                                                              disabled="{!v.disableState}">
                                                <aura:iteration items="{!v.states}" var="state">
                                                    <option value="{!state}">{!state}</option>
                                                </aura:iteration>
                                            </lightning:select>
                                        </div>
                                        <div class="formField"><label for="MailingPostalCode">Zip</label><lightning:inputField aura:id="MailingPostalCode" fieldName="MailingPostalCode" variant="label-hidden" /></div>
                                    </div>
                                </div>
                                <div class="formColumnTwoChilds">
                                    <div class="formField">
                                        <lightning:select aura:id="Country"
                                                          name="Country"
                                                          label="{!v.countryAndStates.parentFieldLabel}"
                                                          value="{!v.userLogged.Contact.MailingCountry}"
                                                          onchange="{!c.handleCountryChange}">
                                            <aura:iteration items="{!v.countries}" var="country">
                                                <option value="{!country}">{!country}</option>
                                            </aura:iteration>
                                        </lightning:select>
                                    </div>
                                    <div class="formColumnBlank"></div>
                                </div>
                                <br />
                                <div style="text-align: right;">
                                    <lightning:button aura:id="submitProfile" type="submit" variant="brand" label="Update" class="formButtonBrand" />
                                </div>
                            </lightning:recordEditForm>
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='password'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Password</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <form class="slds-form-password">
                                <lightning:input aura:id="passwordForm"
                                                 name="currentPassword"
                                                 type="password"
                                                 label="Confirm your current password"
                                                 placeholder="Current password"
                                                 minlength="8"
                                                 required="true" />
                                <br />
                                <lightning:input aura:id="passwordForm"
                                                 name="newPassword"
                                                 type="password"
                                                 label="Enter your new password"
                                                 placeholder="New password"
                                                 required="true"
                                                 pattern="^(?=.*[A-Za-z])(?=.*\d)[A-Za-z\d]{8,}$"
                                                 messageWhenPatternMismatch="A password must contain at least eight characters, including one alphabetic character and one number." />
                                <br />
                                <lightning:input aura:id="passwordForm"
                                                 name="confirmPassword"
                                                 type="password"
                                                 label="Confirm your new password"
                                                 placeholder="Retype new password"
                                                 required="true"/>
                                <br />
                                <div style="text-align: right;">
                                    <lightning:button aura:id="submitPassword" type="submit" variant="brand" label="Change Password" class="formButtonBrand" onclick="{!c.passwordUpdate}" />
                                </div>
                            </form>
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='preferences'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Lodging Preferences</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <lightning:dualListbox name="languages"
                                                   label= ""
                                                   sourceLabel="Preferences"
                                                   selectedLabel="Added Preferences"
                                                   options="{!v.lodgingPreferencesAvailable}"
                                                   value="{!v.lodgingPreferencesSelected}" />
                            <br />
                            <div style="text-align: right;">
                                <lightning:button aura:id="submit" onclick="{!c.savePreferences}" variant="brand" label="Save" class="formButtonBrand" />
                            </div>
                        </div>
                    </div>
                </aura:if>
                <aura:if isTrue="{!v.menuSelected=='privacy'}">
                    <div class="page-section">
                        <div class="page-header"><h1>Privacy</h1></div>
                    </div>
                    <div class="pageContentForm">
                        <div class="page-section">
                            <c:VoyajerPrivacy />
                        </div>
                    </div>
                </aura:if>
            </div>
        </div>
    </div>
</aura:component>
```

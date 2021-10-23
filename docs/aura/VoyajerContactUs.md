---
layout: default
title: VoyajerContactUs
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerContactUs
## Fields
### VoyajerContactUs

```
<aura:component>
    <aura:attribute type="Object" name="contactUsData" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 style="display: flex; align-items: center;">
                            <lightning:icon iconName="utility:share_post" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Contact Us</span>
                        </h1>
                    </div>
                </div>
                <div class="pageContentForm">
                    <div class="page-section">
                        <div class="page-section-content_header">
                            <p style="font-size: 1.75rem; font-weight: 600; margin-bottom: 0;">GET IN TOUCH</p>
                            <p style="margin-top: -0.5em; text-align: center;">
                                <span>We're here whenever you need us,</span>
                                <span> 24 hours a day,</span>
                                <span> 7 days a week</span>
                            </p>
                        </div>
                        <aura:if isTrue="{!v.contactUsData.userAM != null}">
                            <div class="page-section-content_center">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><lightning:icon iconName="utility:questions_and_answers" alternativeText="Manager" /></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userAM.FirstName + ' ' + v.contactUsData.userAM.LastName}</p>
                                        <p>Account Manager</p>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.contactUsData.userAM.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userAM.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userAM.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userAM.MobilePhone}</p>
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.contactUsData.userAM.Email != null}">
                                        	<p><a href="{!'mailto:' + v.contactUsData.userAM.Email}">{!v.contactUsData.userAM.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                		</aura:if>
                        <div class="page-section-content_center">
                            <aura:if isTrue="{!v.contactUsData.userHC != null}">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><i class="fas fa-home fa-2x"></i></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userHC.FirstName + ' ' + v.contactUsData.userHC.LastName}</p>
                                        <p>Lodging Coordinator</p>
                                    </div>
                                    <div class="contactBoxPME">
                                        <aura:if isTrue="{!v.contactUsData.userHC.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userHC.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userHC.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userHC.MobilePhone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userHC.Email != null}">
                                        	<p><a href="{!'mailto:' + v.contactUsData.userHC.Email}">{!v.contactUsData.userHC.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                			</aura:if>
                            <aura:if isTrue="{!v.contactUsData.userAC != null}">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><i class="fas fa-plane fa-2x"></i></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userAC.FirstName + ' ' + v.contactUsData.userAC.LastName}</p>
                                        <p>Air Coordinator</p>
                                    </div>
                                    <div class="contactBoxPME">
                                        <aura:if isTrue="{!v.contactUsData.userAC.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userAC.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userAC.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userAC.MobilePhone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userAC.Email != null}">
                                        	<p><a href="{!'mailto:' + v.contactUsData.userAC.Email}">{!v.contactUsData.userAC.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                			</aura:if>
                            <aura:if isTrue="{!v.contactUsData.userGTC != null}">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><i class="fas fa-bus fa-2x"></i></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userGTC.FirstName + ' ' + v.contactUsData.userGTC.LastName}</p>
                                        <p>Ground Travel Coordinator</p>
                                    </div>
                                    <div class="contactBoxPME">
                                        <aura:if isTrue="{!v.contactUsData.userGTC.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userGTC.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userGTC.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userGTC.MobilePhone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userGTC.Email != null}">
                                            <p><a href="{!'mailto:' + v.contactUsData.userGTC.Email}">{!v.contactUsData.userGTC.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                			</aura:if>
                        </div>
                    </div>
                </div>
                <div class="page-section-footer">
                    <span>For emergency needs, please call the Ring a Rebel line at 612.642.2900</span>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerContactUs

```
.THIS .page-section-footer {
    display: flex;
    height: 5em;
    align-items: center;
    justify-content: center;
    background-color: #282828;
    color: #9f9f9f;
    text-align: center;
    box-shadow: 4px 4px 8px 0px #dbdbdb;
}

.THIS .contactBox {
    width: 20em;
    padding: 2.5em 2em 0;
    position: relative;
}

.THIS .contactBox > div {
    padding: 0.25em 0;
}

.THIS .contactBox p {
    line-height: 1.25;
    margin-bottom: 0;
    white-space: nowrap;
    overflow: hidden;
    display: inline-block;
    text-overflow: ellipsis;
    width: 100%;
}

.THIS .contactBoxName {
    text-transform: uppercase;
    font-weight: 500;
}

.THIS .contactBoxName p:first-child {
    font-weight: 600;
    font-size: 1.25em;
}

.THIS .contactBox .contactBoxIcon {
    padding-bottom: 1em;
}

.THIS .contactBoxIcon .slds-icon {
    fill: black;
}

.THIS .fa-plane {
    transform: rotate(-45deg);
}
```
### VoyajerContactUs

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerContactUs

```
<aura:component>
    <aura:attribute type="Object" name="contactUsData" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 style="display: flex; align-items: center;">
                            <lightning:icon iconName="utility:share_post" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Contact Us</span>
                        </h1>
                    </div>
                </div>
                <div class="pageContentForm">
                    <div class="page-section">
                        <div class="page-section-content_header">
                            <p style="font-size: 1.75rem; font-weight: 600; margin-bottom: 0;">GET IN TOUCH</p>
                            <p style="margin-top: -0.5em; text-align: center;">
                                <span>We're here whenever you need us,</span>
                                <span> 24 hours a day,</span>
                                <span> 7 days a week</span>
                            </p>
                        </div>
                        <aura:if isTrue="{!v.contactUsData.userAM != null}">
                            <div class="page-section-content_center">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><lightning:icon iconName="utility:questions_and_answers" alternativeText="Manager" /></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userAM.FirstName + ' ' + v.contactUsData.userAM.LastName}</p>
                                        <p>Account Manager</p>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.contactUsData.userAM.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userAM.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userAM.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userAM.MobilePhone}</p>
                                        </aura:if>
                                    </div>
                                    <div>
                                        <aura:if isTrue="{!v.contactUsData.userAM.Email != null}">
                                        	<p><a href="{!'mailto:' + v.contactUsData.userAM.Email}">{!v.contactUsData.userAM.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                            </div>
                		</aura:if>
                        <div class="page-section-content_center">
                            <aura:if isTrue="{!v.contactUsData.userHC != null}">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><i class="fas fa-home fa-2x"></i></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userHC.FirstName + ' ' + v.contactUsData.userHC.LastName}</p>
                                        <p>Lodging Coordinator</p>
                                    </div>
                                    <div class="contactBoxPME">
                                        <aura:if isTrue="{!v.contactUsData.userHC.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userHC.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userHC.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userHC.MobilePhone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userHC.Email != null}">
                                        	<p><a href="{!'mailto:' + v.contactUsData.userHC.Email}">{!v.contactUsData.userHC.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                			</aura:if>
                            <aura:if isTrue="{!v.contactUsData.userAC != null}">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><i class="fas fa-plane fa-2x"></i></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userAC.FirstName + ' ' + v.contactUsData.userAC.LastName}</p>
                                        <p>Air Coordinator</p>
                                    </div>
                                    <div class="contactBoxPME">
                                        <aura:if isTrue="{!v.contactUsData.userAC.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userAC.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userAC.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userAC.MobilePhone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userAC.Email != null}">
                                        	<p><a href="{!'mailto:' + v.contactUsData.userAC.Email}">{!v.contactUsData.userAC.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                			</aura:if>
                            <aura:if isTrue="{!v.contactUsData.userGTC != null}">
                                <div class="contactBox">
                                    <div class="contactBoxIcon"><i class="fas fa-bus fa-2x"></i></div>
                                    <div class="contactBoxName">
                                        <p>{!v.contactUsData.userGTC.FirstName + ' ' + v.contactUsData.userGTC.LastName}</p>
                                        <p>Ground Travel Coordinator</p>
                                    </div>
                                    <div class="contactBoxPME">
                                        <aura:if isTrue="{!v.contactUsData.userGTC.Phone != null}">
                                        	<p>PH: {!v.contactUsData.userGTC.Phone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userGTC.MobilePhone != null}">
                                        	<p>Mobile: {!v.contactUsData.userGTC.MobilePhone}</p>
                                        </aura:if>
                                        <aura:if isTrue="{!v.contactUsData.userGTC.Email != null}">
                                            <p><a href="{!'mailto:' + v.contactUsData.userGTC.Email}">{!v.contactUsData.userGTC.Email}</a></p>
                                        </aura:if>
                                    </div>
                                </div>
                			</aura:if>
                        </div>
                    </div>
                </div>
                <div class="page-section-footer">
                    <span>For emergency needs, please call the Ring a Rebel line at 612.642.2900</span>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerContactUs

```
.THIS .page-section-footer {
    display: flex;
    height: 5em;
    align-items: center;
    justify-content: center;
    background-color: #282828;
    color: #9f9f9f;
    text-align: center;
    box-shadow: 4px 4px 8px 0px #dbdbdb;
}

.THIS .contactBox {
    width: 20em;
    padding: 2.5em 2em 0;
    position: relative;
}

.THIS .contactBox > div {
    padding: 0.25em 0;
}

.THIS .contactBox p {
    line-height: 1.25;
    margin-bottom: 0;
    white-space: nowrap;
    overflow: hidden;
    display: inline-block;
    text-overflow: ellipsis;
    width: 100%;
}

.THIS .contactBoxName {
    text-transform: uppercase;
    font-weight: 500;
}

.THIS .contactBoxName p:first-child {
    font-weight: 600;
    font-size: 1.25em;
}

.THIS .contactBox .contactBoxIcon {
    padding-bottom: 1em;
}

.THIS .contactBoxIcon .slds-icon {
    fill: black;
}

.THIS .fa-plane {
    transform: rotate(-45deg);
}
```
### VoyajerContactUs

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```

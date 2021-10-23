---
layout: default
title: VoyajerReports
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerReports
## Fields
### VoyajerReports

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerReports

```
.THIS .reportBox {
    width: 20em;
    padding: 2.5em 2em 0;
    position: relative;
    display: flex;
    flex-direction: column;
}

.THIS .reportBox > div {
    text-align: center;
}

.THIS .reportBoxIcon {
    padding-bottom: 1em;
}

.THIS .reportBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .reportBoxName {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 1.25em;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
}

.THIS .reportBoxName p {
    line-height: 1.5;
    margin-bottom: 0.5em !important;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    max-height: 3em;
}

.THIS .reportBoxDescription p {
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    height: 6.15em;
}
```
### VoyajerReports

```
<aura:component>
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 style="display: flex; align-items: center;">
                            <lightning:icon iconName="utility:description" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Reports</span>
                        </h1>
                    </div>
                </div>
                <div class="pageContentForm">
                    <div class="page-section-content_center">
                        <div class="reportBox">
                            <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                            <div class="reportBoxName">
                                <p title="Report Name">Report Name</p>
                            </div>
                            <div class="reportBoxDescription">
                                <p>
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                                    Cras libero ante, euismod vitae magna vitae, ullamcorper vulputate diam. 
                                    Cras vel mi orci. Proin vel hendrerit leo. Mauris varius orci vel 
                                    sagittis fringilla.
                                </p>
                            </div>
                            <div style="margin-top: 0.5em;">
                                <lightning:button label="Report" variant="brand" class="formButtonBrand" />
                            </div>
                        </div>
                        <div class="reportBox">
                            <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                            <div class="reportBoxName">
                                <p title="The longest report name that you can imagine">The longest report name that you can imagine</p>
                            </div>
                            <div class="reportBoxDescription">
                                <p>
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                                    Cras libero ante, euismod vitae magna vitae, ullamcorper vulputate diam. 
                                    Cras vel mi orci. Proin vel hendrerit leo. Mauris varius orci vel 
                                    sagittis fringilla.
                                </p>
                            </div>
                            <div style="margin-top: 0.5em;">
                                <lightning:button label="Report" variant="brand" class="formButtonBrand" />
                            </div>
                        </div>
                        <div class="reportBox">
                            <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                            <div class="reportBoxName">
                                <p title="Another report name">Another report name</p>
                            </div>
                            <div class="reportBoxDescription">
                                <p>
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                                    Cras libero ante, euismod vitae magna vitae, ullamcorper vulputate diam. 
                                    Cras vel mi orci. Proin vel hendrerit leo. Mauris varius orci vel 
                                    sagittis fringilla.
                                </p>
                            </div>
                            <div style="margin-top: 0.5em;">
                                <lightning:button label="Report" variant="brand" class="formButtonBrand" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```
### VoyajerReports

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerReports

```
.THIS .reportBox {
    width: 20em;
    padding: 2.5em 2em 0;
    position: relative;
    display: flex;
    flex-direction: column;
}

.THIS .reportBox > div {
    text-align: center;
}

.THIS .reportBoxIcon {
    padding-bottom: 1em;
}

.THIS .reportBoxIcon .slds-icon {
    width: 4em;
    height: 4em;
}

.THIS .reportBoxName {
    text-transform: uppercase;
    font-weight: 600;
    font-size: 1.25em;
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
}

.THIS .reportBoxName p {
    line-height: 1.5;
    margin-bottom: 0.5em !important;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    -webkit-box-orient: vertical;
    max-height: 3em;
}

.THIS .reportBoxDescription p {
    line-height: 1.25;
    font-weight: 500;
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 5;
    -webkit-box-orient: vertical;
    height: 6.15em;
}
```
### VoyajerReports

```
<aura:component>
	<aura:attribute type="User" name="userLogged" default="{'sobjectType' : 'User'}" />
    
    <div>
        <div class="pageContent">
            <div class="pageContentSpaces">
                <div class="page-section">
                    <div class="page-header">
                        <h1 style="display: flex; align-items: center;">
                            <lightning:icon iconName="utility:description" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Reports</span>
                        </h1>
                    </div>
                </div>
                <div class="pageContentForm">
                    <div class="page-section-content_center">
                        <div class="reportBox">
                            <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                            <div class="reportBoxName">
                                <p title="Report Name">Report Name</p>
                            </div>
                            <div class="reportBoxDescription">
                                <p>
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                                    Cras libero ante, euismod vitae magna vitae, ullamcorper vulputate diam. 
                                    Cras vel mi orci. Proin vel hendrerit leo. Mauris varius orci vel 
                                    sagittis fringilla.
                                </p>
                            </div>
                            <div style="margin-top: 0.5em;">
                                <lightning:button label="Report" variant="brand" class="formButtonBrand" />
                            </div>
                        </div>
                        <div class="reportBox">
                            <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                            <div class="reportBoxName">
                                <p title="The longest report name that you can imagine">The longest report name that you can imagine</p>
                            </div>
                            <div class="reportBoxDescription">
                                <p>
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                                    Cras libero ante, euismod vitae magna vitae, ullamcorper vulputate diam. 
                                    Cras vel mi orci. Proin vel hendrerit leo. Mauris varius orci vel 
                                    sagittis fringilla.
                                </p>
                            </div>
                            <div style="margin-top: 0.5em;">
                                <lightning:button label="Report" variant="brand" class="formButtonBrand" />
                            </div>
                        </div>
                        <div class="reportBox">
                            <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                            <div class="reportBoxName">
                                <p title="Another report name">Another report name</p>
                            </div>
                            <div class="reportBoxDescription">
                                <p>
                                    Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
                                    Cras libero ante, euismod vitae magna vitae, ullamcorper vulputate diam. 
                                    Cras vel mi orci. Proin vel hendrerit leo. Mauris varius orci vel 
                                    sagittis fringilla.
                                </p>
                            </div>
                            <div style="margin-top: 0.5em;">
                                <lightning:button label="Report" variant="brand" class="formButtonBrand" />
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</aura:component>
```

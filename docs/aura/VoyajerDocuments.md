---
layout: default
title: VoyajerDocuments
parent: aura
---
# Metadata Type
CustomObject

# Name
VoyajerDocuments
## Fields
### VoyajerDocuments

```
.THIS {
}

.THIS .tableDoc {
    width: 100%;
    /*margin-bottom: 1rem;*/
    color: #212529;
    border-collapse: collapse;
}

.THIS .tableDoc thead th {
    vertical-align: bottom;
    border-bottom: 2px solid #dee2e6;
}

.THIS .tableDoc td,
.THIS .tableDoc th {
    padding: .75rem;
    vertical-align: top;
}

.THIS .tableDoc td {
    border-top: 1px solid #dee2e6;
}

.THIS .tableDoc tbody tr:hover {
	background-color: #e7f8ff;
}

.THIS .slds-button,
.THIS .slds-select_container{
    margin: 0rem 0.25rem;
}

.THIS .slds-select {
    border-radius: 3em;
	height: 35px;
    /*text-transform: uppercase;*/
}

.THIS .inputlabelcustom1 .slds-form-element__label {
    color: #000 !important;
    font-size: 14px !important;
    /*display: none;*/
}

.THIS .inputwithfilebtncustom .slds-file-selector__button {
    background-color: #0065ff;
    color: #fff;
}

.THIS .inputlabelhide .slds-form-element__label {
    display: none;
}

.THIS .text-right{
    text-align: right !important;
}

.THIS .formButtonBrandLightInverse {
    color: #00b4ff;
    border-color: #09b7ff;
}

.THIS .formButtonBrandLightInverse:hover {
    background-color: #eaf8ff;
}

.THIS .modalHeaderDocuments {
    background-color: #022066 !important;
    color: #fff !important;
    text-align: left !important;
}
```
### VoyajerDocuments

```
<aura:component>
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="userProfile" />
    
    <aura:attribute type="String" name="serviceId" />
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <aura:attribute name="startDate" type="String" />
	<aura:attribute name="endDate" type="String" />
	<aura:attribute name="selectedLookupId" type="String" />
    <aura:attribute name="selectedPillText" type="String" />
       
   	<aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="subtextinerary" />
    <aura:attribute type="String" name="cityName" />
    <aura:attribute type="String" name="dateIn" />
    <aura:attribute type="String" name="dateOut" />
    <aura:attribute type="List" name="lsDocuments" default="[]" />
    <aura:attribute type="List" name="lsDocuments_org" default="[]" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <!-- modals -->
    <aura:attribute name="isModalUploadOpen" type="boolean" default="false"/>
    <aura:attribute name="documentNameSelected" type="String" default=""/>
    <aura:attribute name="formTextInfo" type="String" default=""/>
    
    <aura:attribute name="isModalPreviewOpen" type="boolean" default="false"/>
    <aura:attribute name="selectedPreviewDocumentId" type="String" default=""/>
    
    <!-- opcs -->
    <aura:attribute type="String" name="serviceType" />
    <aura:attribute name="optionsDocumentType" type="List" />
    <aura:attribute name="optionsDocumentType_selectedValue" type="String" default=""/>
    
    <div class="pageContent">
        <div class="pageContentSpaces">
            <div class="page-section">
                <div class="page-header">
                    <div>
                        <h1 style="display: flex; align-items: center; /*font-weight: 800;*/">
                            <lightning:icon iconName="utility:description" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Documents</span>
                        </h1>
                    </div>
                    <div class="text-right" style="float:left;">
                        <lightning:button label="Back" variant="brand" class="formButtonBrand" onclick="{!c.handleBack}" />
                    </div>
                </div>
            </div>
            <div class="pageContentForm header" style="display: flex;">
                <div>
                    <div>
                        <h3 style="font-weight: 800;">{!v.productionName}</h3>
                    </div>
                    <div>
                        <!--<span style="font-weight: 600; color: #09b7ff;">{!v.cityName}</span> | <span style="font-weight: 600; color: #09b7ff;">{!v.dateIn} - {!v.dateOut}</span>-->
                        <span style="font-weight: 600; color: #09b7ff;">{!v.serviceCityName}</span> | <span style="font-weight: 600; color: #09b7ff;">{!v.serviceDateInAndOut}</span>
                        <!--{!v.serviceData.cityName} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}-->
                    </div>
                    <div>
                        <span style="font-weight: 600;">{!v.bidName}</span>
                    </div>
                </div>
			</div>
            <div class="pageContentForm" style="display: flex; border-bottom: 1px solid #dee2e6; padding: 0em 2em 2em;">
                <div class="page-section-buttons">
                    <div style="height: 2.5em;">
                        <span>Filter by</span>
                        <lightning:select  aura:id="filter_selectDocumentType" name="select1" label="Document Type" required="false" variant="label-inline" class="inputlabelhide">
                            <option value="">Document Type</option>
                            <aura:iteration items="{!v.optionsDocumentType}" var="item">
                                <option text="{!item.label}" value="{!item.value}"/>
                            </aura:iteration>
                        </lightning:select>
                        <lightning:button label="UPDATE" 
                                          name="Update" 
                                          variant="brand" 
                                          class="formButtonBrandLight" 
                                          value="Update"
                                          onclick="{!c.handleFilter}" />
                        <lightning:button label="CLEAR" 
                                          name="Clear" 
                                          variant="neutral" 
                                          class="formButtonBrandLightInverse" 
                                          value="View all"
                                          onclick="{!c.handleFilter}" />

                        <!--<lightning:buttonIcon iconName="utility:sync" variant="brand" class="formButtonBrandLight showOnMobile" onclick="{!c.doInit}" />-->
                    </div>
                </div>
            </div>
            <div class="pageContentForm" style="border-bottom: 1px solid #dee2e6; padding: 0.5em 2em;">
                <div>
                    <table class="tableDoc">
                        <thead>
                            <tr>
                                <th scope="col" width="50%">Document Name</th>
                                <th scope="col" width="">Document Type</th>
                                <th scope="col" width="">Date Uploaded</th>
                                <th scope="col" width=""></th>
                            </tr>
                        </thead>
                        <tbody>
                            <!--<tr>
                                <td>Doc_01.pdf</td>
                                <td>Hotel Contract</td>
                                <td>31 JAN ...</td>
                                <td class="text-right">
                                    <lightning:button label="View" variant="neutral" class="formButtonDestructiveInverse" />
                                    <span style="padding-left: 0.25em;">
                                        <lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" />
                                    </span>
                                </td>
                            </tr>
                            <tr>
                                <td>Doc_02.pdf</td>
                                <td>Hotel Contract</td>
                                <td>31 JAN ...</td>
                                <td class="text-right">
                                    <lightning:button label="View" variant="neutral" class="formButtonDestructiveInverse" />
                                    <span style="padding-left: 0.25em;">
                                        <lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" />
                                    </span>
                                </td>
                            </tr>
                            <tr>
                                <td>Doc_03.pdf</td>
                                <td>Hotel Contract</td>
                                <td>31 JAN ...</td>
                                <td class="text-right">
                                    <lightning:button label="View" variant="neutral" class="formButtonDestructiveInverse" />
                                    <span style="padding-left: 0.25em;">
                                        <lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" />
                                    </span>
                                </td>
                            </tr>-->
                            
                            <aura:iteration items="{!v.lsDocuments}" var="doc" indexVar="docIndex">
                                <tr>
                                    <td>{!doc.Title} <!--.{!doc.FileExtension}--></td>
                                    <td>{!doc.Description} <!--{!doc.FileType}--></td>
                                    <td><lightning:formattedDateTime value="{!doc.CreatedDate}" year="numeric" month="short" day="2-digit" hour="2-digit" minute="2-digit"/></td>
                                    <td class="text-right">
                                        <lightning:button label="View" iconName="utility:download" iconPosition="right" class="formButtonDestructiveInverse" value="{!docIndex}" onclick="{!c.navigateToDownload}"/>
                                        <!--<span style="padding-left: 0.25em;"><lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" value="{!docIndex}" onclick="{!c.navigateToDownload}"/></span>-->
                                    </td>
                                </tr>
							</aura:iteration>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="pageContentForm text-right" style="border-bottom: 1px solid #dee2e6; padding: 1em 2em; background-color: #f8f9fa;">
                <span>{!v.lsDocuments.length} items</span>
                <!--<div class="page-section-content_center">
                    <div class="reportBox">
                        <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                        <div class="reportBoxName">
                            <p title="Report Name">Document Name</p>
                        </div>
                        <div class="reportBoxDescription">
                            <p>
                                file1.pdf
                            </p>
                        </div>
                        <div style="margin-top: 0.5em;">
                            <lightning:button label="View" variant="brand" class="formButtonBrand" />
                        </div>
                    </div>
                </div>-->
            </div>
            <div class="text-right" style="margin-top: 0.5em;">
                <lightning:button label="Upload" variant="brand" class="formButtonBrand" onclick="{!c.openModal}"/>
            </div>
        </div>
    </div>
    
    <!-- modal upload -->
    <aura:if isTrue="{!v.isModalUploadOpen}">
        <!--###### MODAL BOX Start######-->
        <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
            <div class="slds-modal__container">
                <!-- ###### MODAL BOX HEADER Start ######-->
                <header class="slds-modal__header modalHeaderDocuments">
                    <!--<lightning:buttonIcon iconName="utility:close" onclick="{! c.closeModal }" alternativeText="close" variant="bare-inverse" class="slds-modal__close"/>-->
                    <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Add File</h2>
                </header>
                <!--###### MODAL BOX BODY Part Start######-->
                <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                    <p>
                        <lightning:input type="file" aura:id="inputFile" label="Upload File" variant="label-inline" name="inputFile" onchange="{! c.handleDocumentSelected }" required="true" class="inputlabelcustom1 inputwithfilebtncustom"/>
                        <div style="clear: none; padding: .25rem .25rem .25rem 33%;">{!v.documentNameSelected}</div>
                        <lightning:input aura:id="inputRenameFile" label="Rename File" variant="label-inline" name="inputRenameFile" placeholder="" required="true" class="inputlabelcustom1"/>
                        <lightning:select aura:id="selectDocumentType" label="Document Type" variant="label-inline" name="selectDocumentType" required="true" class="slds-form-element_horizontal inputlabelcustom1">
                            <option value="">Choose one...</option>
                            <option value="">test me</option>
                            <aura:iteration items="{!v.optionsDocumentType}" var="item">
                                <option text="{!item.label}" value="{!item.value}"/>
                            </aura:iteration>
                        </lightning:select>
                        
                        <!-- vendor -->
                        <aura:if isTrue="{!v.serviceType == 'All Services'}">
                            <lightning:select aura:id="selectBidId" label="Bid" variant="label-inline" name="selectBidId" required="true" class="slds-form-element_horizontal inputlabelcustom1">
                                <option value="">Choose one...</option>
                                <!--<aura:iteration items="{!v.optionsDocumentType}" var="item">
                                    <option text="{!item.label}" value="{!item.value}"/>
                                </aura:iteration>-->
                            </lightning:select>
    					</aura:if>
                        <!-- end vendor -->
                        
                        <!-- <lightning:fileUpload  name="fileUploader" label= "Choose File" multiple="false" disabled="false" recordId="abcd" onuploadfinished="{! c.handleUploadFinished }"/>-->
                    </p>
                    <span style="color: red;">{!v.formTextInfo}</span>
                </div>
                <!--###### MODAL BOX FOOTER Part Start ######-->
                <footer class="slds-modal__footer">
                    <lightning:button variant="neutral" label="Cancel" title="Cancel" onclick="{!c.closeModal}" class="formButtonBrandLightInverse"/>
                    <lightning:button variant="brand" label="Save" title="Save" onclick="{!c.submitBox}" class="formButtonBrandLight"/>
                </footer>
            </div>
        </section>
        <div class="slds-backdrop slds-backdrop_open"></div>
        <!--###### MODAL BOX Part END Here ######-->
    </aura:if>
    
    <!-- modal preview -->
    <aura:if isTrue="{!v.isModalPreviewOpen}">
        <section onclick="{!c.closeModalPreview}" role="dialog" aria-modal="true" class="slds-modal slds-fade-in-open">
            <div class="slds-modal__container">
                <div class="slds-modal__content slds-p-around_medium slds-text-align_center" style="background: transparent;">
                    <div style="width: 50%; margin: 0 auto; text-align: left">
                        <lightning:fileCard fileId="{!v.selectedPreviewDocumentId}"/>
                    </div>
                </div>
            </div>
        </section>
        <div class="slds-backdrop slds-backdrop_open"></div>
    </aura:if>
</aura:component>
```
### VoyajerDocuments

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerDocumentsController

```
({
	doInit : function(component, event, helper) {
        console.log("## doInit - VoyajerDocumentsController()");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadDocuments");
        callToParent.setParam("data",{
            serviceId: component.get("v.serviceId")
        });
        callToParent.fire();

console.log("## doInit - v.serviceId = " + component.get("v.serviceId"));
console.log("## doInit - v.serviceType = " + component.get("v.serviceType"));
console.log("## doInit - v.serviceCityName = " + component.get("v.serviceCityName"));
console.log("## doInit - v.optionRecordId = " + component.get("v.optionRecordId"));
        
        //set options
        var val_serviceType = component.get("v.serviceType");
        val_serviceType = (val_serviceType == "Housing__c" || val_serviceType == "Housing Bid") ? "Hotel Housing" : (val_serviceType == "Ground__c" || val_serviceType == "GT Bid") ? "Ground" : (val_serviceType == "Freight__c" || val_serviceType == "Freight Bid") ? "Freight" : (val_serviceType == "Air__c" || val_serviceType == "Air Bid") ? "Air" : val_serviceType;
        var opts = [];
        opts.push({ value: "Contract", label: "Contract" });
        switch (val_serviceType) {
            case "Hotel Housing":
                opts = [
                    { value: "Contract", label: "Contract" },
                    { value: "Contract to Client", label: "Contract to Client" },
                    { value: "Final Contract", label: "Final Contract" },
                    { value: "Date Change", label: "Date Change" },
                    { value: "No Rooms PU", label: "No Rooms PU" },
                    { value: "Cancellation", label: "Cancellation" },
                    { value: "GCIP", label: "GCIP" },
                    { value: "Rooming List", label: "Rooming List" },
                    { value: "Contract Client Signed", label: "Contract Client Signed" },
                    { value: "Pick Up Report", label: "Pick Up Report" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            case "Corporate Housing":
                opts = [
                    { value: "Rate Agreement", label: "Rate Agreement" },
                    { value: "Date Change", label: "Date Change" },
                    { value: "Cancellation", label: "Cancellation" },
                    { value: "Rooming List", label: "Rooming List" },
                    { value: "Pick Up Report", label: "Pick Up Report" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            case "Ground":
                opts = [
                    { value: "Contract", label: "Contract" },
                    { value: "Contract to Client", label: "Contract to Client" },
                    { value: "Contract Client Signed", label: "Contract Client Signed" },
                    { value: "Final", label: "Final" },
                    { value: "Trip Update", label: "Trip Update" },
                    { value: "Cancellation", label: "Cancellation" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            case "Air":
                opts = [
                    { value: "Name List", label: "Name List" },
                    { value: "Contract", label: "Contract" },
                    { value: "Deposit/LOCSignedContract", label: "Deposit/LOCSignedContract" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            default:
                break;
        };
        
        component.set("v.optionsDocumentType", opts);
	},
    
	handleBack : function(component, event, helper){
        var userProfile = component.get("v.userProfile");
        if(userProfile == "Customer") component.set("v.mainContent", "overview");
        else component.set("v.mainContent", "dashboardBids");
	},
    
    handleFilter: function(component, event, helper) {
        var val_filterBtn = event.getSource().get("v.value");
        var lsDocuments_org = component.get("v.lsDocuments_org");
        var val_filterSelected = component.find("filter_selectDocumentType").get("v.value");
        
        console.log("val_filterBtn = " + val_filterBtn);
        if(lsDocuments_org != null) console.log("lsDocuments_org.length = " + lsDocuments_org.length);
        console.log("val_filterSelected = " + val_filterSelected);
        
        switch (val_filterBtn) {
            case "Update":
                //filter list..
                if(lsDocuments_org != null && lsDocuments_org.length > 0 && val_filterSelected != ''){
        			var lsAux = [];
                    
                    Object.keys(lsDocuments_org).forEach(function(key){
                        console.log("key = " + key);
                        console.log("Title = " + lsDocuments_org[key].Title);
                        console.log("Description = " + lsDocuments_org[key].Description);
                        
                        if(lsDocuments_org[key].Description == val_filterSelected){
                            console.log("find equal!");
                            lsAux.push(lsDocuments_org[key]);
							/*lsDocuments_org.splice(key, 1);*/
                        };
                    });
					
                    console.log("lsAux.length = " + lsAux.length);
					//set new list filtered
					component.set("v.lsDocuments", lsAux);
                };
                break;
            case "View all":
                var lsDocuments = component.get("v.lsDocuments");
                console.log("lsDocuments.length = " + lsDocuments.length);
                
                component.set("v.lsDocuments", lsDocuments_org);
                component.find("filter_selectDocumentType").set("v.value","");

/*              //call init
                var a = component.get('c.doInit');
                $A.enqueueAction(a);*/
                break;
            default:
                break;
        };
    },
    
    navigateToDownload : function(component, event, helper) {
        var idx = event.getSource().get("v.value");
        var doc = component.get("v.lsDocuments")[idx];
        console.log(" idx = " + idx);
		console.log(" doc.id = " + doc.Id);
        var theURL = window.location.href;
        var isCCDev = theURL.includes('ccdev');
        var url = isCCDev ? 'https://roadrebel--ccdev.lightning.force.com/sfc/servlet.shepherd/document/download/'+doc.ContentDocumentId+'?operationContext=S1' : 'https://roadrebel.lightning.force.com/sfc/servlet.shepherd/document/download/'+doc.ContentDocumentId+'?operationContext=S1'; 

        window.open(url);
	},
    
    //modal preview
    navigateToView : function(component, event, helper) {
        var idx = event.getSource().get("v.value");
        var doc = component.get("v.lsDocuments")[idx];
        console.log(" idx = " + idx);
		console.log(" doc.id = " + doc.Id);
        
        //open url
        /*var url = 'https://roadrebel--ccdev.lightning.force.com/lightning/r/ContentDocument/'+doc.ContentDocumentId+'/view'
        window.open(url);*/
        
        //open modal preview
        component.set("v.isModalPreviewOpen" , true);
        component.set("v.selectedPreviewDocumentId", doc.ContentDocumentId);
	},
    
    closeModalPreview: function(component, event, helper) {
        component.set("v.isModalPreviewOpen", false);
        component.set("v.selectedPreviewDocumentId", null);
    },
    
    //modal upload
    openModal: function(component, event, helper) {
        component.set("v.isModalUploadOpen", true);
    },
    
    closeModal: function(component, event, helper) {
        component.set("v.isModalUploadOpen", false);
        component.set("v.documentNameSelected", "");
        component.set("v.formTextInfo", "");
    },
    
    submitBox: function(component, event, helper) {
        var files = component.find("inputFile").get("v.files");
        var val_inputRenameFile = component.find("inputRenameFile").get("v.value");
        var val_selectDocumentType = component.find("selectDocumentType").get("v.value");
        var val_serviceId = component.get("v.serviceId");
        var callToParent = component.getEvent("callToParent");
        component.set("v.formTextInfo", "");

        //check values to upload function...
        if( files != null && files.length > 0 && val_inputRenameFile != '' && val_selectDocumentType != '' && val_serviceId != ''){
            var fileReader = new FileReader();  
            var file = files[0];
            
            fileReader.readAsDataURL(file);
            fileReader.onload = function () {
                var docName = file.name;
                var docContentBase64 = fileReader.result.split('base64,')[1];
                var docReName = val_inputRenameFile; //component.get("v.documentNameSelected");
                var docType = val_selectDocumentType; //'doc type test';
                var docServiceId = val_serviceId; //component.get("v.serviceId");
            
                console.log(" docName = " + docName);
                console.log(" docContentBase64 = " + docContentBase64);
                console.log(" docReName = " + docReName);
                console.log(" docType = " + docType);
                console.log(" docServiceId = " + docServiceId);
            
                //call parent method
                callToParent.setParam("action","uploadDocument");
                callToParent.setParam("data",{
                    docName: docName,
                    docContentBase64: docContentBase64,
                    docReName: docReName,
                    docType: docType,
                    docServiceId: docServiceId
                });
                callToParent.fire();
                
                //call to load all documents...
                console.log("call to load all documents...");
                var a = component.get('c.doInit');
                $A.enqueueAction(a);
            };
            
            // close modal
        	component.set("v.isModalUploadOpen", false);
        }else{
            console.log("none, complete fields!");
            component.set("v.formTextInfo", "Please complete all required fields.");
        }
    },
    
    handleDocumentSelected: function(component, event, helper) {
    	var files = event.getSource().get("v.files");
    	if( files.length > 0 ){
    		var file = files[0];
    		console.log(" file = " + file);
        	component.set("v.documentNameSelected", file.name);
		}
    }
})
```
### VoyajerDocumentsHelper

```
({
	helperMethod : function() {
		
	}
})
```
### VoyajerDocuments

```
.THIS {
}

.THIS .tableDoc {
    width: 100%;
    /*margin-bottom: 1rem;*/
    color: #212529;
    border-collapse: collapse;
}

.THIS .tableDoc thead th {
    vertical-align: bottom;
    border-bottom: 2px solid #dee2e6;
}

.THIS .tableDoc td,
.THIS .tableDoc th {
    padding: .75rem;
    vertical-align: top;
}

.THIS .tableDoc td {
    border-top: 1px solid #dee2e6;
}

.THIS .tableDoc tbody tr:hover {
	background-color: #e7f8ff;
}

.THIS .slds-button,
.THIS .slds-select_container{
    margin: 0rem 0.25rem;
}

.THIS .slds-select {
    border-radius: 3em;
	height: 35px;
    /*text-transform: uppercase;*/
}

.THIS .inputlabelcustom1 .slds-form-element__label {
    color: #000 !important;
    font-size: 14px !important;
    /*display: none;*/
}

.THIS .inputwithfilebtncustom .slds-file-selector__button {
    background-color: #0065ff;
    color: #fff;
}

.THIS .inputlabelhide .slds-form-element__label {
    display: none;
}

.THIS .text-right{
    text-align: right !important;
}

.THIS .formButtonBrandLightInverse {
    color: #00b4ff;
    border-color: #09b7ff;
}

.THIS .formButtonBrandLightInverse:hover {
    background-color: #eaf8ff;
}

.THIS .modalHeaderDocuments {
    background-color: #022066 !important;
    color: #fff !important;
    text-align: left !important;
}
```
### VoyajerDocuments

```
<aura:component>
    <aura:attribute type="String" name="mainContent" />
    <aura:attribute type="String" name="optionRecordId" />
    <aura:attribute type="String" name="userProfile" />
    
    <aura:attribute type="String" name="serviceId" />
	<aura:attribute name="serviceDateInAndOut" type="String"/>
    <aura:attribute name="serviceCityName" type="String"/>
    <aura:attribute type="String" name="bidName" />
    <aura:attribute name="startDate" type="String" />
	<aura:attribute name="endDate" type="String" />
	<aura:attribute name="selectedLookupId" type="String" />
    <aura:attribute name="selectedPillText" type="String" />
       
   	<aura:attribute type="Object" name="serviceData" />
    <aura:attribute type="String" name="productionName" />
    <aura:attribute type="String" name="subtextinerary" />
    <aura:attribute type="String" name="cityName" />
    <aura:attribute type="String" name="dateIn" />
    <aura:attribute type="String" name="dateOut" />
    <aura:attribute type="List" name="lsDocuments" default="[]" />
    <aura:attribute type="List" name="lsDocuments_org" default="[]" />
    
    <aura:handler name="init" value="{!this}" action="{!c.doInit}" />
    <aura:registerEvent type="c:VoyajerCallToParent" name="callToParent" />
    
    <!-- modals -->
    <aura:attribute name="isModalUploadOpen" type="boolean" default="false"/>
    <aura:attribute name="documentNameSelected" type="String" default=""/>
    <aura:attribute name="formTextInfo" type="String" default=""/>
    
    <aura:attribute name="isModalPreviewOpen" type="boolean" default="false"/>
    <aura:attribute name="selectedPreviewDocumentId" type="String" default=""/>
    
    <!-- opcs -->
    <aura:attribute type="String" name="serviceType" />
    <aura:attribute name="optionsDocumentType" type="List" />
    <aura:attribute name="optionsDocumentType_selectedValue" type="String" default=""/>
    
    <div class="pageContent">
        <div class="pageContentSpaces">
            <div class="page-section">
                <div class="page-header">
                    <div>
                        <h1 style="display: flex; align-items: center; /*font-weight: 800;*/">
                            <lightning:icon iconName="utility:description" alternativeText="Contact" size="small" />
                            <span style="padding-left: 0.25em;">Documents</span>
                        </h1>
                    </div>
                    <div class="text-right" style="float:left;">
                        <lightning:button label="Back" variant="brand" class="formButtonBrand" onclick="{!c.handleBack}" />
                    </div>
                </div>
            </div>
            <div class="pageContentForm header" style="display: flex;">
                <div>
                    <div>
                        <h3 style="font-weight: 800;">{!v.productionName}</h3>
                    </div>
                    <div>
                        <!--<span style="font-weight: 600; color: #09b7ff;">{!v.cityName}</span> | <span style="font-weight: 600; color: #09b7ff;">{!v.dateIn} - {!v.dateOut}</span>-->
                        <span style="font-weight: 600; color: #09b7ff;">{!v.serviceCityName}</span> | <span style="font-weight: 600; color: #09b7ff;">{!v.serviceDateInAndOut}</span>
                        <!--{!v.serviceData.cityName} | {!v.serviceData.dateIn} - {!v.serviceData.dateOut}-->
                    </div>
                    <div>
                        <span style="font-weight: 600;">{!v.bidName}</span>
                    </div>
                </div>
			</div>
            <div class="pageContentForm" style="display: flex; border-bottom: 1px solid #dee2e6; padding: 0em 2em 2em;">
                <div class="page-section-buttons">
                    <div style="height: 2.5em;">
                        <span>Filter by</span>
                        <lightning:select  aura:id="filter_selectDocumentType" name="select1" label="Document Type" required="false" variant="label-inline" class="inputlabelhide">
                            <option value="">Document Type</option>
                            <aura:iteration items="{!v.optionsDocumentType}" var="item">
                                <option text="{!item.label}" value="{!item.value}"/>
                            </aura:iteration>
                        </lightning:select>
                        <lightning:button label="UPDATE" 
                                          name="Update" 
                                          variant="brand" 
                                          class="formButtonBrandLight" 
                                          value="Update"
                                          onclick="{!c.handleFilter}" />
                        <lightning:button label="CLEAR" 
                                          name="Clear" 
                                          variant="neutral" 
                                          class="formButtonBrandLightInverse" 
                                          value="View all"
                                          onclick="{!c.handleFilter}" />

                        <!--<lightning:buttonIcon iconName="utility:sync" variant="brand" class="formButtonBrandLight showOnMobile" onclick="{!c.doInit}" />-->
                    </div>
                </div>
            </div>
            <div class="pageContentForm" style="border-bottom: 1px solid #dee2e6; padding: 0.5em 2em;">
                <div>
                    <table class="tableDoc">
                        <thead>
                            <tr>
                                <th scope="col" width="50%">Document Name</th>
                                <th scope="col" width="">Document Type</th>
                                <th scope="col" width="">Date Uploaded</th>
                                <th scope="col" width=""></th>
                            </tr>
                        </thead>
                        <tbody>
                            <!--<tr>
                                <td>Doc_01.pdf</td>
                                <td>Hotel Contract</td>
                                <td>31 JAN ...</td>
                                <td class="text-right">
                                    <lightning:button label="View" variant="neutral" class="formButtonDestructiveInverse" />
                                    <span style="padding-left: 0.25em;">
                                        <lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" />
                                    </span>
                                </td>
                            </tr>
                            <tr>
                                <td>Doc_02.pdf</td>
                                <td>Hotel Contract</td>
                                <td>31 JAN ...</td>
                                <td class="text-right">
                                    <lightning:button label="View" variant="neutral" class="formButtonDestructiveInverse" />
                                    <span style="padding-left: 0.25em;">
                                        <lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" />
                                    </span>
                                </td>
                            </tr>
                            <tr>
                                <td>Doc_03.pdf</td>
                                <td>Hotel Contract</td>
                                <td>31 JAN ...</td>
                                <td class="text-right">
                                    <lightning:button label="View" variant="neutral" class="formButtonDestructiveInverse" />
                                    <span style="padding-left: 0.25em;">
                                        <lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" />
                                    </span>
                                </td>
                            </tr>-->
                            
                            <aura:iteration items="{!v.lsDocuments}" var="doc" indexVar="docIndex">
                                <tr>
                                    <td>{!doc.Title} <!--.{!doc.FileExtension}--></td>
                                    <td>{!doc.Description} <!--{!doc.FileType}--></td>
                                    <td><lightning:formattedDateTime value="{!doc.CreatedDate}" year="numeric" month="short" day="2-digit" hour="2-digit" minute="2-digit"/></td>
                                    <td class="text-right">
                                        <lightning:button label="View" iconName="utility:download" iconPosition="right" class="formButtonDestructiveInverse" value="{!docIndex}" onclick="{!c.navigateToDownload}"/>
                                        <!--<span style="padding-left: 0.25em;"><lightning:buttonIcon iconName="utility:download" size="large" variant="bare" alternativeText="Download" value="{!docIndex}" onclick="{!c.navigateToDownload}"/></span>-->
                                    </td>
                                </tr>
							</aura:iteration>
                        </tbody>
                    </table>
                </div>
            </div>
            <div class="pageContentForm text-right" style="border-bottom: 1px solid #dee2e6; padding: 1em 2em; background-color: #f8f9fa;">
                <span>{!v.lsDocuments.length} items</span>
                <!--<div class="page-section-content_center">
                    <div class="reportBox">
                        <div><lightning:icon iconName="utility:edit_form" alternativeText="Manager" class="reportBoxIcon" /></div>
                        <div class="reportBoxName">
                            <p title="Report Name">Document Name</p>
                        </div>
                        <div class="reportBoxDescription">
                            <p>
                                file1.pdf
                            </p>
                        </div>
                        <div style="margin-top: 0.5em;">
                            <lightning:button label="View" variant="brand" class="formButtonBrand" />
                        </div>
                    </div>
                </div>-->
            </div>
            <div class="text-right" style="margin-top: 0.5em;">
                <lightning:button label="Upload" variant="brand" class="formButtonBrand" onclick="{!c.openModal}"/>
            </div>
        </div>
    </div>
    
    <!-- modal upload -->
    <aura:if isTrue="{!v.isModalUploadOpen}">
        <!--###### MODAL BOX Start######-->
        <section role="dialog" tabindex="-1" aria-labelledby="modal-heading-01" aria-modal="true" aria-describedby="modal-content-id-1" class="slds-modal slds-fade-in-open">
            <div class="slds-modal__container">
                <!-- ###### MODAL BOX HEADER Start ######-->
                <header class="slds-modal__header modalHeaderDocuments">
                    <!--<lightning:buttonIcon iconName="utility:close" onclick="{! c.closeModal }" alternativeText="close" variant="bare-inverse" class="slds-modal__close"/>-->
                    <h2 id="modal-heading-01" class="slds-text-heading_medium slds-hyphenate">Add File</h2>
                </header>
                <!--###### MODAL BOX BODY Part Start######-->
                <div class="slds-modal__content slds-p-around_medium" id="modal-content-id-1">
                    <p>
                        <lightning:input type="file" aura:id="inputFile" label="Upload File" variant="label-inline" name="inputFile" onchange="{! c.handleDocumentSelected }" required="true" class="inputlabelcustom1 inputwithfilebtncustom"/>
                        <div style="clear: none; padding: .25rem .25rem .25rem 33%;">{!v.documentNameSelected}</div>
                        <lightning:input aura:id="inputRenameFile" label="Rename File" variant="label-inline" name="inputRenameFile" placeholder="" required="true" class="inputlabelcustom1"/>
                        <lightning:select aura:id="selectDocumentType" label="Document Type" variant="label-inline" name="selectDocumentType" required="true" class="slds-form-element_horizontal inputlabelcustom1">
                            <option value="">Choose one...</option>
                            <option value="">test me</option>
                            <aura:iteration items="{!v.optionsDocumentType}" var="item">
                                <option text="{!item.label}" value="{!item.value}"/>
                            </aura:iteration>
                        </lightning:select>
                        
                        <!-- vendor -->
                        <aura:if isTrue="{!v.serviceType == 'All Services'}">
                            <lightning:select aura:id="selectBidId" label="Bid" variant="label-inline" name="selectBidId" required="true" class="slds-form-element_horizontal inputlabelcustom1">
                                <option value="">Choose one...</option>
                                <!--<aura:iteration items="{!v.optionsDocumentType}" var="item">
                                    <option text="{!item.label}" value="{!item.value}"/>
                                </aura:iteration>-->
                            </lightning:select>
    					</aura:if>
                        <!-- end vendor -->
                        
                        <!-- <lightning:fileUpload  name="fileUploader" label= "Choose File" multiple="false" disabled="false" recordId="abcd" onuploadfinished="{! c.handleUploadFinished }"/>-->
                    </p>
                    <span style="color: red;">{!v.formTextInfo}</span>
                </div>
                <!--###### MODAL BOX FOOTER Part Start ######-->
                <footer class="slds-modal__footer">
                    <lightning:button variant="neutral" label="Cancel" title="Cancel" onclick="{!c.closeModal}" class="formButtonBrandLightInverse"/>
                    <lightning:button variant="brand" label="Save" title="Save" onclick="{!c.submitBox}" class="formButtonBrandLight"/>
                </footer>
            </div>
        </section>
        <div class="slds-backdrop slds-backdrop_open"></div>
        <!--###### MODAL BOX Part END Here ######-->
    </aura:if>
    
    <!-- modal preview -->
    <aura:if isTrue="{!v.isModalPreviewOpen}">
        <section onclick="{!c.closeModalPreview}" role="dialog" aria-modal="true" class="slds-modal slds-fade-in-open">
            <div class="slds-modal__container">
                <div class="slds-modal__content slds-p-around_medium slds-text-align_center" style="background: transparent;">
                    <div style="width: 50%; margin: 0 auto; text-align: left">
                        <lightning:fileCard fileId="{!v.selectedPreviewDocumentId}"/>
                    </div>
                </div>
            </div>
        </section>
        <div class="slds-backdrop slds-backdrop_open"></div>
    </aura:if>
</aura:component>
```
### VoyajerDocuments

```
<?xml version="1.0" encoding="UTF-8"?>
<AuraDefinitionBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>48.0</apiVersion>
    <description>A Lightning Component Bundle</description>
</AuraDefinitionBundle>
```
### VoyajerDocumentsController

```
({
	doInit : function(component, event, helper) {
        console.log("## doInit - VoyajerDocumentsController()");
        var callToParent = component.getEvent("callToParent");
        callToParent.setParam("action","loadDocuments");
        callToParent.setParam("data",{
            serviceId: component.get("v.serviceId")
        });
        callToParent.fire();

console.log("## doInit - v.serviceId = " + component.get("v.serviceId"));
console.log("## doInit - v.serviceType = " + component.get("v.serviceType"));
console.log("## doInit - v.serviceCityName = " + component.get("v.serviceCityName"));
console.log("## doInit - v.optionRecordId = " + component.get("v.optionRecordId"));
        
        //set options
        var val_serviceType = component.get("v.serviceType");
        val_serviceType = (val_serviceType == "Housing__c" || val_serviceType == "Housing Bid") ? "Hotel Housing" : (val_serviceType == "Ground__c" || val_serviceType == "GT Bid") ? "Ground" : (val_serviceType == "Freight__c" || val_serviceType == "Freight Bid") ? "Freight" : (val_serviceType == "Air__c" || val_serviceType == "Air Bid") ? "Air" : val_serviceType;
        var opts = [];
        opts.push({ value: "Contract", label: "Contract" });
        switch (val_serviceType) {
            case "Hotel Housing":
                opts = [
                    { value: "Contract", label: "Contract" },
                    { value: "Contract to Client", label: "Contract to Client" },
                    { value: "Final Contract", label: "Final Contract" },
                    { value: "Date Change", label: "Date Change" },
                    { value: "No Rooms PU", label: "No Rooms PU" },
                    { value: "Cancellation", label: "Cancellation" },
                    { value: "GCIP", label: "GCIP" },
                    { value: "Rooming List", label: "Rooming List" },
                    { value: "Contract Client Signed", label: "Contract Client Signed" },
                    { value: "Pick Up Report", label: "Pick Up Report" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            case "Corporate Housing":
                opts = [
                    { value: "Rate Agreement", label: "Rate Agreement" },
                    { value: "Date Change", label: "Date Change" },
                    { value: "Cancellation", label: "Cancellation" },
                    { value: "Rooming List", label: "Rooming List" },
                    { value: "Pick Up Report", label: "Pick Up Report" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            case "Ground":
                opts = [
                    { value: "Contract", label: "Contract" },
                    { value: "Contract to Client", label: "Contract to Client" },
                    { value: "Contract Client Signed", label: "Contract Client Signed" },
                    { value: "Final", label: "Final" },
                    { value: "Trip Update", label: "Trip Update" },
                    { value: "Cancellation", label: "Cancellation" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            case "Air":
                opts = [
                    { value: "Name List", label: "Name List" },
                    { value: "Contract", label: "Contract" },
                    { value: "Deposit/LOCSignedContract", label: "Deposit/LOCSignedContract" },
                    { value: "Send Mail", label: "Send Mail" }
                ];
                break;
            default:
                break;
        };
        
        component.set("v.optionsDocumentType", opts);
	},
    
	handleBack : function(component, event, helper){
        var userProfile = component.get("v.userProfile");
        if(userProfile == "Customer") component.set("v.mainContent", "overview");
        else component.set("v.mainContent", "dashboardBids");
	},
    
    handleFilter: function(component, event, helper) {
        var val_filterBtn = event.getSource().get("v.value");
        var lsDocuments_org = component.get("v.lsDocuments_org");
        var val_filterSelected = component.find("filter_selectDocumentType").get("v.value");
        
        console.log("val_filterBtn = " + val_filterBtn);
        if(lsDocuments_org != null) console.log("lsDocuments_org.length = " + lsDocuments_org.length);
        console.log("val_filterSelected = " + val_filterSelected);
        
        switch (val_filterBtn) {
            case "Update":
                //filter list..
                if(lsDocuments_org != null && lsDocuments_org.length > 0 && val_filterSelected != ''){
        			var lsAux = [];
                    
                    Object.keys(lsDocuments_org).forEach(function(key){
                        console.log("key = " + key);
                        console.log("Title = " + lsDocuments_org[key].Title);
                        console.log("Description = " + lsDocuments_org[key].Description);
                        
                        if(lsDocuments_org[key].Description == val_filterSelected){
                            console.log("find equal!");
                            lsAux.push(lsDocuments_org[key]);
							/*lsDocuments_org.splice(key, 1);*/
                        };
                    });
					
                    console.log("lsAux.length = " + lsAux.length);
					//set new list filtered
					component.set("v.lsDocuments", lsAux);
                };
                break;
            case "View all":
                var lsDocuments = component.get("v.lsDocuments");
                console.log("lsDocuments.length = " + lsDocuments.length);
                
                component.set("v.lsDocuments", lsDocuments_org);
                component.find("filter_selectDocumentType").set("v.value","");

/*              //call init
                var a = component.get('c.doInit');
                $A.enqueueAction(a);*/
                break;
            default:
                break;
        };
    },
    
    navigateToDownload : function(component, event, helper) {
        var idx = event.getSource().get("v.value");
        var doc = component.get("v.lsDocuments")[idx];
        console.log(" idx = " + idx);
		console.log(" doc.id = " + doc.Id);
        var theURL = window.location.href;
        var isCCDev = theURL.includes('ccdev');
        var url = isCCDev ? 'https://roadrebel--ccdev.lightning.force.com/sfc/servlet.shepherd/document/download/'+doc.ContentDocumentId+'?operationContext=S1' : 'https://roadrebel.lightning.force.com/sfc/servlet.shepherd/document/download/'+doc.ContentDocumentId+'?operationContext=S1'; 

        window.open(url);
	},
    
    //modal preview
    navigateToView : function(component, event, helper) {
        var idx = event.getSource().get("v.value");
        var doc = component.get("v.lsDocuments")[idx];
        console.log(" idx = " + idx);
		console.log(" doc.id = " + doc.Id);
        
        //open url
        /*var url = 'https://roadrebel--ccdev.lightning.force.com/lightning/r/ContentDocument/'+doc.ContentDocumentId+'/view'
        window.open(url);*/
        
        //open modal preview
        component.set("v.isModalPreviewOpen" , true);
        component.set("v.selectedPreviewDocumentId", doc.ContentDocumentId);
	},
    
    closeModalPreview: function(component, event, helper) {
        component.set("v.isModalPreviewOpen", false);
        component.set("v.selectedPreviewDocumentId", null);
    },
    
    //modal upload
    openModal: function(component, event, helper) {
        component.set("v.isModalUploadOpen", true);
    },
    
    closeModal: function(component, event, helper) {
        component.set("v.isModalUploadOpen", false);
        component.set("v.documentNameSelected", "");
        component.set("v.formTextInfo", "");
    },
    
    submitBox: function(component, event, helper) {
        var files = component.find("inputFile").get("v.files");
        var val_inputRenameFile = component.find("inputRenameFile").get("v.value");
        var val_selectDocumentType = component.find("selectDocumentType").get("v.value");
        var val_serviceId = component.get("v.serviceId");
        var callToParent = component.getEvent("callToParent");
        component.set("v.formTextInfo", "");

        //check values to upload function...
        if( files != null && files.length > 0 && val_inputRenameFile != '' && val_selectDocumentType != '' && val_serviceId != ''){
            var fileReader = new FileReader();  
            var file = files[0];
            
            fileReader.readAsDataURL(file);
            fileReader.onload = function () {
                var docName = file.name;
                var docContentBase64 = fileReader.result.split('base64,')[1];
                var docReName = val_inputRenameFile; //component.get("v.documentNameSelected");
                var docType = val_selectDocumentType; //'doc type test';
                var docServiceId = val_serviceId; //component.get("v.serviceId");
            
                console.log(" docName = " + docName);
                console.log(" docContentBase64 = " + docContentBase64);
                console.log(" docReName = " + docReName);
                console.log(" docType = " + docType);
                console.log(" docServiceId = " + docServiceId);
            
                //call parent method
                callToParent.setParam("action","uploadDocument");
                callToParent.setParam("data",{
                    docName: docName,
                    docContentBase64: docContentBase64,
                    docReName: docReName,
                    docType: docType,
                    docServiceId: docServiceId
                });
                callToParent.fire();
                
                //call to load all documents...
                console.log("call to load all documents...");
                var a = component.get('c.doInit');
                $A.enqueueAction(a);
            };
            
            // close modal
        	component.set("v.isModalUploadOpen", false);
        }else{
            console.log("none, complete fields!");
            component.set("v.formTextInfo", "Please complete all required fields.");
        }
    },
    
    handleDocumentSelected: function(component, event, helper) {
    	var files = event.getSource().get("v.files");
    	if( files.length > 0 ){
    		var file = files[0];
    		console.log(" file = " + file);
        	component.set("v.documentNameSelected", file.name);
		}
    }
})
```
### VoyajerDocumentsHelper

```
({
	helperMethod : function() {
		
	}
})
```

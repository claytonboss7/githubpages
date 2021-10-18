---
layout: default
title: InboundProcessVFP
parent: pages
---

```<apex:page id="inboundProcess" lightningStylesheets="true" title="Inbound Process" controller="InboundProcessController" standardStylesheets="true" showHeader="false" sidebar="false" cache="false" applyBodyTag="false" applyHtmlTag="false" docType="html-5.0">
    <html xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" lang="en">
        <head>
            <meta charset="utf-8" />
            <meta http-equiv="x-ua-compatible" content="ie=edge" />
        	<title>Inbound Process</title>
        	<meta name="viewport" content="width=device-width, initial-scale=1" />
            <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap.min.css')}"/>
        	<apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/jquery.inputpicker.css')}"/>
            <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/chosen.css')}"/>
        	<apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap-toggle.min.css')}"/>
            <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap-select.css')}"/>
            <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/all.css')}"/>
		    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap-datetimepicker.min.css')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery-3.3.1.min.js')}"  />
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap.min.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap.bundle.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery.inputpicker.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery.autocomplete.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/chosen.jquery.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap-toggle.min.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/ckeditor.js')}"  />
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap-select.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/moment.min.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap-datetimepicker.min.js')}"/>
            <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery.mask.min.js')}"/>
            <apex:includeScript value="{!$Resource.jquerydateFormat}" />
            <apex:slds />
            <style>
                .datePicker{
                display:none;
                padding:0px 0px 0px 0px;
                
                }
                .content { font-size:12px; margin-left: 25px !important; margin-right: 25px !important; }
                .container { font-size:12px; }
                .row { margin-top: 10px !important; }
                .dataCol { width:25% !important; }
                html { height: 100%; }
                body { height: 100%; }
                body .pbSubsection {padding: 3.5px !important; }
                body .bPageBlock .detailList .labelCol { width:25% !important; }
                body .bPageBlock .detailList .labelCol label { margin-top: 0.3rem; }
                body .dataCol select { margin-bottom:0; }
                label { margin-bottom: .2rem; }
                
                /* lookup field override */
                .lookupInput { display: block !important; vertical-align: middle; white-space: nowrap; }
                .lookupInput img { background-repeat: no-repeat; margin-right: .25em; vertical-align: middle; }
                .lookupInput .disabled { background-color: #ccc; }
                .lookupInput .emptyDependentLookup { font-style: italic; }
                .lookupInput input[readonly] { background-color: #e6e6e6; border: 2px solid #e6e6e6; color: #333; cursor: default; }
                .lookupInput a.readOnly { float: right; }
                .lookupInput span.readOnly { display: block; white-space: normal; }
                .lookupInput span.totalSummary { font-weight: bold; }
                .inlineEditRequiredDiv .lookupInput img,.inlineEditDiv .lookupInput img { vertical-align: middle; }
                .quickCreateModule .lookupInput input { max-width: 155px; }
                .lookupIcon { background-image: url(/img/func_icons/util/lookup20.gif); background-position: 0 0; width: 20px; height: 20px; background-position: top left; }
                .lookupIconOn { background-image: url(/img/func_icons/util/lookup20.gif); background-position: 0 0; width: 20px; height: 20px; background-position: top right;  }
                .lookupInput input { float: left; }
                .lookupInput a { width: 4%; border-left: none; position: absolute; right: 0px; border-bottom: none; }
                
                /** LOADING **/
                /* Absolute Center Spinner */
                .loading { position: fixed; z-index: 1051; height: 2em; width: 2em; overflow: show; margin: auto; top: 0; left: 0; bottom: 0; right: 0; }
                
                /* Transparent Overlay */
                .loading:before { content: ''; display: block; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: rgba(0,0,0,0.3); }
                
                /* :not(:required) hides these rules from IE9 and below */
                .loading:not(:required) { /* hide "loading..." text */ font: 0/0 a; color: transparent; text-shadow: none; background-color: transparent; border: 0; }
                .loading:not(:required):after { content: ''; display: block; font-size: 10px; width: 1em; height: 1em; margin-top: -0.5em; -webkit-animation: spinner 1500ms infinite linear; -moz-animation: spinner 1500ms infinite linear; -ms-animation: spinner 1500ms infinite linear; -o-animation: spinner 1500ms infinite linear; animation: spinner 1500ms infinite linear; border-radius: 0.5em; -webkit-box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.5) -1.5em 0 0 0, rgba(0, 0, 0, 0.5) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0, rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0; box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) -1.5em 0 0 0, rgba(0, 0, 0, 0.75) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0, rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0; } 
                
                /* Animation */
                @-webkit-keyframes spinner {
                    0% { -webkit-transform: rotate(0deg); -moz-transform: rotate(0deg); -ms-transform: rotate(0deg); -o-transform: rotate(0deg); transform: rotate(0deg); }
                    100% { -webkit-transform: rotate(360deg); -moz-transform: rotate(360deg); -ms-transform: rotate(360deg); -o-transform: rotate(360deg); transform: rotate(360deg); }
                }
                @-moz-keyframes spinner {
                    0% { -webkit-transform: rotate(0deg); -moz-transform: rotate(0deg); -ms-transform: rotate(0deg); -o-transform: rotate(0deg); transform: rotate(0deg); }
                    100% { -webkit-transform: rotate(360deg); -moz-transform: rotate(360deg); -ms-transform: rotate(360deg); -o-transform: rotate(360deg); transform: rotate(360deg); }
                }
                @-o-keyframes spinner {
                    0% { -webkit-transform: rotate(0deg); -moz-transform: rotate(0deg); -ms-transform: rotate(0deg); -o-transform: rotate(0deg); transform: rotate(0deg); }
                    100% { -webkit-transform: rotate(360deg); -moz-transform: rotate(360deg); -ms-transform: rotate(360deg); -o-transform: rotate(360deg); transform: rotate(360deg); }
                }
                @keyframes spinner {
                    0% { -webkit-transform: rotate(0deg); -moz-transform: rotate(0deg); -ms-transform: rotate(0deg); -o-transform: rotate(0deg); transform: rotate(0deg); }
                    100% { -webkit-transform: rotate(360deg); -moz-transform: rotate(360deg); -ms-transform: rotate(360deg); -o-transform: rotate(360deg); transform: rotate(360deg); }
                }
                /** END LOADING **/
                
                .autocomplete-suggestions { -webkit-box-sizing: border-box; -moz-box-sizing: border-box; box-sizing: border-box; border: 1px solid #999; background: #FFF; cursor: default; overflow: auto; -webkit-box-shadow: 1px 4px 3px rgba(50, 50, 50, 0.64); -moz-box-shadow: 1px 4px 3px rgba(50, 50, 50, 0.64); box-shadow: 1px 4px 3px rgba(50, 50, 50, 0.64); }
                .autocomplete-suggestion { font-size: 12px;padding: 2px 5px; white-space: nowrap; overflow: hidden; }
                .autocomplete-no-suggestion { padding: 2px 5px; }
                .autocomplete-selected { background: #F0F0F0; }
                .autocomplete-suggestions strong { font-weight: bold; color: #000; }
                .autocomplete-group { padding: 2px 5px; font-weight: bold; font-size: 16px; color: #000; display: block; border-bottom: 1px solid #000; }
                
                .tableLight { font-size:12px; }
                .tableLight thead th { background-color: rgb(250, 250, 249); text-transform: uppercase; font-weight: bold; color: rgb(81, 79, 77); }
                .tableLight .first { font-weight: bold; color: rgb(81, 79, 77); }
                
                .btnNew { color: #fff !important; background-color: #007bff !important; border-color: #007bff !important; }
                .pbBody { overflow: hidden !important; }
                .small { font-size:70% !important; }
                .nav li a { font-size: 12px; padding: .5rem 4rem; }
                .tab-content { font-size:12px; padding:10px; }
                .btn-custom { font-size: 11px; }
                .btn-danger { font-weight: 400; color: #fff !important; background-color: #dc3545 !important; border-color: #dc3545 !important; }
                .messageCell h4 { text-align:left !important; font-size:.8125rem !important; }
                .table-custom td { padding: 0px 15px 5px 0px; }
                .error-custom { border-color: red !important; }
                .datePicker { z-index:1051 !important; }
                .fieldset { border: 1px solid #ddd !important; margin: 15px 0 0 0; min-width: 0; padding: 10px;        position: relative; border-radius:4px; background-color:#f5f5f5; padding-left:10px!important; }
                .group-custom { border: 1px solid #ddd !important; margin: 15px 0 0 0; min-width: 0; padding: 10px; position: relative; border-radius:4px; padding-left:10px!important; font-size: 12px; }
                fieldset.scheduler-border { border: 1px groove #ddd !important; padding: 0 1px 10px 10px !important; margin: 0 0 5px 0 !important; -webkit-box-shadow:  0px 0px 0px 0px #000; box-shadow:  0px 0px 0px 0px #000; }
                
                legend.scheduler-border { font-size: 12px !important; font-weight: bold !important; text-align: left !important; width:auto; padding:0 10px; border-bottom:none; }
                .modal-body { max-height: calc(100vh - 150px); overflow-y: auto; }
                .upload-btn-wrapper { position: relative; overflow: hidden; display: inline-block; }
                .upload-btn-wrapper input[type=file] { font-size: 100px; position: absolute; left: 0; top: 0; opacity: 0; }
                .highlighted { background: #ff8c56; }
                .highlighted span { color: #fff; }
                span.email-ids { float: left; /* padding: 4px; */ border: 1px solid #ccc; margin-right: 5px; padding-left: 10px; padding-right: 10px; margin-bottom: 5px; background: #f5f5f5; padding-top: 3px; padding-bottom: 3px; border-radius: 5px; }
                span.cancel-email { border: 1px solid #ccc; width: 18px; display: block; float: right; text-align: center; margin-left: 10px; border-radius: 49%; height: 18px; line-height: 15px; margin-top: 1px;    cursor: pointer; }
                .col-sm-12.email-id-row { border: 1px solid #ccc; }
                .col-sm-12.email-id-row input { border: 0px; outline:0px; }
                span.to-input { display: block; float: left; padding-right: 11px; }
                .col-sm-12.email-id-row { padding-top: 6px; padding-bottom: 7px; margin-top: 23px; }
                .table-whithout-border td { border:0; }
                .chosen-container { width: 100% !important; }
                .chosen-search-input { width:100% !important; }
                .chosen-choices { border-radius: .2rem !important; border: 1px solid #ced4da !important; background-image:none !important; }
                .chosen-search-input { background: none !important; background-color: white !important; min-height: auto !important; }
                .overflow { overflow-y: hidden; }
                .thead-light tr th { padding:0 !important; margin:0 !important; }
                .btn-default { color: #333; background-color: #fff; border-color: #ccc; }
                .btn-xs { padding: 1px 5px; font-size: 10px; line-height: 1.5; border-radius: 3px; }
                .toggle-handle { margin-left: 0 !important; width: 40px !important; }
                .toggle.ios, .toggle-on.ios, .toggle-off.ios { border-radius: 20px; }
                .toggle.ios .toggle-handle { border-radius: 20px; }
                .inputpicker-div { width:100% !important; }
                .table.no-border td { border:0px !important; }
                .table.no-padding td { padding:0px !important; }
                .form-control-small { height:25px !important; min-height:auto !important; width:60px !important; }
                .form-control-smallw { width:60px !important; }
                .btn-nav-modal { width: 1.5rem; height: 1.5rem; border-radius: 12px; border: 1px solid #c5c5c5; margin: 1px; font-size: 0.8rem; padding: 0; line-height: 20px; color: #2e2e2e; background: transparent; }
                .fileRow { background-color: #f5f5f5; }
                .fileRow:nth-child(odd) { background-color: transparent; }
                .btn-custom{color:#fff !important;}
                .table-sm td{padding: 3px 5px 5px 0px !important;}
                h4.modal-title {font-size: 1.5rem;font-weight: 600;}
                .close {font-size: 1.5rem !important;font-weight: 700 !important;}
                .accordion .card {border-bottom: 1px solid rgba(0,0,0,.125) !important;}
                body .dateInput {width: 100% !important;}
                .simulate-disabled {background-color: rgb(236, 235, 234); border: 1px solid rgb(201, 199, 197); border-radius: .25rem; padding: 0 1rem 0 0.75rem; line-height: 1.875rem; width: 100%; display: inline-block;}
                .dropdown-menu > li > a {display: block; padding: 3px 20px; clear: both;font-weight: normal;line-height: 1.42857143;color: #333333;font-size:12px;}
                .dropdown {border: 1px solid #ced4da !important;}
                .dropdown-toggle {background-color: white;height: 28px;margin: 0 !important;}
                .accordion .card {overflow:visible !important;}
                .inputpicker-list-item {font-size:70%;padding:5px;}
                .inputpicker-list-item-sug {font-size:100%;padding:5px;}
                .table-inputpicker tr td {border-top: 1px solid #ddd;}
                .error-message {display: block;color:red;}
            </style>
        </head>
        <body style="background-color: rgba(84,105,141,.97);">
            <div class="slds-scope" style="height: 100%; padding: .75em;">
                <div class="slds-box slds-box_x-small slds-text-heading_medium slds-theme_default" style="font-weight: 700; margin-bottom: 0.5em;">
                    Inbound Process
                    <div class="message-style">
                        <apex:pageMessages />
                    </div>
                </div>
                <div class="slds-box slds-box_x-small slds-grid slds-theme_default"  style="margin-top: 0.5em; flex-direction: column;">
                    <div class="row">
                        <div class="col-md-12">
                            <div style="border-bottom:1px solid rgb(221, 219, 218);">
                                <h2 style="font-size: 20px;">Select Information</h2>
                            </div>
                        </div>
                    </div>
                    <apex:outputPanel id="messagePanel" layout="block" styleClass="row">
                        <div class="col-md-12">
                            <div class="alert alert-danger" role="alert" style="margin-bottom:0!important;{!IF(OR(batchStatus == 'Aborted',batchStatus == 'Extension Fail'),'','display:none;')}">
                                {!BatchStatusNew}
                            </div>
                            <div class="alert alert-success" role="alert" style="margin-bottom:0!important;{!IF(batchStatus == 'Completed','','display:none;')}">
                                {!BatchStatusNew}
                            </div>
                        </div>
                    </apex:outputPanel>
                    <apex:form >
                        <div class="row">
                            <div class="col-md-12"> 
                                <label style="font-weight:bold;">Service:</label>
                            </div>
                            <div class="col-md-2">
                                <apex:selectList size="1" styleClass="form-control form-control-sm" value="{!serviceSelected}">
                                    <apex:selectOptions value="{!services}" />
                                </apex:selectList>
                            </div>
                        </div>
                        <div class="row">
                            <div class="col-md-12">
                                <div class="float:left;">   
                                    <label style="font-weight:bold;">File:</label>
                                </div>
                                <div class="float:left;">
                                    <apex:inputFile value="{!contentFile1}" filename="{!nameFile}" style="padding-right: 50px;" accept="text/csv" contentType="text/csv" />
                                </div>
                            </div>
                            <div class="col-md-12">
                                <apex:commandButton action="{!ReadFile}" value="Upload File" style="margin-top: 2em;" styleClass="btn btn-danger" id="ProcessFile" disabled="{!IF(pollerBool==true,'true','')}" />
                            </div>
                        </div>
                    </apex:form>
                    <div class="row">
                        <div class="col-md-12">
                            <apex:form >
                                <apex:outputPanel rendered="{!batchStatusBool}" id="pg">
                                    <apex:actionStatus id="act" startText="" />
                                    <apex:actionPoller interval="15" action="{!checkBatchStatus}" enabled="{!pollerBool}" reRender="pg,ProcessFile,wBallLoading,messagePanel" status="act"/>
                                    <apex:outputPanel id="wBallLoading">
                                        <div id="contentLoading" class="loading" style="display:{!If(pollerBool==true,'block','none')}"></div>
                                    </apex:outputPanel>
                                </apex:outputPanel>
                            </apex:form>
                        </div>
                    </div>
                </div>
            </div>
        </body>
    </html>
</apex:page>```

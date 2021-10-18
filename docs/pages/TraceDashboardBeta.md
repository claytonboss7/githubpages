---
layout: default
title: TraceDashboardBeta
parent: pages
---

```<apex:page id="traceDashboard" lightningStylesheets="true" title="Trace Dashboard" standardController="Task" extensions="TraceDashboardControllerBeta"
  standardStylesheets="true" showHeader="false" sidebar="false" cache="false" applyBodyTag="false" applyHtmlTag="false" docType="html-5.0">
  <html xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" lang="en">

  <head>
    <meta charset="utf-8" />
    <meta http-equiv="x-ua-compatible" content="ie=edge" />
    <title>Trace Dashboard</title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap.min.css')}" />
    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/jquery.inputpicker.css')}" />
    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/chosen.css')}" />
    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap-toggle.min.css')}" />
    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/bootstrap-select.css')}" />
    <apex:stylesheet value="{!URLFOR($Resource.UltimateUtils, 'css/all.css')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery-3.3.1.min.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap.bundle.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap.min.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery.inputpicker.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/jquery.autocomplete.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/chosen.jquery.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap-toggle.min.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/ckeditor.js')}" />
    <apex:includeScript value="{!URLFOR($Resource.UltimateUtils, 'js/bootstrap-select.js')}" />
    <apex:includeScript value="{!$Resource.jquerydateFormat}" />
    <apex:slds />
    <style>
      .content {
        font-size: 12px;
        margin-left: 25px !important;
        margin-right: 25px !important;
      }

      .container {
        font-size: 12px;
      }

      .row {
        margin-top: 10px !important;
      }

      .dataCol {
        width: 25% !important;
      }

      html {
        height: 100%;
      }

      body {
        height: 100%;
      }

      body .pbSubsection {
        padding: 3.5px !important;
      }

      body .bPageBlock .detailList .labelCol {
        width: 25% !important;
      }

      body .bPageBlock .detailList .labelCol label {
        margin-top: 0.3rem;
      }

      body .dataCol select {
        margin-bottom: 0;
      }

      label {
        margin-bottom: 0.2rem;
      }

      /* lookup field override */

      .lookupInput {
        display: block !important;
        vertical-align: middle;
        white-space: nowrap;
      }

      .lookupInput img {
        background-repeat: no-repeat;
        margin-right: 0.25em;
        vertical-align: middle;
      }

      .lookupInput .disabled {
        background-color: #ccc;
      }

      .lookupInput .emptyDependentLookup {
        font-style: italic;
      }

      .lookupInput input[readonly] {
        background-color: #e6e6e6;
        border: 2px solid #e6e6e6;
        color: #333;
        cursor: default;
      }

      .lookupInput a.readOnly {
        float: right;
      }

      .lookupInput span.readOnly {
        display: block;
        white-space: normal;
      }

      .lookupInput span.totalSummary {
        font-weight: bold;
      }

      .inlineEditRequiredDiv .lookupInput img,
      .inlineEditDiv .lookupInput img {
        vertical-align: middle;
      }

      .quickCreateModule .lookupInput input {
        max-width: 155px;
      }

      .lookupIcon {
        background-image: url(/img/func_icons/util/lookup20.gif);
        background-position: 0 0;
        width: 20px;
        height: 20px;
        background-position: top left;
      }

      .lookupIconOn {
        background-image: url(/img/func_icons/util/lookup20.gif);
        background-position: 0 0;
        width: 20px;
        height: 20px;
        background-position: top right;
      }

      .lookupInput input {
        float: left;
      }

      .lookupInput a {
        width: 4%;
        border-left: none;
        position: absolute;
        right: 0px;
        border-bottom: none;
      }

      /** LOADING **/

      /* Absolute Center Spinner */

      .loading {
        position: fixed;
        z-index: 1051;
        height: 2em;
        width: 2em;
        overflow: show;
        margin: auto;
        top: 0;
        left: 0;
        bottom: 0;
        right: 0;
      }

      /* Transparent Overlay */

      .loading:before {
        content: "";
        display: block;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.3);
      }

      /* :not(:required) hides these rules from IE9 and below */

      .loading:not(:required) {
        /* hide "loading..." text */
        font: 0/0 a;
        color: transparent;
        text-shadow: none;
        background-color: transparent;
        border: 0;
      }

      .loading:not(:required):after {
        content: "";
        display: block;
        font-size: 10px;
        width: 1em;
        height: 1em;
        margin-top: -0.5em;
        -webkit-animation: spinner 1500ms infinite linear;
        -moz-animation: spinner 1500ms infinite linear;
        -ms-animation: spinner 1500ms infinite linear;
        -o-animation: spinner 1500ms infinite linear;
        animation: spinner 1500ms infinite linear;
        border-radius: 0.5em;
        -webkit-box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0,
        rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.5) -1.5em 0 0 0,
        rgba(0, 0, 0, 0.5) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0, rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0;
        box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0,
        rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) -1.5em 0 0 0,
        rgba(0, 0, 0, 0.75) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0,
        rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0;
      }

      /* Animation */

      @-webkit-keyframes spinner {
        0% {
          -webkit-transform: rotate(0deg);
          -moz-transform: rotate(0deg);
          -ms-transform: rotate(0deg);
          -o-transform: rotate(0deg);
          transform: rotate(0deg);
        }
        100% {
          -webkit-transform: rotate(360deg);
          -moz-transform: rotate(360deg);
          -ms-transform: rotate(360deg);
          -o-transform: rotate(360deg);
          transform: rotate(360deg);
        }
      }

      @-moz-keyframes spinner {
        0% {
          -webkit-transform: rotate(0deg);
          -moz-transform: rotate(0deg);
          -ms-transform: rotate(0deg);
          -o-transform: rotate(0deg);
          transform: rotate(0deg);
        }
        100% {
          -webkit-transform: rotate(360deg);
          -moz-transform: rotate(360deg);
          -ms-transform: rotate(360deg);
          -o-transform: rotate(360deg);
          transform: rotate(360deg);
        }
      }

      @-o-keyframes spinner {
        0% {
          -webkit-transform: rotate(0deg);
          -moz-transform: rotate(0deg);
          -ms-transform: rotate(0deg);
          -o-transform: rotate(0deg);
          transform: rotate(0deg);
        }
        100% {
          -webkit-transform: rotate(360deg);
          -moz-transform: rotate(360deg);
          -ms-transform: rotate(360deg);
          -o-transform: rotate(360deg);
          transform: rotate(360deg);
        }
      }

      @keyframes spinner {
        0% {
          -webkit-transform: rotate(0deg);
          -moz-transform: rotate(0deg);
          -ms-transform: rotate(0deg);
          -o-transform: rotate(0deg);
          transform: rotate(0deg);
        }
        100% {
          -webkit-transform: rotate(360deg);
          -moz-transform: rotate(360deg);
          -ms-transform: rotate(360deg);
          -o-transform: rotate(360deg);
          transform: rotate(360deg);
        }
      }

      /** END LOADING **/

      .autocomplete-suggestions {
        -webkit-box-sizing: border-box;
        -moz-box-sizing: border-box;
        box-sizing: border-box;
        border: 1px solid #999;
        background: #fff;
        cursor: default;
        overflow: auto;
        -webkit-box-shadow: 1px 4px 3px rgba(50, 50, 50, 0.64);
        -moz-box-shadow: 1px 4px 3px rgba(50, 50, 50, 0.64);
        box-shadow: 1px 4px 3px rgba(50, 50, 50, 0.64);
      }

      .autocomplete-suggestion {
        font-size: 12px;
        padding: 2px 5px;
        white-space: nowrap;
        overflow: hidden;
      }

      .autocomplete-no-suggestion {
        padding: 2px 5px;
      }

      .autocomplete-selected {
        background: #f0f0f0;
      }

      .autocomplete-suggestions strong {
        font-weight: bold;
        color: #000;
      }

      .autocomplete-group {
        padding: 2px 5px;
        font-weight: bold;
        font-size: 16px;
        color: #000;
        display: block;
        border-bottom: 1px solid #000;
      }

      .tableLight {
        font-size: 12px;
      }

      .tableLight thead th {
        background-color: rgb(250, 250, 249);
        text-transform: uppercase;
        font-weight: bold;
        color: rgb(81, 79, 77);
      }

      .tableLight .first {
        font-weight: bold;
        color: rgb(81, 79, 77);
      }

      .btnNew {
        color: #fff !important;
        background-color: #007bff !important;
        border-color: #007bff !important;
      }

      .pbBody {
        overflow: hidden !important;
      }

      .small {
        font-size: 70% !important;
      }

      .nav li a {
        font-size: 12px;
        padding: 0.5rem 4rem;
      }

      .tab-content {
        font-size: 12px;
        padding: 10px;
      }

      .btn-custom {
        font-size: 11px;
      }

      .btn-danger {
        font-weight: 400;
        color: #fff !important;
        background-color: #dc3545 !important;
        border-color: #dc3545 !important;
      }

      .messageCell h4 {
        text-align: left !important;
        font-size: 0.8125rem !important;
      }

      .table-custom td {
        padding: 0px 15px 5px 0px;
      }

      .error-custom {
        border-color: red !important;
      }

      .datePicker {
        z-index: 1051 !important;
      }

      .fieldset {
        border: 1px solid #ddd !important;
        margin: 15px 0 0 0;
        min-width: 0;
        padding: 10px;
        position: relative;
        border-radius: 4px;
        background-color: #f5f5f5;
        padding-left: 10px !important;
      }

      .group-custom {
        border: 1px solid #ddd !important;
        margin: 15px 0 0 0;
        min-width: 0;
        padding: 10px;
        position: relative;
        border-radius: 4px;
        padding-left: 10px !important;
        font-size: 12px;
      }

      fieldset.scheduler-border {
        border: 1px groove #ddd !important;
        padding: 0 1px 10px 10px !important;
        margin: 0 0 5px 0 !important;
        -webkit-box-shadow: 0px 0px 0px 0px #000;
        box-shadow: 0px 0px 0px 0px #000;
      }

      legend.scheduler-border {
        font-size: 12px !important;
        font-weight: bold !important;
        text-align: left !important;
        width: auto;
        padding: 0 10px;
        border-bottom: none;
      }

      .modal-body {
        max-height: calc(100vh - 150px);
        overflow-y: auto;
      }

      .upload-btn-wrapper {
        position: relative;
        overflow: hidden;
        display: inline-block;
      }

      .upload-btn-wrapper input[type="file"] {
        font-size: 100px;
        position: absolute;
        left: 0;
        top: 0;
        opacity: 0;
      }

      .highlighted {
        background: #ff8c56;
      }

      .highlighted span {
        color: #fff;
      }

      span.email-ids {
        float: left;
        /* padding: 4px; */
        border: 1px solid #ccc;
        margin-right: 5px;
        padding-left: 10px;
        padding-right: 10px;
        margin-bottom: 5px;
        background: #f5f5f5;
        padding-top: 3px;
        padding-bottom: 3px;
        border-radius: 5px;
      }

      span.cancel-email {
        border: 1px solid #ccc;
        width: 18px;
        display: block;
        float: right;
        text-align: center;
        margin-left: 10px;
        border-radius: 49%;
        height: 18px;
        line-height: 15px;
        margin-top: 1px;
        cursor: pointer;
      }

      .col-sm-12.email-id-row {
        border: 1px solid #ccc;
      }

      .col-sm-12.email-id-row input {
        border: 0px;
        outline: 0px;
      }

      span.to-input {
        display: block;
        float: left;
        padding-right: 11px;
      }

      .col-sm-12.email-id-row {
        padding-top: 6px;
        padding-bottom: 7px;
        margin-top: 23px;
      }

      .table-whithout-border td {
        border: 0;
      }

      .chosen-container {
        width: 100% !important;
      }

      .chosen-search-input {
        width: 100% !important;
      }

      .chosen-choices {
        border-radius: 0.2rem !important;
        border: 1px solid #ced4da !important;
        background-image: none !important;
      }

      .chosen-search-input {
        background: none !important;
        background-color: white !important;
        min-height: auto !important;
      }

      .overflow {
        overflow-y: hidden;
      }

      /*.thead-light tr th { padding:0 !important; margin:0 !important; }*/

      .btn-default {
        color: #333;
        background-color: #fff;
        border-color: #ccc;
      }

      .btn-xs {
        padding: 1px 5px;
        font-size: 10px;
        line-height: 1.5;
        border-radius: 3px;
      }

      .toggle-handle {
        margin-left: 0 !important;
        width: 40px !important;
      }

      .toggle.ios,
      .toggle-on.ios,
      .toggle-off.ios {
        border-radius: 20px;
      }

      .toggle.ios .toggle-handle {
        border-radius: 20px;
      }

      .inputpicker-div {
        width: 100% !important;
      }

      .table.no-border td {
        border: 0px !important;
      }

      .table.no-padding td {
        padding: 0px !important;
      }

      .form-control-small {
        height: 25px !important;
        min-height: auto !important;
        width: 60px !important;
      }

      .form-control-smallw {
        width: 60px !important;
      }

      .btn-nav-modal {
        width: 1.5rem;
        height: 1.5rem;
        border-radius: 12px;
        border: 1px solid #c5c5c5;
        margin: 1px;
        font-size: 0.8rem;
        padding: 0;
        line-height: 20px;
        color: #2e2e2e;
        background: transparent;
      }

      .fileRow {
        background-color: #f5f5f5;
      }

      .fileRow:nth-child(odd) {
        background-color: transparent;
      }

      .btn-custom {
        color: #fff !important;
      }

      /*.table-sm td{padding: 3px 5px 5px 0px !important;}*/

      h4.modal-title {
        font-size: 1.5rem;
        font-weight: 600;
      }

      .close {
        font-size: 1.5rem !important;
        font-weight: 700 !important;
      }

      .accordion .card {
        border-bottom: 1px solid rgba(0, 0, 0, 0.125) !important;
      }

      body .dateInput {
        width: 100% !important;
      }

      .simulate-disabled {
        background-color: rgb(236, 235, 234);
        border: 1px solid rgb(201, 199, 197);
        border-radius: 0.25rem;
        padding: 0 1rem 0 0.75rem;
        line-height: 1.875rem;
        width: 100%;
        display: inline-block;
      }

      .dropdown-menu>li>a {
        display: block;
        padding: 3px 20px;
        clear: both;
        font-weight: normal;
        line-height: 1.42857143;
        color: #333333;
        font-size: 12px;
      }

      .dropdown {
        border: 1px solid #ced4da !important;
      }

      .dropdown-toggle {
        background-color: white;
        height: 28px;
        margin: 0 !important;
      }

      .accordion .card {
        overflow: visible !important;
      }

      .inputpicker-list-item {
        font-size: 70%;
        padding: 5px;
      }

      .inputpicker-list-item-sug {
        font-size: 100%;
        padding: 5px;
      }

      .table-inputpicker tr td {
        border-top: 1px solid #ddd;
      }
    </style>
    <!-- 2 -->
    <style>
      /* Custom */

      .ctable td,
      .ctable th {
        padding: 0.3rem !important;
      }

      /* Other */

      .input-search {
        padding-right: 1.8rem !important;
      }

      .input-search-wrapper {
        display: inline-block;
        position: relative;
      }

      .input-search-wrapper:after {
        font-family: "Font Awesome\ 5 Free";
        font-weight: 900;
        content: "002";
        position: absolute;
        right: 0.5rem;
        top: 0.25rem;
        font-size: 1rem;
        color: #495057;
      }

      .tableResult .theadResult th {
        color: #495057;
        background-color: #e9ecef;
        border-color: #dee2e6;
      }

      .darkCard {
        background-color: #efefef;
      }

      .input-group-text {
        background-color: #ffffff;
      }

      /** LOADING SUB TAB **/

      /* Absolute Center Spinner */

      /*.loadingSubTab { position: absolute; z-index: 1051; height: 1em; width: 1em; margin: auto; top: 0; left: 0; bottom: 0; right: 0; }*/

      /* Transparent Overlay */

      .loadingSubTab:before {
        content: "";
        display: block;
        z-index: 1051;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.3);
      }

      /* :not(:required) hides these rules from IE9 and below */

      .loadingSubTabSpinner:not(:required) {
        /* hide "loading..." text */
        font: 0/0 a;
        width: 1em;
        height: 1em;
        margin: auto;
        color: transparent;
        text-shadow: none;
        background-color: transparent;
        border: 0;
      }

      .loadingSubTabSpinner:not(:required):after {
        content: "";
        display: block;
        font-size: 10px;
        width: 1em;
        height: 1em;
        margin-top: -0.5em;
        -webkit-animation: spinner 1500ms infinite linear;
        -moz-animation: spinner 1500ms infinite linear;
        -ms-animation: spinner 1500ms infinite linear;
        -o-animation: spinner 1500ms infinite linear;
        animation: spinner 1500ms infinite linear;
        border-radius: 0.5em;
        -webkit-box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0,
        rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.5) -1.5em 0 0 0,
        rgba(0, 0, 0, 0.5) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0, rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0;
        box-shadow: rgba(0, 0, 0, 0.75) 1.5em 0 0 0, rgba(0, 0, 0, 0.75) 1.1em 1.1em 0 0,
        rgba(0, 0, 0, 0.75) 0 1.5em 0 0, rgba(0, 0, 0, 0.75) -1.1em 1.1em 0 0, rgba(0, 0, 0, 0.75) -1.5em 0 0 0,
        rgba(0, 0, 0, 0.75) -1.1em -1.1em 0 0, rgba(0, 0, 0, 0.75) 0 -1.5em 0 0,
        rgba(0, 0, 0, 0.75) 1.1em -1.1em 0 0;
      }

      /** END LOADING **/
    </style>
  </head>

  <body>
    <div>
      <div id="contentLoading" class="loading" style="display: none"></div>
    </div>
    <div class="slds-scope" style="height: 100%; background-color: rgba(84, 105, 141, 0.97); overflow: auto; padding: 0.75em">
      <!-- Start Trace Dashboard -->
      <div class="slds-box slds-box_x-small slds-text-heading_medium slds-theme_default" style="font-weight: 700; margin-bottom: 0.5em">
        Trace Dashboard
        <div class="message-style">
          <apex:pageMessages />
        </div>
      </div>

      <!-- Start Search FORMs -->
      <apex:form id="theform" styleClass="theform">
        <div class="expand" style="margin-bottom: 0.5em">
          <div class="card" style="padding-bottom: 1em">

            <!--START SEARCH_INPUTS-->
            <div class="row p-2 mx-0 mb-3" style="/*align-items: flex-end;*/">
              <div class="col-md-6 px-2"></div>

              <!--Start searchAllCoordinators -->
              <div class="col-md-2 px-2">
                <apex:inputCheckbox value="{!searchInputs.searchAllCoordinators}" id="inputTraceSearchAllCoordinators" styleClass="inputTraceSearchAllCoordinators"
                  onchange="enableOrDisableFieldsFormByValue(this, false, 'formInputTraceSearchCoordinators');" />
                <label for="inputTraceSearchAllCoordinators">Select All Coordinators</label>
              </div>
              <!--End searchAllCoordinators -->

              <div class="col-md-2 px-2"></div>
              <!-- Start searchAllStatus -->
              <div class="col-md-2 px-2">
                <apex:inputCheckbox value="{!searchInputs.searchAllStatus}" id="inputTraceSearchAllStatus" styleClass="inputTraceSearchAllStatus"
                  onchange="enableOrDisableFieldsFormByValue(this, false, 'formInputTraceSearchStatus');" />
                <label for="inputTraceSearchAllStatus">Select All Status</label>
              </div>
              <!-- End searchAllStatus -->

              <!-- Start inputSearchStartDate -->
              <div class="w-100"></div>
              <div class="col-md-2 px-2">
                <label for="inputTraceSearchStartDate" class="font-weight-bold">From Date</label>
                <br />
                <apex:input type="date" id="inputTraceSearchStartDate" value="{!searchInputs.searchStartDate}" styleClass="form-control form-control-sm"
                  style="padding: 6px 12px" />
              </div>
              <!-- End inputSearchStartDate -->

              <!-- Start inputSearchEndDate -->
              <div class="col-md-2 px-2">
                <label for="inputTraceSearchEndDate" class="font-weight-bold">To Date</label>
                <br />
                <apex:input type="date" id="inputTraceSearchEndDate" value="{!searchInputs.searchEndDate}" styleClass="form-control form-control-sm"
                  style="padding: 6px 12px" />
              </div>
              <!-- End inputSearchEndDate -->

              <!-- Start Trace Coordinator -->
              <div class="col-md-2 px-2">
                <label for="inputTraceSearchSortBy" class="font-weight-bold">Sort by</label>
                <br />
                <apex:selectList id="inputTraceSearchSortBy" size="1" value="{!searchInputs.searchSortBy}" styleClass="form-control form-control-sm">
                  <apex:selectOption itemValue="By Status" itemLabel="By Status"></apex:selectOption>
                  <apex:selectOption itemValue="By Production" itemLabel="By Production"></apex:selectOption>
                  <apex:selectOption itemValue="By Company" itemLabel="By Company"></apex:selectOption>
                  <apex:selectOption itemValue="By City" itemLabel="By City"></apex:selectOption>
                  <apex:selectOption itemValue="By Date" itemLabel="By Date"></apex:selectOption>
                  <apex:selectOption itemValue="By Coordinator" itemLabel="By Coordinator"></apex:selectOption>
                  <apex:selectOption itemValue="By Vendor" itemLabel="By Vendor"></apex:selectOption>
                </apex:selectList>
              </div>
              <div class="col-md-2 px-2 formInputTraceSearchCoordinators">
                <fieldset>
                  <label for="inputTraceSearchCoordinator" class="font-weight-bold">Coordinator</label>
                  <br />
                  <apex:selectList value="{!searchInputs.searchCoordinator}" html-multiple="multiple" multiselect="true" size="1" styleClass="form-control form-control-sm chosen-multiselect inputTraceSearchCoordinator">
                    <apex:selectOptions value="{!searchInputs.searchCoordinatorPL}" />
                  </apex:selectList>
                </fieldset>
              </div>
              <!-- End Input Trace Coordinator -->

              <!-- Start Trace Type input -->
              <div class="col-md-2 px-2">
                <label for="inputTraceSearchTraceType" class="font-weight-bold">Trace Type</label>
                <br />
                <apex:selectList id="inputTraceSearchTraceType" size="1" value="{!searchInputs.searchTraceType}" styleClass="form-control form-control-sm inputTraceSearchTraceType">
                  <apex:selectOption itemValue="Trace Date" itemLabel="Trace Date"></apex:selectOption>
                  <apex:selectOption itemValue="DeadLine Date" itemLabel="DeadLine Date"></apex:selectOption>
                </apex:selectList>
              </div>
              <!-- End Trace Type input -->

              <!-- Start Trace status input -->
              <div class="col-md-2 px-2 formInputTraceSearchStatus">
                <fieldset>
                  <label for="inputTraceSearchStatus" class="font-weight-bold">Status</label>
                  <br />
                  <!-- MultiicklistPL -->
                  <apex:selectList value="{!searchInputs.searchStatus}" html-multiple="multiple" multiselect="true" size="1" styleClass="form-control form-control-sm chosen-multiselect inputTraceSearchStatus">
                    <apex:selectOptions value="{!searchInputs.searchStatusPL}" />
                  </apex:selectList>
                </fieldset>
              </div>
              <!-- End Trace Type input -->

              <!-- Start Trace service input -->
              <div class="w-100"></div>
              <div class="col-md-2 px-2">
                <label for="inputTraceSearchService" class="font-weight-bold">Service</label>
                <br />
                <!-- MPL -->
                <apex:selectList value="{!searchInputs.searchService}" html-multiple="multiple" multiselect="true" size="1" styleClass="form-control form-control-sm chosen-multiselect">
                  <apex:selectOption itemValue="Housing" itemLabel="Housing"></apex:selectOption>
                  <apex:selectOption itemValue="GT" itemLabel="GT"></apex:selectOption>
                  <apex:selectOption itemValue="Freight" itemLabel="Freight"></apex:selectOption>
                  <apex:selectOption itemValue="Air" itemLabel="Air"></apex:selectOption>
                </apex:selectList>
              </div>
              <!-- End Trace service input -->

              <!-- Start Trace service input -->
              <div class="col-md-1 px-2">
                <button type="button" class="btn btn-sm btn-primary btn-custom mt-3 btn-block" onclick="searchTraceInitial();">
                  Search
                </button>
              </div>
              <div class="col-md-1 px-2">
                <button type="button" class="btn btn-sm btn-primary btn-custom mt-3 btn-block" onclick="printTraceDashboard('{!searchInputs}');">
                  Print PDF
                </button>
              </div>
              <div class="col-md-3 px-2 pt-3">
                <apex:inputCheckbox value="{!searchInputs.searchUrgentTaskOnly}" id="searchUrgentTaskOnly" styleClass="" onchange="" />
                <label for="inputTraceSearchAllCoordinators">Urgent tasks only</label>
              </div>
              <!-- Start Trace service input -->
            </div>
            <!--END SEARCH INPUTS-->

            <!-- START SERVICE TRACES NOT INCLUDING ALL OTHER Tables -->
            <apex:outputPanel id="traceListContent" layout="block" styleClass="px-3">

              <!-- START HOUSING TRACES ALL (NOT OTHER) container -->
              <apex:outputPanel layout="block" rendered="{!IF(theJournals.lsJournals_Housing.size > 0 || taskWrappers.lsGroupsTWNoContract_Housing.size > 0 || taskWrappers.lsGroupsTW_Housing_AllOther.size > 0 || taskWrappers.lsGroupsTWContract_Housing.size > 0, true, false)}">
                <p class="text-center h5 font-weight-bold pb-2 pt-3">Housing Traces</p>

                <!-- Start Trace Type is DEADLINE DATE -->
                <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_Housing.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                  styleClass="card mb-3">
                  <div class="card-body card-header p-1">
                    <a class="btn btn-light btn-sm" href="#lsTraceDeadlineDate_Housing" data-toggle="collapse" role="button">
                      <i class="fas fa-arrows-alt-v"></i>
                    </a>
                    <span class="font-weight-bold">DeadLine Dates</span>
                  </div>
                  <div class="collapse show" id="lsTraceDeadlineDate_Housing">
                    <div class="card-body p-0">
                      <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                        <thead class="thead-light font-weight-bold">
                          <tr>
                            <th scope="col">
                              <a href="javascript:void(0);" style="color: #495057">
                                <span class="font-weight-bold" style="float: left">Status</span>
                              </a>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Production</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Stay City</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Company</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Deadline Date</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Trace Date</span>
                            </th>
                            <th scope="col" width="10%">
                              <span class="font-weight-bold" style="float: left">Trace Owner</span>
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_Housing}" var="t">
                            <tr>
                              <td>
                                <apex:outputLink value="/one/one.app#/alohaRedirect/apex/DashboardVFP?ServiceId={!t.taskId}" target="_blank">{!housingMapDeadlines[t.taskId].Status_CC__c}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputLink value="{!'/'+housingMapDeadlines[t.taskId].Production_CC__c}" target="_blank">{!housingMapDeadlines[t.taskId].Production_CC__r.Name}</apex:outputLink>
                              </td>
                              <td>{!housingMapDeadlines[t.taskId].City__r.Name}</td>
                              <td>
                                <apex:outputLink value="{!'/'+housingMapDeadlines[t.taskId].Production_CC__r.AccountId}" target="_blank">{!housingMapDeadlines[t.taskId].Production_CC__r.Account.Name}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadlineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadLineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <span class="show-data">{!t.coordinator}</span>
                              </td>
                            </tr>
                          </apex:repeat>
                        </tbody>
                      </table>
                    </div>
                  </div>
                </apex:outputPanel>
                <!-- End  Trace Type is DEADLINE DATE -->


                <!-- START Trace Type is Trace Date -->
                <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">

                  <!-- START Journals -->
                  <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_Housing.size > 0}" styleClass="card mb-3">
                    <div class="card-body card-header p-1">
                      <a class="btn btn-light btn-sm" href="#lsJournals_Housing" data-toggle="collapse" role="button">
                        <i class="fas fa-arrows-alt-v"></i>
                      </a>
                      <span class="font-weight-bold">Journals</span>
                    </div>
                    <div class="collapse show" id="lsJournals_Housing">
                      <div class="card-body p-0">
                        <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Follow Up / Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Journal Entry</span>
                              </th>
                              <th scope="col" width="15%">
                                <span class="font-weight-bold">Categories</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Created By</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Created On</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Coordinator</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!theJournals.lsJournals_Housing}" var="j">
                              <tr>
                                <td>
                                  <apex:outputLink value="{!'/'+j.id}" target="_blank">
                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                      <apex:param value="{!j.Trace_Date__c}" />
                                    </apex:outputText>
                                  </apex:outputLink>
                                </td>
                                <td>{!j.Journal_Entry__c}</td>
                                <td>
                                  <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Production: </span>
                                    <a href="#">{!j.Production__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                    <span class="font-weight-bold">Company: </span>
                                    <a href="#">{!rcom.Company__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                    <span class="font-weight-bold">Contact: </span>
                                    <a href="#">{!rcon.Contact__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Contract: </span>
                                    <a href="#">{!j.Bid__r.Contract_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                  <!-- id ? -->
                                  <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Bid: </span>
                                    <a href="#">{!j.Bid__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Stay: </span>
                                    <a href="#">{!j.Bid__r.Stay_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                </td>
                                <td>{!j.CreatedBy.Name}</td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!j.CreatedDate}" />
                                  </apex:outputText>
                                </td>
                                <td>{!j.Trace_Coordinator__r.Name}</td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                      </div>
                      <div class="card-footer p-1 text-center {!IF(theJournals.lsJournals_Housing.size != 10 || lsJournals_Housing_limit == 1000, 'd-none', '')}">
                        <button type="button" class="btn btn-sm btn-outline-primary" onclick="loadAllJournals_HousingJs();">
                          Show All
                          <i class="fas fa-chevron-down"></i>
                        </button>
                      </div>
                    </div>
                  </apex:outputPanel>
                  <!-- END   Journals -->

                  <!-- START Group Traces NO Contract List Housing -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_Housing.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">Housing Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllNoContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllNoContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_Housing}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#lsGroupsTWNoContract_Housing_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="lsGroupsTWNoContract_Housing_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="5%">
                                      <span class="font-weight-bold">Follow Up</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trace Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold"><a href="javascript:void(0);" style="color: #495057" onclick="sortTracesByCategoryJs('lsGroupsTWNoContract_Housing', '{!gls.groupTitle}', 'Check in date', '{!if(AND(gls.sortDir <> null, gls.sortDir == 'ASC'),'DESC','ASC')}')">
                                        <span>Check In Date</span>
                                        <i class="fas fa-sort-down" style="{!IF(AND(gls.sortField == 'Check in date',gls.sortDir == 'DESC'),'','display:none;')}"></i>
                                        <i class="fas fa-sort-up" style="{!IF(AND(gls.sortField == 'Check in date',gls.sortDir == 'ASC'),'','display:none;')}"></i>
                                        </a>
                                      </span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Check Out Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">City</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Deadline Date</span>
                                    <!-- option Date -->
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td class="text-center">
                                        <span
                                          class="{!IF(tw.priority == 'Normal Follow up', 'text-success', IF(tw.priority == 'Urgent Follow Up', 'text-danger', 'd-none'))}"
                                          ><i class="fas fa-flag"></i
                                        ></span>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/DashboardVFP?ServiceId={!tw.serviceId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.checkInDate}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.checkOutDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.city}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.deadlineDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                  <!-- END   Group Traces NO Contract List Housing -->

                  <!-- START Group Traces Contract List Housing -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWContract_Housing.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">All Contract Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWContract_Housing}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#gls_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="gls_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="5%">
                                    <span class="font-weight-bold">Follow Up</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Follow Up Date</span>
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">
                                        <a href="javascript:void(0);" style="color: #495057" onclick="sortTracesByCategoryJs('lsGroupsTWContract_Housing', '{!gls.groupTitle}', 'Check in date', '{!if(AND(gls.sortDir <> null, gls.sortDir == 'ASC'),'DESC','ASC')}')">
                                            <span>Check In Date</span>
                                            <i class="fas fa-sort-down" style="{!IF(AND(gls.sortField == 'Check in date',gls.sortDir == 'DESC'),'','display:none;')}"></i>
                                            <i class="fas fa-sort-up" style="{!IF(AND(gls.sortField == 'Check in date',gls.sortDir == 'ASC'),'','display:none;')}"></i>
                                         </a>
                                      </span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Check Out Date</span>
                                  </th>
                                  <th scope="col" width="13%">
                                    <span class="font-weight-bold">City</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Vendor</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td class="text-center">
                                      <span class="{!IF(tw.priority == 'Normal Follow up', 'text-success', IF(tw.priority == 'Urgent Follow Up', 'text-danger', 'd-none'))}">
                                        <i class="fas fa-flag"></i>
                                      </span>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/DashboardVFP?ContractBidId={!tw.bidId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.checkInDate}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.checkOutDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.city}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.vendorId}" target="_blank">{!tw.vendor}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                  <!-- END   Group Traces Contract List Housing -->

                </apex:outputPanel>
                <!-- END Trace Type is Trace Date -->

              </apex:outputPanel>
              <!-- END HOUSING TRACES ALL (NOT OTHER) container -->

              <!-- START GT TRACES ALL (NOT OTHER) -->
              <apex:outputPanel layout="block" rendered="{!IF(theJournals.lsJournals_GT.size > 0 || (taskWrappers.lsGroupsTWNoContract_GT.size > 0 || taskWrappers.lsGroupsTW_GT_AllOther.size > 0 && searchInputs.searchTraceType=='Trace Date'), true, false)}">
                <p class="text-center h5 font-weight-bold pb-2 pt-3">Ground Trace</p>
                <!-- Start DEADLINE DATE -->
                <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_GT.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                  styleClass="card mb-3">
                  <div class="card-body card-header p-1">
                    <a class="btn btn-light btn-sm" href="#lsTraceDeadlineDate_GT" data-toggle="collapse" role="button">
                      <i class="fas fa-arrows-alt-v"></i>
                    </a>
                    <span class="font-weight-bold">DeadLine Dates</span>
                  </div>
                  <div class="collapse show" id="lsTraceDeadlineDate_GT">
                    <div class="card-body p-0">
                      <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                        <thead class="thead-light font-weight-bold">
                          <tr>
                            <th scope="col">
                              <a href="javascript:void(0);" style="color: #495057">
                                <span class="font-weight-bold" style="float: left">Status</span>
                              </a>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Production</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Stay City</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Company</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Deadline Date</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Trace Date</span>
                            </th>
                            <th scope="col" width="10%">
                              <span class="font-weight-bold" style="float: left">Trace Owner</span>
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_GT}" var="t">
                            <tr>
                              <td>
                                <apex:outputLink value="/one/one.app#/alohaRedirect/apex/DashboardVFP?ServiceId={!t.taskId}" target="_blank">{!gtMapDeadlines[t.taskId].Status__c}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputLink value="{!'/'+gtMapDeadlines[t.taskId].Production_Ground__c}" target="_blank">{!gtMapDeadlines[t.taskId].Production_Ground__r.Name}</apex:outputLink>
                              </td>
                              <td>City Field</td>
                              <td>
                                <apex:outputLink value="{!'/'+gtMapDeadlines[t.taskId].Production_Ground__r.AccountId}" target="_blank">{!gtMapDeadlines[t.taskId].Production_Ground__r.Account.Name}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadlineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadLineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <span class="show-data">{!t.coordinator}</span>
                              </td>
                            </tr>
                          </apex:repeat>
                        </tbody>
                      </table>
                    </div>
                  </div>
                </apex:outputPanel>
                <!-- End DEADLINE DATE -->
                <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                  <!-- START - Journals -->
                  <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_GT.size > 0}" styleClass="card mb-3">
                    <div class="card-body card-header p-1">
                      <a class="btn btn-light btn-sm" href="#lsJournals_GT" data-toggle="collapse" role="button">
                        <i class="fas fa-arrows-alt-v"></i>
                      </a>
                      <span class="font-weight-bold">Journals</span>
                    </div>
                    <div class="collapse show" id="lsJournals_GT">
                      <div class="card-body p-0">
                        <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Follow Up / Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Journal Entry</span>
                              </th>
                              <th scope="col" width="15%">
                                <span class="font-weight-bold">Categories</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Created By</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Created On</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Coordinator</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!theJournals.lsJournals_GT}" var="j">
                              <tr>
                                <td>
                                  <apex:outputLink value="{!'/'+j.id}" target="_blank">
                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                      <apex:param value="{!j.Trace_Date__c}" />
                                    </apex:outputText>
                                  </apex:outputLink>
                                </td>
                                <td>{!j.Journal_Entry__c}</td>
                                <td>
                                  <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Production: </span>
                                    <a href="#">{!j.Production__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                    <span class="font-weight-bold">Company: </span>
                                    <a href="#">{!rcom.Company__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                    <span class="font-weight-bold">Contact: </span>
                                    <a href="#">{!rcon.Contact__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Contract: </span>
                                    <a href="#">{!j.Bid__r.Contract_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                  <!-- id ? -->
                                  <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Bid: </span>
                                    <a href="#">{!j.Bid__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Stay: </span>
                                    <a href="#">{!j.Bid__r.Stay_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                </td>
                                <td>{!j.CreatedBy.Name}</td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!j.CreatedDate}" />
                                  </apex:outputText>
                                </td>
                                <td>{!j.Trace_Coordinator__r.Name}</td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                      </div>
                      <div class="card-footer p-1 text-center {!IF(theJournals.lsJournals_GT.size != 10 || lsJournals_GT_limit == 1000, 'd-none', '')}">
                        <button type="button" class="btn btn-sm btn-outline-primary" onclick="loadAllJournals_GTJs();">
                          Show All
                          <i class="fas fa-chevron-down"></i>
                        </button>
                      </div>
                    </div>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Traces
                                                    <apex:outputPanel layout="block" rendered="{!lsTraces_GT.size > 0}" styleClass="card mb-3">
                                                        <div class="card-body card-header p-1">
                                                            <a class="btn btn-light btn-sm" href="#lsTraces_GT" data-toggle="collapse" role="button"><i class="fas fa-arrows-alt-v"></i></a><span class="font-weight-bold">Traces</span>
                                                        </div>
                                                        <div class="collapse show" id="lsTraces_GT">
                                                            <div class="card-body p-0">
                                                                <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px;">
                                                                    <thead class="thead-light font-weight-bold">
                                                                        <tr>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trace Date</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trip Start Date</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trip End Date</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Description</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">City</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Service Type</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Production</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Company</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Status</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Deadline Date</span>
                                                                            </th>
                                                                            <th scope="col" width="10%">
                                                                                <span class="font-weight-bold">Coordinator</span>
                                                                            </th>
                                                                        </tr>
                                                                    </thead>
                                                                    <tbody>
                                                                        <apex:repeat value="{!lsTraces_GT}" var="g">
                                                                            <tr>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!g.Trace_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!g.Start_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!g.End_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    {!g.Description__c}
                                                                                </td>
                                                                                <td>
                                                                                    {!g.Start_City__r.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!g.Service_Type__c}
                                                                                </td>
                                                                                <td>
                                                                                    {!g.Production_Ground__r.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!g.Production_Ground__r.Account.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!g.Status_Ground__c}
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!g.Deadline_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    {!proCoordinatorMap[g.Production_Ground__c]}
                                                                                </td>
                                                                            </tr>
                                                                        </apex:repeat>
                                                                    </tbody>
                                                                </table>
                                                            </div>
                                                        </div>
                                                    </apex:outputPanel>
                                                    <! END -->

                  <!-- START - Group Traces 1 GT -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_GT.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_GTJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_GT}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#lsGroupsTWNoContract_GT_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="lsGroupsTWNoContract_GT_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trace Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip End Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">City</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Service Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Deadline Date</span>
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/GTDashboard?ServiceId={!tw.serviceId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_gtfr}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.tripEndDate_gtfr}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.tripDescription_gtfr}</td>
                                    <td>{!tw.city}</td>
                                    <td>{!tw.tripServiceType_gtfr}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.deadlineDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Group Traces Contract List GT -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTW_GT_AllOther.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">All Contract Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTW_GT_AllOther}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#gls_gt_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="gls_gt_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="5%">
                                    <span class="font-weight-bold">Follow Up</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Follow Up Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col" width="15%">
                                    <span class="font-weight-bold">City</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Service Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Vendor</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td class="text-center">
                                      <span class="{!IF(tw.priority == 'Normal Follow up', 'text-success', IF(tw.priority == 'Urgent Follow Up', 'text-danger', 'd-none'))}">
                                        <i class="fas fa-flag"></i>
                                      </span>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/GTDashboard?ContractBidId={!tw.bidId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_gtfr}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>{!tw.tripDescription_gtfr}</td>
                                    <td>{!tw.city}</td>
                                    <td>{!tw.tripServiceType_gtfr}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.vendorId}" target="_blank">{!tw.vendor}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                </apex:outputPanel>
                <!-- END -->
              </apex:outputPanel>
              <!-- START GT TRACES ALL (NOT OTHER) -->

              <!-- START FREIGHT TRACES ALL (NOT OTHER) -->
              <apex:outputPanel id="traceListContentFreight" layout="block" rendered="{!IF(theJournals.lsJournals_Freight.size > 0 || (taskWrappers.lsGroupsTWNoContract_Freight.size > 0 && searchInputs.searchTraceType=='Trace Date') || (taskWrappers.lsGroupsTW_Freight_AllOther.size > 0 && searchInputs.searchTraceType=='Trace Date'), true, false)}">
                <p class="text-center h5 font-weight-bold pb-2 pt-3">Freight Trace</p>
                <!-- Start DEADLINE DATE -->
                <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_Freight.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                  styleClass="card mb-3">
                  <div class="card-body card-header p-1">
                    <a class="btn btn-light btn-sm" href="#lsTraceDeadlineDate_Freight" data-toggle="collapse" role="button">
                      <i class="fas fa-arrows-alt-v"></i>
                    </a>
                    <span class="font-weight-bold">DeadLine Dates</span>
                  </div>
                  <div class="collapse show" id="lsTraceDeadlineDate_Freight">
                    <div class="card-body p-0">
                      <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                        <thead class="thead-light font-weight-bold">
                          <tr>
                            <th scope="col">
                              <a href="javascript:void(0);" style="color: #495057">
                                <span class="font-weight-bold" style="float: left">Status</span>
                              </a>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Production</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Stay City</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Company</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Deadline Date</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Trace Date</span>
                            </th>
                            <th scope="col" width="10%">
                              <span class="font-weight-bold" style="float: left">Trace Owner</span>
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_Freight}" var="t">
                            <tr>
                              <td>
                                <apex:outputLink value="/one/one.app#/alohaRedirect/apex/DashboardVFP?ServiceId={!t.taskId}" target="_blank">{!freightMapDeadlines[t.taskId].Status__c}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputLink value="{!'/'+housingMapDeadlines[t.taskId].Production_CC__c}" target="_blank">{!freightMapDeadlines[t.taskId].Production__r.Name}</apex:outputLink>
                              </td>
                              <td>{!freightMapDeadlines[t.taskId].Start_City__r.Name}</td>
                              <td>
                                <apex:outputLink value="{!'/'+housingMapDeadlines[t.taskId].Production_CC__r.AccountId}" target="_blank">{!freightMapDeadlines[t.taskId].Production__r.Account.Name}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadlineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadLineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <span class="show-data">{!t.coordinator}</span>
                              </td>
                            </tr>
                          </apex:repeat>
                        </tbody>
                      </table>
                    </div>
                  </div>
                </apex:outputPanel>
                <!-- End DEADLINE DATE -->

                <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                  <!-- START - Journals -->
                  <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_Freight.size > 0}" styleClass="card mb-3">
                    <div class="card-body card-header p-1">
                      <a class="btn btn-light btn-sm" href="#lsJournals_Freight" data-toggle="collapse" role="button">
                        <i class="fas fa-arrows-alt-v"></i>
                      </a>
                      <span class="font-weight-bold">Journals</span>
                    </div>
                    <div class="collapse show" id="lsJournals_Freight">
                      <div class="card-body p-0">
                        <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Follow Up / Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Journal Entry</span>
                              </th>
                              <th scope="col" width="15%">
                                <span class="font-weight-bold">Categories</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Created By</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Created On</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Coordinator</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!theJournals.lsJournals_Freight}" var="j">
                              <tr>
                                <td>
                                  <apex:outputLink value="{!'/'+j.id}" target="_blank">
                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                      <apex:param value="{!j.Trace_Date__c}" />
                                    </apex:outputText>
                                  </apex:outputLink>
                                </td>
                                <td>{!j.Journal_Entry__c}</td>
                                <td>
                                  <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Production: </span>
                                    <a href="#">{!j.Production__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                    <span class="font-weight-bold">Company: </span>
                                    <a href="#">{!rcom.Company__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                    <span class="font-weight-bold">Contact: </span>
                                    <a href="#">{!rcon.Contact__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Contract: </span>
                                    <a href="#">{!j.Bid__r.Contract_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                  <!-- id ? -->
                                  <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Bid: </span>
                                    <a href="#">{!j.Bid__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Stay: </span>
                                    <a href="#">{!j.Bid__r.Stay_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                </td>
                                <td>{!j.CreatedBy.Name}</td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!j.CreatedDate}" />
                                  </apex:outputText>
                                </td>
                                <td>{!j.Trace_Coordinator__r.Name}</td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                      </div>
                      <div class="card-footer p-1 text-center {!IF(theJournals.lsJournals_Freight.size != 10 || lsJournals_Freight_limit == 1000, 'd-none', '')}">
                        <button type="button" class="btn btn-sm btn-outline-primary" onclick="loadAllJournals_FreightJs();">
                          Show All
                          <i class="fas fa-chevron-down"></i>
                        </button>
                      </div>
                    </div>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Traces
                                                    <apex:outputPanel layout="block" rendered="{!lsTraces_Freight.size > 0}" styleClass="card mb-3">
                                                        <div class="card-body card-header p-1">
                                                            <a class="btn btn-light btn-sm" href="#lsTraces_Freight" data-toggle="collapse" role="button"><i class="fas fa-arrows-alt-v"></i></a><span class="font-weight-bold">Traces</span>
                                                        </div>
                                                        <div class="collapse show" id="lsTraces_Freight">
                                                            <div class="card-body p-0">
                                                                <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px;">
                                                                    <thead class="thead-light font-weight-bold">
                                                                        <tr>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trace Date</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trip Start Date</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trip End Date</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Description</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">City</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Service Type</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Production</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Company</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Status</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Deadline Date</span>
                                                                            </th>
                                                                            <th scope="col" width="10%">
                                                                                <span class="font-weight-bold">Coordinator</span>
                                                                            </th>
                                                                        </tr>
                                                                    </thead>
                                                                    <tbody>
                                                                        <apex:repeat value="{!lsTraces_Freight}" var="f">
                                                                            <tr>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!f.Trace_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!f.Start_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!f.End_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    {!f.Description__c}
                                                                                </td>
                                                                                <td>
                                                                                    {!f.Start_City__r.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!f.Service_Type__c}
                                                                                </td>
                                                                                <td>
                                                                                    {!f.Production__r.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!f.Production__r.Account.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!f.Status__c}
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!f.Deadline_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    {!proCoordinatorMap[f.Production__c]}
                                                                                </td>
                                                                            </tr>
                                                                        </apex:repeat>
                                                                    </tbody>
                                                                </table>
                                                            </div>
                                                        </div>
                                                    </apex:outputPanel>
                                                    < END -->

                  <!-- START - Group Traces 1 Freight -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_Freight.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_GT_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_Freight}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#lsGroupsTWNoContract_Freight_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="lsGroupsTWNoContract_Freight_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trace Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip End Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">City</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Service Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Deadline Date</span>
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/FreightDashboard?ServiceId={!tw.serviceId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_gtfr}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.tripEndDate_gtfr}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.tripDescription_gtfr}</td>
                                    <td>{!tw.city}</td>
                                    <td>{!tw.tripServiceType_gtfr}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.deadlineDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Group Traces Contract List Freight -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWContract_Freight.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">All Contract Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWContract_Freight}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#gls_freight_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="gls_freight_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="5%">
                                    <span class="font-weight-bold">Follow Up</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Follow Up Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col" width="15%">
                                    <span class="font-weight-bold">City</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Service Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Vendor</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td class="text-center">
                                      <span class="{!IF(tw.priority == 'Normal Follow up', 'text-success', IF(tw.priority == 'Urgent Follow Up', 'text-danger', 'd-none'))}">
                                        <i class="fas fa-flag"></i>
                                      </span>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/FreightDashboard?ContractBidId={!tw.bidId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_gtfr}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>{!tw.tripDescription_gtfr}</td>
                                    <td>{!tw.city}</td>
                                    <td>{!tw.tripServiceType_gtfr}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.vendorId}" target="_blank">{!tw.vendor}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                </apex:outputPanel>
                <!-- END -->
              </apex:outputPanel>
              <!-- START FREIGHT TRACES ALL (NOT OTHER) -->

              <!-- START AIR TRACES ALL (NOT OTHER) -->
              <apex:outputPanel layout="block" rendered="{!IF(theJournals.lsJournals_Air.size > 0 || (taskWrappers.lsGroupsTWNoContract_Air.size > 0 || taskWrappers.lsGroupsTW_Air_AllOther.size > 0 && searchInputs.searchTraceType=='Trace Date'), true, false)}">
                <p class="text-center h5 font-weight-bold pb-2 pt-3">Air Trace</p>
                <!-- Start DEADLINE DATE -->
                <apex:outputPanel layout="block" rendered="{!IF(taskWrappers.lsTraceDeadlineDate_Air.size > 0 && searchInputs.searchTraceType=='DeadLine Date',true,false)}"
                  styleClass="card mb-3">
                  <div class="card-body card-header p-1">
                    <a class="btn btn-light btn-sm" href="#lsTraceDeadlineDate_Air" data-toggle="collapse" role="button">
                      <i class="fas fa-arrows-alt-v"></i>
                    </a>
                    <span class="font-weight-bold">DeadLine Dates</span>
                  </div>
                  <div class="collapse show" id="lsTraceDeadlineDate_Air">
                    <div class="card-body p-0">
                      <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                        <thead class="thead-light font-weight-bold">
                          <tr>
                            <th scope="col">
                              <a href="javascript:void(0);" style="color: #495057">
                                <span class="font-weight-bold" style="float: left">Status</span>
                              </a>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Production</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Stay City</span>
                            </th>
                            <th scope="col">
                              <span class="font-weight-bold" style="float: left">Company</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Deadline Date</span>
                            </th>
                            <th scope="col" width="8%">
                              <span class="font-weight-bold" style="float: left">Trace Date</span>
                            </th>
                            <th scope="col" width="10%">
                              <span class="font-weight-bold" style="float: left">Trace Owner</span>
                            </th>
                          </tr>
                        </thead>
                        <tbody>
                          <apex:repeat value="{!taskWrappers.lsTraceDeadlineDate_Air}" var="t">
                            <tr>
                              <td>
                                <apex:outputLink value="/one/one.app#/alohaRedirect/apex/DashboardVFP?ServiceId={!t.taskId}" target="_blank">{!airMapDeadlines[t.taskId].Status__c}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputLink value="{!'/'+airMapDeadlines[t.taskId].Production__c}" target="_blank">{!airMapDeadlines[t.taskId].Production__r.Name}</apex:outputLink>
                              </td>
                              <td>City Field</td>
                              <td>
                                <apex:outputLink value="{!'/'+airMapDeadlines[t.taskId].Production__r.AccountId}" target="_blank">{!airMapDeadlines[t.taskId].Production__r.Account.Name}</apex:outputLink>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadlineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                  <apex:param value="{!t.deadLineDate}" />
                                </apex:outputText>
                              </td>
                              <td>
                                <span class="show-data">{!t.coordinator}</span>
                              </td>
                            </tr>
                          </apex:repeat>
                        </tbody>
                      </table>
                    </div>
                  </div>
                </apex:outputPanel>
                <!-- End DEADLINE DATE -->

                <apex:outputPanel rendered="{!searchInputs.searchTraceType=='Trace Date'}">
                  <!-- START - Journals -->
                  <apex:outputPanel layout="block" rendered="{!theJournals.lsJournals_Air.size > 0}" styleClass="card mb-3">
                    <div class="card-body card-header p-1">
                      <a class="btn btn-light btn-sm" href="#lsJournals_Air" data-toggle="collapse" role="button">
                        <i class="fas fa-arrows-alt-v"></i>
                      </a>
                      <span class="font-weight-bold">Journals</span>
                    </div>
                    <div class="collapse show" id="lsJournals_Air">
                      <div class="card-body p-0">
                        <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Follow Up / Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Journal Entry</span>
                              </th>
                              <th scope="col" width="15%">
                                <span class="font-weight-bold">Categories</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Created By</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Created On</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Coordinator</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!theJournals.lsJournals_Air}" var="j">
                              <tr>
                                <td>
                                  <apex:outputLink value="{!'/'+j.id}" target="_blank">
                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                      <apex:param value="{!j.Trace_Date__c}" />
                                    </apex:outputText>
                                  </apex:outputLink>
                                </td>
                                <td>{!j.Journal_Entry__c}</td>
                                <td>
                                  <apex:outputText rendered="{!IF(j.Production__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Production: </span>
                                    <a href="#">{!j.Production__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:repeat value="{!j.Related_Companies__r}" var="rcom">
                                    <span class="font-weight-bold">Company: </span>
                                    <a href="#">{!rcom.Company__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:repeat value="{!j.Related_Contact__r}" var="rcon">
                                    <span class="font-weight-bold">Contact: </span>
                                    <a href="#">{!rcon.Contact__r.Name}</a>
                                    <br />
                                  </apex:repeat>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Contract_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Contract: </span>
                                    <a href="#">{!j.Bid__r.Contract_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                  <!-- id ? -->
                                  <apex:outputText rendered="{!IF(j.Bid__r.Name == null, false, true)}">
                                    <span class="font-weight-bold">Bid: </span>
                                    <a href="#">{!j.Bid__r.Name}</a>
                                    <br />
                                  </apex:outputText>
                                  <apex:outputText rendered="{!IF(j.Bid__r.Stay_ID__c == null, false, true)}">
                                    <span class="font-weight-bold">Stay: </span>
                                    <a href="#">{!j.Bid__r.Stay_ID__c}</a>
                                    <br />
                                  </apex:outputText>
                                </td>
                                <td>{!j.CreatedBy.Name}</td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!j.CreatedDate}" />
                                  </apex:outputText>
                                </td>
                                <td>{!j.Trace_Coordinator__r.Name}</td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                      </div>
                      <div class="card-footer p-1 text-center {!IF(theJournals.lsJournals_Air.size != 10 || lsJournals_Air_limit == 1000, 'd-none', '')}">
                        <button type="button" class="btn btn-sm btn-outline-primary" onclick="loadAllJournals_AirJs();">
                          Show All
                          <i class="fas fa-chevron-down"></i>
                        </button>
                      </div>
                    </div>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Traces
                                                    <apex:outputPanel layout="block" rendered="{!lsTraces_Air.size > 0}" styleClass="card mb-3">
                                                        <div class="card-body card-header p-1">
                                                            <a class="btn btn-light btn-sm" href="#lsTraces_Air" data-toggle="collapse" role="button"><i class="fas fa-arrows-alt-v"></i></a><span class="font-weight-bold">Traces</span>
                                                        </div>
                                                        <div class="collapse show" id="lsTraces_Air">
                                                            <div class="card-body p-0">
                                                                <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px;">
                                                                    <thead class="thead-light font-weight-bold">
                                                                        <tr>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trace Date</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trip Start Date</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Trip End Date</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Description</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Group Type</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Production</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Company</span>
                                                                            </th>
                                                                            <th scope="col">
                                                                                <span class="font-weight-bold">Status</span>
                                                                            </th>
                                                                            <th scope="col" width="8%">
                                                                                <span class="font-weight-bold">Decision Due Date</span>
                                                                            </th>
                                                                            <th scope="col" width="10%">
                                                                                <span class="font-weight-bold">Coordinator</span>
                                                                            </th>
                                                                        </tr>
                                                                    </thead>
                                                                    <tbody>
                                                                        <apex:repeat value="{!lsTraces_Air}" var="a">
                                                                            <tr>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!a.Trace_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!a.Departure_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!a.Arrival_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    {!a.Description__c}
                                                                                </td>
                                                                                <td>
                                                                                    {!a.Group_Type__c}
                                                                                </td>
                                                                                <td>
                                                                                    {!a.Production__r.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!a.Production__r.Account.Name}
                                                                                </td>
                                                                                <td>
                                                                                    {!a.Status__c}
                                                                                </td>
                                                                                <td>
                                                                                    <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                                                                        <apex:param value="{!a.Decision_Due_Date__c}" />
                                                                                    </apex:outputText>
                                                                                </td>
                                                                                <td>
                                                                                    {!proCoordinatorMap[a.Production__c]}
                                                                                </td>
                                                                            </tr>
                                                                        </apex:repeat>
                                                                    </tbody>
                                                                </table>
                                                            </div>
                                                        </div>
                                                    </apex:outputPanel>
                                                    <! END -->

                  <!-- START - Group Traces 1 Air -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTWNoContract_Air.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTWNoContract_Air}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#lsGroupsTWNoContract_Air_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="lsGroupsTWNoContract_Air_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trace Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip End Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Group Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Deadline Date</span>
                                  </th>
                                  <th scope="col" width="10%">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/AirDashboard?ServiceId={!tw.serviceId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_air}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.tripEndDate_air}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.tripDescription_air}</td>
                                    <td>{!tw.tripGroupType_air}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.deadlineDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                  <!-- END -->

                  <!-- START - Group Traces Contract List Air -->
                  <apex:outputPanel layout="block" rendered="{!taskWrappers.lsGroupsTW_Air_AllOther.size > 0}">
                    <apex:variable var="item_number" value="0" />
                    <!-- Init -->
                    <p class="pb-2">
                      <span class="font-weight-bold h6">All Contract Traces</span>
                      <button type="button" class="btn btn-sm btn-outline-primary {!IF(loadAllContractTraces_Housing_showBtn == false, 'd-none', '')}"
                        onclick="loadAllContractTraces_HousingJs();">
                        Show All
                        <i class="fas fa-chevron-down"></i>
                      </button>
                    </p>
                    <apex:repeat value="{!taskWrappers.lsGroupsTW_Air_AllOther}" var="gls">
                      <apex:variable var="item_number" value="{!VALUE(item_number) + 1}" />
                      <div class="card mb-3">
                        <div class="card-body card-header p-1">
                          <a class="btn btn-light btn-sm" href="#gls_air_{!item_number}" data-toggle="collapse" role="button">
                            <i class="fas fa-arrows-alt-v"></i>
                          </a>
                          <span class="font-weight-bold">{!gls.groupTitle} ({!gls.totalTasks})</span>
                        </div>
                        <div class="collapse show" id="gls_air_{!item_number}">
                          <div class="card-body p-0">
                            <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                              <thead class="thead-light font-weight-bold">
                                <tr>
                                  <th scope="col" width="5%">
                                    <span class="font-weight-bold">Urgent</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Follow Up Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip Start Date</span>
                                  </th>
                                  <th scope="col" width="8%">
                                    <span class="font-weight-bold">Trip End Date</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Description</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Group Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Trip Type</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Production</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Company</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Vendor</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Status</span>
                                  </th>
                                  <th scope="col">
                                    <span class="font-weight-bold">Coordinator</span>
                                  </th>
                                </tr>
                              </thead>
                              <tbody>
                                <apex:repeat value="{!gls.lsTasks}" var="tw">
                                  <tr>
                                    <td class="text-center">
                                      <span class="{!IF(tw.priority == 'Normal Follow up', 'text-success', IF(tw.priority == 'Urgent Follow Up', 'text-danger', 'd-none'))}">
                                        <i class="fas fa-flag"></i>
                                      </span>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}" styleClass="text-danger">
                                        <apex:param value="{!tw.followUpDate}" />
                                      </apex:outputText>
                                    </td>
                                    <td>
                                      <a href="/one/one.app#/alohaRedirect/apex/AirDashboard?ContractBidId={!tw.bidId}" target="_blank">
                                        <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                          <apex:param value="{!tw.tripStartDate_air}" />
                                        </apex:outputText>
                                      </a>
                                    </td>
                                    <td>
                                      <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                        <apex:param value="{!tw.tripEndDate_air}" />
                                      </apex:outputText>
                                    </td>
                                    <td>{!tw.tripDescription_air}</td>
                                    <td>{!tw.tripGroupType_air}</td>
                                    <td>{!tw.tripType_air}</td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.productionId}" target="_blank">{!tw.production}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.companiesId}" target="_blank">{!tw.companies}</apex:outputLink>
                                    </td>
                                    <td>
                                      <apex:outputLink value="{!'/'+tw.vendorId}" target="_blank">{!tw.vendor}</apex:outputLink>
                                    </td>
                                    <td>{!tw.status}</td>
                                    <td>{!tw.coordinator}</td>
                                  </tr>
                                </apex:repeat>
                              </tbody>
                            </table>
                          </div>
                        </div>
                      </div>
                    </apex:repeat>
                  </apex:outputPanel>
                </apex:outputPanel>
                <!-- END -->
              </apex:outputPanel>
              <!-- START AIR TRACES ALL (NOT OTHER) -->
              <!-- START ALL OTHER -->
              <apex:outputPanel >
                <apex:outputPanel layout="block" rendered="{!IF(lsTrace_AllOther.size > 0, true, false)}">
                  <p class="text-center h5 font-weight-bold pb-2 pt-3">All Other Traces</p>
                  <!-- START - Traces -->
                  <div class="card mb-3">
                    <!--<apex:outputPanel layout="block" rendered="{!lsTrace_AllOther.size > 0}" styleClass="card mb-3">-->
                    <div class="card-body card-header p-1">
                      <a class="btn btn-light btn-sm" href="#lsTrace_AllOther" data-toggle="collapse" role="button">
                        <i class="fas fa-arrows-alt-v"></i>
                      </a>
                      <span class="font-weight-bold">Traces</span>
                    </div>
                    <div class="collapse show" id="lsTrace_AllOther">
                      <div class="card-body p-0">
                        <table class="table table-sm table-bordered table-hover m-0 ctable" style="font-size: 12px">
                          <thead class="thead-light font-weight-bold">
                            <tr>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Trace Date</span>
                              </th>
                              <th scope="col">
                                <span class="font-weight-bold">Trace Subject</span>
                              </th>
                              <th scope="col" width="8%">
                                <span class="font-weight-bold">Deadline Date</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Trace Owner</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Assigned To</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Status</span>
                              </th>
                              <th scope="col" width="10%">
                                <span class="font-weight-bold">Action</span>
                              </th>
                            </tr>
                          </thead>
                          <tbody>
                            <apex:repeat value="{!lsTrace_AllOther}" var="t">
                              <tr>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!t.ActivityDate}" />
                                  </apex:outputText>
                                </td>
                                <td>
                                  <apex:outputPanel rendered="{!t.IsForCloseOut__c == true}">
                                    <a href="/one/one.app#/alohaRedirect/apex/DashboardVFP?ContractBidId={!t.Bid_Id__c}"
                                    target="_blank">{!t.Subject}</a>
                                </apex:outputPanel>
                                <apex:outputPanel rendered="{!t.subject=='Request to Resend Contract'}">
                                    <apex:outputLink value="/one/one.app#/alohaRedirect/apex/DashboardVFP?ContractBidId={!t.Bid_Id__c}"
                                    target="_blank">{!t.Subject}</apex:outputLink>
                                </apex:outputPanel>
                                <apex:outputPanel rendered="{!t.subject=='Lodging Itinerary Received in Community'}">
                                    <apex:outputLink value="/one/one.app#/alohaRedirect/apex/DashboardVFP?ServiceId={!t.Service_Id__c}"
                                    target="_blank">{!t.Subject}</apex:outputLink>
                                </apex:outputPanel>
                                <apex:outputPanel rendered="{!and(t.IsForCloseOut__c == false,t.Subject!='Request to Resend Contract',
                                                            t.Subject!='Lodging Itinerary Received in Community')}">
                                    <apex:outputLink value="{!'/'+t.WhatId}" target="_blank"
                                    >{!t.Subject}</apex:outputLink>
                                </apex:outputPanel>
                                </td>
                                <td>
                                  <apex:outputText value="{0, date, MM'/'dd'/'yyyy}">
                                    <apex:param value="{!t.Deadline_Date__c}" />
                                  </apex:outputText>
                                </td>
                                <td>
                                  <span class="show-data">{!t.CreatedBy.Name}</span>
                                </td>
                                <td>
                                  <span class="show-data">{!t.Owner.Name}</span>
                                </td>
                                <td>
                                  <span class="show-data">{!t.Status}</span>
                                </td>
                                <td>
                                  <button type="button" class="btn btn-sm btn-outline-primary" onclick="completeTraceJs('{!t.Id}');">
                                    Complete
                                  </button>
                                </td>
                              </tr>
                            </apex:repeat>
                          </tbody>
                        </table>
                      </div>
                      <div class="card-footer p-1 text-center {!IF(lsTrace_AllOther.size != 10 || lsTrace_AllOther_limit == 1000, 'd-none', '')}">
                        <button type="button" class="btn btn-sm btn-outline-primary" onclick="loadAllTrace_AllOtherJs();">
                          Show All
                          <i class="fas fa-chevron-down"></i>
                        </button>
                      </div>
                    </div>
                    <!--</apex:outputPanel>-->
                  </div>
                  <!-- END -->
                </apex:outputPanel>
              </apex:outputPanel>
              <!-- END ALL OTHER -->
            </apex:outputPanel>
            <!-- END  SERVICE  TRACES NOT INCLUDING ALL OTHER Tables -->
          </div>
        </div>

        <!-- actionFunctions -->
        <apex:actionStatus id="loading" onstart="loading(true)" onstop="loading(false)" />
        <apex:actionFunction name="searchTraceJs" action="{!searchTrace}" status="loading" reRender="traceListContent" oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="getEncodedSearchParametersJs" action="{!getEncodedSearchParameters}" status="loading" reRender="traceListContent" oncomplete="openTraceDashboardPDF('{!encodedSearchInputs}');">
        </apex:actionFunction>
        <apex:actionFunction name="sortTracesByCategoryJs" action="{!sortTracesByCategory}" status="loading" reRender="traceListContent" oncomplete="$('.chosen-multiselect').chosen();">
        	<apex:param assignTo="{!lsGroupName}" name="lsGroupName" value="" />
            <apex:param assignTo="{!groupTitle}" name="groupTitle" value="" />
            <apex:param assignTo="{!sortFieldName}" name="sortFieldName" value="Check in date" />
            <apex:param assignTo="{!sortDirection}" name="sortDirection" value="ASC" />
        </apex:actionFunction>
        <apex:actionFunction name="loadAllJournals_HousingJs" action="{!loadAllJournals_Housing}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllNoContractTraces_HousingJs" action="{!loadAllNoContractTraces_Housing}" status="loading"
          reRender="traceListContent" oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllContractTraces_HousingJs" action="{!loadAllContractTraces_Housing}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllContractTraces_GTJs" action="{!loadAllContractTraces_GT}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllJournals_GTJs" action="{!loadAllJournals_GT}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllJournals_FreightJs" action="{!loadAllJournals_Freight}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllJournals_AirJs" action="{!loadAllJournals_Air}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="loadAllTrace_AllOtherJs" action="{!loadAllTrace_AllOther}" status="loading" reRender="traceListContent"
          oncomplete="$('.chosen-multiselect').chosen();">
        </apex:actionFunction>
        <apex:actionFunction name="completeTraceJs" action="{!completeTrace}" status="loading" reRender="traceListContent" oncomplete="$('.chosen-multiselect').chosen();">
          <apex:param assignTo="{!traceToComplete}" name="traceToComplete" value="" />
        </apex:actionFunction>
      </apex:form>
      <!-- Start Search FORMs -->

    </div>
    <script>
      $(document).ready(function ($) {
        console.log("## TraceDashboard - call from ready!!!! ");

        //Chosen
        //set value for chosen
        //setValueToEle('cm_inputTraceSearchCoordinator', 'cm_val_inputTraceSearchCoordinator');

        //active chosen MPL
        $(".chosen-multiselect").chosen();
      });

      function loading(val) {
        if (val) document.getElementById("contentLoading").style.display = "block";
        else document.getElementById("contentLoading").style.display = "none";
      }
      
      function sortTabel(column, dir, tableName) {
        console.log(column + ' '+dir+'  ' + tableName);
      }
      
      function printTraceDashboard(searchParams) {
          if (
              $(".inputTraceSearchAllCoordinators").is(":checked") == false &&
              $(".inputTraceSearchCoordinator").val() == ""
          ) {
              confirm("Please select a coordinator");
              return;
          }
          
          if ($(".inputTraceSearchAllStatus").is(":checked") == false && $(".inputTraceSearchStatus").val() == "") {
              confirm("Please select a status");
              return;
          }
          getEncodedSearchParametersJs();
      }
      
      function openTraceDashboardPDF(encodedSearchParams) {
          window.open('/apex/PDF_TraceDashboardBeta?' + encodedSearchParams, '_blank');
      }

      function searchTraceInitial() {
        console.log("## searchTrace()");
        console.log("# inputTraceSearchAllCoordinators = " + $(".inputTraceSearchAllCoordinators").is(":checked"));
        console.log("# inputTraceSearchCoordinator = " + $(".inputTraceSearchCoordinator").val());

        //check required fields..
        if (
          $(".inputTraceSearchAllCoordinators").is(":checked") == false &&
          $(".inputTraceSearchCoordinator").val() == ""
        ) {
          confirm("Please select a coordinator");
          return;
        }

        if ($(".inputTraceSearchAllStatus").is(":checked") == false && $(".inputTraceSearchStatus").val() == "") {
          confirm("Please select a status");
          return;
        }
        searchTraceJs();
      }

      function setValueToEle(eleClassName, eleClassNameToSetValue) {
        console.log("## setValueToEle()");
        var v = $("." + eleClassName).val();
        $("." + eleClassNameToSetValue).val(v);
        console.log("# ....val() = " + $("." + eleClassNameToSetValue).val());
      }

      function enableOrDisableFieldsFormByValue(el, valToEnableFields, divClassNameToEnableOrDisable) {
        //call ex: showOrHideElementByRadio(this, 'Sold Out for a portion of stay', 'divNoBidAuxWhichDate');
        console.log("## enableOrDisableFieldsFormByValue()");
        //var v = el.value;
        var v = el.checked;

        console.log("# enableOrDisableFieldsFormByValue() - v = " + v);
        console.log("# enableOrDisableFieldsFormByValue() - valToEnableFields = " + valToEnableFields);
        console.log(
          "# enableOrDisableFieldsFormByValue() - divClassNameToEnableOrDisable = " + divClassNameToEnableOrDisable
        );

        //test
        console.log(
          "# TEST - VALOR DE MPL ANTES DE LIMPIAR = " +
          $("." + divClassNameToEnableOrDisable + " fieldset")
            .find(".chosen-multiselect")
            .val()
        );
        //end

        if (v == valToEnableFields) {
          /*$('.' + divClassNameToEnableOrDisable).find(':input').prop('disabled', false);
                    $('.' + divClassNameToEnableOrDisable).find(':checkbox, :radio').prop('disabled', false);*/

          $("." + divClassNameToEnableOrDisable + " fieldset").prop("disabled", false);

          $("." + divClassNameToEnableOrDisable + " fieldset")
            .find(".chosen-multiselect")
            .prop("disabled", false)
            .trigger("chosen:updated");
        } else {
          /*$('.' + divClassNameToEnableOrDisable).find(':input').prop('disabled', true);
                    $('.' + divClassNameToEnableOrDisable).find(':checkbox, :radio').prop('disabled', true);*/

          $("." + divClassNameToEnableOrDisable + " fieldset").prop("disabled", true);

          //$('.fieldset-disabled .chosen-multiselect').prop('disabled', true).trigger("chosen:updated");
          $("." + divClassNameToEnableOrDisable + " fieldset")
            .find(".chosen-multiselect")
            .prop("disabled", true)
            .trigger("chosen:updated");
        }
        //resetForm(divClassNameToEnableOrDisable);
      }
    </script>
  </body>

  </html>
</apex:page>```
